---
title: "Configuration de l'équilibrage de charge pour SQL Always On | Microsoft Docs"
description: "Configuration de l'équilibrage de charge pour fonctionner avec SQL Alway On et procédure d’exploitation de Powershell pour créer l'équilibrage de charge pour l'implémentation de SQL"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 68aad6253f185d53fdd7f11c8660c7287ef12655
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="809c2-103">Configuration de l'équilibrage de charge pour SQL Always On</span><span class="sxs-lookup"><span data-stu-id="809c2-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="809c2-104">Les groupes de disponibilité Always On de SQL Server peuvent maintenant être exécutés avec l’équilibrage de charge interne (ILB).</span><span class="sxs-lookup"><span data-stu-id="809c2-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="809c2-105">Le groupe de disponibilité constitue la solution phare de SQL Server pour une haute disponibilité et la récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="809c2-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="809c2-106">L’écouteur du groupe de disponibilité permet aux applications clientes de se connecter en toute transparence au réplica principal, quel que soit le nombre de réplicas dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="809c2-106">The Availability Group Listener allows client applications to seamlessly connect to the primary replica, irrespective of the number of the replicas in the configuration.</span></span>

<span data-ttu-id="809c2-107">Le nom (DNS) de l'écouteur est mappé vers une adresse IP de l’équilibrage de charge et l’équilibrage de charge Azure dirige le trafic entrant vers le serveur principal du jeu de réplicas uniquement.</span><span class="sxs-lookup"><span data-stu-id="809c2-107">The listener (DNS) name is mapped to a load-balanced IP address and Azure's load balancer directs the incoming traffic to only the primary server in the replica set.</span></span>

<span data-ttu-id="809c2-108">Vous pouvez utiliser le support de l'équilibrage de charge pour les points de terminaison (écouteur) de SQL Server AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="809c2-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="809c2-109">Vous avez désormais un contrôle sur l'accessibilité de l'écouteur et vous pouvez choisir l'adresse IP de l’équilibrage de charge à partir d'un sous-réseau spécifique dans votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="809c2-109">You now have control over the accessibility of the listener and can choose the load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="809c2-110">À l'aide de l'ILB sur l'écouteur, le point de terminaison du serveur SQL (par exemple, Server=tcp:ListenerName,1433;Database=DatabaseName) est accessible uniquement via :</span><span class="sxs-lookup"><span data-stu-id="809c2-110">By using ILB on the listener, the SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="809c2-111">Services et machines virtuelles dans le même réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="809c2-111">Services and VMs in the same Virtual network</span></span>
* <span data-ttu-id="809c2-112">Services et machines virtuelles d’un réseau local connecté</span><span class="sxs-lookup"><span data-stu-id="809c2-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="809c2-113">Services et machines virtuelles de réseaux virtuels interconnectés</span><span class="sxs-lookup"><span data-stu-id="809c2-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="809c2-115">Figure 1 : SQL AlwaysOn configuré avec équilibrage de charge côté Internet</span><span class="sxs-lookup"><span data-stu-id="809c2-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-to-the-service"></a><span data-ttu-id="809c2-116">Ajout d’un équilibrage de charge interne au service</span><span class="sxs-lookup"><span data-stu-id="809c2-116">Add Internal Load Balancer to the service</span></span>

1. <span data-ttu-id="809c2-117">Dans l’exemple suivant, nous allons configurer un réseau virtuel contenant un sous-réseau nommé 'Sous-réseau 1' :</span><span class="sxs-lookup"><span data-stu-id="809c2-117">In the following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="809c2-118">Ajout des points de terminaison avec une charge équilibrée pour l'ILB sur chaque machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="809c2-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="809c2-119">Dans l'exemple ci-dessus, la machine virtuelle 2 est appelée « sqlsvc1 » et « sqlsvc2 » en cours d'exécution dans le service de cloud « Sqlsvc ».</span><span class="sxs-lookup"><span data-stu-id="809c2-119">In the example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in the cloud service "Sqlsvc".</span></span> <span data-ttu-id="809c2-120">Après avoir créé l’ILB avec le commutateur `DirectServerReturn`, vous ajoutez à l’ILB des points de terminaison à charge équilibrée pour permettre à SQL de configurer les écouteurs pour les groupes de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="809c2-120">After creating the ILB with `DirectServerReturn` switch, you add load balanced endpoints to the ILB to allow SQL to configure the listeners for the availability groups.</span></span>

<span data-ttu-id="809c2-121">Pour plus d’informations sur SQL AlwaysOn, voir [Configurer un équilibrage de charge interne pour un groupe de disponibilité AlwaysOn dans Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="809c2-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="809c2-122">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="809c2-122">See Also</span></span>
[<span data-ttu-id="809c2-123">Prise en main de la configuration d’un équilibrage de charge sur Internet</span><span class="sxs-lookup"><span data-stu-id="809c2-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="809c2-124">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="809c2-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="809c2-125">Configuration d’un mode de distribution d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="809c2-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="809c2-126">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="809c2-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
