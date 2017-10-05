---
title: "Créer une configuration SAP multi-SID dans Azure | Microsoft Docs"
description: "Guide de configuration de haute disponibilité pour SAP NetWeaver multi-SID sur machines virtuelles Windows"
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
ms.openlocfilehash: b48df78df9f53ac7bf0804f55a8d36a2fe2f86b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="c416a-103">Créer une configuration SAP NetWeaver multi-SID</span><span class="sxs-lookup"><span data-stu-id="c416a-103">Create an SAP NetWeaver multi-SID configuration</span></span>

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

<span data-ttu-id="c416a-104">En septembre 2016, Microsoft a publié une fonctionnalité vous permettant de gérer plusieurs adresses IP virtuelles à l’aide d’un équilibrage de charge interne Azure.</span><span class="sxs-lookup"><span data-stu-id="c416a-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="c416a-105">Cette fonctionnalité existe déjà dans l’équilibrage de charge externe Azure.</span><span class="sxs-lookup"><span data-stu-id="c416a-105">This functionality already exists in the Azure external load balancer.</span></span>

<span data-ttu-id="c416a-106">Dans le cas d’un déploiement SAP, vous pouvez utiliser un équilibrage de charge interne pour créer une configuration de cluster Windows pour SAP ASCS/SCS, comme indiqué dans le [Guide de haute disponibilité SAP NetWeaver sur machines virtuelles Windows][sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="c416a-106">If you have an SAP deployment, you can use an internal load balancer to create a Windows cluster configuration for SAP ASCS/SCS, as documented in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="c416a-107">Cet article met l’accent sur le passage d’une installation ASCS/SCS unique à une configuration SAP multi-SID en installant des instances SAP ASCS/SCS en cluster supplémentaires dans un cluster de basculement Windows Server (WSFC) existant.</span><span class="sxs-lookup"><span data-stu-id="c416a-107">This article focuses on how to move from a single ASCS/SCS installation to an SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="c416a-108">Lorsque ce processus est terminé, vous aurez configuré un cluster multi-SID SAP.</span><span class="sxs-lookup"><span data-stu-id="c416a-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c416a-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c416a-109">Prerequisites</span></span>
<span data-ttu-id="c416a-110">Vous avez déjà configuré un cluster WSFC qui est utilisé pour une instance SAP ASCS/SCS, comme indiqué dans le [Guide de haute disponibilité SAP NetWeaver sur machines virtuelles Windows][sap-ha-guide] et comme illustré dans ce diagramme.</span><span class="sxs-lookup"><span data-stu-id="c416a-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Instance SAP ASCS/SCS à haute disponibilité][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="c416a-112">Architecture cible</span><span class="sxs-lookup"><span data-stu-id="c416a-112">Target architecture</span></span>

<span data-ttu-id="c416a-113">L’objectif est d’installer plusieurs instances en cluster SAP ABAP ASCS ou SAP Java SCS dans un même cluster WSFC, comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="c416a-113">The goal is to install multiple SAP ABAP ASCS or SAP Java SCS clustered instances in the same WSFC cluster, as illustrated here:</span></span>

![Plusieurs instances SAP ASCS/SCS en cluster dans Azure][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="c416a-115">Il existe une limite au nombre d’adresses IP frontales privées pour chaque équilibrage de charge interne Azure.</span><span class="sxs-lookup"><span data-stu-id="c416a-115">There is a limit to the number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="c416a-116">Le nombre maximal d’instances SAP ASCS/SCS dans un cluster WSFC est égal au nombre maximal d’adresses IP frontales privées pour chaque équilibrage de charge interne Azure.</span><span class="sxs-lookup"><span data-stu-id="c416a-116">The maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal to the maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="c416a-117">Pour plus d’informations sur les limites de l’équilibreur de charge, consultez Adresse IP frontale privée par équilibreur de charge sous [Limites de réseau – Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="c416a-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="c416a-118">Voici une vue d’ensemble avec deux systèmes SAP à haute disponibilité :</span><span class="sxs-lookup"><span data-stu-id="c416a-118">The complete landscape with two high-availability SAP systems would look like this:</span></span>

![Configuration SAP multi-SID haute disponibilité avec deux SID système SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="c416a-120">La configuration doit répondre aux conditions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c416a-120">The setup must meet the following conditions:</span></span>
> - <span data-ttu-id="c416a-121">Les instances SAP ASCS/SCS partagent le même cluster WSFC.</span><span class="sxs-lookup"><span data-stu-id="c416a-121">The SAP ASCS/SCS instances must share the same WSFC cluster.</span></span>
> - <span data-ttu-id="c416a-122">Chaque SID DBMS a son propre cluster WSFC dédié.</span><span class="sxs-lookup"><span data-stu-id="c416a-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="c416a-123">Les serveurs d’applications SAP appartenant au système SAP SID utilisent leurs propres machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c416a-123">SAP application servers that belong to one SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-the-infrastructure"></a><span data-ttu-id="c416a-124">Préparer l’infrastructure</span><span class="sxs-lookup"><span data-stu-id="c416a-124">Prepare the infrastructure</span></span>
<span data-ttu-id="c416a-125">Pour préparer votre infrastructure, vous pouvez installer une instance SAP ASCS/SCS supplémentaire avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="c416a-125">To prepare your infrastructure, you can install an additional SAP ASCS/SCS instance with the following parameters:</span></span>

| <span data-ttu-id="c416a-126">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="c416a-126">Parameter name</span></span> | <span data-ttu-id="c416a-127">Valeur</span><span class="sxs-lookup"><span data-stu-id="c416a-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c416a-128">SID ASCS/SCS SAP</span><span class="sxs-lookup"><span data-stu-id="c416a-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="c416a-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="c416a-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="c416a-130">Équilibrage de charge interne du SGBD SAP</span><span class="sxs-lookup"><span data-stu-id="c416a-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="c416a-131">PR5</span><span class="sxs-lookup"><span data-stu-id="c416a-131">PR5</span></span> |
| <span data-ttu-id="c416a-132">Nom d’hôte virtuel SAP</span><span class="sxs-lookup"><span data-stu-id="c416a-132">SAP virtual host name</span></span> | <span data-ttu-id="c416a-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="c416a-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="c416a-134">Adresse IP de l’hôte virtuel SAP ASCS/SCS (adresse IP d’équilibrage de charge Azure supplémentaire)</span><span class="sxs-lookup"><span data-stu-id="c416a-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="c416a-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="c416a-135">10.0.0.50</span></span> |
| <span data-ttu-id="c416a-136">Numéro de l’instance SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="c416a-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="c416a-137">50</span><span class="sxs-lookup"><span data-stu-id="c416a-137">50</span></span> |
| <span data-ttu-id="c416a-138">Port de sonde d’équilibrage de charge interne pour l’instance SAP ASCS/SCS supplémentaire</span><span class="sxs-lookup"><span data-stu-id="c416a-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="c416a-139">62350</span><span class="sxs-lookup"><span data-stu-id="c416a-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="c416a-140">Pour des instances SAP ASCS/SCS en cluster, chaque adresse IP doit avoir un port de sonde unique.</span><span class="sxs-lookup"><span data-stu-id="c416a-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="c416a-141">Par exemple, si une adresse IP sur un équilibrage de charge interne Azure utilise le port de sonde 62300, aucune autre adresse IP de cet équilibrage de charge ne peut utiliser le port 62300 de la sonde.</span><span class="sxs-lookup"><span data-stu-id="c416a-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="c416a-142">Pour nos besoins, car le port de sonde 62300 est déjà réservé, nous utilisons le port de sonde 62350.</span><span class="sxs-lookup"><span data-stu-id="c416a-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="c416a-143">Vous pouvez installer des instances SAP ASCS/SCS supplémentaire dans le cluster WSFC existant avec deux nœuds :</span><span class="sxs-lookup"><span data-stu-id="c416a-143">You can install additional SAP ASCS/SCS instances in the existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="c416a-144">Rôle de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c416a-144">Virtual machine role</span></span> | <span data-ttu-id="c416a-145">Nom d’hôte de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c416a-145">Virtual machine host name</span></span> | <span data-ttu-id="c416a-146">Adresse IP statique</span><span class="sxs-lookup"><span data-stu-id="c416a-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c416a-147">1er nœud de cluster pour l’instance ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="c416a-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="c416a-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="c416a-148">pr1-ascs-0</span></span> |<span data-ttu-id="c416a-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="c416a-149">10.0.0.10</span></span> |
| <span data-ttu-id="c416a-150">2e nœud de cluster pour l’instance ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="c416a-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="c416a-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="c416a-151">pr1-ascs-1</span></span> |<span data-ttu-id="c416a-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="c416a-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-the-clustered-sap-ascsscs-instance-on-the-dns-server"></a><span data-ttu-id="c416a-153">Créer un nom d’hôte virtuel pour l’instance SAP ASCS/SCS en cluster sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="c416a-153">Create a virtual host name for the clustered SAP ASCS/SCS instance on the DNS server</span></span>

<span data-ttu-id="c416a-154">Vous pouvez créer une entrée DNS pour le nom d’hôte virtuel de l’instance ASCS/SCS en utilisant les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="c416a-154">You can create a DNS entry for the virtual host name of the ASCS/SCS instance by using the following parameters:</span></span>

| <span data-ttu-id="c416a-155">Nouveau nom d’hôte virtuel SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="c416a-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="c416a-156">Adresse IP associée</span><span class="sxs-lookup"><span data-stu-id="c416a-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="c416a-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="c416a-157">pr5-sap-cl</span></span> |<span data-ttu-id="c416a-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="c416a-158">10.0.0.50</span></span> |

<span data-ttu-id="c416a-159">Le nouveau nom d’hôte et l’adresse IP apparaissent dans le Gestionnaire DNS, comme illustré dans la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="c416a-159">The new host name and IP address are displayed in the DNS Manager, as shown in the following screenshot:</span></span>

![Liste du Gestionnaire DNS mettant en surbrillance l’entrée DNS définie pour le nom virtuel et l’adresse TCP/IP du nouveau cluster SAP ASCS/SCS][sap-ha-guide-figure-6004]

<span data-ttu-id="c416a-161">La procédure de création d’une entrée DNS est également décrite en détail dans le principal [guide de haute disponibilité SAP NetWeaver sur des machines virtuelles Windows][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="c416a-161">The procedure for creating a DNS entry is also described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="c416a-162">La nouvelle adresse IP que vous affectez au nom d’hôte virtuel de l’instance ASCS/SCS supplémentaire doit être identique à la nouvelle adresse IP que vous avez affectée à l’équilibrage de charge SAP Azure.</span><span class="sxs-lookup"><span data-stu-id="c416a-162">The new IP address that you assign to the virtual host name of the additional ASCS/SCS instance must be the same as the new IP address that you assigned to the SAP Azure load balancer.</span></span>
>
><span data-ttu-id="c416a-163">Dans notre scénario, l’adresse IP est 10.0.0.50.</span><span class="sxs-lookup"><span data-stu-id="c416a-163">In our scenario, the IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-to-an-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="c416a-164">Ajouter une adresse IP à un équilibrage de charge interne Azure existant à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c416a-164">Add an IP address to an existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="c416a-165">Pour créer plusieurs instances SAP ASCS/SCS dans le même cluster WSFC, utilisez PowerShell pour ajouter une adresse IP à un équilibrage de charge interne Azure existant.</span><span class="sxs-lookup"><span data-stu-id="c416a-165">To create more than one SAP ASCS/SCS instance in the same WSFC cluster, use PowerShell to add an IP address to an existing Azure internal load balancer.</span></span> <span data-ttu-id="c416a-166">Chaque adresse IP requiert une règle d’équilibrage de charge, un port de sonde, un pool IP frontal et un pool principal propres.</span><span class="sxs-lookup"><span data-stu-id="c416a-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="c416a-167">Le script suivant ajoute une nouvelle adresse IP à un équilibreur de charge existant.</span><span class="sxs-lookup"><span data-stu-id="c416a-167">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="c416a-168">Mettez à jour les variables PowerShell de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="c416a-168">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="c416a-169">Le script crée toutes les règles d’équilibrage de charge requises pour tous les ports SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="c416a-169">The script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

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

# Get the Azure VNet and subnet
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

# Assign VM NICs to backend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of the '$VMName' VM to the backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for the ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for the port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' to the internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="c416a-170">Une fois le script exécuté, les résultats sont affichés dans le portail Azure, comme indiqué dans la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="c416a-170">After the script has run, the results are displayed in the Azure portal, as shown in the following screenshot:</span></span>

![Nouveau pool IP frontal dans le portail Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-to-cluster-machines-and-configure-the-sios-cluster-share-disk"></a><span data-ttu-id="c416a-172">Ajouter des disques aux machines du cluster et configurer le disque de partage de cluster SIOS</span><span class="sxs-lookup"><span data-stu-id="c416a-172">Add disks to cluster machines, and configure the SIOS cluster share disk</span></span>

<span data-ttu-id="c416a-173">Vous devez ajouter un nouveau disque de partage de cluster pour chaque instance SAP ASCS/SCS supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="c416a-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="c416a-174">Pour Windows Server 2012 R2, le disque de partage de cluster WSFC utilisé actuellement est la solution logicielle SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="c416a-174">For Windows Server 2012 R2, the WSFC cluster share disk currently in use is the SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="c416a-175">Effectuez les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c416a-175">Do the following:</span></span>
1. <span data-ttu-id="c416a-176">Ajoutez un ou plusieurs disques supplémentaires de même taille (que vous devrez entrelacer) à chacun des nœuds du cluster et formatez-les.</span><span class="sxs-lookup"><span data-stu-id="c416a-176">Add an additional disk or disks of the same size (which you need to stripe) to each of the cluster nodes, and format them.</span></span>
2. <span data-ttu-id="c416a-177">Configurez la réplication de stockage avec SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="c416a-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="c416a-178">Cette procédure suppose que vous avez déjà installé SIOS DataKeeper sur les machines du cluster WSFC.</span><span class="sxs-lookup"><span data-stu-id="c416a-178">This procedure assumes that you have already installed SIOS DataKeeper on the WSFC cluster machines.</span></span> <span data-ttu-id="c416a-179">Si vous l’avez installé, vous devez maintenant configurer la réplication entre les machines.</span><span class="sxs-lookup"><span data-stu-id="c416a-179">If you have installed it, you must now configure replication between the machines.</span></span> <span data-ttu-id="c416a-180">La procédure est décrite en détail dans le principal [guide de haute disponibilité SAP NetWeaver sur des machines virtuelles Windows][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="c416a-180">The process is described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![Mise en miroir synchrone de DataKeeper pour le nouveau disque de partage SAP ASCS/SCS][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="c416a-182">Déployer des machines virtuelles pour les serveurs d’applications SAP et le cluster DBMS</span><span class="sxs-lookup"><span data-stu-id="c416a-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="c416a-183">Pour terminer la préparation de l’infrastructure pour le deuxième système SAP, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c416a-183">To complete the infrastructure preparation for the second SAP system, do the following:</span></span>

1. <span data-ttu-id="c416a-184">Déployer des machines virtuelles dédiées pour les serveurs d’applications SAP et les placer dans leur groupe de disponibilité dédié.</span><span class="sxs-lookup"><span data-stu-id="c416a-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="c416a-185">Déployer des machines virtuelles dédiées pour le cluster DBMS et les placer dans leur groupe de disponibilité dédié.</span><span class="sxs-lookup"><span data-stu-id="c416a-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-the-second-sap-sid2-netweaver-system"></a><span data-ttu-id="c416a-186">Installer le deuxième système SAP SID2 NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c416a-186">Install the second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="c416a-187">Le processus complet d’installation d’un deuxième système SAP SID2 est décrit dans le principal [guide de haute disponibilité SAP NetWeaver sur des machines virtuelles Windows][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="c416a-187">The complete process of installing a second SAP SID2 system is described in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="c416a-188">La procédure détaillée est la suivante :</span><span class="sxs-lookup"><span data-stu-id="c416a-188">The high-level procedure is as follows:</span></span>

1. <span data-ttu-id="c416a-189">[Installez le premier nœud de cluster SAP][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="c416a-189">[Install the SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="c416a-190">Dans cette étape, vous installez SAP avec une instance ASCS/SCS à haute disponibilité sur le **nœud de cluster WSFC existant 1**.</span><span class="sxs-lookup"><span data-stu-id="c416a-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="c416a-191">[Modifiez le profil SAP de l’instance ASCS/SCS][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="c416a-191">[Modify the SAP profile of the ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="c416a-192">[Configurez un port de sonde][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="c416a-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="c416a-193">Dans cette étape, vous configurez le port de sonde SAP-SID2-IP d’une ressource de cluster SAP à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c416a-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="c416a-194">Exécutez cette configuration sur un des nœuds de cluster SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="c416a-194">Execute this configuration on one of the SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="c416a-195">[Installer l’instance de base de données][sap-ha-guide-9.2].</span><span class="sxs-lookup"><span data-stu-id="c416a-195">[Install the database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="c416a-196">Dans cette étape, vous installez SGBD sur un cluster WSFC dédié.</span><span class="sxs-lookup"><span data-stu-id="c416a-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="c416a-197">[Installer le deuxième nœud de cluster][sap-ha-guide-9.3].</span><span class="sxs-lookup"><span data-stu-id="c416a-197">[Install the second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="c416a-198">Dans cette étape, vous installez SAP avec une instance ASCS/SCS à haute disponibilité sur le nœud de cluster WSFC existant 2.</span><span class="sxs-lookup"><span data-stu-id="c416a-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="c416a-199">Ouvrez les ports du pare-feu Windows de l’instance SAP ASCS/SCS et ProbePort.</span><span class="sxs-lookup"><span data-stu-id="c416a-199">Open Windows Firewall ports for the SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="c416a-200">Sur les deux nœuds de cluster utilisés pour l’instance SAP ASCS/SCS, vous ouvrez tous les ports du pare-feu Windows utilisés par SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="c416a-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="c416a-201">Ces ports sont répertoriés dans le [guide de haute disponibilité SAP NetWeaver sur des machines virtuelles Windows][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="c416a-201">These ports are listed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="c416a-202">Ouvrez également le port de sonde de l’équilibrage de charge interne Azure, 62350 dans notre scénario.</span><span class="sxs-lookup"><span data-stu-id="c416a-202">Also open the Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="c416a-203">[Modifiez le type de démarrage de l’instance de service Windows SAP ERS][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="c416a-203">[Change the start type of the SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="c416a-204">[Installez le serveur d’applications principal SAP][sap-ha-guide-9.5] sur la nouvelle machine virtuelle dédiée.</span><span class="sxs-lookup"><span data-stu-id="c416a-204">[Install the SAP primary application server][sap-ha-guide-9.5] on the new dedicated VM.</span></span>

9. <span data-ttu-id="c416a-205">[Installez le serveur d’applications SAP supplémentaire][sap-ha-guide-9.6] sur la nouvelle machine virtuelle dédiée.</span><span class="sxs-lookup"><span data-stu-id="c416a-205">[Install the SAP additional application server][sap-ha-guide-9.6] on the new dedicated VM.</span></span>

10. <span data-ttu-id="c416a-206">[Testez le basculement et la réplication SIOS de l’instance SAP ASCS/SCS][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="c416a-206">[Test the SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c416a-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c416a-207">Next steps</span></span>

- <span data-ttu-id="c416a-208">[Limites de mise en réseau : Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="c416a-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="c416a-209">[Adresses IP virtuelles multiples pour l’équilibrage de charge Azure][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="c416a-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="c416a-210">[Guide de haute disponibilité SAP NetWeaver sur des machines virtuelles Windows][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="c416a-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
