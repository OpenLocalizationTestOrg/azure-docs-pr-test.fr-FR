---
title: "Planification et conception des connexions entre les systèmes locaux : passerelle VPN Azure | Microsoft Docs"
description: "En savoir plus sur la planification et la conception de la passerelle VPN pour les connexions entre locaux, hybrides et entre réseaux virtuels"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="8fcad-103">Planification et conception de la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="8fcad-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="8fcad-104">La planification et la conception de vos configurations intersites et entre réseaux virtuels peuvent être simples ou complexes, selon vos besoins de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="8fcad-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="8fcad-105">Cet article présente diverses considérations relatives à la conception et à la planification de base.</span><span class="sxs-lookup"><span data-stu-id="8fcad-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="8fcad-106"><a name="planning"></a>Planification</span><span class="sxs-lookup"><span data-stu-id="8fcad-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="8fcad-107"><a name="compare"></a>Options de connectivité intersite</span><span class="sxs-lookup"><span data-stu-id="8fcad-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="8fcad-108">Si vous souhaitez tooconnect votre site sur les sites en toute sécurité tooa des réseaux virtuels, que vous disposez de trois façons différentes toodo donc : Site à Site, Point-to-Site et ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fcad-108">If you want tooconnect your on-premises sites securely tooa virtual network, you have three different ways toodo so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="8fcad-109">Comparer les connexions entre différents sites hello qui sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="8fcad-109">Compare hello different cross-premises connections that are available.</span></span> <span data-ttu-id="8fcad-110">option Hello que vous choisissez peut dépendre d’un certain nombre d’éléments, tels que :</span><span class="sxs-lookup"><span data-stu-id="8fcad-110">hello option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="8fcad-111">Quel est le type de débit requis par votre solution ?</span><span class="sxs-lookup"><span data-stu-id="8fcad-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="8fcad-112">Voulez-vous vraiment toocommunicate sur hello Internet public via VPN sécurisée, ou via une connexion privée ?</span><span class="sxs-lookup"><span data-stu-id="8fcad-112">Do you want toocommunicate over hello public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="8fcad-113">Avez-vous un toouse de disponible d’adresse IP publique ?</span><span class="sxs-lookup"><span data-stu-id="8fcad-113">Do you have a public IP address available toouse?</span></span>
* <span data-ttu-id="8fcad-114">Envisagez-vous toouse un périphérique VPN ?</span><span class="sxs-lookup"><span data-stu-id="8fcad-114">Are you planning toouse a VPN device?</span></span> <span data-ttu-id="8fcad-115">Si tel est le cas, est-il compatible ?</span><span class="sxs-lookup"><span data-stu-id="8fcad-115">If so, is it compatible?</span></span>
* <span data-ttu-id="8fcad-116">Ne voulez-vous connecter qu’un petit nombre d’ordinateurs, ou souhaitez-vous mettre en place une connexion permanente pour votre site ?</span><span class="sxs-lookup"><span data-stu-id="8fcad-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="8fcad-117">Quel type de passerelle VPN est requis pour la solution de hello souhaité toocreate ?</span><span class="sxs-lookup"><span data-stu-id="8fcad-117">What type of VPN gateway is required for hello solution you want toocreate?</span></span>
* <span data-ttu-id="8fcad-118">Quelle référence SKU de passerelle devez-vous utiliser ?</span><span class="sxs-lookup"><span data-stu-id="8fcad-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="8fcad-119"><a name="planningtable"></a>Tableau de planification</span><span class="sxs-lookup"><span data-stu-id="8fcad-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="8fcad-120">Hello tableau suivant peut vous aider à déterminer hello meilleure option de connectivité de votre solution.</span><span class="sxs-lookup"><span data-stu-id="8fcad-120">hello following table can help you decide hello best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="8fcad-121"><a name="gwsku"></a>SKU de passerelle</span><span class="sxs-lookup"><span data-stu-id="8fcad-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="8fcad-122"><a name="wf"></a>Flux de travail</span><span class="sxs-lookup"><span data-stu-id="8fcad-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="8fcad-123">Hello liste suivante indique hello des flux de travail courant pour la connectivité du cloud :</span><span class="sxs-lookup"><span data-stu-id="8fcad-123">hello following list outlines hello common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="8fcad-124">Conception et planification de que votre adresse de hello connectivité topologie et de la liste des espaces pour tous les réseaux vous souhaitez tooconnect.</span><span class="sxs-lookup"><span data-stu-id="8fcad-124">Design and plan your connectivity topology and list hello address spaces for all networks you want tooconnect.</span></span>
2. <span data-ttu-id="8fcad-125">Créez un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="8fcad-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="8fcad-126">Créer une passerelle VPN de réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="8fcad-126">Create a VPN gateway for hello virtual network.</span></span>
4. <span data-ttu-id="8fcad-127">Créez et configurez des connexions tooon des réseaux locaux ou autres réseaux virtuels (si nécessaire).</span><span class="sxs-lookup"><span data-stu-id="8fcad-127">Create and configure connections tooon-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="8fcad-128">Créez et configurez une connexion Point-à-Site pour votre passerelle VPN Azure (en fonction des besoins).</span><span class="sxs-lookup"><span data-stu-id="8fcad-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="8fcad-129"><a name="design"></a>Conception</span><span class="sxs-lookup"><span data-stu-id="8fcad-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="8fcad-130"><a name="topologies"></a>Topologies de connexion</span><span class="sxs-lookup"><span data-stu-id="8fcad-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="8fcad-131">Commencez par examiner les diagrammes hello Bonjour [sur la passerelle du VPN](vpn-gateway-about-vpngateways.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="8fcad-131">Start by looking at hello diagrams in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="8fcad-132">article de Hello contient des diagrammes de base, les modèles de déploiement hello pour chaque topologie et les outils de déploiement disponibles hello vous pouvez utiliser toodeploy votre configuration.</span><span class="sxs-lookup"><span data-stu-id="8fcad-132">hello article contains basic diagrams, hello deployment models for each topology, and hello available deployment tools you can use toodeploy your configuration.</span></span>

