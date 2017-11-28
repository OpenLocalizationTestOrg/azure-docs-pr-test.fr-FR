---
title: "Présentation de l’équilibrage de charge interne | Microsoft Docs"
description: "Vue d'ensemble de l'équilibrage de charge interne et de ses fonctionnalités. Procédure de fonctionnement de l'équilibrage de charge pour Azure et les scénarios de configuration possibles des points de terminaison internes"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d324aaf8ec2c8766d5cf11452158d14c19cba4d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="73fb2-103">Présentation de l’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="73fb2-103">Internal load balancer overview</span></span>

<span data-ttu-id="73fb2-104">Contrairement à l’équilibreur de charge avec accès par Internet, l’équilibreur de charge interne (ILB) dirige le trafic uniquement vers les ressources au sein du service cloud ou via le VPN pour accéder à l’infrastructure Azure.</span><span class="sxs-lookup"><span data-stu-id="73fb2-104">Unlike the Internet facing load balancer, the internal load balancer (ILB) directs traffic only to resources inside the cloud service or using VPN to access the Azure infrastructure.</span></span> <span data-ttu-id="73fb2-105">L’infrastructure limite l’accès aux adresses IP virtuelles à charge équilibrée d’un service cloud ou d’un réseau virtuel. Ainsi, elles ne seront jamais exposées directement à un point de terminaison Internet.</span><span class="sxs-lookup"><span data-stu-id="73fb2-105">The infrastructure restricts access to the load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed to an Internet endpoint.</span></span> <span data-ttu-id="73fb2-106">Cela permet aux applications cœur de métier (LOB) internes de s’exécuter dans Azure et d’être accessibles depuis le cloud ou à partir de ressources locales.</span><span class="sxs-lookup"><span data-stu-id="73fb2-106">This enables internal line of business (LOB) applications to run in Azure and be accessed from within the cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="73fb2-107">Pourquoi utiliser un équilibreur de charge interne</span><span class="sxs-lookup"><span data-stu-id="73fb2-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="73fb2-108">L’équilibrage de charge interne (ILB) d’Azure fournit un équilibrage de charge entre les machines virtuelles qui résident dans un service cloud ou un réseau virtuel avec une portée régionale.</span><span class="sxs-lookup"><span data-stu-id="73fb2-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="73fb2-109">Pour plus d'informations sur l'utilisation et la configuration des réseaux virtuels avec une portée régionale, consultez [Réseaux virtuels régionaux](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) sur le blog Azure.</span><span class="sxs-lookup"><span data-stu-id="73fb2-109">For information about the use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in the Azure blog.</span></span> <span data-ttu-id="73fb2-110">Les réseaux virtuels existants qui ont été configurés pour un groupe d'affinités ne peuvent pas utiliser l'ILB.</span><span class="sxs-lookup"><span data-stu-id="73fb2-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="73fb2-111">L’ILB permet d’effectuer les types d'équilibrage de charge suivants :</span><span class="sxs-lookup"><span data-stu-id="73fb2-111">ILB enables the following types of load balancing:</span></span>

