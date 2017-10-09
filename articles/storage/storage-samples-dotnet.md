---
title: "exemples de stockage aaaAzure à l’aide de .NET | Documents Microsoft"
description: "Affichez, téléchargez et exécutez des exemples de code et des applications pour Azure Storage. Découvrez la prise en main des exemples pour les objets BLOB, les files d’attente, les tables et les fichiers, à l’aide de bibliothèques clientes de stockage de .NET hello."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 9a7055645b0f0658b850f024b8b19ab19840330e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="4eb6a-104">Exemples de stockage Azure avec .NET</span><span class="sxs-lookup"><span data-stu-id="4eb6a-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="4eb6a-105">Index des exemples .NET</span><span class="sxs-lookup"><span data-stu-id="4eb6a-105">.NET sample index</span></span>

<span data-ttu-id="4eb6a-106">Hello tableau suivant fournit une vue d’ensemble de nos exemples de scénarios de référentiel et hello couvertes dans chaque exemple.</span><span class="sxs-lookup"><span data-stu-id="4eb6a-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="4eb6a-107">Cliquez sur hello liens tooview hello exemple de code correspondant dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="4eb6a-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="4eb6a-108">Point de terminaison</span><span class="sxs-lookup"><span data-stu-id="4eb6a-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="4eb6a-109">Scénario</span><span class="sxs-lookup"><span data-stu-id="4eb6a-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="4eb6a-110">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="4eb6a-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="4eb6a-111"><b>Objet blob</b></span><span class="sxs-lookup"><span data-stu-id="4eb6a-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="4eb6a-112">Append Blob</span><span class="sxs-lookup"><span data-stu-id="4eb6a-112">Append Blob</span></span></td> 
<td><span data-ttu-id="4eb6a-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Exemple de méthode CloudBlobContainer.GetAppendBlobReference</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-114">Objet blob de blocs</span><span class="sxs-lookup"><span data-stu-id="4eb6a-114">Block Blob</span></span></td>
<td><span data-ttu-id="4eb6a-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Application web de la galerie photos d’Azure Blob Storage</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-116">Chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="4eb6a-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="4eb6a-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Exemples de chiffrement d’objets blob</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-118">Copie d'un objet blob</span><span class="sxs-lookup"><span data-stu-id="4eb6a-118">Copy Blob</span></span></td>
<td><span data-ttu-id="4eb6a-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="4eb6a-120">Create Container</span></span></td>
<td><span data-ttu-id="4eb6a-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Application web de la galerie photos d’Azure Blob Storage</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="4eb6a-122">Delete Blob</span></span></td>
<td><span data-ttu-id="4eb6a-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Application web de la galerie photos d’Azure Blob Storage</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="4eb6a-124">Delete Container</span></span></td>
<td><span data-ttu-id="4eb6a-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-126">Métadonnées/propriétés/statistiques des objets blob</span><span class="sxs-lookup"><span data-stu-id="4eb6a-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="4eb6a-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-128">ACL/métadonnées/propriétés du conteneur</span><span class="sxs-lookup"><span data-stu-id="4eb6a-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="4eb6a-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Application web de la galerie photos d’Azure Blob Storage</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="4eb6a-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="4eb6a-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-132">Objet blob/conteneur de bail</span><span class="sxs-lookup"><span data-stu-id="4eb6a-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="4eb6a-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-134">Objet blob/conteneur de liste</span><span class="sxs-lookup"><span data-stu-id="4eb6a-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="4eb6a-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-136">Objet blob de pages</span><span class="sxs-lookup"><span data-stu-id="4eb6a-136">Page Blob</span></span></td>
<td><span data-ttu-id="4eb6a-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="4eb6a-138">SAS</span><span class="sxs-lookup"><span data-stu-id="4eb6a-138">SAS</span></span></td>
<td><span data-ttu-id="4eb6a-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="4eb6a-140">Propriétés du service</span><span class="sxs-lookup"><span data-stu-id="4eb6a-140">Service Properties</span></span></td>
<td><span data-ttu-id="4eb6a-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="4eb6a-142">Snapshot Blob</span><span class="sxs-lookup"><span data-stu-id="4eb6a-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="4eb6a-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Sauvegarder des disques de machine virtuelle Azure avec des instantanés incrémentiels</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="4eb6a-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="4eb6a-144"><b>File</b></span></span></td>
<td><span data-ttu-id="4eb6a-145">Créer des partages/répertoires/fichiers</span><span class="sxs-lookup"><span data-stu-id="4eb6a-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="4eb6a-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="4eb6a-147">Créer des partages/répertoires/fichiers</span><span class="sxs-lookup"><span data-stu-id="4eb6a-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="4eb6a-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Prise en main du service de fichiers Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-149">Propriétés/métadonnées du répertoire</span><span class="sxs-lookup"><span data-stu-id="4eb6a-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="4eb6a-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-151">Télécharger des fichiers</span><span class="sxs-lookup"><span data-stu-id="4eb6a-151">Download Files</span></span></td> 
<td><span data-ttu-id="4eb6a-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-153">Propriétés/métadonnées/mesures de fichier</span><span class="sxs-lookup"><span data-stu-id="4eb6a-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="4eb6a-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-155">Propriétés du service de fichiers</span><span class="sxs-lookup"><span data-stu-id="4eb6a-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="4eb6a-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-157">Liste des répertoires et des fichiers</span><span class="sxs-lookup"><span data-stu-id="4eb6a-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="4eb6a-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="4eb6a-159">Partages de listes</span><span class="sxs-lookup"><span data-stu-id="4eb6a-159">List Shares</span></span></td> 
<td><span data-ttu-id="4eb6a-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="4eb6a-161">Propriétés/métadonnées/statistiques de partage</span><span class="sxs-lookup"><span data-stu-id="4eb6a-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="4eb6a-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="4eb6a-163"><b>File d'attente</b></span><span class="sxs-lookup"><span data-stu-id="4eb6a-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="4eb6a-164">Ajouter un message</span><span class="sxs-lookup"><span data-stu-id="4eb6a-164">Add Message</span></span></td> 
<td><span data-ttu-id="4eb6a-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-166">Chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="4eb6a-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="4eb6a-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Chiffrement côté client de la file d’attente .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-168">Créer des files d’attente</span><span class="sxs-lookup"><span data-stu-id="4eb6a-168">Create Queues</span></span></td> 
<td><span data-ttu-id="4eb6a-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-170">Supprimer le message/la file d’attente</span><span class="sxs-lookup"><span data-stu-id="4eb6a-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="4eb6a-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-172">Lire furtivement un message</span><span class="sxs-lookup"><span data-stu-id="4eb6a-172">Peek Message</span></span></td> 
<td><span data-ttu-id="4eb6a-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-174">ACL/métadonnées/statistiques de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="4eb6a-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="4eb6a-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-176">Propriétés du service de File d’attente</span><span class="sxs-lookup"><span data-stu-id="4eb6a-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="4eb6a-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-178">Mise à jour de message</span><span class="sxs-lookup"><span data-stu-id="4eb6a-178">Update Message</span></span></td> 
<td><span data-ttu-id="4eb6a-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="4eb6a-180"><b>Table</b></span><span class="sxs-lookup"><span data-stu-id="4eb6a-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="4eb6a-181">Créer une table</span><span class="sxs-lookup"><span data-stu-id="4eb6a-181">Create Table</span></span></td> 
<td><span data-ttu-id="4eb6a-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestion de l’accès concurrentiel avec Azure Storage - Exemple d’application</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-183">Supprimer l’entité/la table</span><span class="sxs-lookup"><span data-stu-id="4eb6a-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="4eb6a-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET (Prise en main de Stockage Table Azure dans .NET)</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-185">Insertion/fusion/remplacement d’entité</span><span class="sxs-lookup"><span data-stu-id="4eb6a-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="4eb6a-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestion de l’accès concurrentiel avec Azure Storage - Exemple d’application</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="4eb6a-187">Query Entities</span></span></td> 
<td><span data-ttu-id="4eb6a-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET (Prise en main de Stockage Table Azure dans .NET)</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-189">Tables de requête</span><span class="sxs-lookup"><span data-stu-id="4eb6a-189">Query Tables</span></span></td> 
<td><span data-ttu-id="4eb6a-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET (Prise en main de Stockage Table Azure dans .NET)</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-191">ACL/propriétés de la table</span><span class="sxs-lookup"><span data-stu-id="4eb6a-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="4eb6a-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET (Prise en main de Stockage Table Azure dans .NET)</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4eb6a-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="4eb6a-193">Update Entity</span></span></td> 
<td><span data-ttu-id="4eb6a-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestion de l’accès concurrentiel avec Azure Storage - Exemple d’application</a></span><span class="sxs-lookup"><span data-stu-id="4eb6a-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="4eb6a-195">Bibliothèque Exemples de code Azure</span><span class="sxs-lookup"><span data-stu-id="4eb6a-195">Azure Code Samples library</span></span>

