---
title: Outils du stockage Azure Stack
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
ms.date: 9/25/2017
ms.author: xiaofmao
ms.openlocfilehash: 9799498a11449a9ed496d0fdb40312603eda064e
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="tools-for-azure-stack-storage"></a><span data-ttu-id="58b2c-103">Outils du stockage Azure Stack</span><span class="sxs-lookup"><span data-stu-id="58b2c-103">Tools for Azure Stack Storage</span></span>

<span data-ttu-id="58b2c-104">*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="58b2c-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="58b2c-105">Microsoft Azure Stack fournit un ensemble de services de stockage pour les disques, les objets blob, les tables, les files d’attente, ainsi que des fonctionnalités de gestion de compte.</span><span class="sxs-lookup"><span data-stu-id="58b2c-105">Microsoft Azure Stack provides a set of the storage services for disks, blobs, tables, queues, and account management functionality.</span></span> <span data-ttu-id="58b2c-106">Vous pouvez utiliser un ensemble d’outils de stockage Azure si vous voulez gérer des données ou les déplacer vers ou à partir du stockage Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="58b2c-106">You can use a set of Azure Storage tools if you want to manage or move data to or from Azure Stack Storage.</span></span> <span data-ttu-id="58b2c-107">Cet article fournit une vue d’ensemble rapide des outils disponibles.</span><span class="sxs-lookup"><span data-stu-id="58b2c-107">This article provides a quick overview of the tools available.</span></span>

