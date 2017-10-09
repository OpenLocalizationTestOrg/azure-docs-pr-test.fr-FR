---
title: aaaTools pour le stockage de la pile de Azure
description: "En savoir plus sur les outils de transfert de données du stockage Azure Stack"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/16/2017
ms.author: xiaofmao
ms.openlocfilehash: 184a1a51b4267e913aae823df31df3704d8e7b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tools-for-azure-stack-storage"></a><span data-ttu-id="b25b3-103">Outils du stockage Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b25b3-103">Tools for Azure Stack Storage</span></span>

<span data-ttu-id="b25b3-104">Pile de Microsoft Azure fournit un ensemble de services de stockage hello pour les disques, les objets BLOB, les tables, les files d’attente et les fonctionnalités de gestion de compte.</span><span class="sxs-lookup"><span data-stu-id="b25b3-104">Microsoft Azure Stack provides a set of hello storage services for disks, blobs, tables, queues, and account management functionality.</span></span> <span data-ttu-id="b25b3-105">Vous pouvez utiliser un ensemble d’outils de stockage Azure si vous souhaitez toomanage ou déplacez des données tooor depuis le stockage Azure pile.</span><span class="sxs-lookup"><span data-stu-id="b25b3-105">You can use a set of Azure Storage tools if you want toomanage or move data tooor from Azure Stack Storage.</span></span> <span data-ttu-id="b25b3-106">Cet article fournit une vue d’ensemble rapide des outils hello disponibles.</span><span class="sxs-lookup"><span data-stu-id="b25b3-106">This article provides a quick overview of hello tools available.</span></span>

