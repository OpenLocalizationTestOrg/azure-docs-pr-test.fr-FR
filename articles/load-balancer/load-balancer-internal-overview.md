---
title: "équilibrage de charge aaaInternal vue d’ensemble | Documents Microsoft"
description: "Vue d’ensemble de l’équilibreur de charge interne et de ses fonctionnalités. Fonctionne d’un équilibrage de charge pour les points de terminaison internes des scénarios possibles et Azure tooconfigure"
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
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="c9597-103">Présentation de l’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="c9597-103">Internal load balancer overview</span></span>

<span data-ttu-id="c9597-104">Contrairement aux hello Internet exposés à équilibrage de charge, équilibreur de charge interne hello (équilibrage de charge interne) dirige le trafic tooresources uniquement à l’intérieur du service de cloud computing hello ou à l’aide de VPN tooaccess hello infrastructure Azure.</span><span class="sxs-lookup"><span data-stu-id="c9597-104">Unlike hello Internet facing load balancer, hello internal load balancer (ILB) directs traffic only tooresources inside hello cloud service or using VPN tooaccess hello Azure infrastructure.</span></span> <span data-ttu-id="c9597-105">infrastructure de Hello restreint l’accès toohello à charge équilibrée adresses IP virtuelles (VIP) d’un Service Cloud ou d’un réseau virtuel afin qu’ils ne seront jamais directement exposé tooan Internet point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="c9597-105">hello infrastructure restricts access toohello load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed tooan Internet endpoint.</span></span> <span data-ttu-id="c9597-106">Cela permet la ligne interne de toorun d’applications métier (LOB) dans Azure et accessible à partir de dans le cloud de hello ou à partir des ressources locales.</span><span class="sxs-lookup"><span data-stu-id="c9597-106">This enables internal line of business (LOB) applications toorun in Azure and be accessed from within hello cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="c9597-107">Pourquoi utiliser un équilibreur de charge interne</span><span class="sxs-lookup"><span data-stu-id="c9597-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="c9597-108">L’équilibrage de charge interne (ILB) d’Azure fournit un équilibrage de charge entre les machines virtuelles qui résident dans un service cloud ou un réseau virtuel avec une portée régionale.</span><span class="sxs-lookup"><span data-stu-id="c9597-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="c9597-109">Pour plus d’informations sur l’utilisation de hello et la configuration de réseaux virtuels avec une portée régionale, consultez [des réseaux virtuels régionaux](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) Bonjour blog Azure.</span><span class="sxs-lookup"><span data-stu-id="c9597-109">For information about hello use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure blog.</span></span> <span data-ttu-id="c9597-110">Les réseaux virtuels existants qui ont été configurés pour un groupe d'affinités ne peuvent pas utiliser l'ILB.</span><span class="sxs-lookup"><span data-stu-id="c9597-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="c9597-111">Équilibrage de charge interne permet hello les types d’équilibrage de charge suivants :</span><span class="sxs-lookup"><span data-stu-id="c9597-111">ILB enables hello following types of load balancing:</span></span>

