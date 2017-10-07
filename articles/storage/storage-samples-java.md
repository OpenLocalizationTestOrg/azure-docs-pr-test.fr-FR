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
# <a name="azure-storage-samples-using-java"></a>Exemples de stockage Azure avec Java

## <a name="java-sample-index"></a>Index des exemples Java

Hello tableau suivant fournit une vue d’ensemble de nos exemples de scénarios de référentiel et hello couvertes dans chaque exemple. Cliquez sur hello liens tooview hello exemple de code correspondant dans GitHub.

<table style="font-size:90%"><thead><tr><th style="font-size:110%">Point de terminaison</th><th style="font-size:110%">Scénario</th><th style="font-size:110%">Exemple de code</th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><b>Objet blob</b></td>
<td>Append Blob</td> 
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td> 
</tr> 
<tr> 
<td>Objet blob de blocs</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr> 
<tr> 
<td>Chiffrement côté client</td>
<td><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java (Prise en main du chiffrement côté client Azure dans Java)</a></td>
</tr> 
<tr> 
<td>Copie d'un objet blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr> 
<tr> 
<td>Create Container</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr> 
<tr> 
<td>Delete Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr> 
<tr> 
<td>Delete Container</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr> 
<tr> 
<td>Métadonnées/propriétés/statistiques des objets blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr> 
<tr> 
<td>ACL/métadonnées/propriétés du conteneur</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr> 
<tr> 
<td>Get Page Ranges</td>
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Exemple de tests d’objet blob de pages</a></td>
</tr> 
<tr> 
<td>Objet blob/conteneur de bail</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr> 
<tr> 
<td>Objet blob/conteneur de liste</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr> 
<tr> 
<td>Objet blob de pages</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr>
<tr> 
<td>SAS</td>
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Exemple de tests SAS</a></td>
</tr>   
<tr> 
<td>Propriétés du service</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr>           
<tr> 
<td>Snapshot Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)</a></td>
</tr> 
<tr> 
<td rowspan="9"><b>File</b></td>
<td>Créer des partages/répertoires/fichiers</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></td> 
</tr>
<tr> 
<td>Créer des partages/répertoires/fichiers</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Propriétés/métadonnées du répertoire</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Télécharger des fichiers</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Propriétés/métadonnées/mesures de fichier</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Propriétés du service de fichiers</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Liste des répertoires et des fichiers</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></td> 
</tr>
<tr> 
<td>Partages de listes</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></td> 
</tr>
<tr> 
<td>Propriétés/métadonnées/statistiques de partage</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)</a></td> 
</tr>
<tr> 
<td rowspan="8"><b>File d'attente</b></td>
<td>Ajouter un message</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></td> 
</tr> 
<tr> 
<td>Chiffrement côté client</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></td> 
</tr> 
<tr> 
<td>Créer des files d’attente</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Supprimer le message/la file d’attente</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Lire furtivement un message</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></td> 
</tr> 
<tr> 
<td>ACL/métadonnées/statistiques de la file d’attente</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Propriétés du service de File d’attente</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Mise à jour de message</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)</a></td> 
</tr> 
<tr> 
<td rowspan="7"><b>Table</b></td>
<td>Créer une table</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Supprimer l’entité/la table</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Insertion/fusion/remplacement d’entité</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></td> 
</tr> 
<tr> 
<td>Query Entities</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Tables de requête</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></td> 
</tr> 
<tr> 
<td>ACL/propriétés de la table</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)</a></td> 
</tr> 
<tr> 
<td>Update Entity</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples (Exemples de bibliothèque cliente de stockage en Java)</a></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a>Bibliothèque Exemples de code Azure

bibliothèque d’exemple complet tooview hello, accédez toohello [exemples de Code Azure](https://azure.microsoft.com/resources/samples/?service=storage) library, qui comprend des exemples pour le stockage Azure que vous pouvez télécharger et exécuter localement. Hello, exemple de Code de bibliothèque fournit un exemple de code au format .zip. Ou bien, vous pouvez parcourir et cloner le référentiel GitHub de hello pour chaque échantillon.

[!INCLUDE [storage-java-samples-include](../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a>Guides de prise en main

Extraire hello suivant guides si vous recherchez des instructions sur la façon de tooinstall et prise en main hello bibliothèques clientes de stockage Azure.

* [Getting Started with Azure Blob Service in Java (Prise en main du service Azure Blob en Java)](storage-java-how-to-use-blob-storage.md)
* [Getting Started with Azure Queue Service in Java (Prise en main du service de File d’attente Azure en Java)](storage-java-how-to-use-queue-storage.md)
* [Getting Started with Azure Table Service in Java (Prise en main du service de Table Azure en Java)](storage-java-how-to-use-table-storage.md)
* [Getting Started with Azure File Service in Java (Prise en main du service de fichiers Azure en Java)](storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les exemples pour d’autres langages :

* .NET : [exemples de stockage Azure avec .NET](storage-samples-dotnet.md)
* Tous les autres langages : [exemples de stockage Azure](storage-samples.md)
