---
title: "aaaCreate une machine virtuelle (classique) avec plusieurs cartes réseau - Azure PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle (classique) avec plusieurs cartes réseau à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a>Créer une machine virtuelle (classique) avec plusieurs cartes réseau à l’aide de PowerShell

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Vous pouvez créer des machines virtuelles (VM) dans Azure et attacher plusieurs tooeach de cartes réseau de vos ordinateurs virtuels. Plusieurs cartes réseau permettent la séparation des types de trafic entre les cartes réseau. Par exemple, une que carte réseau peut communiquer avec hello Internet, tandis que l’autre communique uniquement avec les ressources internes non connecté toohello Internet. Hello capacité tooseparate le trafic entre plusieurs cartes réseau est requis pour les nombreux équipements virtuels réseau, telles que la remise des applications et des solutions d’optimisation de réseau étendu.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Découvrez comment tooperform ces étapes à l’aide de hello [modèle de déploiement de gestionnaire de ressources](virtual-network-deploy-multinic-arm-ps.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

étapes suivantes Hello utilisent un groupe de ressources nommé *IaaSStory* pour les serveurs WEB hello et un groupe de ressources nommé *IaaSStory-principal* pour les serveurs de base de données de hello.

## <a name="prerequisites"></a>Composants requis

Avant de pouvoir créer hello des serveurs de base de données, vous devez toocreate hello *IaaSStory* groupe de ressources avec toutes les ressources nécessaires hello pour ce scénario. toocreate ces ressources, complètes hello étapes qui suivent. Créer un réseau virtuel en suivant les étapes de hello Bonjour [créer un réseau virtuel](virtual-networks-create-vnet-classic-netcfg-ps.md) l’article.

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Créer des machines virtuelles de back-end hello
Hello machines virtuelles du serveur principal dépendent de la création de hello Hello suivant des ressources :

* **Sous-réseau principal**. serveurs de base de données Hello feront partie d’un sous-réseau distinct, le trafic de toosegregate. le script ci-dessous Hello attend ce tooexist de sous-réseau dans un réseau virtuel nommé *WTestVnet*.
* **Compte de stockage pour les disques de données**. Pour de meilleures performances, les disques de données hello sur les serveurs de base de données hello utilisera (SSD) de lecteur SSD, ce qui nécessite un compte de stockage premium. Vérifiez que hello emplacement Azure que vous déployez le stockage de premium toosupport.
* **Groupe à haute disponibilité**. Tous les serveurs de base de données seront ajoutés à haute disponibilité unique tooa, tooensure au moins une des machines virtuelles de hello est en cours d’exécution lors de la maintenance.

### <a name="step-1---start-your-script"></a>Étape 1 : démarrer votre script
Vous pouvez télécharger le script PowerShell complet hello utilisé [ici](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1). Suivez les étapes de hello ci-dessous toochange hello script toowork dans votre environnement.

1. Modifier les valeurs hello de variables hello ci-dessous en fonction de votre groupe de ressources existant déployé ci-dessus dans [conditions préalables](#Prerequisites).

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. Modifier les valeurs hello de variables hello ci-dessous en fonction des valeurs de hello souhaité toouse pour votre déploiement de serveur principal.

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Étape 2 : création des ressources nécessaires pour vos machines virtuelles
Vous devez toocreate compte un nouveau service cloud et un stockage pour les disques de données hello pour toutes les machines virtuelles. Vous devez également toospecify d’une image et un compte d’administrateur local pour hello machines virtuelles. fin de ces ressources, toocreate hello comme suit :

1. Créez un nouveau service cloud.

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. Créez un compte de stockage Premium.

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. Compte de stockage hello jeu créé ci-dessus en tant que compte de stockage actif hello pour votre abonnement.

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. Sélectionnez une image pour hello machine virtuelle.

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. Définir les informations d’identification du compte hello administrateur local.

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a>Étape 3 : création de machines virtuelles
Vous devez toouse une toocreate boucle comme de nombreux ordinateurs virtuels que vous souhaitez et créez hello nécessaires des cartes réseau et des machines virtuelles au sein de la boucle de hello. toocreate hello cartes réseau et les ordinateurs virtuels, exécutez hello comme suit.

1. Démarrer un `for` hello toorepeat de boucle commandes toocreate une machine virtuelle et deux cartes réseau comme autant de fois que nécessaire, en fonction de la valeur hello hello `$numberOfVMs` variable.

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. Créer un `VMConfig` objet spécifiant hello image, taille et ensemble de disponibilité pour hello machine virtuelle.

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. Configurer hello machine virtuelle comme une machine virtuelle Windows.

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. Définir la valeur par défaut de hello NIC et attribuez-lui une adresse IP statique.

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. Ajoutez une deuxième carte réseau pour chaque machine virtuelle.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. Créer des disques toodata pour chaque machine virtuelle.

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. Créer chaque machine virtuelle et terminer la boucle hello.

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a>Étape 4 : exécution hello script
Maintenant que vous avez téléchargé et modifié le script de hello selon vos besoins, exécutez il script de base de données principale toocreate hello machines virtuelles avec plusieurs cartes réseau.

1. Enregistrez votre script et exécutez-le à partir de hello **PowerShell** invite de commandes, ou **PowerShell ISE**. Vous verrez un résultat initial de hello, comme indiqué ci-dessous.

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. Remplissez les informations hello nécessaires dans l’invite d’informations d’identification hello et cliquez sur **OK**. Hello ci-dessous est retourné.

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
