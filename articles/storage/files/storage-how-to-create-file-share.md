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
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="7aa72-103">Création d’un partage de fichiers dans le Stockage Fichier Azure</span><span class="sxs-lookup"><span data-stu-id="7aa72-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="7aa72-104">Vous pouvez créer des partages de fichiers Azure à l’aide de [portail Azure](https://portal.azure.com/), hello applets de commande PowerShell de stockage Azure, hello des bibliothèques clientes de stockage Azure ou hello API REST de stockage Azure. Dans ce didacticiel, vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="7aa72-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="7aa72-105">Comment toocreate un fichier Azure partager à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7aa72-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="7aa72-106">Comment toocreate un Azure de partage de fichiers à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="7aa72-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="7aa72-107">Comment toocreate un Azure de partage de fichiers à l’aide de CLI</span><span class="sxs-lookup"><span data-stu-id="7aa72-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="7aa72-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7aa72-108">Prerequisites</span></span>
<span data-ttu-id="7aa72-109">toocreate un partage de fichiers Azure, vous pouvez utiliser un compte de stockage existe déjà, ou [créer un nouveau compte de stockage Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7aa72-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span> <span data-ttu-id="7aa72-110">toocreate un partage de fichiers Azure avec PowerShell, vous devez clé de compte hello et le nom de votre compte de stockage...</span><span class="sxs-lookup"><span data-stu-id="7aa72-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="7aa72-111">Si vous envisagez de toouse Powershell ou CLI, vous devez clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7aa72-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="7aa72-112">Créer le partage de fichiers via hello portail</span><span class="sxs-lookup"><span data-stu-id="7aa72-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="7aa72-113">**Panneau de compte tooStorage accédez sur le portail Azure**:</span><span class="sxs-lookup"><span data-stu-id="7aa72-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="7aa72-114">![Panneau Compte de stockage](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="7aa72-114">![Storage Account Blade](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="7aa72-115">**Cliquez sur Ajouter un partage de fichiers** :</span><span class="sxs-lookup"><span data-stu-id="7aa72-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="7aa72-116">![Cliquez sur hello ajouter le bouton de partage de fichier](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="7aa72-116">![Click hello add file share button](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="7aa72-117">**Indiquez le nom et le quota. Actuellement, la limite de quota maximum est 5 To** :</span><span class="sxs-lookup"><span data-stu-id="7aa72-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="7aa72-118">![Fournir un nom et un quota de votre choix pour le nouveau partage de fichiers hello](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="7aa72-118">![Provide a name and a desired quota for hello new file share](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="7aa72-119">**Affichez votre nouveau partage de fichiers** : ![Affichez votre nouveau partage de fichiers](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="7aa72-119">**View your new file share**:  ![View your new file share](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="7aa72-120">**Importez un fichier** : ![Importez un fichier](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="7aa72-120">**Upload a file**:  ![Upload a file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="7aa72-121">**Parcourez le partage de fichiers et gérez vos répertoires et vos fichiers** : ![Parcourez le partage de fichiers](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="7aa72-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="7aa72-122">Création d’un partage de fichiers via PowerShell</span><span class="sxs-lookup"><span data-stu-id="7aa72-122">Create file share through PowerShell</span></span>
<span data-ttu-id="7aa72-123">tooprepare toouse PowerShell, téléchargez et installez les applets de commande PowerShell Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7aa72-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="7aa72-124">Consultez [comment tooinstall et configurer Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) Pourquoi installer instructions d’installation et de point.</span><span class="sxs-lookup"><span data-stu-id="7aa72-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="7aa72-125">Il est recommandé de télécharger et installer ou mettre à niveau du module Azure PowerShell toohello plus récent.</span><span class="sxs-lookup"><span data-stu-id="7aa72-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="7aa72-126">**Créer un contexte pour votre compte de stockage et de la clé** contexte de hello encapsule la clé de compte et le nom du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="7aa72-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="7aa72-127">Pour obtenir des instructions sur la copie de votre clé de compte à partir du [portail Azure](https://portal.azure.com/), voir [Afficher et copier les clés d’accès de stockage](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="7aa72-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="7aa72-128">**Créez un nouveau partage de fichiers** :</span><span class="sxs-lookup"><span data-stu-id="7aa72-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="7aa72-129">nom de Hello de votre partage de fichiers doit être tout en minuscules.</span><span class="sxs-lookup"><span data-stu-id="7aa72-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="7aa72-130">Pour plus d’informations sur la façon de nommer des partages de fichiers et des fichiers, consultez la rubrique [Affectation de noms et références aux partages, répertoires, fichiers et métadonnées](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="7aa72-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="7aa72-131">Création d’un partage de fichiers via l’Interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="7aa72-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="7aa72-132">**tooprepare toouse une Interface de ligne de commande (CLI), téléchargez et installez les hello CLI d’Azure.**</span><span class="sxs-lookup"><span data-stu-id="7aa72-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="7aa72-133">Consultez [Installation d’Azure CLI 2.0](/cli/azure/install-az-cli2.md) et [Prise en main d’Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7aa72-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="7aa72-134">**Créer un compte de stockage de chaîne de connexion toohello où vous souhaitez partager de hello toocreate.**</span><span class="sxs-lookup"><span data-stu-id="7aa72-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="7aa72-135">Remplacez ```<storage-account>``` et ```<resource_group>``` avec votre compte nom et la ressource de groupe de stockage Bonjour l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="7aa72-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="7aa72-136">**Créez le partage de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="7aa72-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="7aa72-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7aa72-137">Next steps</span></span>
* [<span data-ttu-id="7aa72-138">Connexion et montage du partage de fichiers – Windows</span><span class="sxs-lookup"><span data-stu-id="7aa72-138">Connect and Mount File Share - Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="7aa72-139">Connexion et montage du partage de fichiers – Linux</span><span class="sxs-lookup"><span data-stu-id="7aa72-139">Connect and Mount File Share - Linux</span></span>](../storage-how-to-use-files-linux.md)
* [<span data-ttu-id="7aa72-140">Connexion et montage du partage de fichiers – MacOS</span><span class="sxs-lookup"><span data-stu-id="7aa72-140">Connect and Mount File Share - macOS</span></span>](storage-how-to-use-files-mac.md)

<span data-ttu-id="7aa72-141">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="7aa72-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="7aa72-142">FAQ</span><span class="sxs-lookup"><span data-stu-id="7aa72-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="7aa72-143">Résolution des problèmes sur Windows</span><span class="sxs-lookup"><span data-stu-id="7aa72-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="7aa72-144">Résolution des problèmes sur Linux</span><span class="sxs-lookup"><span data-stu-id="7aa72-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   