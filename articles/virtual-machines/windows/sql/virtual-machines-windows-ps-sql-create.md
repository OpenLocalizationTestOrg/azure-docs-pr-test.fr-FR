---
title: aaaCreate une Machine virtuelle de SQL Server dans Azure PowerShell (Resource Manager) | Documents Microsoft
description: "Fournit une procédure et des scripts PowerShell pour la création d’une machine virtuelle Azure à l’aide des images de la galerie de machines virtuelles SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>Approvisionner une machine virtuelle SQL Server à l’aide d’Azure PowerShell (Resource Manager)
> [!div class="op_single_selector"]
> * [Portail](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment une seule machine virtuelle Azure à l’aide de toocreate hello **Azure Resource Manager** modèle de déploiement à l’aide des applets de commande PowerShell de Azure. Dans ce didacticiel, nous allons créer une seule machine virtuelle à l’aide d’un seul lecteur de disque à partir d’une image Bonjour SQL galerie. Nous allons créer de nouveaux fournisseurs de stockage de hello, réseau et les ressources de calcul qui seront utilisées par l’ordinateur virtuel de hello. Si vous avez déjà des fournisseurs pour ces ressources, vous pouvez les utiliser.

Si vous avez besoin de hello version classique de cette rubrique, consultez [configurer un ordinateur virtuel de SQL Server à l’aide de PowerShell Azure Classic](../classic/ps-sql-create.md).

## <a name="prerequisites"></a>Composants requis
Pour ce didacticiel, vous devez disposer des éléments suivants :

* Un compte Azure et un abonnement, avant de commencer. Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
* [Azure PowerShell](/powershell/azure/overview)1.4.0 ou version ultérieure (ce didacticiel a été écrit avec la version 1.5.0).
  * tooretrieve votre version, le type **Azure de Get-Module - ListAvailable**.

## <a name="configure-your-subscription"></a>Configurer votre abonnement
Ouvrez Windows PowerShell et établir un accès tooyour compte Azure en exécutant hello suivant l’applet de commande. S’affiche avec un signe dans l’écran tooenter vos informations d’identification. Utilisez hello même courrier électronique et le mot de passe que vous utilisez toosign dans toohello portail Azure.

    Add-AzureRmAccount

Une fois connecté avec succès, vous verrez des informations sur l’écran qui inclut l’ID d’abonnement hello avec lequel vous êtes dans. Il s’agit d’abonnement hello dans lequel les ressources hello pour ce didacticiel sont créées, sauf si vous modifiez tooa autre abonnement. Si vous avez plusieurs abonnement, exécutez hello suivant l’applet de commande tooreturn une liste de tous les de votre abonnement :

    Get-AzureRmSubscription

toochange tooanother ID d’abonnement, exécutez hello suivant l’applet de commande avec votre ID d’abonnement souhaité.

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>Définir des variables d’image
utilisation de toosimplify et la compréhension du script hello effectuée à partir de ce didacticiel, nous allons commencer en définissant un nombre de variables. Modifier les valeurs de paramètre de hello que vous convenance mais Méfiez-vous des caractères spéciaux et les longueurs de tooname connexes de restrictions d’affectation de noms lors de la modification des valeurs hello fournies.

### <a name="location-and-resource-group"></a>Emplacement et groupe de ressources
Utilisez les deux variables toodefine hello données hello et zone de groupe de ressources dans lequel vous allez créer vos autres ressources pour la machine virtuelle de hello hello.

Modifiez-le selon vos besoins, puis exécutez hello suivant d’applets de commande tooinitialize à ces variables.

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>Propriétés de stockage
Utilisez hello suivant variables toodefine hello compte et hello type de stockage de toobe de stockage utilisé par l’ordinateur virtuel de hello.

Modifiez-le selon vos besoins, puis exécutez hello suivant tooinitialize de l’applet de commande à ces variables. Notez que, dans cet exemple, nous utilisons [Premium Storage](../../../storage/common/storage-premium-storage.md), qui est recommandé pour les charges de travail de production. Pour plus d’informations et d’autres recommandations, consultez [Meilleures pratiques relatives aux performances de SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>Propriétés du réseau
Utilisez hello suivant l’interface de réseau variables toodefine hello, méthode d’allocation de TCP/IP hello, nom de réseau virtuel hello, nom de sous-réseau virtuel hello, hello plage d’adresses IP pour le réseau virtuel de hello, hello plage d’adresses IP pour le sous-réseau de hello et hello domaine public toobe d’étiquette nom utilisé par le réseau hello dans la machine virtuelle de hello.

Modifiez-le selon vos besoins, puis exécutez hello suivant tooinitialize de l’applet de commande à ces variables.

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>Propriétés de machine virtuelle
Utilisez hello suivant le nom d’ordinateur virtuel de variables toodefine hello, Nom_Ordinateur hello, taille de machine virtuelle hello et nom du disque de système d’exploitation pour la machine virtuelle de hello hello.

Modifiez-le selon vos besoins, puis exécutez hello suivant tooinitialize de l’applet de commande à ces variables.

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>Propriétés de l’image
Utilisez hello suivant variables toodefine hello image toouse pour la machine virtuelle de hello. Dans cet exemple, l’image de SQL Server 2016 Enterprise hello est utilisé.

Modifiez-le selon vos besoins, puis exécutez hello suivant tooinitialize de l’applet de commande à ces variables.

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

Notez que vous pouvez obtenir une liste complète des offres d’image de SQL Server avec la commande hello Get-AzureRmVMImageOffer :

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

Et vous pouvez voir hello références (SKU) disponible pour une offre avec la commande Get-AzureRmVMImageSku de hello. Hello commande suivante affiche toutes les références (SKU) disponible pour hello **SQL2014SP1-WS2012R2** offre.

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>Créer un groupe de ressources
Avec le modèle de déploiement du Gestionnaire de ressources hello, hello premier objet que vous créez est le groupe de ressources hello. Nous allons utiliser hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) toocreate de l’applet de commande un groupe de ressources Azure et ses ressources avec des ressources de hello groupe le nom et l’emplacement défini par des variables hello que vous avez déjà initialisé.

Exécutez hello suivant l’applet de commande toocreate votre nouveau groupe de ressources.

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>Créez un compte de stockage.
Hello virtual machine nécessite des ressources de stockage pour le disque du système d’exploitation hello et hello de données SQL Server et les fichiers journaux. Pour plus de simplicité, nous allons créer un seul disque pour les deux. Vous pouvez attacher des disques supplémentaires ultérieurement à l’aide de hello [disque Add-Azure](/powershell/module/azure/add-azuredisk) applet de commande de commande tooplace vos données SQL Server et les journaux sur des disques dédiés. Nous allons utiliser hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) toocreate de l’applet de commande un stockage standard de compte dans votre nouveau groupe de ressources et avec le nom de compte de stockage hello, nom de référence (SKU) de stockage et l’emplacement définis à l’aide de variables de hello que vous avez précédemment initialisé.

