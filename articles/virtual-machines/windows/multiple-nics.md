---
title: "aaaCreate et gérer des machines virtuelles Windows dans Azure qui utilisent plusieurs cartes réseau | Documents Microsoft"
description: "Découvrez comment toocreate et gérer une machine virtuelle Windows qui a plusieurs tooit de cartes réseau attachée à l’aide de modèles Azure PowerShell ou le Gestionnaire de ressources."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a>Créer et gérer une machine virtuelle Windows équipée de plusieurs cartes d’interface réseau
Machines virtuelles (VM) dans Azure peut avoir plusieurs toothem de cartes (NIC) connectées interface réseau virtuel. Un scénario courant consiste à toohave des sous-réseaux différents pour la connectivité des serveurs frontale et principaux, ou un réseau dédié tooa analyse ou la solution de sauvegarde. Cet article décrit en détail comment toocreate une machine virtuelle qui possède plusieurs cartes réseau connectée tooit. Vous apprendrez également comment tooadd ou supprimer des cartes réseau à partir d’une machine virtuelle existante. Comme le nombre de cartes réseau prises en charge varie suivant la [taille des machines virtuelles](sizes.md) , pensez à dimensionner la vôtre en conséquence.

Pour plus d’informations, y compris toocreate plusieurs cartes réseau dans vos propres scripts PowerShell, voir [déploiement de machines virtuelles de plusieurs cartes](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="prerequisites"></a>Composants requis
Assurez-vous que vous avez hello [dernière version de Azure PowerShell installé et configuré](/powershell/azure/overview).

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.


## <a name="create-a-vm-with-multiple-nics"></a>Créer une machine virtuelle avec plusieurs cartes d’interface réseau
Créez d’abord un groupe de ressources. Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *EastUs* emplacement :

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a>Créer un réseau virtuel et des sous-réseaux
Un scénario courant consiste pour un réseau virtuel de toohave deux ou plusieurs sous-réseaux. Un sous-réseau est peut-être pour le trafic frontal, hello autre pour le trafic du serveur principal. tooconnect tooboth sous-réseaux, vous utilisez ensuite plusieurs cartes réseau sur votre machine virtuelle.

1. Définissez deux sous-réseaux de réseau virtuel avec la commande [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Hello exemple suivant définit les sous-réseaux hello pour *mySubnetFrontEnd* et *mySubnetBackEnd*:

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. Créez votre réseau virtuel et vos sous-réseaux avec la commande [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hello exemple suivant crée un réseau virtuel nommé *myVnet*:

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a>Créer plusieurs cartes réseau
Créez deux cartes d’interface réseau avec la commande [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Attacher un sous-réseau frontal toohello de la carte réseau et un sous-réseau de principaux de toohello de carte réseau. exemple Hello crée NIC nommé *myNic1* et *myNic2*:

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

En général, vous créez également un [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) ou [l’équilibrage de charge](../../load-balancer/load-balancer-overview.md) toohelp gérer et répartir le trafic entre vos machines virtuelles. Hello [plus d’ordinateurs virtuels de plusieurs cartes](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article explique comment créer un groupe de sécurité réseau et l’affectation des cartes réseau.

### <a name="create-hello-virtual-machine"></a>Créer la machine virtuelle de hello
Maintenant démarrer toobuild votre configuration d’ordinateur virtuel. Chaque taille de machine virtuelle a une limite pour le nombre total de hello de cartes réseau que vous pouvez ajouter tooa machine virtuelle. Pour plus d’informations, voir [Tailles des machines virtuelles Windows](sizes.md).

1. Définir votre toohello d’informations d’identification de machine virtuelle `$cred` variable comme suit :

    ```powershell
    $cred = Get-Credential
    ```

2. Définissez votre machine virtuelle avec la commande [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig). Hello exemple suivant définit un ordinateur virtuel nommé *myVM* et utilise une taille de machine virtuelle qui prend en charge plus de deux cartes réseau (*Standard_DS3_v2*) :

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. Créez reste hello de configuration de votre machine virtuelle avec [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) et [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage). Bonjour à l’exemple suivant crée un ordinateur Windows Server 2016 :

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. Attacher des cartes réseau hello deux que vous avez créé précédemment avec [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. Enfin, créez votre machine virtuelle avec la commande [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) :

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a>Ajouter un tooan de carte réseau existante de machine virtuelle
tooadd une carte réseau virtuelle tooan existant de machine virtuelle, vous libérer hello machine virtuelle, ajoutez hello carte réseau virtuelle, puis démarrer hello machine virtuelle.

1. Désallouer hello machine virtuelle avec [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). exemple Hello désalloue hello ordinateur virtuel nommé *myVM* dans *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Obtenir la configuration existante de hello Hello machine virtuelle avec [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Hello exemple suivant obtient les informations pour hello ordinateur virtuel nommé *myVM* dans *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Hello exemple suivant crée une carte réseau virtuelle avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) nommé *myNic3* qui est attaché trop*mySubnetBackEnd*. Hello carte réseau virtuelle est ensuite jointe toohello ordinateur virtuel nommé *myVM* dans *myResourceGroup* avec [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a>Cartes d’interface réseau virtuelles principales
    Une des cartes réseau sur une machine virtuelle multi-NIC de hello doit toobe principal. Si un des hello existant de cartes réseau virtuelles sur hello machine virtuelle est déjà défini comme principal, vous pouvez ignorer cette étape. Hello exemple suivant suppose que deux cartes réseau virtuelles est désormais présentes sur une machine virtuelle et que vous souhaitez tooadd hello la première carte réseau (`[0]`) en tant que hello principal :
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. Démarrer hello machine virtuelle avec [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a>Supprimer une carte réseau d’une machine virtuelle existante
tooremove une carte réseau virtuelle à partir d’un ordinateur virtuel existant, vous libérer hello machine virtuelle, supprimez hello carte réseau virtuelle, puis démarrer hello machine virtuelle.

1. Désallouer hello machine virtuelle avec [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). exemple Hello désalloue hello ordinateur virtuel nommé *myVM* dans *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Obtenir la configuration existante de hello Hello machine virtuelle avec [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Hello exemple suivant obtient les informations pour hello ordinateur virtuel nommé *myVM* dans *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Obtenir des informations sur hello NIC supprimer avec [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface). Hello exemple suivant obtient des informations sur *myNic3*:

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. Supprimer hello carte réseau avec [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) puis mettez à jour hello machine virtuelle avec [AzureRmVm de mise à jour](/powershell/module/azurerm.compute/update-azurermvm). Hello exemple suivant supprime *myNic3* tels qu’obtenus par `$nicId` Bonjour précédant l’étape :

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. Démarrer hello machine virtuelle avec [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a>Créer plusieurs cartes d’interface réseau avec des modèles
Les modèles de gestionnaire de ressources Azure fournissent un toocreate de façon plusieurs instances d’une ressource pendant le déploiement, telles que la création de plusieurs cartes réseau. Modèles du Gestionnaire de ressources utilisent toodefine de fichiers JSON déclarative de votre environnement. Pour plus d’informations, voir [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Vous pouvez utiliser *copie* nombre de hello toospecify de toocreate d’instances :

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

Pour plus d’informations, voir [Création de plusieurs instances à l’aide de la commande *copie*](../../resource-group-create-multiple.md). 

Vous pouvez également utiliser `copyIndex()` tooappend un nom de ressource tooa nombre. Vous pouvez ensuite créer les cartes *myNic1*, *MyNic2* et ainsi de suite. Hello de code suivant montre un exemple d’ajout de valeur d’index hello :

```json
"name": "[concat('myNic', copyIndex())]", 
```

Vous pouvez consulter un exemple complet de la [création de plusieurs cartes d’interface réseau à l’aide de modèles Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Étapes suivantes
Révision [tailles de machine virtuelle Windows](sizes.md) lorsque vous essayez de toocreate une machine virtuelle qui possède plusieurs cartes réseau. Payer une attention toohello nombre de cartes réseau prenant en charge la taille de chaque machine virtuelle. 