<span data-ttu-id="4eb6a-196">bibliothèque d’exemple complet tooview hello, accédez toohello [exemples de Code Azure](https://azure.microsoft.com/resources/samples/?service=storage) library, qui comprend des exemples pour le stockage Azure que vous pouvez télécharger et exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="4eb6a-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="4eb6a-197">Hello, exemple de Code de bibliothèque fournit un exemple de code au format .zip.</span><span class="sxs-lookup"><span data-stu-id="4eb6a-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="4eb6a-198">Ou bien, vous pouvez parcourir et cloner le référentiel GitHub de hello pour chaque échantillon.</span><span class="sxs-lookup"><span data-stu-id="4eb6a-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="4eb6a-199">Guides de prise en main</span><span class="sxs-lookup"><span data-stu-id="4eb6a-199">Getting started guides</span></span>

<span data-ttu-id="4eb6a-200">Extraire hello suivant guides si vous recherchez des instructions sur la façon de tooinstall et prise en main hello bibliothèques clientes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="4eb6a-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="4eb6a-201">Prise en main du service BLOB Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="4eb6a-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="4eb6a-202">Prise en main du service de File d’attente Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="4eb6a-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="4eb6a-203">Prise en main du service de Table Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="4eb6a-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="4eb6a-204">Prise en main du service de fichiers Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="4eb6a-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="4eb6a-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4eb6a-205">Next steps</span></span>

<span data-ttu-id="4eb6a-206">Pour plus d’informations sur les exemples pour d’autres langages :</span><span class="sxs-lookup"><span data-stu-id="4eb6a-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="4eb6a-207">Java : [exemples de stockage Azure avec Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="4eb6a-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="4eb6a-208">Tous les autres langages : [exemples de stockage Azure](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="4eb6a-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
