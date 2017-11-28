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
ms.openlocfilehash: e3b8fbe86e82dd58c2a13a3c68760cbf6e9a6e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="70e54-104">Exemples de stockage Azure avec Java</span><span class="sxs-lookup"><span data-stu-id="70e54-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="70e54-105">Index des exemples Java</span><span class="sxs-lookup"><span data-stu-id="70e54-105">Java sample index</span></span>

<span data-ttu-id="70e54-106">Hello tableau suivant fournit une vue d’ensemble de nos exemples de scénarios de référentiel et hello couvertes dans chaque exemple.</span><span class="sxs-lookup"><span data-stu-id="70e54-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="70e54-107">Cliquez sur hello liens tooview hello exemple de code correspondant dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="70e54-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="70e54-108">Point de terminaison</span><span class="sxs-lookup"><span data-stu-id="70e54-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="70e54-109">Scénario</span><span class="sxs-lookup"><span data-stu-id="70e54-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="70e54-110">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="70e54-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="70e54-111"><b>Objet blob</b></span><span class="sxs-lookup"><span data-stu-id="70e54-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="70e54-112">Append Blob</span><span class="sxs-lookup"><span data-stu-id="70e54-112">Append Blob</span></span></td> 
<td><span data-ttu-id="70e54-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-114">Objet blob de blocs</span><span class="sxs-lookup"><span data-stu-id="70e54-114">Block Blob</span></span></td>
<td><span data-ttu-id="70e54-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="70e54-116">Chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="70e54-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="70e54-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java (Prise en main du chiffrement côté client Azure dans Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="70e54-118">Copie d'un objet blob</span><span class="sxs-lookup"><span data-stu-id="70e54-118">Copy Blob</span></span></td>
<td><span data-ttu-id="70e54-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="70e54-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="70e54-120">Create Container</span></span></td>
<td><span data-ttu-id="70e54-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="70e54-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="70e54-122">Delete Blob</span></span></td>
<td><span data-ttu-id="70e54-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="70e54-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="70e54-124">Delete Container</span></span></td>
<td><span data-ttu-id="70e54-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="70e54-126">Métadonnées/propriétés/statistiques des objets blob</span><span class="sxs-lookup"><span data-stu-id="70e54-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="70e54-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="70e54-128">ACL/métadonnées/propriétés du conteneur</span><span class="sxs-lookup"><span data-stu-id="70e54-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="70e54-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="70e54-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="70e54-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="70e54-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Exemple de tests d’objet blob de pages</a></span><span class="sxs-lookup"><span data-stu-id="70e54-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="70e54-132">Objet blob/conteneur de bail</span><span class="sxs-lookup"><span data-stu-id="70e54-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="70e54-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="70e54-134">Objet blob/conteneur de liste</span><span class="sxs-lookup"><span data-stu-id="70e54-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="70e54-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="70e54-136">Objet blob de pages</span><span class="sxs-lookup"><span data-stu-id="70e54-136">Page Blob</span></span></td>
<td><span data-ttu-id="70e54-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="70e54-138">SAS</span><span class="sxs-lookup"><span data-stu-id="70e54-138">SAS</span></span></td>
<td><span data-ttu-id="70e54-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Exemple de tests SAS</a></span><span class="sxs-lookup"><span data-stu-id="70e54-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="70e54-140">Propriétés du service</span><span class="sxs-lookup"><span data-stu-id="70e54-140">Service Properties</span></span></td>
<td><span data-ttu-id="70e54-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="70e54-142">Snapshot Blob</span><span class="sxs-lookup"><span data-stu-id="70e54-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="70e54-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="70e54-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="70e54-144"><b>File</b></span></span></td>
<td><span data-ttu-id="70e54-145">Créer des partages/répertoires/fichiers</span><span class="sxs-lookup"><span data-stu-id="70e54-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="70e54-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="70e54-147">Créer des partages/répertoires/fichiers</span><span class="sxs-lookup"><span data-stu-id="70e54-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="70e54-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-149">Propriétés/métadonnées du répertoire</span><span class="sxs-lookup"><span data-stu-id="70e54-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="70e54-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-151">Télécharger des fichiers</span><span class="sxs-lookup"><span data-stu-id="70e54-151">Download Files</span></span></td> 
<td><span data-ttu-id="70e54-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-153">Propriétés/métadonnées/mesures de fichier</span><span class="sxs-lookup"><span data-stu-id="70e54-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="70e54-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-155">Propriétés du service de fichiers</span><span class="sxs-lookup"><span data-stu-id="70e54-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="70e54-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-157">Liste des répertoires et des fichiers</span><span class="sxs-lookup"><span data-stu-id="70e54-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="70e54-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="70e54-159">Partages de listes</span><span class="sxs-lookup"><span data-stu-id="70e54-159">List Shares</span></span></td> 
<td><span data-ttu-id="70e54-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="70e54-161">Propriétés/métadonnées/statistiques de partage</span><span class="sxs-lookup"><span data-stu-id="70e54-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="70e54-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="70e54-163"><b>File d'attente</b></span><span class="sxs-lookup"><span data-stu-id="70e54-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="70e54-164">Ajouter un message</span><span class="sxs-lookup"><span data-stu-id="70e54-164">Add Message</span></span></td> 
<td><span data-ttu-id="70e54-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-166">Chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="70e54-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="70e54-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-168">Créer des files d’attente</span><span class="sxs-lookup"><span data-stu-id="70e54-168">Create Queues</span></span></td> 
<td><span data-ttu-id="70e54-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-170">Supprimer le message/la file d’attente</span><span class="sxs-lookup"><span data-stu-id="70e54-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="70e54-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-172">Lire furtivement un message</span><span class="sxs-lookup"><span data-stu-id="70e54-172">Peek Message</span></span></td> 
<td><span data-ttu-id="70e54-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-174">ACL/métadonnées/statistiques de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="70e54-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="70e54-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-176">Propriétés du service de File d’attente</span><span class="sxs-lookup"><span data-stu-id="70e54-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="70e54-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-178">Mise à jour de message</span><span class="sxs-lookup"><span data-stu-id="70e54-178">Update Message</span></span></td> 
<td><span data-ttu-id="70e54-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="70e54-180"><b>Table</b></span><span class="sxs-lookup"><span data-stu-id="70e54-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="70e54-181">Créer une table</span><span class="sxs-lookup"><span data-stu-id="70e54-181">Create Table</span></span></td> 
<td><span data-ttu-id="70e54-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-183">Supprimer l’entité/la table</span><span class="sxs-lookup"><span data-stu-id="70e54-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="70e54-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-185">Insertion/fusion/remplacement d’entité</span><span class="sxs-lookup"><span data-stu-id="70e54-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="70e54-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="70e54-187">Query Entities</span></span></td> 
<td><span data-ttu-id="70e54-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-189">Tables de requête</span><span class="sxs-lookup"><span data-stu-id="70e54-189">Query Tables</span></span></td> 
<td><span data-ttu-id="70e54-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-191">ACL/propriétés de la table</span><span class="sxs-lookup"><span data-stu-id="70e54-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="70e54-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="70e54-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="70e54-193">Update Entity</span></span></td> 
<td><span data-ttu-id="70e54-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></span><span class="sxs-lookup"><span data-stu-id="70e54-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="70e54-195">Bibliothèque Exemples de code Azure</span><span class="sxs-lookup"><span data-stu-id="70e54-195">Azure Code Samples library</span></span>