### <span data-ttu-id="8fcad-133"><a name="designbasics"></a>Concepts de base</span><span class="sxs-lookup"><span data-stu-id="8fcad-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="8fcad-134">Hello les sections suivantes présentent les principes fondamentaux de passerelle hello VPN.</span><span class="sxs-lookup"><span data-stu-id="8fcad-134">hello following sections discuss hello VPN gateway basics.</span></span> 

#### <span data-ttu-id="8fcad-135"><a name="servicelimits"></a>Limites des services de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="8fcad-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="8fcad-136">Faites défiler hello tables tooview [limites des services de mise en réseau](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="8fcad-136">Scroll through hello tables tooview [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="8fcad-137">limites de Hello répertoriés peuvent affecter votre conception.</span><span class="sxs-lookup"><span data-stu-id="8fcad-137">hello limits listed may impact your design.</span></span>

#### <span data-ttu-id="8fcad-138"><a name="subnets"></a>À propos des sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="8fcad-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="8fcad-139">Lorsque vous créez des connexions, vous devez prendre en compte vos plages de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="8fcad-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="8fcad-140">Il ne peut pas avoir de chevauchement entre des plages d’adresses de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="8fcad-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="8fcad-141">Un sous-réseau qui se chevauchent est lorsqu’un emplacement local ou de réseau virtuel contient hello contient du même espace d’adressage hello autre emplacement.</span><span class="sxs-lookup"><span data-stu-id="8fcad-141">An overlapping subnet is when one virtual network or on-premises location contains hello same address space that hello other location contains.</span></span> <span data-ttu-id="8fcad-142">Cela signifie que vous avez besoin des ingénieurs de votre réseau pour votre toocarve de réseaux sur site local à une plage pour vous toouse pour votre adresse IP Azure/sous-réseaux de l’espace d’adressage.</span><span class="sxs-lookup"><span data-stu-id="8fcad-142">This means that you need your network engineers for your local on-premises networks toocarve out a range for you toouse for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="8fcad-143">Vous avez besoin d’espace d’adressage qui n’est pas utilisé sur le réseau de site local hello.</span><span class="sxs-lookup"><span data-stu-id="8fcad-143">You need address space that is not being used on hello local on-premises network.</span></span>

<span data-ttu-id="8fcad-144">Il est également important d’éviter le chevauchement des sous-réseaux lorsque vous travaillez avec des connexions entre réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="8fcad-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="8fcad-145">Si vos sous-réseaux se chevauchent et une adresse IP existe dans l’envoi de hello et la destination des réseaux virtuels, les connexions réseau à échouent.</span><span class="sxs-lookup"><span data-stu-id="8fcad-145">If your subnets overlap and an IP address exists in both hello sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="8fcad-146">Azure ne peut pas acheminer hello données toohello autre réseau virtuel comme adresse de destination hello fait partie de hello envoi réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8fcad-146">Azure can't route hello data toohello other VNet because hello destination address is part of hello sending VNet.</span></span>

