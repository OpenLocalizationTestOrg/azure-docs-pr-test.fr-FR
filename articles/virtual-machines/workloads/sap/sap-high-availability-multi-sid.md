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
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="62177-103">Créer une configuration SAP NetWeaver multi-SID</span><span class="sxs-lookup"><span data-stu-id="62177-103">Create an SAP NetWeaver multi-SID configuration</span></span>

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

<span data-ttu-id="62177-104">En septembre 2016, Microsoft a publié une fonctionnalité vous permettant de gérer plusieurs adresses IP virtuelles à l’aide d’un équilibrage de charge interne Azure.</span><span class="sxs-lookup"><span data-stu-id="62177-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="62177-105">Cette fonctionnalité existe déjà dans le programme d’équilibrage de charge externe Azure hello.</span><span class="sxs-lookup"><span data-stu-id="62177-105">This functionality already exists in hello Azure external load balancer.</span></span>

<span data-ttu-id="62177-106">Si vous disposez d’un déploiement de SAP, vous pouvez utiliser une toocreate d’équilibrage de charge interne une configuration de cluster Windows pour SAP ASCS/SCS, comme documenté dans hello [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows] [ sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="62177-106">If you have an SAP deployment, you can use an internal load balancer toocreate a Windows cluster configuration for SAP ASCS/SCS, as documented in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="62177-107">Cet article se concentre sur la manière dont toomove à partir d’une configuration de multi-SID de SAP ASCS/SCS installation tooan unique en installant supplémentaires SAP ASCS/SCS des instances de cluster dans un cluster de Clustering de basculement Windows Server (WSFC) existant.</span><span class="sxs-lookup"><span data-stu-id="62177-107">This article focuses on how toomove from a single ASCS/SCS installation tooan SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="62177-108">Lorsque ce processus est terminé, vous aurez configuré un cluster multi-SID SAP.</span><span class="sxs-lookup"><span data-stu-id="62177-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="62177-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="62177-109">Prerequisites</span></span>
<span data-ttu-id="62177-110">Vous avez déjà configuré un cluster WSFC qui est utilisé pour une instance SAP ASCS/SCS, comme indiqué dans hello [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows] [ sap-ha-guide] et, comme représenté dans ce diagramme.</span><span class="sxs-lookup"><span data-stu-id="62177-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Instance SAP ASCS/SCS à haute disponibilité][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="62177-112">Architecture cible</span><span class="sxs-lookup"><span data-stu-id="62177-112">Target architecture</span></span>

<span data-ttu-id="62177-113">Hello vise tooinstall plusieurs ASC de ABAP SAP ou SCS Java de SAP en cluster des instances Bonjour même cluster WSFC, comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="62177-113">hello goal is tooinstall multiple SAP ABAP ASCS or SAP Java SCS clustered instances in hello same WSFC cluster, as illustrated here:</span></span>

![Plusieurs instances SAP ASCS/SCS en cluster dans Azure][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="62177-115">Il existe un toohello limiter le nombre d’adresses IP frontal privées pour chaque équilibrage de charge interne Azure.</span><span class="sxs-lookup"><span data-stu-id="62177-115">There is a limit toohello number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="62177-116">nombre maximal de Hello d’instances SAP ASCS/SCS dans un cluster WSFC est égal toohello le nombre maximal d’adresses IP frontal privées pour chaque équilibrage de charge interne Azure.</span><span class="sxs-lookup"><span data-stu-id="62177-116">hello maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal toohello maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="62177-117">Pour plus d’informations sur les limites de l’équilibreur de charge, consultez Adresse IP frontale privée par équilibreur de charge sous [Limites de réseau – Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="62177-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="62177-118">liste complète de Hello avec deux systèmes SAP à haute disponibilité ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="62177-118">hello complete landscape with two high-availability SAP systems would look like this:</span></span>

![Configuration SAP multi-SID haute disponibilité avec deux SID système SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="62177-120">le programme d’installation Hello doit respecter hello conditions suivantes :</span><span class="sxs-lookup"><span data-stu-id="62177-120">hello setup must meet hello following conditions:</span></span>
> - <span data-ttu-id="62177-121">Hello SAP ASCS/SCS instances doivent partager hello même cluster WSFC.</span><span class="sxs-lookup"><span data-stu-id="62177-121">hello SAP ASCS/SCS instances must share hello same WSFC cluster.</span></span>
> - <span data-ttu-id="62177-122">Chaque SID DBMS a son propre cluster WSFC dédié.</span><span class="sxs-lookup"><span data-stu-id="62177-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="62177-123">Serveurs d’applications SAP qui appartiennent SID du système SAP tooone doivent avoir leurs propres ordinateurs virtuels dédiés.</span><span class="sxs-lookup"><span data-stu-id="62177-123">SAP application servers that belong tooone SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-hello-infrastructure"></a><span data-ttu-id="62177-124">Préparer l’infrastructure de hello</span><span class="sxs-lookup"><span data-stu-id="62177-124">Prepare hello infrastructure</span></span>
<span data-ttu-id="62177-125">tooprepare votre infrastructure, vous pouvez installer une instance SAP ASCS/SCS supplémentaire avec hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="62177-125">tooprepare your infrastructure, you can install an additional SAP ASCS/SCS instance with hello following parameters:</span></span>

| <span data-ttu-id="62177-126">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="62177-126">Parameter name</span></span> | <span data-ttu-id="62177-127">Valeur</span><span class="sxs-lookup"><span data-stu-id="62177-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="62177-128">SID ASCS/SCS SAP</span><span class="sxs-lookup"><span data-stu-id="62177-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="62177-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="62177-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="62177-130">Équilibrage de charge interne du SGBD SAP</span><span class="sxs-lookup"><span data-stu-id="62177-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="62177-131">PR5</span><span class="sxs-lookup"><span data-stu-id="62177-131">PR5</span></span> |
| <span data-ttu-id="62177-132">Nom d’hôte virtuel SAP</span><span class="sxs-lookup"><span data-stu-id="62177-132">SAP virtual host name</span></span> | <span data-ttu-id="62177-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="62177-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="62177-134">Adresse IP de l’hôte virtuel SAP ASCS/SCS (adresse IP d’équilibrage de charge Azure supplémentaire)</span><span class="sxs-lookup"><span data-stu-id="62177-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="62177-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="62177-135">10.0.0.50</span></span> |
| <span data-ttu-id="62177-136">Numéro de l’instance SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="62177-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="62177-137">50</span><span class="sxs-lookup"><span data-stu-id="62177-137">50</span></span> |
| <span data-ttu-id="62177-138">Port de sonde d’équilibrage de charge interne pour l’instance SAP ASCS/SCS supplémentaire</span><span class="sxs-lookup"><span data-stu-id="62177-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="62177-139">62350</span><span class="sxs-lookup"><span data-stu-id="62177-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="62177-140">Pour des instances SAP ASCS/SCS en cluster, chaque adresse IP doit avoir un port de sonde unique.</span><span class="sxs-lookup"><span data-stu-id="62177-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="62177-141">Par exemple, si une adresse IP sur un équilibrage de charge interne Azure utilise le port de sonde 62300, aucune autre adresse IP de cet équilibrage de charge ne peut utiliser le port 62300 de la sonde.</span><span class="sxs-lookup"><span data-stu-id="62177-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="62177-142">Pour nos besoins, car le port de sonde 62300 est déjà réservé, nous utilisons le port de sonde 62350.</span><span class="sxs-lookup"><span data-stu-id="62177-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="62177-143">Vous pouvez installer des instances SAP ASCS/SCS supplémentaires hello existant cluster WSFC avec deux nœuds :</span><span class="sxs-lookup"><span data-stu-id="62177-143">You can install additional SAP ASCS/SCS instances in hello existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="62177-144">Rôle de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="62177-144">Virtual machine role</span></span> | <span data-ttu-id="62177-145">Nom d’hôte de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="62177-145">Virtual machine host name</span></span> | <span data-ttu-id="62177-146">Adresse IP statique</span><span class="sxs-lookup"><span data-stu-id="62177-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62177-147">1er nœud de cluster pour l’instance ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="62177-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="62177-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="62177-148">pr1-ascs-0</span></span> |<span data-ttu-id="62177-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="62177-149">10.0.0.10</span></span> |
| <span data-ttu-id="62177-150">2e nœud de cluster pour l’instance ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="62177-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="62177-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="62177-151">pr1-ascs-1</span></span> |<span data-ttu-id="62177-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="62177-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a><span data-ttu-id="62177-153">Créer un nom d’hôte virtuel d’instance de SAP ASCS/SCS hello en cluster sur le serveur DNS de hello</span><span class="sxs-lookup"><span data-stu-id="62177-153">Create a virtual host name for hello clustered SAP ASCS/SCS instance on hello DNS server</span></span>

<span data-ttu-id="62177-154">Vous pouvez créer une entrée DNS pour le nom d’hôte virtuel hello de l’instance ASCS/SCS hello à l’aide de hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="62177-154">You can create a DNS entry for hello virtual host name of hello ASCS/SCS instance by using hello following parameters:</span></span>

| <span data-ttu-id="62177-155">Nouveau nom d’hôte virtuel SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="62177-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="62177-156">Adresse IP associée</span><span class="sxs-lookup"><span data-stu-id="62177-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="62177-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="62177-157">pr5-sap-cl</span></span> |<span data-ttu-id="62177-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="62177-158">10.0.0.50</span></span> |

<span data-ttu-id="62177-159">nouveau nom d’hôte Hello et l’adresse IP sont affichées Bonjour le Gestionnaire DNS, comme indiqué dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="62177-159">hello new host name and IP address are displayed in hello DNS Manager, as shown in hello following screenshot:</span></span>

![Liste du Gestionnaire DNS mise en surbrillance hello défini par l’entrée DNS pour hello nouvelle SAP ASCS/SCS nom virtuel de cluster et l’adresse TCP/IP][sap-ha-guide-figure-6004]

<span data-ttu-id="62177-161">procédure Hello pour la création d’une entrée DNS est également décrit en détail dans hello principal [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="62177-161">hello procedure for creating a DNS entry is also described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="62177-162">Hello nouvelle adresse IP que vous affectez le nom d’hôte virtuel toohello d’instance ASCS/SCS supplémentaire de hello doit être hello identique à la nouvelle adresse IP hello, que vous avez affecté à équilibrage de charge toohello SAP Azure.</span><span class="sxs-lookup"><span data-stu-id="62177-162">hello new IP address that you assign toohello virtual host name of hello additional ASCS/SCS instance must be hello same as hello new IP address that you assigned toohello SAP Azure load balancer.</span></span>
>
><span data-ttu-id="62177-163">Dans notre scénario, adresse IP de hello est 10.0.0.50.</span><span class="sxs-lookup"><span data-stu-id="62177-163">In our scenario, hello IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="62177-164">Ajouter un équilibrage de charge interne Azure IP adresse tooan existant à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="62177-164">Add an IP address tooan existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="62177-165">toocreate, et plusieurs instances SAP ASCS/SCS dans hello WSFC même cluster, utilisez PowerShell tooadd un tooan d’adresse IP existante d’équilibrage de charge interne Azure.</span><span class="sxs-lookup"><span data-stu-id="62177-165">toocreate more than one SAP ASCS/SCS instance in hello same WSFC cluster, use PowerShell tooadd an IP address tooan existing Azure internal load balancer.</span></span> <span data-ttu-id="62177-166">Chaque adresse IP requiert une règle d’équilibrage de charge, un port de sonde, un pool IP frontal et un pool principal propres.</span><span class="sxs-lookup"><span data-stu-id="62177-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="62177-167">Hello script suivant ajoute un nouvelle adresse tooan existant équilibreur de charge IP.</span><span class="sxs-lookup"><span data-stu-id="62177-167">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="62177-168">Mettre à jour les variables PowerShell hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="62177-168">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="62177-169">Hello script crée des règles de l’équilibrage de charge tous les besoins pour tous les ports de SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="62177-169">hello script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

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
<span data-ttu-id="62177-170">Après l’exécution de script de hello, hello résultats s’affichent dans hello portail Azure, comme indiqué dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="62177-170">After hello script has run, hello results are displayed in hello Azure portal, as shown in hello following screenshot:</span></span>

![Nouveau pool d’IP frontale Bonjour portail Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a><span data-ttu-id="62177-172">Ajoutez des disques toocluster machines et configurer hello SIOS cluster partage de disque</span><span class="sxs-lookup"><span data-stu-id="62177-172">Add disks toocluster machines, and configure hello SIOS cluster share disk</span></span>

<span data-ttu-id="62177-173">Vous devez ajouter un nouveau disque de partage de cluster pour chaque instance SAP ASCS/SCS supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="62177-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="62177-174">Pour Windows Server 2012 R2, disque du partage du cluster WSFC hello en cours d’utilisation est hello SIOS DataKeeper logiciel.</span><span class="sxs-lookup"><span data-stu-id="62177-174">For Windows Server 2012 R2, hello WSFC cluster share disk currently in use is hello SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="62177-175">Hello suivant :</span><span class="sxs-lookup"><span data-stu-id="62177-175">Do hello following:</span></span>
1. <span data-ttu-id="62177-176">Ajouter un autre ou les disques de hello même taille (dont vous avez besoin toostripe) tooeach Hello des nœuds de cluster et les mettre en forme.</span><span class="sxs-lookup"><span data-stu-id="62177-176">Add an additional disk or disks of hello same size (which you need toostripe) tooeach of hello cluster nodes, and format them.</span></span>
2. <span data-ttu-id="62177-177">Configurez la réplication de stockage avec SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="62177-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="62177-178">Cette procédure suppose que vous avez déjà installé SIOS DataKeeper sur les ordinateurs du cluster WSFC hello.</span><span class="sxs-lookup"><span data-stu-id="62177-178">This procedure assumes that you have already installed SIOS DataKeeper on hello WSFC cluster machines.</span></span> <span data-ttu-id="62177-179">Si vous l’avez installé, vous devez maintenant configurer la réplication entre les machines hello.</span><span class="sxs-lookup"><span data-stu-id="62177-179">If you have installed it, you must now configure replication between hello machines.</span></span> <span data-ttu-id="62177-180">processus de Hello est décrit en détail dans hello principal [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="62177-180">hello process is described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![DataKeeper synchrone de mise en miroir pour hello nouveau SAP ASCS/SCS partage de disque][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="62177-182">Déployer des machines virtuelles pour les serveurs d’applications SAP et le cluster DBMS</span><span class="sxs-lookup"><span data-stu-id="62177-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="62177-183">Préparation pour le système SAP de la deuxième hello, toocomplete hello hello suivant :</span><span class="sxs-lookup"><span data-stu-id="62177-183">toocomplete hello infrastructure preparation for hello second SAP system, do hello following:</span></span>

1. <span data-ttu-id="62177-184">Déployer des machines virtuelles dédiées pour les serveurs d’applications SAP et les placer dans leur groupe de disponibilité dédié.</span><span class="sxs-lookup"><span data-stu-id="62177-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="62177-185">Déployer des machines virtuelles dédiées pour le cluster DBMS et les placer dans leur groupe de disponibilité dédié.</span><span class="sxs-lookup"><span data-stu-id="62177-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-hello-second-sap-sid2-netweaver-system"></a><span data-ttu-id="62177-186">Installer le système SAP NetWeaver de SID2 de la deuxième hello</span><span class="sxs-lookup"><span data-stu-id="62177-186">Install hello second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="62177-187">processus d’installation d’un système SAP SID2 deuxième Hello est décrite dans hello principal [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="62177-187">hello complete process of installing a second SAP SID2 system is described in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="62177-188">procédure de haut niveau de Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="62177-188">hello high-level procedure is as follows:</span></span>

1. <span data-ttu-id="62177-189">[Installer hello SAP premier nœud de cluster][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="62177-189">[Install hello SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="62177-190">Dans cette étape, vous installez SAP avec une instance ASCS/SCS de haute disponibilité sur hello **le nœud de cluster WSFC existant 1**.</span><span class="sxs-lookup"><span data-stu-id="62177-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="62177-191">[Modifier hello profil de SAP de l’instance ASCS/SCS hello][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="62177-191">[Modify hello SAP profile of hello ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="62177-192">[Configurez un port de sonde][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="62177-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="62177-193">Dans cette étape, vous configurez le port de sonde SAP-SID2-IP d’une ressource de cluster SAP à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62177-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="62177-194">Exécutez cette configuration sur l’un des nœuds de cluster SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="62177-194">Execute this configuration on one of hello SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="62177-195">[Installer l’instance de base de données hello] [sap-ha-guide-9.2].</span><span class="sxs-lookup"><span data-stu-id="62177-195">[Install hello database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="62177-196">Dans cette étape, vous installez SGBD sur un cluster WSFC dédié.</span><span class="sxs-lookup"><span data-stu-id="62177-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="62177-197">[Installer le second nœud de cluster hello] [sap-ha-guide-9.3].</span><span class="sxs-lookup"><span data-stu-id="62177-197">[Install hello second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="62177-198">Dans cette étape, vous installez SAP avec une instance ASCS/SCS de haute disponibilité sur le nœud de cluster WSFC existant hello 2.</span><span class="sxs-lookup"><span data-stu-id="62177-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="62177-199">Ouvrir les ports du pare-feu Windows pour l’instance de SAP ASCS/SCS hello et ProbePort.</span><span class="sxs-lookup"><span data-stu-id="62177-199">Open Windows Firewall ports for hello SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="62177-200">Sur les deux nœuds de cluster utilisés pour l’instance SAP ASCS/SCS, vous ouvrez tous les ports du pare-feu Windows utilisés par SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="62177-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="62177-201">Ces ports sont répertoriés dans hello [guide pour la haute disponibilité SAP NetWeaver sur machines virtuelles Windows][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="62177-201">These ports are listed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="62177-202">Également ouvrir le port de sonde équilibrage hello de charge interne Azure, est 62350 dans notre scénario.</span><span class="sxs-lookup"><span data-stu-id="62177-202">Also open hello Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="62177-203">[Modifier le type de démarrage hello d’instance de service SAP ERS Windows hello][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="62177-203">[Change hello start type of hello SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="62177-204">[Installer le serveur principal de l’application de SAP hello] [ sap-ha-guide-9.5] sur hello nouvelle dédiée de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="62177-204">[Install hello SAP primary application server][sap-ha-guide-9.5] on hello new dedicated VM.</span></span>

9. <span data-ttu-id="62177-205">[Installer le serveur d’application supplémentaires SAP hello] [ sap-ha-guide-9.6] sur hello nouvelle dédiée de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="62177-205">[Install hello SAP additional application server][sap-ha-guide-9.6] on hello new dedicated VM.</span></span>

10. <span data-ttu-id="62177-206">[Tester une instance SAP ASCS/SCS hello ou la réplication SIOS][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="62177-206">[Test hello SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="62177-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62177-207">Next steps</span></span>

- <span data-ttu-id="62177-208">[Limites de mise en réseau : Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="62177-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="62177-209">[Adresses IP virtuelles multiples pour l’équilibrage de charge Azure][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="62177-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="62177-210">[Guide de haute disponibilité SAP NetWeaver sur des machines virtuelles Windows][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="62177-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