<span data-ttu-id="b25b3-107">outil Hello qui vous convient le mieux varie selon vos besoins :</span><span class="sxs-lookup"><span data-stu-id="b25b3-107">hello tool that works best for you depends on your requirements:</span></span>
* [<span data-ttu-id="b25b3-108">AZCopy</span><span class="sxs-lookup"><span data-stu-id="b25b3-108">AzCopy</span></span>](#azcopy)

    <span data-ttu-id="b25b3-109">Utilitaire de ligne de commande spécifiques au stockage que vous pouvez télécharger les données toocopy à partir d’un objet tooanother dans votre compte de stockage, ou entre des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="b25b3-109">A storage-specific command-line utility that you can download toocopy data from one object tooanother within your storage account, or between storage accounts.</span></span>

* [<span data-ttu-id="b25b3-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b25b3-110">Azure PowerShell</span></span>](#azure-powershell)

    <span data-ttu-id="b25b3-111">Interpréteur de ligne de commande basé sur les tâches et langage de génération de scripts conçu spécialement pour l’administration de systèmes.</span><span class="sxs-lookup"><span data-stu-id="b25b3-111">A task-based command-line shell and scripting language designed especially for system administration.</span></span>

* [<span data-ttu-id="b25b3-112">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="b25b3-112">Azure CLI</span></span>](#azure-cli)

    <span data-ttu-id="b25b3-113">Un outil open source, multiplateforme qui fournit un ensemble de commandes pour travailler avec les plateformes d’Azure et Azure pile hello.</span><span class="sxs-lookup"><span data-stu-id="b25b3-113">An open-source, cross-platform tool that provides a set of commands for working with hello Azure and Azure Stack platforms.</span></span>

* [<span data-ttu-id="b25b3-114">Explorateur Stockage Microsoft (préversion)</span><span class="sxs-lookup"><span data-stu-id="b25b3-114">Microsoft Storage Explorer (Preview)</span></span>](#microsoft-azure-storage-explorer)

    <span data-ttu-id="b25b3-115">Une application autonome toouse simple avec une interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b25b3-115">An easy toouse standalone app with a user interface.</span></span>

<span data-ttu-id="b25b3-116">En raison de différences de services toohello stockage entre Azure et Azure pile, il peut y avoir certaines exigences de chaque outil décrit dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="b25b3-116">Due toohello Storage services differences between Azure and Azure Stack, there might be some specific requirements for each tool described in hello following sections.</span></span> <span data-ttu-id="b25b3-117">Pour une comparaison entre le stockage Azure et le stockage Azure Stack, consultez [Stockage Azure Stack : Différences et considérations](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="b25b3-117">For a comparison between Azure Stack storage and Azure storage, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>


## <a name="azcopy"></a><span data-ttu-id="b25b3-118">AzCopy</span><span class="sxs-lookup"><span data-stu-id="b25b3-118">AzCopy</span></span>
<span data-ttu-id="b25b3-119">AzCopy est un tooand de données toocopy utilitaire de ligne de commande conçu à partir du stockage d’objets Blob Microsoft Azure et de Table à l’aide de commandes simples avec des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="b25b3-119">AzCopy is a command-line utility designed toocopy data tooand from Microsoft Azure Blob and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="b25b3-120">Vous pouvez copier des données à partir d’un objet tooanother dans votre compte de stockage, ou entre des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="b25b3-120">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span> <span data-ttu-id="b25b3-121">Il existe deux versions de hello AzCopy : AzCopy sur Windows et AzCopy sur Linux.</span><span class="sxs-lookup"><span data-stu-id="b25b3-121">There are two version of hello AzCopy: AzCopy on Windows and AzCopy on Linux.</span></span> <span data-ttu-id="b25b3-122">Pile Azure prend uniquement en charge la version de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="b25b3-122">Azure Stack only supports hello Windows version.</span></span> 
 
### <a name="download-and-install-azcopy"></a><span data-ttu-id="b25b3-123">Téléchargement et installation d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="b25b3-123">Download and install AzCopy</span></span> 
<span data-ttu-id="b25b3-124">[Télécharger](https://aka.ms/azcopyforazurestack) version de Windows hello pris en charge de AzCopy pour la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="b25b3-124">[Download](https://aka.ms/azcopyforazurestack) hello supported Windows version of AzCopy for Azure Stack.</span></span> <span data-ttu-id="b25b3-125">Vous pouvez installer et utiliser AzCopy sur hello de pile de Azure comme Azure.</span><span class="sxs-lookup"><span data-stu-id="b25b3-125">You can install and use AzCopy on Azure Stack hello same way as Azure.</span></span> <span data-ttu-id="b25b3-126">toolearn, voir [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="b25b3-126">toolearn more, see [Transfer data with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="azcopy-command-examples-for-data-transfer"></a><span data-ttu-id="b25b3-127">Exemples de commandes AzCopy pour le transfert de données</span><span class="sxs-lookup"><span data-stu-id="b25b3-127">AzCopy command examples for data transfer</span></span>
<span data-ttu-id="b25b3-128">Hello suivant exemples montrent quelques scénarios classiques pour la copie des données tooand à partir de la pile d’Azure BLOB.</span><span class="sxs-lookup"><span data-stu-id="b25b3-128">hello following examples demonstrate a few typical scenarios for copying data tooand from Azure Stack blobs.</span></span> <span data-ttu-id="b25b3-129">toolearn, voir [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](../storage/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="b25b3-129">toolearn more, see [Transfer data with hello AzCopy Command-Line Utility](../storage/storage-use-azcopy.md).</span></span> 
#### <a name="download-all-blobs-toolocal-disk"></a><span data-ttu-id="b25b3-130">Téléchargez le disque de toolocal tous les objets BLOB</span><span class="sxs-lookup"><span data-stu-id="b25b3-130">Download all blobs toolocal disk</span></span>
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="b25b3-131">Téléchargement de fichier unique toovirtual Active</span><span class="sxs-lookup"><span data-stu-id="b25b3-131">Upload single file toovirtual directory</span></span> 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a><span data-ttu-id="b25b3-132">Déplacer des données entre le stockage Azure et Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b25b3-132">Move data between Azure and Azure Stack Storage</span></span> 
<span data-ttu-id="b25b3-133">Le transfert de données asynchrone entre le stockage Azure et Azure Stack n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b25b3-133">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="b25b3-134">vous avez besoin de transfert de hello toospecify avec hello `/SyncCopy` option.</span><span class="sxs-lookup"><span data-stu-id="b25b3-134">you need toospecify hello transfer with hello `/SyncCopy` option.</span></span> 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a><span data-ttu-id="b25b3-135">Problèmes connus d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="b25b3-135">Azcopy Known issues</span></span>
* <span data-ttu-id="b25b3-136">Toute opération AzCopy sur le stockage Fichier n’est pas disponible, car le stockage Fichier n’est pas encore disponible dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b25b3-136">Any AzCopy operation on File storage is not available because File Storage is not yet available in Azure Stack.</span></span>
* <span data-ttu-id="b25b3-137">Le transfert de données asynchrone entre le stockage Azure et Azure Stack n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b25b3-137">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="b25b3-138">Vous pouvez spécifier hello transfert avec hello `/SyncCopy` option toocopy les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="b25b3-138">You can specify hello transfer with hello `/SyncCopy` option toocopy hello data.</span></span>
* <span data-ttu-id="b25b3-139">version de Linux Hello de Azcopy n’est pas prise en charge pour le stockage Azure pile.</span><span class="sxs-lookup"><span data-stu-id="b25b3-139">hello Linux version of Azcopy is not supported for Azure Stack Storage.</span></span> 

## <a name="azure-powershell"></a><span data-ttu-id="b25b3-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b25b3-140">Azure PowerShell</span></span>
<span data-ttu-id="b25b3-141">Le module Azure PowerShell fournit des applets de commande pour gérer des services sur Azure et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b25b3-141">Azure PowerShell is a module that provides cmdlets for managing services on both Azure and Azure Stack.</span></span> <span data-ttu-id="b25b3-142">Il s’agit d’un interpréteur en ligne de commande basé sur les tâches et d’un langage de génération de scripts conçu spécialement pour l’administration de systèmes.</span><span class="sxs-lookup"><span data-stu-id="b25b3-142">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

### <a name="install-and-configure-powershell-for-azure-stack"></a><span data-ttu-id="b25b3-143">Installer et configurer PowerShell pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b25b3-143">Install and Configure PowerShell for Azure Stack</span></span>
<span data-ttu-id="b25b3-144">Les modules Azure PowerShell compatibles pile Azure sont requis toowork avec la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="b25b3-144">Azure Stack compatible Azure PowerShell modules are required toowork with Azure Stack.</span></span> <span data-ttu-id="b25b3-145">Pour plus d’informations, consultez [installer PowerShell pour Azure pile](azure-stack-powershell-install.md) et [configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell](azure-stack-powershell-configure-user.md) toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="b25b3-145">For more information, see [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) and [Configure hello Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) toolearn more.</span></span>

### <a name="powershell-sample-script-for-azure-stack"></a><span data-ttu-id="b25b3-146">Exemple de script PowerShell pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b25b3-146">PowerShell Sample script for Azure Stack</span></span> 
<span data-ttu-id="b25b3-147">Cet exemple suppose que vous avez [installé PowerShell pour Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="b25b3-147">This sample assume you have successfully [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> <span data-ttu-id="b25b3-148">Ce script vous permet de configuration de hello conplete et demandez à que votre client Azure pile des informations d’identification tooadd votre environnement de PowerShell compte toohello local.</span><span class="sxs-lookup"><span data-stu-id="b25b3-148">This script will help you conplete hello configuration and ask your Azure Stack tenant credentials tooadd your account toohello local PowerShell environemnt.</span></span> <span data-ttu-id="b25b3-149">Ensuite, hello script définir la valeur par défaut de hello abonnement Azure, créez un compte de stockage dans Azure, créer un nouveau conteneur dans ce nouveau compte de stockage et télécharger un conteneur de toothat (blob) de fichier image existant.</span><span class="sxs-lookup"><span data-stu-id="b25b3-149">Then, hello script will set hello default Azure subscription, create a new storage account in Azure, create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="b25b3-150">Une fois le script de hello répertorie tous les objets BLOB dans le conteneur, elle crée un nouveau répertoire de destination dans votre ordinateur local et télécharger le fichier d’image hello.</span><span class="sxs-lookup"><span data-stu-id="b25b3-150">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>

1. <span data-ttu-id="b25b3-151">Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="b25b3-151">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
2. <span data-ttu-id="b25b3-152">Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="b25b3-152">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  
3. <span data-ttu-id="b25b3-153">Ouvrez **Windows PowerShell ISE** et **exécuter en tant qu’administrateur**, cliquez sur **fichier** > **nouveau** toocreate un fichier de script.</span><span class="sxs-lookup"><span data-stu-id="b25b3-153">Open **Windows PowerShell ISE** and **Run as Administrator**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="b25b3-154">Copiez le script ci-dessous hello et collez le nouveau fichier de script toohello.</span><span class="sxs-lookup"><span data-stu-id="b25b3-154">Copy hello script below and paste toohello new script file.</span></span>
5. <span data-ttu-id="b25b3-155">Mettre à jour les variables de script hello en fonction de vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="b25b3-155">Update hello script variables based on your configuration settings.</span></span> 
6. <span data-ttu-id="b25b3-156">Remarque : ce script a toobe s’exécutent sous la racine hello téléchargé **AzureStack_Tools**.</span><span class="sxs-lookup"><span data-stu-id="b25b3-156">Note: this script has toobe run under hello root of downloaded **AzureStack_Tools**.</span></span> 

```PowerShell 
# begin

$ARMEvnName = "AzureStackUser" # set AzureStackUser as your Azure Stack environemnt name
$ARMEndPoint = "https://management.local.azurestack.external" 
$GraphAudiance = "https://graph.windows.net/" 
$AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com" 

$SubscriptionName = "basic" # Update with hello name of your subscription.
$ResourceGroupName = "myTestRG" # Give a name tooyour new resource group.
$StorageAccountName = "azsblobcontainer" # Give a name tooyour new storage account. It must be lowercase!
$Location = "Local" # Choose "Local" as an example.
$ContainerName = "photo" # Give a name tooyour new container.
$ImageToUpload = "C:\temp\Hello.jpg" # Prepare an image file and a source directory in your local computer.
$DestinationFolder = "C:\temp\downlaod" # A destination directory in your local computer.

# Import hello Connect PowerShell module"
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Import-Module .\Connect\AzureStack.Connect.psm1

# Configure hello PowerShell environment
# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRmEnvironment -Name $ARMEvnName -ARMEndpoint $ARMEndPoint 

# Set hello GraphEndpointResourceId value
Set-AzureRmEnvironment -Name $ARMEvnName -GraphEndpoint $GraphAudiance

# Login
$TenantID = Get-AzsDirectoryTenantId -AADTenantName $AADTenantName -EnvironmentName $ARMEvnName
Login-AzureRmAccount -EnvironmentName $ARMEvnName -TenantId $TenantID 

# Set a default Azure subscription.
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Create a new Resource Group 
New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

# Create a new storage account.
New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS

# Set a default storage account.
Set-AzureRmCurrentStorageAccount -StorageAccountName $StorageAccountName -ResourceGroupName $ResourceGroupName 

# Create a new container.
New-AzureStorageContainer -Name $ContainerName -Permission Off

# Upload a blob into a container.
Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload

# List all blobs in a container.
Get-AzureStorageBlob -Container $ContainerName

# Download blobs from hello container:
# Get a reference tooa list of all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName

# Create hello destination directory.
New-Item -Path $DestinationFolder -ItemType Directory -Force  

# Download blobs into hello local destination directory.
$blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder

# end
```

### <a name="powershell-known-issues"></a><span data-ttu-id="b25b3-157">Problèmes connus de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b25b3-157">PowerShell Known Issues</span></span> 
<span data-ttu-id="b25b3-158">Hello actuel compatible Azure PowerShell version du module pour la pile de Azure est 1.2.10.</span><span class="sxs-lookup"><span data-stu-id="b25b3-158">hello current compatible Azure PowerShell module version for Azure Stack is 1.2.10.</span></span> <span data-ttu-id="b25b3-159">Il est différent de la version la plus récente d’Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="b25b3-159">It’s different from hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="b25b3-160">Cette différence impacte le fonctionnement des services de stockage :</span><span class="sxs-lookup"><span data-stu-id="b25b3-160">This difference impacts storage services operation:</span></span>

* <span data-ttu-id="b25b3-161">format de valeur de retour Hello de `Get-AzureRmStorageAccountKey` dans la version 1.2.10 a deux propriétés : `Key1` et `Key2`, alors que la version de Microsoft Azure actuel hello retourne un tableau contenant toutes les clés de compte hello.</span><span class="sxs-lookup"><span data-stu-id="b25b3-161">hello return value format of `Get-AzureRmStorageAccountKey` in version 1.2.10 has two properties: `Key1` and `Key2`, while hello current Azure version returns an array containing all hello account keys.</span></span>
   ```
   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.4, and later versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Value[0]

   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.3.2, and previous versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Key1

   ```
   <span data-ttu-id="b25b3-162">Pour plus d’informations, consultez [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="b25b3-162">For more information, see [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span></span>

## <a name="azure-cli"></a><span data-ttu-id="b25b3-163">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="b25b3-163">Azure CLI</span></span>
<span data-ttu-id="b25b3-164">Hello CLI d’Azure est de Azure en ligne de commande pour la gestion des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b25b3-164">hello Azure CLI is Azure’s command-line experience for managing Azure resources.</span></span> <span data-ttu-id="b25b3-165">Vous pouvez l’installer sur Windows, Linux et macOS et exécutez-le à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="b25b3-165">You can install it on macOS, Linux, and Windows and run it from hello command line.</span></span> 

<span data-ttu-id="b25b3-166">CLI Azure est optimisé pour gérer et administrer les ressources Azure à partir de la ligne de commande hello et de créer des scripts d’automatisation qui fonctionnent sur hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b25b3-166">Azure CLI is optimized for managing and administering Azure resources from hello command line, and for building automation scripts that work against hello Azure Resource Manager.</span></span> <span data-ttu-id="b25b3-167">Il fournit un grand nombre de hello mêmes fonctions trouvées dans le portail Azure pile hello, y compris l’accès aux données enrichi.</span><span class="sxs-lookup"><span data-stu-id="b25b3-167">It provides many of hello same functions found in hello Azure Stack portal, including rich data access.</span></span>

<span data-ttu-id="b25b3-168">Azure Stack nécessite la version 2.0 d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b25b3-168">Azure Stack requires Azure CLI version 2.0.</span></span> <span data-ttu-id="b25b3-169">Pour plus d’informations sur l’installation et la configuration d’Azure CLI avec Azure Stack, consultez [Installer et configurer Azure Stack CLI](azure-stack-connect-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b25b3-169">For more information about installing and configuring Azure CLI with Azure Stack, see [Install and configure Azure Stack CLI](azure-stack-connect-cli.md).</span></span> <span data-ttu-id="b25b3-170">Pour plus d’informations sur comment toouse hello Azure CLI 2.0 tooperform plusieurs tâches, utilisation des ressources dans votre compte de stockage de pile d’Azure, consultez [Using hello CLI2.0 Azure avec le stockage Azure](../storage/storage-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b25b3-170">For more information about how toouse hello Azure CLI 2.0 tooperform several tasks working with resources in your Azure Stack Storage account, see [Using hello Azure CLI2.0 with Azure Storage](../storage/storage-azure-cli.md)</span></span>

### <a name="azure-cli-sample-script-for-azure-stack"></a><span data-ttu-id="b25b3-171">Exemple de script Azure CLI pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b25b3-171">Azure CLI sample script for Azure Stack</span></span> 
<span data-ttu-id="b25b3-172">Après avoir terminé l’installation du CLI hello et la configuration, vous pouvez essayer hello suivant toowork étapes avec un toointeract de script shell petit exemple avec les ressources de stockage de pile Azure.</span><span class="sxs-lookup"><span data-stu-id="b25b3-172">Once you complete hello CLI installation and configuration, you can try hello following steps toowork with a small shell sample script toointeract with Azure Stack Storage resources.</span></span> <span data-ttu-id="b25b3-173">script de Hello crée d’abord un nouveau conteneur dans votre compte de stockage, puis télécharge un conteneur existant pour le fichier (comme un objet blob) toothat répertorie tous les objets BLOB dans le conteneur de hello et enfin, télécharge destination de tooa hello fichier sur votre ordinateur local que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="b25b3-173">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container, lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span> <span data-ttu-id="b25b3-174">Avant d’exécuter ce script, assurez-vous que vous êtes connecté et connexion toohello cible Azure pile.</span><span class="sxs-lookup"><span data-stu-id="b25b3-174">Before you run this script, make sure you successfully connect and login toohello target Azure Stack.</span></span> 
1. <span data-ttu-id="b25b3-175">Ouvrez l’éditeur de texte, puis copier- coller hello précédant le script dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="b25b3-175">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>
2. <span data-ttu-id="b25b3-176">Mettre à jour tooreflect de variables de script hello vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="b25b3-176">Update hello script's variables tooreflect your configuration settings.</span></span> 
3. <span data-ttu-id="b25b3-177">Une fois que vous avez mis à jour les variables nécessaires hello, enregistrer le script de hello et quittez l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="b25b3-177">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="b25b3-178">les étapes suivantes Hello supposent que vous avez nommé votre my_storage_sample.sh de script.</span><span class="sxs-lookup"><span data-stu-id="b25b3-178">hello next steps assume you've named your script my_storage_sample.sh.</span></span>
4. <span data-ttu-id="b25b3-179">Marquer le script hello en tant que fichier exécutable, si nécessaire :`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="b25b3-179">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>
5. <span data-ttu-id="b25b3-180">Exécuter le script de hello.</span><span class="sxs-lookup"><span data-stu-id="b25b3-180">Execute hello script.</span></span> <span data-ttu-id="b25b3-181">Par exemple, dans Bash : `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="b25b3-181">For example, in Bash: `./my_storage_sample.sh`</span></span>

```bash
#!/bin/bash
# A simple Azure Stack Storage example script

export AZURESTACK_RESOURCE_GROUP=<resource_group_name>
export AZURESTACK_RG_LOCATION="local"
export AZURESTACK_STORAGE_ACCOUNT_NAME=<storage_account_name>
export AZURESTACK_STORAGE_CONTAINER_NAME=<container_name>
export AZURESTACK_STORAGE_BLOB_NAME=<blob_name>
export FILE_TO_UPLOAD=<file_to_upload>
export DESTINATION_FILE=<destination_file>

echo "Creating hello resource group..."
az group create --name $AZURESTACK_RESOURCE_GROUP --location $AZURESTACK_RG_LOCATION

echo "Creating hello storage account..."
az storage account create --name $AZURESTACK_STORAGE_ACCOUNT_NAME --resource-group $AZURESTACK_RESOURCE_GROUP --account-type Standard_LRS

echo "Creating hello blob container..."
az storage container create --name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Uploading hello file..."
az storage blob upload --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --file $FILE_TO_UPLOAD --name $AZURESTACK_STORAGE_BLOB_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Listing hello blobs..."
az storage blob list --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --output table

echo "Downloading hello file..."
az storage blob download --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --name $AZURESTACK_STORAGE_BLOB_NAME --file $DESTINATION_FILE --output table

echo "Done"
```

## <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="b25b3-182">Explorateur Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b25b3-182">Microsoft Azure Storage Explorer</span></span>

<span data-ttu-id="b25b3-183">L’Explorateur Stockage Microsoft Azure est une application autonome de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b25b3-183">Microsoft Azure Storage Explorer is a standalone app from Microsoft.</span></span> <span data-ttu-id="b25b3-184">Il vous permet de travail tooeasily avec les données de stockage Azure et Azure pile de stockage sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="b25b3-184">It allows you tooeasily work with both Azure Storage and Azure Stack Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="b25b3-185">Si vous souhaitez un toomanage facilement les données de votre stockage de pile Azure, envisagez d’utiliser l’Explorateur de stockage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b25b3-185">If you want an easy way toomanage your Azure Stack Storage data, then consider using Microsoft Azure Storage Explorer.</span></span>

<span data-ttu-id="b25b3-186">Pour plus d’informations sur la configuration d’Azure Storage Explorer toowork avec la pile d’Azure, consultez [connecter l’Explorateur de stockage tooan abonnement de Azure pile](azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="b25b3-186">For more information about configuring Azure Storage Explorer toowork with Azure Stack, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack-storage-connect-se.md).</span></span>

<span data-ttu-id="b25b3-187">Pour plus d’informations sur l’Explorateur Stockage Microsoft Azure, consultez [Bien démarrer avec l’Explorateur Stockage (préversion)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span><span class="sxs-lookup"><span data-stu-id="b25b3-187">For more information about Microsoft Azure Storage Explorer, see [Get started with Storage Explorer (Preview)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b25b3-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b25b3-188">Next steps</span></span>
* [<span data-ttu-id="b25b3-189">Connecter l’Explorateur de stockage tooan Azure pile abonnement</span><span class="sxs-lookup"><span data-stu-id="b25b3-189">Connect Storage Explorer tooan Azure Stack subscription</span></span>](azure-stack-storage-connect-se.md)
* [<span data-ttu-id="b25b3-190">Bien démarrer avec l’Explorateur Stockage (préversion)</span><span class="sxs-lookup"><span data-stu-id="b25b3-190">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="b25b3-191">Stockage Azure : Différences et considérations</span><span class="sxs-lookup"><span data-stu-id="b25b3-191">Azure-consistent storage: differences and considerations</span></span>](azure-stack-acs-differences.md)
* [<span data-ttu-id="b25b3-192">Introduction tooMicrosoft stockage Azure</span><span class="sxs-lookup"><span data-stu-id="b25b3-192">Introduction tooMicrosoft Azure Storage</span></span>](../storage/common/storage-introduction.md)