<span data-ttu-id="8fcad-147">Les passerelles VPN nécessitent un sous-réseau spécifique appelé sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="8fcad-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="8fcad-148">Tous les sous-réseaux de passerelle doivent être nommés GatewaySubnet toowork correctement.</span><span class="sxs-lookup"><span data-stu-id="8fcad-148">All gateway subnets must be named GatewaySubnet toowork properly.</span></span> <span data-ttu-id="8fcad-149">Veillez tooname pas votre sous-réseau de passerelle, un autre nom et ne pas déployer des machines virtuelles ou n’importe quel autre sous-réseau de passerelle toohello.</span><span class="sxs-lookup"><span data-stu-id="8fcad-149">Be sure not tooname your gateway subnet a different name, and don't deploy VMs or anything else toohello gateway subnet.</span></span> <span data-ttu-id="8fcad-150">Voir [Sous-réseaux de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="8fcad-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="8fcad-151"><a name="local"></a>À propos des passerelles de réseau local</span><span class="sxs-lookup"><span data-stu-id="8fcad-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="8fcad-152">passerelle de réseau local Hello fait généralement référence d’emplacement de site tooyour.</span><span class="sxs-lookup"><span data-stu-id="8fcad-152">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="8fcad-153">Dans le modèle de déploiement classique de hello, passerelle de réseau local hello est tooas auxquels un Site réseau Local.</span><span class="sxs-lookup"><span data-stu-id="8fcad-153">In hello classic deployment model, hello local network gateway is referred tooas a Local Network Site.</span></span> <span data-ttu-id="8fcad-154">Lorsque vous configurez une passerelle de réseau local, vous lui donnez un nom, spécifiez hello adresse IP publique du périphérique VPN hello localement et les préfixes d’adresse hello qui se trouvent dans un emplacement local de hello.</span><span class="sxs-lookup"><span data-stu-id="8fcad-154">When you configure a local network gateway, you give it a name, specify hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are in hello on-premises location.</span></span> <span data-ttu-id="8fcad-155">Azure examine les préfixes d’adresse de destination hello pour le trafic réseau, consulte configuration hello que vous avez spécifié pour la passerelle de réseau local hello et route les paquets en conséquence.</span><span class="sxs-lookup"><span data-stu-id="8fcad-155">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for hello local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="8fcad-156">Vous pouvez modifier les préfixes d’adresse hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="8fcad-156">You can modify hello address prefixes as needed.</span></span> <span data-ttu-id="8fcad-157">Pour plus d’informations, voir [Passerelles de réseau local](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="8fcad-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="8fcad-158"><a name="gwtype"></a>À propos des types de passerelles</span><span class="sxs-lookup"><span data-stu-id="8fcad-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="8fcad-159">Il est essentiel de sélection du type de passerelle est correct de hello pour votre topologie.</span><span class="sxs-lookup"><span data-stu-id="8fcad-159">Selecting hello correct gateway type for your topology is critical.</span></span> <span data-ttu-id="8fcad-160">Si vous sélectionnez un type incorrect hello, votre passerelle ne fonctionne pas correctement.</span><span class="sxs-lookup"><span data-stu-id="8fcad-160">If you select hello wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="8fcad-161">type de passerelle Hello spécifie comment la passerelle hello elle-même se connecte et est un paramètre de configuration requise pour le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="8fcad-161">hello gateway type specifies how hello gateway itself connects and is a required configuration setting for hello Resource Manager deployment model.</span></span>

<span data-ttu-id="8fcad-162">types de passerelle Hello sont :</span><span class="sxs-lookup"><span data-stu-id="8fcad-162">hello gateway types are:</span></span>

* <span data-ttu-id="8fcad-163">Vpn</span><span class="sxs-lookup"><span data-stu-id="8fcad-163">Vpn</span></span>
* <span data-ttu-id="8fcad-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8fcad-164">ExpressRoute</span></span>

#### <span data-ttu-id="8fcad-165"><a name="connectiontype"></a>À propos des types de connexions</span><span class="sxs-lookup"><span data-stu-id="8fcad-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="8fcad-166">Chaque configuration nécessite un type de connexion spécifique.</span><span class="sxs-lookup"><span data-stu-id="8fcad-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="8fcad-167">types de connexion Hello sont :</span><span class="sxs-lookup"><span data-stu-id="8fcad-167">hello connection types are:</span></span>

* <span data-ttu-id="8fcad-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="8fcad-168">IPsec</span></span>
* <span data-ttu-id="8fcad-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="8fcad-169">Vnet2Vnet</span></span>
* <span data-ttu-id="8fcad-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8fcad-170">ExpressRoute</span></span>
* <span data-ttu-id="8fcad-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="8fcad-171">VPNClient</span></span>

