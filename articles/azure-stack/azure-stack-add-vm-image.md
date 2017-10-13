---
title: "Ajouter une image de machine virtuelle à Azure Stack | Microsoft Docs"
description: "Ajouter une image de machine virtuelle Windows ou Linux personnalisée de votre organisation à utiliser par les locataires"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: e5a4236b-1b32-4ee6-9aaa-fcde297a020f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/25/2017
ms.author: sngun
ms.openlocfilehash: de8540397b63093457382cf427a65ea0e48b93e0
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a><span data-ttu-id="2aee5-103">Mettre une image de machine virtuelle personnalisée à la disposition des utilisateurs dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2aee5-103">Make a custom virtual machine image available in Azure Stack</span></span>

<span data-ttu-id="2aee5-104">*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="2aee5-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="2aee5-105">Azure Stack permet aux opérateurs de mettre des images de machine virtuelle personnalisées à la disposition de leurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2aee5-105">Azure Stack enables operators to make custom virtual machine images available to their users.</span></span> <span data-ttu-id="2aee5-106">Ces images peuvent être référencées par des modèles Azure Resource Manager ou être ajoutées à l’interface utilisateur de la Place de marché Azure au moment de la création d’un élément sur la Place de marché.</span><span class="sxs-lookup"><span data-stu-id="2aee5-106">These images can be referenced by Azure Resource Manager templates or added to the Azure Marketplace UI with the creation of a Marketplace item.</span></span> 

## <a name="add-a-vm-image-to-marketplace-with-powershell"></a><span data-ttu-id="2aee5-107">Ajouter une image de machine virtuelle sur la Place de marché à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2aee5-107">Add a VM image to marketplace with PowerShell</span></span>

