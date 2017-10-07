---
title: aaaUse le stockage Azure Premium avec SQL Server | Documents Microsoft
description: "Cet article utilise les ressources créées avec le modèle de déploiement classique hello et fournit des conseils sur l’utilisation de stockage Azure Premium avec SQL Server s’exécutant sur des Machines virtuelles Azure."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a>Utilisation du stockage Premium Azure avec SQL Server sur des machines virtuelles
## <a name="overview"></a>Vue d'ensemble
[Stockage Azure Premium](../../../storage/common/storage-premium-storage.md) est hello nouvelle génération de stockage qui fournit une latence faible et haut débit d’e/s. Il est particulièrement adapté aux principales charges de travail E/S intensives telles que SQL Server sur [des machines virtuelles](https://azure.microsoft.com/services/virtual-machines/)IaaS.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Cet article fournit des conseils pour migrer un ordinateur virtuel en cours d’exécution SQL Server toouse stockage Premium et planification. Cela inclut l'infrastructure Azure (mise en réseau, stockage) et les étapes de la machine virtuelle Windows hôte. exemple Hello Bonjour [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) montre une migration de tooend complètes de fin de l’amélioration des toomove supérieure machines virtuelles tootake parti de local stockage SSD avec PowerShell.

Elle consiste toounderstand important hello bout en bout utilisant le stockage Azure Premium avec SQL Server sur des machines virtuelles IAAS. notamment :

* Identification des conditions préalables de hello toouse stockage Premium.
* Exemples de déploiement de SQL Server sur IaaS tooPremium stockage pour les nouveaux déploiements.
* Exemples de migration de déploiements existants, à la fois de serveurs autonomes et de déploiements à l’aide de groupes de disponibilité SQL Always On.
* Approches de migration possibles.
* Exemple de bout en bout complète les étapes de Azure, Windows et SQL Server pour la migration de hello d’une implémentation existante Always On.

Pour plus de détails sur l’utilisation de SQL Server dans les machines virtuelles Azure, consultez la rubrique [SQL Server dans les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

**Auteur :** Daniel Sol **Réviseurs techniques :** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.

## <a name="prerequisites-for-premium-storage"></a>Configuration requise pour le stockage Premium
Il existe plusieurs conditions préalables à l'utilisation du stockage Premium.

### <a name="machine-size"></a>Taille de la machine
Pour l’utilisation de stockage Premium, vous devrez toouse DS série Machines virtuelles (VM). Si vous n’avez pas utilisé les ordinateurs de la série DS dans votre service cloud avant, vous devez supprimer hello existante de machine virtuelle, conserver les disques hello attaché et ensuite créer un nouveau service cloud avant de recréer hello machine virtuelle en tant que DS * taille de rôle. Pour plus d’informations sur l’utilisation des tailles des machines virtuelles, consultez la rubrique [Tailles des machines virtuelles et des services cloud pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="cloud-services"></a>Services cloud
Vous pouvez uniquement utiliser des machines virtuelles DS* avec un stockage Premium si elles ont été créées dans un nouveau service cloud. Si vous utilisez SQL Server Always On dans Azure, hello toujours écouteur fait référence toohello Azure interne ou externe charge équilibrage de l’adresse IP qui est associé à un service cloud. Cet article se concentre sur la façon de toomigrate tout en conservant la disponibilité dans ce scénario.

> [!NOTE]
> Doit être une série DS * hello première machine virtuelle qui est déployé toohello nouveau Service Cloud.
>
>

### <a name="regional-vnets"></a>Réseaux virtuels régionaux
Pour les machines virtuelles DS * vous devez configurer hello réseau virtuel (VNET) qui héberge votre toobe de machines virtuelles régional. Cette hello « s’étend » le réseau virtuel est tooallow toobe de machines virtuelles plus grande hello configuré dans d’autres clusters et autoriser la communication entre eux. Bonjour suivant capture d’écran, hello emplacement en surbrillance montre les réseaux virtuels régionaux, tandis que le premier résultat de hello montre un réseau virtuel « étroit ».

![RegionalVNET][1]

Vous pouvez déclencher un tooa de toomigrate de ticket de support Microsoft réseau virtuel régional, Microsoft fera une modification, puis toocomplete hello migration tooregional réseaux virtuels, attribuez à la propriété de hello AffinityGroup dans la configuration de réseau hello. Tout d’abord exporter hello Configuration réseau dans PowerShell, puis remplacez hello **AffinityGroup** propriété Bonjour **VirtualNetworkSite** élément avec un **emplacement** propriété. Spécifiez `Location = XXXX` où `XXXX` est une région Azure. Importez ensuite la nouvelle configuration de hello.

Prenons l’exemple hello suivant la configuration du réseau virtuel :

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

toomove cette tooa réseau virtuel régional en Europe de l’ouest, modifiez hello toohello de configuration suivant :

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a>Comptes de stockage
Vous devez toocreate un compte de stockage qui est configuré pour le stockage Premium. Notez que l’utilisation hello du stockage Premium est définie à partir du compte de stockage hello, pas sur les disques durs virtuels individuels, toutefois, lors de l’utilisation d’une machine virtuelle DS * série vous pouvez attacher des disques durs virtuels à partir de comptes Premium et Standard de stockage. Vous pouvez envisager cette option si vous ne souhaitez pas tooplace hello disque dur virtuel du système d’exploitation sur toohello compte de stockage Premium.

suivant de Hello **New-AzureStorageAccountPowerShell** avec hello « Premium_LRS » **Type** crée un compte de stockage Premium :

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a>Paramètres de cache des disques durs virtuels
Hello principale différence entre la création de disques qui font partie d’un compte de stockage Premium est un paramètre de cache du disque hello. Pour les disques de volume de données SQL Server, il est recommandé d’utiliser le paramètre de cache de lecture**Read Caching**. Pour les volumes de journal de Transaction, le paramètre de cache de disque hello doit être défini trop '**aucun**'. Cela est différent des recommandations hello pour les comptes de stockage Standard.

Une fois que les disques durs virtuels hello ont été attachées, paramètre de cache hello ne peut pas être modifiée. Vous devez toodetach et rattachez hello disque dur virtuel avec un paramètre de cache mis à jour.

### <a name="windows-storage-spaces"></a>Espaces de stockage Windows
Vous pouvez utiliser [espaces de stockage Windows](https://technet.microsoft.com/library/hh831739.aspx) comme vous le faisiez avec le stockage Standard précédents, cela vous permettra de toomigrate une machine virtuelle qui utilise déjà des espaces de stockage. exemple Hello dans [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (étape 9 et suivantes) montre hello tooextract de code Powershell et importer une machine virtuelle avec plusieurs disques durs virtuels attachés.

Pools de stockage ont été utilisés avec un débit de tooenhance de compte de stockage Azure Standard et réduisent la latence. Vous trouverez peut-être utile de tester des pools de stockage avec un stockage Premium pour les nouveaux déploiements, mais notez que ces tests compliquent la configuration du stockage.

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a>Comment toofind les disques virtuels Azure mapper les pools de toostorage
Qu’il existe des recommandations de cache différent pour les disques durs virtuels attachés, vous pouvez décider toocopy hello disques durs virtuels tooa compte de stockage Premium. Toutefois, lorsque vous les rattachez toohello la série DS nouvelle machine virtuelle, vous devrez peut-être les paramètres de cache tooalter hello. Il est plus simple hello tooapply que stockage Premium recommandé de paramètres de cache lorsque vous avez des disques durs virtuels distincts pour hello de données SQL fichiers et journal des fichiers (plutôt qu’un disque dur virtuel unique qui contient à la fois).

> [!NOTE]
> Si vous avez des fichiers journaux et de données de SQL Server sur le même volume, hello mise en cache de l’option choisie dépend des modèles d’accès aux e/s hello pour vos charges de travail de base de données de hello. Seuls des tests permettent d'identifier l'option de mise en cache la mieux adaptée à ce scénario.
>
>

Toutefois, si vous utilisez des espaces de stockage Windows sont composés de plusieurs disques durs virtuels vous devez toolook à votre tooidentify des scripts d’origine qui joint des disques durs virtuels sont dans un pool spécifique qui, par conséquent, vous pouvez ensuite définir les paramètres de cache hello en conséquence pour chaque disque.

Si vous n’avez pas d’origine tooshow disponible de script vous qui mappent des disques durs virtuels toohello pool de stockage, vous pouvez utiliser hello suivant le mappage de pools de stockage sur disque/étapes toodetermine hello.

Pour chaque disque, utilisez hello comme suit :

1. Obtenez la liste des disques attachés tooVM avec hello **Get-AzureVM** commande :

    Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk
2. Notez hello Diskname et numéro d’unité logique.

    ![DisknameAndLUN][2]
3. Bureau à distance dans hello machine virtuelle. Passez trop**gestion de l’ordinateur** | **le Gestionnaire de périphériques** | **disques**. Examiner les propriétés hello de chacune des hello « Microsoft des disques virtuels »

    ![VirtualDiskProperties][3]
4. nombre LUN Hello ici est un nombre de numéro d’unité logique de toohello de référence que vous spécifiez lors de l’attachement hello VHD toohello machine virtuelle.
5. Pour hello 'Disque virtuel Microsoft' go toohello **détails** onglet, puis dans hello **propriété** liste, passez trop**clé pilote**. Bonjour **valeur**, hello de note **décalage**, qui est 0002 Bonjour suivant capture d’écran. Hello 0002 indique hello PhysicalDisk2 hello références de pool de stockage.

    ![VirtualDiskPropertyDetails][4]
6. Pour chaque pool de stockage, vidage out hello de disques associés :

    Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk

    ![GetStoragePool][5]

Vous pouvez maintenant utiliser cette tooassociate informations attaché disques tooPhysical de disques durs virtuels dans les Pools de stockage.

Une fois que vous avez mappé les disques tooPhysical de disques durs virtuels dans les Pools de stockage, vous pouvez détacher et copiez-les sur tooa compte de stockage Premium, puis de les joindre avec hello correct du paramètre de. Consultez l’exemple hello Bonjour [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), les étapes 8 à 12. Ces étapes indiquent comment tooextract un fichier VHD de machine virtuelle attachée disque configuration tooa CSV, copier les disques durs virtuels hello, modifier les paramètres de cache de configuration de disque hello et enfin redéployer hello machine virtuelle comme disque attaché d’une machine virtuelle de la série DS avec hello tous les.

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a>Bande passante de stockage de la machine virtuelle et débit de stockage du disque dur virtuel
Hello des performances de stockage dépend hello taille de VM DS * spécifié et hello des tailles de disque dur virtuel. machines virtuelles de Hello ont différentes allocations pour le nombre de hello de disques durs virtuels qui peuvent être attachés et hello ils prend en charge (Mo/s) de la bande passante maximale. Pour les nombres de la bande passante spécifique hello, consultez [Machine virtuelle et les tailles de Service Cloud pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Les disques de plus grande taille augmentent le nombre d'opérations d'E/S par seconde. Vous devez en tenir compte lorsque vous étudiez votre chemin de migration. Pour plus d’informations, [consultez la table de hello pour les e/s et les Types de disques](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).

Enfin, notez que les machines virtuelles prennent en charge différentes bandes passantes maximales pour tous les disques connectés. Sous une charge élevée, vous pourriez saturer hello maximale disque la bande passante disponible pour cette taille de rôle de machine virtuelle. Par exemple un Standard_DS14 prendra en charge des too512MB/s ; Par conséquent, avec trois disques P30 vous pourriez saturer la bande passante du disque de hello Hello machine virtuelle. Mais dans cet exemple, la limite de débit hello peut être dépassée en fonction de la combinaison de hello de lecture et d’écriture e/s.

## <a name="new-deployments"></a>Nouveaux déploiements
Hello deux sections suivantes montrent comment vous pouvez déployer des machines virtuelles SQL Server tooPremium stockage. Comme mentionné précédemment, vous ne devez pas nécessairement disque de système d’exploitation tooplace hello sur le stockage Premium. Vous pouvez choisir toodo cela si vous avez l’intention tooplace toutes les charges de travail intensives d’e/s sur le disque dur virtuel du système d’exploitation de hello.

Hello premier exemple illustre l’utilisation des Images de la galerie Azure existant. Hello deuxième exemple montre comment toouse une machine virtuelle personnalisée de l’image que vous disposez d’un compte de stockage Standard existant.

> [!NOTE]
> Ces exemples supposent que vous avez déjà créé un réseau virtuel régional.
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a>Création d'une nouvelle machine virtuelle avec un stockage Premium et une image de galerie
exemple Hello ci-dessous montre comment les tooplace hello du disque dur virtuel du système d’exploitation sur un stockage premium et attacher des disques durs virtuels de stockage Premium. Toutefois, vous pouvez également placer le disque du système d’exploitation hello dans un compte de stockage Standard et puis attachez les disques durs virtuels qui résident dans un compte de stockage Premium. Ces deux scénarios sont présentés.

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a>Étape 1 : création d'un compte de stockage Premium
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a>Étape 2 : création d'un nouveau service cloud
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a>Étape 3 : réservation d'une adresse IP virtuelle de service cloud (facultatif)
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a>Étape 4 : création d'un conteneur de machines virtuelles
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a>Étape 5 : placement du disque dur virtuel du système d'exploitation sur Standard ou Premium stockage
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a>Étape 6 : création d'une machine virtuelle
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a>Créer un nouveau toouse de machine virtuelle stockage Premium avec une image personnalisée
Ce scénario vous montre où sont placées les images personnalisées existantes qui résident sur un compte de stockage Standard. Comme mentionné si vous voulez tooplace hello disque dur virtuel du système d’exploitation sur stockage Premium vous devez toocopy hello image qui existe dans le compte de stockage Standard de hello et les transfèrent tooa stockage Premium avant de pouvoir être utilisé. Si vous disposez d’une image locale, vous pouvez également utiliser cette méthode toocopy directement toohello compte de stockage Premium.

#### <a name="step-1-create-storage-account"></a>Étape 1 : création d'un compte de stockage
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a>Étape 2 : création d'un service cloud
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a>Étape 3 : utilisation d’une image existante
Vous pouvez utiliser une image existante. Vous pouvez [prendre l’image d’une machine existante](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Machine de hello Remarque vous de l’image n’a pas de toobe DS * machine. Une fois que vous avez hello image, hello suivant les étapes indiquent comment toocopy il toohello compte de stockage Premium avec hello **AzureStorageBlobCopy de début** applet de commande PowerShell.

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a>Étape 4: copie d'objets Blob entre des comptes de stockage
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a>Étape 5 : vérification régulière de l'état de la copie :
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a>Étape 6 : Ajouter l’Image tooAzure sur le disque référentiel dans l’abonnement
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> Vous constaterez peut-être que même si les rapports d’état sur hello comme une réussite, vous pouvez toujours obtenir une erreur de bail de disque. Dans ce cas, attendez 10 minutes environ.
>
>

#### <a name="step-7--build-hello-vm"></a>Étape 7 : Créer hello machine virtuelle
Vous créez ici hello machine virtuelle à partir de votre image et l’attachement de deux disques durs virtuels de stockage Premium :

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a>Déploiements existants qui n’utilisent pas les groupes de disponibilité Always On
> [!NOTE]
> Pour les déploiements existants, tout d’abord voir hello [conditions préalables](#prerequisites-for-premium-storage) section de cette rubrique.
>
>

Il existe différents points à prendre en compte concernant les déploiements SQL Server qui utilisent ou non des groupes de disponibilité Always On. Si vous n’utilisez pas Always On et que vous disposez d’un autonome existante de SQL Server, vous pouvez mettre à niveau tooPremium stockage à l’aide d’un nouveau compte service et le stockage cloud. Tenez compte des hello options suivantes :

* **Créez une nouvelle machine virtuelle SQL Server**. Vous pouvez créer une nouvelle machine virtuelle SQL qui utilise un compte de stockage Premium comme décrit dans les nouveaux déploiements. Ensuite, sauvegardez et restaurez votre configuration SQL Server et vos bases de données utilisateur. Hello application aura besoin des mises à jour de toobe tooreference hello nouveau SQL Server si elle est accessible en interne ou externe. Vous devez toocopy tous les objets « hors db' comme si vous effectuiez une migration de (SxS) SQL Server côte à côte. Cela inclut des objets tels que les connexions, les certificats et les serveurs liés.
* **Migrez une machine virtuelle SQL Server existante**. Vous devrez déconnecter hello machine virtuelle SQL Server, puis transférer tooa nouveau service cloud, qui inclut la copie de tous ses toohello de disques durs virtuels attaché compte de stockage Premium. Lors du hello machine virtuelle est en ligne, application hello fait référence le nom d’hôte serveur hello comme avant. N’oubliez pas que la taille hello du disque existant de hello affectera des caractéristiques de performances hello. Par exemple, un disque de 400 Go obtient arrondi par excès tooa P20. Si vous savez que vous ne requièrent pas les performances du disque, vous pourriez recréer hello machine virtuelle comme une machine virtuelle de série DS et attacher des disques durs virtuels de stockage Premium de spécification de taille et de performances hello que vous avez besoin. Ensuite, vous pouvez détacher et rattacher les fichiers de base de données SQL hello.

> [!NOTE]
> Lors de la copie de disques de disque dur virtuel hello vous devez être conscient de la taille de hello, selon la taille de hello signifie le type de disque de stockage Premium peuvent être regroupées en, cela détermine la spécification de performances de disque. Taille de Azure arrondit les toohello le plus proche du disque, donc si vous avez un disque Go 400, cela sera arrondie tooa P20. Selon vos exigences d’e/s existants de hello disque dur virtuel du système d’exploitation, vous ne devrez pas peut-être toomigrate cette tooa compte de stockage Premium.
>
>

Si votre serveur SQL Server est accessible en externe, adresse IP virtuelle de service de cloud hello changera. Vous devez également les points de terminaison tooupdate, ACL et DNS paramètres.

## <a name="existing-deployments-that-use-always-on-availability-groups"></a>Déploiements existants qui utilisent les groupes de disponibilité Always On
> [!NOTE]
> Pour les déploiements existants, tout d’abord voir hello [conditions préalables](#prerequisites-for-premium-storage) section de cette rubrique.
>
>

Dans cette section, nous examinons la façon dont le groupe de disponibilité Always On interagit avec la mise en réseau Azure. Nous sera puis décomposer les migrations dans les scénarios de tootwo : les migrations où aucun temps d’arrêt peut être tolérée et les migrations où vous devez obtenir un temps mort minimal.

Les groupes locaux de disponibilité Always On SQL Server utilisent un écouteur local qui inscrit un nom DNS virtuel ainsi qu’une adresse IP partagée entre un ou plusieurs serveurs SQL. Lorsque les clients se connectent, ils sont routées via hello écouteur IP toohello principal SQL Server. Il s’agit de serveur hello propriétaire hello ressource toujours sur IP à ce moment-là.

![DeploymentsUseAlways On][6]

Dans Microsoft Azure vous pouvez avoir qu’un seul IP adresse affectée tooa NIC sur hello machine virtuelle, dans commande tooachieve hello même couche d’abstraction comme local, Azure utilise l’adresse IP hello affectée équilibreurs de charge interne/externe toohello (équilibrage de charge interne/ELB). la ressource IP Hello qui est partagée entre les serveurs de hello est définie toohello même adresse IP en tant que hello/ELB de l’équilibrage de charge interne. Il est publié dans hello DNS, et le trafic du client est passé au réplica de serveur SQL principal toohello hello/ELB de l’équilibrage de charge interne. Hello équilibrage de charge interne/ELB sait quel serveur SQL principal, car elle utilise des ressources de sondes tooprobe hello toujours sur IP. Dans l’exemple précédent de hello, il teste chaque nœud qui possède un point de terminaison référencé par hello ELB/équilibrage de charge interne, selon celle qui répond est hello principal SQL Server.

> [!NOTE]
> Hello équilibrage de charge interne et ELB sont tous deux affectés service de cloud computing Azure particulier tooa, par conséquent, toute migration cloud dans Azure signifie probablement que hello que change IP d’équilibrage de charge.
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a>Migration de déploiements Always On autorisant des temps d’arrêt
Il existe deux stratégies toomigrate toujours sur les déploiements qui permet des temps morts :

1. **Ajouter plusieurs réplicas secondaires tooan existant toujours sur le Cluster**
2. **Migrer tooa nouveau toujours sur Cluster**

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a>1. Ajouter plusieurs réplicas secondaires tooan toujours sur Cluster existant
Une stratégie est tooadd plusieurs bases de données secondaires toohello toujours sur le groupe de disponibilité. Vous devez tooadd ces éléments dans un nouveau service cloud et mettre à jour d’écouteur de hello avec hello équilibreur de charge nouvelle adresse IP.

##### <a name="points-of-downtime"></a>Points d’arrêt :
* Validation de cluster.
* Test des basculements Always On de nouveaux réplicas secondaires.

Si vous utilisez des Pools de stockage Windows dans hello VM pour augmenter le débit d’e/s, celles-ci sont effectuées en mode hors connexion pendant une Validation de Cluster complète. test de validation Hello est requis lorsque vous ajoutez le cluster toohello de nœuds. Hello temps test de hello toorun peut varier, donc vous devez tester cela dans votre tooget d’environnement de test représentatif une durée approximative de la durée de cette opération.

Vous devez configurer le moment où vous pouvez effectuer un basculement manuel et chaos test sur hello qui vient d’être ajouté des fonctions de haute disponibilité Always On tooensure nœuds comme prévu.

![DeploymentUseAlways On2][7]

> [!NOTE]
> Vous devez arrêter toutes les instances de SQL Server où les Pools de stockage hello sont utilisées avant hello la Validation s’exécute.
>
> ##### <a name="high-level-steps"></a>Procédure générale
>

1. Créez deux serveurs SQL dans le nouveau service cloud avec une connexion au stockage Premium.
2. Copiez les sauvegardes complètes et effectuez une restauration avec **NORECOVERY**.
3. Copiez les objets dépendants 'out of user DB', notamment que les connexions.
4. Créez un nouvel équilibreur de charge interne (ILB) ou utilisez un équilibreur de charge externe (ELB), puis configurez ensuite les points de terminaison d'équilibrage de charge sur les deux nouveaux nœuds.

   > [!NOTE]
   > Vérifiez que tous les nœuds ont la configuration de point de terminaison hello correcte avant de continuer
   >
   >
5. Arrêter toohello d’accès de l’Application d’utilisateur SQL Server (si vous utilisez des Pools de stockage).
6. Arrêtez les services du moteur SQL Server sur tous les nœuds (si vous utilisez des pools de stockage).
7. Ajouter de nouveaux nœuds toocluster et exécuter la validation complète.
8. Une fois la validation réussie, démarrez tous les services SQL Server.
9. Sauvegardez les journaux des transactions et restaurez les bases de données utilisateur.
10. Ajouter de nouveaux nœuds dans le groupe de disponibilité AlwaysOn de hello et de le placer dans la réplication **synchrone**.
11. Ajouter hello IP ressource d’adresse de hello nouveau Cloud Service équilibrage de charge interne ELB via PowerShell pour Always On sur la base hello multisite exemple Bonjour [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage). Dans le clustering Windows, définissez hello **propriétaires possibles** Hello **adresse IP** ressource toohello nouveaux nœuds ancien. Consultez hello 'Ajout de ressource d’adresse IP sur le même sous-réseau' section Hello [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
12. Tooone de basculement de nouveaux nœuds de hello.
13. Rendre des partenaires de basculement automatique de nouveaux nœuds hello et les tests de basculement.
14. Supprimez les nœuds d'origine du groupe de disponibilité.

##### <a name="advantages"></a>Avantages
* Nouveaux serveurs SQL peut être testé (SQL Server et Application) avant d’être ajoutés sur tooAlways.
* Vous pouvez modifier la taille de machine virtuelle hello et personnaliser des spécifications exactes de hello stockage tooyour. Toutefois, il serait utile tookeep tous les chemins de fichier SQL hello hello identiques.
* Vous pouvez contrôler le démarrage de transfert hello de toohello de sauvegardes de base de données hello réplicas secondaires. Cela diffère de l’utilisation d’Azure **Start-AzureStorageBlobCopy** toocopy de l’applet de commande disques durs virtuels, car il s’agit d’une copie asynchrone.

##### <a name="disadvantages"></a>Inconvénients
* Lorsque vous utilisez des Pools de stockage Azure, est interruptions de service de Cluster pendant hello complète la Validation du Cluster pour les nœuds supplémentaires nouvelle hello.
* Selon hello Version de SQL Server et le nombre d’existant hello des réplicas secondaires, vous ne pouvez pas être en mesure de tooadd plusieurs réplicas secondaires sans supprimer les bases de données secondaires existantes.
* Il peut être long temps de transfert de données SQL lors de la configuration des bases de données secondaires hello.
* Pendant la migration, l’exécution de nouvelles machines en parallèle entraîne un coût supplémentaire.

#### <a name="2-migrate-tooa-new-always-on-cluster"></a>2. Migrer tooa nouveau toujours sur Cluster
Une autre stratégie est toocreate un tout nouveau toujours sur Cluster avec tout nouveau nœuds dans le nouveau service cloud, puis redirection hello clients toouse il.

##### <a name="points-of-downtime"></a>Points d’arrêt
Il est temps d’arrêt lorsque vous transférez des applications et les utilisateurs toohello nouveau toujours l’écouteur de. temps d’arrêt Hello dépend :

* Hello durée toorestore transaction finale journal sauvegardes toodatabases sur de nouveaux serveurs.
* Hello durée tooupdate applications toouse nouveau Always On écouteur client.

##### <a name="advantages"></a>Avantages
* Vous pouvez tester hello véritable environnement de production, SQL Server, et les modifications de génération du système d’exploitation.
* Vous avez hello option toocustomize hello stockage et toopotentially réduire la taille de machine virtuelle. Cela pourrait entraîner une réduction des coûts.
* Vous pouvez mettre à jour votre build ou version SQL Server pendant ce processus. Vous pouvez également mettre à niveau hello système d’exploitation.
* Hello que précédente toujours sur Cluster peut agir comme une cible de restauration solide.

##### <a name="disadvantages"></a>Inconvénients
* Vous devez le nom DNS toochange hello d’écouteur de hello si vous souhaitez que les deux clusters toujours en cours d’exécution simultanément. Cette opération ajoute administration surcharge lors de la migration de hello comme chaînes d’application cliente doivent refléter le nouveau nom de port d’écoute hello.
* Vous devez implémenter un mécanisme de synchronisation entre deux tookeep environnements hello, en tant que fermer toominimize possible hello synchronisation finale à la configuration requise avant la migration.
* Est ajoutée coût pendant la migration pendant que vous avez hello nouvel environnement en cours d’exécution.

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a>Migration de déploiements Always On avec un temps d’arrêt minimal
Il existe deux stratégies pour effectuer la migration de déploiements Always On avec un temps d’arrêt minimal :

1. **Utiliser un service secondaire existant : site unique**
2. **Utiliser des réplicas secondaires existants : multi-sites**

#### <a name="1-utilize-an-existing-secondary-single-site"></a>1. Utilisation d’un service secondaire existant : site unique
Une stratégie pour un temps mort minimal est tootake un cloud existant secondaire et le supprimer du service de cloud actuelle hello. Puis copiez hello toohello de disques durs virtuels de nouveau compte de stockage Premium et créer hello machine virtuelle dans le nouveau service de cloud hello. Puis mettez à jour un écouteur de hello dans la gestion de clusters et le basculement.

##### <a name="points-of-downtime"></a>Points d’arrêt
* Il est temps d’arrêt lorsque vous mettez à jour le nœud final de hello avec point de terminaison à charge équilibrée hello.
* La reconnexion de votre client peut être retardée en fonction de votre configuration client/DNS.
* Il est temps d’arrêt supplémentaires si vous choisissez tootake hello toujours sur le Cluster groupe hors connexion tooswap les adresses IP de hello. Vous pouvez éviter cela à l’aide de la dépendance OR et propriétaires possibles pour hello ajouté la ressource d’adresse IP. Consultez hello 'Ajout de ressource d’adresse IP sur le même sous-réseau' section Hello [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).

> [!NOTE]
> Lorsque vous souhaitez hello toopartake nœud ajouté dans en tant qu’un toujours sur partenaire de basculement, vous devez tooadd un point de terminaison Azure avec un toohello de référence de charge équilibrée définie. Lorsque vous exécutez hello **Add-AzureEndpoint** commande toodo, tooremain de connexions en cours ouvert, mais le nouvel écouteur de toohello de connexions ne seront pas en mesure de toobe établie jusqu'à ce que l’équilibrage de charge hello a mis à jour. Dans le test, il s’agissait toolast vu 90-120 secondes, cela doit être testé.
>
>

##### <a name="advantages"></a>Avantages
* Aucun coût supplémentaire pendant la migration.
* Une migration un à un.
* Moins de complexité.
* Permet d'augmenter le nombre d'opérations d'E/S à partir des SKU de stockage Premium. Lors de la partie d’un 3e hello disques sont détachés hello VM et copiés toohello de nouveau service cloud, outil peut être de taille de disque dur virtuel hello tooincrease utilisé, qui fournit des débits plus importants. Pour augmenter la taille du disque dur virtuel, consultez ce [forum de discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).

##### <a name="disadvantages"></a>Inconvénients
* Il existe une perte temporaire de haute disponibilité et de récupération d'urgence pendant la migration.
* Comme il s’agit d’une migration 1:1, vous devez toouse une taille minimale de machine virtuelle qui prend en charge le nombre de disques durs virtuels, donc vous n’êtes peut-être pas en mesure de toodownsize vos machines virtuelles.
* Ce scénario utiliseriez hello Azure **AzureStorageBlobCopy de début** applet de commande, qui est asynchrone. Il n'existe aucun contrat SLA à la fin de la copie. le délai de Hello de copies de hello varie, cela dépend de l’attente dans la file d’attente qu'il dépend également du montant hello de tootransfer de données. heure Hello augmente si le transfert de hello est en train de centre de données Azure tooanother qui prend en charge le stockage Premium dans une autre région. Si vous avez seulement 2 nœuds, envisagez une atténuation possibles en cas de copie de hello dure plus longtemps que dans le test. Cela peut inclure hello suivant des idées.
  * Ajouter un nœud SQL Server 3e temporaire pour la haute disponibilité avant la migration hello avec un temps mort convenu.
  * Exécutez la migration hello en dehors d’Azure maintenance planifiée.
  * Vérifiez que vous avez correctement configuré votre quorum de cluster.  

##### <a name="high-level-steps"></a>Procédure générale
Ce document ne présente pas d’un exemple de tooend fin terminée, cependant hello [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) fournit des détails qui peuvent être optimisée tooperform cela.

![MinimalDowntime][8]

* Collecte la configuration de disque et supprimer un nœud hello (ne pas supprimer les disques durs virtuels attachés).
* Créez un compte de stockage Premium et copier les disques durs virtuels à partir de hello compte de stockage Standard
* Création du service cloud et redéployer hello SQL2 VM dans ce service cloud. Créer hello machine virtuelle à l’aide de hello copié de disque dur virtuel de système d’exploitation d’origine et attachement hello copiés les disques durs virtuels.
* Configurez l'ILB/ELB et ajoutez des points de terminaison.
* Mettez à jour l'écouteur en procédant comme suit :
  * Prendre hello groupe Always On en mode hors connexion et de mise à jour hello toujours l’écouteur d’avec équilibrage de charge interne nouveau / adresse IP de ELB.
  * Ou l’ajout de ressource d’adresse hello IP de nouveau Cloud Service équilibrage de charge interne/ELB via PowerShell dans le clustering Windows. Puis ensemble hello des propriétaires possibles de toohello de ressource d’adresse IP hello migrés de nœud, SQL2 et que la dépendance OR Bonjour nom réseau. Consultez hello 'Ajout de ressource d’adresse IP sur le même sous-réseau' section Hello [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
* Vérifiez les clients toohello de configuration/propagation DNS.
* Migrez la machine virtuelle SQL1 et suivez les étapes 2 à 4.
* Si des étapes 5ii, puis ajouter SQL1 comme propriétaire Possible pour hello ajouté la ressource d’adresse IP
* Testez les basculements.

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a>2. Utilisation de réplicas secondaires existants : multi-sites
Si vous avez des nœuds dans plusieurs centres de données Azure (DC) ou si vous avez un environnement hybride, vous pouvez utiliser une configuration Always On ce temps d’arrêt toominimize environnement.

approche de Hello est toochange hello Always On synchronisation tooSynchronous hello localement ou contrôleur de domaine Azure secondaire, puis basculement sur toothat SQL Server. Puis copier les disques durs virtuels de hello tooa compte de stockage Premium et redéployer la machine de hello dans un nouveau service cloud. Mettre à jour le port d’écoute hello et restaurez.

##### <a name="points-of-downtime"></a>Points d’arrêt
temps d’arrêt Hello se compose de hello temps toofailover toohello autre contrôleur de domaine et un précédent. Il dépend de votre configuration client/DNS et la reconnexion du client peut être retardée.
Tenez compte des hello, exemple d’une configuration Always On hybride suivant :

![MultiSite1][9]

##### <a name="advantages"></a>Avantages
* Vous pouvez utiliser l'infrastructure existante.
* Vous avez tout d’abord hello de mise à niveau toopre option hello stockage Azure sur hello contrôleur de domaine de récupération d’urgence Azure.
* Hello stockage de récupération d’urgence Azure le contrôleur de domaine peut être reconfiguré.
* Il existe un minimum de deux basculements pendant la migration, à l'exclusion des basculements de test.
* Vous ne devez toomove des données de SQL Server avec une sauvegarde et restauration.

##### <a name="disadvantages"></a>Inconvénients
* En fonction de tooSQL d’accès client serveur, il peut y avoir une latence accrue lorsque SQL Server est en cours d’exécution dans une autre application de toohello de contrôleur de domaine.
* heure de disques durs virtuels tooPremium stockage Hello risque de durer longtemps. Cela peut affecter votre décision sur si tookeep hello nœud Bonjour groupe de disponibilité. Là lorsque le travail nécessitant de journal charges sont en cours d’exécution pendant la migration de hello est requis, étant donné que nœud principal de hello portera tookeep hello des transactions non répliquées dans son journal des transactions. Par conséquent, cela peut augmenter considérablement.
* Ce scénario utiliseriez hello Azure **AzureStorageBlobCopy de début** applet de commande, qui est asynchrone. Il n'existe aucun contrat SLA à la fin. Hello le délai de copies de hello varie, cela dépend de l’attente dans la file d’attente, elle dépend également du montant hello de tootransfer de données. Par conséquent, vous avez uniquement un seul nœud dans votre centre de données 2, vous devez prendre des mesures d’atténuation en cas de copie de hello dure plus longtemps que dans le test. Cela peut inclure hello suivant des idées.
  * Ajouter un nœud SQL 2e temporaire pour la haute disponibilité avant la migration hello avec un temps mort convenu.
  * Exécutez la migration hello en dehors d’Azure maintenance planifiée.
  * Vérifiez que vous avez correctement configuré votre quorum de cluster.

Ce scénario suppose que vous avez documenté votre installation et savez comment le stockage de hello est mappé dans classer les modifications toomake pour les paramètres du cache disque optimales.

##### <a name="high-level-steps"></a>Procédure générale
![Multisite2][10]

* Rendre hello local / remplacement hello Azure le contrôleur de domaine principal de SQL Server et les rendre hello autres partenaires de basculement automatique (AFP).
* Recueillir des informations de configuration de disque de SQL2 et supprimer un nœud hello (ne pas supprimer les disques durs virtuels attachés).
* Créez un compte de stockage Premium et copier les disques durs virtuels à partir de hello compte de stockage Standard.
* Créez un nouveau service cloud et hello SQL2 VM avec ses disques primes stockage attachés.
* Configurez l'ILB/ELB et ajoutez des points de terminaison.
* Hello de mise à jour toujours l’écouteur d’avec équilibrage de charge interne nouveau / ELB IP adresse et testez le basculement.
* Vérifiez la configuration de DNS hello.
* Hello AFP tooSQL2, puis migrer SQL1 et parcourez les étapes 2 à 5.
* Testez les basculements.
* Commutateur tooSQL1 arrière de hello AFP et SQL2

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a>Annexe : Migration d’un stockage de tooPremium toujours sur Cluster Multisite
reste Hello de cette rubrique fournit un exemple détaillé de la conversion d’un stockage de plusieurs site Always On cluster tooPremium. Il convertit également hello écouteur à l’aide d’un équilibreur de charge interne de tooan équilibrage de charge externe (équilibrage de charge interne).

### <a name="environment"></a>Environnement
* Windows 2k12 / SQL 2k12
* 1 base de données de fichiers sur SP
* 2 x pools de stockage par nœud

![Appendix1][11]

### <a name="vm"></a>MV :
Dans cet exemple, nous allons toodemonstrate déplacement à partir d’un tooILB ELB. ELB était disponible avant l’équilibrage de charge interne, cet exemple montre comment toothis tooswitch pendant hello migration.

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a>Étapes de Pre : Se connecter tooSubscription
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a>Étape 1: créer les nouveaux compte de stockage et service cloud
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a>Étape 2 : Hello d’augmentation autorisée des défaillances sur les ressources<Optional>
Sur certaines ressources qui appartiennent tooyour toujours sur le groupe de disponibilité sont les limites de nombre d’échecs qui peut se produire pendant une période où le service de cluster hello va tenter de groupe de ressources toorestart hello. Il est recommandé de qu'augmenter ce tandis que vous parcourez cette procédure, étant donné que si vous n’avez pas manuellement les basculements de basculement et de déclencheur en arrêtant ordinateurs, vous peuvent obtenir toothis fermer limite.

Il serait être prudent toodouble l’allocation échec hello, toodo ce gestionnaire du Cluster de basculement, consultez des propriétés toohello hello Always On du groupe de ressources :

![Appendix3][13]

Modifier hello too6 du nombre maximal de pannes.

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a>Étape 3 : ajouter une ressource d’adresse IP au groupe de clusters <Optional>
Si vous avez une seule adresse IP pour hello groupe du Cluster et il est aligné toohello cloud sous-réseau, soyez attentif aux, si vous accidentellement Mettez hors connexion tous les nœuds de cluster dans le cloud de hello que réseau puis de ressource d’adresse IP du Cluster hello et de nom réseau du Cluster seront pas en mesure de toocome en ligne. Bonjour événements de ce qu’il empêchera met à jour les ressources de cluster tooother.

#### <a name="step-4-dns-configuration"></a>Étape 4 : configuration DNS
une transition en douceur dépend de la manière dont DNS est en cours de tooimplement utilisés et mis à jour.
Always On est installé, il crée un groupe de ressources de Cluster Windows, si vous ouvrez le Gestionnaire du Cluster de basculement, vous verrez qu’au minimum, il aura trois ressources, hello deux hello document fait référence à tooare :

* Nom de réseau virtuel (VNN) – il s’agit hello DNS nom de ce client se connecter toowhen souhaitant tooconnect tooSQL serveurs via Always On.
* Ressource d’adresse IP : il s’agit de hello d’adresses IP associées aux hello VNN, vous pouvez avoir plusieurs, et dans une configuration multisite, vous aurez une adresse IP par sous-réseau/site.

Lors de la connexion tooSQL Server, le pilote de SQL Server Client hello récupère les enregistrements DNS de hello associés au port d’écoute hello et essayez tooconnect tooeach Always On associées adresse IP, ci-dessous, nous aborderons certains facteurs pouvant influencer cela.

Hello nombre d’enregistrements DNS simultanées qui sont associés au nom de l’écouteur hello dépend non seulement de nombre hello d’adresses IP, mais hello ' RegisterAllIpProviders'setting dans le Clustering de basculement pour hello les ressources Always ON VNN.

Lorsque vous déployez Always On dans Azure il y a des étapes différentes toocreate hello écouteur et les adresses IP, toomanually configurer hello 'RegisterAllIpProviders' too1, cela est tooan autre déploiement Always On local où il est déjà défini too1.

Si 'RegisterAllIpProviders' est 0, puis vous verrez seulement un enregistrement DNS dans DNS associé hello écouteur :

![Appendix4][14]

Si 'RegisterAllIpProviders' est 1 :

![Appendix5][15]

code Hello ci-dessous vider les paramètres VNN hello et définissez-le pour vous, veuillez Remarque, Pourquoi modifier tootake effet, vous devez tootake hello VNN hors connexion et activez de nouveau en ligne, cette prise hello hors connexion à l’origine interruptions de connectivité client écouteur.

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

Dans une étape ultérieure de la migration, vous devez tooupdate hello Always On écouteur avec l’adresse IP mise à jour qui fera référence à un équilibrage de charge, cela implique une suppression de ressource d’adresse IP et l’addition. Après la mise à jour de hello IP, vous devez tooensure hello nouvelle adresse IP a été mis à jour dans la Zone DNS et que les clients de hello sont à jour son cache DNS local.

Si vos clients se trouvent dans un segment de réseau et faire référence à un autre serveur DNS, vous devez tooconsider que se passe-t-il sur le transfert de Zone DNS pendant la migration de hello, reconnecter hello application heure sera contraint au moins hello temps de transfert de Zone de toutes les nouvelles adresses IP pour le port d’écoute hello. Si vous êtes sous contrainte de temps ici, vous devez discuter test forcer un transfert de zone incrémentiel avec vos équipes de Windows, et également placer hello DNS tooa enregistrement d’hôte inférieur durée tooLive (TTL), afin de mettre à jour des clients de hello. Pour plus d’informations, consultez [Transferts de zone incrémentiels](https://technet.microsoft.com/library/cc958973.aspx) et [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).

Est de 1200 secondes par hello de valeur par défaut durée de vie pour l’enregistrement DNS associé hello écouteur dans Always On dans Azure. Vous souhaiterez peut-être tooreduce cela si vous êtes sous contrainte de temps pendant votre migration tooensure hello clients mise à jour leurs DNS avec adresse IP hello mis à jour une adresse pour l’écouteur de hello. Vous pouvez consulter et modifier la configuration de hello en vidant configuration hello Hello VNN :

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

Notez hello inférieur de hello 'HostRecordTTL', un montant supérieur du trafic DNS se produit.

##### <a name="client-application-settings"></a>Paramètres de l’application cliente
Si votre application prend en charge SQL client hello .net 4.5 SQLClient, puis vous pouvez utiliser « MULTISUBNETFAILOVER = TRUE' (mot clé), cette opération est recommandée toobe appliquée car elle permet au cours du basculement plus rapide connexion tooSQL toujours sur le groupe de disponibilité. Il énumère toutes les adresses IP associés hello toujours sur l’écouteur en parallèle et effectue une vitesse de nouvelle tentative de connexion TCP plus agressive lors d’un basculement.

Pour plus d’informations sur les paramètres de hello ci-dessus, consultez [mot clé MultiSubnetFailover et fonctionnalités associées aux](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover). Consultez également [Prise en charge SqlClient pour la haute disponibilité et récupération d’urgence](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).

#### <a name="step-5-cluster-quorum-settings"></a>Étape 5 : paramètres de quorum de cluster
Comme vous vous apprêtez toobe prendre au moins un serveur SQL vers le bas à la fois, vous devez modifier la configuration de quorum du cluster hello, si avec fichier partage témoin de 2 nœuds, vous devez définir tooallow nœud majoritaire hello quorum et utiliser le vote dynamique, il s’agit de tooallow pour un permanent de tooremain nœud unique.

    Set-ClusterQuorum -NodeMajority  

Pour plus d’informations sur la gestion et la configuration de quorum du cluster hello, consultez [configurer et gérer le Quorum dans un Cluster de basculement Windows Server 2012 de hello](https://technet.microsoft.com/library/jj612870.aspx).

#### <a name="step-6-extract-existing-endpoints-and-acls"></a>Étape 6 : extraction des points de terminaison et des ACL existants
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

Enregistrer ces fichiers de texte tooa.

#### <a name="step-7-change-failover-partners-and-replication-modes"></a>Étape 7 : modification les partenaires de basculement et des modes de réplication
Si vous avez plus de 2 serveurs SQL Server, vous devez modifier hello de basculement d’une autre base de données secondaire dans un autre contrôleur de domaine ou local 'too'Synchronous et que vous un partenaire de basculement automatique (AFP), il s’agit donc mettre à jour de la haute disponibilité tandis que vous apportez des modifications. Vous pouvez le faire via TSQL ou via SSMS :

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a>Étape 8 : Suppression de la machine virtuelle secondaire du service cloud
Vous devez planifier toomigrate un nœud secondaire du cloud en premier lieu, s’il s’agit actuellement principal, vous devez entreprendre un basculement manuel.

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a>Étape 9 : modification des paramètres de mise en cache du disque dans un fichier CSV et enregistrement
Pour les volumes de données il doivent être définis tooREADONLY.

Pour les volumes TLOG ces doivent être définis tooNONE.

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a>Étape 10 : copie de disques durs virtuels
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



Vous pouvez vérifier l’état de la copie de disques durs virtuels de hello toohello compte de stockage Premium hello :

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

Attendez que toutes ces opérations soient correctement terminées.

Pour plus d'informations pour les objets BLOB individuels :

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a>Étape 11 : inscription du disque du système d’exploitation
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a>Étape 12 : importation d’un serveur secondaire dans un nouveau service cloud
code Hello ci-dessous utilise également les hello ajouté option ici vous pouvez importer un ordinateur hello et utiliser VIP conservables de hello.

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a>Étape 13 : création d'un ILB sur le nouveau service cloud, ajout de points terminaux d'équilibrage de charge et d'ACL
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a>Étape 14 : mise à jour d’Always On
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

Supprimer le service de cloud computing ancien hello adresse IP.

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a>Étape 15 : vérification de la mise à jour DNS
Vous devez maintenant vérifier les serveurs DNS sur votre réseau de client SQL Server et assurez-vous que le clustering a ajouté hello enregistrement d’hôte supplémentaires pour hello ajouté l’adresse IP. Si ces serveurs DNS n’ont pas été mis à jour, envisagez de forcer un transfert de Zone DNS et vous assurer que les clients dans un sous-réseau il n’y a hello sont en mesure de tooresolve tooboth toujours sur des adresses IP, il s’agit donc vous n’avez pas besoin de toowait pour la réplication DNS automatique.

#### <a name="step-16-reconfigure-always-on"></a>Étape 16 : reconfiguration d’Always On
À ce stade vous attendez hello secondaire ce nœud qui a été migré toofully se resynchroniser avec le nœud local de hello et nœud de réplication toosynchronous et rendre hello AFP.  

#### <a name="step-17-migrate-second-node"></a>Étape 17 : migration du deuxième nœud
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a>Étape 18 : modification des paramètres de mise en cache du disque dans un fichier CSV et enregistrement
Pour les volumes de données il doivent être définis tooREADONLY.

Pour les volumes TLOG ces doivent être définis tooNONE.

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a>Étape 19 : création d'un nouveau compte de stockage indépendant pour le nœud secondaire
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a>Étape 20 : copie de disques durs virtuels
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


Vous pouvez vérifier l’état de copie du disque dur virtuel hello pour tous les VHD : ForEach ($disk dans $diskobjects) {$lun = $disk. Numéro d’unité logique $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. Étiquette disquette $diskName = $disk. DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

Attendez que toutes ces opérations soient correctement terminées.

Pour plus d'informations pour les objets BLOB individuels :

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a>Étape 21 : inscription du disque du système d’exploitation
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a>Étape 22 : ajout de points de terminaison et de ACL avec équilibrage de charge
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a>Étape 23 : test du basculement
Vous devez permettent désormais de nœud migrés de hello synchroniser avec hello local toujours sur le nœud, placez-le dans le mode de réplication toosynchronous et attendez qu’il est synchronisé. Basculement local toohello premier nœud migrées, c'est-à-dire hello AFP. Une fois qu’a précédemment fonctionné, dernière modification hello migration AFP toohello de nœud.

Vous devez les tests de basculement entre tous les nœuds et exécuter que les tests chaos tooensure basculements fonctionnent comme prévu et dans un mode en temps voulu.

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a>Étape 24 : réinitialisation des paramètres du quorum de cluster / TTL DNS / Partenaires de basculement / Paramètres de synchronisation
##### <a name="adding-ip-address-resource-on-same-subnet"></a>Ajout de ressource d'adresse IP sur le même sous-réseau
Si vous avez seulement 2 serveurs SQL Server et que vous souhaitez toomigrate les tooa nouveau service cloud, mais souhaitez tookeep sur hello même sous-réseau, vous pouvez éviter de créer de port d’écoute hello toodelete hors connexion d’origine de hello toujours sur l’adresse IP et ajouter la nouvelle adresse IP de hello. Si vous migrez un sous-réseau de tooanother de machines virtuelles hello vous en n'aurez pas besoin toodo comme il y aura un réseau de cluster supplémentaire qui fera référence à ce sous-réseau.

Une fois que vous avez affiché hello migrer la base de données secondaire et ajouté dans la nouvelle ressource d’adresse IP hello pour le nouveau service de cloud hello avant basculement hello principal existant, vous devez effectuer ces opérations dans hello Gestionnaire du Cluster de basculement :

tooadd dans l’adresse IP, consultez hello [annexe](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), étape 14.

1. Pour la ressource d’adresse IP actuelle hello, modifier hello propriétaire possible too'Existing principal SQL Server », dans l’exemple hello ci-dessous, « dansqlams4 » :

    ![Appendix13][23]
2. Nouvelle ressource d’adresse IP hello, modifiez hello propriétaire possible too'Migrated secondaire SQL Server », dans l’exemple hello ci-dessous, « dansqlams5 » :

    ![Appendix14][24]
3. Une fois cette vous pouvez basculer et lors de la migration du dernier nœud hello hello des propriétaires possibles doivent être modifiés afin de ce nœud est ajouté comme propriétaire Possible :

    ![Appendix15][25]

## <a name="additional-resources"></a>Ressources supplémentaires
* [Stockage Premium Azure](../../../storage/common/storage-premium-storage.md)
* [Machines virtuelles](https://azure.microsoft.com/services/virtual-machines/)
* [SQL Server dans des machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
