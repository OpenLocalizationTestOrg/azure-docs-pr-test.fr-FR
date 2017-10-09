---
title: "tooand de données aaaMove à partir du stockage d’objets Blob Azure à l’aide de AzCopy | Documents Microsoft"
description: "Déplacer les données tooand à partir du stockage d’objets Blob Azure à l’aide d’AzCopy"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a>Déplacer les données tooand à partir du stockage d’objets Blob Azure à l’aide d’AzCopy
AzCopy est un utilitaire de ligne de commande conçu pour le téléchargement, le téléchargement et la copie tooand de données à partir d’objets blob Microsoft Azure, de fichiers et de stockage de table.

Pour obtenir des instructions sur l’installation des AzCopy et des informations supplémentaires sur l’utilisation d’hello plateforme Azure, consultez [prise en main de l’utilitaire de ligne de commande AzCopy de hello](../storage/common/storage-use-azcopy.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Si vous utilisez une machine virtuelle qui a été configuré avec des scripts hello fournies par [des machines virtuelles de science des données dans Azure](machine-learning-data-science-virtual-machines.md), puis AzCopy est déjà installé sur hello machine virtuelle.
> 
> [!NOTE]
> Pour un stockage d’objets blob tooAzure présentation complète, consultez trop[principes de base Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) et trop[Service d’objets Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Composants requis
Ce document suppose que vous avez un abonnement Azure, un compte de stockage et hello clé de stockage correspondante pour ce compte. Avant de charger ou télécharger des données, vous devez connaître le nom et la clé de votre compte Azure Storage.

* tooset d’un abonnement Azure, consultez [version d’évaluation d’un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).
* Pour obtenir des instructions sur la création d’un compte de stockage, ainsi que des informations sur le compte et la clé, consultez [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).

## <a name="run-azcopy-commands"></a>Exécuter des commandes AzCopy
commandes AzCopy de toorun, ouvrez une fenêtre de commande et accédez de répertoire d’installation toohello AzCopy sur votre ordinateur où se trouve le fichier exécutable de AzCopy.exe hello. 

syntaxe de base Hello pour les commandes AzCopy est la suivante :

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> Vous pouvez ajouter le chemin d’accès de hello AzCopy installation emplacement tooyour système et puis exécutez les commandes hello à partir de n’importe quel répertoire. Par défaut, AzCopy est installé trop*% ProgramFiles% (x86) %\Microsoft SDKs\Azure\AzCopy* ou *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.
> 
> 

## <a name="upload-files-tooan-azure-blob"></a>Télécharger les fichiers tooan objets blob Azure
tooupload un fichier, utilisez hello de commande suivante :

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a>Téléchargement de fichiers à partir d'un objet blob Azure
toodownload un fichier à partir d’un objet blob Azure, hello utilisez commande suivante :

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a>Transfert d’objets blob entre des conteneurs Azure
BLOB tootransfer entre les conteneurs Azure, utilisez hello de commande suivante :

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a>Conseils d'utilisation d’AzCopy
> [!TIP]
> 1. Lors du **chargement** de fichiers, le paramètre */S* charge les fichiers de manière récursive. Sans ce paramètre, les fichiers situés dans les sous-répertoires ne sont pas téléchargés.  
> 2. Lorsque **téléchargement** fichier */S* recherches hello conteneur de manière récursive jusqu'à ce que tous les fichiers dans le répertoire spécifié de hello et ses sous-répertoires, ou tous les fichiers qui correspondent aux hello modèle spécifié dans hello donné répertoire et ses sous-répertoires, sont téléchargées.  
> 3. Vous ne pouvez pas spécifier un **fichier blob spécifique** toodownload à l’aide de hello */Source* paramètre. toodownload un fichier spécifique, spécifiez toodownload de nom du fichier de blob hello à l’aide de hello */modèle* paramètre. **/S** paramètre peut être utilisé toohave AzCopy, recherchez un modèle de nom de fichier manière récursive. Sans paramètre de modèle hello, AzCopy télécharge tous les fichiers dans ce répertoire.
> 
> 

