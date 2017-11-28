---
title: "Éléments internes de collection fiable et de gestionnaire d’état fiable Azure Service Fabric | Microsoft Docs"
description: "Présentation approfondie sur la conception et les concepts de collection fiable dans Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: d607449a16e886337ab1bd96213fbb4231124353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="100b7-103">Éléments internes de collection fiable et de gestionnaire d’état fiable Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="100b7-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="100b7-104">Ce document examine en profondeur le Gestionnaire d’état fiable et les Collections fiables pour comprendre comment les principaux composants fonctionnent en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="100b7-104">This document delves inside Reliable State Manager and Reliable Collections to see how core components work behind the scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="100b7-105">Ce document est en évolution.</span><span class="sxs-lookup"><span data-stu-id="100b7-105">This document is work in-progress.</span></span> <span data-ttu-id="100b7-106">Laissez des commentaires sur cet article pour nous faire des suggestions sur les sujets à explorer.</span><span class="sxs-lookup"><span data-stu-id="100b7-106">Add comments to this article to tell us what topic you would like to learn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="100b7-107">Modèle de persistance local : journal et point de contrôle</span><span class="sxs-lookup"><span data-stu-id="100b7-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="100b7-108">Le gestionnaire d’état fiable et les Collections fiables suivent un modèle de persistance appelé Journal et Point de contrôle.</span><span class="sxs-lookup"><span data-stu-id="100b7-108">The Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="100b7-109">Dans ce modèle, chaque changement d’état est d’abord enregistré sur le disque, puis appliqué dans la mémoire.</span><span class="sxs-lookup"><span data-stu-id="100b7-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="100b7-110">L’état complet proprement dit n’est conservé qu’occasionnellement (également appelé</span><span class="sxs-lookup"><span data-stu-id="100b7-110">The complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="100b7-111">Point de contrôle).</span><span class="sxs-lookup"><span data-stu-id="100b7-111">Checkpoint).</span></span>
<span data-ttu-id="100b7-112">L'avantage fourni est le suivant : les deltas sont transformés en écritures séquentielles en mode ajouter uniquement sur disque pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="100b7-112">The benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="100b7-113">Pour mieux comprendre le modèle de journal et de point de contrôle, penchons-nous d’abord sur le scénario de disque infini.</span><span class="sxs-lookup"><span data-stu-id="100b7-113">To better understand the Log and Checkpoint model, let’s first look at the infinite disk scenario.</span></span>
<span data-ttu-id="100b7-114">Le gestionnaire d’état fiable enregistre chaque opération avant qu’elle ne soit répliquée.</span><span class="sxs-lookup"><span data-stu-id="100b7-114">The Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="100b7-115">La journalisation permet aux Collections fiables d’appliquer l’opération uniquement dans la mémoire.</span><span class="sxs-lookup"><span data-stu-id="100b7-115">Logging allows the Reliable Collections to apply the operation only in memory.</span></span>
<span data-ttu-id="100b7-116">Dans la mesure où les journaux sont conservés, même lorsque le réplica échoue et doit être redémarré, le Gestionnaire d’état fiable possède suffisamment d’informations dans son journal pour recréer toutes les opérations perdues par le réplica.</span><span class="sxs-lookup"><span data-stu-id="100b7-116">Since logs are persisted, even when the replica fails and needs to be restarted, the Reliable State Manager has enough information in its log to replay all the operations the replica has lost.</span></span>
<span data-ttu-id="100b7-117">Étant donné que le disque est infini, les enregistrements du journal n’ont jamais besoin d’être supprimés, et la Collection fiable ne doit gérer que l’état en mémoire.</span><span class="sxs-lookup"><span data-stu-id="100b7-117">As the disk is infinite, log records never need to be removed and the Reliable Collection needs to manage only the in-memory state.</span></span>

<span data-ttu-id="100b7-118">Maintenant, examinons le scénario de disque limité.</span><span class="sxs-lookup"><span data-stu-id="100b7-118">Now let’s look at the finite disk scenario.</span></span>
<span data-ttu-id="100b7-119">À mesure que les journaux se remplissent, le gestionnaire d’état fiable manquera d’espace disque.</span><span class="sxs-lookup"><span data-stu-id="100b7-119">As log records accumulate, the Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="100b7-120">Avant que cela n’arrive, le gestionnaire d’état fiable doit tronquer son journal pour accueillir les enregistrements plus récents.</span><span class="sxs-lookup"><span data-stu-id="100b7-120">Before that happens, the Reliable State Manager needs to truncate its log to make room for the newer records.</span></span>
<span data-ttu-id="100b7-121">Le gestionnaire d’état fiable demande aux Collections fiables de contrôler leur état en mémoire sur disque.</span><span class="sxs-lookup"><span data-stu-id="100b7-121">Reliable State Manager requests the Reliable Collections to checkpoint their in-memory state to disk.</span></span>
<span data-ttu-id="100b7-122">À ce stade, les Collections fiables conservent leur état en mémoire.</span><span class="sxs-lookup"><span data-stu-id="100b7-122">At this point, the Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="100b7-123">Une fois que les Collections fiables ont terminé leur contrôle, le Gestionnaire d'état fiable peut tronquer le journal pour libérer de l'espace disque.</span><span class="sxs-lookup"><span data-stu-id="100b7-123">Once the Reliable Collections complete their checkpoints, the Reliable State Manager can truncate the log to free up disk space.</span></span>
<span data-ttu-id="100b7-124">Lorsque le réplica doit être redémarré, les Collections fiables récupèrent leur état contrôlé et le Gestionnaire d’état fiable récupère et lit tous les changements d’état qui se sont produits depuis le dernier point de contrôle.</span><span class="sxs-lookup"><span data-stu-id="100b7-124">When the replica needs to be restarted, Reliable Collections recover their checkpointed state, and the Reliable State Manager recovers and plays back all the state changes that occurred since the last checkpoint.</span></span>

<span data-ttu-id="100b7-125">Le point de contrôle améliore également les délais de récupération dans les cas courants.</span><span class="sxs-lookup"><span data-stu-id="100b7-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="100b7-126">Le journal contient toutes les opérations qui se sont produites depuis le dernier point de contrôle.</span><span class="sxs-lookup"><span data-stu-id="100b7-126">Log contains all operations that have happened since the last checkpoint.</span></span>
<span data-ttu-id="100b7-127">Par conséquent, il peut inclure plusieurs versions d’un élément. Par exemple, plusieurs valeurs pour une ligne donnée dans le dictionnaire fiable.</span><span class="sxs-lookup"><span data-stu-id="100b7-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="100b7-128">En revanche, la collection fiable ne contrôle que la dernière version de chaque valeur pour une clé.</span><span class="sxs-lookup"><span data-stu-id="100b7-128">In contrast, a Reliable Collection checkpoints only the latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="100b7-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="100b7-129">Next steps</span></span>
* [<span data-ttu-id="100b7-130">Transactions et verrous</span><span class="sxs-lookup"><span data-stu-id="100b7-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

