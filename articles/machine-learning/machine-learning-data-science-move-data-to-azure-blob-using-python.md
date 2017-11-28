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
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a><span data-ttu-id="cb3a3-103">Déplacer les données tooand de stockage d’objets Blob Azure à l’aide de Python</span><span class="sxs-lookup"><span data-stu-id="cb3a3-103">Move data tooand from Azure Blob Storage using Python</span></span>
<span data-ttu-id="cb3a3-104">Cette rubrique décrit comment toolist, télécharger, des objets BLOB à l’aide de hello Python API.</span><span class="sxs-lookup"><span data-stu-id="cb3a3-104">This topic describes how toolist, upload, and download blobs using hello Python API.</span></span> <span data-ttu-id="cb3a3-105">Avec hello API Python fourni dans Windows Azure SDK, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="cb3a3-105">With hello Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="cb3a3-106">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb3a3-106">Create a container</span></span>
* <span data-ttu-id="cb3a3-107">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="cb3a3-107">Upload a blob into a container</span></span>
* <span data-ttu-id="cb3a3-108">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="cb3a3-108">Download blobs</span></span>
* <span data-ttu-id="cb3a3-109">Répertorier les objets BLOB hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="cb3a3-109">List hello blobs in a container</span></span>
* <span data-ttu-id="cb3a3-110">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="cb3a3-110">Delete a blob</span></span>

<span data-ttu-id="cb3a3-111">Pour plus d’informations sur l’utilisation de hello Python API, consultez [comment tooUse hello Service de stockage d’objets Blob à partir de Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="cb3a3-111">For more information about using hello Python API, see [How tooUse hello Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="cb3a3-112">Si vous utilisez une machine virtuelle qui a été configuré avec des scripts hello fournies par [des machines virtuelles de science des données dans Azure](machine-learning-data-science-virtual-machines.md), puis AzCopy est déjà installé sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cb3a3-112">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="cb3a3-113">Pour un stockage d’objets blob tooAzure présentation complète, consultez trop[principes de base Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) et trop[Service d’objets Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb3a3-113">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="cb3a3-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cb3a3-114">Prerequisites</span></span>
<span data-ttu-id="cb3a3-115">Ce document suppose que vous disposez d’un abonnement Azure, un compte de stockage et la clé de stockage correspondante hello pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="cb3a3-115">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="cb3a3-116">Avant de charger ou télécharger des données, vous devez connaître le nom et la clé de votre compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="cb3a3-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="cb3a3-117">tooset d’un abonnement Azure, consultez [version d’évaluation d’un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb3a3-117">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cb3a3-118">Pour obtenir des instructions sur la création d’un compte de stockage, ainsi que des informations sur le compte et la clé, consultez [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="cb3a3-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-tooblob"></a><span data-ttu-id="cb3a3-119">Télécharger des données tooBlob</span><span class="sxs-lookup"><span data-stu-id="cb3a3-119">Upload Data tooBlob</span></span>
<span data-ttu-id="cb3a3-120">Ajoutez hello suivant extrait haut hello de n’importe quel code Python dans lesquels vous souhaitez tooprogrammatically accès Azure Storage :</span><span class="sxs-lookup"><span data-stu-id="cb3a3-120">Add hello following snippet near hello top of any Python code in which you wish tooprogrammatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="cb3a3-121">Hello **BlobService** objet vous permet de travailler avec les conteneurs et objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb3a3-121">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="cb3a3-122">Hello suivante de code crée un objet BlobService à l’aide de la clé de compte et le nom du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="cb3a3-122">hello following code creates a BlobService object using hello storage account name and account key.</span></span> <span data-ttu-id="cb3a3-123">Remplacez le nom et la clé du compte de stockage par le nom et la clé de votre compte.</span><span class="sxs-lookup"><span data-stu-id="cb3a3-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="cb3a3-124">Utilisez hello suivant les méthodes tooupload tooa objet blob :</span><span class="sxs-lookup"><span data-stu-id="cb3a3-124">Use hello following methods tooupload data tooa blob:</span></span>

1. <span data-ttu-id="cb3a3-125">Put\_bloc\_blob\_de\_chemin d’accès (télécharge le contenu de hello d’un fichier à partir du chemin d’accès spécifié de hello)</span><span class="sxs-lookup"><span data-stu-id="cb3a3-125">put\_block\_blob\_from\_path (uploads hello contents of a file from hello specified path)</span></span>
2. <span data-ttu-id="cb3a3-126">Put\_block_blob\_de\_fichier (télécharge le contenu hello à partir d’un flux de fichier/déjà ouvert)</span><span class="sxs-lookup"><span data-stu-id="cb3a3-126">put\_block_blob\_from\_file (uploads hello contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="cb3a3-127">put\_block\_blob\_from\_bytes (charge un tableau d’octets)</span><span class="sxs-lookup"><span data-stu-id="cb3a3-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="cb3a3-128">Put\_bloc\_blob\_de\_texte (télécharge hello spécifié spécifié de valeur de texte à l’aide de hello encodage)</span><span class="sxs-lookup"><span data-stu-id="cb3a3-128">put\_block\_blob\_from\_text (uploads hello specified text value using hello specified encoding)</span></span>

<span data-ttu-id="cb3a3-129">Hello suivant l’exemple de code télécharge un conteneur de tooa fichier local :</span><span class="sxs-lookup"><span data-stu-id="cb3a3-129">hello following sample code uploads a local file tooa container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="cb3a3-130">Hello exemple de code suivant télécharge tous les fichiers hello (à l’exclusion de répertoires) dans un stockage tooblob de répertoire local :</span><span class="sxs-lookup"><span data-stu-id="cb3a3-130">hello following sample code uploads all hello files (excluding directories) in a local directory tooblob storage:</span></span>

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


## <a name="download-data-from-blob"></a><span data-ttu-id="cb3a3-131">Télécharger des données à partir d’un blob</span><span class="sxs-lookup"><span data-stu-id="cb3a3-131">Download Data from Blob</span></span>
<span data-ttu-id="cb3a3-132">Utilisez hello suivant des données de toodownload de méthodes à partir d’un objet blob :</span><span class="sxs-lookup"><span data-stu-id="cb3a3-132">Use hello following methods toodownload data from a blob:</span></span>

1. <span data-ttu-id="cb3a3-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="cb3a3-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="cb3a3-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="cb3a3-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="cb3a3-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="cb3a3-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="cb3a3-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="cb3a3-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="cb3a3-137">Ces méthodes qui effectuent la segmentation nécessaire hello lorsque la taille de hello de données de hello dépasse 64 Mo.</span><span class="sxs-lookup"><span data-stu-id="cb3a3-137">These methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="cb3a3-138">Hello exemple de code suivant télécharge contenu hello d’un objet blob dans un fichier local tooa de conteneur :</span><span class="sxs-lookup"><span data-stu-id="cb3a3-138">hello following sample code downloads hello contents of a blob in a container tooa local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="cb3a3-139">Hello exemple de code suivant télécharge tous les objets BLOB à partir d’un conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb3a3-139">hello following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="cb3a3-140">Il utilise la liste\_des objets BLOB de liste de hello tooget d’objets BLOB de disponibles dans le conteneur de hello et les télécharge un répertoire local de tooa.</span><span class="sxs-lookup"><span data-stu-id="cb3a3-140">It uses list\_blobs tooget hello list of available blobs in hello container and downloads them tooa local directory.</span></span>

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
