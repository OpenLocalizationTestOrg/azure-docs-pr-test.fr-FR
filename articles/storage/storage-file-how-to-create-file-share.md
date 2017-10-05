---
title: "Création d’un partage de fichiers Azure | Microsoft Docs"
description: "Comment créer un partage de fichiers Azure dans le Stockage Fichier Azure à l’aide du portail Azure, de PowerShell et de l’interface de ligne de commande Azure CLI."
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
ms.openlocfilehash: 10da4d903eaab290a6cca2c4f674548a43a70c53
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="daacd-103">Création d’un partage de fichiers dans le Stockage Fichier Azure</span><span class="sxs-lookup"><span data-stu-id="daacd-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="daacd-104">Vous pouvez créer des partages de fichiers Azure à l’aide du [portail Azure](https://portal.azure.com/), des applets de commande PowerShell pour Stockage Azure, des bibliothèques clientes Stockage Azure ou de l’API REST de Stockage Azure. Ce didacticiel contient des informations concernant les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="daacd-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), the Azure Storage PowerShell cmdlets, the Azure Storage client libraries, or the Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="daacd-105">Création d’un partage de fichiers Azure avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="daacd-105">How to create an Azure File share using the Azure portal</span></span>](#Create file share through the Portal)
* [<span data-ttu-id="daacd-106">Création d’un partage de fichiers Azure avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="daacd-106">How to create an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="daacd-107">Création d’un partage de fichiers Azure avec CLI</span><span class="sxs-lookup"><span data-stu-id="daacd-107">How to create an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="daacd-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="daacd-108">Prerequisites</span></span>
<span data-ttu-id="daacd-109">Pour créer un partage de fichiers Azure, vous pouvez utiliser un compte de stockage existant ou [créer un nouveau compte de stockage Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="daacd-109">To create an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](storage-create-storage-account.md).</span></span> <span data-ttu-id="daacd-110">Pour créer un partage de fichiers Azure avec PowerShell, vous avez besoin de la clé de compte et du nom de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="daacd-110">To create an Azure File share with PowerShell, you will need the account key and name of your storage account..</span></span> <span data-ttu-id="daacd-111">Si vous envisagez d’utiliser Powershell ou CLI, vous aurez besoin de la clé du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="daacd-111">You will need Storage account key if you plan to use Powershell or CLI.</span></span>

## <a name="create-file-share-through-the-portal"></a><span data-ttu-id="daacd-112">Création d’un partage de fichiers via le portail</span><span class="sxs-lookup"><span data-stu-id="daacd-112">Create file share through the Portal</span></span>
1. <span data-ttu-id="daacd-113">**Accédez au panneau Compte de stockage dans le portail Azure** :</span><span class="sxs-lookup"><span data-stu-id="daacd-113">**Go to Storage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="daacd-114">![Panneau Compte de stockage](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="daacd-114">![Storage Account Blade](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="daacd-115">**Cliquez sur Ajouter un partage de fichiers** :</span><span class="sxs-lookup"><span data-stu-id="daacd-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="daacd-116">![Cliquez sur Ajouter un partage de fichiers](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="daacd-116">![Click the add file share button](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="daacd-117">**Indiquez le nom et le quota. Actuellement, la limite de quota maximum est 5 To** :</span><span class="sxs-lookup"><span data-stu-id="daacd-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="daacd-118">![Indiquez un nom et le quota souhaité pour le nouveau partage de fichiers](media/storage-file-how-to-create-file-share/create-file-share-portal3.png).</span><span class="sxs-lookup"><span data-stu-id="daacd-118">![Provide a name and a desired quota for the new file share](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="daacd-119">**Affichez votre nouveau partage de fichiers** : ![Affichez votre nouveau partage de fichiers](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="daacd-119">**View your new file share**:  ![View your new file share](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="daacd-120">**Importez un fichier** : ![Importez un fichier](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="daacd-120">**Upload a file**:  ![Upload a file](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="daacd-121">**Parcourez le partage de fichiers et gérez vos répertoires et vos fichiers** : ![Parcourez le partage de fichiers](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="daacd-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="daacd-122">Création d’un partage de fichiers via PowerShell</span><span class="sxs-lookup"><span data-stu-id="daacd-122">Create file share through PowerShell</span></span>
<span data-ttu-id="daacd-123">Pour vous préparer à utiliser PowerShell, téléchargez et installez les applets de commande PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="daacd-123">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="daacd-124">Consultez la rubrique [Installation et configuration d’Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) pour des instructions sur l’installation et le point d’installation.</span><span class="sxs-lookup"><span data-stu-id="daacd-124">See [How to install and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for the install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="daacd-125">Il est recommandé de télécharger et d’installer le dernier module Azure PowerShell ou d’effectuer une mise à niveau vers celui-ci.</span><span class="sxs-lookup"><span data-stu-id="daacd-125">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="daacd-126">**Créez un contexte pour le compte de stockage et la clé**. Le contexte regroupe la clé de compte et le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="daacd-126">**Create a context for your storage account and key** The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="daacd-127">Pour obtenir des instructions sur la copie de votre clé de compte à partir du [portail Azure](https://portal.azure.com/), voir [Afficher et copier les clés d’accès de stockage](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="daacd-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="daacd-128">**Créez un nouveau partage de fichiers** :</span><span class="sxs-lookup"><span data-stu-id="daacd-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="daacd-129">Le nom de votre partage de fichiers doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="daacd-129">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="daacd-130">Pour plus d’informations sur la façon de nommer des partages de fichiers et des fichiers, consultez la rubrique [Affectation de noms et références aux partages, répertoires, fichiers et métadonnées](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="daacd-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="daacd-131">Création d’un partage de fichiers via l’Interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="daacd-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="daacd-132">**Pour vous préparer à utiliser une Interface de ligne de commande (CLI), téléchargez et installez Azure CLI.**</span><span class="sxs-lookup"><span data-stu-id="daacd-132">**To prepare to use a Command Line Interface (CLI), download and install the Azure CLI.**</span></span>  
    <span data-ttu-id="daacd-133">Consultez [Installation d’Azure CLI 2.0](/cli/azure/install-az-cli2.md) et [Prise en main d’Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="daacd-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="daacd-134">**Créez une chaîne de connexion vers le compte de stockage dans lequel vous souhaitez créer le partage.**</span><span class="sxs-lookup"><span data-stu-id="daacd-134">**Create a connection string to the storage account where you want to create the share.**</span></span>  
    <span data-ttu-id="daacd-135">Remplacez ```<storage-account>``` et ```<resource_group>``` par le nom de votre compte de stockage et le groupe de ressources de l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="daacd-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in the following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve the connection string."
    fi
    ```

3. <span data-ttu-id="daacd-136">**Créez le partage de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="daacd-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="daacd-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="daacd-137">Next steps</span></span>
* [<span data-ttu-id="daacd-138">Connexion et montage du partage de fichiers – Windows</span><span class="sxs-lookup"><span data-stu-id="daacd-138">Connect and Mount File Share - Windows</span></span>](storage-file-how-to-use-files-windows.md)
* [<span data-ttu-id="daacd-139">Connexion et montage du partage de fichiers – Linux</span><span class="sxs-lookup"><span data-stu-id="daacd-139">Connect and Mount File Share - Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="daacd-140">Connexion et montage du partage de fichiers – MacOS</span><span class="sxs-lookup"><span data-stu-id="daacd-140">Connect and Mount File Share - macOS</span></span>](storage-file-how-to-use-files-mac.md)

<span data-ttu-id="daacd-141">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="daacd-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="daacd-142">FAQ</span><span class="sxs-lookup"><span data-stu-id="daacd-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="daacd-143">Dépannage</span><span class="sxs-lookup"><span data-stu-id="daacd-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)