Exécutez hello suivant l’applet de commande toocreate votre nouveau compte de stockage.

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>Créer des ressources réseau
machine virtuelle de Hello nécessite un nombre de ressources réseau pour la connectivité réseau.

* Chaque machine virtuelle requiert un réseau virtuel.
* Un réseau virtuel doit avoir au moins un sous-réseau.
* Une interface réseau doit être définie avec une adresse IP privée ou publique.

### <a name="create-a-virtual-network-subnet-configuration"></a>Créer une configuration de sous-réseau de réseau virtuel
Nous allons commencer par créer une configuration de sous-réseau pour notre réseau virtuel. Pour notre didacticiel, nous allons créer un sous-réseau par défaut à l’aide de hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) applet de commande. Nous allons créer notre configuration de sous-réseau de réseau virtuel avec hello nom et adresse de préfixe du sous-réseau défini à l’aide de variables hello que vous avez déjà initialisé.

> [!NOTE]
> Vous pouvez définir des propriétés supplémentaires de la configuration de sous-réseau de réseau virtuel hello à l’aide de cette applet de commande, mais qui est abordée dans ce didacticiel hello.
>
>

Exécutez hello suivant toocreate de l’applet de commande de votre configuration de sous-réseau virtuel.

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>Créez un réseau virtuel
Ensuite, nous allons créer notre réseau virtuel à l’aide de hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) applet de commande. Nous allons créer notre réseau virtuel dans votre nouveau groupe de ressources, avec un préfixe d’adresse définie à l’aide de variables de hello précédemment initialisée et à l’aide de la configuration de sous-réseau hello que vous avez définie à l’étape précédente de hello, l’emplacement et nom de hello.

