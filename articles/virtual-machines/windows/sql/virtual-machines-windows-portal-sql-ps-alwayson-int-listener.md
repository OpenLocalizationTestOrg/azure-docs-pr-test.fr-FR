---
title: "aaaConfigure toujours sur disponibilité écouteurs de groupe – Microsoft Azure | Documents Microsoft"
description: "Configurer les écouteurs de groupe de disponibilité sur le modèle Azure Resource Manager hello à l’aide d’un équilibreur de charge interne avec une ou plusieurs adresses IP."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a>Configurer un ou plusieurs écouteurs de groupe de disponibilité AlwaysOn - Resource Manager
Cette rubrique explique comment effectuer les opérations suivantes :

* créer un équilibreur de charge interne pour les groupes de disponibilité SQL Server à l’aide d’applets de commande PowerShell ;
* Ajoutez supplémentaires IP adresses tooa équilibrage pour de plus d’un groupe de disponibilité. 

Un écouteur de groupe de disponibilité est un nom de réseau virtuel que les clients connectent à accès de base de données toofor. Sur les machines virtuelles Azure, un équilibreur de charge conserve adresse hello pour le port d’écoute hello. Hello charge équilibrage itinéraires du trafic toohello instance de SQL Server qui est à l’écoute sur le port de la sonde hello. Dans la plupart des cas, un groupe de disponibilité utilise un équilibreur de charge interne. Un équilibreur de charge interne Azure peut héberger une ou plusieurs adresses IP. Chaque adresse IP utilise un port de sonde spécifique. Ce document montre comment toouse PowerShell toocreate un équilibreur de charge, ou ajoutez les adresses IP tooan équilibreur de charge existant pour les groupes de disponibilité de SQL Server. 

