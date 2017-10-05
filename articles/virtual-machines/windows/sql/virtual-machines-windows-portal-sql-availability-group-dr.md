---
title: "Groupes de disponibilité SQL Server - Machines virtuelles Azure - Récupération d’urgence | Microsoft Docs"
description: "Cet article explique comment configurer un groupe de disponibilité SQL Server sur des machines virtuelles avec un réplica dans une autre région."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 1ce90cf4bae66bfd6387a2698fd9b1ba7fc64595
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="c99e6-103">Configurer un groupe de disponibilité AlwaysOn sur des machines virtuelles Azure dans des emplacements différents</span><span class="sxs-lookup"><span data-stu-id="c99e6-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="c99e6-104">Cet article explique comment configurer un réplica de groupe de disponibilité SQL Server AlwaysOn sur des machines virtuelles Azure dans un emplacement Azure distant.</span><span class="sxs-lookup"><span data-stu-id="c99e6-104">This article explains how to configure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="c99e6-105">Utilisez cette configuration pour prendre en charge la récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="c99e6-105">Use this configuration to support disaster recovery.</span></span>

<span data-ttu-id="c99e6-106">Cet article s’applique aux machines virtuelles Azure s’exécutant en mode Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c99e6-106">This article applies to Azure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="c99e6-107">L’illustration suivante montre un déploiement classique d’un groupe de disponibilité sur des machines virtuelles Azure :</span><span class="sxs-lookup"><span data-stu-id="c99e6-107">The following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="c99e6-109">Dans ce déploiement, toutes les machines virtuelles sont dans une région Azure.</span><span class="sxs-lookup"><span data-stu-id="c99e6-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="c99e6-110">Les réplicas de groupe de disponibilité peuvent avoir une validation synchrone avec basculement automatique sur SQL-1 et SQL-2.</span><span class="sxs-lookup"><span data-stu-id="c99e6-110">The availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="c99e6-111">Pour générer cette architecture, consultez [Modèle de groupe de disponibilité ou didacticiel](virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c99e6-111">To build this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="c99e6-112">Cette architecture est vulnérable aux interruptions de service si la région Azure devient inaccessible.</span><span class="sxs-lookup"><span data-stu-id="c99e6-112">This architecture is vulnerable to downtime if the Azure region becomes inaccessible.</span></span> <span data-ttu-id="c99e6-113">Pour résoudre cette vulnérabilité, ajoutez un réplica dans une autre région Azure.</span><span class="sxs-lookup"><span data-stu-id="c99e6-113">To overcome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="c99e6-114">Le schéma suivant illustre l’aspect de la nouvelle architecture :</span><span class="sxs-lookup"><span data-stu-id="c99e6-114">The following diagram shows how the new architecture would look:</span></span>

   ![Récupération d’urgence du groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="c99e6-116">Le diagramme précédent illustre une nouvelle machine virtuelle appelée SQL-3.</span><span class="sxs-lookup"><span data-stu-id="c99e6-116">The preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="c99e6-117">SQL-3 se trouve dans une autre région Azure.</span><span class="sxs-lookup"><span data-stu-id="c99e6-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="c99e6-118">SQL-3 est ajoutée au cluster de basculement Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c99e6-118">SQL-3 is added to the Windows Server Failover Cluster.</span></span> <span data-ttu-id="c99e6-119">SQL-3 peut héberger un réplica de groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="c99e6-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="c99e6-120">Notez enfin que la région Azure de SQL-3 a un nouvel équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="c99e6-120">Finally, notice that the Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="c99e6-121">Un groupe à haute disponibilité Azure est requis lorsque plusieurs machines virtuelles se trouvent dans la même région.</span><span class="sxs-lookup"><span data-stu-id="c99e6-121">An Azure availability set is required when more than one virtual machine is in the same region.</span></span> <span data-ttu-id="c99e6-122">Si une seule machine virtuelle se trouve dans la région, le groupe à haute disponibilité n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c99e6-122">If only one virtual machine is in the region, then the availability set is not required.</span></span> <span data-ttu-id="c99e6-123">Vous ne pouvez placer une machine virtuelle dans un groupe à haute disponibilité que lors de la création.</span><span class="sxs-lookup"><span data-stu-id="c99e6-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="c99e6-124">Si la machine virtuelle se trouve déjà dans un groupe à haute disponibilité, vous pouvez ajouter une machine virtuelle à un réplica supplémentaire ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="c99e6-124">If the virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="c99e6-125">Dans cette architecture, le réplica dans la région distante est normalement configuré avec le mode de disponibilité à validation asynchrone et le mode de basculement manuel.</span><span class="sxs-lookup"><span data-stu-id="c99e6-125">In this architecture, the replica in the remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="c99e6-126">Lorsque les réplicas du groupe de disponibilité se trouvent sur des machines virtuelles Azure dans différentes régions Azure, chaque région requiert :</span><span class="sxs-lookup"><span data-stu-id="c99e6-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="c99e6-127">Une passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="c99e6-127">A virtual network gateway</span></span>
* <span data-ttu-id="c99e6-128">Une connexion à la passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="c99e6-128">A virtual network gateway connection</span></span>

<span data-ttu-id="c99e6-129">Le schéma suivant montre comment les réseaux communiquent entre les centres de données.</span><span class="sxs-lookup"><span data-stu-id="c99e6-129">The following diagram shows how the networks communicate between data centers.</span></span>

   ![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="c99e6-131">Cette architecture facture les données sortantes des données répliquées entre des régions Azure.</span><span class="sxs-lookup"><span data-stu-id="c99e6-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="c99e6-132">Consultez [Détails de la tarification de la bande passante](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="c99e6-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="c99e6-133">Créer un réplica distant</span><span class="sxs-lookup"><span data-stu-id="c99e6-133">Create remote replica</span></span>

<span data-ttu-id="c99e6-134">Pour créer un réplica dans un centre de données distant, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c99e6-134">To create a replica in a remote data center, do the following steps:</span></span>

1. <span data-ttu-id="c99e6-135">[Créez un réseau virtuel dans la nouvelle région](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c99e6-135">[Create a virtual network in the new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="c99e6-136">[Configurez une connexion de réseau virtuel à réseau virtuel à l’aide du portail Azure](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c99e6-136">[Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="c99e6-137">Parfois, vous serez amené à utiliser PowerShell pour créer la connexion de réseau virtuel à réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c99e6-137">In some cases, you may have to use PowerShell to create the VNet-to-VNet connection.</span></span> <span data-ttu-id="c99e6-138">Par exemple, si vous utilisez différents comptes Azure, vous ne pouvez pas configurer la connexion dans le portail.</span><span class="sxs-lookup"><span data-stu-id="c99e6-138">For example, if you use different Azure accounts you cannot configure the connection in the portal.</span></span> <span data-ttu-id="c99e6-139">Dans ce cas, [configurez une connexion de réseau virtuel à réseau virtuel à l’aide du portail Azure](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c99e6-139">In this case see, [Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="c99e6-140">[Créez un contrôleur de domaine dans la nouvelle région](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="c99e6-140">[Create a domain controller in the new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="c99e6-141">Ce contrôleur de domaine assure l’authentification si le contrôleur de domaine dans le site principal n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="c99e6-141">This domain controller provides authentication if the domain controller in the primary site is not available.</span></span>

1. <span data-ttu-id="c99e6-142">[Créez une machine virtuelle SQL Server dans la nouvelle région](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="c99e6-142">[Create a SQL Server virtual machine in the new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="c99e6-143">[Créez un équilibrage de charge Azure dans le réseau sur la nouvelle région](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="c99e6-143">[Create an Azure load balancer in the network on the new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="c99e6-144">Cet équilibrage de charge doit :</span><span class="sxs-lookup"><span data-stu-id="c99e6-144">This load balancer must:</span></span>

   - <span data-ttu-id="c99e6-145">Être dans les mêmes réseau et sous-réseau que la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c99e6-145">Be in the same network and subnet as the new virtual machine.</span></span>
   - <span data-ttu-id="c99e6-146">Avoir une adresse IP statique pour l’écouteur du groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="c99e6-146">Have a static IP address for the availability group listener.</span></span>
   - <span data-ttu-id="c99e6-147">Inclure un pool principal comprenant uniquement des machines virtuelles situées dans la même région que l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="c99e6-147">Include a backend pool consisting of only the virtual machines in the same region as the load balancer.</span></span>
   - <span data-ttu-id="c99e6-148">Utiliser une sonde de port TCP propre à l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="c99e6-148">Use a TCP port probe specific to the IP address.</span></span>
   - <span data-ttu-id="c99e6-149">Avoir une règle d’équilibrage de charge propre à SQL Server dans la même région.</span><span class="sxs-lookup"><span data-stu-id="c99e6-149">Have a load balancing rule specific to the SQL Server in the same region.</span></span>  

1. <span data-ttu-id="c99e6-150">[Ajoutez la fonction de Clustering avec basculement au nouveau serveur SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="c99e6-150">[Add Failover Clustering feature to the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="c99e6-151">[Joignez le nouveau SQL Server au domaine](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="c99e6-151">[Join the new SQL Server to the domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="c99e6-152">[Configurez le nouveau compte de service SQL Server pour qu’il utilise un compte de domaine](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="c99e6-152">[Set the new SQL Server service account to use a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="c99e6-153">[Ajoutez le nouveau SQL Server au cluster de basculement Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="c99e6-153">[Add the new SQL Server to the Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="c99e6-154">Créez une ressource à adresse IP sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="c99e6-154">Create an IP address resource on the cluster.</span></span>

   <span data-ttu-id="c99e6-155">Vous pouvez créer la ressource à adresse IP dans le Gestionnaire du cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="c99e6-155">You can create the IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="c99e6-156">Cliquez avec le bouton droit sur le rôle du groupe de disponibilité, cliquez sur **Ajouter une ressource**, **More Resources (Plus de ressources)** puis **Adresse IP**.</span><span class="sxs-lookup"><span data-stu-id="c99e6-156">Right-click the availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![Création d’une adresse IP](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="c99e6-158">Configurez cette adresse IP comme suit :</span><span class="sxs-lookup"><span data-stu-id="c99e6-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="c99e6-159">Utilisez le réseau à partir du centre de données distant.</span><span class="sxs-lookup"><span data-stu-id="c99e6-159">Use the network from the remote data center.</span></span>
   - <span data-ttu-id="c99e6-160">Attribuez l’adresse IP à partir du nouvel équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="c99e6-160">Assign the IP address from the new Azure load balancer.</span></span> 

1. <span data-ttu-id="c99e6-161">Sur le nouveau SQL Server dans le Gestionnaire de configuration SQL Server, [activez les groupes de disponibilité AlwaysOn](http://msdn.microsoft.com/library/ff878259.aspx).</span><span class="sxs-lookup"><span data-stu-id="c99e6-161">On the new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="c99e6-162">[Ouvrez les ports de pare-feu sur le nouveau SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="c99e6-162">[Open firewall ports on the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="c99e6-163">Les numéros de port que vous devez ouvrir varient selon votre environnement.</span><span class="sxs-lookup"><span data-stu-id="c99e6-163">The port numbers you need to open depend on your environment.</span></span> <span data-ttu-id="c99e6-164">Ouvrez les ports du point de terminaison de la mise en miroir et de la sonde d’intégrité d’Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="c99e6-164">Open ports for the mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="c99e6-165">[Ajoutez un réplica au groupe de disponibilité sur le nouveau SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="c99e6-165">[Add a replica to the availability group on the new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="c99e6-166">Pour un réplica dans une région Azure distante, configurez-le pour une réplication asynchrone avec basculement manuel.</span><span class="sxs-lookup"><span data-stu-id="c99e6-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="c99e6-167">Ajoutez la ressource à adresse IP comme une dépendance du cluster (nom de réseau) du point d’accès au client écouteur.</span><span class="sxs-lookup"><span data-stu-id="c99e6-167">Add the IP address resource as a dependency for the listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="c99e6-168">La capture d’écran suivante illustre une ressource de cluster à adresse IP configurée correctement :</span><span class="sxs-lookup"><span data-stu-id="c99e6-168">The following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="c99e6-170">Le groupe de ressources de cluster inclut les deux adresses IP.</span><span class="sxs-lookup"><span data-stu-id="c99e6-170">The cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="c99e6-171">Ces deux adresses IP sont des dépendances du point d’accès au client écouteur.</span><span class="sxs-lookup"><span data-stu-id="c99e6-171">Both IP addresses are dependencies for the listener client access point.</span></span> <span data-ttu-id="c99e6-172">Utilisez l’opérateur **OR** dans la configuration de dépendance de cluster.</span><span class="sxs-lookup"><span data-stu-id="c99e6-172">Use the **OR** operator in the cluster dependency configuration.</span></span>

1. <span data-ttu-id="c99e6-173">[Définissez les paramètres de cluster dans PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="c99e6-173">[Set the cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="c99e6-174">Exécutez le script PowerShell avec le nom réseau du cluster, une adresse IP et un port de sonde que vous avez configurés sur l’équilibrage de charge dans la nouvelle région.</span><span class="sxs-lookup"><span data-stu-id="c99e6-174">Run the PowerShell script with the cluster network name, IP address, and probe port that you configured on the load balancer in the new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # The cluster name for the network in the new region (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "<IPResourceName>" # The cluster name for the new IP Address resource.
   $ILBIP = “<n.n.n.n>” # The IP Address of the Internal Load Balancer (ILB) in the new region. This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <nnnnn> # The probe port you set on the ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="c99e6-175">Configurer la connexion à plusieurs sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="c99e6-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="c99e6-176">Le réplica dans le centre de données distant fait partie du groupe de disponibilité, mais il se trouve dans un autre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="c99e6-176">The replica in the remote data center is part of the availability group but it is in a different subnet.</span></span> <span data-ttu-id="c99e6-177">Si ce réplica devient le réplica principal, la connexion d’application peut être perturbée.</span><span class="sxs-lookup"><span data-stu-id="c99e6-177">If this replica becomes the primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="c99e6-178">Ce comportement est identique à un groupe de disponibilité local dans un déploiement de plusieurs sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="c99e6-178">This behavior is the same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="c99e6-179">Pour autoriser les connexions des applications clientes, mettez à jour la connexion cliente ou configurez la mise en cache de la résolution du nom sur la ressource de nom de réseau de cluster.</span><span class="sxs-lookup"><span data-stu-id="c99e6-179">To allow connections from client applications, either update the client connection or configure name resolution caching on the cluster network name resource.</span></span>

<span data-ttu-id="c99e6-180">Idéalement, mettez à jour les chaînes de connexion au client pour qu’elles indiquent `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="c99e6-180">Preferably, update the client connection strings to set `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="c99e6-181">Consultez [Connexion à MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="c99e6-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="c99e6-182">Si vous ne pouvez pas modifier les chaînes de connexion, vous pouvez configurer la mise en cache de la résolution des noms.</span><span class="sxs-lookup"><span data-stu-id="c99e6-182">If you cannot modify the connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="c99e6-183">Consultez [Connection Timeouts in Multi-subnet Availability Group (Délais d’expiration de la connexion dans le groupe de disponibilité de plusieurs sous-réseaux)](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span><span class="sxs-lookup"><span data-stu-id="c99e6-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-to-remote-region"></a><span data-ttu-id="c99e6-184">Basculer vers la région distante</span><span class="sxs-lookup"><span data-stu-id="c99e6-184">Fail over to remote region</span></span>

<span data-ttu-id="c99e6-185">Pour tester la connectivité de l’écouteur à la région distante, vous pouvez basculer le réplica vers la région distante.</span><span class="sxs-lookup"><span data-stu-id="c99e6-185">To test listener connectivity to the remote region, you can fail over the replica to the remote region.</span></span> <span data-ttu-id="c99e6-186">Si le réplica est asynchrone, le basculement est vulnérable à la perte potentielle de données.</span><span class="sxs-lookup"><span data-stu-id="c99e6-186">While the replica is asynchronous, failover is vulnerable to potential data loss.</span></span> <span data-ttu-id="c99e6-187">Pour effectuer un basculement sans perte de données, modifiez le mode de disponibilité en synchrone et définissez le mode de basculement automatique.</span><span class="sxs-lookup"><span data-stu-id="c99e6-187">To fail over without data loss, change the availability mode to synchronous and set the failover mode to automatic.</span></span> <span data-ttu-id="c99e6-188">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c99e6-188">Use the following steps:</span></span>

1. <span data-ttu-id="c99e6-189">Dans l’**Explorateur d’objets**, connectez-vous à l’instance de SQL Server qui héberge le réplica principal.</span><span class="sxs-lookup"><span data-stu-id="c99e6-189">In **Object Explorer**, connect to the instance of SQL Server that hosts the primary replica.</span></span>
1. <span data-ttu-id="c99e6-190">Sous **Groupes de disponibilité AlwaysOn**, **Groupes de disponibilité**, cliquez avec le bouton droit sur votre groupe de disponibilité, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="c99e6-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="c99e6-191">Dans la page **Général**, sous **Réplicas de disponibilité**, configurez le réplica secondaire dans le site de récupération d’urgence pour qu’il utilise le mode de disponibilité **Validation synchrone** et le mode de basculement **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="c99e6-191">On the **General** page, under **Availability Replicas**, set the secondary replica in the DR site to use **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="c99e6-192">Si vous avez un réplica secondaire dans le même site que le réplica principal pour la haute disponibilité, configurez ce réplica en **Validation asynchrone** et **Manuel**.</span><span class="sxs-lookup"><span data-stu-id="c99e6-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica to **Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="c99e6-193">Cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="c99e6-193">Click OK.</span></span>
1. <span data-ttu-id="c99e6-194">Dans l’**Explorateur d’objets**, cliquez sur le groupe de disponibilité puis sur **Afficher le tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="c99e6-194">In **Object Explorer**, right-click the availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="c99e6-195">Dans le tableau de bord, vérifiez que le réplica sur le site de récupération d’urgence est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="c99e6-195">On the dashboard, verify that the replica on the DR site is synchronized.</span></span>
1. <span data-ttu-id="c99e6-196">Dans l’**Explorateur d’objets**, cliquez sur le groupe de disponibilité puis sur **Basculer...**.</span><span class="sxs-lookup"><span data-stu-id="c99e6-196">In **Object Explorer**, right-click the availability group, and click **Failover...**.</span></span> <span data-ttu-id="c99e6-197">SQL Server Management Studio ouvre un assistant pour effectuer le basculement vers SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c99e6-197">SQL Server Management Studios opens a wizard to fail over SQL Server.</span></span>  
1. <span data-ttu-id="c99e6-198">Cliquez sur **Suivant** et sélectionnez l’instance de SQL Server sur le site de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="c99e6-198">Click **Next**, and select the SQL Server instance in the DR site.</span></span> <span data-ttu-id="c99e6-199">Cliquez à nouveau sur **Suivant** .</span><span class="sxs-lookup"><span data-stu-id="c99e6-199">Click **Next** again.</span></span>
1. <span data-ttu-id="c99e6-200">Connectez-vous à l’instance de SQL Server sur le site de récupération d’urgence et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c99e6-200">Connect to the SQL Server instance in the DR site and click **Next**.</span></span>
1. <span data-ttu-id="c99e6-201">Dans la page **Synthèse**, vérifiez les paramètres et cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="c99e6-201">On the **Summary** page, verify the settings and click **Finish**.</span></span>

<span data-ttu-id="c99e6-202">Après avoir testé la connectivité, replacez le réplica principal dans votre centre de données principal et rétablissez les paramètres de fonctionnement normaux du mode de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="c99e6-202">After testing connectivity, move the primary replica back to your primary data center and set the availability mode back to their normal operating settings.</span></span> <span data-ttu-id="c99e6-203">Le tableau suivant présente les paramètres de fonctionnement normaux de l’architecture décrite dans ce document :</span><span class="sxs-lookup"><span data-stu-id="c99e6-203">The following table shows the normal operational settings for the architecture described in this document:</span></span>

| <span data-ttu-id="c99e6-204">Emplacement</span><span class="sxs-lookup"><span data-stu-id="c99e6-204">Location</span></span> | <span data-ttu-id="c99e6-205">Instance de serveur</span><span class="sxs-lookup"><span data-stu-id="c99e6-205">Server Instance</span></span> | <span data-ttu-id="c99e6-206">Rôle</span><span class="sxs-lookup"><span data-stu-id="c99e6-206">Role</span></span> | <span data-ttu-id="c99e6-207">Mode de disponibilité</span><span class="sxs-lookup"><span data-stu-id="c99e6-207">Availability Mode</span></span> | <span data-ttu-id="c99e6-208">Mode de basculement</span><span class="sxs-lookup"><span data-stu-id="c99e6-208">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="c99e6-209">Centre de données principal</span><span class="sxs-lookup"><span data-stu-id="c99e6-209">Primary data center</span></span> | <span data-ttu-id="c99e6-210">SQL-1</span><span class="sxs-lookup"><span data-stu-id="c99e6-210">SQL-1</span></span> | <span data-ttu-id="c99e6-211">Primaire</span><span class="sxs-lookup"><span data-stu-id="c99e6-211">Primary</span></span> | <span data-ttu-id="c99e6-212">Synchrone</span><span class="sxs-lookup"><span data-stu-id="c99e6-212">Synchronous</span></span> | <span data-ttu-id="c99e6-213">Automatique</span><span class="sxs-lookup"><span data-stu-id="c99e6-213">Automatic</span></span>
| <span data-ttu-id="c99e6-214">Centre de données principal</span><span class="sxs-lookup"><span data-stu-id="c99e6-214">Primary data center</span></span> | <span data-ttu-id="c99e6-215">SQL-2</span><span class="sxs-lookup"><span data-stu-id="c99e6-215">SQL-2</span></span> | <span data-ttu-id="c99e6-216">Secondaire</span><span class="sxs-lookup"><span data-stu-id="c99e6-216">Secondary</span></span> | <span data-ttu-id="c99e6-217">Synchrone</span><span class="sxs-lookup"><span data-stu-id="c99e6-217">Synchronous</span></span> | <span data-ttu-id="c99e6-218">Automatique</span><span class="sxs-lookup"><span data-stu-id="c99e6-218">Automatic</span></span>
| <span data-ttu-id="c99e6-219">Centre de données secondaire ou distant</span><span class="sxs-lookup"><span data-stu-id="c99e6-219">Secondary or remote data center</span></span> | <span data-ttu-id="c99e6-220">SQL-3</span><span class="sxs-lookup"><span data-stu-id="c99e6-220">SQL-3</span></span> | <span data-ttu-id="c99e6-221">Secondaire</span><span class="sxs-lookup"><span data-stu-id="c99e6-221">Secondary</span></span> | <span data-ttu-id="c99e6-222">Asynchrone</span><span class="sxs-lookup"><span data-stu-id="c99e6-222">Asynchronous</span></span> | <span data-ttu-id="c99e6-223">Manuel</span><span class="sxs-lookup"><span data-stu-id="c99e6-223">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="c99e6-224">Plus d’informations sur le basculement manuel forcé et planifié</span><span class="sxs-lookup"><span data-stu-id="c99e6-224">More information about planned and forced manual failover</span></span>

<span data-ttu-id="c99e6-225">Pour plus d’informations, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="c99e6-225">For more information, see the following topics:</span></span>

- [<span data-ttu-id="c99e6-226">Effectuer un basculement manuel planifié d'un groupe de disponibilité (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="c99e6-226">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="c99e6-227">Effectuer un basculement manuel forcé d'un groupe de disponibilité (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="c99e6-227">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="c99e6-228">Liens supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c99e6-228">Additional Links</span></span>

* [<span data-ttu-id="c99e6-229">Groupes de disponibilité AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="c99e6-229">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="c99e6-230">Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="c99e6-230">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="c99e6-231">Équilibrages de charge Azure</span><span class="sxs-lookup"><span data-stu-id="c99e6-231">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="c99e6-232">Groupes à haute disponibilité Azure</span><span class="sxs-lookup"><span data-stu-id="c99e6-232">Azure Availability Sets</span></span>](../manage-availability.md)
