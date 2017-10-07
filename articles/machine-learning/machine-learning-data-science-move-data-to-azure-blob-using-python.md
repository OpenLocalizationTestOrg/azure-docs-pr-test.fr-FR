---
title: "tooand de données aaaMove à partir du stockage d’objets Blob Azure à l’aide de Python | Documents Microsoft"
description: "Déplacer les données tooand de stockage d’objets Blob Azure à l’aide de Python"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a>Déplacer les données tooand de stockage d’objets Blob Azure à l’aide de Python
Cette rubrique décrit comment toolist, télécharger, des objets BLOB à l’aide de hello Python API. Avec hello API Python fourni dans Windows Azure SDK, vous pouvez :

* Créez un conteneur.
* Charger un objet blob dans un conteneur
* Télécharger des objets blob
* Répertorier les objets BLOB hello dans un conteneur
* Supprimer un objet blob

Pour plus d’informations sur l’utilisation de hello Python API, consultez [comment tooUse hello Service de stockage d’objets Blob à partir de Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Si vous utilisez une machine virtuelle qui a été configuré avec des scripts hello fournies par [des machines virtuelles de science des données dans Azure](machine-learning-data-science-virtual-machines.md), puis AzCopy est déjà installé sur hello machine virtuelle.
> 
> [!NOTE]
> Pour un stockage d’objets blob tooAzure présentation complète, consultez trop[principes de base Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) et trop[Service d’objets Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Composants requis
Ce document suppose que vous disposez d’un abonnement Azure, un compte de stockage et la clé de stockage correspondante hello pour ce compte. Avant de charger ou télécharger des données, vous devez connaître le nom et la clé de votre compte Azure Storage.

* tooset d’un abonnement Azure, consultez [version d’évaluation d’un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).
* Pour obtenir des instructions sur la création d’un compte de stockage, ainsi que des informations sur le compte et la clé, consultez [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).

## <a name="upload-data-tooblob"></a>Télécharger des données tooBlob
Ajoutez hello suivant extrait haut hello de n’importe quel code Python dans lesquels vous souhaitez tooprogrammatically accès Azure Storage :

    from azure.storage.blob import BlobService

Hello **BlobService** objet vous permet de travailler avec les conteneurs et objets BLOB. Hello suivante de code crée un objet BlobService à l’aide de la clé de compte et le nom du compte de stockage hello. Remplacez le nom et la clé du compte de stockage par le nom et la clé de votre compte.

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

Utilisez hello suivant les méthodes tooupload tooa objet blob :

1. Put\_bloc\_blob\_de\_chemin d’accès (télécharge le contenu de hello d’un fichier à partir du chemin d’accès spécifié de hello)
2. Put\_block_blob\_de\_fichier (télécharge le contenu hello à partir d’un flux de fichier/déjà ouvert)
3. put\_block\_blob\_from\_bytes (charge un tableau d’octets)
4. Put\_bloc\_blob\_de\_texte (télécharge hello spécifié spécifié de valeur de texte à l’aide de hello encodage)

Hello suivant l’exemple de code télécharge un conteneur de tooa fichier local :

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Hello exemple de code suivant télécharge tous les fichiers hello (à l’exclusion de répertoires) dans un stockage tooblob de répertoire local :

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a>Télécharger des données à partir d’un blob
Utilisez hello suivant des données de toodownload de méthodes à partir d’un objet blob :

1. get\_blob\_to\_path
2. get\_blob\_to\_file
3. get\_blob\_to\_bytes
4. get\_blob\_to\_text

Ces méthodes qui effectuent la segmentation nécessaire hello lorsque la taille de hello de données de hello dépasse 64 Mo.

Hello exemple de code suivant télécharge contenu hello d’un objet blob dans un fichier local tooa de conteneur :

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Hello exemple de code suivant télécharge tous les objets BLOB à partir d’un conteneur. Il utilise la liste\_des objets BLOB de liste de hello tooget d’objets BLOB de disponibles dans le conteneur de hello et les télécharge un répertoire local de tooa.

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading hello data %s"%blob.name
