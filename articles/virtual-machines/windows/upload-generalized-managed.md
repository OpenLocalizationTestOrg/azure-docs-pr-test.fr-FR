---
title: "aaaCreate un managé Azure VM à partir d’un disque dur virtuel généralisé local | Documents Microsoft"
description: "Télécharger un tooAzure de disque dur virtuel généralisé et utilisez-le toocreate nouvelles machines virtuelles, dans le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a>Télécharger un disque dur virtuel généralisé et utilisez-le toocreate nouvelles machines virtuelles dans Azure

Cette rubrique vous guide à l’aide de PowerShell tooupload un disque dur virtuel d’un tooAzure de machine virtuelle généralisée, créer une image de disque dur virtuel de hello et créer une machine virtuelle à partir de cette image. Vous pouvez charger un disque dur virtuel exporté à partir d’un outil de virtualisation local ou d’un autre cloud. À l’aide de [disques gérés](managed-disks-overview.md) pour hello nouvelle machine virtuelle simplifie la gestion des ordinateurs virtuels hello et fournit une meilleure disponibilité lorsque hello VM est placé dans un ensemble de disponibilité. 

Si vous souhaitez toouse un exemple de script, consultez [exemple tooupload de script un tooAzure de disque dur virtuel et créer une machine virtuelle](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)

## <a name="before-you-begin"></a>Avant de commencer

- Avant de télécharger tout tooAzure de disque dur virtuel, vous devez suivre [préparer un tooAzure tooupload Windows VHD ou VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
- Révision [planifier la migration de hello de disques de tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) avant de commencer votre migration trop[disques gérés](managed-disks-overview.md).
- Assurez-vous que vous avez hello dernière version du module PowerShell de AzureRM.Compute de hello. Exécutez hello après la commande tooinstall il.

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).


## <a name="generalize-hello-windows-vm-using-sysprep"></a>Généraliser hello virtuelle Windows à l’aide de Sysprep

Sysprep supprime toutes vos informations de compte personnel, entre autres choses et prépare hello machine toobe est utilisé en tant qu’image. Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx).