<span data-ttu-id="58b2c-108">L’outil qui vous convient le mieux dépend de vos besoins :</span><span class="sxs-lookup"><span data-stu-id="58b2c-108">The tool that works best for you depends on your requirements:</span></span>
* [<span data-ttu-id="58b2c-109">AZCopy</span><span class="sxs-lookup"><span data-stu-id="58b2c-109">AzCopy</span></span>](#azcopy)

    <span data-ttu-id="58b2c-110">Utilitaire de ligne de commande propre au stockage que vous pouvez télécharger pour copier des données d’un objet vers un autre au sein de votre compte de stockage ou entre des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="58b2c-110">A storage-specific command-line utility that you can download to copy data from one object to another within your storage account, or between storage accounts.</span></span>

* [<span data-ttu-id="58b2c-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="58b2c-111">Azure PowerShell</span></span>](#azure-powershell)

    <span data-ttu-id="58b2c-112">Interpréteur de ligne de commande basé sur les tâches et langage de génération de scripts conçu spécialement pour l’administration de systèmes.</span><span class="sxs-lookup"><span data-stu-id="58b2c-112">A task-based command-line shell and scripting language designed especially for system administration.</span></span>

* [<span data-ttu-id="58b2c-113">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="58b2c-113">Azure CLI</span></span>](#azure-cli)

    <span data-ttu-id="58b2c-114">Outil multiplateforme open source qui fournit un ensemble de commandes pour utiliser les plateformes Azure et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="58b2c-114">An open-source, cross-platform tool that provides a set of commands for working with the Azure and Azure Stack platforms.</span></span>

* [<span data-ttu-id="58b2c-115">Explorateur Stockage Microsoft (préversion)</span><span class="sxs-lookup"><span data-stu-id="58b2c-115">Microsoft Storage Explorer (Preview)</span></span>](#microsoft-azure-storage-explorer)

    <span data-ttu-id="58b2c-116">Application autonome, facile à utiliser, avec une interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58b2c-116">An easy to use standalone app with a user interface.</span></span>

<span data-ttu-id="58b2c-117">En raison des différences des services de stockage Azure et Azure Stack, chaque outil décrit dans les sections suivantes peut avoir des exigences spécifiques.</span><span class="sxs-lookup"><span data-stu-id="58b2c-117">Due to the Storage services differences between Azure and Azure Stack, there might be some specific requirements for each tool described in the following sections.</span></span> <span data-ttu-id="58b2c-118">Pour une comparaison entre le stockage Azure et le stockage Azure Stack, consultez [Stockage Azure Stack : Différences et considérations](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="58b2c-118">For a comparison between Azure Stack storage and Azure storage, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>


## <a name="azcopy"></a><span data-ttu-id="58b2c-119">AzCopy</span><span class="sxs-lookup"><span data-stu-id="58b2c-119">AzCopy</span></span>
<span data-ttu-id="58b2c-120">AzCopy est un utilitaire de ligne de commande conçu pour copier des données à partir et vers le stockage Blob et Table Microsoft Azure à l’aide de commandes simples avec des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="58b2c-120">AzCopy is a command-line utility designed to copy data to and from Microsoft Azure Blob and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="58b2c-121">Vous pouvez copier des données d’un objet vers un autre au sein de votre compte de stockage ou entre des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="58b2c-121">You can copy data from one object to another within your storage account, or between storage accounts.</span></span> <span data-ttu-id="58b2c-122">Il existe deux versions d’AzCopy : AzCopy sur Windows et AzCopy sur Linux.</span><span class="sxs-lookup"><span data-stu-id="58b2c-122">There are two version of the AzCopy: AzCopy on Windows and AzCopy on Linux.</span></span> <span data-ttu-id="58b2c-123">Azure Stack prend uniquement en charge la version Windows.</span><span class="sxs-lookup"><span data-stu-id="58b2c-123">Azure Stack only supports the Windows version.</span></span> 
 
### <a name="download-and-install-azcopy"></a><span data-ttu-id="58b2c-124">Téléchargement et installation d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="58b2c-124">Download and install AzCopy</span></span> 
<span data-ttu-id="58b2c-125">[Téléchargez](https://aka.ms/azcopyforazurestack) la version Windows d’AzCopy prise en charge par Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="58b2c-125">[Download](https://aka.ms/azcopyforazurestack) the supported Windows version of AzCopy for Azure Stack.</span></span> <span data-ttu-id="58b2c-126">Vous pouvez installer et utiliser AzCopy sur Azure Stack comme sur Azure.</span><span class="sxs-lookup"><span data-stu-id="58b2c-126">You can install and use AzCopy on Azure Stack the same way as Azure.</span></span> <span data-ttu-id="58b2c-127">Pour en savoir plus, consultez [Transfert de données avec l’utilitaire de ligne de commande AzCopy](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="58b2c-127">To learn more, see [Transfer data with the AzCopy Command-Line Utility](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="azcopy-command-examples-for-data-transfer"></a><span data-ttu-id="58b2c-128">Exemples de commandes AzCopy pour le transfert de données</span><span class="sxs-lookup"><span data-stu-id="58b2c-128">AzCopy command examples for data transfer</span></span>
<span data-ttu-id="58b2c-129">Les exemples suivants montrent différents scénarios permettant de copier des données vers et à partir d’objets blob Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="58b2c-129">The following examples demonstrate a few typical scenarios for copying data to and from Azure Stack blobs.</span></span> <span data-ttu-id="58b2c-130">Pour en savoir plus, consultez [Transfert de données avec l’utilitaire de ligne de commande AzCopy](../../storage/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="58b2c-130">To learn more, see [Transfer data with the AzCopy Command-Line Utility](../../storage/storage-use-azcopy.md).</span></span> 
#### <a name="download-all-blobs-to-local-disk"></a><span data-ttu-id="58b2c-131">Télécharger tous les objets blob sur le disque local</span><span class="sxs-lookup"><span data-stu-id="58b2c-131">Download all blobs to local disk</span></span>
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="58b2c-132">Télécharger un fichier unique dans le répertoire virtuel</span><span class="sxs-lookup"><span data-stu-id="58b2c-132">Upload single file to virtual directory</span></span> 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a><span data-ttu-id="58b2c-133">Déplacer des données entre le stockage Azure et Azure Stack</span><span class="sxs-lookup"><span data-stu-id="58b2c-133">Move data between Azure and Azure Stack Storage</span></span> 
<span data-ttu-id="58b2c-134">Le transfert de données asynchrone entre le stockage Azure et Azure Stack n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="58b2c-134">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="58b2c-135">Vous devez spécifier le transfert avec l’option `/SyncCopy`.</span><span class="sxs-lookup"><span data-stu-id="58b2c-135">you need to specify the transfer with the `/SyncCopy` option.</span></span> 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a><span data-ttu-id="58b2c-136">Problèmes connus d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="58b2c-136">Azcopy Known issues</span></span>
* <span data-ttu-id="58b2c-137">Toute opération AzCopy sur le stockage Fichier n’est pas disponible, car le stockage Fichier n’est pas encore disponible dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="58b2c-137">Any AzCopy operation on File storage is not available because File Storage is not yet available in Azure Stack.</span></span>
* <span data-ttu-id="58b2c-138">Le transfert de données asynchrone entre le stockage Azure et Azure Stack n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="58b2c-138">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="58b2c-139">Vous pouvez spécifier le transfert avec l’option `/SyncCopy` pour copier les données.</span><span class="sxs-lookup"><span data-stu-id="58b2c-139">You can specify the transfer with the `/SyncCopy` option to copy the data.</span></span>
* <span data-ttu-id="58b2c-140">La version Linux d’AzCopy n’est pas prise en charge pour le stockage Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="58b2c-140">The Linux version of Azcopy is not supported for Azure Stack Storage.</span></span> 

## <a name="azure-powershell"></a><span data-ttu-id="58b2c-141">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="58b2c-141">Azure PowerShell</span></span>
<span data-ttu-id="58b2c-142">Le module Azure PowerShell fournit des applets de commande pour gérer des services sur Azure et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="58b2c-142">Azure PowerShell is a module that provides cmdlets for managing services on both Azure and Azure Stack.</span></span> <span data-ttu-id="58b2c-143">Il s’agit d’un interpréteur en ligne de commande basé sur les tâches et d’un langage de génération de scripts conçu spécialement pour l’administration de systèmes.</span><span class="sxs-lookup"><span data-stu-id="58b2c-143">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

### <a name="install-and-configure-powershell-for-azure-stack"></a><span data-ttu-id="58b2c-144">Installer et configurer PowerShell pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="58b2c-144">Install and Configure PowerShell for Azure Stack</span></span>
<span data-ttu-id="58b2c-145">Des modules Azure PowerShell compatibles avec Azure Stack sont nécessaires pour utiliser Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="58b2c-145">Azure Stack compatible Azure PowerShell modules are required to work with Azure Stack.</span></span> <span data-ttu-id="58b2c-146">Pour plus d’informations, consultez [Installer PowerShell pour Azure Stack](azure-stack-powershell-install.md) et [Configurer l’environnement PowerShell de l’utilisateur Azure Stack](azure-stack-powershell-configure-user.md).</span><span class="sxs-lookup"><span data-stu-id="58b2c-146">For more information, see [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) and [Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) to learn more.</span></span>

### <a name="powershell-sample-script-for-azure-stack"></a><span data-ttu-id="58b2c-147">Exemple de script PowerShell pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="58b2c-147">PowerShell Sample script for Azure Stack</span></span> 
<span data-ttu-id="58b2c-148">Cet exemple suppose que vous avez [installé PowerShell pour Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="58b2c-148">This sample assume you have successfully [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> <span data-ttu-id="58b2c-149">Ce script vous permet d’effectuer la configuration et de demander à votre locataire Azure Stack des informations d’identification pour ajouter votre compte à l’environnement PowerShell local.</span><span class="sxs-lookup"><span data-stu-id="58b2c-149">This script will help you conplete the configuration and ask your Azure Stack tenant credentials to add your account to the local PowerShell environemnt.</span></span> <span data-ttu-id="58b2c-150">Ensuite, le script définit l’abonnement Azure par défaut, crée un compte de stockage dans Azure, crée un conteneur dans ce nouveau compte de stockage et charge un fichier image existant (blob) dans ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="58b2c-150">Then, the script will set the default Azure subscription, create a new storage account in Azure, create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="58b2c-151">Une fois que le script répertorie tous les objets blob de ce conteneur, il crée un répertoire de destination sur votre ordinateur local et télécharge le fichier image.</span><span class="sxs-lookup"><span data-stu-id="58b2c-151">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>

1. <span data-ttu-id="58b2c-152">Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="58b2c-152">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
2. <span data-ttu-id="58b2c-153">Téléchargez les [outils nécessaires pour utiliser Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="58b2c-153">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  
3. <span data-ttu-id="58b2c-154">Ouvrez **Windows PowerShell ISE** et **Exécuter en tant qu’administrateur**, cliquez sur **Fichier** > **Nouveau** pour créer un fichier script.</span><span class="sxs-lookup"><span data-stu-id="58b2c-154">Open **Windows PowerShell ISE** and **Run as Administrator**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="58b2c-155">Copiez le script ci-dessous et collez-le dans le nouveau fichier script.</span><span class="sxs-lookup"><span data-stu-id="58b2c-155">Copy the script below and paste to the new script file.</span></span>
5. <span data-ttu-id="58b2c-156">Mettez à jour les variables du script en fonction de vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="58b2c-156">Update the script variables based on your configuration settings.</span></span> 
6. <span data-ttu-id="58b2c-157">Remarque : Ce script doit être exécuté à la racine du **AzureStack_Tools** téléchargé.</span><span class="sxs-lookup"><span data-stu-id="58b2c-157">Note: this script has to be run under the root of downloaded **AzureStack_Tools**.</span></span> 

```PowerShell 
# begin

$ARMEvnName = "AzureStackUser" # set AzureStackUser as your Azure Stack environemnt name
$ARMEndPoint = "https://management.local.azurestack.external" 
$GraphAudiance = "https://graph.windows.net/" 
$AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com" 

$SubscriptionName = "basic" # Update with the name of your subscription.
$ResourceGroupName = "myTestRG" # Give a name to your new resource group.
$StorageAccountName = "azsblobcontainer" # Give a name to your new storage account. It must be lowercase!
$Location = "Local" # Choose "Local" as an example.
$ContainerName = "photo" # Give a name to your new container.
$ImageToUpload = "C:\temp\Hello.jpg" # Prepare an image file and a source directory in your local computer.
$DestinationFolder = "C:\temp\downlaod" # A destination directory in your local computer.

# Import the Connect PowerShell module"
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Import-Module .\Connect\AzureStack.Connect.psm1

# Configure the PowerShell environment
# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRmEnvironment -Name $ARMEvnName -ARMEndpoint $ARMEndPoint 

# Set the GraphEndpointResourceId value
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

# Download blobs from the container:
# Get a reference to a list of all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName

# Create the destination directory.
New-Item -Path $DestinationFolder -ItemType Directory -Force  

# Download blobs into the local destination directory.
$blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder

# end
```

### <a name="powershell-known-issues"></a><span data-ttu-id="58b2c-158">Problèmes connus de PowerShell</span><span class="sxs-lookup"><span data-stu-id="58b2c-158">PowerShell Known Issues</span></span> 
<span data-ttu-id="58b2c-159">La version actuelle du module Azure PowerShell compatible avec Azure Stack est 1.2.10.</span><span class="sxs-lookup"><span data-stu-id="58b2c-159">The current compatible Azure PowerShell module version for Azure Stack is 1.2.10.</span></span> <span data-ttu-id="58b2c-160">Elle est différente de la dernière version d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58b2c-160">It’s different from the latest version of Azure PowerShell.</span></span> <span data-ttu-id="58b2c-161">Cette différence impacte le fonctionnement des services de stockage :</span><span class="sxs-lookup"><span data-stu-id="58b2c-161">This difference impacts storage services operation:</span></span>

* <span data-ttu-id="58b2c-162">Le format de la valeur de retour de `Get-AzureRmStorageAccountKey` dans la version 1.2.10 a deux propriétés : `Key1` et `Key2`, alors que la version actuelle d’Azure retourne un tableau contenant toutes les clés de compte.</span><span class="sxs-lookup"><span data-stu-id="58b2c-162">The return value format of `Get-AzureRmStorageAccountKey` in version 1.2.10 has two properties: `Key1` and `Key2`, while the current Azure version returns an array containing all the account keys.</span></span>
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
   <span data-ttu-id="58b2c-163">Pour plus d’informations, consultez [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="58b2c-163">For more information, see [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span></span>

## <a name="azure-cli"></a><span data-ttu-id="58b2c-164">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="58b2c-164">Azure CLI</span></span>
<span data-ttu-id="58b2c-165">L’interface de ligne de commande Azure (Azure CLI) est l’expérience de ligne de commande d’Azure pour gérer les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="58b2c-165">The Azure CLI is Azure’s command-line experience for managing Azure resources.</span></span> <span data-ttu-id="58b2c-166">Vous pouvez l’installer sur Windows, Linux et macOS, et l’exécuter à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="58b2c-166">You can install it on macOS, Linux, and Windows and run it from the command line.</span></span> 

<span data-ttu-id="58b2c-167">Azure CLI est optimisé pour la gestion et l’administration des ressources Azure à partir de la ligne de commande, et pour la création de scripts d’automatisation qui opèrent sur Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="58b2c-167">Azure CLI is optimized for managing and administering Azure resources from the command line, and for building automation scripts that work against the Azure Resource Manager.</span></span> <span data-ttu-id="58b2c-168">Elle offre de nombreuses fonctionnalités similaires à celles du portail Azure Stack, notamment l’accès étendu aux données.</span><span class="sxs-lookup"><span data-stu-id="58b2c-168">It provides many of the same functions found in the Azure Stack portal, including rich data access.</span></span>

<span data-ttu-id="58b2c-169">Azure Stack nécessite la version 2.0 d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="58b2c-169">Azure Stack requires Azure CLI version 2.0.</span></span> <span data-ttu-id="58b2c-170">Pour plus d’informations sur l’installation et la configuration d’Azure CLI avec Azure Stack, consultez [Installer et configurer Azure Stack CLI](azure-stack-connect-cli.md).</span><span class="sxs-lookup"><span data-stu-id="58b2c-170">For more information about installing and configuring Azure CLI with Azure Stack, see [Install and configure Azure Stack CLI](azure-stack-connect-cli.md).</span></span> <span data-ttu-id="58b2c-171">Pour plus d’informations sur l’utilisation d’Azure CLI 2.0 pour effectuer plusieurs tâches en utilisant des ressources dans votre compte de stockage Azure Stack, consultez [Utilisation d’Azure CLI 2.0 avec le stockage Azure](../../storage/storage-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="58b2c-171">For more information about how to use the Azure CLI 2.0 to perform several tasks working with resources in your Azure Stack Storage account, see [Using the Azure CLI2.0 with Azure Storage](../../storage/storage-azure-cli.md)</span></span>

### <a name="azure-cli-sample-script-for-azure-stack"></a><span data-ttu-id="58b2c-172">Exemple de script Azure CLI pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="58b2c-172">Azure CLI sample script for Azure Stack</span></span> 
<span data-ttu-id="58b2c-173">Une fois que vous avez terminé l’installation et la configuration de l’interface CLI, vous pouvez essayer les étapes suivantes pour utiliser un petit exemple de script shell afin d’interagir avec les ressources de stockage Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="58b2c-173">Once you complete the CLI installation and configuration, you can try the following steps to work with a small shell sample script to interact with Azure Stack Storage resources.</span></span> <span data-ttu-id="58b2c-174">Le script commence par créer un conteneur dans votre compte de stockage, puis charge un fichier existant (un objet blob, par exemple) dans ce conteneur, répertorie tous les objets blob dans le conteneur et, enfin, télécharge le fichier vers une destination que vous spécifiez sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="58b2c-174">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container, lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span> <span data-ttu-id="58b2c-175">Avant d’exécuter ce script, vérifiez que vous êtes connecté au stockage Azure Stack cible.</span><span class="sxs-lookup"><span data-stu-id="58b2c-175">Before you run this script, make sure you successfully connect and login to the target Azure Stack.</span></span> 
1. <span data-ttu-id="58b2c-176">Ouvrez votre éditeur de texte préféré, puis copiez et collez le script précédent dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="58b2c-176">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>
2. <span data-ttu-id="58b2c-177">Mettez à jour les variables du script pour refléter vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="58b2c-177">Update the script's variables to reflect your configuration settings.</span></span> 
3. <span data-ttu-id="58b2c-178">Une fois que vous avez mis à jour les variables nécessaires, enregistrez le script et quittez l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="58b2c-178">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="58b2c-179">Les étapes suivantes supposent que vous avez nommé votre script my_storage_sample.sh.</span><span class="sxs-lookup"><span data-stu-id="58b2c-179">The next steps assume you've named your script my_storage_sample.sh.</span></span>
4. <span data-ttu-id="58b2c-180">Rendez le script exécutable, si nécessaire : `chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="58b2c-180">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>
5. <span data-ttu-id="58b2c-181">Exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="58b2c-181">Execute the script.</span></span> <span data-ttu-id="58b2c-182">Par exemple, dans Bash : `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="58b2c-182">For example, in Bash: `./my_storage_sample.sh`</span></span>

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

echo "Creating the resource group..."
az group create --name $AZURESTACK_RESOURCE_GROUP --location $AZURESTACK_RG_LOCATION

echo "Creating the storage account..."
az storage account create --name $AZURESTACK_STORAGE_ACCOUNT_NAME --resource-group $AZURESTACK_RESOURCE_GROUP --account-type Standard_LRS

echo "Creating the blob container..."
az storage container create --name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Uploading the file..."
az storage blob upload --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --file $FILE_TO_UPLOAD --name $AZURESTACK_STORAGE_BLOB_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Listing the blobs..."
az storage blob list --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --output table

echo "Downloading the file..."
az storage blob download --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --name $AZURESTACK_STORAGE_BLOB_NAME --file $DESTINATION_FILE --output table

echo "Done"
```

## <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="58b2c-183">Explorateur Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="58b2c-183">Microsoft Azure Storage Explorer</span></span>

<span data-ttu-id="58b2c-184">L’Explorateur Stockage Microsoft Azure est une application autonome de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="58b2c-184">Microsoft Azure Storage Explorer is a standalone app from Microsoft.</span></span> <span data-ttu-id="58b2c-185">Cet outil vous permet d’utiliser facilement des données du stockage Azure et du stockage Azure Stack sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="58b2c-185">It allows you to easily work with both Azure Storage and Azure Stack Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="58b2c-186">Si vous voulez un moyen simple de gérer les données de votre stockage Azure Stack, utilisez l’Explorateur Stockage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="58b2c-186">If you want an easy way to manage your Azure Stack Storage data, then consider using Microsoft Azure Storage Explorer.</span></span>

<span data-ttu-id="58b2c-187">Pour plus d’informations sur la configuration de l’Explorateur Stockage Azure afin d’utiliser Azure Stack, consultez [Connecter l’Explorateur Stockage à un abonnement Azure Stack](azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="58b2c-187">For more information about configuring Azure Storage Explorer to work with Azure Stack, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack-storage-connect-se.md).</span></span>

<span data-ttu-id="58b2c-188">Pour plus d’informations sur l’Explorateur Stockage Microsoft Azure, consultez [Bien démarrer avec l’Explorateur Stockage (préversion)](../../vs-azure-tools-storage-manage-with-storage-explorer.md)</span><span class="sxs-lookup"><span data-stu-id="58b2c-188">For more information about Microsoft Azure Storage Explorer, see [Get started with Storage Explorer (Preview)](../../vs-azure-tools-storage-manage-with-storage-explorer.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="58b2c-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58b2c-189">Next steps</span></span>
* [<span data-ttu-id="58b2c-190">Connecter l’Explorateur Stockage à un abonnement Azure Stack</span><span class="sxs-lookup"><span data-stu-id="58b2c-190">Connect Storage Explorer to an Azure Stack subscription</span></span>](azure-stack-storage-connect-se.md)
* [<span data-ttu-id="58b2c-191">Bien démarrer avec l’Explorateur Stockage (préversion)</span><span class="sxs-lookup"><span data-stu-id="58b2c-191">Get started with Storage Explorer (Preview)</span></span>](../../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="58b2c-192">Stockage Azure : Différences et considérations</span><span class="sxs-lookup"><span data-stu-id="58b2c-192">Azure-consistent storage: differences and considerations</span></span>](azure-stack-acs-differences.md)
* [<span data-ttu-id="58b2c-193">Introduction à Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="58b2c-193">Introduction to Microsoft Azure Storage</span></span>](../../storage/common/storage-introduction.md)

