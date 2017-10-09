---
title: "aaaAzure mécanismes internes de gestionnaire d’état de Service Fabric fiable et Collection fiable | Documents Microsoft"
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
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="942d5-103">Éléments internes de collection fiable et de gestionnaire d’état fiable Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="942d5-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="942d5-104">Ce document examine dans toosee fiable Gestionnaire d’état et les Collections fiable de fonctionnement des composants principaux coulisses hello.</span><span class="sxs-lookup"><span data-stu-id="942d5-104">This document delves inside Reliable State Manager and Reliable Collections toosee how core components work behind hello scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="942d5-105">Ce document est en évolution.</span><span class="sxs-lookup"><span data-stu-id="942d5-105">This document is work in-progress.</span></span> <span data-ttu-id="942d5-106">Ajouter des commentaires toothis article tootell nous sujet que vous aimeriez toolearn plus en détail.</span><span class="sxs-lookup"><span data-stu-id="942d5-106">Add comments toothis article tootell us what topic you would like toolearn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="942d5-107">Modèle de persistance local : journal et point de contrôle</span><span class="sxs-lookup"><span data-stu-id="942d5-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="942d5-108">Hello fiable Gestionnaire d’état et les Collections fiable suivent un modèle de persistance qui est appelé point de contrôle et de journal.</span><span class="sxs-lookup"><span data-stu-id="942d5-108">hello Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="942d5-109">Dans ce modèle, chaque changement d’état est d’abord enregistré sur le disque, puis appliqué dans la mémoire.</span><span class="sxs-lookup"><span data-stu-id="942d5-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="942d5-110">Hello complète état lui-même est rendu persistant qu’occasionnellement (aussi appelé)</span><span class="sxs-lookup"><span data-stu-id="942d5-110">hello complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="942d5-111">Point de contrôle).</span><span class="sxs-lookup"><span data-stu-id="942d5-111">Checkpoint).</span></span>
<span data-ttu-id="942d5-112">avantages de Hello sont que les deltas sont transformées en séquentiel en mode append-only écritures sur disque pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="942d5-112">hello benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="942d5-113">toobetter comprendre hello journal et le modèle de point de contrôle, commençons par examiner au scénario de disque infinie hello.</span><span class="sxs-lookup"><span data-stu-id="942d5-113">toobetter understand hello Log and Checkpoint model, let’s first look at hello infinite disk scenario.</span></span>
<span data-ttu-id="942d5-114">Hello fiable Gestionnaire d’état enregistre chaque opération avant sa réplication.</span><span class="sxs-lookup"><span data-stu-id="942d5-114">hello Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="942d5-115">Journalisation permet hello Collections fiable tooapply hello uniquement en mémoire.</span><span class="sxs-lookup"><span data-stu-id="942d5-115">Logging allows hello Reliable Collections tooapply hello operation only in memory.</span></span>
<span data-ttu-id="942d5-116">Étant donné que les journaux sont conservées, même lorsque le réplica de hello échoue et qu’il doit toobe redémarré, hello fiable Gestionnaire d’état a suffisamment d’informations dans ses tooreplay journal toutes les opérations de hello a perdu le réplica de hello.</span><span class="sxs-lookup"><span data-stu-id="942d5-116">Since logs are persisted, even when hello replica fails and needs toobe restarted, hello Reliable State Manager has enough information in its log tooreplay all hello operations hello replica has lost.</span></span>
<span data-ttu-id="942d5-117">Comme disque de hello est infinie, les enregistrements de journal n’ont jamais besoin toobe supprimé et état de toomanage uniquement hello en mémoire doit hello Collection fiable.</span><span class="sxs-lookup"><span data-stu-id="942d5-117">As hello disk is infinite, log records never need toobe removed and hello Reliable Collection needs toomanage only hello in-memory state.</span></span>

<span data-ttu-id="942d5-118">Maintenant examinons le scénario de disque finie hello.</span><span class="sxs-lookup"><span data-stu-id="942d5-118">Now let’s look at hello finite disk scenario.</span></span>
<span data-ttu-id="942d5-119">Comme les enregistrements de journal s’accumulent, hello fiable Gestionnaire d’état manquiez d’espace disque.</span><span class="sxs-lookup"><span data-stu-id="942d5-119">As log records accumulate, hello Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="942d5-120">Avant cela, hello fiable Gestionnaire d’état doit tootruncate son espace de toomake de journal pour les enregistrements de nouveaux hello.</span><span class="sxs-lookup"><span data-stu-id="942d5-120">Before that happens, hello Reliable State Manager needs tootruncate its log toomake room for hello newer records.</span></span>
<span data-ttu-id="942d5-121">Des demandes du gestionnaire Reliable état hello Collections fiable toocheckpoint toodisk de leur état en mémoire.</span><span class="sxs-lookup"><span data-stu-id="942d5-121">Reliable State Manager requests hello Reliable Collections toocheckpoint their in-memory state toodisk.</span></span>
<span data-ttu-id="942d5-122">À ce stade, hello Collections fiable' serait conserver son état en mémoire.</span><span class="sxs-lookup"><span data-stu-id="942d5-122">At this point, hello Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="942d5-123">Une fois que les Collections fiable hello terminé leurs points de contrôle, hello fiable Gestionnaire d’état peut tronquer toofree de journal hello l’espace disque.</span><span class="sxs-lookup"><span data-stu-id="942d5-123">Once hello Reliable Collections complete their checkpoints, hello Reliable State Manager can truncate hello log toofree up disk space.</span></span>
<span data-ttu-id="942d5-124">Lorsque les besoins de réplica de hello toobe redémarré, Collections fiable récupérer leur état de point de contrôle et récupère hello Gestionnaire d’état fiable et lit toutes les modifications d’état hello qui se sont produites depuis le dernier point de contrôle hello.</span><span class="sxs-lookup"><span data-stu-id="942d5-124">When hello replica needs toobe restarted, Reliable Collections recover their checkpointed state, and hello Reliable State Manager recovers and plays back all hello state changes that occurred since hello last checkpoint.</span></span>

<span data-ttu-id="942d5-125">Le point de contrôle améliore également les délais de récupération dans les cas courants.</span><span class="sxs-lookup"><span data-stu-id="942d5-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="942d5-126">Journal contient toutes les opérations qui se sont produites depuis le dernier point de contrôle hello.</span><span class="sxs-lookup"><span data-stu-id="942d5-126">Log contains all operations that have happened since hello last checkpoint.</span></span>
<span data-ttu-id="942d5-127">Par conséquent, il peut inclure plusieurs versions d’un élément. Par exemple, plusieurs valeurs pour une ligne donnée dans le dictionnaire fiable.</span><span class="sxs-lookup"><span data-stu-id="942d5-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="942d5-128">En revanche, points de contrôle de la Collection fiable hello uniquement la version la plus récente de chaque valeur d’une clé.</span><span class="sxs-lookup"><span data-stu-id="942d5-128">In contrast, a Reliable Collection checkpoints only hello latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="942d5-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="942d5-129">Next steps</span></span>
* [<span data-ttu-id="942d5-130">Transactions et verrous</span><span class="sxs-lookup"><span data-stu-id="942d5-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