Bonjour capacité tooassign plusieurs équilibreur de charge interne tooan des adresses IP est de nouveau tooAzure et est disponible uniquement dans le modèle de gestionnaire de ressources. toocomplete cette tâche, vous devez toohave un groupe de disponibilité de SQL Server est déployé sur les machines virtuelles dans le modèle de gestionnaire de ressources. Les deux machines virtuelles de SQL Server doit appartenir toohello même groupe à haute disponibilité. Vous pouvez utiliser hello [modèle Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically créer le groupe de disponibilité hello dans Azure Resource Manager. Ce modèle crée automatiquement le groupe de disponibilité hello, notamment l’équilibrage de charge interne hello pour vous. Si vous préférez, vous pouvez [configurer manuellement un groupe de disponibilité AlwaysOn](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Cette rubrique requiert que vos groupes de disponibilité soient déjà configurés.  

Rubriques connexes :

* [Configuration de groupes de disponibilité AlwaysOn dans Azure VM (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Configurer une connexion de réseau virtuel à réseau virtuel à l’aide d’Azure Resource Manager et de PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a>Configurer le pare-feu Windows de hello
Configurez l’accès de SQL Server tooallow hello le pare-feu Windows. règles de pare-feu Hello autorisent ports toohello de connexions TCP à utiliser par l’instance de SQL Server hello et la sonde d’écouteur hello. Pour obtenir des instructions détaillées, consultez [Configurer un pare-feu Windows pour accéder au moteur de base de données](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1). Créer une règle de trafic entrant pour hello port SQL Server et pour le port de la sonde hello.

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a>Exemple de script : Créer un équilibreur de charge interne à l’aide de PowerShell
> [!NOTE]
> Si vous avez créé votre groupe de disponibilité avec hello [modèle Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), équilibrage de charge interne hello a déjà été créé. 
> 
> 

Hello script PowerShell suivant crée un équilibreur de charge interne, configure les règles d’équilibrage de charge hello et définit une adresse IP pour l’équilibrage de charge hello. script de hello toorun, ouvrez Windows PowerShell ISE et collez le script de hello dans le volet de Script hello. Utilisez `Login-AzureRMAccount` toolog dans tooPowerShell. Si vous avez plusieurs abonnements Azure, utilisez `Select-AzureRmSubscription ` abonnement de hello tooset. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <a name="Add-IP"></a>Exemple de script : ajouter un adresse tooan existant équilibreur de charge IP avec PowerShell
toouse plus de groupe de disponibilité d’un seul, ajouter un équilibrage de charge IP adresse toohello supplémentaire. Chaque adresse IP requiert une règle d’équilibrage de charge, un port de sonde et un port frontal propres.

Hello frontal hello port est que les applications utilisent instance de SQL Server tooconnect toohello. Adresses IP pour les différents groupes de disponibilité peuvent utilisez hello même port frontal.

> [!NOTE]
> Pour les groupes de disponibilité SQL Server, chaque adresse IP nécessite un port de sonde spécifique. Par exemple, si une adresse IP sur un équilibreur de charge utilise le port de sonde 59999, aucune autre adresse IP de cet équilibreur de charge ne peut utiliser le port 59999 de la sonde.

* Pour plus d’informations sur les limites de l’équilibreur de charge, consultez **Adresse IP frontale privée par équilibreur de charge** sous [Limites de mise en réseau – Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).
* Pour plus d’informations sur les limites de groupe de disponibilité, consultez [Restrictions (groupes de disponibilité)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).

Hello script suivant ajoute un nouvelle adresse tooan existant équilibreur de charge IP. Hello équilibrage de charge interne utilise le port d’écoute hello pour port frontal d’équilibrage de charge de hello. Ce port peut être port hello qui écoute sur SQL Server. Pour les instances par défaut de SQL Server, le port de hello est 1433. règle pour un groupe de disponibilité d’équilibrage Hello requiert une adresse IP flottante (retour direct du serveur) pour le port principal hello est hello même en tant que port frontal de hello. Mettre à jour les variables hello pour votre environnement. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a>Configurer le port d’écoute hello

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a>Définir le port d’écoute hello dans SQL Server Management Studio

1. Lancez SQL Server Management Studio et connectez-vous toohello le réplica principal.

1. Accédez trop**haute disponibilité AlwaysOn** | **groupes de disponibilité** | **écouteurs de groupe de disponibilité**. 

1. Vous devez maintenant voir le nom de l’écouteur hello que vous avez créé dans le Gestionnaire de Cluster de basculement. Cliquez sur le nom d’écouteur hello et cliquez sur **propriétés**.

1. Bonjour **Port** , spécifiez un numéro de port hello écouteur hello à l’aide de hello $EndpointPort utilisé précédemment (1433 était la valeur par défaut hello), puis cliquez sur **OK**.

## <a name="test-hello-connection-toohello-listener"></a>Écouteur de toohello connexion test hello

connexion de hello tootest :

1. RDP tooa SQL Server qui se trouve dans hello virtuel même réseau, mais ne pas les réplicas hello propre. Cela peut être hello autre serveur SQL Server dans un cluster de hello.

1. Utilisez **sqlcmd** connexion de hello tootest utilitaire. Par exemple, hello script suivant établit une **sqlcmd** réplica principal de connexion toohello via écouteur hello avec l’authentification Windows :
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    Si l’écouteur de hello utilise un port autre que hello par défaut du port (1433), spécifiez le port de hello dans la chaîne de connexion hello. Par exemple, hello commande sqlcmd suivante établit une connexion écouteur tooa sur le port 1435 : 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Hello connexion de SQLCMD connecte automatiquement à instance toowhichever de SQL Server héberge hello le réplica principal. 

> [!NOTE]
> Assurez-vous que port hello que vous spécifiez est ouvert sur le pare-feu hello des deux serveurs SQL. Les deux serveurs requièrent une règle de trafic entrant pour hello le port TCP que vous utilisez. Pour plus d’informations, consultez [Ajouter ou modifier une règle de pare-feu](http://technet.microsoft.com/library/cc753558.aspx) . 
> 
> 

## <a name="guidelines-and-limitations"></a>Instructions et limitations
Notez hello suivant les instructions sur l’écouteur du groupe de disponibilité dans Azure à l’aide d’équilibreur de charge interne :

* Un équilibreur de charge interne, vous uniquement d’accéder à l’écouteur de hello dans hello même réseau virtuel.


## <a name="for-more-information"></a>Pour plus d’informations
Pour plus d’informations, consultez [Configure Always On availability group in Azure VM manually (Configuration manuelle d’un groupe de disponibilité Always On dans une machine virtuelle Azure)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

## <a name="powershell-cmdlets"></a>Applets de commande PowerShell
Utilisez hello suivant toocreate d’applets de commande PowerShell un équilibreur de charge interne pour les machines virtuelles.

* [New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) permet de créer un équilibreur de charge. 
* [New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) permet de créer une configuration d’adresse IP frontale pour un équilibreur de charge. 
* [New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) permet de créer une configuration de règle pour un équilibreur de charge. 
* [New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) permet de créer une configuration de pool d’adresses principales pour un équilibreur de charge. 
* [New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) permet de créer une configuration de sonde pour un équilibreur de charge.
* [Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) permet de supprimer un équilibreur de charge à partir d’un groupe de ressources Azure.