#### <span data-ttu-id="8fcad-172"><a name="vpntype"></a>À propos des types de VPN</span><span class="sxs-lookup"><span data-stu-id="8fcad-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="8fcad-173">Chaque configuration nécessite un type de VPN spécifique.</span><span class="sxs-lookup"><span data-stu-id="8fcad-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="8fcad-174">Si vous combinez deux configurations, telles que la création d’une connexion Site à Site et un toohello de connexion de Point-to-Site même réseau virtuel, vous devez utiliser un type VPN qui satisfait les exigences de connexion.</span><span class="sxs-lookup"><span data-stu-id="8fcad-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection toohello same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="8fcad-175">Hello tableaux suivants indiquent les type de VPN hello comme il mappe tooeach configuration de la connexion.</span><span class="sxs-lookup"><span data-stu-id="8fcad-175">hello following tables show hello VPN type as it maps tooeach connection configuration.</span></span> <span data-ttu-id="8fcad-176">Vérifiez que hello type VPN pour votre configuration de hello correspond à la passerelle que vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="8fcad-176">Make sure hello VPN type for your gateway matches hello configuration that you want toocreate.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="8fcad-177"><a name="devices"></a>Périphériques VPN et connexions de site à site</span><span class="sxs-lookup"><span data-stu-id="8fcad-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="8fcad-178">connexion tooconfigure un Site à Site, quel que soit le modèle de déploiement, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8fcad-178">tooconfigure a Site-to-Site connection, regardless of deployment model, you need hello following items:</span></span>

* <span data-ttu-id="8fcad-179">un périphérique VPN compatible avec les passerelles VPN Azure</span><span class="sxs-lookup"><span data-stu-id="8fcad-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="8fcad-180">une adresse IPv4 publique qui ne se trouve pas derrière un NAT</span><span class="sxs-lookup"><span data-stu-id="8fcad-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="8fcad-181">Vous devez être toohave configurer votre périphérique VPN ou demandez à une personne qui peut configurer le périphérique de hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="8fcad-181">You need toohave experience configuring your VPN device, or have someone that can configure hello device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="8fcad-182"><a name="forcedtunnel"></a>Envisager le routage avec tunneling forcé</span><span class="sxs-lookup"><span data-stu-id="8fcad-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="8fcad-183">Dans la plupart des configurations, vous pouvez configurer le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="8fcad-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="8fcad-184">Forcé tunneling permet de rediriger ou de « forcer » tous les Internet liées au trafic tooyour arrière local emplacement via un tunnel VPN de Site à Site pour l’inspection et d’audit.</span><span class="sxs-lookup"><span data-stu-id="8fcad-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="8fcad-185">Il s’agit d’une condition de sécurité critique pour la plupart des stratégies informatiques d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="8fcad-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="8fcad-186">Sans tunneling forcé, le trafic Internet à partir de vos machines virtuelles dans Azure traverse toujours l’infrastructure réseau Azure directement out toohello Internet, sans hello option tooallow vous tooinspect ou audit du trafic hello.</span><span class="sxs-lookup"><span data-stu-id="8fcad-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="8fcad-187">Accès Internet non autorisé peut entraîner la divulgation de tooinformation ou d’autres types de failles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="8fcad-187">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

<span data-ttu-id="8fcad-188">Une connexion de tunneling forcé peut être configurée dans les deux modèles de déploiement et à l’aide de différents outils.</span><span class="sxs-lookup"><span data-stu-id="8fcad-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="8fcad-189">Pour plus d’informations, consultez [Configurer un tunneling forcé](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="8fcad-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="8fcad-190">**Diagramme du tunneling forcé**</span><span class="sxs-lookup"><span data-stu-id="8fcad-190">**Forced tunneling diagram**</span></span>

![Diagramme du tunneling forcé de la passerelle VPN Azure](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="8fcad-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8fcad-192">Next steps</span></span>

<span data-ttu-id="8fcad-193">Consultez hello [Forum aux questions de la passerelle VPN](vpn-gateway-vpn-faq.md) et [sur la passerelle du VPN](vpn-gateway-about-vpngateways.md) articles pour plus d’informations toohelp vous avec votre conception.</span><span class="sxs-lookup"><span data-stu-id="8fcad-193">See hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information toohelp you with your design.</span></span>

<span data-ttu-id="8fcad-194">Pour plus d’informations sur les paramètres de passerelle spécifiques, voir [À propos des paramètres de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="8fcad-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>