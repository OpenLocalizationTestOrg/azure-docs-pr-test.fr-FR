---
title: "aaaFrequently aux questions pour la passerelle d’Application Azure | Documents Microsoft"
description: "Cette page fournit des réponses aux questions sur la passerelle d’Application Azure d’elles sonttrop"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="7e299-103">Forum aux questions pour Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="7e299-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="7e299-104">Généralités</span><span class="sxs-lookup"><span data-stu-id="7e299-104">General</span></span>

<span data-ttu-id="7e299-105">**Q. Qu’est-ce qu’Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="7e299-106">Azure Application Gateway est un contrôleur de remise d’application proposé sous la forme d’un service, qui offre diverses fonctionnalités d’équilibrage de charge de couche 7 pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="7e299-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="7e299-107">Il fournit un service hautement disponible et évolutif, entièrement géré par Azure.</span><span class="sxs-lookup"><span data-stu-id="7e299-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="7e299-108">**Q. Quelles sont les fonctionnalités prises en charge par Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="7e299-109">Passerelle d’application prend en charge SSL tooend fin et de déchargement SSL, pare-feu d’applications Web, d’affinité de session basée sur un cookie, l’url basée sur le chemin d’accès routage, hébergement de plusieurs sites et d’autres.</span><span class="sxs-lookup"><span data-stu-id="7e299-109">Application Gateway supports SSL offloading and end tooend SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="7e299-110">Pour obtenir une liste complète des fonctionnalités prises en charge, visitez [Introduction tooApplication passerelle](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="7e299-110">For a full list of supported features, visit [Introduction tooApplication Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="7e299-111">**Q. Qu’est la différence de hello entre la passerelle d’Application et l’équilibrage de charge Azure ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-111">**Q. What is hello difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="7e299-112">Application Gateway est un équilibreur de charge de couche 7, ce qui signifie qu’il fonctionne avec le trafic web uniquement (HTTP/HTTPS/WebSocket).</span><span class="sxs-lookup"><span data-stu-id="7e299-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="7e299-113">Il prend en charge des fonctionnalités telles que la terminaison SSL, l’affinité de session basée sur les cookies et le tourniquet (round robin) pour le trafic d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="7e299-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="7e299-114">Load Balancer équilibre la charge du trafic au niveau de la couche 4 (TCP/UDP).</span><span class="sxs-lookup"><span data-stu-id="7e299-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="7e299-115">**Q. Quels sont les protocoles pris en charge par Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="7e299-116">Application Gateway prend en charge les protocoles HTTP, HTTPS et WebSocket.</span><span class="sxs-lookup"><span data-stu-id="7e299-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="7e299-117">**Q. Quelles sont les ressources actuellement prises en charge dans le pool backend ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="7e299-118">Les pools backend peuvent être composés de cartes d’interface réseau, de groupes de machines virtuelles identiques, d’adresses IP publiques, d’adresses IP internes, de noms de domaine complets et de serveurs principaux multi-locataires comme Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="7e299-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="7e299-119">Passerelle d’application ne sont pas membres du pool principal lié tooan à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="7e299-119">Application Gateway backend pool members are not tied tooan availability set.</span></span> <span data-ttu-id="7e299-120">Les membres des pools backend peuvent être sur des clusters, des centres de données ou en dehors d’Azure tant qu’ils disposent d’une connectivité IP.</span><span class="sxs-lookup"><span data-stu-id="7e299-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="7e299-121">**Q. Les régions de service n’hello est disponible dans ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-121">**Q. What regions is hello service available in?**</span></span>

<span data-ttu-id="7e299-122">Application Gateway est disponible dans toutes les régions de la version globale d’Azure.</span><span class="sxs-lookup"><span data-stu-id="7e299-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="7e299-123">Il est également disponible dans [Azure en Chine](https://www.azure.cn/) et [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/).</span><span class="sxs-lookup"><span data-stu-id="7e299-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="7e299-124">**Q. S’agit-il d’un déploiement dédié à mon abonnement ou est-il partagé entre les clients ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="7e299-125">Application Gateway est un déploiement dédié dans votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="7e299-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="7e299-126">**Q. La redirection HTTP->HTTPS est-elle prise en charge ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="7e299-127">La redirection est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="7e299-127">Redirection is supported.</span></span> <span data-ttu-id="7e299-128">Visitez [vue d’ensemble de la redirection de passerelle d’Application](application-gateway-redirect-overview.md) toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="7e299-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn more.</span></span>

<span data-ttu-id="7e299-129">**Q. Dans quel ordre les écouteurs sont-ils traités ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="7e299-130">Écouteurs sont traités dans l’ordre de hello qu'elles sont affichées.</span><span class="sxs-lookup"><span data-stu-id="7e299-130">Listeners are processed in hello order they are shown.</span></span> <span data-ttu-id="7e299-131">Pour cette raison, si un écouteur de base correspond à une demande entrante, il la traite en premier.</span><span class="sxs-lookup"><span data-stu-id="7e299-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="7e299-132">Écouteurs de plusieurs sites doivent être configurés avant un trafic de tooensure base écouteur est routé toohello correct principal.</span><span class="sxs-lookup"><span data-stu-id="7e299-132">Multi-site listeners should be configured before a basic listener tooensure traffic is routed toohello correct back-end.</span></span>

<span data-ttu-id="7e299-133">**Q. Où puis-je trouver le DNS et l’adresse IP d’Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="7e299-134">Lorsque vous utilisez une adresse IP publique comme point de terminaison, ces informations sont accessibles sur la ressource d’adresse IP publique hello ou sur la page de vue d’ensemble de hello pour hello passerelle d’Application dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="7e299-134">When using a public IP address as an endpoint, this information can be found on hello public IP address resource or on hello Overview page for hello Application Gateway in hello portal.</span></span> <span data-ttu-id="7e299-135">Pour les adresses IP internes, ce sont accessibles sur la page de vue d’ensemble de hello.</span><span class="sxs-lookup"><span data-stu-id="7e299-135">For internal IP addresses, this can be found on hello Overview page.</span></span>

<span data-ttu-id="7e299-136">**Q. Hello DNS ou IP change sur la durée de vie hello Hello passerelle d’Application ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-136">**Q. Does hello IP or DNS change over hello lifetime of hello Application Gateway?**</span></span>

<span data-ttu-id="7e299-137">Hello adresse IP virtuelle peut changer si la passerelle de hello est arrêté et démarré par le client de hello.</span><span class="sxs-lookup"><span data-stu-id="7e299-137">hello VIP can change if hello gateway is stopped and started by hello customer.</span></span> <span data-ttu-id="7e299-138">Hello DNS associés avec la passerelle d’Application ne change pas hello du cycle de vie de la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="7e299-138">hello DNS associated with Application Gateway does not change over hello lifecycle of hello gateway.</span></span> <span data-ttu-id="7e299-139">Pour cette raison, il est recommandé de toouse un alias CNAME et faites-le pointer adresse DNS toohello hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="7e299-139">For this reason, it is recommended toouse a CNAME alias and point it toohello DNS address of hello Application Gateway.</span></span>

<span data-ttu-id="7e299-140">**Q. Application Gateway prend-il en charge les adresses IP statiques ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="7e299-141">Non, Application Gateway ne prend pas en charge les adresses IP publiques statiques. Néanmoins, les adresses IP internes statiques sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="7e299-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="7e299-142">**Q. Passerelle d’Application prend-elle en charge plusieurs adresses IP publique sur la passerelle hello ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-142">**Q. Does Application Gateway support multiple public IPs on hello gateway?**</span></span>

<span data-ttu-id="7e299-143">Une seule adresse IP publique est prise en charge sur Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7e299-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="7e299-144">**Q. Application Gateway prend-il en charge les en-têtes x-forwarded-for ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="7e299-145">Oui, passerelle d’Application insère x transmis pour, proto x transféré et en-têtes x-transféré-port dans la demande de hello transmis toohello principal.</span><span class="sxs-lookup"><span data-stu-id="7e299-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into hello request forwarded toohello backend.</span></span> <span data-ttu-id="7e299-146">format Hello pour x transmis pour l’en-tête est une liste séparée par des virgules d’IP : port.</span><span class="sxs-lookup"><span data-stu-id="7e299-146">hello format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="7e299-147">les valeurs valides Hello proto x transmis sont http ou https.</span><span class="sxs-lookup"><span data-stu-id="7e299-147">hello valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="7e299-148">X-transféré-port Spécifie le port hello qui demande hello atteint hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="7e299-148">X-forwarded-port specifies hello port at which hello request reached at hello Application Gateway.</span></span>

<span data-ttu-id="7e299-149">**Q. Combien de temps faut-il toodeploy une passerelle d’Application ? Mon Application Gateway continue-t-elle de fonctionner après une mise à jour  ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-149">**Q. How long does it take toodeploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="7e299-150">Les nouveaux déploiements de passerelle d’Application peuvent prendre jusqu'à too20 minutes tooprovision.</span><span class="sxs-lookup"><span data-stu-id="7e299-150">New Application Gateway deployments can take up too20 minutes tooprovision.</span></span> <span data-ttu-id="7e299-151">Taille ou de nombre modifications tooinstance ne sont pas sans interruption, et passerelle de hello reste actif pendant ce temps.</span><span class="sxs-lookup"><span data-stu-id="7e299-151">Changes tooinstance size/count are not disruptive, and hello gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="7e299-152">Configuration</span><span class="sxs-lookup"><span data-stu-id="7e299-152">Configuration</span></span>

<span data-ttu-id="7e299-153">**Q. Application Gateway est-il toujours déployé dans un réseau virtuel ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="7e299-154">Oui, Application Gateway est toujours déployé dans un sous-réseau de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="7e299-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="7e299-155">Ce sous-réseau ne peut contenir que des Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7e299-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="7e299-156">**Q. Passerelle d’Application peut communiquer avec tooinstances en dehors de son réseau virtuel ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-156">**Q. Can Application Gateway talk tooinstances outside its virtual network?**</span></span>

<span data-ttu-id="7e299-157">Passerelle d’application peut communiquer avec tooinstances en dehors du réseau virtuel hello qu’il est aussi de connectivité IP.</span><span class="sxs-lookup"><span data-stu-id="7e299-157">Application Gateway can talk tooinstances outside of hello virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="7e299-158">Si vous prévoyez de toouse le nécessite des adresses IP internes en tant que membres du pool principal, puis il [réseau virtuel d’homologation](../virtual-network/virtual-network-peering-overview.md) ou [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="7e299-158">If you plan toouse internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="7e299-159">**Q. Puis-je déployer rien d’autre dans le sous-réseau de passerelle d’Application hello ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-159">**Q. Can I deploy anything else in hello Application Gateway subnet?**</span></span>

<span data-ttu-id="7e299-160">Non, mais vous pouvez déployer d’autres passerelles d’application dans un sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="7e299-160">No, but you can deploy other application gateways in hello subnet.</span></span>

<span data-ttu-id="7e299-161">**Q. Groupes de sécurité réseau sont pris en charge sur le sous-réseau de passerelle d’Application hello ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-161">**Q. Are Network Security Groups supported on hello Application Gateway subnet?**</span></span>

<span data-ttu-id="7e299-162">Groupes de sécurité réseau sont pris en charge sur le sous-réseau de passerelle d’Application hello hello suivant restrictions :</span><span class="sxs-lookup"><span data-stu-id="7e299-162">Network Security Groups are supported on hello Application Gateway subnet with hello following restrictions:</span></span>

* <span data-ttu-id="7e299-163">Exceptions doivent être placées dans pour le trafic entrant sur les ports 65503-65 534 pour le serveur principal d’intégrité toowork correctement.</span><span class="sxs-lookup"><span data-stu-id="7e299-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health toowork correctly.</span></span>

* <span data-ttu-id="7e299-164">La connectivité Internet sortante ne peut pas être bloquée.</span><span class="sxs-lookup"><span data-stu-id="7e299-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="7e299-165">Le trafic à partir de hello AzureLoadBalancer balise doit être autorisé.</span><span class="sxs-lookup"><span data-stu-id="7e299-165">Traffic from hello AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="7e299-166">**Q. Quelles sont les limites de hello sur la passerelle d’Application ? Puis-je augmenter ces limites ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-166">**Q. What are hello limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="7e299-167">Visitez [limites de passerelle d’Application](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limites.</span><span class="sxs-lookup"><span data-stu-id="7e299-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limits.</span></span>

<span data-ttu-id="7e299-168">**Q. Puis-je utiliser Application Gateway pour le trafic externe et interne simultanément ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="7e299-169">Oui, Application Gateway peut avoir une adresse IP interne et une adresse IP externe par Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7e299-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="7e299-170">**Q. VNET Peering est-il pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="7e299-171">Oui, VNET Peering est pris en charge et est utile pour équilibrer la charge du trafic des autres réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="7e299-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="7e299-172">**Q. Puis-je parler tooon des serveurs locaux lorsqu’ils sont connectés par des tunnels ExpressRoute ou VPN ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-172">**Q. Can I talk tooon-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="7e299-173">Oui, tant que le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="7e299-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="7e299-174">**Q. Puis-je avoir un pool backend servant plusieurs applications sur des ports différents ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="7e299-175">L’architecture orientée microservices est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="7e299-175">Micro service architecture is supported.</span></span> <span data-ttu-id="7e299-176">Il vous faudrait plusieurs tooprobe de paramètres configurés http sur des ports différents.</span><span class="sxs-lookup"><span data-stu-id="7e299-176">You would need multiple http settings configured tooprobe on different ports.</span></span>

<span data-ttu-id="7e299-177">**Q. Les sondes personnalisées prennent-elles en charge les caractères génériques/les expressions régulières sur les données de réponse ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="7e299-178">Les sondes personnalisées ne prennent pas en charge les caractères génériques/les expressions régulières sur les données de réponse.</span><span class="sxs-lookup"><span data-stu-id="7e299-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="7e299-179">**Q. Comment les règles sont-elles traitées ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="7e299-180">Les règles sont traitées dans l’ordre de hello qu’ils sont configurés.</span><span class="sxs-lookup"><span data-stu-id="7e299-180">Rules are processed in hello order they are configured.</span></span> <span data-ttu-id="7e299-181">Il est recommandé que les règles de plusieurs sites sont configurés avant que les règles de base tooreduce hello risque que le trafic est acheminé principal inappropriée de toohello comme règle de base hello correspondrait à trafic en fonction de la règle de plusieurs sites toohello préalable des ports en cours d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="7e299-181">It is recommended that multi-site rules are configured before basic rules tooreduce hello chance that traffic is routed toohello inappropriate backend as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="7e299-182">**Q. Comment les règles sont-elles traitées ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="7e299-183">Les règles sont traitées dans hello leur ordre de création.</span><span class="sxs-lookup"><span data-stu-id="7e299-183">Rules are processed in hello order they are created.</span></span> <span data-ttu-id="7e299-184">Nous vous recommandons de configurer les règles multi-sites avant les règles de base.</span><span class="sxs-lookup"><span data-stu-id="7e299-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="7e299-185">En configurant les écouteurs multisites tout d’abord, cette configuration réduit les risques de hello que le trafic est routé toohello les principaux inappropriés.</span><span class="sxs-lookup"><span data-stu-id="7e299-185">By configuring multi-site listeners first, this configuration reduces hello chance that traffic is routed toohello inappropriate backend.</span></span> <span data-ttu-id="7e299-186">Ce problème de routage peut se produire comme règle de base hello correspondrait à trafic en fonction de la règle de plusieurs sites toohello préalable des ports en cours d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="7e299-186">This routing issue can occur as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="7e299-187">**Q. Ce que signifier champ de l’hôte hello pour les sondes personnalisés ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-187">**Q. What does hello Host field for custom probes signify?**</span></span>

<span data-ttu-id="7e299-188">Champ de l’hôte spécifie hello nom toosend hello de la sonde.</span><span class="sxs-lookup"><span data-stu-id="7e299-188">Host field specifies hello name toosend hello probe to.</span></span> <span data-ttu-id="7e299-189">S’applique uniquement lorsque plusieurs sites sont configurés sur Application Gateway, sinon utilisez '127.0.0.1'.</span><span class="sxs-lookup"><span data-stu-id="7e299-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="7e299-190">Cette valeur est différente du nom d’hôte de machine virtuelle et se trouve au format suivant : \<protocole\>://\<hôte\>:\<port\>\<chemin d’accès\>.</span><span class="sxs-lookup"><span data-stu-id="7e299-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="7e299-191">**Q. Puis-je tooa d’accès d’autorisation Application Gateway quelques adresses IP de source ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-191">**Q. Can I whitelist Application Gateway access tooa few source IPs?**</span></span>

<span data-ttu-id="7e299-192">Ce scénario peut être réalisé en utilisant des groupes de sécurité réseau sur le sous-réseau d’Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7e299-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="7e299-193">Hello suivant restrictions doit être placé sur sous-réseau hello dans l’ordre de hello répertorié de priorité :</span><span class="sxs-lookup"><span data-stu-id="7e299-193">hello following restrictions should be put on hello subnet in hello listed order of priority:</span></span>

* <span data-ttu-id="7e299-194">Autoriser le trafic entrant à partir de l’adresse IP ou de la plage d’adresses IP sources.</span><span class="sxs-lookup"><span data-stu-id="7e299-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="7e299-195">Autoriser les demandes entrantes à partir de toutes les sources tooports 65503-65 534 pour [communication de contrôle d’intégrité de serveur principal](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="7e299-195">Allow incoming requests from all sources tooports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="7e299-196">Autoriser les sondes d’équilibrage de charge Azure entrants (balise AzureLoadBalancer) et virtuel le trafic réseau entrant (balise VirtualNetwork) sur hello [NSG](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="7e299-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on hello [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="7e299-197">Bloquer tout autre trafic entrant avec une règle Refuser tout.</span><span class="sxs-lookup"><span data-stu-id="7e299-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="7e299-198">Autoriser le trafic sortant toohello internet pour toutes les destinations.</span><span class="sxs-lookup"><span data-stu-id="7e299-198">Allow outbound traffic toohello internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="7e299-199">Performances</span><span class="sxs-lookup"><span data-stu-id="7e299-199">Performance</span></span>

<span data-ttu-id="7e299-200">**Q. Comment Application Gateway prend-il en charge la haute disponibilité et l’évolutivité ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="7e299-201">Application Gateway prend en charge les scénarios de haute disponibilité lorsque vous avez deux instances déployées ou plus.</span><span class="sxs-lookup"><span data-stu-id="7e299-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="7e299-202">Azure distribue ces instances sur mise à jour et les pannes tooensure domaines que toutes les instances n’échouent pas à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="7e299-202">Azure distributes these instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="7e299-203">Passerelle d’application prend en charge l’évolutivité en ajoutant plusieurs instances de hello charge hello de tooshare même passerelle.</span><span class="sxs-lookup"><span data-stu-id="7e299-203">Application Gateway supports scalability by adding multiple instances of hello same gateway tooshare hello load.</span></span>

<span data-ttu-id="7e299-204">**Q. Comment puis-je obtenir le scénario de récupération d’urgence dans les centres de données avec Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="7e299-205">Les clients peuvent utiliser Traffic Manager toodistribute trafic entre plusieurs passerelles d’Application dans différents centres de données.</span><span class="sxs-lookup"><span data-stu-id="7e299-205">Customers can use Traffic Manager toodistribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="7e299-206">**Q. La mise à l’échelle automatique est-elle prise en charge ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="7e299-207">Non, mais la passerelle d’Application a une mesure de débit qui peut être utilisé tooalert lorsqu’un seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="7e299-207">No, but Application Gateway has a throughput metric that can be used tooalert you when a threshold is reached.</span></span> <span data-ttu-id="7e299-208">Manuellement l’ajout d’instances ou de modification de taille ne redémarre pas de passerelle de hello et n’affecte pas le trafic existant.</span><span class="sxs-lookup"><span data-stu-id="7e299-208">Manually adding instances or changing size does not restart hello gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="7e299-209">**Q. Est-ce que les opérations de montée/descente en puissance effectuées manuellement interrompent le service ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="7e299-210">Aucune interruption de service n’a lieu, les instances sont réparties entre les domaines de mise à niveau et les domaines d’erreur.</span><span class="sxs-lookup"><span data-stu-id="7e299-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="7e299-211">**Q. Puis-je modifier taille de l’instance à partir de la moyenne toolarge sans interruption de service ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-211">**Q. Can I change instance size from medium toolarge without disruption?**</span></span>

<span data-ttu-id="7e299-212">Oui, Azure distribue les instances sur la mise à jour et les pannes tooensure domaines que toutes les instances n’échouent pas à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="7e299-212">Yes, Azure distributes instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="7e299-213">Application prend en charge de la passerelle mise à l’échelle en ajoutant plusieurs instances de hello même passerelle tooshare hello de charge.</span><span class="sxs-lookup"><span data-stu-id="7e299-213">Application Gateway supports scaling by adding multiple instances of hello same gateway tooshare hello load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="7e299-214">Configuration SSL</span><span class="sxs-lookup"><span data-stu-id="7e299-214">SSL Configuration</span></span>

<span data-ttu-id="7e299-215">**Q. Quels sont les certificats pris en charge sur Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="7e299-216">Les certificats auto-signés, les certificats d’autorité de certification et les certificats génériques sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7e299-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="7e299-217">Les certificats de validation étendue ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7e299-217">EV certs are not supported.</span></span>

<span data-ttu-id="7e299-218">**Q. Quelles sont les hello actuel les suites de chiffrement pris en charge par la passerelle d’Application ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-218">**Q. What are hello current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="7e299-219">Hello Voici hello actuel les suites de chiffrement pris en charge par la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="7e299-219">hello following are hello current cipher suites supported by application gateway.</span></span> <span data-ttu-id="7e299-220">Visite : [configurer SSL versions de stratégie et des suites de chiffrement sur la passerelle d’Application](application-gateway-configure-ssl-policy-powershell.md) toolearn comment toocustomize options d’authentification SSL.</span><span class="sxs-lookup"><span data-stu-id="7e299-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn how toocustomize SSL options.</span></span>

- <span data-ttu-id="7e299-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="7e299-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="7e299-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="7e299-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="7e299-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="7e299-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="7e299-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="7e299-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="7e299-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="7e299-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="7e299-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="7e299-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="7e299-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="7e299-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="7e299-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="7e299-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="7e299-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="7e299-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="7e299-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="7e299-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="7e299-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="7e299-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="7e299-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="7e299-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="7e299-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="7e299-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="7e299-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="7e299-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="7e299-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="7e299-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="7e299-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="7e299-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="7e299-247">**Q. Passerelle d’Application prennent également en charge rechiffrement de trafic toohello principal ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-247">**Q. Does Application Gateway also support re-encryption of traffic toohello backend?**</span></span>

<span data-ttu-id="7e299-248">Oui, déchargement de passerelle d’Application prend en charge SSL et fin tooend SSL, qui chiffre à nouveau hello trafic toohello principal.</span><span class="sxs-lookup"><span data-stu-id="7e299-248">Yes, Application Gateway supports SSL offload, and end tooend SSL, which re-encrypts hello traffic toohello backend.</span></span>

<span data-ttu-id="7e299-249">**Q. Puis-je configurer des versions de protocole SSL de toocontrol de stratégie SSL ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-249">**Q. Can I configure SSL policy toocontrol SSL Protocol versions?**</span></span>

<span data-ttu-id="7e299-250">Oui, vous pouvez configurer la passerelle d’Application toodeny TLS1.0, TLS1.1 et TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="7e299-250">Yes, you can configure Application Gateway toodeny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="7e299-251">SSL 2.0 et 3.0 sont déjà désactivés par défaut et ne sont pas configurables.</span><span class="sxs-lookup"><span data-stu-id="7e299-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="7e299-252">**Q. Puis-je configurer les suites de chiffrement et l’ordre de la stratégie ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="7e299-253">Oui, la [configuration des suites de chiffrement](application-gateway-ssl-policy-overview.md) est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="7e299-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="7e299-254">Lorsque vous définissez une stratégie personnalisée, au moins un des hello suivant des suites de chiffrement doit être activé.</span><span class="sxs-lookup"><span data-stu-id="7e299-254">When defining a custom policy, at least one of hello following cipher suites must be enabled.</span></span> <span data-ttu-id="7e299-255">Passerelle d’application utilise la gestion de serveur principal toofor SHA256.</span><span class="sxs-lookup"><span data-stu-id="7e299-255">Application gateway uses SHA256 toofor backend management.</span></span>

* <span data-ttu-id="7e299-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="7e299-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="7e299-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="7e299-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="7e299-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="7e299-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="7e299-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="7e299-262">**Q. Quel est le nombre de certificats SSL pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="7e299-263">Too20 SSL certificats sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7e299-263">Up too20 SSL certificates are supported.</span></span>

<span data-ttu-id="7e299-264">**Q. Quel est le nombre de certificats d’authentification pour le nouveau chiffrement du backend pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="7e299-265">Jusqu'à too10 les certificats d’authentification sont pris en charge avec la valeur par défaut est 5.</span><span class="sxs-lookup"><span data-stu-id="7e299-265">Up too10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="7e299-266">**Q. Application Gateway s’intègre-t-il à Azure Key Vault en mode natif ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="7e299-267">Non, il n’est pas intégré à Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="7e299-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="7e299-268">Configuration du pare-feu d’application web</span><span class="sxs-lookup"><span data-stu-id="7e299-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="7e299-269">**Q. Hello WAF référence (SKU) offre toutes les fonctionnalités de hello disponibles avec hello référence (SKU) Standard ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-269">**Q. Does hello WAF SKU offer all hello features available with hello Standard SKU?**</span></span>

<span data-ttu-id="7e299-270">Oui, WAF prend en charge toutes les fonctionnalités de hello hello référence (SKU) Standard.</span><span class="sxs-lookup"><span data-stu-id="7e299-270">Yes, WAF supports all hello features in hello Standard SKU.</span></span>

<span data-ttu-id="7e299-271">**Q. Quelle est la version CRS hello que prend en charge de la passerelle d’Application ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-271">**Q. What is hello CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="7e299-272">Application Gateway prend en charge CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) et CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="7e299-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="7e299-273">**Q. Comment puis-je surveiller le pare-feu d’application web ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="7e299-274">Le pare-feu d’application web est surveillé via la journalisation des diagnostics. Vous trouverez plus d’informations sur la journalisation des diagnostics dans l’article [Intégrité du serveur principal, journalisation des diagnostics et métriques pour la passerelle Application Gateway](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="7e299-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="7e299-275">**Q. Est-ce que le mode de détection bloque le trafic ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="7e299-276">Non, le mode de détection journalise uniquement le trafic, ce qui a déclenché une règle de pare-feu d’application web.</span><span class="sxs-lookup"><span data-stu-id="7e299-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="7e299-277">**Q. Comment puis-je personnaliser les règles de pare-feu d’application web ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="7e299-278">Oui, les règles WAF sont personnalisables, pour plus d’informations sur comment toocustomize les visitez [WAF de personnaliser les règles et groupes de règles](application-gateway-customize-waf-rules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7e299-278">Yes, WAF rules are customizable, for more information on how toocustomize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="7e299-279">**Q. Quelles sont les règles actuellement disponibles ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="7e299-280">WAF prend actuellement en charge CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) et [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), qui fournissent la sécurité de référence par rapport à la plupart des hello vulnérabilités 10 premiers identifiées par hello ouvrir Web Application sécurité projet (OWASP avoir) est disponible ici [OWASP avoir top 10 vulnérabilités](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="7e299-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of hello top 10 vulnerabilities identified by hello Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="7e299-281">Protection contre les injections de code SQL</span><span class="sxs-lookup"><span data-stu-id="7e299-281">SQL injection protection</span></span>

* <span data-ttu-id="7e299-282">Protection de l’exécution de script de site à site</span><span class="sxs-lookup"><span data-stu-id="7e299-282">Cross site scripting protection</span></span>

* <span data-ttu-id="7e299-283">Protection contre les attaques web courante comme l’injection de commande, les dissimulations de requêtes HTTP, la séparation de réponse HTTP et les attaques RFI (Remote File Inclusion)</span><span class="sxs-lookup"><span data-stu-id="7e299-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="7e299-284">Protection contre les violations de protocole HTTP</span><span class="sxs-lookup"><span data-stu-id="7e299-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="7e299-285">Protection contre les anomalies de protocole HTTP comme un agent-utilisateur hôte manquant et les en-têtes Accept</span><span class="sxs-lookup"><span data-stu-id="7e299-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="7e299-286">Protection contre les robots, les crawlers et les scanneurs</span><span class="sxs-lookup"><span data-stu-id="7e299-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="7e299-287">Détection des erreurs de configuration d’application courantes (par exemple, Apache, IIS, etc.)</span><span class="sxs-lookup"><span data-stu-id="7e299-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="7e299-288">**Q. Le pare-feu d’application web prend-il également en charge la prévention DDoS ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="7e299-289">Non, le pare-feu d’application web ne fournit pas de prévention DDoS.</span><span class="sxs-lookup"><span data-stu-id="7e299-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="7e299-290">Diagnostics et journalisation</span><span class="sxs-lookup"><span data-stu-id="7e299-290">Diagnostics and Logging</span></span>

<span data-ttu-id="7e299-291">**Q. Quels sont les types de journaux disponibles avec Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="7e299-292">Trois journaux sont disponibles pour Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7e299-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="7e299-293">Pour plus d’informations sur ces journaux et d’autres fonctionnalités de diagnostic, consultez l’article [Intégrité backend, journaux des diagnostics et métriques pour la passerelle Application Gateway](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="7e299-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="7e299-294">**ApplicationGatewayAccessLog** -journal d’accès hello contient chaque demande envoyée toohello passerelle d’Application frontale.</span><span class="sxs-lookup"><span data-stu-id="7e299-294">**ApplicationGatewayAccessLog** - hello access log contains each request submitted toohello Application Gateway frontend.</span></span> <span data-ttu-id="7e299-295">les données de salutation incluent IP l’appelant hello, URL demandée, latence de la réponse, code de retour, octets et l’extraction. Le journal d’accès est collecté toutes les 300 secondes.</span><span class="sxs-lookup"><span data-stu-id="7e299-295">hello data includes hello caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="7e299-296">Ce journal contient un enregistrement par instance Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7e299-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="7e299-297">**ApplicationGatewayPerformanceLog** -journal de performances hello capture des informations de performances sur par instance, y compris le total de demandes traitée, le débit en octets, le nombre total de demandes traitées, nombre de demandes ayant échoué et incorrect nombre d’instances de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="7e299-297">**ApplicationGatewayPerformanceLog** - hello performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="7e299-298">**ApplicationGatewayFirewallLog** -journal du pare-feu hello contient des requêtes qui sont enregistrés via le mode de détection ou de prévention d’une passerelle d’application qui est configuré avec un pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="7e299-298">**ApplicationGatewayFirewallLog** - hello firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="7e299-299">**Q. Comment savoir si les membres de mon pool backend sont intègres ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="7e299-300">Vous pouvez utiliser les applets de commande PowerShell hello `Get-AzureRmApplicationGatewayBackendHealth` ou vérifier l’intégrité via le portail de hello en vous rendant sur [Diagnostics de passerelle d’Application](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="7e299-300">You can use hello PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through hello portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="7e299-301">**Q. Quelle est la stratégie de rétention hello sur les journaux de diagnostic hello ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-301">**Q. What is hello retention policy on hello diagnostics logs?**</span></span>

<span data-ttu-id="7e299-302">Compte de stockage de toohello clients des journaux de diagnostic et les clients peuvent définir la stratégie de rétention de hello en fonction de leurs préférences.</span><span class="sxs-lookup"><span data-stu-id="7e299-302">Diagnostic logs flow toohello customers storage account and customers can set hello retention policy based on their preference.</span></span> <span data-ttu-id="7e299-303">Journaux de diagnostic peuvent également être envoyés à tooan concentrateur d’événements ou Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="7e299-303">Diagnostic logs can also be sent tooan Event Hub or Log Analytics.</span></span> <span data-ttu-id="7e299-304">Consultez l’article [Intégrité du serveur principal, journalisation des diagnostics et métriques pour la passerelle Application Gateway](application-gateway-diagnostics.md) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="7e299-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="7e299-305">**Q. Comment puis-je obtenir des journaux d’audit pour Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="7e299-306">Les journaux d’audit sont disponibles pour Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7e299-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="7e299-307">Dans le portail de hello, cliquez sur **le journal d’activité** dans le panneau de menu hello d’un journal d’audit de passerelle d’Application tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="7e299-307">In hello portal, click **Activity Log** in hello menu blade of an Application Gateway tooaccess hello audit log.</span></span> 

<span data-ttu-id="7e299-308">**Q. Puis-je définir des alertes avec Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="7e299-309">Oui, Application Gateway prend en charge les alertes ; les alertes sont configurées à partir des mesures.</span><span class="sxs-lookup"><span data-stu-id="7e299-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="7e299-310">Passerelle d’application n’a actuellement une métrique de « débit », qui peut être tooalert configuré.</span><span class="sxs-lookup"><span data-stu-id="7e299-310">Application Gateway currently has a metric of "throughput", which can be configured tooalert.</span></span> <span data-ttu-id="7e299-311">toolearn en savoir plus sur les alertes, visitez [recevoir des notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="7e299-311">toolearn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="7e299-312">**Q. L’intégrité du serveur principal renvoie un état inconnu, à quoi est dû cet état ?**</span><span class="sxs-lookup"><span data-stu-id="7e299-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="7e299-313">raison la plus courante Hello est accès toohello principal est bloqué par un groupe de sécurité réseau ou le DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="7e299-313">hello most common reason is access toohello backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="7e299-314">Visitez [principal d’intégrité, de journalisation des diagnostics et de mesures pour la passerelle d’Application](application-gateway-diagnostics.md) toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="7e299-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e299-315">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e299-315">Next Steps</span></span>

<span data-ttu-id="7e299-316">toolearn plus sur la passerelle d’Application, visitez [Introduction tooApplication passerelle](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e299-316">toolearn more about Application Gateway visit [Introduction tooApplication Gateway](application-gateway-introduction.md).</span></span>
