---
title: Exemples de stockage Azure avec .NET| Microsoft Docs
description: "Affichez, téléchargez et exécutez des exemples de code et des applications pour Azure Storage. Découvrez la mise en route des exemples d’objets blob, de files d’attente, de tables et de fichiers qui utilisent des bibliothèques clientes de stockage .NET."
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
ms.openlocfilehash: d2b6b3d9483f230ad25ae47255a4f28c1a67e064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="f2893-104">Exemples de stockage Azure avec .NET</span><span class="sxs-lookup"><span data-stu-id="f2893-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="f2893-105">Index des exemples .NET</span><span class="sxs-lookup"><span data-stu-id="f2893-105">.NET sample index</span></span>

<span data-ttu-id="f2893-106">Le tableau suivant fournit une vue d’ensemble de notre référentiel d’exemples et des scénarios traités dans chaque exemple.</span><span class="sxs-lookup"><span data-stu-id="f2893-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="f2893-107">Cliquez sur les liens pour afficher l’exemple de code correspondant dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="f2893-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="f2893-108">Point de terminaison</span><span class="sxs-lookup"><span data-stu-id="f2893-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="f2893-109">Scénario</span><span class="sxs-lookup"><span data-stu-id="f2893-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="f2893-110">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="f2893-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="f2893-111"><b>Objet blob</b></span><span class="sxs-lookup"><span data-stu-id="f2893-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="f2893-112">Append Blob</span><span class="sxs-lookup"><span data-stu-id="f2893-112">Append Blob</span></span></td> 
<td><span data-ttu-id="f2893-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Exemple de méthode CloudBlobContainer.GetAppendBlobReference</a></span><span class="sxs-lookup"><span data-stu-id="f2893-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-114">Objet blob de blocs</span><span class="sxs-lookup"><span data-stu-id="f2893-114">Block Blob</span></span></td>
<td><span data-ttu-id="f2893-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Application web de la galerie photos d’Azure Blob Storage</a></span><span class="sxs-lookup"><span data-stu-id="f2893-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f2893-116">Chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="f2893-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="f2893-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Exemples de chiffrement d’objets blob</a></span><span class="sxs-lookup"><span data-stu-id="f2893-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f2893-118">Copie d'un objet blob</span><span class="sxs-lookup"><span data-stu-id="f2893-118">Copy Blob</span></span></td>
<td><span data-ttu-id="f2893-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="f2893-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f2893-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="f2893-120">Create Container</span></span></td>
<td><span data-ttu-id="f2893-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Application web de la galerie photos d’Azure Blob Storage</a></span><span class="sxs-lookup"><span data-stu-id="f2893-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f2893-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="f2893-122">Delete Blob</span></span></td>
<td><span data-ttu-id="f2893-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Application web de la galerie photos d’Azure Blob Storage</a></span><span class="sxs-lookup"><span data-stu-id="f2893-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f2893-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="f2893-124">Delete Container</span></span></td>
<td><span data-ttu-id="f2893-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="f2893-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f2893-126">Métadonnées/propriétés/statistiques des objets blob</span><span class="sxs-lookup"><span data-stu-id="f2893-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="f2893-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="f2893-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f2893-128">ACL/métadonnées/propriétés du conteneur</span><span class="sxs-lookup"><span data-stu-id="f2893-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="f2893-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Application web de la galerie photos d’Azure Blob Storage</a></span><span class="sxs-lookup"><span data-stu-id="f2893-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f2893-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="f2893-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="f2893-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="f2893-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f2893-132">Objet blob/conteneur de bail</span><span class="sxs-lookup"><span data-stu-id="f2893-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="f2893-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="f2893-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f2893-134">Objet blob/conteneur de liste</span><span class="sxs-lookup"><span data-stu-id="f2893-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="f2893-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="f2893-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f2893-136">Objet blob de pages</span><span class="sxs-lookup"><span data-stu-id="f2893-136">Page Blob</span></span></td>
<td><span data-ttu-id="f2893-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="f2893-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="f2893-138">SAS</span><span class="sxs-lookup"><span data-stu-id="f2893-138">SAS</span></span></td>
<td><span data-ttu-id="f2893-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="f2893-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="f2893-140">Propriétés du service</span><span class="sxs-lookup"><span data-stu-id="f2893-140">Service Properties</span></span></td>
<td><span data-ttu-id="f2893-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Prise en main des objets blob</a></span><span class="sxs-lookup"><span data-stu-id="f2893-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="f2893-142">Snapshot Blob</span><span class="sxs-lookup"><span data-stu-id="f2893-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="f2893-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Sauvegarder des disques de machine virtuelle Azure avec des instantanés incrémentiels</a></span><span class="sxs-lookup"><span data-stu-id="f2893-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="f2893-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="f2893-144"><b>File</b></span></span></td>
<td><span data-ttu-id="f2893-145">Créer des partages/répertoires/fichiers</span><span class="sxs-lookup"><span data-stu-id="f2893-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="f2893-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="f2893-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="f2893-147">Créer des partages/répertoires/fichiers</span><span class="sxs-lookup"><span data-stu-id="f2893-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="f2893-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Prise en main du service de fichiers Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="f2893-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-149">Propriétés/métadonnées du répertoire</span><span class="sxs-lookup"><span data-stu-id="f2893-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="f2893-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="f2893-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-151">Télécharger des fichiers</span><span class="sxs-lookup"><span data-stu-id="f2893-151">Download Files</span></span></td> 
<td><span data-ttu-id="f2893-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="f2893-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-153">Propriétés/métadonnées/mesures de fichier</span><span class="sxs-lookup"><span data-stu-id="f2893-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="f2893-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="f2893-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-155">Propriétés du service de fichiers</span><span class="sxs-lookup"><span data-stu-id="f2893-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="f2893-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="f2893-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-157">Liste des répertoires et des fichiers</span><span class="sxs-lookup"><span data-stu-id="f2893-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="f2893-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="f2893-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="f2893-159">Partages de listes</span><span class="sxs-lookup"><span data-stu-id="f2893-159">List Shares</span></span></td> 
<td><span data-ttu-id="f2893-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="f2893-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="f2893-161">Propriétés/métadonnées/statistiques de partage</span><span class="sxs-lookup"><span data-stu-id="f2893-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="f2893-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemple de stockage de fichier .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="f2893-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="f2893-163"><b>File d'attente</b></span><span class="sxs-lookup"><span data-stu-id="f2893-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="f2893-164">Ajouter un message</span><span class="sxs-lookup"><span data-stu-id="f2893-164">Add Message</span></span></td> 
<td><span data-ttu-id="f2893-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="f2893-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-166">Chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="f2893-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="f2893-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Chiffrement côté client de la file d’attente .NET Stockage Azure</a></span><span class="sxs-lookup"><span data-stu-id="f2893-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-168">Créer des files d’attente</span><span class="sxs-lookup"><span data-stu-id="f2893-168">Create Queues</span></span></td> 
<td><span data-ttu-id="f2893-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="f2893-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-170">Supprimer le message/la file d’attente</span><span class="sxs-lookup"><span data-stu-id="f2893-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="f2893-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="f2893-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-172">Lire furtivement un message</span><span class="sxs-lookup"><span data-stu-id="f2893-172">Peek Message</span></span></td> 
<td><span data-ttu-id="f2893-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="f2893-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-174">ACL/métadonnées/statistiques de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="f2893-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="f2893-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="f2893-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-176">Propriétés du service de File d’attente</span><span class="sxs-lookup"><span data-stu-id="f2893-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="f2893-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="f2893-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-178">Mise à jour de message</span><span class="sxs-lookup"><span data-stu-id="f2893-178">Update Message</span></span></td> 
<td><span data-ttu-id="f2893-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Prise en main du service de File d’attente Azure dans .NET</a></span><span class="sxs-lookup"><span data-stu-id="f2893-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="f2893-180"><b>Table</b></span><span class="sxs-lookup"><span data-stu-id="f2893-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="f2893-181">Créer une table</span><span class="sxs-lookup"><span data-stu-id="f2893-181">Create Table</span></span></td> 
<td><span data-ttu-id="f2893-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestion de l’accès concurrentiel avec Azure Storage - Exemple d’application</a></span><span class="sxs-lookup"><span data-stu-id="f2893-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-183">Supprimer l’entité/la table</span><span class="sxs-lookup"><span data-stu-id="f2893-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="f2893-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET (Prise en main de Stockage Table Azure dans .NET)</a></span><span class="sxs-lookup"><span data-stu-id="f2893-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-185">Insertion/fusion/remplacement d’entité</span><span class="sxs-lookup"><span data-stu-id="f2893-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="f2893-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestion de l’accès concurrentiel avec Azure Storage - Exemple d’application</a></span><span class="sxs-lookup"><span data-stu-id="f2893-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="f2893-187">Query Entities</span></span></td> 
<td><span data-ttu-id="f2893-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET (Prise en main de Stockage Table Azure dans .NET)</a></span><span class="sxs-lookup"><span data-stu-id="f2893-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-189">Tables de requête</span><span class="sxs-lookup"><span data-stu-id="f2893-189">Query Tables</span></span></td> 
<td><span data-ttu-id="f2893-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET (Prise en main de Stockage Table Azure dans .NET)</a></span><span class="sxs-lookup"><span data-stu-id="f2893-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-191">ACL/propriétés de la table</span><span class="sxs-lookup"><span data-stu-id="f2893-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="f2893-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET (Prise en main de Stockage Table Azure dans .NET)</a></span><span class="sxs-lookup"><span data-stu-id="f2893-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f2893-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="f2893-193">Update Entity</span></span></td> 
<td><span data-ttu-id="f2893-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestion de l’accès concurrentiel avec Azure Storage - Exemple d’application</a></span><span class="sxs-lookup"><span data-stu-id="f2893-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="f2893-195">Bibliothèque d’exemples de code Azure</span><span class="sxs-lookup"><span data-stu-id="f2893-195">Azure Code Samples library</span></span>

