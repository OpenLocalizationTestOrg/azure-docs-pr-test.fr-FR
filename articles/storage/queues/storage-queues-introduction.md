---
title: "aaaIntroduction tooAzure stockage de file d’attente | Documents Microsoft"
description: "Introduction tooAzure stockage de file d’attente"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a><span data-ttu-id="b08df-103">Introduction tooQueues</span><span class="sxs-lookup"><span data-stu-id="b08df-103">Introduction tooQueues</span></span>

<span data-ttu-id="b08df-104">Stockage de file d’attente Azure est un service pour stocker un grand nombre de messages qui sont accessibles à partir de n’importe où dans le monde hello via des appels authentifiés à l’aide de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b08df-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="b08df-105">Un message de la file d’attente unique peut être de taille too64 Ko, et une file d’attente peut contenir des millions de messages, des limites de capacité totale de toohello d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="b08df-105">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="b08df-106">Utilisations courantes</span><span class="sxs-lookup"><span data-stu-id="b08df-106">Common uses</span></span>

<span data-ttu-id="b08df-107">Voici quelques utilisations courantes des files d’attente de stockage :</span><span class="sxs-lookup"><span data-stu-id="b08df-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="b08df-108">Création d’une file d’attente de travail tooprocess asynchrone</span><span class="sxs-lookup"><span data-stu-id="b08df-108">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="b08df-109">Transmission de messages à partir d’un rôle de travail Azure tooan rôle web Azure</span><span class="sxs-lookup"><span data-stu-id="b08df-109">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="b08df-110">Concepts du service File d’attente</span><span class="sxs-lookup"><span data-stu-id="b08df-110">Queue service concepts</span></span>

<span data-ttu-id="b08df-111">Hello service file d’attente contient hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="b08df-111">hello Queue service contains hello following components:</span></span>

![Concepts de File d’attente](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="b08df-113">**Format d’URL :** files d’attente sont adressables hello suivant le format d’URL :</span><span class="sxs-lookup"><span data-stu-id="b08df-113">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="b08df-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="b08df-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="b08df-115">Hello suivant URL traite une file d’attente dans le diagramme de hello :</span><span class="sxs-lookup"><span data-stu-id="b08df-115">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="b08df-116">**Compte de stockage :** tous accéder tooAzure stockage s’effectue via un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="b08df-116">**Storage account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="b08df-117">Pour plus d’informations sur la capacité du compte de stockage, consultez la page [Objectifs de performance et évolutivité du stockage Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="b08df-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="b08df-118">**File d’attente :** une file d’attente contient un ensemble de messages.</span><span class="sxs-lookup"><span data-stu-id="b08df-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="b08df-119">Tous les messages doivent être dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="b08df-119">All messages must be in a queue.</span></span> <span data-ttu-id="b08df-120">Notez que ce nom de file d’attente hello doit être en minuscule.</span><span class="sxs-lookup"><span data-stu-id="b08df-120">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="b08df-121">Pour plus d'informations sur l’affectation de noms à des files d’attente, consultez [Affectation de noms pour les files d'attente et les métadonnées](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="b08df-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="b08df-122">**Message :** un message, dans n’importe quel format, des too64 Ko.</span><span class="sxs-lookup"><span data-stu-id="b08df-122">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="b08df-123">Hello durée maximale pendant laquelle un message peut rester dans la file d’attente hello est de sept jours.</span><span class="sxs-lookup"><span data-stu-id="b08df-123">hello maximum time that a message can remain in hello queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b08df-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b08df-124">Next steps</span></span>

* [<span data-ttu-id="b08df-125">Créer un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="b08df-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="b08df-126">Bien démarrer avec les files d’attente en utilisant .NET</span><span class="sxs-lookup"><span data-stu-id="b08df-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
