---
title: aaaCreate une configuration de multi-SID SAP dans Azure | Documents Microsoft
description: "Configuration de multi-SID Guide toohigh disponibilité SAP NetWeaver sur machines virtuelles Windows"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a>Créer une configuration SAP NetWeaver multi-SID

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

En septembre 2016, Microsoft a publié une fonctionnalité vous permettant de gérer plusieurs adresses IP virtuelles à l’aide d’un équilibrage de charge interne Azure. Cette fonctionnalité existe déjà dans le programme d’équilibrage de charge externe Azure hello.

Si vous disposez d’un déploiement de SAP, vous pouvez utiliser une toocreate d’équilibrage de charge interne une configuration de cluster Windows pour SAP ASCS/SCS, comme documenté dans hello [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows] [ sap-ha-guide].

Cet article se concentre sur la manière dont toomove à partir d’une configuration de multi-SID de SAP ASCS/SCS installation tooan unique en installant supplémentaires SAP ASCS/SCS des instances de cluster dans un cluster de Clustering de basculement Windows Server (WSFC) existant. Lorsque ce processus est terminé, vous aurez configuré un cluster multi-SID SAP.


## <a name="prerequisites"></a>Composants requis
Vous avez déjà configuré un cluster WSFC qui est utilisé pour une instance SAP ASCS/SCS, comme indiqué dans hello [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows] [ sap-ha-guide] et, comme représenté dans ce diagramme.

