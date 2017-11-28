---
title: "aaaAzure avantage d’utiliser hybride pour Windows Server et Windows Client | Documents Microsoft"
description: "Découvrez comment toomaximize votre toobring avantages de Windows Software Assurance sur site licences tooAzure"
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="ebaa9-103">Azure Hybrid Use Benefit pour Windows Server et client Windows</span><span class="sxs-lookup"><span data-stu-id="ebaa9-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="ebaa9-104">Pour les clients avec Software Assurance, avantage d’utiliser Azure hybride vous permet de toouse vos licences de Windows Server et Windows Client local et l’exécution virtuels Windows dans Azure à moindre coût.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you toouse your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="ebaa9-105">Azure Hybrid Use Benefit pour Windows Server inclut Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2 et Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="ebaa9-106">Azure Hybrid Use Benefit pour le client Windows inclut Windows 10.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="ebaa9-107">Pour plus d’informations, consultez hello [page de licence avantage d’utiliser Azure hybride](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-107">For more information, please see hello [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="ebaa9-108">Azure hybride utilisez avantages pour Client Windows est actuellement en version préliminaire à l’aide d’image de Windows 10 de hello Bonjour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using hello Windows 10 image in hello Azure Marketplace.</span></span> <span data-ttu-id="ebaa9-109">Seuls les clients Enterprise avec Windows 10 Entreprise E3/E5 par utilisateur ou Windows VDA par utilisateur (licences d’abonnement utilisateur ou module complémentaire de licence d’abonnement utilisateur) (« licences éligibles ») sont éligibles.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a><span data-ttu-id="ebaa9-110">Méthodes toouse avantage d’utiliser Azure hybride</span><span class="sxs-lookup"><span data-stu-id="ebaa9-110">Ways toouse Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="ebaa9-111">Il existe deux façons différentes toodeploy les machines virtuelles Windows avec hello avantage d’utiliser Azure hybride :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-111">There are a couple of different ways toodeploy Windows VMs with hello Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="ebaa9-112">Vous pouvez déployer des machines virtuelles à partir [d’images spécifiques de la Place de marché](#deploy-a-vm-using-the-azure-marketplace) qui sont préconfigurées avec Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 et Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="ebaa9-113">Vous pouvez [télécharger une machine virtuelle personnalisée](#upload-a-windows-vhd) et [effectuez le déploiement à l’aide d’un modèle Resource Manager](#deploy-a-vm-via-resource-manager) ou [d’Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a><span data-ttu-id="ebaa9-114">Déployer un ordinateur virtuel à l’aide de hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ebaa9-114">Deploy a VM using hello Azure Marketplace</span></span>
<span data-ttu-id="ebaa9-115">Les images suivantes sont disponibles dans hello Marketplace préconfiguré avec l’avantage d’utiliser Azure hybride : Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-115">Following images are available in hello Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="ebaa9-116">Ces images peuvent être déployés directement à partir de hello portail Azure, les modèles de gestionnaire de ressources ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-116">These images can be deployed directly from hello Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="ebaa9-117">Vous pouvez déployer ces images directement à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-117">You can deploy these images directly from hello Azure portal.</span></span> <span data-ttu-id="ebaa9-118">Pour une utilisation dans les modèles de gestionnaire de ressources et avec Azure PowerShell, affichez la liste hello des images comme suit :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-118">For use in Resource Manager templates and with Azure PowerShell, view hello list of images as follows:</span></span>

<span data-ttu-id="ebaa9-119">Pour Windows Server :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="ebaa9-120">2016-Datacenter version 2016.127.20170406 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="ebaa9-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="ebaa9-121">2012-R2-Datacenter version 4.127.20170406 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="ebaa9-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="ebaa9-122">2012-Datacenter version 3.127.20170406 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="ebaa9-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="ebaa9-123">2008-R2-SP1 version 2.127.20170406 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="ebaa9-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="ebaa9-124">Pour le client Windows :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="ebaa9-125">Téléchargement d’un disque dur virtuel Windows Server</span><span class="sxs-lookup"><span data-stu-id="ebaa9-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="ebaa9-126">toodeploy une machine virtuelle Windows Server dans Azure, vous devez tout d’abord toocreate un disque dur virtuel qui contient votre build Windows de base.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-126">toodeploy a Windows Server VM in Azure, you first need toocreate a VHD that contains your base Windows build.</span></span> <span data-ttu-id="ebaa9-127">Ce disque dur virtuel doit être correctement préparé par Sysprep avant de le télécharger tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-127">This VHD must be appropriately prepared via Sysprep before you upload it tooAzure.</span></span> <span data-ttu-id="ebaa9-128">Vous pouvez [en savoir plus sur la configuration requise de disque dur virtuel hello et processus Sysprep](upload-generalized-managed.md) et [prise en charge de Sysprep pour les rôles de serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-128">You can [read more about hello VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="ebaa9-129">Sauvegardez hello machine virtuelle avant d’exécuter Sysprep.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-129">Back up hello VM before running Sysprep.</span></span> 

<span data-ttu-id="ebaa9-130">Assurez-vous que vous avez [installé et hello configuré Azure PowerShell dernière](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-130">Make sure you have [installed and configured hello latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="ebaa9-131">Une fois que vous avez préparé votre disque dur virtuel, téléchargez le compte de stockage Azure hello VHD tooyour à l’aide de hello `Add-AzureRmVhd` applet de commande comme suit :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-131">Once you have prepared your VHD, upload hello VHD tooyour Azure Storage account using hello `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="ebaa9-132">Microsoft SQL Server, SharePoint Server et Dynamics peuvent également utiliser vos licences Software Assurance.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="ebaa9-133">Vous devez toujours l’image de Windows Server tooprepare hello par l’installation des composants de votre application et en fournissant des clés de licence en conséquence, puis télécharger hello disque image tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-133">You still need tooprepare hello Windows Server image by installing your application components and providing license keys accordingly, then uploading hello disk image tooAzure.</span></span> <span data-ttu-id="ebaa9-134">Passez en revue la documentation appropriée de hello pour l’exécution de Sysprep avec votre application, telles que [considérations pour l’installation de SQL Server à l’aide de Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) ou [créer une Image de référence SharePoint Server 2016 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-134">Review hello appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="ebaa9-135">Vous pouvez également en savoir plus sur [hello VHD tooAzure processus de téléchargement](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="ebaa9-135">You can also read more about [uploading hello VHD tooAzure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="ebaa9-136">Déployer une machine virtuelle à l’aide du modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ebaa9-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="ebaa9-137">Dans vos modèles Resource Manager, vous pouvez spécifier un paramètre supplémentaire pour `licenseType` .</span><span class="sxs-lookup"><span data-stu-id="ebaa9-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="ebaa9-138">Pour en savoir plus sur la création de modèles Azure Resource Manager, [cliquez ici](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="ebaa9-139">Une fois que vous avez tooAzure de votre disque dur virtuel téléchargé, modifier vous type de licence de gestionnaire de ressources du modèle tooinclude hello comme partie de hello fournisseur de calcul et déployer votre modèle normalement :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-139">Once you have your VHD uploaded tooAzure, edit you Resource Manager template tooinclude hello license type as part of hello compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="ebaa9-140">Pour Windows Server :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="ebaa9-141">Pour toouse de Client Windows avec une Image Marketplace Azure uniquement :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-141">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="ebaa9-142">Déployer une machine virtuelle à l’aide du démarrage rapide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebaa9-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="ebaa9-143">Lors du déploiement de votre machine virtuelle Windows Server par le biais de PowerShell, vous disposez d’un paramètre supplémentaire pour `-LicenseType`.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="ebaa9-144">Une fois que vous avez tooAzure de votre disque dur virtuel téléchargé, vous créez une machine virtuelle à l’aide de `New-AzureRmVM` et spécifiez le type de licence hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-144">Once you have your VHD uploaded tooAzure, you create a VM using `New-AzureRmVM` and specify hello licensing type as follows:</span></span>

<span data-ttu-id="ebaa9-145">Pour Windows Server :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="ebaa9-146">Pour toouse de Client Windows avec une Image Marketplace Azure uniquement :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-146">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="ebaa9-147">Vous pouvez [lire une description plus détaillée sur le déploiement d’une machine virtuelle dans Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) ci-dessous, ou de lire un guide plus descriptif hello différentes étapes trop[créer une machine virtuelle de Windows à l’aide du Gestionnaire de ressources et PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on hello different steps too[create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a><span data-ttu-id="ebaa9-148">Vérifiez que votre machine virtuelle utilise avantage de licences hello</span><span class="sxs-lookup"><span data-stu-id="ebaa9-148">Verify your VM is utilizing hello licensing benefit</span></span>
<span data-ttu-id="ebaa9-149">Une fois que vous avez déployé votre machine virtuelle via hello PowerShell ou de la méthode de déploiement Resource Manager, vérifiez le type de licence hello avec `Get-AzureRmVM` comme suit :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-149">Once you have deployed your VM through either hello PowerShell or Resource Manager deployment method, verify hello license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="ebaa9-150">Hello la sortie est similaire toohello exemple suivant pour Windows Server :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-150">hello output is similar toohello following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="ebaa9-151">Cette sortie contraste avec hello que suivant de machine virtuelle déployée sans l’avantage d’utiliser Azure hybride de licences, par exemple un ordinateur virtuel déployé directement à partir de la galerie Azure de hello :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-151">This output contrasts with hello following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from hello Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="ebaa9-152">Procédure détaillée de déploiement avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebaa9-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="ebaa9-153">suivant de Hello détaillées afficher des étapes PowerShell un déploiement complet d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-153">hello following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="ebaa9-154">Vous pouvez lire davantage de contexte en tant que toohello réel applets de commande et les différents composants en cours de création dans [créer une machine virtuelle de Windows à l’aide du Gestionnaire de ressources et PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-154">You can read more context as toohello actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ebaa9-155">Vous créez votre groupe de ressources, votre compte de stockage et votre réseau virtuel, puis définissez et créez votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="ebaa9-156">Tout d’abord, procurez-vous des informations d’identification de manière sécurisée, puis définissez un emplacement et le nom du groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="ebaa9-157">Créez une adresse IP publique :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="ebaa9-158">Définissez votre sous-réseau, votre carte réseau et votre réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-158">Define your subnet, NIC, and VNET:</span></span>

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

<span data-ttu-id="ebaa9-159">Nommez votre machine virtuelle et créez une configuration de machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="ebaa9-160">Définissez votre serveur DNS :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="ebaa9-161">Ajoutez votre toohello de carte réseau virtuelle :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-161">Add your NIC toohello VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="ebaa9-162">Définissez toouse de compte de stockage hello :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-162">Define hello storage account toouse:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="ebaa9-163">Télécharger votre disque dur virtuel, convenablement préparé et joindre tooyour machine virtuelle à utiliser :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-163">Upload your VHD, suitably prepared, and attach tooyour VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="ebaa9-164">Enfin, créer votre machine virtuelle et définir hello licences type tooutilize avantage d’utiliser Azure hybride :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-164">Finally, create your VM and define hello licensing type tooutilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="ebaa9-165">Pour Windows Server :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="ebaa9-166">Déployez un groupe de machines virtuelles identiques avec un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ebaa9-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="ebaa9-167">Dans vos modèles Resource Manager de groupe de machines virtuelles identiques, vous pouvez spécifier un paramètre supplémentaire pour `licenseType` .</span><span class="sxs-lookup"><span data-stu-id="ebaa9-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="ebaa9-168">Pour en savoir plus sur la création de modèles Azure Resource Manager, [cliquez ici](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="ebaa9-169">Modifier votre propriété de gestionnaire de ressources du modèle tooinclude hello licenseType dans le cadre de virtualMachineProfile de l’ensemble d’échelle hello et déployer votre modèle normalement - voir l’exemple ci-dessous à l’aide d’image de Windows Server 2016 :</span><span class="sxs-lookup"><span data-stu-id="ebaa9-169">Edit your Resource Manager template tooinclude hello licenseType property as part of hello scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> <span data-ttu-id="ebaa9-170">La prise en charge du déploiement d’un groupe de machines virtuelles identiques avec des avantages AHUB via PowerShell et d’autres outils de kit SDK sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="ebaa9-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="ebaa9-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ebaa9-171">Next steps</span></span>
<span data-ttu-id="ebaa9-172">En savoir plus sur les [licences Azure Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="ebaa9-173">En savoir plus sur [l’utilisation de modèles Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="ebaa9-174">En savoir plus sur [avantage d’utiliser Azure hybride et Azure Site Recovery rendent migration tooAzure d’applications même plus rentable](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span><span class="sxs-lookup"><span data-stu-id="ebaa9-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications tooAzure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>