<span data-ttu-id="70e54-196">bibliothèque d’exemple complet tooview hello, accédez toohello [exemples de Code Azure](https://azure.microsoft.com/resources/samples/?service=storage) library, qui comprend des exemples pour le stockage Azure que vous pouvez télécharger et exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="70e54-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="70e54-197">Hello, exemple de Code de bibliothèque fournit un exemple de code au format .zip.</span><span class="sxs-lookup"><span data-stu-id="70e54-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="70e54-198">Ou bien, vous pouvez parcourir et cloner le référentiel GitHub de hello pour chaque échantillon.</span><span class="sxs-lookup"><span data-stu-id="70e54-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="70e54-199">Guides de prise en main</span><span class="sxs-lookup"><span data-stu-id="70e54-199">Getting started guides</span></span>

<span data-ttu-id="70e54-200">Extraire hello suivant guides si vous recherchez des instructions sur la façon de tooinstall et prise en main hello bibliothèques clientes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="70e54-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="70e54-201">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</span><span class="sxs-lookup"><span data-stu-id="70e54-201">Getting Started with Azure Blob Service in Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="70e54-202">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="70e54-202">Getting Started with Azure Queue Service in Java</span></span>](storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="70e54-203">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="70e54-203">Getting Started with Azure Table Service in Java</span></span>](storage-java-how-to-use-table-storage.md)
* [<span data-ttu-id="70e54-204">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</span><span class="sxs-lookup"><span data-stu-id="70e54-204">Getting Started with Azure File Service in Java</span></span>](storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="70e54-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="70e54-205">Next steps</span></span>

<span data-ttu-id="70e54-206">Pour plus d’informations sur les exemples pour d’autres langages :</span><span class="sxs-lookup"><span data-stu-id="70e54-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="70e54-207">.NET : [exemples de stockage Azure avec .NET](storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="70e54-207">.NET: [Azure Storage samples using .NET](storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="70e54-208">Tous les autres langages : [exemples de stockage Azure](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="70e54-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
