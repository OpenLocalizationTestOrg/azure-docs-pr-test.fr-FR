---
title: "Déplacer des données vers et depuis le stockage d’objets blob Azure à l’aide d’AzCopy | Microsoft Docs"
description: "Déplacer des données vers et depuis le stockage d’objets blob Azure à l’aide d’AzCopy"
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
ms.openlocfilehash: a41ccdd5739a5b10cef201910abd639ae3126c02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="027f3-103">Déplacer des données vers et depuis Stockage Blob Azure à l’aide d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="027f3-103">Move data to and from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="027f3-104">AzCopy est un utilitaire de ligne de commande conçu pour charger, télécharger et copier des données vers et à partir d'un stockage de fichiers, d'objets blob et de tables Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="027f3-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data to and from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="027f3-105">Pour obtenir des instructions sur l’installation d’AzCopy et des informations supplémentaires sur son utilisation avec la plateforme Azure, consultez [Prise en maint de l’utilitaire de ligne de commande AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="027f3-105">For instructions on installing AzCopy and additional information on using it with the Azure platform, see [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="027f3-106">Si vous utilisez une machine virtuelle qui a été configurée avec les scripts fournis par les [machines virtuelles de science des données dans Azure](machine-learning-data-science-virtual-machines.md), cela signifie qu’AzCopy est déjà installé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="027f3-106">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="027f3-107">Pour une présentation complète du stockage d’objets blob Azure, consultez les articles [Fonctionnalités de base des objets blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) et [Service Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="027f3-107">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="027f3-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="027f3-108">Prerequisites</span></span>
<span data-ttu-id="027f3-109">Ce document suppose que vous disposez d’un abonnement Azure, d’un compte de stockage et de la clé de stockage correspondante pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="027f3-109">This document assumes that you have an Azure subscription, a storage account and the corresponding storage key for that account.</span></span> <span data-ttu-id="027f3-110">Avant de charger ou télécharger des données, vous devez connaître le nom et la clé de votre compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="027f3-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="027f3-111">Pour configurer un abonnement Azure, consultez [Essai gratuit pendant un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="027f3-111">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="027f3-112">Pour obtenir des instructions sur la création d’un compte de stockage, ainsi que des informations sur le compte et la clé, consultez [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="027f3-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="027f3-113">Exécuter des commandes AzCopy</span><span class="sxs-lookup"><span data-stu-id="027f3-113">Run AzCopy commands</span></span>
<span data-ttu-id="027f3-114">Pour exécuter des commandes AzCopy, ouvrez une fenêtre de commande, puis naviguez jusqu'au répertoire d'installation d’AzCopy sur votre ordinateur, où se trouve l'exécutable AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="027f3-114">To run AzCopy commands, open a command window and navigate to the AzCopy installation directory on your computer, where the AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="027f3-115">La syntaxe de base d’une commande AzCopy est :</span><span class="sxs-lookup"><span data-stu-id="027f3-115">The basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="027f3-116">Vous pouvez ajouter l’emplacement d’installation d’AzCopy au chemin système puis exécuter les commandes depuis n’importe quel répertoire.</span><span class="sxs-lookup"><span data-stu-id="027f3-116">You can add the AzCopy installation location to your system path and then run the commands from any directory.</span></span> <span data-ttu-id="027f3-117">Par défaut, AzCopy est installé dans *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* ou *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="027f3-117">By default, AzCopy is installed to *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-to-an-azure-blob"></a><span data-ttu-id="027f3-118">Téléchargement de fichiers vers un objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="027f3-118">Upload files to an Azure blob</span></span>
<span data-ttu-id="027f3-119">Pour télécharger un fichier, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="027f3-119">To upload a file, use the following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="027f3-120">Téléchargement de fichiers à partir d'un objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="027f3-120">Download files from an Azure blob</span></span>
<span data-ttu-id="027f3-121">Pour télécharger un fichier à partir d’un objet blob Azure, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="027f3-121">To download a file from an Azure blob, use the following command:</span></span>

    # Downloading blobs to local file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="027f3-122">Transfert d’objets blob entre des conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="027f3-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="027f3-123">Pour transférer des objets blob entre des conteneurs Azure, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="027f3-123">To transfer blobs between Azure containers, use the following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: the sub directory in the container
    <your_local_directory>: directory of local file system where files to be uploaded from or the directory of local file system files to be downloaded to
    <file_pattern>: pattern of file names to be transferred. The standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="027f3-124">Conseils d'utilisation d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="027f3-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="027f3-125">Lors du **chargement** de fichiers, le paramètre */S* charge les fichiers de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="027f3-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="027f3-126">Sans ce paramètre, les fichiers situés dans les sous-répertoires ne sont pas téléchargés.</span><span class="sxs-lookup"><span data-stu-id="027f3-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="027f3-127">Lors du **téléchargement** du fichier, */S* recherche le conteneur de manière récursive jusqu’à ce que tous les fichiers du répertoire spécifié et de ses sous-répertoires ou que tous les fichiers répondant au critère spécifié dans le répertoire concerné et ses sous-répertoires soient téléchargés.</span><span class="sxs-lookup"><span data-stu-id="027f3-127">When **downloading** file, */S* searches the container recursively until all files in the specified directory and its subdirectories, or all files that match the specified pattern in the given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="027f3-128">Vous ne pouvez pas spécifier un **fichier de blob** à télécharger, à l’aide du paramètre */Source* .</span><span class="sxs-lookup"><span data-stu-id="027f3-128">You cannot specify a **specific blob file** to download using the */Source* parameter.</span></span> <span data-ttu-id="027f3-129">Pour télécharger un fichier spécifique, spécifiez le nom du fichier à télécharger à l’aide du paramètre */Pattern* .</span><span class="sxs-lookup"><span data-stu-id="027f3-129">To download a specific file, specify the blob file name to download using the */Pattern* parameter.</span></span> <span data-ttu-id="027f3-130">**/S** peut être utilisé pour qu’AzCopy recherche un modèle de nom de fichier de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="027f3-130">**/S** parameter can be used to have AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="027f3-131">Sans le paramètre /Pattern, AzCopy télécharge tous les fichiers de ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="027f3-131">Without the pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