Assurez-vous que les rôles de serveur hello en cours d’exécution sur l’ordinateur de hello sont pris en charge par Sysprep. Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Si vous exécutez Sysprep avant de télécharger votre tooAzure de disque dur virtuel pour hello première fois, vérifiez que vous disposez [préparé votre machine virtuelle](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’exécuter Sysprep. 
> 
> 

1. Se connecter toohello machine virtuelle Windows.
2. Ouvrez la fenêtre d’invite de commandes hello en tant qu’administrateur. Basculez hello trop**%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.
3. Bonjour **outil de préparation système** boîte de dialogue, sélectionnez **entrer le système Out-of-Box Experience (OOBE)**et assurez-vous que hello **Generalize** case à cocher est activée.
4. Dans **Options d’arrêt**, sélectionnez **Arrêter**.
5. Cliquez sur **OK**.
   
    ![Démarrer Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Quand Sysprep se termine, il arrête de machine virtuelle de hello. Ne redémarrez pas hello machine virtuelle.



## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure
Si vous n’avez pas encore PowerShell version 1.4 ou version ultérieure installé, lire [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

1. Ouvrez Azure PowerShell et connectez-vous à tooyour compte Azure. Une fenêtre contextuelle s’ouvre pour vous tooenter vos informations d’identification de compte Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Obtenir l’ID d’abonnement hello pour vos abonnements disponibles.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Définir l’abonnement approprié de hello à l’aide des ID d’abonnement hello. Remplacez  *<subscriptionID>*  avec l’ID de hello Hello corriger l’abonnement.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a>Obtenir le compte de stockage hello
Vous avez besoin d’un compte de stockage dans l’image de machine virtuelle Azure toostore hello téléchargé. Vous pouvez utiliser un compte de stockage existant ou en créer un. 

Si vous utilisez hello toocreate de disque dur virtuel un disque géré pour une machine virtuelle, emplacement du compte de stockage hello doit être même hello où vous allez créer hello machine virtuelle.

comptes de stockage disponibles hello tooshow, tapez :

```powershell
Get-AzureRmStorageAccount
```

Si vous voulez toouse un compte de stockage existant, passez toohello [image de machine virtuelle téléchargement hello](#upload-the-vm-vhd-to-your-storage-account) section.

Si vous avez besoin de toocreate un compte de stockage, procédez comme suit :

1. Vous devez nom hello hello du groupe de ressources où le compte de stockage hello doit être créé. toofind tous les groupes de ressources hello qui se trouvent dans votre abonnement, type :
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    toocreate un groupe de ressources nommé **myResourceGroup** Bonjour **États-Unis** région, tapez :

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. Créer un compte de stockage nommé **mystorageaccount** dans ce groupe de ressources à l’aide de hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) applet de commande :
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    Les valeurs valides pour -SkuName sont :
   
   * **Standard_LRS** - Stockage localement redondant. 
   * **Standard_ZRS** - Stockage redondant dans une zone.
   * **Standard_GRS** - Stockage géo-redondant. 
   * **Standard_RAGRS** - Stockage géo-redondant avec accès en lecture. 
   * **Premium_LRS** - Stockage Premium localement redondant. 

## <a name="upload-hello-vhd-tooyour-storage-account"></a>Télécharger le compte de stockage tooyour hello disque dur virtuel

Hello d’utilisation [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) conteneur applet de commande tooupload hello VHD tooa dans votre compte de stockage. Cet exemple téléchargements hello fichier *myVHD.vhd* de *» des disques durs C:\Users\Public\Documents\Virtual\"*  tooa compte de stockage nommé *mystorageaccount*Bonjour *myResourceGroup* groupe de ressources. fichier de Hello est placé dans le conteneur hello nommé *mycontainer* et nouveau nom de fichier hello seront *myUploadedVHD.vhd*.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


En cas de réussite, vous obtenez une réponse qui recherche toothis similaire :

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

Selon votre connexion réseau et la taille de hello de votre fichier de disque dur virtuel, cette commande peut prendre un certain temps toocomplete

Enregistrer hello **URI de Destination** toouse de chemin d’accès plus tard si vous vous apprêtez toocreate un disque géré ou un nouvel ordinateur virtuel à l’aide de hello téléchargé le disque dur virtuel.

### <a name="other-options-for-uploading-a-vhd"></a>Autres options de téléchargement d’un disque dur virtuel
 
 
Vous pouvez également télécharger un compte de stockage de tooyour de disque dur virtuel à l’aide de valeurs hello suivantes :

- [AZCopy](http://aka.ms/downloadazcopy)
- [API de copie d’un objet blob de stockage Azure](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [Téléchargement d’objets blob dans Storage Explorer](https://azurestorageexplorer.codeplex.com/)
- [Référence sur l’API REST du service Import/Export Storage](https://msdn.microsoft.com/library/dn529096.aspx)
-   Nous recommandons l’utilisation de du service d’importation/exportation si l’estimation du temps de téléchargement est de plus de 7 jours. Vous pouvez utiliser [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate les temps de hello à partir de l’unité de taille et de transfert de données. 
    Importation/exportation peut être utilisé le compte de stockage standard toocopy tooa. Vous devez toocopy de compte de stockage toopremium de stockage standard à l’aide d’un outil tel que AzCopy.


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a>Créer un objet image à partir de hello téléchargé le disque dur virtuel 

Créez une image managée à l’aide de votre disque dur virtuel généralisé de système d’exploitation. Remplacez les valeurs hello par vos propres informations.


1.  Tout d’abord, définissez les paramètres communs hello :

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  Créer l’image de hello à l’aide de votre disque dur virtuel du système d’exploitation généralisé.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a>Créez un réseau virtuel
Créer le réseau virtuel de hello et un sous-réseau de hello [réseau virtuel](../../virtual-network/virtual-networks-overview.md).

1. Créer un sous-réseau de hello. Cet exemple crée un sous-réseau nommé *mySubnet* avec le préfixe d’adresse de hello *10.0.0.0/24*.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Créer un réseau virtuel de hello. Cet exemple crée un réseau virtuel nommé *myVnet* avec le préfixe d’adresse de hello *10.0.0.0/16*.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Création d'une adresse IP publique et une interface réseau

tooenable une communication avec l’ordinateur virtuel de hello dans le réseau virtuel de hello, vous devez un [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et une interface réseau.

1. Créez une adresse IP publique. Cet exemple crée une adresse IP publique nommée *myPip*. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Créer la carte de réseau hello. Cet exemple crée une carte réseau nommée **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Créer une règle RDP et groupe de sécurité réseau hello

toolog en mesure de toobe dans tooyour machine virtuelle à l’aide du protocole RDP, vous devez toohave une règle de sécurité réseau (NSG) qui autorise l’accès RDP sur le port 3389. 

Cet exemple crée un groupe de sécurité réseau nommé *myNsg* qui contient une règle nommée *myRdpRule* autorisant le trafic RDP sur le port 3389. Pour plus d’informations sur les groupes de sécurité réseau, consultez [l’ouverture de ports tooa machine virtuelle dans Azure à l’aide de PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Créez une variable pour le réseau virtuel de hello

Créez une variable pour le réseau virtuel de hello s’est terminée. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Obtenir des informations d’identification de hello pour hello machine virtuelle

Hello applet de commande suivante ouvre une fenêtre dans laquelle vous entrerez un toouse nouveau du nom et mot de passe utilisateur en tant que compte d’administrateur local hello pour accéder à distance aux hello machine virtuelle. 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a>Ajoutez hello nom d’ordinateur virtuel et configuration d’ordinateur virtuel de taille toohello.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Image de machine virtuelle hello ensemble en tant qu’image source pour hello nouvelle machine virtuelle

Définir l’image source de hello à l’aide de code hello d’image de machine virtuelle hello géré.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Définir la configuration du système d’exploitation hello et ajouter de carte réseau de hello.

Entrez le type de stockage de hello (PremiumLRS ou StandardLRS) et la taille de hello du disque du système d’exploitation hello. Cet exemple définit le type de compte hello trop*PremiumLRS*, hello trop de taille de disque*128 Go* et mise en cache disque trop*ReadWrite*.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Créer hello machine virtuelle

Créer la nouvelle machine virtuelle à l’aide de la configuration de hello stockée Bonjour hello **$vm** variable.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Vérifiez que hello que machine virtuelle a été créée.
Lorsque vous avez terminé, vous devez voir hello nouvellement créé VM dans hello [portail Azure](https://portal.azure.com) sous **Parcourir** > **virtuels**, ou en utilisant hello Commandes PowerShell :

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Étapes suivantes

toosign dans tooyour nouvel ordinateur virtuel, parcourir toohello VM Bonjour [portal](https://portal.azure.com), cliquez sur **connexion**et le fichier de bureau à distance ouverte hello. Utilisez les informations d’identification du compte de hello de votre toosign d’ordinateur virtuel d’origine dans la machine virtuelle tooyour. Pour plus d’informations, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

