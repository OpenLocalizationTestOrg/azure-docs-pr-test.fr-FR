---
title: "aaaCreate machine virtuelle à partir d’un disque spécialisé dans Azure | Documents Microsoft"
description: "Créer une machine virtuelle en attachant un disque spécialisé non managé, dans le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a>Création d’une machine virtuelle à partir d’un disque dur virtuel spécialisé dans un compte de stockage

Créer une machine virtuelle en attachant un disque spécialisé de non managé en tant que disque de système d’exploitation hello à l’aide de Powershell. Un disque spécialisé est une copie du disque dur virtuel à partir d’une machine virtuelle existante qui gère les comptes d’utilisateur hello, des applications et autres données d’état à partir de votre machine virtuelle d’origine. 

Deux options s'offrent à vous :
* [Charger un disque dur virtuel](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [Copiez hello disque dur virtuel d’une machine virtuelle Azure existante](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a>Avant de commencer
Si vous utilisez PowerShell, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello. Exécutez hello après la commande tooinstall il.

```powershell
Install-Module AzureRM.Compute 
```
Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Option 1 : Charger un disque dur virtuel spécialisé

Vous pouvez télécharger hello que disque dur virtuel à partir d’une machine virtuelle spécialisée créé avec un outil de virtualisation sur site, telles que Hyper-V ou un ordinateur virtuel exporté à partir d’un autre cloud.

### <a name="prepare-hello-vm"></a>Préparer hello machine virtuelle
Vous pouvez charger un disque dur virtuel spécialisé créé à l’aide d’une machine virtuelle sur site ou un disque dur virtuel exporté à partir d’un autre cloud. Un disque dur virtuel spécialisé gère les comptes d’utilisateur hello, des applications et autres données d’état à partir de votre machine virtuelle d’origine. Si vous avez l’intention toouse hello du disque dur virtuel en tant que-est toocreate un nouvel ordinateur virtuel, vérifiez hello suivant étapes est terminée. 
  
  * [Préparer un tooAzure tooupload de disque dur virtuel Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Ne le faites pas** généraliser hello machine virtuelle à l’aide de Sysprep.
  * Supprimer les outils de virtualisation invité et les agents installés sur hello VM (autrement dit, les outils VMware).
  * Assurez-vous de hello machine virtuelle est configurée toopull son adresse IP et les paramètres DNS via DHCP. Cela garantit que ce serveur hello Obtient une adresse IP dans le réseau virtuel de hello lors de son démarrage. 


### <a name="get-hello-storage-account"></a>Obtenir le compte de stockage hello
Vous avez besoin d’un compte de stockage dans l’image de machine virtuelle Azure toostore hello téléchargé. Vous pouvez utiliser un compte de stockage existant ou en créer un. 

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

    toocreate un groupe de ressources nommé **myResourceGroup** Bonjour **ouest des États-Unis** région, tapez :

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Créer un compte de stockage nommé **mystorageaccount** dans ce groupe de ressources à l’aide de hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) applet de commande :
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a>Télécharger le compte de stockage tooyour hello disque dur virtuel
Hello d’utilisation [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) conteneur tooa d’images de hello tooupload applet de commande dans votre compte de stockage. Cet exemple montre comment les téléchargements hello fichier **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa compte de stockage nommé **mystorageaccount** Bonjour **myResourceGroup** groupe de ressources. fichier de Hello est placé dans le conteneur hello nommé **mycontainer** et nouveau nom de fichier hello seront **myUploadedVHD.vhd**.

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

Cette commande peut prendre du temps en fonction de votre connexion réseau et la taille de hello de votre fichier de disque dur virtuel, toocomplete.


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a>Option 2 : Copiez hello disque dur virtuel à partir d’une machine virtuelle Azure existante

Vous pouvez copier un toouse de compte de stockage tooanother disque dur virtuel lors de la création d’une machine virtuelle au nouveau, en double.

### <a name="before-you-begin"></a>Avant de commencer
Veillez à :

* Informations sur hello **comptes de stockage source et destination**. Pour la source de hello machine virtuelle, vous devez toohave hello compte conteneur de noms de stockage et. En règle générale, le nom du conteneur hello sera **disques durs virtuels**. Vous devez également toohave un compte de stockage de destination. Si vous n’en avez déjà, vous pouvez créer un à l’aide de des portails hello (**plus Services** > comptes de stockage > Add) ou à l’aide de hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) applet de commande. 
* Téléchargé et installé hello [outil AzCopy](../../storage/common/storage-use-azcopy.md). 

### <a name="deallocate-hello-vm"></a>Désallouer hello machine virtuelle
Désallouer hello machine virtuelle, ce qui libère des hello toobe de disque dur virtuel copié. 

* **Portail** : cliquez sur **Machines virtuelles** > **myVM** &gt; Arrêter
* **PowerShell**: utilisez [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (désallouer) hello d’ordinateur virtuel nommé **myVM** dans le groupe de ressources **myResourceGroup**.

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Hello **état** pour hello VM Bonjour Azure portal passe de **arrêté** trop**arrêté (désallouée)**.

### <a name="get-hello-storage-account-urls"></a>Obtenir l’URL de compte de stockage hello
Vous devez URL hello hello source et destination de comptes de stockage. Hello URL ressembler à : `https://<storageaccount>.blob.core.windows.net/<containerName>/`. Si vous connaissez déjà le nom de compte et conteneur de stockage hello, vous pouvez simplement remplacer informations hello entre hello crochets toocreate votre URL. 

Vous pouvez utiliser hello portail Azure ou Azure Powershell tooget hello URL :

* **Portail**: cliquez sur hello  **>**  pour **davantage de services** > **comptes de stockage**  >   *compte de stockage* > **BLOB** et votre fichier de disque dur virtuel source est probablement Bonjour **disques durs virtuels** conteneur. Cliquez sur **propriétés** pour le conteneur de hello et copier le texte hello étiqueté **URL**. Vous aurez besoin des URL hello de deux conteneurs de hello source et de destination. 
* **PowerShell**: utilisez [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget les informations de hello pour l’ordinateur virtuel nommé **myVM** dans le groupe de ressources hello **myResourceGroup**. Dans les résultats de hello, recherchez dans hello **profil de stockage** section pour hello **Vhd Uri**. Hello première partie de hello Uri est le conteneur de toohello URL hello et hello dernière partie est hello nom de disque dur virtuel du système d’exploitation pour hello machine virtuelle.

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a>Obtenir les clés d’accès de stockage de hello
Rechercher des clés d’accès hello pour hello comptes de stockage source et de destination. Pour plus d’informations sur les clés d’accès, consultez la page [À propos des comptes de stockage Azure](../../storage/common/storage-create-storage-account.md).

* **Portail** : cliquez sur **Plus de services** > **Comptes de stockage** > *compte de stockage* > **Clés d’accès**. Copier la clé hello étiquetés comme **key1**.
* **PowerShell**: utilisez [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello stockage clé hello compte de stockage **mystorageaccount** dans le groupe de ressources hello  **myResourceGroup**. Copier la clé hello étiquetée **key1**.

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a>Copiez hello disque dur virtuel
Vous pouvez copier des fichiers entre comptes de stockage avec AzCopy. Pour le conteneur de destination hello, si le conteneur spécifié de hello n’existe pas, elle sera créée pour vous. 

toouse AzCopy, ouvrez une invite de commandes sur votre ordinateur local et l’exploration du dossier toohello où AzCopy est installé. Elle sera semblable trop*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*. 

toocopy hello tous les fichiers dans un conteneur, vous utilisez hello **/S** basculer. Cela peut être utilisé toocopy hello disque dur virtuel du système d’exploitation et tous les disques de données hello s’ils sont en hello même conteneur. Cet exemple montre comment toocopy hello tous les fichiers dans le conteneur de hello **mysourcecontainer** dans le compte de stockage **mysourcestorageaccount** toohello conteneur **mydestinationcontainer**  Bonjour **mydestinationstorageaccount** compte de stockage. Remplacez les noms de hello des comptes de stockage hello et des conteneurs par les vôtres. Remplacez `<sourceStorageAccountKey1>` et `<destinationStorageAccountKey1>` par vos propres clés.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

Si vous souhaitez uniquement toocopy un disque dur virtuel spécifique dans un conteneur avec plusieurs fichiers, vous pouvez également spécifier le nom du fichier à l’aide du commutateur de /Pattern hello hello. Dans cet exemple, uniquement hello fichier nommé **myFileName.vhd** seront copiés.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


Une fois la copie terminée, vous recevez un message du type :

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a>Résolution des problèmes
* Lorsque vous utilisez AZCopy, si vous voyez hello erreur « Échec de demande de hello tooauthenticate de serveur », assurez-vous que valeur hello de l’en-tête d’autorisation hello est formé correctement, notamment la signature de hello. Si vous utilisez la clé de 2 ou la clé de stockage secondaire hello, essayez d’utiliser la clé de stockage principal ou le 1er hello.

## <a name="create-hello-new-vm"></a>Créer hello nouvelle machine virtuelle 

Vous avez besoin de mise en réseau toocreate et autres toobe de ressources de machine virtuelle utilisée par hello nouvelle machine virtuelle.

### <a name="create-hello-subnet-and-vnet"></a>Créer le réseau virtuel et le sous-réseau de hello

Créer le réseau virtuel de hello et un sous-réseau de hello [réseau virtuel](../../virtual-network/virtual-networks-overview.md).

1. Créer un sous-réseau de hello. Cet exemple crée un sous-réseau nommé **mySubNet**, dans le groupe de ressources hello **myResourceGroup**, et les jeux de hello préfixe d’adresse de sous-réseau trop**10.0.0.0/24**.
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Créer un réseau virtuel de hello. Cet exemple définit hello toobe de nom de réseau virtuel **myVnetName**, hello emplacement trop**ouest des États-Unis**, et hello trop de préfixe d’adresse de réseau virtuel de hello**10.0.0.0/16**. 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a>Créer une adresse IP publique et une carte réseau
tooenable une communication avec l’ordinateur virtuel de hello dans le réseau virtuel de hello, vous devez un [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et une interface réseau.

1. Créer l’adresse IP publique hello. Dans cet exemple, le nom d’adresse IP publique hello est défini trop**myIP**.
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Créer la carte de réseau hello. Dans cet exemple, le nom de carte réseau hello est défini trop**myNicName**.
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Créer une règle RDP et groupe de sécurité réseau hello
toolog en mesure de toobe dans tooyour machine virtuelle à l’aide du protocole RDP, vous devez toohave une règle de sécurité qui autorise l’accès RDP sur le port 3389. Car hello disque dur virtuel pour hello que nouvel ordinateur virtuel a été créé à partir d’un fichier spécialisé machine virtuelle, après que hello machine virtuelle est créée, vous pouvez utiliser un compte existant à partir de l’ordinateur virtuel source hello avait toolog d’autorisation sur l’utilisation de RDP.
Cet exemple définit hello nom du groupe de sécurité réseau trop**myNsg** et nom de la règle hello RDP trop**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Pour plus d’informations sur les points de terminaison et les règles du groupe de sécurité réseau, consultez [l’ouverture de ports tooa machine virtuelle dans Azure à l’aide de PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="set-hello-vm-name-and-size"></a>Nom d’ordinateur virtuel hello et la taille

Cet exemple définit hello nom d’ordinateur virtuel trop « myVM » et hello VM taille trop « Standard_A2 ».
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Ajouter hello NIC
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a>Configurer le disque de hello du système d’exploitation

1. Définissez hello URI pour hello disque dur virtuel que vous avez téléchargé ou copié. Dans cet exemple, hello le fichier de disque dur virtuel nommé **myOsDisk.vhd** est conservée dans un compte de stockage nommé **myStorageAccount** dans un conteneur nommé **myContainer**.

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. Ajouter un disque de hello du système d’exploitation. Dans cet exemple, lorsque hello disque de système d’exploitation est créé, hello terme « osDisk » est le nom du disque du système d’exploitation nom toocreate hello appened toohello machine virtuelle. Cet exemple spécifie également que ce disque dur virtuel basé sur Windows doit être attaché toohello machine virtuelle en tant que disque de hello du système d’exploitation.
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

Facultatif : Si vous avez des disques de données qui toobe besoin attaché toohello VM, ajouter des disques de données hello à l’aide des URL hello de disques durs virtuels de données et hello approprié numéro d’unité logique (Lun).

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

Lorsque vous utilisez un compte de stockage, les données de salutation et URL de disque de système d’exploitation ressembler à ceci : `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`. Vous pouvez le trouver sur le portail hello en parcourant le conteneur de stockage cible toohello, en cliquant sur le système d’exploitation de hello ou des données de disque dur virtuel qui a été copié, puis en copiant contenu hello de hello URL.


### <a name="complete-hello-vm"></a>Machine virtuelle de hello terminée 

Créer hello machine virtuelle à l’aide de configurations de hello que nous venons de créer.

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

Si la commande a été exécutée avec succès, vous obtiendrez une sortie similaire à celle-ci :

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>Vérifiez que hello que machine virtuelle a été créée.
Vous devez voir hello nouvellement créées VM dans hello [portail Azure](https://portal.azure.com), sous **Parcourir** > **virtuels**, ou à l’aide de hello suivant PowerShell commandes :

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a>Étapes suivantes
toosign dans tooyour nouvel ordinateur virtuel, parcourir toohello VM Bonjour [portal](https://portal.azure.com), cliquez sur **connexion**et le fichier de bureau à distance ouverte hello. Utilisez les informations d’identification du compte de hello de votre toosign d’ordinateur virtuel d’origine dans la machine virtuelle tooyour. Pour plus d’informations, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](connect-logon.md).

