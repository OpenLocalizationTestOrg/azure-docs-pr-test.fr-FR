---
title: "aaaIntroduction tooAzure stockage d’objets Blob | Documents Microsoft"
description: "Introduction tooAzure stockage d’objets Blob"
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
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a><span data-ttu-id="85eda-103">Stockage de tooBlob de présentation</span><span class="sxs-lookup"><span data-stu-id="85eda-103">Introduction tooBlob storage</span></span>

<span data-ttu-id="85eda-104">Stockage d’objets Blob Azure est un service pour le stockage de grandes quantités de données d’objet non structurées, telles que les données texte ou binaire, qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="85eda-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="85eda-105">Vous pouvez utiliser les données de tooexpose de stockage Blob publiquement toohello world ou les données d’application toostore en privé.</span><span class="sxs-lookup"><span data-stu-id="85eda-105">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span>

<span data-ttu-id="85eda-106">Voici quelques utilisations courantes du stockage d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="85eda-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="85eda-107">Service des images ou des documents directement tooa navigateur</span><span class="sxs-lookup"><span data-stu-id="85eda-107">Serving images or documents directly tooa browser</span></span>
* <span data-ttu-id="85eda-108">Stockage de fichiers pour un accès distribué</span><span class="sxs-lookup"><span data-stu-id="85eda-108">Storing files for distributed access</span></span>
* <span data-ttu-id="85eda-109">Diffusion en continu de vidéo et d’audio</span><span class="sxs-lookup"><span data-stu-id="85eda-109">Streaming video and audio</span></span>
* <span data-ttu-id="85eda-110">Stockage de données pour la sauvegarde et la restauration, la récupération d’urgence et l’archivage</span><span class="sxs-lookup"><span data-stu-id="85eda-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="85eda-111">Stockage des données pour l’analyse par un service local ou hébergé par Azure</span><span class="sxs-lookup"><span data-stu-id="85eda-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="85eda-112">Concepts du service BLOB</span><span class="sxs-lookup"><span data-stu-id="85eda-112">Blob service concepts</span></span>

<span data-ttu-id="85eda-113">Hello service Blob contient hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="85eda-113">hello Blob service contains hello following components:</span></span>

![Architecture d’objets blob](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="85eda-115">**Compte de stockage :** tous accéder tooAzure stockage s’effectue via un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="85eda-115">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="85eda-116">Ce compte de stockage peut être un **compte de stockage à usage général** ou un **compte de stockage d’objets blob** spécialisé pour le stockage d’objets/objets blob.</span><span class="sxs-lookup"><span data-stu-id="85eda-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="85eda-117">Pour plus d’informations, voir [À propos des comptes de stockage Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="85eda-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="85eda-118">**Conteneur :** un conteneur regroupe un ensemble d'objets blob.</span><span class="sxs-lookup"><span data-stu-id="85eda-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="85eda-119">Tous les objets blob doivent figurer dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="85eda-119">All blobs must be in a container.</span></span> <span data-ttu-id="85eda-120">Un compte peut contenir un nombre illimité de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="85eda-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="85eda-121">Un conteneur peut stocker un nombre illimité d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="85eda-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="85eda-122">Notez que ce nom de conteneur hello doit être en minuscule.</span><span class="sxs-lookup"><span data-stu-id="85eda-122">Note that hello container name must be lowercase.</span></span>

* <span data-ttu-id="85eda-123">**Objet blob :** fichier de tout type et de toute taille.</span><span class="sxs-lookup"><span data-stu-id="85eda-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="85eda-124">Azure Storage propose trois types d’objets blob : les objets blob de blocs, les objets blob d’ajouts et les objets blob de pages.</span><span class="sxs-lookup"><span data-stu-id="85eda-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="85eda-125">Les *objets blob de blocs* sont parfaits pour le stockage des fichiers texte ou binaires, tels que les documents et les fichiers multimédias.</span><span class="sxs-lookup"><span data-stu-id="85eda-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="85eda-126">*Ajouter des objets BLOB* sont similaires tooblock BLOB dans la mesure où ils sont composés de blocs, mais ils sont optimisés pour les opérations d’ajout, afin qu’ils soient utiles pour les scénarios de journalisation.</span><span class="sxs-lookup"><span data-stu-id="85eda-126">*Append blobs* are similar tooblock blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="85eda-127">Objet blob de blocs unique peut contenir des too50, 000 blocs de too100 Mo chacun, pour une taille totale de 4,75 To légèrement supérieur à (100 Mo X 50 000).</span><span class="sxs-lookup"><span data-stu-id="85eda-127">A single block blob can contain up too50,000 blocks of up too100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="85eda-128">Un objet blob d’ajout unique peut contenir des too50, 000 blocs de too4 Mo chacun, pour une taille totale de légèrement supérieur à 195 Go (4 Mo X 50 000).</span><span class="sxs-lookup"><span data-stu-id="85eda-128">A single append blob can contain up too50,000 blocks of up too4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="85eda-129">*Objets BLOB de pages* peut être jusqu'à to too1 taille et sont plus efficaces pour les opérations de lecture/écriture fréquentes.</span><span class="sxs-lookup"><span data-stu-id="85eda-129">*Page blobs* can be up too1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="85eda-130">Les machines virtuelles Azure utilisent les objets blob de pages comme disques de données et disques de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="85eda-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="85eda-131">Pour plus de détails sur l’affectation de noms aux conteneurs et objets blob, consultez [Affectation de noms et références aux conteneurs, objets blob et métadonnées](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="85eda-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="85eda-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="85eda-132">Next steps</span></span>

* [<span data-ttu-id="85eda-133">Créer un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="85eda-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="85eda-134">Prise en main du Stockage Blob avec .NET</span><span class="sxs-lookup"><span data-stu-id="85eda-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)