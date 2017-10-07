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
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a>Azure Hybrid Use Benefit pour Windows Server et client Windows
Pour les clients avec Software Assurance, avantage d’utiliser Azure hybride vous permet de toouse vos licences de Windows Server et Windows Client local et l’exécution virtuels Windows dans Azure à moindre coût. Azure Hybrid Use Benefit pour Windows Server inclut Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2 et Windows Server 2016. Azure Hybrid Use Benefit pour le client Windows inclut Windows 10. Pour plus d’informations, consultez hello [page de licence avantage d’utiliser Azure hybride](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

>[!IMPORTANT]
>Azure hybride utilisez avantages pour Client Windows est actuellement en version préliminaire à l’aide d’image de Windows 10 de hello Bonjour Azure Marketplace. Seuls les clients Enterprise avec Windows 10 Entreprise E3/E5 par utilisateur ou Windows VDA par utilisateur (licences d’abonnement utilisateur ou module complémentaire de licence d’abonnement utilisateur) (« licences éligibles ») sont éligibles.
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a>Méthodes toouse avantage d’utiliser Azure hybride
Il existe deux façons différentes toodeploy les machines virtuelles Windows avec hello avantage d’utiliser Azure hybride :

1. Vous pouvez déployer des machines virtuelles à partir [d’images spécifiques de la Place de marché](#deploy-a-vm-using-the-azure-marketplace) qui sont préconfigurées avec Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 et Windows Server 2008SP1.
2. Vous pouvez [télécharger une machine virtuelle personnalisée](#upload-a-windows-vhd) et [effectuez le déploiement à l’aide d’un modèle Resource Manager](#deploy-a-vm-via-resource-manager) ou [d’Azure PowerShell](#detailed-powershell-deployment-walkthrough).

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a>Déployer un ordinateur virtuel à l’aide de hello Azure Marketplace
Les images suivantes sont disponibles dans hello Marketplace préconfiguré avec l’avantage d’utiliser Azure hybride : Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008SP1. Ces images peuvent être déployés directement à partir de hello portail Azure, les modèles de gestionnaire de ressources ou Azure PowerShell.

Vous pouvez déployer ces images directement à partir de hello portail Azure. Pour une utilisation dans les modèles de gestionnaire de ressources et avec Azure PowerShell, affichez la liste hello des images comme suit :

Pour Windows Server :
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- 2016-Datacenter version 2016.127.20170406 ou ultérieure

- 2012-R2-Datacenter version 4.127.20170406 ou ultérieure

- 2012-Datacenter version 3.127.20170406 ou ultérieure

- 2008-R2-SP1 version 2.127.20170406 ou ultérieure

Pour le client Windows :
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a>Téléchargement d’un disque dur virtuel Windows Server
toodeploy une machine virtuelle Windows Server dans Azure, vous devez tout d’abord toocreate un disque dur virtuel qui contient votre build Windows de base. Ce disque dur virtuel doit être correctement préparé par Sysprep avant de le télécharger tooAzure. Vous pouvez [en savoir plus sur la configuration requise de disque dur virtuel hello et processus Sysprep](upload-generalized-managed.md) et [prise en charge de Sysprep pour les rôles de serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles). Sauvegardez hello machine virtuelle avant d’exécuter Sysprep. 

Assurez-vous que vous avez [installé et hello configuré Azure PowerShell dernière](/powershell/azure/overview). Une fois que vous avez préparé votre disque dur virtuel, téléchargez le compte de stockage Azure hello VHD tooyour à l’aide de hello `Add-AzureRmVhd` applet de commande comme suit :

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> Microsoft SQL Server, SharePoint Server et Dynamics peuvent également utiliser vos licences Software Assurance. Vous devez toujours l’image de Windows Server tooprepare hello par l’installation des composants de votre application et en fournissant des clés de licence en conséquence, puis télécharger hello disque image tooAzure. Passez en revue la documentation appropriée de hello pour l’exécution de Sysprep avec votre application, telles que [considérations pour l’installation de SQL Server à l’aide de Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) ou [créer une Image de référence SharePoint Server 2016 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).
>
>

Vous pouvez également en savoir plus sur [hello VHD tooAzure processus de téléchargement](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)


## <a name="deploy-a-vm-via-resource-manager-template"></a>Déployer une machine virtuelle à l’aide du modèle Resource Manager
Dans vos modèles Resource Manager, vous pouvez spécifier un paramètre supplémentaire pour `licenseType` . Pour en savoir plus sur la création de modèles Azure Resource Manager, [cliquez ici](../../resource-group-authoring-templates.md). Une fois que vous avez tooAzure de votre disque dur virtuel téléchargé, modifier vous type de licence de gestionnaire de ressources du modèle tooinclude hello comme partie de hello fournisseur de calcul et déployer votre modèle normalement :

Pour Windows Server :
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

Pour toouse de Client Windows avec une Image Marketplace Azure uniquement :
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a>Déployer une machine virtuelle à l’aide du démarrage rapide de PowerShell
Lors du déploiement de votre machine virtuelle Windows Server par le biais de PowerShell, vous disposez d’un paramètre supplémentaire pour `-LicenseType`. Une fois que vous avez tooAzure de votre disque dur virtuel téléchargé, vous créez une machine virtuelle à l’aide de `New-AzureRmVM` et spécifiez le type de licence hello comme suit :

Pour Windows Server :
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

Pour toouse de Client Windows avec une Image Marketplace Azure uniquement :
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

Vous pouvez [lire une description plus détaillée sur le déploiement d’une machine virtuelle dans Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) ci-dessous, ou de lire un guide plus descriptif hello différentes étapes trop[créer une machine virtuelle de Windows à l’aide du Gestionnaire de ressources et PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a>Vérifiez que votre machine virtuelle utilise avantage de licences hello
Une fois que vous avez déployé votre machine virtuelle via hello PowerShell ou de la méthode de déploiement Resource Manager, vérifiez le type de licence hello avec `Get-AzureRmVM` comme suit :

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

Hello la sortie est similaire toohello exemple suivant pour Windows Server :

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

Cette sortie contraste avec hello que suivant de machine virtuelle déployée sans l’avantage d’utiliser Azure hybride de licences, par exemple un ordinateur virtuel déployé directement à partir de la galerie Azure de hello :

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a>Procédure détaillée de déploiement avec PowerShell
suivant de Hello détaillées afficher des étapes PowerShell un déploiement complet d’une machine virtuelle. Vous pouvez lire davantage de contexte en tant que toohello réel applets de commande et les différents composants en cours de création dans [créer une machine virtuelle de Windows à l’aide du Gestionnaire de ressources et PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Vous créez votre groupe de ressources, votre compte de stockage et votre réseau virtuel, puis définissez et créez votre machine virtuelle.

Tout d’abord, procurez-vous des informations d’identification de manière sécurisée, puis définissez un emplacement et le nom du groupe de ressources :

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

Créez une adresse IP publique :

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

Définissez votre sous-réseau, votre carte réseau et votre réseau virtuel :

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

Nommez votre machine virtuelle et créez une configuration de machine virtuelle :

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

Définissez votre serveur DNS :

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Ajoutez votre toohello de carte réseau virtuelle :

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Définissez toouse de compte de stockage hello :

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

Télécharger votre disque dur virtuel, convenablement préparé et joindre tooyour machine virtuelle à utiliser :

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

Enfin, créer votre machine virtuelle et définir hello licences type tooutilize avantage d’utiliser Azure hybride :

Pour Windows Server :
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a>Déployez un groupe de machines virtuelles identiques avec un modèle Resource Manager
Dans vos modèles Resource Manager de groupe de machines virtuelles identiques, vous pouvez spécifier un paramètre supplémentaire pour `licenseType` . Pour en savoir plus sur la création de modèles Azure Resource Manager, [cliquez ici](../../resource-group-authoring-templates.md). Modifier votre propriété de gestionnaire de ressources du modèle tooinclude hello licenseType dans le cadre de virtualMachineProfile de l’ensemble d’échelle hello et déployer votre modèle normalement - voir l’exemple ci-dessous à l’aide d’image de Windows Server 2016 :


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
> La prise en charge du déploiement d’un groupe de machines virtuelles identiques avec des avantages AHUB via PowerShell et d’autres outils de kit SDK sera bientôt disponible.
>

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les [licences Azure Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

En savoir plus sur [l’utilisation de modèles Resource Manager](../../azure-resource-manager/resource-group-overview.md).

En savoir plus sur [avantage d’utiliser Azure hybride et Azure Site Recovery rendent migration tooAzure d’applications même plus rentable](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).
