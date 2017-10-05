---
title: "Présentation du Stockage File d’attente Azure | Microsoft Docs"
description: "Présentation du Stockage File d’attente Azure"
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
ms.openlocfilehash: 4db7552a1b76c89151405c55c8682abbb5326bb6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-queues"></a><span data-ttu-id="02fab-103">Présentation des files d’attente</span><span class="sxs-lookup"><span data-stu-id="02fab-103">Introduction to Queues</span></span>

<span data-ttu-id="02fab-104">Les files d’attente de stockage Azure sont un service permettant de stocker un grand nombre de messages accessibles depuis n’importe où dans le monde via des appels authentifiés avec HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="02fab-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="02fab-105">Un simple message de file d’attente peut avoir une taille de 64 Ko et une file d’attente peut contenir des millions de messages, jusqu’à la limite de capacité totale d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="02fab-105">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="02fab-106">Utilisations courantes</span><span class="sxs-lookup"><span data-stu-id="02fab-106">Common uses</span></span>

<span data-ttu-id="02fab-107">Voici quelques utilisations courantes des files d’attente de stockage :</span><span class="sxs-lookup"><span data-stu-id="02fab-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="02fab-108">Création d'un journal des travaux en souffrance de travail à traiter de manière asynchrone</span><span class="sxs-lookup"><span data-stu-id="02fab-108">Creating a backlog of work to process asynchronously</span></span>
* <span data-ttu-id="02fab-109">Transmission de messages d’un rôle web Azure à un rôle de travail Azure</span><span class="sxs-lookup"><span data-stu-id="02fab-109">Passing messages from an Azure web role to an Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="02fab-110">Concepts du service File d’attente</span><span class="sxs-lookup"><span data-stu-id="02fab-110">Queue service concepts</span></span>

<span data-ttu-id="02fab-111">Le service de file d’attente contient les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="02fab-111">The Queue service contains the following components:</span></span>

![Concepts de File d’attente](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="02fab-113">**Format d’URL :** les files d’attente sont adressables à l’aide du format d’URL suivant :</span><span class="sxs-lookup"><span data-stu-id="02fab-113">**URL format:** Queues are addressable using the following URL format:</span></span>   
    <span data-ttu-id="02fab-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="02fab-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="02fab-115">L'URL suivante désigne une file d'attente du schéma :</span><span class="sxs-lookup"><span data-stu-id="02fab-115">The following URL addresses a queue in the diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="02fab-116">**Compte de stockage :** tous les accès au Stockage Azure s’effectuent via un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="02fab-116">**Storage account:** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="02fab-117">Pour plus d’informations sur la capacité du compte de stockage, consultez la page [Objectifs de performance et évolutivité du stockage Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="02fab-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="02fab-118">**File d’attente :** une file d’attente contient un ensemble de messages.</span><span class="sxs-lookup"><span data-stu-id="02fab-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="02fab-119">Tous les messages doivent être dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="02fab-119">All messages must be in a queue.</span></span> <span data-ttu-id="02fab-120">Notez que le nom de la file d’attente doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="02fab-120">Note that the queue name must be all lowercase.</span></span> <span data-ttu-id="02fab-121">Pour plus d'informations sur l’affectation de noms à des files d’attente, consultez [Affectation de noms pour les files d'attente et les métadonnées](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="02fab-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="02fab-122">**Message :** message dans n’importe quel format d’une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="02fab-122">**Message:** A message, in any format, of up to 64 KB.</span></span> <span data-ttu-id="02fab-123">La durée maximale pendant laquelle un message peut rester dans la file d’attente est de sept jours.</span><span class="sxs-lookup"><span data-stu-id="02fab-123">The maximum time that a message can remain in the queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02fab-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="02fab-124">Next steps</span></span>

* [<span data-ttu-id="02fab-125">Créer un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="02fab-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="02fab-126">Bien démarrer avec les files d’attente en utilisant .NET</span><span class="sxs-lookup"><span data-stu-id="02fab-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