* <span data-ttu-id="c9597-112">Dans un service cloud, à partir de l’ensemble de tooa de machines virtuelles des machines virtuelles qui résident dans hello même service cloud (voir Figure 1).</span><span class="sxs-lookup"><span data-stu-id="c9597-112">Within a cloud service, from virtual machines tooa set of virtual machines that reside within hello same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="c9597-113">Dans un réseau virtuel, à partir d’ordinateurs virtuels dans le jeu de tooa de réseau virtuel hello des machines virtuelles qui résident dans hello même service cloud de hello virtuel réseau (voir Figure 2).</span><span class="sxs-lookup"><span data-stu-id="c9597-113">Within a virtual network, from virtual machines in hello virtual network tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 2).</span></span>
* <span data-ttu-id="c9597-114">Pour un réseau virtuel intersite, à partir de l’ensemble de tooa d’ordinateurs locaux des machines virtuelles qui résident dans hello même service cloud de hello virtuel réseau (voir Figure 3).</span><span class="sxs-lookup"><span data-stu-id="c9597-114">For a cross-premises virtual network, from on-premises computers tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 3).</span></span>
* <span data-ttu-id="c9597-115">Les applications accessibles sur Internet, à plusieurs niveaux dans lequel les couches principales de hello ne sont pas exposés à Internet mais nécessitent équilibrage de charge pour le trafic à partir de la couche de hello sur Internet.</span><span class="sxs-lookup"><span data-stu-id="c9597-115">Internet-facing, multi-tier applications in which hello back-end tiers are not Internet-facing but require load balancing for traffic from hello Internet-facing tier.</span></span>
* <span data-ttu-id="c9597-116">Équilibrer la charge pour des applications métier (LOB) hébergées dans Azure, sans matériel ou logiciel d'équilibrage de charge supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="c9597-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="c9597-117">Inclure des serveurs locaux jeu hello d’ordinateurs dont le trafic est à charge équilibrée.</span><span class="sxs-lookup"><span data-stu-id="c9597-117">Including on-premises servers in hello set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="c9597-118">Une application multiniveau sur internet</span><span class="sxs-lookup"><span data-stu-id="c9597-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="c9597-119">niveau de Hello web possède des points de terminaison exposés à Internet pour les clients Internet et fait partie d’un jeu d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="c9597-119">hello web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="c9597-120">équilibrage de charge Hello distribue le trafic entrant à partir des clients web pour les serveurs web TCP port 443 (HTTPS) toohello.</span><span class="sxs-lookup"><span data-stu-id="c9597-120">hello load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) toohello web servers.</span></span>

<span data-ttu-id="c9597-121">serveurs de base de données Hello sont derrière un point de terminaison d’équilibrage de charge qui utilisent des serveurs web de hello pour le stockage.</span><span class="sxs-lookup"><span data-stu-id="c9597-121">hello database servers are behind an ILB endpoint which hello web servers use for storage.</span></span> <span data-ttu-id="c9597-122">Cette base de données service Équilibrage de point de terminaison, le trafic qui est à charge équilibrée entre les serveurs de base de données hello dans le jeu d’équilibrage de charge interne hello.</span><span class="sxs-lookup"><span data-stu-id="c9597-122">This database service load balanced endpoint, which traffic is load balanced across hello database servers in hello ILB set.</span></span>

<span data-ttu-id="c9597-123">Hello ci-dessous illustre d’image hello Internet faisant face à des applications à plusieurs niveaux au sein de hello même service cloud.</span><span class="sxs-lookup"><span data-stu-id="c9597-123">hello following image shows hello Internet facing multi-tier application within hello same cloud service.</span></span>

