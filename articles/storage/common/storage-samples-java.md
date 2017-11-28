---
title: "exemples de stockage aaaAzure à l’aide de Java | Documents Microsoft"
description: "Affichez, téléchargez et exécutez des exemples de code et des applications pour Azure Storage. Découvrez la prise en main des exemples pour les objets BLOB, les files d’attente, les tables et les fichiers, à l’aide de bibliothèques clientes de stockage de Java hello."
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
ms.openlocfilehash: 6aec326cbfedc1166fc61037ac39d33c15d28d2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="6c6d9-104">Exemples de stockage Azure avec Java</span><span class="sxs-lookup"><span data-stu-id="6c6d9-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="6c6d9-105">Index des exemples Java</span><span class="sxs-lookup"><span data-stu-id="6c6d9-105">Java sample index</span></span>

<span data-ttu-id="6c6d9-106">Hello tableau suivant fournit une vue d’ensemble de nos exemples de scénarios de référentiel et hello couvertes dans chaque exemple.</span><span class="sxs-lookup"><span data-stu-id="6c6d9-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="6c6d9-107">Cliquez sur hello liens tooview hello exemple de code correspondant dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="6c6d9-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="6c6d9-108">Point de terminaison</span><span class="sxs-lookup"><span data-stu-id="6c6d9-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="6c6d9-109">Scénario</span><span class="sxs-lookup"><span data-stu-id="6c6d9-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="6c6d9-110">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="6c6d9-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="6c6d9-111"><b>Objet blob</b></span><span class="sxs-lookup"><span data-stu-id="6c6d9-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="6c6d9-112">Append Blob</span><span class="sxs-lookup"><span data-stu-id="6c6d9-112">Append Blob</span></span></td> 
<td><span data-ttu-id="6c6d9-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-114">Objet blob de blocs</span><span class="sxs-lookup"><span data-stu-id="6c6d9-114">Block Blob</span></span></td>
<td><span data-ttu-id="6c6d9-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-116">Chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="6c6d9-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="6c6d9-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java (Prise en main du chiffrement côté client Azure dans Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-118">Copie d'un objet blob</span><span class="sxs-lookup"><span data-stu-id="6c6d9-118">Copy Blob</span></span></td>
<td><span data-ttu-id="6c6d9-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="6c6d9-120">Create Container</span></span></td>
<td><span data-ttu-id="6c6d9-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="6c6d9-122">Delete Blob</span></span></td>
<td><span data-ttu-id="6c6d9-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="6c6d9-124">Delete Container</span></span></td>
<td><span data-ttu-id="6c6d9-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-126">Métadonnées/propriétés/statistiques des objets blob</span><span class="sxs-lookup"><span data-stu-id="6c6d9-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="6c6d9-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-128">ACL/métadonnées/propriétés du conteneur</span><span class="sxs-lookup"><span data-stu-id="6c6d9-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="6c6d9-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="6c6d9-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="6c6d9-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Exemple de tests d’objet blob de pages</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-132">Objet blob/conteneur de bail</span><span class="sxs-lookup"><span data-stu-id="6c6d9-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="6c6d9-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-134">Objet blob/conteneur de liste</span><span class="sxs-lookup"><span data-stu-id="6c6d9-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="6c6d9-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-136">Objet blob de pages</span><span class="sxs-lookup"><span data-stu-id="6c6d9-136">Page Blob</span></span></td>
<td><span data-ttu-id="6c6d9-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="6c6d9-138">SAS</span><span class="sxs-lookup"><span data-stu-id="6c6d9-138">SAS</span></span></td>
<td><span data-ttu-id="6c6d9-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Exemple de tests SAS</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="6c6d9-140">Propriétés du service</span><span class="sxs-lookup"><span data-stu-id="6c6d9-140">Service Properties</span></span></td>
<td><span data-ttu-id="6c6d9-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="6c6d9-142">Snapshot Blob</span><span class="sxs-lookup"><span data-stu-id="6c6d9-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="6c6d9-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="6c6d9-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="6c6d9-144"><b>File</b></span></span></td>
<td><span data-ttu-id="6c6d9-145">Créer des partages/répertoires/fichiers</span><span class="sxs-lookup"><span data-stu-id="6c6d9-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="6c6d9-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="6c6d9-147">Créer des partages/répertoires/fichiers</span><span class="sxs-lookup"><span data-stu-id="6c6d9-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="6c6d9-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-149">Propriétés/métadonnées du répertoire</span><span class="sxs-lookup"><span data-stu-id="6c6d9-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="6c6d9-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-151">Télécharger des fichiers</span><span class="sxs-lookup"><span data-stu-id="6c6d9-151">Download Files</span></span></td> 
<td><span data-ttu-id="6c6d9-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-153">Propriétés/métadonnées/mesures de fichier</span><span class="sxs-lookup"><span data-stu-id="6c6d9-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="6c6d9-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-155">Propriétés du service de fichiers</span><span class="sxs-lookup"><span data-stu-id="6c6d9-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="6c6d9-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-157">Liste des répertoires et des fichiers</span><span class="sxs-lookup"><span data-stu-id="6c6d9-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="6c6d9-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="6c6d9-159">Partages de listes</span><span class="sxs-lookup"><span data-stu-id="6c6d9-159">List Shares</span></span></td> 
<td><span data-ttu-id="6c6d9-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="6c6d9-161">Propriétés/métadonnées/statistiques de partage</span><span class="sxs-lookup"><span data-stu-id="6c6d9-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="6c6d9-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="6c6d9-163"><b>File d'attente</b></span><span class="sxs-lookup"><span data-stu-id="6c6d9-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="6c6d9-164">Ajouter un message</span><span class="sxs-lookup"><span data-stu-id="6c6d9-164">Add Message</span></span></td> 
<td><span data-ttu-id="6c6d9-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-166">Chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="6c6d9-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="6c6d9-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-168">Créer des files d’attente</span><span class="sxs-lookup"><span data-stu-id="6c6d9-168">Create Queues</span></span></td> 
<td><span data-ttu-id="6c6d9-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-170">Supprimer le message/la file d’attente</span><span class="sxs-lookup"><span data-stu-id="6c6d9-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="6c6d9-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-172">Lire furtivement un message</span><span class="sxs-lookup"><span data-stu-id="6c6d9-172">Peek Message</span></span></td> 
<td><span data-ttu-id="6c6d9-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-174">ACL/métadonnées/statistiques de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="6c6d9-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="6c6d9-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-176">Propriétés du service de File d’attente</span><span class="sxs-lookup"><span data-stu-id="6c6d9-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="6c6d9-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-178">Mise à jour de message</span><span class="sxs-lookup"><span data-stu-id="6c6d9-178">Update Message</span></span></td> 
<td><span data-ttu-id="6c6d9-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="6c6d9-180"><b>Table</b></span><span class="sxs-lookup"><span data-stu-id="6c6d9-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="6c6d9-181">Créer une table</span><span class="sxs-lookup"><span data-stu-id="6c6d9-181">Create Table</span></span></td> 
<td><span data-ttu-id="6c6d9-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-183">Supprimer l’entité/la table</span><span class="sxs-lookup"><span data-stu-id="6c6d9-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="6c6d9-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-185">Insertion/fusion/remplacement d’entité</span><span class="sxs-lookup"><span data-stu-id="6c6d9-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="6c6d9-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="6c6d9-187">Query Entities</span></span></td> 
<td><span data-ttu-id="6c6d9-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-189">Tables de requête</span><span class="sxs-lookup"><span data-stu-id="6c6d9-189">Query Tables</span></span></td> 
<td><span data-ttu-id="6c6d9-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-191">ACL/propriétés de la table</span><span class="sxs-lookup"><span data-stu-id="6c6d9-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="6c6d9-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="6c6d9-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="6c6d9-193">Update Entity</span></span></td> 
<td><span data-ttu-id="6c6d9-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="6c6d9-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="6c6d9-195">Bibliothèque Exemples de code Azure</span><span class="sxs-lookup"><span data-stu-id="6c6d9-195">Azure Code Samples library</span></span>

<span data-ttu-id="6c6d9-196">bibliothèque d’exemple complet tooview hello, accédez toohello [exemples de Code Azure](https://azure.microsoft.com/resources/samples/?service=storage) library, qui comprend des exemples pour le stockage Azure que vous pouvez télécharger et exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="6c6d9-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="6c6d9-197">Hello, exemple de Code de bibliothèque fournit un exemple de code au format .zip.</span><span class="sxs-lookup"><span data-stu-id="6c6d9-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="6c6d9-198">Ou bien, vous pouvez parcourir et cloner le référentiel GitHub de hello pour chaque échantillon.</span><span class="sxs-lookup"><span data-stu-id="6c6d9-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="6c6d9-199">Guides de prise en main</span><span class="sxs-lookup"><span data-stu-id="6c6d9-199">Getting started guides</span></span>

<span data-ttu-id="6c6d9-200">Extraire hello suivant guides si vous recherchez des instructions sur la façon de tooinstall et prise en main hello bibliothèques clientes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="6c6d9-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="6c6d9-201">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</span><span class="sxs-lookup"><span data-stu-id="6c6d9-201">Getting Started with Azure Blob Service in Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="6c6d9-202">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="6c6d9-202">Getting Started with Azure Queue Service in Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="6c6d9-203">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="6c6d9-203">Getting Started with Azure Table Service in Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="6c6d9-204">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="6c6d9-204">Getting Started with Azure File Service in Java</span></span>](../storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="6c6d9-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c6d9-205">Next steps</span></span>

<span data-ttu-id="6c6d9-206">Pour plus d’informations sur les exemples pour d’autres langages :</span><span class="sxs-lookup"><span data-stu-id="6c6d9-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="6c6d9-207">.NET : [exemples de stockage Azure avec .NET](../storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="6c6d9-207">.NET: [Azure Storage samples using .NET](../storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="6c6d9-208">Tous les autres langages : [exemples de stockage Azure](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="6c6d9-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