![Instance SAP ASCS/SCS à haute disponibilité][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a>Architecture cible

Hello vise tooinstall plusieurs ASC de ABAP SAP ou SCS Java de SAP en cluster des instances Bonjour même cluster WSFC, comme illustré ici :

![Plusieurs instances SAP ASCS/SCS en cluster dans Azure][sap-ha-guide-figure-6002]

> [!NOTE]
>Il existe un toohello limiter le nombre d’adresses IP frontal privées pour chaque équilibrage de charge interne Azure.
>
>nombre maximal de Hello d’instances SAP ASCS/SCS dans un cluster WSFC est égal toohello le nombre maximal d’adresses IP frontal privées pour chaque équilibrage de charge interne Azure.
>

Pour plus d’informations sur les limites de l’équilibreur de charge, consultez Adresse IP frontale privée par équilibreur de charge sous [Limites de réseau – Azure Resource Manager][networking-limits-azure-resource-manager].

liste complète de Hello avec deux systèmes SAP à haute disponibilité ressemble à ceci :

![Configuration SAP multi-SID haute disponibilité avec deux SID système SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> le programme d’installation Hello doit respecter hello conditions suivantes :
> - Hello SAP ASCS/SCS instances doivent partager hello même cluster WSFC.
> - Chaque SID DBMS a son propre cluster WSFC dédié.
> - Serveurs d’applications SAP qui appartiennent SID du système SAP tooone doivent avoir leurs propres ordinateurs virtuels dédiés.


## <a name="prepare-hello-infrastructure"></a>Préparer l’infrastructure de hello
tooprepare votre infrastructure, vous pouvez installer une instance SAP ASCS/SCS supplémentaire avec hello paramètres suivants :

| Nom du paramètre | Valeur |
| --- | --- |
| SID ASCS/SCS SAP |pr1-lb-ascs |
| Équilibrage de charge interne du SGBD SAP | PR5 |
| Nom d’hôte virtuel SAP | pr5-sap-cl |
| Adresse IP de l’hôte virtuel SAP ASCS/SCS (adresse IP d’équilibrage de charge Azure supplémentaire) | 10.0.0.50 |
| Numéro de l’instance SAP ASCS/SCS | 50 |
| Port de sonde d’équilibrage de charge interne pour l’instance SAP ASCS/SCS supplémentaire | 62350 |

> [!NOTE]
> Pour des instances SAP ASCS/SCS en cluster, chaque adresse IP doit avoir un port de sonde unique. Par exemple, si une adresse IP sur un équilibrage de charge interne Azure utilise le port de sonde 62300, aucune autre adresse IP de cet équilibrage de charge ne peut utiliser le port 62300 de la sonde.
>
>Pour nos besoins, car le port de sonde 62300 est déjà réservé, nous utilisons le port de sonde 62350.

Vous pouvez installer des instances SAP ASCS/SCS supplémentaires hello existant cluster WSFC avec deux nœuds :

| Rôle de la machine virtuelle | Nom d’hôte de la machine virtuelle | Adresse IP statique |
| --- | --- | --- |
| 1er nœud de cluster pour l’instance ASCS/SCS |pr1-ascs-0 |10.0.0.10 |
| 2e nœud de cluster pour l’instance ASCS/SCS |pr1-ascs-1 |10.0.0.9 |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a>Créer un nom d’hôte virtuel d’instance de SAP ASCS/SCS hello en cluster sur le serveur DNS de hello

Vous pouvez créer une entrée DNS pour le nom d’hôte virtuel hello de l’instance ASCS/SCS hello à l’aide de hello paramètres suivants :

| Nouveau nom d’hôte virtuel SAP ASCS/SCS | Adresse IP associée |
| --- | --- | --- |
|pr5-sap-cl |10.0.0.50 |

nouveau nom d’hôte Hello et l’adresse IP sont affichées Bonjour le Gestionnaire DNS, comme indiqué dans hello suivant capture d’écran :

![Liste du Gestionnaire DNS mise en surbrillance hello défini par l’entrée DNS pour hello nouvelle SAP ASCS/SCS nom virtuel de cluster et l’adresse TCP/IP][sap-ha-guide-figure-6004]

procédure Hello pour la création d’une entrée DNS est également décrit en détail dans hello principal [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows][sap-ha-guide-9.1.1].

> [!NOTE]
> Hello nouvelle adresse IP que vous affectez le nom d’hôte virtuel toohello d’instance ASCS/SCS supplémentaire de hello doit être hello identique à la nouvelle adresse IP hello, que vous avez affecté à équilibrage de charge toohello SAP Azure.
>
>Dans notre scénario, adresse IP de hello est 10.0.0.50.

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a>Ajouter un équilibrage de charge interne Azure IP adresse tooan existant à l’aide de PowerShell

toocreate, et plusieurs instances SAP ASCS/SCS dans hello WSFC même cluster, utilisez PowerShell tooadd un tooan d’adresse IP existante d’équilibrage de charge interne Azure. Chaque adresse IP requiert une règle d’équilibrage de charge, un port de sonde, un pool IP frontal et un pool principal propres.

Hello script suivant ajoute un nouvelle adresse tooan existant équilibreur de charge IP. Mettre à jour les variables PowerShell hello pour votre environnement. Hello script crée des règles de l’équilibrage de charge tous les besoins pour tous les ports de SAP ASCS/SCS.

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get hello Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
Après l’exécution de script de hello, hello résultats s’affichent dans hello portail Azure, comme indiqué dans hello suivant capture d’écran :

![Nouveau pool d’IP frontale Bonjour portail Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a>Ajoutez des disques toocluster machines et configurer hello SIOS cluster partage de disque

Vous devez ajouter un nouveau disque de partage de cluster pour chaque instance SAP ASCS/SCS supplémentaire. Pour Windows Server 2012 R2, disque du partage du cluster WSFC hello en cours d’utilisation est hello SIOS DataKeeper logiciel.

Hello suivant :
1. Ajouter un autre ou les disques de hello même taille (dont vous avez besoin toostripe) tooeach Hello des nœuds de cluster et les mettre en forme.
2. Configurez la réplication de stockage avec SIOS DataKeeper.

Cette procédure suppose que vous avez déjà installé SIOS DataKeeper sur les ordinateurs du cluster WSFC hello. Si vous l’avez installé, vous devez maintenant configurer la réplication entre les machines hello. processus de Hello est décrit en détail dans hello principal [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows][sap-ha-guide-8.12.3.3].  

![DataKeeper synchrone de mise en miroir pour hello nouveau SAP ASCS/SCS partage de disque][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a>Déployer des machines virtuelles pour les serveurs d’applications SAP et le cluster DBMS

Préparation pour le système SAP de la deuxième hello, toocomplete hello hello suivant :

1. Déployer des machines virtuelles dédiées pour les serveurs d’applications SAP et les placer dans leur groupe de disponibilité dédié.
2. Déployer des machines virtuelles dédiées pour le cluster DBMS et les placer dans leur groupe de disponibilité dédié.


## <a name="install-hello-second-sap-sid2-netweaver-system"></a>Installer le système SAP NetWeaver de SID2 de la deuxième hello

processus d’installation d’un système SAP SID2 deuxième Hello est décrite dans hello principal [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows][sap-ha-guide-9].

procédure de haut niveau de Hello est comme suit :

1. [Installer hello SAP premier nœud de cluster][sap-ha-guide-9.1.2].  
 Dans cette étape, vous installez SAP avec une instance ASCS/SCS de haute disponibilité sur hello **le nœud de cluster WSFC existant 1**.

2. [Modifier hello profil de SAP de l’instance ASCS/SCS hello][sap-ha-guide-9.1.3].

3. [Configurez un port de sonde][sap-ha-guide-9.1.4].  
 Dans cette étape, vous configurez le port de sonde SAP-SID2-IP d’une ressource de cluster SAP à l’aide de PowerShell. Exécutez cette configuration sur l’un des nœuds de cluster SAP ASCS/SCS hello.

4. [Installer l’instance de base de données hello] [sap-ha-guide-9.2].  
 Dans cette étape, vous installez SGBD sur un cluster WSFC dédié.

5. [Installer le second nœud de cluster hello] [sap-ha-guide-9.3].  
 Dans cette étape, vous installez SAP avec une instance ASCS/SCS de haute disponibilité sur le nœud de cluster WSFC existant hello 2.

6. Ouvrir les ports du pare-feu Windows pour l’instance de SAP ASCS/SCS hello et ProbePort.  
 Sur les deux nœuds de cluster utilisés pour l’instance SAP ASCS/SCS, vous ouvrez tous les ports du pare-feu Windows utilisés par SAP ASCS/SCS. Ces ports sont répertoriés dans hello [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows][sap-ha-guide-8.8].  
 Également ouvrir le port de sonde équilibrage hello de charge interne Azure, est 62350 dans notre scénario.

7. [Modifier le type de démarrage hello d’instance de service SAP ERS Windows hello][sap-ha-guide-9.4].

8. [Installer le serveur principal de l’application de SAP hello] [ sap-ha-guide-9.5] sur hello nouvelle dédiée de machine virtuelle.

9. [Installer le serveur d’application supplémentaires SAP hello] [ sap-ha-guide-9.6] sur hello nouvelle dédiée de machine virtuelle.

10. [Tester une instance SAP ASCS/SCS hello ou la réplication SIOS][sap-ha-guide-10].

## <a name="next-steps"></a>Étapes suivantes

- [Limites de mise en réseau : Azure Resource Manager][networking-limits-azure-resource-manager]
- [Adresses IP virtuelles multiples pour l’équilibrage de charge Azure][load-balancer-multivip-overview]
- [Guide de haute disponibilité SAP NetWeaver sur des machines virtuelles Windows][sap-ha-guide]
