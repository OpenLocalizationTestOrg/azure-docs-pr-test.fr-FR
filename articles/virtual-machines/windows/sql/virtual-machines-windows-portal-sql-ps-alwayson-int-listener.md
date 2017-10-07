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
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="cf102-103">Configurer un ou plusieurs écouteurs de groupe de disponibilité AlwaysOn - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cf102-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="cf102-104">Cette rubrique explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="cf102-104">This topic shows how to:</span></span>

* <span data-ttu-id="cf102-105">créer un équilibreur de charge interne pour les groupes de disponibilité SQL Server à l’aide d’applets de commande PowerShell ;</span><span class="sxs-lookup"><span data-stu-id="cf102-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="cf102-106">Ajoutez supplémentaires IP adresses tooa équilibrage pour de plus d’un groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="cf102-106">Add additional IP addresses tooa load balancer for more than one availability group.</span></span> 

<span data-ttu-id="cf102-107">Un écouteur de groupe de disponibilité est un nom de réseau virtuel que les clients connectent à accès de base de données toofor.</span><span class="sxs-lookup"><span data-stu-id="cf102-107">An availability group listener is a virtual network name that clients connect toofor database access.</span></span> <span data-ttu-id="cf102-108">Sur les machines virtuelles Azure, un équilibreur de charge conserve adresse hello pour le port d’écoute hello.</span><span class="sxs-lookup"><span data-stu-id="cf102-108">On Azure virtual machines, a load balancer holds hello IP address for hello listener.</span></span> <span data-ttu-id="cf102-109">Hello charge équilibrage itinéraires du trafic toohello instance de SQL Server qui est à l’écoute sur le port de la sonde hello.</span><span class="sxs-lookup"><span data-stu-id="cf102-109">hello load balancer routes traffic toohello instance of SQL Server that is listening on hello probe port.</span></span> <span data-ttu-id="cf102-110">Dans la plupart des cas, un groupe de disponibilité utilise un équilibreur de charge interne.</span><span class="sxs-lookup"><span data-stu-id="cf102-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="cf102-111">Un équilibreur de charge interne Azure peut héberger une ou plusieurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="cf102-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="cf102-112">Chaque adresse IP utilise un port de sonde spécifique.</span><span class="sxs-lookup"><span data-stu-id="cf102-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="cf102-113">Ce document montre comment toouse PowerShell toocreate un équilibreur de charge, ou ajoutez les adresses IP tooan équilibreur de charge existant pour les groupes de disponibilité de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cf102-113">This document shows how toouse PowerShell toocreate a load balancer, or add IP addresses tooan existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="cf102-114">Bonjour capacité tooassign plusieurs équilibreur de charge interne tooan des adresses IP est de nouveau tooAzure et est disponible uniquement dans le modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="cf102-114">hello ability tooassign multiple IP addresses tooan internal load balancer is new tooAzure and is only available in Resource Manager model.</span></span> <span data-ttu-id="cf102-115">toocomplete cette tâche, vous devez toohave un groupe de disponibilité de SQL Server est déployé sur les machines virtuelles dans le modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="cf102-115">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="cf102-116">Les deux machines virtuelles de SQL Server doit appartenir toohello même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="cf102-116">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="cf102-117">Vous pouvez utiliser hello [modèle Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically créer le groupe de disponibilité hello dans Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cf102-117">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Azure Resource Manager.</span></span> <span data-ttu-id="cf102-118">Ce modèle crée automatiquement le groupe de disponibilité hello, notamment l’équilibrage de charge interne hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="cf102-118">This template automatically creates hello availability group, including hello internal load balancer for you.</span></span> <span data-ttu-id="cf102-119">Si vous préférez, vous pouvez [configurer manuellement un groupe de disponibilité AlwaysOn](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="cf102-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="cf102-120">Cette rubrique requiert que vos groupes de disponibilité soient déjà configurés.</span><span class="sxs-lookup"><span data-stu-id="cf102-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="cf102-121">Rubriques connexes :</span><span class="sxs-lookup"><span data-stu-id="cf102-121">Related topics include:</span></span>

* [<span data-ttu-id="cf102-122">Configuration de groupes de disponibilité AlwaysOn dans Azure VM (GUI)</span><span class="sxs-lookup"><span data-stu-id="cf102-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="cf102-123">Configurer une connexion de réseau virtuel à réseau virtuel à l’aide d’Azure Resource Manager et de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf102-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a><span data-ttu-id="cf102-124">Configurer le pare-feu Windows de hello</span><span class="sxs-lookup"><span data-stu-id="cf102-124">Configure hello Windows Firewall</span></span>
<span data-ttu-id="cf102-125">Configurez l’accès de SQL Server tooallow hello le pare-feu Windows.</span><span class="sxs-lookup"><span data-stu-id="cf102-125">Configure hello Windows Firewall tooallow SQL Server access.</span></span> <span data-ttu-id="cf102-126">règles de pare-feu Hello autorisent ports toohello de connexions TCP à utiliser par l’instance de SQL Server hello et la sonde d’écouteur hello.</span><span class="sxs-lookup"><span data-stu-id="cf102-126">hello firewall rules allow TCP connections toohello ports use by hello SQL Server instance, and hello listener probe.</span></span> <span data-ttu-id="cf102-127">Pour obtenir des instructions détaillées, consultez [Configurer un pare-feu Windows pour accéder au moteur de base de données](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="cf102-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="cf102-128">Créer une règle de trafic entrant pour hello port SQL Server et pour le port de la sonde hello.</span><span class="sxs-lookup"><span data-stu-id="cf102-128">Create an inbound rule for hello SQL Server port and for hello probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="cf102-129">Exemple de script : Créer un équilibreur de charge interne à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf102-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="cf102-130">Si vous avez créé votre groupe de disponibilité avec hello [modèle Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), équilibrage de charge interne hello a déjà été créé.</span><span class="sxs-lookup"><span data-stu-id="cf102-130">If you created your availability group with hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="cf102-131">Hello script PowerShell suivant crée un équilibreur de charge interne, configure les règles d’équilibrage de charge hello et définit une adresse IP pour l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="cf102-131">hello following PowerShell script creates an internal load balancer, configures hello load balancing rules, and sets an IP address for hello load balancer.</span></span> <span data-ttu-id="cf102-132">script de hello toorun, ouvrez Windows PowerShell ISE et collez le script de hello dans le volet de Script hello.</span><span class="sxs-lookup"><span data-stu-id="cf102-132">toorun hello script, open Windows PowerShell ISE, and paste hello script in hello Script pane.</span></span> <span data-ttu-id="cf102-133">Utilisez `Login-AzureRMAccount` toolog dans tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf102-133">Use `Login-AzureRMAccount` toolog in tooPowerShell.</span></span> <span data-ttu-id="cf102-134">Si vous avez plusieurs abonnements Azure, utilisez `Select-AzureRmSubscription ` abonnement de hello tooset.</span><span class="sxs-lookup"><span data-stu-id="cf102-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` tooset hello subscription.</span></span> 

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

## <span data-ttu-id="cf102-135"><a name="Add-IP"></a>Exemple de script : ajouter un adresse tooan existant équilibreur de charge IP avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf102-135"><a name="Add-IP"></a> Example script: Add an IP address tooan existing load balancer with PowerShell</span></span>
<span data-ttu-id="cf102-136">toouse plus de groupe de disponibilité d’un seul, ajouter un équilibrage de charge IP adresse toohello supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="cf102-136">toouse more than one availability group, add an additional IP address toohello load balancer.</span></span> <span data-ttu-id="cf102-137">Chaque adresse IP requiert une règle d’équilibrage de charge, un port de sonde et un port frontal propres.</span><span class="sxs-lookup"><span data-stu-id="cf102-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="cf102-138">Hello frontal hello port est que les applications utilisent instance de SQL Server tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="cf102-138">hello front-end port is hello port that applications use tooconnect toohello SQL Server instance.</span></span> <span data-ttu-id="cf102-139">Adresses IP pour les différents groupes de disponibilité peuvent utilisez hello même port frontal.</span><span class="sxs-lookup"><span data-stu-id="cf102-139">IP addresses for different availability groups can use hello same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="cf102-140">Pour les groupes de disponibilité SQL Server, chaque adresse IP nécessite un port de sonde spécifique.</span><span class="sxs-lookup"><span data-stu-id="cf102-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="cf102-141">Par exemple, si une adresse IP sur un équilibreur de charge utilise le port de sonde 59999, aucune autre adresse IP de cet équilibreur de charge ne peut utiliser le port 59999 de la sonde.</span><span class="sxs-lookup"><span data-stu-id="cf102-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="cf102-142">Pour plus d’informations sur les limites de l’équilibreur de charge, consultez **Adresse IP frontale privée par équilibreur de charge** sous [Limites de mise en réseau – Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="cf102-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="cf102-143">Pour plus d’informations sur les limites de groupe de disponibilité, consultez [Restrictions (groupes de disponibilité)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="cf102-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="cf102-144">Hello script suivant ajoute un nouvelle adresse tooan existant équilibreur de charge IP.</span><span class="sxs-lookup"><span data-stu-id="cf102-144">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="cf102-145">Hello équilibrage de charge interne utilise le port d’écoute hello pour port frontal d’équilibrage de charge de hello.</span><span class="sxs-lookup"><span data-stu-id="cf102-145">hello ILB uses hello listener port for hello load balancing front-end port.</span></span> <span data-ttu-id="cf102-146">Ce port peut être port hello qui écoute sur SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cf102-146">This port can be hello port that SQL Server is listening on.</span></span> <span data-ttu-id="cf102-147">Pour les instances par défaut de SQL Server, le port de hello est 1433.</span><span class="sxs-lookup"><span data-stu-id="cf102-147">For default instances of SQL Server, hello port is 1433.</span></span> <span data-ttu-id="cf102-148">règle pour un groupe de disponibilité d’équilibrage Hello requiert une adresse IP flottante (retour direct du serveur) pour le port principal hello est hello même en tant que port frontal de hello.</span><span class="sxs-lookup"><span data-stu-id="cf102-148">hello load balancing rule for an availability group requires a floating IP (direct server return) so hello back-end port is hello same as hello front-end port.</span></span> <span data-ttu-id="cf102-149">Mettre à jour les variables hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="cf102-149">Update hello variables for your environment.</span></span> 

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

## <a name="configure-hello-listener"></a><span data-ttu-id="cf102-150">Configurer le port d’écoute hello</span><span class="sxs-lookup"><span data-stu-id="cf102-150">Configure hello listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="cf102-151">Définir le port d’écoute hello dans SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="cf102-151">Set hello listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="cf102-152">Lancez SQL Server Management Studio et connectez-vous toohello le réplica principal.</span><span class="sxs-lookup"><span data-stu-id="cf102-152">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="cf102-153">Accédez trop**haute disponibilité AlwaysOn** | **groupes de disponibilité** | **écouteurs de groupe de disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="cf102-153">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="cf102-154">Vous devez maintenant voir le nom de l’écouteur hello que vous avez créé dans le Gestionnaire de Cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="cf102-154">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="cf102-155">Cliquez sur le nom d’écouteur hello et cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="cf102-155">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="cf102-156">Bonjour **Port** , spécifiez un numéro de port hello écouteur hello à l’aide de hello $EndpointPort utilisé précédemment (1433 était la valeur par défaut hello), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf102-156">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="cf102-157">Écouteur de toohello connexion test hello</span><span class="sxs-lookup"><span data-stu-id="cf102-157">Test hello connection toohello listener</span></span>

<span data-ttu-id="cf102-158">connexion de hello tootest :</span><span class="sxs-lookup"><span data-stu-id="cf102-158">tootest hello connection:</span></span>

1. <span data-ttu-id="cf102-159">RDP tooa SQL Server qui se trouve dans hello virtuel même réseau, mais ne pas les réplicas hello propre.</span><span class="sxs-lookup"><span data-stu-id="cf102-159">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="cf102-160">Cela peut être hello autre serveur SQL Server dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="cf102-160">This can be hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="cf102-161">Utilisez **sqlcmd** connexion de hello tootest utilitaire.</span><span class="sxs-lookup"><span data-stu-id="cf102-161">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="cf102-162">Par exemple, hello script suivant établit une **sqlcmd** réplica principal de connexion toohello via écouteur hello avec l’authentification Windows :</span><span class="sxs-lookup"><span data-stu-id="cf102-162">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="cf102-163">Si l’écouteur de hello utilise un port autre que hello par défaut du port (1433), spécifiez le port de hello dans la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="cf102-163">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="cf102-164">Par exemple, hello commande sqlcmd suivante établit une connexion écouteur tooa sur le port 1435 :</span><span class="sxs-lookup"><span data-stu-id="cf102-164">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="cf102-165">Hello connexion de SQLCMD connecte automatiquement à instance toowhichever de SQL Server héberge hello le réplica principal.</span><span class="sxs-lookup"><span data-stu-id="cf102-165">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="cf102-166">Assurez-vous que port hello que vous spécifiez est ouvert sur le pare-feu hello des deux serveurs SQL.</span><span class="sxs-lookup"><span data-stu-id="cf102-166">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="cf102-167">Les deux serveurs requièrent une règle de trafic entrant pour hello le port TCP que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="cf102-167">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="cf102-168">Pour plus d’informations, consultez [Ajouter ou modifier une règle de pare-feu](http://technet.microsoft.com/library/cc753558.aspx) .</span><span class="sxs-lookup"><span data-stu-id="cf102-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="cf102-169">Instructions et limitations</span><span class="sxs-lookup"><span data-stu-id="cf102-169">Guidelines and limitations</span></span>
<span data-ttu-id="cf102-170">Notez hello suivant les instructions sur l’écouteur du groupe de disponibilité dans Azure à l’aide d’équilibreur de charge interne :</span><span class="sxs-lookup"><span data-stu-id="cf102-170">Note hello following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="cf102-171">Un équilibreur de charge interne, vous uniquement d’accéder à l’écouteur de hello dans hello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="cf102-171">With an internal load balancer, you only access hello listener from within hello same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="cf102-172">Pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="cf102-172">For more information</span></span>
<span data-ttu-id="cf102-173">Pour plus d’informations, consultez [Configure Always On availability group in Azure VM manually (Configuration manuelle d’un groupe de disponibilité Always On dans une machine virtuelle Azure)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="cf102-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="cf102-174">Applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf102-174">PowerShell cmdlets</span></span>
<span data-ttu-id="cf102-175">Utilisez hello suivant toocreate d’applets de commande PowerShell un équilibreur de charge interne pour les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="cf102-175">Use hello following PowerShell cmdlets toocreate an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="cf102-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) permet de créer un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="cf102-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="cf102-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) permet de créer une configuration d’adresse IP frontale pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="cf102-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="cf102-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) permet de créer une configuration de règle pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="cf102-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="cf102-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) permet de créer une configuration de pool d’adresses principales pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="cf102-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="cf102-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) permet de créer une configuration de sonde pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="cf102-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="cf102-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) permet de supprimer un équilibreur de charge à partir d’un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="cf102-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
