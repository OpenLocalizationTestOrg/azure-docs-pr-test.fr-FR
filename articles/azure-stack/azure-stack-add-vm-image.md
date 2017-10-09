---
title: "aaaAdding une machine virtuelle de l’image tooAzure pile | Documents Microsoft"
description: "Ajout Windows ou Linux VM image personnalisée de votre organisation pour les locataires toouse"
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
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 26dd6c289664c4d64d5932f4396ae778f3f1e1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a><span data-ttu-id="f3079-103">Mettre une image de machine virtuelle personnalisée à la disposition des utilisateurs dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f3079-103">Make a custom virtual machine image available in Azure Stack</span></span>

<span data-ttu-id="f3079-104">Les administrateurs toomake machine virtuelle personnalisée images disponibles tootheir utilisateurs du cloud de Azure permet de pile.</span><span class="sxs-lookup"><span data-stu-id="f3079-104">Azure Stack enables cloud administrators toomake custom virtual machine images available tootheir users.</span></span> <span data-ttu-id="f3079-105">Ces images peuvent être référencés par les modèles Azure Resource Manager ou ajouté toothe Azure Marketplace UI avec la création d’un élément de Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-105">These images can be referenced by Azure Resource Manager templates or added toothe Azure Marketplace UI with hello creation of a Marketplace item.</span></span> 

## <a name="add-a-vm-image-toomarketplace-with-powershell"></a><span data-ttu-id="f3079-106">Ajouter un toomarketplace d’image de machine virtuelle avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3079-106">Add a VM image toomarketplace with PowerShell</span></span>

