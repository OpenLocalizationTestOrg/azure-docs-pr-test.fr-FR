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
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="13244-103">Déplacer les données tooand à partir du stockage d’objets Blob Azure à l’aide d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="13244-103">Move data tooand from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="13244-104">AzCopy est un utilitaire de ligne de commande conçu pour le téléchargement, le téléchargement et la copie tooand de données à partir d’objets blob Microsoft Azure, de fichiers et de stockage de table.</span><span class="sxs-lookup"><span data-stu-id="13244-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data tooand from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="13244-105">Pour obtenir des instructions sur l’installation des AzCopy et des informations supplémentaires sur l’utilisation d’hello plateforme Azure, consultez [prise en main de l’utilitaire de ligne de commande AzCopy de hello](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="13244-105">For instructions on installing AzCopy and additional information on using it with hello Azure platform, see [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="13244-106">Si vous utilisez une machine virtuelle qui a été configuré avec des scripts hello fournies par [des machines virtuelles de science des données dans Azure](machine-learning-data-science-virtual-machines.md), puis AzCopy est déjà installé sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="13244-106">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="13244-107">Pour un stockage d’objets blob tooAzure présentation complète, consultez trop[principes de base Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) et trop[Service d’objets Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="13244-107">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="13244-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="13244-108">Prerequisites</span></span>
<span data-ttu-id="13244-109">Ce document suppose que vous avez un abonnement Azure, un compte de stockage et hello clé de stockage correspondante pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="13244-109">This document assumes that you have an Azure subscription, a storage account and hello corresponding storage key for that account.</span></span> <span data-ttu-id="13244-110">Avant de charger ou télécharger des données, vous devez connaître le nom et la clé de votre compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="13244-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="13244-111">tooset d’un abonnement Azure, consultez [version d’évaluation d’un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13244-111">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="13244-112">Pour obtenir des instructions sur la création d’un compte de stockage, ainsi que des informations sur le compte et la clé, consultez [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="13244-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="13244-113">Exécuter des commandes AzCopy</span><span class="sxs-lookup"><span data-stu-id="13244-113">Run AzCopy commands</span></span>
<span data-ttu-id="13244-114">commandes AzCopy de toorun, ouvrez une fenêtre de commande et accédez de répertoire d’installation toohello AzCopy sur votre ordinateur où se trouve le fichier exécutable de AzCopy.exe hello.</span><span class="sxs-lookup"><span data-stu-id="13244-114">toorun AzCopy commands, open a command window and navigate toohello AzCopy installation directory on your computer, where hello AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="13244-115">syntaxe de base Hello pour les commandes AzCopy est la suivante :</span><span class="sxs-lookup"><span data-stu-id="13244-115">hello basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="13244-116">Vous pouvez ajouter le chemin d’accès de hello AzCopy installation emplacement tooyour système et puis exécutez les commandes hello à partir de n’importe quel répertoire.</span><span class="sxs-lookup"><span data-stu-id="13244-116">You can add hello AzCopy installation location tooyour system path and then run hello commands from any directory.</span></span> <span data-ttu-id="13244-117">Par défaut, AzCopy est installé trop*% ProgramFiles% (x86) %\Microsoft SDKs\Azure\AzCopy* ou *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="13244-117">By default, AzCopy is installed too*%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-tooan-azure-blob"></a><span data-ttu-id="13244-118">Télécharger les fichiers tooan objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="13244-118">Upload files tooan Azure blob</span></span>
<span data-ttu-id="13244-119">tooupload un fichier, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="13244-119">tooupload a file, use hello following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="13244-120">Téléchargement de fichiers à partir d'un objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="13244-120">Download files from an Azure blob</span></span>
<span data-ttu-id="13244-121">toodownload un fichier à partir d’un objet blob Azure, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="13244-121">toodownload a file from an Azure blob, use hello following command:</span></span>

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="13244-122">Transfert d’objets blob entre des conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="13244-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="13244-123">BLOB tootransfer entre les conteneurs Azure, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="13244-123">tootransfer blobs between Azure containers, use hello following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="13244-124">Conseils d'utilisation d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="13244-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="13244-125">Lors du **chargement** de fichiers, le paramètre */S* charge les fichiers de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="13244-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="13244-126">Sans ce paramètre, les fichiers situés dans les sous-répertoires ne sont pas téléchargés.</span><span class="sxs-lookup"><span data-stu-id="13244-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="13244-127">Lorsque **téléchargement** fichier */S* recherches hello conteneur de manière récursive jusqu'à ce que tous les fichiers dans le répertoire spécifié de hello et ses sous-répertoires, ou tous les fichiers qui correspondent aux hello modèle spécifié dans hello donné répertoire et ses sous-répertoires, sont téléchargées.</span><span class="sxs-lookup"><span data-stu-id="13244-127">When **downloading** file, */S* searches hello container recursively until all files in hello specified directory and its subdirectories, or all files that match hello specified pattern in hello given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="13244-128">Vous ne pouvez pas spécifier un **fichier blob spécifique** toodownload à l’aide de hello */Source* paramètre.</span><span class="sxs-lookup"><span data-stu-id="13244-128">You cannot specify a **specific blob file** toodownload using hello */Source* parameter.</span></span> <span data-ttu-id="13244-129">toodownload un fichier spécifique, spécifiez toodownload de nom du fichier de blob hello à l’aide de hello */modèle* paramètre.</span><span class="sxs-lookup"><span data-stu-id="13244-129">toodownload a specific file, specify hello blob file name toodownload using hello */Pattern* parameter.</span></span> <span data-ttu-id="13244-130">**/S** paramètre peut être utilisé toohave AzCopy, recherchez un modèle de nom de fichier manière récursive.</span><span class="sxs-lookup"><span data-stu-id="13244-130">**/S** parameter can be used toohave AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="13244-131">Sans paramètre de modèle hello, AzCopy télécharge tous les fichiers dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="13244-131">Without hello pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