![Service cloud unique d'équilibrage de charge interne](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="c9597-125">Illustration 1 - Application multi-niveau sur Internet</span><span class="sxs-lookup"><span data-stu-id="c9597-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="c9597-126">Une autre utilisation possible pour une application multicouche est lorsque hello équilibrage de charge interne déployé tooa autre service cloud que hello un service hello consommateur pour hello équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="c9597-126">Another possible use for a multi-tier application is when hello ILB deployed tooa different cloud service than hello one consuming hello service for hello ILB.</span></span>

<span data-ttu-id="c9597-127">Cloud services à l’aide du même réseau virtuel aura de hello accéder au point de terminaison toohello équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="c9597-127">Cloud services using hello same virtual network will have access toohello ILB endpoint.</span></span> <span data-ttu-id="c9597-128">Hello ci-dessous illustre image sont des serveurs web frontaux dans un autre service cloud à partir de hello de base de données principale et à l’aide de hello de point de terminaison ILB dans hello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c9597-128">hello following image shows front-end web servers are in a different cloud service from hello database back-end and using hello ILB endpoint within hello same virtual network.</span></span>

![Équilibrage de charge interne entre les services cloud](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="c9597-130">Figure 2 : serveurs frontaux dans un service cloud différent</span><span class="sxs-lookup"><span data-stu-id="c9597-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="c9597-131">Applications cœur de métier (LOB) Intranet</span><span class="sxs-lookup"><span data-stu-id="c9597-131">Intranet line of business applications</span></span>

<span data-ttu-id="c9597-132">Le trafic des clients sur le réseau local de hello obtenir équilibrée ensemble hello serveurs métier à l’aide du réseau de tooAzure de connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="c9597-132">Traffic from clients on hello on-premises network get load-balanced across hello set of LOB servers using VPN connection tooAzure network.</span></span>

<span data-ttu-id="c9597-133">ordinateur client de Hello aura accès tooan IP adresse du service VPN Azure à l’aide de VPN de point de toosite.</span><span class="sxs-lookup"><span data-stu-id="c9597-133">hello client machine will have access tooan IP address from Azure VPN service using point toosite VPN.</span></span> <span data-ttu-id="c9597-134">Il permet de hello d’utilisation hello application LOB hébergée derrière le point de terminaison hello équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="c9597-134">It allows hello use hello LOB application hosted behind hello ILB endpoint.</span></span>

![À l’aide de VPN de point de toosite d’équilibrage de charge interne](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="c9597-136">Figure 3 : applications métier hébergées derrière le point de terminaison hello équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="c9597-136">Figure 3 - LOB applications hosted behind hello LB endpoint</span></span>

<span data-ttu-id="c9597-137">Un autre scénario pour hello LOB est toohave un réseau de toohello virtuel site toosite VPN où le point de terminaison ILB hello est configuré.</span><span class="sxs-lookup"><span data-stu-id="c9597-137">Another scenario for hello LOB is toohave a site toosite VPN toohello virtual network where hello ILB endpoint is configured.</span></span> <span data-ttu-id="c9597-138">Ainsi, sur site réseau du trafic toobe routé toohello point de terminaison ILB.</span><span class="sxs-lookup"><span data-stu-id="c9597-138">This allows on-premises network traffic toobe routed toohello ILB endpoint.</span></span>

![À l’aide du site toosite VPN d’équilibrage de charge interne](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="c9597-140">Point de terminaison de la figure 4 - le trafic de réseau local routée toohello équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="c9597-140">Figure 4 - On-premises network traffic routed toohello ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="c9597-141">Limites</span><span class="sxs-lookup"><span data-stu-id="c9597-141">Limitations</span></span>

<span data-ttu-id="c9597-142">Les configurations d’équilibrage de charge internes ne prennent pas en charge SNAT.</span><span class="sxs-lookup"><span data-stu-id="c9597-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="c9597-143">Dans le contexte de hello de ce document, SNAT fait référence de traduction d’adresses réseau tooport usurpation d’identité source.</span><span class="sxs-lookup"><span data-stu-id="c9597-143">In hello context of this document, SNAT refers tooport masquerading source  network address translation.</span></span>  <span data-ttu-id="c9597-144">Cela s’applique tooscenarios où une machine virtuelle dans un pool d’équilibrage de charge a besoin d’adresse IP de serveur frontal de tooreach hello respectifs interne équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="c9597-144">This applies tooscenarios where a VM in a load balancer pool needs tooreach hello respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="c9597-145">Ce scénario n’est pas pris en charge pour l’équilibreur de charge interne.</span><span class="sxs-lookup"><span data-stu-id="c9597-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="c9597-146">Échecs de connexion seront produit lorsque les flux hello sont à charge équilibrée toohello machine virtuelle qui provient du flux de hello.</span><span class="sxs-lookup"><span data-stu-id="c9597-146">Connection failures will occur when hello flow is load balanced toohello VM which originated hello flow.</span></span> <span data-ttu-id="c9597-147">Vous devez utiliser un équilibreur de charge de type proxy pour de tels scénarios.</span><span class="sxs-lookup"><span data-stu-id="c9597-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9597-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c9597-148">Next Steps</span></span>

[<span data-ttu-id="c9597-149">Prise en charge d'Azure Resource Manager pour l'équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="c9597-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="c9597-150">Prise en main de la configuration d’un équilibrage de charge sur Internet</span><span class="sxs-lookup"><span data-stu-id="c9597-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="c9597-151">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="c9597-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="c9597-152">Configuration d’un mode de distribution d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="c9597-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c9597-153">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="c9597-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