* <span data-ttu-id="73fb2-112">Dans un service cloud, des machines virtuelles à un ensemble de machines virtuelles qui résident dans le même service cloud (voir Figure 1).</span><span class="sxs-lookup"><span data-stu-id="73fb2-112">Within a cloud service, from virtual machines to a set of virtual machines that reside within the same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="73fb2-113">Dans un réseau virtuel, des machines virtuelles dans le réseau virtuel à un ensemble de machines virtuelles qui résident dans le même service cloud du réseau virtuel (voir Figure 2).</span><span class="sxs-lookup"><span data-stu-id="73fb2-113">Within a virtual network, from virtual machines in the virtual network to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 2).</span></span>
* <span data-ttu-id="73fb2-114">Dans un réseau virtuel entre différents locaux, des ordinateurs locaux à un ensemble de machines virtuelles qui résident dans le même service cloud du réseau virtuel (voir Figure 3).</span><span class="sxs-lookup"><span data-stu-id="73fb2-114">For a cross-premises virtual network, from on-premises computers to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 3).</span></span>
* <span data-ttu-id="73fb2-115">Les applications multiniveau sur internet pour lesquelles les principaux niveaux ne sont pas sur internet mais nécessitent un équilibrage de charge pour le trafic depuis le niveau sur internet.</span><span class="sxs-lookup"><span data-stu-id="73fb2-115">Internet-facing, multi-tier applications in which the back-end tiers are not Internet-facing but require load balancing for traffic from the Internet-facing tier.</span></span>
* <span data-ttu-id="73fb2-116">Équilibrer la charge pour des applications métier (LOB) hébergées dans Azure, sans matériel ou logiciel d'équilibrage de charge supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="73fb2-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="73fb2-117">Y compris les serveurs locaux d'un ensemble d'ordinateurs dont la charge du trafic est équilibrée.</span><span class="sxs-lookup"><span data-stu-id="73fb2-117">Including on-premises servers in the set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="73fb2-118">Une application multiniveau sur internet</span><span class="sxs-lookup"><span data-stu-id="73fb2-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="73fb2-119">La couche web a des points de terminaison sur Internet pour les clients Internet et fait partie d'un jeu d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="73fb2-119">The web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="73fb2-120">L'équilibrage de charge répartit le trafic entrant à partir des clients web pour le port TCP 443 (HTTPS) pour les serveurs web.</span><span class="sxs-lookup"><span data-stu-id="73fb2-120">The load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) to the web servers.</span></span>

<span data-ttu-id="73fb2-121">Les serveurs de base de données sont situés derrière un point de terminaison d'ILB utilisé par les serveurs web pour le stockage.</span><span class="sxs-lookup"><span data-stu-id="73fb2-121">The database servers are behind an ILB endpoint which the web servers use for storage.</span></span> <span data-ttu-id="73fb2-122">Cette base de données dispose d’un point de terminaison d’équilibrage de charge dont la charge du trafic est équilibrée entre les serveurs de base de données dans le jeu d'ILB.</span><span class="sxs-lookup"><span data-stu-id="73fb2-122">This database service load balanced endpoint, which traffic is load balanced across the database servers in the ILB set.</span></span>

<span data-ttu-id="73fb2-123">L'image suivante présente l’application multiniveau sur Internet dans le même service cloud.</span><span class="sxs-lookup"><span data-stu-id="73fb2-123">The following image shows the Internet facing multi-tier application within the same cloud service.</span></span>

