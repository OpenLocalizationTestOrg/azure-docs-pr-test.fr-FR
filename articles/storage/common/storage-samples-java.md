---
title: Exemples de stockage Azure avec Java| Microsoft Docs
description: "Affichez, téléchargez et exécutez des exemples de code et des applications pour Azure Storage. Découvrez des exemples de mise en route d’objets blob, de files d’attente, de tables et de fichiers à l’aide des bibliothèques clientes de stockage Java."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: fd27e1ac9a773e7b0f5245aa74acdb0521cd098c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="f0628-104">Exemples de stockage Azure avec Java</span><span class="sxs-lookup"><span data-stu-id="f0628-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="f0628-105">Index des exemples Java</span><span class="sxs-lookup"><span data-stu-id="f0628-105">Java sample index</span></span>

<span data-ttu-id="f0628-106">Le tableau suivant fournit une vue d’ensemble de notre référentiel d’exemples et des scénarios traités dans chaque exemple.</span><span class="sxs-lookup"><span data-stu-id="f0628-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="f0628-107">Cliquez sur les liens pour afficher l’exemple de code correspondant dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0628-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="f0628-108">Point de terminaison</span><span class="sxs-lookup"><span data-stu-id="f0628-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="f0628-109">Scénario</span><span class="sxs-lookup"><span data-stu-id="f0628-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="f0628-110">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="f0628-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="f0628-111"><b>Objet blob</b></span><span class="sxs-lookup"><span data-stu-id="f0628-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="f0628-112">Append Blob</span><span class="sxs-lookup"><span data-stu-id="f0628-112">Append Blob</span></span></td> 
<td><span data-ttu-id="f0628-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-114">Objet blob de blocs</span><span class="sxs-lookup"><span data-stu-id="f0628-114">Block Blob</span></span></td>
<td><span data-ttu-id="f0628-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f0628-116">Chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="f0628-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="f0628-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java (Prise en main du chiffrement côté client Azure dans Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f0628-118">Copie d'un objet blob</span><span class="sxs-lookup"><span data-stu-id="f0628-118">Copy Blob</span></span></td>
<td><span data-ttu-id="f0628-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f0628-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="f0628-120">Create Container</span></span></td>
<td><span data-ttu-id="f0628-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f0628-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="f0628-122">Delete Blob</span></span></td>
<td><span data-ttu-id="f0628-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f0628-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="f0628-124">Delete Container</span></span></td>
<td><span data-ttu-id="f0628-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f0628-126">Métadonnées/propriétés/statistiques des objets blob</span><span class="sxs-lookup"><span data-stu-id="f0628-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="f0628-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f0628-128">ACL/métadonnées/propriétés du conteneur</span><span class="sxs-lookup"><span data-stu-id="f0628-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="f0628-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f0628-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="f0628-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="f0628-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Exemple de tests d’objet blob de pages</a></span><span class="sxs-lookup"><span data-stu-id="f0628-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f0628-132">Objet blob/conteneur de bail</span><span class="sxs-lookup"><span data-stu-id="f0628-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="f0628-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f0628-134">Objet blob/conteneur de liste</span><span class="sxs-lookup"><span data-stu-id="f0628-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="f0628-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f0628-136">Objet blob de pages</span><span class="sxs-lookup"><span data-stu-id="f0628-136">Page Blob</span></span></td>
<td><span data-ttu-id="f0628-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="f0628-138">SAS</span><span class="sxs-lookup"><span data-stu-id="f0628-138">SAS</span></span></td>
<td><span data-ttu-id="f0628-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Exemple de tests SAS</a></span><span class="sxs-lookup"><span data-stu-id="f0628-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="f0628-140">Propriétés du service</span><span class="sxs-lookup"><span data-stu-id="f0628-140">Service Properties</span></span></td>
<td><span data-ttu-id="f0628-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="f0628-142">Snapshot Blob</span><span class="sxs-lookup"><span data-stu-id="f0628-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="f0628-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="f0628-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="f0628-144"><b>File</b></span></span></td>
<td><span data-ttu-id="f0628-145">Créer des partages/répertoires/fichiers</span><span class="sxs-lookup"><span data-stu-id="f0628-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="f0628-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="f0628-147">Créer des partages/répertoires/fichiers</span><span class="sxs-lookup"><span data-stu-id="f0628-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="f0628-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-149">Propriétés/métadonnées du répertoire</span><span class="sxs-lookup"><span data-stu-id="f0628-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="f0628-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-151">Télécharger des fichiers</span><span class="sxs-lookup"><span data-stu-id="f0628-151">Download Files</span></span></td> 
<td><span data-ttu-id="f0628-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-153">Propriétés/métadonnées/mesures de fichier</span><span class="sxs-lookup"><span data-stu-id="f0628-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="f0628-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-155">Propriétés du service de fichiers</span><span class="sxs-lookup"><span data-stu-id="f0628-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="f0628-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-157">Liste des répertoires et des fichiers</span><span class="sxs-lookup"><span data-stu-id="f0628-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="f0628-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="f0628-159">Partages de listes</span><span class="sxs-lookup"><span data-stu-id="f0628-159">List Shares</span></span></td> 
<td><span data-ttu-id="f0628-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="f0628-161">Propriétés/métadonnées/statistiques de partage</span><span class="sxs-lookup"><span data-stu-id="f0628-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="f0628-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="f0628-163"><b>File d'attente</b></span><span class="sxs-lookup"><span data-stu-id="f0628-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="f0628-164">Ajouter un message</span><span class="sxs-lookup"><span data-stu-id="f0628-164">Add Message</span></span></td> 
<td><span data-ttu-id="f0628-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-166">Chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="f0628-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="f0628-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-168">Créer des files d’attente</span><span class="sxs-lookup"><span data-stu-id="f0628-168">Create Queues</span></span></td> 
<td><span data-ttu-id="f0628-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-170">Supprimer le message/la file d’attente</span><span class="sxs-lookup"><span data-stu-id="f0628-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="f0628-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-172">Lire furtivement un message</span><span class="sxs-lookup"><span data-stu-id="f0628-172">Peek Message</span></span></td> 
<td><span data-ttu-id="f0628-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-174">ACL/métadonnées/statistiques de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="f0628-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="f0628-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-176">Propriétés du service de File d’attente</span><span class="sxs-lookup"><span data-stu-id="f0628-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="f0628-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-178">Mise à jour de message</span><span class="sxs-lookup"><span data-stu-id="f0628-178">Update Message</span></span></td> 
<td><span data-ttu-id="f0628-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="f0628-180"><b>Table</b></span><span class="sxs-lookup"><span data-stu-id="f0628-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="f0628-181">Créer une table</span><span class="sxs-lookup"><span data-stu-id="f0628-181">Create Table</span></span></td> 
<td><span data-ttu-id="f0628-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-183">Supprimer l’entité/la table</span><span class="sxs-lookup"><span data-stu-id="f0628-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="f0628-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-185">Insertion/fusion/remplacement d’entité</span><span class="sxs-lookup"><span data-stu-id="f0628-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="f0628-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="f0628-187">Query Entities</span></span></td> 
<td><span data-ttu-id="f0628-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-189">Tables de requête</span><span class="sxs-lookup"><span data-stu-id="f0628-189">Query Tables</span></span></td> 
<td><span data-ttu-id="f0628-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-191">ACL/propriétés de la table</span><span class="sxs-lookup"><span data-stu-id="f0628-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="f0628-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f0628-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="f0628-193">Update Entity</span></span></td> 
<td><span data-ttu-id="f0628-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="f0628-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="f0628-195">Bibliothèque d’exemples de code Azure</span><span class="sxs-lookup"><span data-stu-id="f0628-195">Azure Code Samples library</span></span>

<span data-ttu-id="f0628-196">Pour voir la bibliothèque complète des exemples, consultez la bibliothèque d’[exemples de code Azure](https://azure.microsoft.com/resources/samples/?service=storage) pour trouver des exemples de stockage Azure que vous pouvez télécharger et exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="f0628-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="f0628-197">Les exemples de code fournis par la bibliothèque sont au format .zip.</span><span class="sxs-lookup"><span data-stu-id="f0628-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="f0628-198">Vous pouvez également parcourir et cloner le dépôt GitHub pour chaque exemple.</span><span class="sxs-lookup"><span data-stu-id="f0628-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="f0628-199">Guides de prise en main</span><span class="sxs-lookup"><span data-stu-id="f0628-199">Getting started guides</span></span>

<span data-ttu-id="f0628-200">Consultez les guides suivants si vous recherchez des instructions sur l’installation et la prise en main des bibliothèques clientes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="f0628-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="f0628-201">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</span><span class="sxs-lookup"><span data-stu-id="f0628-201">Getting Started with Azure Blob Service in Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="f0628-202">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="f0628-202">Getting Started with Azure Queue Service in Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="f0628-203">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="f0628-203">Getting Started with Azure Table Service in Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="f0628-204">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="f0628-204">Getting Started with Azure File Service in Java</span></span>](../storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="f0628-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0628-205">Next steps</span></span>

<span data-ttu-id="f0628-206">Pour plus d’informations sur les exemples pour d’autres langages :</span><span class="sxs-lookup"><span data-stu-id="f0628-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="f0628-207">.NET : [exemples de stockage Azure avec .NET](../storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="f0628-207">.NET: [Azure Storage samples using .NET](../storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="f0628-208">Tous les autres langages : [exemples de stockage Azure](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="f0628-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