<span data-ttu-id="f2893-196">Pour voir la bibliothèque complète des exemples, consultez la bibliothèque d’[exemples de code Azure](https://azure.microsoft.com/resources/samples/?service=storage) pour trouver des exemples de stockage Azure que vous pouvez télécharger et exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="f2893-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="f2893-197">Les exemples de code fournis par la bibliothèque sont au format .zip.</span><span class="sxs-lookup"><span data-stu-id="f2893-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="f2893-198">Vous pouvez également parcourir et cloner le dépôt GitHub pour chaque exemple.</span><span class="sxs-lookup"><span data-stu-id="f2893-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="f2893-199">Guides de prise en main</span><span class="sxs-lookup"><span data-stu-id="f2893-199">Getting started guides</span></span>

<span data-ttu-id="f2893-200">Consultez les guides suivants si vous recherchez des instructions sur l’installation et la prise en main des bibliothèques clientes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="f2893-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="f2893-201">Prise en main du service BLOB Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="f2893-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="f2893-202">Prise en main du service de File d’attente Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="f2893-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="f2893-203">Prise en main du service de Table Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="f2893-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="f2893-204">Prise en main du service de fichiers Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="f2893-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="f2893-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f2893-205">Next steps</span></span>

<span data-ttu-id="f2893-206">Pour plus d’informations sur les exemples pour d’autres langages :</span><span class="sxs-lookup"><span data-stu-id="f2893-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="f2893-207">Java : [exemples de stockage Azure avec Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="f2893-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="f2893-208">Tous les autres langages : [exemples de stockage Azure](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="f2893-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