![Service cloud unique d'équilibrage de charge interne](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="73fb2-125">Illustration 1 - Application multi-niveau sur Internet</span><span class="sxs-lookup"><span data-stu-id="73fb2-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="73fb2-126">Une autre utilisation possible pour une application multiniveau se présente lorsqu’une ILB est déployée dans un service cloud différent de celui consommant le service pour l'ILB.</span><span class="sxs-lookup"><span data-stu-id="73fb2-126">Another possible use for a multi-tier application is when the ILB deployed to a different cloud service than the one consuming the service for the ILB.</span></span>

<span data-ttu-id="73fb2-127">Les services cloud qui utilisent le même réseau virtuel auront accès au point de terminaison de l'ILB.</span><span class="sxs-lookup"><span data-stu-id="73fb2-127">Cloud services using the same virtual network will have access to the ILB endpoint.</span></span> <span data-ttu-id="73fb2-128">L’image suivante présente des serveurs web frontaux qui se trouvent dans un autre service cloud que la base de données principale et utilisent le point de terminaison d’ILB dans le même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="73fb2-128">The following image shows front-end web servers are in a different cloud service from the database back-end and using the ILB endpoint within the same virtual network.</span></span>

![Équilibrage de charge interne entre les services cloud](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="73fb2-130">Figure 2 : serveurs frontaux dans un service cloud différent</span><span class="sxs-lookup"><span data-stu-id="73fb2-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="73fb2-131">Applications cœur de métier (LOB) Intranet</span><span class="sxs-lookup"><span data-stu-id="73fb2-131">Intranet line of business applications</span></span>

<span data-ttu-id="73fb2-132">Le trafic des clients sur le réseau local obtient un équilibrage de charge sur l'ensemble des serveurs cœur de métier à l'aide de la connexion VPN au réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="73fb2-132">Traffic from clients on the on-premises network get load-balanced across the set of LOB servers using VPN connection to Azure network.</span></span>

<span data-ttu-id="73fb2-133">L’ordinateur client aura accès à une adresse IP du service VPN Azure à l’aide d’un VPN point à site.</span><span class="sxs-lookup"><span data-stu-id="73fb2-133">The client machine will have access to an IP address from Azure VPN service using point to site VPN.</span></span> <span data-ttu-id="73fb2-134">Il permet l’utilisation de l’application de cœur de métier (LOB) hébergée derrière le point de terminaison d’équilibrage de charge interne (ILB).</span><span class="sxs-lookup"><span data-stu-id="73fb2-134">It allows the use the LOB application hosted behind the ILB endpoint.</span></span>

![Équilibrage de charge interne utilisant le VPN de point à site](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="73fb2-136">Figure 3 : applications de cœur de métier (LOB) hébergées derrière le point de terminaison d’équilibrage de charge (ILB)</span><span class="sxs-lookup"><span data-stu-id="73fb2-136">Figure 3 - LOB applications hosted behind the LB endpoint</span></span>

<span data-ttu-id="73fb2-137">Un autre scénario pour le système cœur de métier est d'avoir un VPN de site à site sur le réseau virtuel dans lequel le point de terminaison de l’ILB est configuré.</span><span class="sxs-lookup"><span data-stu-id="73fb2-137">Another scenario for the LOB is to have a site to site VPN to the virtual network where the ILB endpoint is configured.</span></span> <span data-ttu-id="73fb2-138">Cela permet au trafic du réseau local d’être acheminé vers le point de terminaison d’équilibrage de charge interne (ILB).</span><span class="sxs-lookup"><span data-stu-id="73fb2-138">This allows on-premises network traffic to be routed to the ILB endpoint.</span></span>

![Équilibrage de charge interne utilisant le VPN de site à site](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="73fb2-140">Figure 4 : trafic du réseau local acheminé vers le point de terminaison d’équilibrage de charge interne (ILB)</span><span class="sxs-lookup"><span data-stu-id="73fb2-140">Figure 4 - On-premises network traffic routed to the ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="73fb2-141">Limitations</span><span class="sxs-lookup"><span data-stu-id="73fb2-141">Limitations</span></span>

<span data-ttu-id="73fb2-142">Les configurations d’équilibrage de charge internes ne prennent pas en charge SNAT.</span><span class="sxs-lookup"><span data-stu-id="73fb2-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="73fb2-143">Dans le cadre de ce document, SNAT fait référence à la traduction d’adresses réseau sources en masquant des ports.</span><span class="sxs-lookup"><span data-stu-id="73fb2-143">In the context of this document, SNAT refers to port masquerading source  network address translation.</span></span>  <span data-ttu-id="73fb2-144">Cela s’applique aux scénarios où une machine virtuelle dans un pool d’équilibrage de charge doit atteindre l’adresse PI frontale de son équilibreur de charge interne respectif.</span><span class="sxs-lookup"><span data-stu-id="73fb2-144">This applies to scenarios where a VM in a load balancer pool needs to reach the respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="73fb2-145">Ce scénario n’est pas pris en charge pour l’équilibreur de charge interne.</span><span class="sxs-lookup"><span data-stu-id="73fb2-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="73fb2-146">Des problèmes de connexion surviennent lorsque le flux est à charge équilibrée pour la machine virtuelle à l’origine du flux.</span><span class="sxs-lookup"><span data-stu-id="73fb2-146">Connection failures will occur when the flow is load balanced to the VM which originated the flow.</span></span> <span data-ttu-id="73fb2-147">Vous devez utiliser un équilibreur de charge de type proxy pour de tels scénarios.</span><span class="sxs-lookup"><span data-stu-id="73fb2-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73fb2-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="73fb2-148">Next Steps</span></span>

[<span data-ttu-id="73fb2-149">Prise en charge d'Azure Resource Manager pour l'équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="73fb2-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="73fb2-150">Prise en main de la configuration d’un équilibrage de charge sur Internet</span><span class="sxs-lookup"><span data-stu-id="73fb2-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="73fb2-151">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="73fb2-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="73fb2-152">Configuration d’un mode de distribution d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="73fb2-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="73fb2-153">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="73fb2-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
