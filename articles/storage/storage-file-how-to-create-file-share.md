---
title: aaaHow toocreate un partage de fichiers Azure | Documents Microsoft
description: "Comment toocreate un Azure partage de fichiers dans le stockage de fichiers Azure à l’aide de hello portail Azure, PowerShell et hello CLI d’Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="b23bf-103">Création d’un partage de fichiers dans le Stockage Fichier Azure</span><span class="sxs-lookup"><span data-stu-id="b23bf-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="b23bf-104">Vous pouvez créer des partages de fichiers Azure à l’aide de [portail Azure](https://portal.azure.com/), hello applets de commande PowerShell de stockage Azure, hello des bibliothèques clientes de stockage Azure ou hello API REST de stockage Azure. Dans ce didacticiel, vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="b23bf-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="b23bf-105">Comment toocreate un fichier Azure partager à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b23bf-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="b23bf-106">Comment toocreate un Azure de partage de fichiers à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="b23bf-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="b23bf-107">Comment toocreate un Azure de partage de fichiers à l’aide de CLI</span><span class="sxs-lookup"><span data-stu-id="b23bf-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="b23bf-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b23bf-108">Prerequisites</span></span>
<span data-ttu-id="b23bf-109">toocreate un partage de fichiers Azure, vous pouvez utiliser un compte de stockage existe déjà, ou [créer un nouveau compte de stockage Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b23bf-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](storage-create-storage-account.md).</span></span> <span data-ttu-id="b23bf-110">toocreate un partage de fichiers Azure avec PowerShell, vous devez clé de compte hello et le nom de votre compte de stockage...</span><span class="sxs-lookup"><span data-stu-id="b23bf-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="b23bf-111">Si vous envisagez de toouse Powershell ou CLI, vous devez clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="b23bf-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="b23bf-112">Créer le partage de fichiers via hello portail</span><span class="sxs-lookup"><span data-stu-id="b23bf-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="b23bf-113">**Panneau de compte tooStorage accédez sur le portail Azure**:</span><span class="sxs-lookup"><span data-stu-id="b23bf-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="b23bf-114">![Panneau Compte de stockage](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="b23bf-114">![Storage Account Blade](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="b23bf-115">**Cliquez sur Ajouter un partage de fichiers** :</span><span class="sxs-lookup"><span data-stu-id="b23bf-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="b23bf-116">![Cliquez sur hello ajouter le bouton de partage de fichier](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="b23bf-116">![Click hello add file share button](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="b23bf-117">**Indiquez le nom et le quota. Actuellement, la limite de quota maximum est 5 To** :</span><span class="sxs-lookup"><span data-stu-id="b23bf-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="b23bf-118">![Fournir un nom et un quota de votre choix pour le nouveau partage de fichiers hello](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="b23bf-118">![Provide a name and a desired quota for hello new file share](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="b23bf-119">**Affichez votre nouveau partage de fichiers** : ![Affichez votre nouveau partage de fichiers](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="b23bf-119">**View your new file share**:  ![View your new file share](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="b23bf-120">**Importez un fichier** : ![Importez un fichier](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="b23bf-120">**Upload a file**:  ![Upload a file](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="b23bf-121">**Parcourez le partage de fichiers et gérez vos répertoires et vos fichiers** : ![Parcourez le partage de fichiers](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="b23bf-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="b23bf-122">Création d’un partage de fichiers via PowerShell</span><span class="sxs-lookup"><span data-stu-id="b23bf-122">Create file share through PowerShell</span></span>
<span data-ttu-id="b23bf-123">tooprepare toouse PowerShell, téléchargez et installez les applets de commande PowerShell Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b23bf-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="b23bf-124">Consultez [comment tooinstall et configurer Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) Pourquoi installer instructions d’installation et de point.</span><span class="sxs-lookup"><span data-stu-id="b23bf-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="b23bf-125">Il est recommandé de télécharger et installer ou mettre à niveau du module Azure PowerShell toohello plus récent.</span><span class="sxs-lookup"><span data-stu-id="b23bf-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="b23bf-126">**Créer un contexte pour votre compte de stockage et de la clé** contexte de hello encapsule la clé de compte et le nom du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="b23bf-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="b23bf-127">Pour obtenir des instructions sur la copie de votre clé de compte à partir du [portail Azure](https://portal.azure.com/), voir [Afficher et copier les clés d’accès de stockage](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="b23bf-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="b23bf-128">**Créez un nouveau partage de fichiers** :</span><span class="sxs-lookup"><span data-stu-id="b23bf-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="b23bf-129">nom de Hello de votre partage de fichiers doit être tout en minuscules.</span><span class="sxs-lookup"><span data-stu-id="b23bf-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="b23bf-130">Pour plus d’informations sur la façon de nommer des partages de fichiers et des fichiers, consultez la rubrique [Affectation de noms et références aux partages, répertoires, fichiers et métadonnées](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="b23bf-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="b23bf-131">Création d’un partage de fichiers via l’Interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="b23bf-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="b23bf-132">**tooprepare toouse une Interface de ligne de commande (CLI), téléchargez et installez les hello CLI d’Azure.**</span><span class="sxs-lookup"><span data-stu-id="b23bf-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="b23bf-133">Consultez [Installation d’Azure CLI 2.0](/cli/azure/install-az-cli2.md) et [Prise en main d’Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b23bf-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="b23bf-134">**Créer un compte de stockage de chaîne de connexion toohello où vous souhaitez partager de hello toocreate.**</span><span class="sxs-lookup"><span data-stu-id="b23bf-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="b23bf-135">Remplacez ```<storage-account>``` et ```<resource_group>``` avec votre compte nom et la ressource de groupe de stockage Bonjour l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="b23bf-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="b23bf-136">**Créez le partage de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="b23bf-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="b23bf-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b23bf-137">Next steps</span></span>
* [<span data-ttu-id="b23bf-138">Connexion et montage du partage de fichiers – Windows</span><span class="sxs-lookup"><span data-stu-id="b23bf-138">Connect and Mount File Share - Windows</span></span>](storage-file-how-to-use-files-windows.md)
* [<span data-ttu-id="b23bf-139">Connexion et montage du partage de fichiers – Linux</span><span class="sxs-lookup"><span data-stu-id="b23bf-139">Connect and Mount File Share - Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="b23bf-140">Connexion et montage du partage de fichiers – MacOS</span><span class="sxs-lookup"><span data-stu-id="b23bf-140">Connect and Mount File Share - macOS</span></span>](storage-file-how-to-use-files-mac.md)

<span data-ttu-id="b23bf-141">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="b23bf-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="b23bf-142">FAQ</span><span class="sxs-lookup"><span data-stu-id="b23bf-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="b23bf-143">Dépannage</span><span class="sxs-lookup"><span data-stu-id="b23bf-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)