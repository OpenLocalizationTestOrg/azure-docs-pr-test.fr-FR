---
title: "équilibrage de charge aaaConfigure pour SQL always on | Documents Microsoft"
description: "Configurer toowork d’équilibrage de charge avec SQL toujours sur et comment tooleverage powershell toocreate l’équilibrage de charge pour l’implémentation de SQL hello"
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
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="d5236-103">Configuration de l'équilibrage de charge pour SQL Always On</span><span class="sxs-lookup"><span data-stu-id="d5236-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="d5236-104">Les groupes de disponibilité Always On de SQL Server peuvent maintenant être exécutés avec l’équilibrage de charge interne (ILB).</span><span class="sxs-lookup"><span data-stu-id="d5236-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="d5236-105">Le groupe de disponibilité constitue la solution phare de SQL Server pour une haute disponibilité et la récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="d5236-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="d5236-106">Hello écouteur du groupe de disponibilité permet aux applications clientes tooseamlessly connecter toohello réplica principal, quel que soit le nombre de hello de réplicas hello dans la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="d5236-106">hello Availability Group Listener allows client applications tooseamlessly connect toohello primary replica, irrespective of hello number of hello replicas in hello configuration.</span></span>

<span data-ttu-id="d5236-107">nom de l’écouteur (DNS) Hello est adresse tooa mappé avec équilibrage de charge et équilibrage de charge de Azure dirige le serveur principal de hello entrants trafic tooonly hello dans le jeu de réplicas hello.</span><span class="sxs-lookup"><span data-stu-id="d5236-107">hello listener (DNS) name is mapped tooa load-balanced IP address and Azure's load balancer directs hello incoming traffic tooonly hello primary server in hello replica set.</span></span>

<span data-ttu-id="d5236-108">Vous pouvez utiliser le support de l'équilibrage de charge pour les points de terminaison (écouteur) de SQL Server AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="d5236-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="d5236-109">Maintenant, vous contrôlez accessibilité hello d’écouteur de hello et que vous pouvez choisir l’adresse IP de charge équilibrée hello à partir d’un sous-réseau spécifique dans votre réseau virtuel (VNet).</span><span class="sxs-lookup"><span data-stu-id="d5236-109">You now have control over hello accessibility of hello listener and can choose hello load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="d5236-110">En utilisant l’équilibrage de charge interne sur le port d’écoute hello, hello le point de terminaison SQL server (par exemple, Server = tcp:ListenerName, 1433 ; base de données = DatabaseName) est accessible uniquement par :</span><span class="sxs-lookup"><span data-stu-id="d5236-110">By using ILB on hello listener, hello SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="d5236-111">Services et machines virtuelles dans hello même réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="d5236-111">Services and VMs in hello same Virtual network</span></span>
* <span data-ttu-id="d5236-112">Services et machines virtuelles d’un réseau local connecté</span><span class="sxs-lookup"><span data-stu-id="d5236-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="d5236-113">Services et machines virtuelles de réseaux virtuels interconnectés</span><span class="sxs-lookup"><span data-stu-id="d5236-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="d5236-115">Figure 1 : SQL AlwaysOn configuré avec équilibrage de charge côté Internet</span><span class="sxs-lookup"><span data-stu-id="d5236-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-toohello-service"></a><span data-ttu-id="d5236-116">Ajouter un service de toohello d’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="d5236-116">Add Internal Load Balancer toohello service</span></span>

1. <span data-ttu-id="d5236-117">Bonjour l’exemple suivant, nous configure un réseau virtuel qui contient un sous-réseau nommé 'Sous-réseau-1' :</span><span class="sxs-lookup"><span data-stu-id="d5236-117">In hello following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="d5236-118">Ajout des points de terminaison avec une charge équilibrée pour l'ILB sur chaque machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d5236-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="d5236-119">Dans l’exemple hello ci-dessus, vous avez appelé « sqlsvc1 » et « sqlsvc2 » en cours d’exécution de la machine 2 virtuelle dans le cloud de hello de service « Sqlsvc ».</span><span class="sxs-lookup"><span data-stu-id="d5236-119">In hello example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in hello cloud service "Sqlsvc".</span></span> <span data-ttu-id="d5236-120">Après la création d’hello avec équilibrage de charge interne `DirectServerReturn` commutateur, vous ajoutez des points de terminaison à charge équilibrée toohello équilibrage de charge interne tooallow SQL tooconfigure hello écouteurs de groupes de disponibilité hello de charge.</span><span class="sxs-lookup"><span data-stu-id="d5236-120">After creating hello ILB with `DirectServerReturn` switch, you add load balanced endpoints toohello ILB tooallow SQL tooconfigure hello listeners for hello availability groups.</span></span>

<span data-ttu-id="d5236-121">Pour plus d’informations sur SQL AlwaysOn, voir [Configurer un équilibrage de charge interne pour un groupe de disponibilité AlwaysOn dans Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="d5236-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d5236-122">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d5236-122">See Also</span></span>
[<span data-ttu-id="d5236-123">Prise en main de la configuration d’un équilibrage de charge sur Internet</span><span class="sxs-lookup"><span data-stu-id="d5236-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="d5236-124">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="d5236-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="d5236-125">Configuration d’un mode de distribution d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="d5236-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d5236-126">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="d5236-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
