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
ms.openlocfilehash: 0eea1ff8e4f4c1d108445e1a1250b6fa8ff48910
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-python"></a><span data-ttu-id="c7da4-103">Déplacer des données vers et depuis Stockage Blob Azure à l’aide de Python</span><span class="sxs-lookup"><span data-stu-id="c7da4-103">Move data to and from Azure Blob Storage using Python</span></span>
<span data-ttu-id="c7da4-104">Cette rubrique décrit comment répertorier, charger et télécharger des objets blob à l’aide de l’API Python.</span><span class="sxs-lookup"><span data-stu-id="c7da4-104">This topic describes how to list, upload, and download blobs using the Python API.</span></span> <span data-ttu-id="c7da4-105">Avec l’API Python fournie dans le SDK Azure, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="c7da4-105">With the Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="c7da4-106">Créer un conteneur</span><span class="sxs-lookup"><span data-stu-id="c7da4-106">Create a container</span></span>
* <span data-ttu-id="c7da4-107">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="c7da4-107">Upload a blob into a container</span></span>
* <span data-ttu-id="c7da4-108">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="c7da4-108">Download blobs</span></span>
* <span data-ttu-id="c7da4-109">Créer une liste d'objets blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="c7da4-109">List the blobs in a container</span></span>
* <span data-ttu-id="c7da4-110">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="c7da4-110">Delete a blob</span></span>

<span data-ttu-id="c7da4-111">Pour plus d’informations sur l’utilisation de l’API Python, consultez [Utilisation du service de stockage d’objets blob à partir de Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="c7da4-111">For more information about using the Python API, see [How to Use the Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="c7da4-112">Si vous utilisez une machine virtuelle qui a été configurée avec les scripts fournis par les [machines virtuelles de science des données dans Azure](machine-learning-data-science-virtual-machines.md), cela signifie qu’AzCopy est déjà installé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c7da4-112">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="c7da4-113">Pour une présentation complète du stockage d’objets blob Azure, consultez les articles [Fonctionnalités de base des objets blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) et [Service Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7da4-113">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c7da4-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c7da4-114">Prerequisites</span></span>
<span data-ttu-id="c7da4-115">Ce document suppose que vous disposez d’un abonnement Azure, d’un compte de stockage et de la clé de stockage correspondante pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="c7da4-115">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="c7da4-116">Avant de charger ou télécharger des données, vous devez connaître le nom et la clé de votre compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c7da4-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="c7da4-117">Pour configurer un abonnement Azure, consultez [Essai gratuit pendant un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7da4-117">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c7da4-118">Pour obtenir des instructions sur la création d’un compte de stockage, ainsi que des informations sur le compte et la clé, consultez [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="c7da4-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-to-blob"></a><span data-ttu-id="c7da4-119">Charger les données dans le blob</span><span class="sxs-lookup"><span data-stu-id="c7da4-119">Upload Data to Blob</span></span>
<span data-ttu-id="c7da4-120">Ajoutez la ligne suivante vers le début du code Python dans lequel vous souhaitez programmer l’accès au service Azure Storage :</span><span class="sxs-lookup"><span data-stu-id="c7da4-120">Add the following snippet near the top of any Python code in which you wish to programmatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="c7da4-121">L'objet **BlobService** permet d'utiliser des conteneurs et des objets blob.</span><span class="sxs-lookup"><span data-stu-id="c7da4-121">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="c7da4-122">Le code suivant crée un objet BlobService à l’aide du nom et de la clé du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c7da4-122">The following code creates a BlobService object using the storage account name and account key.</span></span> <span data-ttu-id="c7da4-123">Remplacez le nom et la clé du compte de stockage par le nom et la clé de votre compte.</span><span class="sxs-lookup"><span data-stu-id="c7da4-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="c7da4-124">Pour charger les données dans un blob, utilisez les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c7da4-124">Use the following methods to upload data to a blob:</span></span>

1. <span data-ttu-id="c7da4-125">put\_block\_blob\_from\_path (charge le contenu d’un fichier situé à l’emplacement spécifié)</span><span class="sxs-lookup"><span data-stu-id="c7da4-125">put\_block\_blob\_from\_path (uploads the contents of a file from the specified path)</span></span>
2. <span data-ttu-id="c7da4-126">put\_block_blob\_from\_file (charge le contenu d’un fichier/flux déjà ouvert)</span><span class="sxs-lookup"><span data-stu-id="c7da4-126">put\_block_blob\_from\_file (uploads the contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="c7da4-127">put\_block\_blob\_from\_bytes (charge un tableau d’octets)</span><span class="sxs-lookup"><span data-stu-id="c7da4-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="c7da4-128">put\_block\_blob\_from\_text (charge la valeur de texte indiquée, dans l’encodage spécifié)</span><span class="sxs-lookup"><span data-stu-id="c7da4-128">put\_block\_blob\_from\_text (uploads the specified text value using the specified encoding)</span></span>

<span data-ttu-id="c7da4-129">L’exemple de code suivant charge un fichier local dans un conteneur :</span><span class="sxs-lookup"><span data-stu-id="c7da4-129">The following sample code uploads a local file to a container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="c7da4-130">L’exemple de code suivant charge tous les fichiers (à l’exception des sous-répertoires) d’un répertoire local dans le blob :</span><span class="sxs-lookup"><span data-stu-id="c7da4-130">The following sample code uploads all the files (excluding directories) in a local directory to blob storage:</span></span>

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


## <a name="download-data-from-blob"></a><span data-ttu-id="c7da4-131">Télécharger des données à partir d’un blob</span><span class="sxs-lookup"><span data-stu-id="c7da4-131">Download Data from Blob</span></span>
<span data-ttu-id="c7da4-132">Pour télécharger des données à partir d’un blob, utilisez les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c7da4-132">Use the following methods to download data from a blob:</span></span>

1. <span data-ttu-id="c7da4-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="c7da4-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="c7da4-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="c7da4-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="c7da4-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="c7da4-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="c7da4-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="c7da4-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="c7da4-137">Ces méthodes effectuent le traitement nécessaire lorsque les données dépassent 64 Mo.</span><span class="sxs-lookup"><span data-stu-id="c7da4-137">These methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="c7da4-138">L’exemple de code suivant télécharge le contenu d’un blob d’un conteneur dans un fichier local :</span><span class="sxs-lookup"><span data-stu-id="c7da4-138">The following sample code downloads the contents of a blob in a container to a local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="c7da4-139">L’exemple de code suivant télécharge tous les blobs d’un conteneur.</span><span class="sxs-lookup"><span data-stu-id="c7da4-139">The following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="c7da4-140">Il utilise list\_blobs pour obtenir la liste des objets blob disponibles dans le conteneur et les télécharge dans un répertoire local.</span><span class="sxs-lookup"><span data-stu-id="c7da4-140">It uses list\_blobs to get the list of available blobs in the container and downloads them to a local directory.</span></span>

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