<span data-ttu-id="f3079-107">Exécution hello suivant la configuration requise à partir de hello [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe basé sur Windows si vous êtes [connectés via VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span><span class="sxs-lookup"><span data-stu-id="f3079-107">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span></span>

* <span data-ttu-id="f3079-108">[Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="f3079-108">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="f3079-109">Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="f3079-109">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="f3079-110">Préparez une image de disque dur virtuel du système d’exploitation Windows ou Linux au format VHD (et non VHDX).</span><span class="sxs-lookup"><span data-stu-id="f3079-110">Prepare a Windows or Linux operating system virtual hard disk image in VHD format (not VHDX).</span></span>
   
   * <span data-ttu-id="f3079-111">Pour les images Windows hello article [télécharger un tooAzure d’image de machine virtuelle Windows pour les déploiements de gestionnaire de ressources](../virtual-machines/windows/upload-generalized-managed.md) contient des instructions de préparation d’image Bonjour **hello préparation du disque dur virtuel pour le téléchargement** section.</span><span class="sxs-lookup"><span data-stu-id="f3079-111">For Windows images, hello article [Upload a Windows VM image tooAzure for Resource Manager deployments](../virtual-machines/windows/upload-generalized-managed.md) contains image preparation instructions in hello **Prepare hello VHD for upload** section.</span></span>
   * <span data-ttu-id="f3079-112">Pour les images de Linux, suivez les étapes de hello pour préparer l’image de hello ou utiliser une image Linux de pile Azure existante comme décrit dans l’article de hello [ordinateurs virtuels Linux de déployer sur Azure pile](azure-stack-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f3079-112">For Linux images, follow hello steps to prepare hello image or use an existing Azure Stack Linux image as described in hello article [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md).</span></span>  

<span data-ttu-id="f3079-113">Maintenant, exécutez hello suivant marketplace de la pile de Azure étapes tooadd hello image toohello :</span><span class="sxs-lookup"><span data-stu-id="f3079-113">Now run hello following steps tooadd hello image toohello Azure Stack marketplace:</span></span>

1. <span data-ttu-id="f3079-114">Importer des modules de se connecter et ComputeAdmin hello :</span><span class="sxs-lookup"><span data-stu-id="f3079-114">Import hello Connect and ComputeAdmin modules:</span></span>
   
   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ``` 

2. <span data-ttu-id="f3079-115">Se connecter tooyour environnement Azure pile.</span><span class="sxs-lookup"><span data-stu-id="f3079-115">Sign in tooyour Azure Stack environment.</span></span> <span data-ttu-id="f3079-116">De script suivante d’exécution hello selon si votre environnement Azure pile est déployé à l’aide d’AAD ou ADFS (Assurez-vous que tooreplace hello AAD nom_client) :</span><span class="sxs-lookup"><span data-stu-id="f3079-116">Run hello following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure tooreplace hello AAD tenant name):</span></span> 

   <span data-ttu-id="f3079-117">a.</span><span class="sxs-lookup"><span data-stu-id="f3079-117">a.</span></span> <span data-ttu-id="f3079-118">**Azure Active Directory**, utilisez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="f3079-118">**Azure Active Directory**, use hello following cmdlet:</span></span>

   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   <span data-ttu-id="f3079-119">b.</span><span class="sxs-lookup"><span data-stu-id="f3079-119">b.</span></span> <span data-ttu-id="f3079-120">**Active Directory Federation Services**, utilisez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="f3079-120">**Active Directory Federation Services**, use hello following cmdlet:</span></span>
    
   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external"

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience "https://graph.local.azurestack.external/" `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
    
3. <span data-ttu-id="f3079-121">Ajouter l’image de machine virtuelle hello en appelant hello `Add-AzsVMImage` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f3079-121">Add hello VM image by invoking hello `Add-AzsVMImage` cmdlet.</span></span> <span data-ttu-id="f3079-122">Dans l’applet de commande Add-AzsVMImage hello, attribuez-leur hello osType Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="f3079-122">In hello Add-AzsVMImage cmdlet, specify hello osType as Windows or Linux.</span></span> <span data-ttu-id="f3079-123">Inclure le serveur de publication hello, offre, référence (SKU) et la version pour l’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-123">Include hello publisher, offer, SKU, and version for hello VM image.</span></span> <span data-ttu-id="f3079-124">Consultez hello [paramètres](#parameters) section pour plus d’informations sur hello autorisé de paramètres.</span><span class="sxs-lookup"><span data-stu-id="f3079-124">See hello [Parameters](#parameters) section for information about hello allowed parameters.</span></span> <span data-ttu-id="f3079-125">Ces paramètres sont utilisés par l’image de machine virtuelle Azure Resource Manager modèles tooreference hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-125">These parameters are used by Azure Resource Manager templates tooreference hello VM image.</span></span> <span data-ttu-id="f3079-126">Voici un appel de l’exemple de script de hello :</span><span class="sxs-lookup"><span data-stu-id="f3079-126">Following is an example invocation of hello script:</span></span>
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

<span data-ttu-id="f3079-127">commande Hello hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f3079-127">hello command does hello following:</span></span>

* <span data-ttu-id="f3079-128">Authentifie l’environnement de Azure pile toohello</span><span class="sxs-lookup"><span data-stu-id="f3079-128">Authenticates toohello Azure Stack environment</span></span>
* <span data-ttu-id="f3079-129">Télécharge hello tooa de disque dur virtuel local créé le compte de stockage temporaire</span><span class="sxs-lookup"><span data-stu-id="f3079-129">Uploads hello local VHD tooa newly created temporary storage account</span></span>
* <span data-ttu-id="f3079-130">Ajoute le référentiel d’images hello VM image toohello machine virtuelle et</span><span class="sxs-lookup"><span data-stu-id="f3079-130">Adds hello VM image toohello VM image repository and</span></span>
* <span data-ttu-id="f3079-131">Elle crée un élément de Place de marché.</span><span class="sxs-lookup"><span data-stu-id="f3079-131">Creates a Marketplace item</span></span>

<span data-ttu-id="f3079-132">tooverify commande hello s’est correctement exécutée, tooMarketplace dans le portail de hello, puis vérifiez cette image de machine virtuelle hello est disponible dans hello **virtuels** catégorie.</span><span class="sxs-lookup"><span data-stu-id="f3079-132">tooverify that hello command ran successfully, go tooMarketplace in hello portal, and then verify that hello VM image is available in hello **Virtual Machines** category.</span></span>

![Image de machine virtuelle correctement ajoutée](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a><span data-ttu-id="f3079-134">Supprimer une image de machine virtuelle à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3079-134">Remove a VM image with PowerShell</span></span>

<span data-ttu-id="f3079-135">Lorsque vous avez besoin n’est plus hello image de machine virtuelle que vous avez téléchargés précédemment, vous pouvez le supprimer à partir du marketplace de hello à l’aide de hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="f3079-135">When you no longer need hello virtual machine image that you have uploaded earlier, you can delete it from hello marketplace by using hello following cmdlet:</span></span>

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a><span data-ttu-id="f3079-136">Paramètres</span><span class="sxs-lookup"><span data-stu-id="f3079-136">Parameters</span></span>

| <span data-ttu-id="f3079-137">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f3079-137">Parameter</span></span> | <span data-ttu-id="f3079-138">Description</span><span class="sxs-lookup"><span data-stu-id="f3079-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f3079-139">**publisher**</span><span class="sxs-lookup"><span data-stu-id="f3079-139">**publisher**</span></span> |<span data-ttu-id="f3079-140">segment de nom Hello Éditeur d’image de machine virtuelle hello que les utilisateurs utilisent lors du déploiement d’image de hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-140">hello publisher name segment of hello VM image that users use when deploying hello image.</span></span> <span data-ttu-id="f3079-141">Exemple : « Microsoft ».</span><span class="sxs-lookup"><span data-stu-id="f3079-141">An example is ‘Microsoft’.</span></span> <span data-ttu-id="f3079-142">N’incluez aucun espace ou autre caractère spécial dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="f3079-142">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="f3079-143">**offer**</span><span class="sxs-lookup"><span data-stu-id="f3079-143">**offer**</span></span> |<span data-ttu-id="f3079-144">segment de nom Hello offre de hello Image de machine virtuelle que les utilisateurs utilisent lors du déploiement d’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-144">hello offer name segment of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="f3079-145">Exemple : « WindowsServer ».</span><span class="sxs-lookup"><span data-stu-id="f3079-145">An example is ‘WindowsServer’.</span></span> <span data-ttu-id="f3079-146">N’incluez aucun espace ou autre caractère spécial dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="f3079-146">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="f3079-147">**sku**</span><span class="sxs-lookup"><span data-stu-id="f3079-147">**sku**</span></span> |<span data-ttu-id="f3079-148">segment de nom Hello référence (SKU) de hello Image de machine virtuelle que les utilisateurs utilisent lors du déploiement d’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-148">hello SKU name segment of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="f3079-149">Exemple : « Datacenter2016 ».</span><span class="sxs-lookup"><span data-stu-id="f3079-149">An example is ‘Datacenter2016’.</span></span> <span data-ttu-id="f3079-150">N’incluez aucun espace ou autre caractère spécial dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="f3079-150">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="f3079-151">**version**</span><span class="sxs-lookup"><span data-stu-id="f3079-151">**version**</span></span> |<span data-ttu-id="f3079-152">version Hello Hello Image de machine virtuelle que les utilisateurs utilisent lors du déploiement d’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-152">hello version of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="f3079-153">Cette version est au format de hello  *\#.\#. \#*.</span><span class="sxs-lookup"><span data-stu-id="f3079-153">This version is in hello format *\#.\#.\#*.</span></span> <span data-ttu-id="f3079-154">par exemple, « 1.0.0 ».</span><span class="sxs-lookup"><span data-stu-id="f3079-154">An example is ‘1.0.0’.</span></span> <span data-ttu-id="f3079-155">N’incluez aucun espace ou autre caractère spécial dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="f3079-155">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="f3079-156">**osType**</span><span class="sxs-lookup"><span data-stu-id="f3079-156">**osType**</span></span> |<span data-ttu-id="f3079-157">osType Hello d’image de hello doit être 'Windows' ou 'Linux'.</span><span class="sxs-lookup"><span data-stu-id="f3079-157">hello osType of hello image must be either ‘Windows’ or ‘Linux’.</span></span> |
| <span data-ttu-id="f3079-158">**osDiskLocalPath**</span><span class="sxs-lookup"><span data-stu-id="f3079-158">**osDiskLocalPath**</span></span> |<span data-ttu-id="f3079-159">disque toohello du système d’exploitation du chemin d’accès local de Hello VHD que vous chargez en tant qu’un tooAzure d’image de machine virtuelle pile.</span><span class="sxs-lookup"><span data-stu-id="f3079-159">hello local path toohello OS disk VHD that you are uploading as a VM image tooAzure Stack.</span></span> |
| <span data-ttu-id="f3079-160">**dataDiskLocalPaths**</span><span class="sxs-lookup"><span data-stu-id="f3079-160">**dataDiskLocalPaths**</span></span> |<span data-ttu-id="f3079-161">Tableau facultatif de chemins d’accès local de hello pour les disques de données qui peuvent être téléchargés dans le cadre de l’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-161">An optional array of hello local paths for data disks that can be uploaded as part of hello VM image.</span></span> |
| <span data-ttu-id="f3079-162">**CreateGalleryItem**</span><span class="sxs-lookup"><span data-stu-id="f3079-162">**CreateGalleryItem**</span></span> |<span data-ttu-id="f3079-163">Indicateur booléen qui détermine si un élément dans le Marketplace de toocreate.</span><span class="sxs-lookup"><span data-stu-id="f3079-163">A Boolean flag that determines whether toocreate an item in Marketplace.</span></span> <span data-ttu-id="f3079-164">Par défaut, elle a la valeur tootrue.</span><span class="sxs-lookup"><span data-stu-id="f3079-164">By default, it is set tootrue.</span></span> |
| <span data-ttu-id="f3079-165">**title**</span><span class="sxs-lookup"><span data-stu-id="f3079-165">**title**</span></span> |<span data-ttu-id="f3079-166">Hello affiche le nom de l’élément du Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f3079-166">hello display name of Marketplace item.</span></span> <span data-ttu-id="f3079-167">Par défaut, elle a la valeur toohello Publisher-offre-référence (SKU) de l’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-167">By default, it is set toohello Publisher-Offer-Sku of hello VM image.</span></span> |
| <span data-ttu-id="f3079-168">**description**</span><span class="sxs-lookup"><span data-stu-id="f3079-168">**description**</span></span> |<span data-ttu-id="f3079-169">description de Hello d’élément du Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-169">hello description of hello Marketplace item.</span></span> |
| <span data-ttu-id="f3079-170">**location**</span><span class="sxs-lookup"><span data-stu-id="f3079-170">**location**</span></span> |<span data-ttu-id="f3079-171">image de machine virtuelle Hello emplacement toowhich hello doit être publié.</span><span class="sxs-lookup"><span data-stu-id="f3079-171">hello location toowhich hello VM image should be published.</span></span> <span data-ttu-id="f3079-172">Par défaut, cette valeur est définie à toolocal.</span><span class="sxs-lookup"><span data-stu-id="f3079-172">By default, this value is set toolocal.</span></span>|
| <span data-ttu-id="f3079-173">**osDiskBlobURI**</span><span class="sxs-lookup"><span data-stu-id="f3079-173">**osDiskBlobURI**</span></span> |<span data-ttu-id="f3079-174">(Facultatif) Ce script accepte également un URI de stockage Blob pour osDisk.</span><span class="sxs-lookup"><span data-stu-id="f3079-174">Optionally, this script also accepts a Blob storage URI for osDisk.</span></span> |
| <span data-ttu-id="f3079-175">**dataDiskBlobURIs**</span><span class="sxs-lookup"><span data-stu-id="f3079-175">**dataDiskBlobURIs**</span></span> |<span data-ttu-id="f3079-176">Si vous le souhaitez, ce script accepte également un tableau de stockage d’objets Blob URI pour l’ajout d’image de toohello de disques de données.</span><span class="sxs-lookup"><span data-stu-id="f3079-176">Optionally, this script also accepts an array of Blob storage URIs for adding data disks toohello image.</span></span> |

## <a name="add-a-vm-image-through-hello-portal"></a><span data-ttu-id="f3079-177">Ajouter une image de machine virtuelle via le portail de hello</span><span class="sxs-lookup"><span data-stu-id="f3079-177">Add a VM image through hello portal</span></span>

> [!NOTE]
> <span data-ttu-id="f3079-178">Cette méthode requiert la création d’élément du Marketplace hello séparément.</span><span class="sxs-lookup"><span data-stu-id="f3079-178">This method requires creating hello Marketplace item separately.</span></span>

<span data-ttu-id="f3079-179">L’une des exigences pour les images est de permettre leur référencement par un URI de stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="f3079-179">One requirement of images is that they can be referenced by a Blob storage URI.</span></span> <span data-ttu-id="f3079-180">Préparer une image de système d’exploitation Windows ou Linux au format de disque dur virtuel (pas VHDX) et puis télécharger hello image tooa compte de stockage Azure ou de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3079-180">Prepare a Windows or Linux operating system image in VHD format (not VHDX), and then upload hello image tooa storage account in Azure or Azure Stack.</span></span> <span data-ttu-id="f3079-181">Si votre image est déjà téléchargé toohello stockage d’objets Blob dans Azure ou de la pile d’Azure, vous pouvez ignorer l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="f3079-181">If your image is already uploaded toohello Blob storage in Azure or Azure Stack, you can skip step1.</span></span>

1. <span data-ttu-id="f3079-182">[Télécharger un tooAzure d’image de machine virtuelle Windows pour les déploiements de gestionnaire de ressources](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) ou d’une image Linux, suivez les instructions de hello décrites dans hello [ordinateurs virtuels Linux de déployer sur Azure pile](azure-stack-linux.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="f3079-182">[Upload a Windows VM image tooAzure for Resource Manager deployments](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) or for a Linux image, follow hello instructions described in hello [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md) article.</span></span> <span data-ttu-id="f3079-183">Vous devez comprendre hello suivant considérations avant de charger hello image :</span><span class="sxs-lookup"><span data-stu-id="f3079-183">You should understand hello following considerations before you upload hello image:</span></span>

   * <span data-ttu-id="f3079-184">Il est plus efficace tooupload une tooAzure image stockage d’objets Blob de pile à tooAzure stockage d’objets Blob, car il prend moins référentiel d’images temps toopush toohello hello image Azure pile.</span><span class="sxs-lookup"><span data-stu-id="f3079-184">It's more efficient tooupload an image tooAzure Stack Blob storage than tooAzure Blob storage because it takes less time toopush hello image toohello Azure Stack image repository.</span></span> 
   
   * <span data-ttu-id="f3079-185">Lors du téléchargement hello [image de machine virtuelle Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), assurez-vous que toosubstitute hello **connexion tooAzure** étape avec hello [configurer l’environnement PowerShell de l’opérateur de pile de Azure hello](azure-stack-powershell-configure-admin.md)étape.</span><span class="sxs-lookup"><span data-stu-id="f3079-185">When uploading hello [Windows VM image](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), make sure toosubstitute hello **Login tooAzure** step with hello [Configure hello Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md)  step.</span></span>  

   * <span data-ttu-id="f3079-186">Prenez note de hello URI où vous téléchargez l’image hello, qui se trouve dans hello format de stockage d’objets Blob :  *&lt;storageAccount&gt;/&lt;blobContainer&gt; / &lt;targetVHDName&gt;*.vhd</span><span class="sxs-lookup"><span data-stu-id="f3079-186">Make a note of hello Blob storage URI where you upload hello image, which is in hello following format: *&lt;storageAccount&gt;/&lt;blobContainer&gt;/&lt;targetVHDName&gt;*.vhd</span></span>

   * <span data-ttu-id="f3079-187">toomake hello accessible de manière anonyme, accédez toohello compte blob conteneur de stockage blob hello VM où l’image disque dur virtuel a été téléchargé trop**Blob,** , puis sélectionnez **la stratégie d’accès**.</span><span class="sxs-lookup"><span data-stu-id="f3079-187">toomake hello blob anonymously accessible, go toohello storage account blob container where hello VM image VHD was uploaded too**Blob,** and then select **Access Policy**.</span></span> <span data-ttu-id="f3079-188">Si vous le souhaitez, vous pouvez à la place générer une signature d’accès partagé pour le conteneur de hello et inclure dans le cadre de l’URI d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-188">If you want, you can instead generate a shared access signature for hello container and include it as part of hello blob URI.</span></span>

   ![Parcourir les objets BLOB du compte toostorage](./media/azure-stack-add-vm-image/image1.png)

   ![Jeu d’objets blob accès toopublic](./media/azure-stack-add-vm-image/image2.png)

2. <span data-ttu-id="f3079-191">Connectez-vous à tooAzure pile sous la forme d’un administrateur de cloud > hello menu, cliquez sur **davantage de services** > **fournisseurs de ressources** > sélectionnez **de calcul**  >  **Images de machine virtuelle** > **ajouter**</span><span class="sxs-lookup"><span data-stu-id="f3079-191">Sign in tooAzure Stack as a cloud administrator > From hello menu, click **More services** > **Resource Providers** > select  **Compute** > **VM images** > **Add**</span></span>

3. <span data-ttu-id="f3079-192">Sur hello **ajouter une Image de machine virtuelle** panneau, entrez le serveur de publication hello, offre, référence (SKU) et la version de l’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="f3079-192">On hello **Add a VM Image** blade, enter hello publisher, offer, SKU, and version of hello virtual machine image.</span></span> <span data-ttu-id="f3079-193">Ces segments de noms font référence toohello image de machine virtuelle dans les modèles de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="f3079-193">These name segments refer toohello VM image in Resource Manager templates.</span></span> <span data-ttu-id="f3079-194">Assurez-vous que tooselect le **osType** correctement.</span><span class="sxs-lookup"><span data-stu-id="f3079-194">Make sure tooselect the **osType** correctly.</span></span> <span data-ttu-id="f3079-195">Pour **OD disque Blob URI**, entrez hello URI d’objet Blob où l’image a été téléchargée, cliquez sur **créer** toobegin création de l’Image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f3079-195">For **OD Disk Blob URI**, enter hello Blob URI where the image was uploaded and click **Create** toobegin creating the VM Image.</span></span>
   
   ![BEGIN toocreate hello image](./media/azure-stack-add-vm-image/image4.png)

   <span data-ttu-id="f3079-197">Lorsque l’image de hello est correctement créé, hello état d’image de machine virtuelle change too'Succeeded'.</span><span class="sxs-lookup"><span data-stu-id="f3079-197">When hello image is successfully created, hello VM image status changes too‘Succeeded’.</span></span>

4. <span data-ttu-id="f3079-198">image de machine virtuelle hello toomake plus facilement disponible pour un utilisateur dans l’interface utilisateur de hello, il est préférable de trop[créer un élément du Marketplace](azure-stack-create-and-publish-marketplace-item.md).</span><span class="sxs-lookup"><span data-stu-id="f3079-198">toomake hello virtual machine image more readily available for user consumption in hello UI, it is best too[create a Marketplace item](azure-stack-create-and-publish-marketplace-item.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3079-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f3079-199">Next steps</span></span>

[<span data-ttu-id="f3079-200">Approvisionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f3079-200">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)