Exécutez hello suivant toocreate de l’applet de commande de votre réseau virtuel.

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a>Créer une adresse IP publique hello
Maintenant que nous avons notre réseau virtuel défini, nous devons tooconfigure une adresse IP pour la machine virtuelle de toohello connectivité. Pour ce didacticiel, nous allons créer une adresse IP publique à l’aide de la connectivité Internet de toosupport d’adressage IP dynamique. Nous allons utiliser hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) applet de commande toocreate hello adresse IP publique dans hello ressource groupe créé prevously et avec le nom de hello, l’emplacement, méthode d’allocation et étiquette de nom de domaine DNS défini à l’aide de hello variables que vous avez déjà initialisé.

> [!NOTE]
> Vous pouvez définir des propriétés supplémentaires de l’adresse IP publique hello à l’aide de cette applet de commande, mais qui est abordée dans ce didacticiel initial hello. Vous pouvez également créer une adresse privée ou une adresse avec une adresse statique, mais qui est également abordée dans ce didacticiel hello.
>
>

Exécutez hello suivant l’applet de commande toocreate votre adresse IP publique.

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a>Créer l’interface de réseau hello
Nous sommes maintenant interface réseau hello prêt toocreate notre ordinateur virtuel utilisera. Nous allons utiliser hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) toocreate de l’applet de commande notre interface réseau dans le groupe de ressources hello créé précédemment et avec le nom de hello, l’emplacement, sous-réseau et adresse IP publique définie précédemment.

Exécutez hello suivant l’applet de commande toocreate votre interface réseau.

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>Configurer un objet de machine virtuelle
Maintenant que nous avons des ressources réseau et de stockage définies, nous sommes les ressources de calcul toodefine prêt pour la machine virtuelle de hello. Pour notre didacticiel, nous sera spécifier la taille de machine virtuelle hello et diverses propriétés de système d’exploitation, spécifiez hello une interface réseau que vous avez créée précédemment, définir le stockage d’objets blob, puis spécifiez le disque du système d’exploitation hello.

### <a name="create-hello-vm-object"></a>Créer l’objet d’ordinateur virtuel hello
Nous allons commencer en spécifiant la taille de machine virtuelle hello. Dans ce didacticiel, nous spécifions une DS13. Nous allons utiliser hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) toocreate de l’applet de commande un objet configurables par l’ordinateur virtuel avec le nom de hello et la taille définie à l’aide de variables hello que vous avez déjà initialisé.

Exécutez hello suivant l’objet d’ordinateur virtuel d’applet de commande toocreate hello.

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a>Créer un nom de hello toohold l’objet d’informations d’identification et un mot de passe pour les informations d’identification d’administrateur local de hello
Nous pouvons définir les propriétés de système d’exploitation hello pour la machine virtuelle de hello, nous devons informations d’identification de toosupply hello pour le compte d’administrateur local hello sous forme de chaîne sécurisée. tooaccomplish, nous allons utiliser hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) applet de commande.