<span data-ttu-id="2aee5-108">Effectuez les étapes prérequises suivantes à partir du [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe Windows si vous êtes [connecté par le biais d’un VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span><span class="sxs-lookup"><span data-stu-id="2aee5-108">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span></span>

* <span data-ttu-id="2aee5-109">[Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="2aee5-109">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="2aee5-110">Téléchargez les [outils nécessaires pour utiliser Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="2aee5-110">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="2aee5-111">Préparez une image de disque dur virtuel du système d’exploitation Windows ou Linux au format VHD (et non VHDX).</span><span class="sxs-lookup"><span data-stu-id="2aee5-111">Prepare a Windows or Linux operating system virtual hard disk image in VHD format (not VHDX).</span></span>
   
   * <span data-ttu-id="2aee5-112">Pour les images Windows, suivez les instructions sur la préparation des images fournies dans l’article [Charger une image de machine virtuelle Windows dans Azure pour des déploiements Resource Manager](../virtual-machines/windows/upload-generalized-managed.md), à la section **Préparer le disque VHD pour le chargement**.</span><span class="sxs-lookup"><span data-stu-id="2aee5-112">For Windows images, the article [Upload a Windows VM image to Azure for Resource Manager deployments](../virtual-machines/windows/upload-generalized-managed.md) contains image preparation instructions in the **Prepare the VHD for upload** section.</span></span>
   * <span data-ttu-id="2aee5-113">Pour les images Linux, suivez les étapes décrites dans l’article [Déployer des machines virtuelles Linux dans Azure Stack](azure-stack-linux.md) pour préparer l’image ou utiliser une image Linux existante dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2aee5-113">For Linux images, follow the steps to prepare the image or use an existing Azure Stack Linux image as described in the article [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md).</span></span>  

<span data-ttu-id="2aee5-114">Effectuez maintenant les étapes suivantes pour ajouter l’image sur la Place de marché Azure Stack :</span><span class="sxs-lookup"><span data-stu-id="2aee5-114">Now run the following steps to add the image to the Azure Stack marketplace:</span></span>

1. <span data-ttu-id="2aee5-115">Importez les modules Connect et ComputeAdmin :</span><span class="sxs-lookup"><span data-stu-id="2aee5-115">Import the Connect and ComputeAdmin modules:</span></span>
   
   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ``` 

2. <span data-ttu-id="2aee5-116">Connectez-vous à votre environnement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2aee5-116">Sign in to your Azure Stack environment.</span></span> <span data-ttu-id="2aee5-117">Exécutez le script suivant en fonction du type de déploiement de votre environnement Azure Stack : AAD ou AD FS (veillez à remplacer les valeurs tenantName AAD, le point de terminaison GraphAudience et la valeur ArmEndpoint conformément à la configuration de votre environnement) :</span><span class="sxs-lookup"><span data-stu-id="2aee5-117">Run the following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure to replace the AAD tenantName, GraphAudience endpoint and ArmEndpoint values as per your environment configuration):</span></span> 

   <span data-ttu-id="2aee5-118">a.</span><span class="sxs-lookup"><span data-stu-id="2aee5-118">a.</span></span> <span data-ttu-id="2aee5-119">Pour **AAD**, utilisez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2aee5-119">**Azure Active Directory**, use the following cmdlet:</span></span>

   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.windows.net/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"

   #Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience $GraphAudience

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   <span data-ttu-id="2aee5-120">b.</span><span class="sxs-lookup"><span data-stu-id="2aee5-120">b.</span></span> <span data-ttu-id="2aee5-121">Pour **AD FS**, utilisez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2aee5-121">**Active Directory Federation Services**, use the following cmdlet:</span></span>
    
   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.local.azurestack.external/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"

   # Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience $GraphAudience `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
    
3. <span data-ttu-id="2aee5-122">Ajoutez l’image de machine virtuelle en appelant l’applet de commande `Add-AzsVMImage`.</span><span class="sxs-lookup"><span data-stu-id="2aee5-122">Add the VM image by invoking the `Add-AzsVMImage` cmdlet.</span></span> <span data-ttu-id="2aee5-123">Dans l’applet de commande Add-AzsVMImage, spécifiez Windows ou Linux comme valeur du paramètre « osType ».</span><span class="sxs-lookup"><span data-stu-id="2aee5-123">In the Add-AzsVMImage cmdlet, specify the osType as Windows or Linux.</span></span> <span data-ttu-id="2aee5-124">Indiquez l’éditeur (« publisher »), l’offre (« offer »), la référence SKU (« sku ») et la version pour l’image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2aee5-124">Include the publisher, offer, SKU, and version for the VM image.</span></span> <span data-ttu-id="2aee5-125">Consultez la section [Paramètres](#parameters) pour plus d’informations sur les paramètres autorisés.</span><span class="sxs-lookup"><span data-stu-id="2aee5-125">See the [Parameters](#parameters) section for information about the allowed parameters.</span></span> <span data-ttu-id="2aee5-126">Ces paramètres sont utilisés par les modèles Azure Resource Manager pour référencer l’image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2aee5-126">These parameters are used by Azure Resource Manager templates to reference the VM image.</span></span> <span data-ttu-id="2aee5-127">Voici un exemple d’appel du script :</span><span class="sxs-lookup"><span data-stu-id="2aee5-127">Following is an example invocation of the script:</span></span>
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

<span data-ttu-id="2aee5-128">La commande exécute les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="2aee5-128">The command does the following:</span></span>

* <span data-ttu-id="2aee5-129">Elle effectue l’authentification auprès de l’environnement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2aee5-129">Authenticates to the Azure Stack environment</span></span>
* <span data-ttu-id="2aee5-130">Elle charge le disque VHD local dans un nouveau compte de stockage temporaire.</span><span class="sxs-lookup"><span data-stu-id="2aee5-130">Uploads the local VHD to a newly created temporary storage account</span></span>
* <span data-ttu-id="2aee5-131">Elle ajoute l’image de machine virtuelle dans le référentiel d’images de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2aee5-131">Adds the VM image to the VM image repository and</span></span>
* <span data-ttu-id="2aee5-132">Elle crée un élément de Place de marché.</span><span class="sxs-lookup"><span data-stu-id="2aee5-132">Creates a Marketplace item</span></span>

<span data-ttu-id="2aee5-133">Pour vous assurer que la commande s’est correctement exécutée, accédez à la Place de marché dans le portail, puis vérifiez que l’image de machine virtuelle est disponible dans la catégorie **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="2aee5-133">To verify that the command ran successfully, go to Marketplace in the portal, and then verify that the VM image is available in the **Virtual Machines** category.</span></span>

![Image de machine virtuelle correctement ajoutée](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a><span data-ttu-id="2aee5-135">Supprimer une image de machine virtuelle à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2aee5-135">Remove a VM image with PowerShell</span></span>

<span data-ttu-id="2aee5-136">Si vous n’avez plus besoin de l’image de machine virtuelle que vous avez chargée, vous pouvez la supprimer sur la Place de marché à l’aide de l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2aee5-136">When you no longer need the virtual machine image that you have uploaded earlier, you can delete it from the marketplace by using the following cmdlet:</span></span>

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a><span data-ttu-id="2aee5-137">Paramètres</span><span class="sxs-lookup"><span data-stu-id="2aee5-137">Parameters</span></span>

| <span data-ttu-id="2aee5-138">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2aee5-138">Parameter</span></span> | <span data-ttu-id="2aee5-139">Description</span><span class="sxs-lookup"><span data-stu-id="2aee5-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2aee5-140">**publisher**</span><span class="sxs-lookup"><span data-stu-id="2aee5-140">**publisher**</span></span> |<span data-ttu-id="2aee5-141">Segment du nom de l’éditeur de l’image de machine virtuelle que les utilisateurs indiquent pour déployer l’image.</span><span class="sxs-lookup"><span data-stu-id="2aee5-141">The publisher name segment of the VM image that users use when deploying the image.</span></span> <span data-ttu-id="2aee5-142">Exemple : « Microsoft ».</span><span class="sxs-lookup"><span data-stu-id="2aee5-142">An example is ‘Microsoft’.</span></span> <span data-ttu-id="2aee5-143">N’incluez aucun espace ou autre caractère spécial dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="2aee5-143">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="2aee5-144">**offer**</span><span class="sxs-lookup"><span data-stu-id="2aee5-144">**offer**</span></span> |<span data-ttu-id="2aee5-145">Segment du nom de l’offre de l’image de machine virtuelle que les utilisateurs indiquent pour déployer l’image.</span><span class="sxs-lookup"><span data-stu-id="2aee5-145">The offer name segment of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="2aee5-146">Exemple : « WindowsServer ».</span><span class="sxs-lookup"><span data-stu-id="2aee5-146">An example is ‘WindowsServer’.</span></span> <span data-ttu-id="2aee5-147">N’incluez aucun espace ou autre caractère spécial dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="2aee5-147">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="2aee5-148">**sku**</span><span class="sxs-lookup"><span data-stu-id="2aee5-148">**sku**</span></span> |<span data-ttu-id="2aee5-149">Segment du nom de la référence SKU de l’image de machine virtuelle que les utilisateurs indiquent pour déployer l’image.</span><span class="sxs-lookup"><span data-stu-id="2aee5-149">The SKU name segment of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="2aee5-150">Exemple : « Datacenter2016 ».</span><span class="sxs-lookup"><span data-stu-id="2aee5-150">An example is ‘Datacenter2016’.</span></span> <span data-ttu-id="2aee5-151">N’incluez aucun espace ou autre caractère spécial dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="2aee5-151">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="2aee5-152">**version**</span><span class="sxs-lookup"><span data-stu-id="2aee5-152">**version**</span></span> |<span data-ttu-id="2aee5-153">Version de l’image de machine virtuelle que les utilisateurs indiquent pour déployer l’image.</span><span class="sxs-lookup"><span data-stu-id="2aee5-153">The version of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="2aee5-154">La version suit le format *\#.\#.\#*,</span><span class="sxs-lookup"><span data-stu-id="2aee5-154">This version is in the format *\#.\#.\#*.</span></span> <span data-ttu-id="2aee5-155">par exemple, « 1.0.0 ».</span><span class="sxs-lookup"><span data-stu-id="2aee5-155">An example is ‘1.0.0’.</span></span> <span data-ttu-id="2aee5-156">N’incluez aucun espace ou autre caractère spécial dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="2aee5-156">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="2aee5-157">**osType**</span><span class="sxs-lookup"><span data-stu-id="2aee5-157">**osType**</span></span> |<span data-ttu-id="2aee5-158">Type d’exploitation de l’image, qui doit être « Windows » ou « Linux ».</span><span class="sxs-lookup"><span data-stu-id="2aee5-158">The osType of the image must be either ‘Windows’ or ‘Linux’.</span></span> |
| <span data-ttu-id="2aee5-159">**osDiskLocalPath**</span><span class="sxs-lookup"><span data-stu-id="2aee5-159">**osDiskLocalPath**</span></span> |<span data-ttu-id="2aee5-160">Chemin d’accès local au disque VHD de système d’exploitation que vous chargez comme image de machine virtuelle dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2aee5-160">The local path to the OS disk VHD that you are uploading as a VM image to Azure Stack.</span></span> |
| <span data-ttu-id="2aee5-161">**dataDiskLocalPaths**</span><span class="sxs-lookup"><span data-stu-id="2aee5-161">**dataDiskLocalPaths**</span></span> |<span data-ttu-id="2aee5-162">Tableau facultatif des chemins d’accès locaux des disques de données qui peuvent être chargés comme partie de l’image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2aee5-162">An optional array of the local paths for data disks that can be uploaded as part of the VM image.</span></span> |
| <span data-ttu-id="2aee5-163">**CreateGalleryItem**</span><span class="sxs-lookup"><span data-stu-id="2aee5-163">**CreateGalleryItem**</span></span> |<span data-ttu-id="2aee5-164">Indicateur booléen qui détermine s’il faut créer un élément sur la Place de marché.</span><span class="sxs-lookup"><span data-stu-id="2aee5-164">A Boolean flag that determines whether to create an item in Marketplace.</span></span> <span data-ttu-id="2aee5-165">Par défaut, il est défini sur true.</span><span class="sxs-lookup"><span data-stu-id="2aee5-165">By default, it is set to true.</span></span> |
| <span data-ttu-id="2aee5-166">**title**</span><span class="sxs-lookup"><span data-stu-id="2aee5-166">**title**</span></span> |<span data-ttu-id="2aee5-167">Nom d’affichage de l’élément de la Place de marché.</span><span class="sxs-lookup"><span data-stu-id="2aee5-167">The display name of Marketplace item.</span></span> <span data-ttu-id="2aee5-168">Par défaut, il se compose des segments Éditeur-Offre-SKU de l’image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2aee5-168">By default, it is set to the Publisher-Offer-Sku of the VM image.</span></span> |
| <span data-ttu-id="2aee5-169">**description**</span><span class="sxs-lookup"><span data-stu-id="2aee5-169">**description**</span></span> |<span data-ttu-id="2aee5-170">Description de l’élément de la Place de marché.</span><span class="sxs-lookup"><span data-stu-id="2aee5-170">The description of the Marketplace item.</span></span> |
| <span data-ttu-id="2aee5-171">**location**</span><span class="sxs-lookup"><span data-stu-id="2aee5-171">**location**</span></span> |<span data-ttu-id="2aee5-172">Emplacement de publication de l’image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2aee5-172">The location to which the VM image should be published.</span></span> <span data-ttu-id="2aee5-173">Par défaut, cette valeur est définie sur «local ».</span><span class="sxs-lookup"><span data-stu-id="2aee5-173">By default, this value is set to local.</span></span>|
| <span data-ttu-id="2aee5-174">**osDiskBlobURI**</span><span class="sxs-lookup"><span data-stu-id="2aee5-174">**osDiskBlobURI**</span></span> |<span data-ttu-id="2aee5-175">(Facultatif) Ce script accepte également un URI de stockage Blob pour osDisk.</span><span class="sxs-lookup"><span data-stu-id="2aee5-175">Optionally, this script also accepts a Blob storage URI for osDisk.</span></span> |
| <span data-ttu-id="2aee5-176">**dataDiskBlobURIs**</span><span class="sxs-lookup"><span data-stu-id="2aee5-176">**dataDiskBlobURIs**</span></span> |<span data-ttu-id="2aee5-177">(Facultatif) Ce script accepte également un tableau d’URI de stockage Blob pour l’ajout de disques de données à l’image.</span><span class="sxs-lookup"><span data-stu-id="2aee5-177">Optionally, this script also accepts an array of Blob storage URIs for adding data disks to the image.</span></span> |

## <a name="add-a-vm-image-through-the-portal"></a><span data-ttu-id="2aee5-178">Ajouter une image de machine virtuelle par le biais du portail</span><span class="sxs-lookup"><span data-stu-id="2aee5-178">Add a VM image through the portal</span></span>

> [!NOTE]
> <span data-ttu-id="2aee5-179">Cette méthode nécessite de créer l’élément de la Place de marché séparément.</span><span class="sxs-lookup"><span data-stu-id="2aee5-179">This method requires creating the Marketplace item separately.</span></span>

<span data-ttu-id="2aee5-180">L’une des exigences pour les images est de permettre leur référencement par un URI de stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="2aee5-180">One requirement of images is that they can be referenced by a Blob storage URI.</span></span> <span data-ttu-id="2aee5-181">Préparez une image de système d’exploitation Windows ou Linux au format VHD (pas VHDX), puis chargez cette image dans un compte de stockage Azure ou Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2aee5-181">Prepare a Windows or Linux operating system image in VHD format (not VHDX), and then upload the image to a storage account in Azure or Azure Stack.</span></span> <span data-ttu-id="2aee5-182">Si votre image est déjà chargée dans le stockage Blob Azure ou Azure Stack, ignorez l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="2aee5-182">If your image is already uploaded to the Blob storage in Azure or Azure Stack, you can skip step1.</span></span>

1. <span data-ttu-id="2aee5-183">[Chargez une image de machine virtuelle Windows dans Azure pour les déploiements Resource Manager ](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) ou, pour une image Linux, suivez les instructions fournies dans l’article [Déployer des machines virtuelles Linux dans Azure Stack](azure-stack-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2aee5-183">[Upload a Windows VM image to Azure for Resource Manager deployments](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) or for a Linux image, follow the instructions described in the [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md) article.</span></span> <span data-ttu-id="2aee5-184">Avant de charger l’image, tenez compte des points suivants :</span><span class="sxs-lookup"><span data-stu-id="2aee5-184">You should understand the following considerations before you upload the image:</span></span>

   * <span data-ttu-id="2aee5-185">Il est préférable de charger une image dans le stockage Blob Azure Stack plutôt que dans le stockage Blob Azure, car la publication d’une image dans le référentiel d’images Azure Stack est plus rapide.</span><span class="sxs-lookup"><span data-stu-id="2aee5-185">It's more efficient to upload an image to Azure Stack Blob storage than to Azure Blob storage because it takes less time to push the image to the Azure Stack image repository.</span></span> 
   
   * <span data-ttu-id="2aee5-186">Quand vous chargez [l’image de machine virtuelle Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), pensez à substituer l’étape **Se connecter à Azure** par l’étape [Configurer l’environnement PowerShell de l’opérateur Azure Stack](azure-stack-powershell-configure-admin.md).</span><span class="sxs-lookup"><span data-stu-id="2aee5-186">When uploading the [Windows VM image](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), make sure to substitute the **Login to Azure** step with the [Configure the Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md)  step.</span></span>  

   * <span data-ttu-id="2aee5-187">Notez l’URI du stockage Blob où vous chargez l’image, au format suivant : *&lt;compteStockage&gt;/&lt;conteneurBlob&gt;/&lt;nomVHDCible&gt;*.vhd</span><span class="sxs-lookup"><span data-stu-id="2aee5-187">Make a note of the Blob storage URI where you upload the image, which is in the following format: *&lt;storageAccount&gt;/&lt;blobContainer&gt;/&lt;targetVHDName&gt;*.vhd</span></span>

   * <span data-ttu-id="2aee5-188">Pour rendre le stockage Blob accessible de manière anonyme, accédez au conteneur d’objets blob du compte de stockage dans lequel l’image de machine virtuelle VHD a été chargée dans **Blob**, puis sélectionnez **Stratégie d’accès**.</span><span class="sxs-lookup"><span data-stu-id="2aee5-188">To make the blob anonymously accessible, go to the storage account blob container where the VM image VHD was uploaded to **Blob,** and then select **Access Policy**.</span></span> <span data-ttu-id="2aee5-189">Si vous le souhaitez, vous pouvez à la place générer une signature d’accès partagé pour le conteneur et l’inclure dans l’URI de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="2aee5-189">If you want, you can instead generate a shared access signature for the container and include it as part of the blob URI.</span></span>

   ![Accéder aux objets blob du compte de stockage](./media/azure-stack-add-vm-image/image1.png)

   ![Définir un accès public pour les objets blob](./media/azure-stack-add-vm-image/image2.png)

2. <span data-ttu-id="2aee5-192">Connectez-vous à Azure Stack en tant qu’opérateur : dans le menu, cliquez sur **Plus de services** > **Fournisseurs de ressources** > sélectionnez **Compute** > **Images de machine virtuelle** > **Ajouter**</span><span class="sxs-lookup"><span data-stu-id="2aee5-192">Sign in to Azure Stack as operator > From the menu, click **More services** > **Resource Providers** > select  **Compute** > **VM images** > **Add**</span></span>

3. <span data-ttu-id="2aee5-193">Dans le panneau **Ajouter une image de machine virtuelle**, entrez l’éditeur, l’offre, la référence SKU et la version de l’image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2aee5-193">On the **Add a VM Image** blade, enter the publisher, offer, SKU, and version of the virtual machine image.</span></span> <span data-ttu-id="2aee5-194">Ces segments de nom référencent l’image de machine virtuelle dans les modèles Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2aee5-194">These name segments refer to the VM image in Resource Manager templates.</span></span> <span data-ttu-id="2aee5-195">Sélectionnez le **type de système d’exploitation** approprié.</span><span class="sxs-lookup"><span data-stu-id="2aee5-195">Make sure to select the **osType** correctly.</span></span> <span data-ttu-id="2aee5-196">Dans **URI d’objet blob du disque de système d’exploitation**, entrez l’URI de l’objet blob où l’image a été chargée, puis cliquez sur **Créer** pour démarrer la création de l’image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2aee5-196">For **OD Disk Blob URI**, enter the Blob URI where the image was uploaded and click **Create** to begin creating the VM Image.</span></span>
   
   ![Démarrer la création de l’image](./media/azure-stack-add-vm-image/image4.png)

   <span data-ttu-id="2aee5-198">Une fois que l’image de machine virtuelle a été créée, son état passe à « Réussi ».</span><span class="sxs-lookup"><span data-stu-id="2aee5-198">When the image is successfully created, the VM image status changes to ‘Succeeded’.</span></span>

4. <span data-ttu-id="2aee5-199">Pour rendre une image de machine virtuelle plus rapidement disponible dans l’interface utilisateur, il est préférable de [créer un élément de Place de marché](azure-stack-create-and-publish-marketplace-item.md).</span><span class="sxs-lookup"><span data-stu-id="2aee5-199">To make the virtual machine image more readily available for user consumption in the UI, it is best to [create a Marketplace item](azure-stack-create-and-publish-marketplace-item.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2aee5-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2aee5-200">Next steps</span></span>

[<span data-ttu-id="2aee5-201">Approvisionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2aee5-201">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)