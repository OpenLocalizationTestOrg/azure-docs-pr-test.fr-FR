---
title: "Déplacer des données vers et depuis le stockage d’objets blob Azure à l’aide de Python | Microsoft Docs"
description: "Déplacer des données vers et depuis le stockage d’objets blob Azure à l’aide de Python"
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
ms.openlocfilehash: d7847f695a77ad469f56a20518cb979c41384d1e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-python"></a>Déplacer des données vers et depuis Stockage Blob Azure à l’aide de Python
Cette rubrique décrit comment répertorier, charger et télécharger des objets blob à l’aide de l’API Python. Avec l’API Python fournie dans le SDK Azure, vous pouvez :

* Créer un conteneur
* Charger un objet blob dans un conteneur
* Télécharger des objets blob
* Créer une liste d'objets blob dans un conteneur
* Supprimer un objet blob

Pour plus d’informations sur l’utilisation de l’API Python, consultez [Utilisation du service de stockage d’objets blob à partir de Python](../../storage/blobs/storage-python-how-to-use-blob-storage.md).

[!INCLUDE [blob-storage-tool-selector](../../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Si vous utilisez une machine virtuelle qui a été configurée avec les scripts fournis par les [machines virtuelles de science des données dans Azure](virtual-machines.md), cela signifie qu’AzCopy est déjà installé sur la machine virtuelle.
> 
> [!NOTE]
> Pour une présentation complète du stockage d’objets blob Azure, consultez les articles [Fonctionnalités de base des objets blob Azure](../../storage/blobs/storage-dotnet-how-to-use-blobs.md) et [Service Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Composants requis
Ce document suppose que vous disposez d’un abonnement Azure, d’un compte de stockage et de la clé de stockage correspondante pour ce compte. Avant de charger ou télécharger des données, vous devez connaître le nom et la clé de votre compte Azure Storage.

* Pour configurer un abonnement Azure, consultez [Essai gratuit pendant un mois](https://azure.microsoft.com/pricing/free-trial/).
* Pour obtenir des instructions sur la création d’un compte de stockage, ainsi que des informations sur le compte et la clé, consultez [À propos des comptes de stockage Azure](../../storage/common/storage-create-storage-account.md).

## <a name="upload-data-to-blob"></a>Charger les données dans le blob
Ajoutez la ligne suivante vers le début du code Python dans lequel vous souhaitez programmer l’accès au service Azure Storage :

    from azure.storage.blob import BlobService

L'objet **BlobService** permet d'utiliser des conteneurs et des objets blob. Le code suivant crée un objet BlobService à l’aide du nom et de la clé du compte de stockage. Remplacez le nom et la clé du compte de stockage par le nom et la clé de votre compte.

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

Pour charger les données dans un blob, utilisez les méthodes suivantes :

1. put\_block\_blob\_from\_path (charge le contenu d’un fichier situé à l’emplacement spécifié)
2. put\_block_blob\_from\_file (charge le contenu d’un fichier/flux déjà ouvert)
3. put\_block\_blob\_from\_bytes (charge un tableau d’octets)
4. put\_block\_blob\_from\_text (charge la valeur de texte indiquée, dans l’encodage spécifié)

L’exemple de code suivant charge un fichier local dans un conteneur :

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

L’exemple de code suivant charge tous les fichiers (à l’exception des sous-répertoires) d’un répertoire local dans le blob :

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in the LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading the data %s"%blob_name


## <a name="download-data-from-blob"></a>Télécharger des données à partir d’un blob
Pour télécharger des données à partir d’un blob, utilisez les méthodes suivantes :

1. get\_blob\_to\_path
2. get\_blob\_to\_file
3. get\_blob\_to\_bytes
4. get\_blob\_to\_text

Ces méthodes effectuent le traitement nécessaire lorsque les données dépassent 64 Mo.

L’exemple de code suivant télécharge le contenu d’un blob d’un conteneur dans un fichier local :

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

L’exemple de code suivant télécharge tous les blobs d’un conteneur. Il utilise list\_blobs pour obtenir la liste des objets blob disponibles dans le conteneur et les télécharge dans un répertoire local.

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
            print "something wrong happened when downloading the data %s"%blob.name