Exécutez hello suivant l’applet de commande et, dans la fenêtre de demande d’informations d’identification hello Windows PowerShell, tapez toouse de hello nom et mot de passe pour le compte d’administrateur local hello dans l’ordinateur virtuel Windows hello.

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a>Définir les propriétés de système d’exploitation hello pour la machine virtuelle de hello
Nous sommes maintenant les propriétés de système d’exploitation de l’ordinateur virtuel tooset prêt hello. Nous allons utiliser hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) type de hello tooset applet de commande du système d’exploitation Windows, nécessitent hello [agent de machine virtuelle](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installé, spécifiez cette applet de commande hello active automatiquement mettre à jour et définir le nom de machine virtuelle hello, Nom_Ordinateur hello et informations d’identification hello à l’aide de variables hello que vous avez déjà initialisé.

Exécutez hello suivant des propriétés de système d’exploitation tooset hello applet de commande pour votre machine virtuelle.

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a>Ajouter une machine virtuelle de hello réseau interface toohello
Ensuite, nous allons ajouter interface de réseau hello que nous avons créé précédemment toohello machine virtuelle. Nous allons utiliser hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) interface de réseau hello tooadd applet de commande à l’aide de la variable d’interface réseau hello que vous avez défini précédemment.

Exécutez hello suivant l’interface de réseau tooset hello applet de commande pour votre machine virtuelle.

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a>Définir l’emplacement de stockage d’objets blob hello pour hello toobe de disque utilisé par l’ordinateur virtuel de hello
Ensuite, nous allons définir emplacement de stockage d’objets blob hello pour hello toobe de disque utilisé par l’ordinateur virtuel de hello à l’aide de variables hello que vous avez défini précédemment.

Exécutez hello suivant l’emplacement de stockage des objets blob applet de commande tooset hello.

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a>Définir des propriétés du disque pour la machine virtuelle de hello de système d’exploitation de hello
Ensuite, nous allons définir système d’exploitation de hello propriétés du disque pour la machine virtuelle de hello. Nous allons utiliser hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify d’applet de commande qui hello du système d’exploitation pour la machine virtuelle de hello est issu d’une image, tooset tooread uniquement la mise en cache (étant donné que SQL Server est installé sur hello même disque) et définir nom d’ordinateur virtuel Hello et disque de système d’exploitation hello définis à l’aide de variables hello définie précédemment.

Exécutez hello suivant des propriétés de disque de système d’exploitation applet de commande tooset hello pour votre machine virtuelle.

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a>Spécifiez l’image de plateforme hello pour la machine virtuelle de hello
Notre dernière étape de configuration est l’image de plateforme toospecify hello pour notre machine virtuelle. Pour notre didacticiel, nous utilisons dernière image de SQL Server 2016 CTP hello. Nous allons utiliser hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) toouse de l’applet de commande cette image comme défini par les variables hello que vous avez défini précédemment.

Exécutez hello suivant l’image de plateforme toospecify hello applet de commande pour votre machine virtuelle.

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a>Créer hello SQL VM
Maintenant que vous avez terminé les étapes de configuration hello, vous êtes prêt toocreate hello virtual machine. Nous allons utiliser hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) applet de commande toocreate hello virtual machine à l’aide de variables hello que nous avons définie.

Exécutez hello suivant toocreate de l’applet de commande à votre machine virtuelle.

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

machine virtuelle de Hello est créé. Notez qu’un compte de stockage standard est créé pour les diagnostics de démarrage car hello spécifié de compte de stockage pour le disque de l’ordinateur virtuel de hello est un compte de stockage premium.

Vous pouvez maintenant afficher cet ordinateur dans hello Azure Portal toosee [son adresse IP publique et son nom de domaine complet](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="example-script"></a>Exemple de script
Hello script suivant contient complète du script PowerShell hello pour ce didacticiel. Il suppose que vous avez déjà le programme d’installation hello abonnement Azure toouse avec hello **Add-AzureRmAccount** et **sélectionnez-AzureRmSubscription** commandes.

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a>Étapes suivantes
Après la création de la machine virtuelle de hello, vous êtes prêt tooconnect toohello virtuels à l’aide de la connexion RDP et le programme d’installation. Pour plus d’informations, consultez [connecter tooa Machine virtuelle de SQL Server sur Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).

