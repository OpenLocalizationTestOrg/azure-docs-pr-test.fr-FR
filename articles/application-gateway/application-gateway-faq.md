---
title: Forum aux questions pour Azure Application Gateway | Microsoft Docs
description: "Cette page fournit des réponses aux questions les plus souvent posées sur Azure Application Gateway"
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
ms.openlocfilehash: 4e6244d92f41e0aa5c8a70db0db2881036984247
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="03312-103">Forum aux questions pour Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="03312-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="03312-104">Généralités</span><span class="sxs-lookup"><span data-stu-id="03312-104">General</span></span>

<span data-ttu-id="03312-105">**Q. Qu’est-ce qu’Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="03312-106">Azure Application Gateway est un contrôleur de remise d’application proposé sous la forme d’un service, qui offre diverses fonctionnalités d’équilibrage de charge de couche 7 pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="03312-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="03312-107">Il fournit un service hautement disponible et évolutif, entièrement géré par Azure.</span><span class="sxs-lookup"><span data-stu-id="03312-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="03312-108">**Q. Quelles sont les fonctionnalités prises en charge par Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="03312-109">Application Gateway prend en charge le déchargement SSL et SSL de bout en bout, le pare-feu d’application web, l’affinité de session basée sur les cookies, le routage basé sur le chemin d’accès de l’URL, l’hébergement de plusieurs sites, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="03312-109">Application Gateway supports SSL offloading and end to end SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="03312-110">Pour obtenir une liste complète des fonctionnalités prises en charge, consultez [Vue d’ensemble d’Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="03312-110">For a full list of supported features, visit [Introduction to Application Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="03312-111">**Q. Quelle est la différence entre Application Gateway et Azure Load Balancer ?**</span><span class="sxs-lookup"><span data-stu-id="03312-111">**Q. What is the difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="03312-112">Application Gateway est un équilibreur de charge de couche 7, ce qui signifie qu’il fonctionne avec le trafic web uniquement (HTTP/HTTPS/WebSocket).</span><span class="sxs-lookup"><span data-stu-id="03312-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="03312-113">Il prend en charge des fonctionnalités telles que la terminaison SSL, l’affinité de session basée sur les cookies et le tourniquet (round robin) pour le trafic d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="03312-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="03312-114">Load Balancer équilibre la charge du trafic au niveau de la couche 4 (TCP/UDP).</span><span class="sxs-lookup"><span data-stu-id="03312-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="03312-115">**Q. Quels sont les protocoles pris en charge par Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="03312-116">Application Gateway prend en charge les protocoles HTTP, HTTPS et WebSocket.</span><span class="sxs-lookup"><span data-stu-id="03312-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="03312-117">**Q. Quelles sont les ressources actuellement prises en charge dans le pool backend ?**</span><span class="sxs-lookup"><span data-stu-id="03312-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="03312-118">Les pools backend peuvent être composés de cartes d’interface réseau, de groupes de machines virtuelles identiques, d’adresses IP publiques, d’adresses IP internes, de noms de domaine complets et de serveurs principaux multi-locataires comme Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="03312-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="03312-119">Les membres du pool backend d’Application Gateway ne sont pas liés à un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="03312-119">Application Gateway backend pool members are not tied to an availability set.</span></span> <span data-ttu-id="03312-120">Les membres des pools backend peuvent être sur des clusters, des centres de données ou en dehors d’Azure tant qu’ils disposent d’une connectivité IP.</span><span class="sxs-lookup"><span data-stu-id="03312-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="03312-121">**Q. Dans quelles régions le service est-il disponible ?**</span><span class="sxs-lookup"><span data-stu-id="03312-121">**Q. What regions is the service available in?**</span></span>

<span data-ttu-id="03312-122">Application Gateway est disponible dans toutes les régions de la version globale d’Azure.</span><span class="sxs-lookup"><span data-stu-id="03312-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="03312-123">Il est également disponible dans [Azure en Chine](https://www.azure.cn/) et [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/).</span><span class="sxs-lookup"><span data-stu-id="03312-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="03312-124">**Q. S’agit-il d’un déploiement dédié à mon abonnement ou est-il partagé entre les clients ?**</span><span class="sxs-lookup"><span data-stu-id="03312-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="03312-125">Application Gateway est un déploiement dédié dans votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="03312-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="03312-126">**Q. La redirection HTTP->HTTPS est-elle prise en charge ?**</span><span class="sxs-lookup"><span data-stu-id="03312-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="03312-127">La redirection est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="03312-127">Redirection is supported.</span></span> <span data-ttu-id="03312-128">Consultez la rubrique [Vue d’ensemble de la redirection Application Gateway](application-gateway-redirect-overview.md) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="03312-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) to learn more.</span></span>

<span data-ttu-id="03312-129">**Q. Dans quel ordre les écouteurs sont-ils traités ?**</span><span class="sxs-lookup"><span data-stu-id="03312-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="03312-130">Les écouteurs sont traités selon leur ordre d’affichage.</span><span class="sxs-lookup"><span data-stu-id="03312-130">Listeners are processed in the order they are shown.</span></span> <span data-ttu-id="03312-131">Pour cette raison, si un écouteur de base correspond à une demande entrante, il la traite en premier.</span><span class="sxs-lookup"><span data-stu-id="03312-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="03312-132">Les écouteurs multisites doivent être configurés avant un écouteur élémentaire pour garantir l’acheminement du trafic vers le serveur back-end correct.</span><span class="sxs-lookup"><span data-stu-id="03312-132">Multi-site listeners should be configured before a basic listener to ensure traffic is routed to the correct back-end.</span></span>

<span data-ttu-id="03312-133">**Q. Où puis-je trouver le DNS et l’adresse IP d’Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="03312-134">Lorsque vous utilisez une adresse IP publique en tant que point de terminaison, ces informations sont disponibles dans la ressource d’adresse IP publique ou sur la page de présentation d’Application Gateway dans le portail.</span><span class="sxs-lookup"><span data-stu-id="03312-134">When using a public IP address as an endpoint, this information can be found on the public IP address resource or on the Overview page for the Application Gateway in the portal.</span></span> <span data-ttu-id="03312-135">Si vous utilisez des adresses IP internes, les données se trouvent sur la page de présentation.</span><span class="sxs-lookup"><span data-stu-id="03312-135">For internal IP addresses, this can be found on the Overview page.</span></span>

<span data-ttu-id="03312-136">**Q. Est-ce que l’adresse IP ou le DNS changent au cours de la vie d’Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-136">**Q. Does the IP or DNS change over the lifetime of the Application Gateway?**</span></span>

<span data-ttu-id="03312-137">L’adresse IP virtuelle peut changer si la passerelle est arrêtée et démarrée par le client.</span><span class="sxs-lookup"><span data-stu-id="03312-137">The VIP can change if the gateway is stopped and started by the customer.</span></span> <span data-ttu-id="03312-138">Le DNS associé à Application Gateway ne change pas au cours du cycle de vie de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="03312-138">The DNS associated with Application Gateway does not change over the lifecycle of the gateway.</span></span> <span data-ttu-id="03312-139">Pour cette raison, il est recommandé d’utiliser un alias CNAME et de le pointer vers l’adresse DNS d’Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="03312-139">For this reason, it is recommended to use a CNAME alias and point it to the DNS address of the Application Gateway.</span></span>

<span data-ttu-id="03312-140">**Q. Application Gateway prend-il en charge les adresses IP statiques ?**</span><span class="sxs-lookup"><span data-stu-id="03312-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="03312-141">Non, Application Gateway ne prend pas en charge les adresses IP publiques statiques. Néanmoins, les adresses IP internes statiques sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="03312-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="03312-142">**Q. Application Gateway prend-il en charge plusieurs adresses IP publiques sur la plateforme ?**</span><span class="sxs-lookup"><span data-stu-id="03312-142">**Q. Does Application Gateway support multiple public IPs on the gateway?**</span></span>

<span data-ttu-id="03312-143">Une seule adresse IP publique est prise en charge sur Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="03312-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="03312-144">**Q. Application Gateway prend-il en charge les en-têtes x-forwarded-for ?**</span><span class="sxs-lookup"><span data-stu-id="03312-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="03312-145">Oui, Application Gateway insère les en-têtes x-forwarded-for, x-forwarded-proto et x-forwarded-port dans la demande transmise au backend.</span><span class="sxs-lookup"><span data-stu-id="03312-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into the request forwarded to the backend.</span></span> <span data-ttu-id="03312-146">Le format d’en-tête x-forwarded-for est une liste séparée par des virgules d’éléments IP:Port.</span><span class="sxs-lookup"><span data-stu-id="03312-146">The format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="03312-147">Les valeurs valides pour x-forwarded-proto sont http ou https.</span><span class="sxs-lookup"><span data-stu-id="03312-147">The valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="03312-148">X-forwarded-port spécifie le port atteint par la demande au niveau d’Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="03312-148">X-forwarded-port specifies the port at which the request reached at the Application Gateway.</span></span>

<span data-ttu-id="03312-149">**Q. Combien de temps faut-il pour déployer une Application Gateway ? Mon Application Gateway continue-t-elle de fonctionner après une mise à jour  ?**</span><span class="sxs-lookup"><span data-stu-id="03312-149">**Q. How long does it take to deploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="03312-150">L’approvisionnement de nouveaux déploiements d’Application Gateway peut prendre jusqu’à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="03312-150">New Application Gateway deployments can take up to 20 minutes to provision.</span></span> <span data-ttu-id="03312-151">Les modifications apportées à la taille et au nombre des instances n’entraînent pas d’interruption, et la passerelle reste active pendant ce temps.</span><span class="sxs-lookup"><span data-stu-id="03312-151">Changes to instance size/count are not disruptive, and the gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="03312-152">Configuration</span><span class="sxs-lookup"><span data-stu-id="03312-152">Configuration</span></span>

<span data-ttu-id="03312-153">**Q. Application Gateway est-il toujours déployé dans un réseau virtuel ?**</span><span class="sxs-lookup"><span data-stu-id="03312-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="03312-154">Oui, Application Gateway est toujours déployé dans un sous-réseau de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="03312-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="03312-155">Ce sous-réseau ne peut contenir que des Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="03312-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="03312-156">**Q. Application Gateway peut-il communiquer avec des instances en dehors de son réseau virtuel ?**</span><span class="sxs-lookup"><span data-stu-id="03312-156">**Q. Can Application Gateway talk to instances outside its virtual network?**</span></span>

<span data-ttu-id="03312-157">Application Gateway peut communiquer avec des instances en dehors du réseau virtuel où il se trouve tant qu’une connectivité IP existe.</span><span class="sxs-lookup"><span data-stu-id="03312-157">Application Gateway can talk to instances outside of the virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="03312-158">Si vous prévoyez d’utiliser des adresses IP internes en tant que membres du pool backend, il vous faudra utiliser [VNET Peering](../virtual-network/virtual-network-peering-overview.md) ou [une passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="03312-158">If you plan to use internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="03312-159">**Q. Puis-je déployer autre chose dans le sous-réseau d’Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-159">**Q. Can I deploy anything else in the Application Gateway subnet?**</span></span>

<span data-ttu-id="03312-160">Non, mais vous pouvez déployer d’autres passerelles d’application dans le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="03312-160">No, but you can deploy other application gateways in the subnet.</span></span>

<span data-ttu-id="03312-161">**Q. Les groupes de sécurité réseau sont-ils pris en charge sur le sous-réseau d’Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-161">**Q. Are Network Security Groups supported on the Application Gateway subnet?**</span></span>

<span data-ttu-id="03312-162">Les groupes de sécurité réseau sont pris en charge sur le sous-réseau d’Application Gateway avec les restrictions suivantes :</span><span class="sxs-lookup"><span data-stu-id="03312-162">Network Security Groups are supported on the Application Gateway subnet with the following restrictions:</span></span>

* <span data-ttu-id="03312-163">Des exceptions doivent être imposées au trafic entrant sur les ports 65503-65 534 pour que l’intégrité backend opère correctement.</span><span class="sxs-lookup"><span data-stu-id="03312-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health to work correctly.</span></span>

* <span data-ttu-id="03312-164">La connectivité Internet sortante ne peut pas être bloquée.</span><span class="sxs-lookup"><span data-stu-id="03312-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="03312-165">Le trafic en provenance de la balise AzureLoadBalancer doit être autorisé.</span><span class="sxs-lookup"><span data-stu-id="03312-165">Traffic from the AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="03312-166">**Q. Quelles sont les limites d’Application Gateway ? Puis-je augmenter ces limites ?**</span><span class="sxs-lookup"><span data-stu-id="03312-166">**Q. What are the limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="03312-167">Consultez [Limites d’Application Gateway](../azure-subscription-service-limits.md#application-gateway-limits) pour afficher les limites.</span><span class="sxs-lookup"><span data-stu-id="03312-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) to view the limits.</span></span>

<span data-ttu-id="03312-168">**Q. Puis-je utiliser Application Gateway pour le trafic externe et interne simultanément ?**</span><span class="sxs-lookup"><span data-stu-id="03312-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="03312-169">Oui, Application Gateway peut avoir une adresse IP interne et une adresse IP externe par Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="03312-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="03312-170">**Q. VNET Peering est-il pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="03312-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="03312-171">Oui, VNET Peering est pris en charge et est utile pour équilibrer la charge du trafic des autres réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="03312-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="03312-172">**Q. Puis-je communiquer avec les serveurs locaux lorsqu’ils sont connectés via ExpressRoute ou des tunnels VPN ?**</span><span class="sxs-lookup"><span data-stu-id="03312-172">**Q. Can I talk to on-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="03312-173">Oui, tant que le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="03312-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="03312-174">**Q. Puis-je avoir un pool backend servant plusieurs applications sur des ports différents ?**</span><span class="sxs-lookup"><span data-stu-id="03312-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="03312-175">L’architecture orientée microservices est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="03312-175">Micro service architecture is supported.</span></span> <span data-ttu-id="03312-176">Plusieurs paramètres HTTP doivent être configurés pour une sonde sur différents ports.</span><span class="sxs-lookup"><span data-stu-id="03312-176">You would need multiple http settings configured to probe on different ports.</span></span>

<span data-ttu-id="03312-177">**Q. Les sondes personnalisées prennent-elles en charge les caractères génériques/les expressions régulières sur les données de réponse ?**</span><span class="sxs-lookup"><span data-stu-id="03312-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="03312-178">Les sondes personnalisées ne prennent pas en charge les caractères génériques/les expressions régulières sur les données de réponse.</span><span class="sxs-lookup"><span data-stu-id="03312-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="03312-179">**Q. Comment les règles sont-elles traitées ?**</span><span class="sxs-lookup"><span data-stu-id="03312-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="03312-180">Les règles sont traitées dans l’ordre où elles sont configurées.</span><span class="sxs-lookup"><span data-stu-id="03312-180">Rules are processed in the order they are configured.</span></span> <span data-ttu-id="03312-181">Il est recommandé de configurer les règles multisites avant les règles élémentaires pour réduire les risques que le trafic soit acheminé vers le serveur backend inapproprié si une règle élémentaire mettait en correspondance le trafic basé sur le port avant l’évaluation de la règle multisite.</span><span class="sxs-lookup"><span data-stu-id="03312-181">It is recommended that multi-site rules are configured before basic rules to reduce the chance that traffic is routed to the inappropriate backend as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="03312-182">**Q. Comment les règles sont-elles traitées ?**</span><span class="sxs-lookup"><span data-stu-id="03312-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="03312-183">Les règles sont traitées dans leur ordre de création.</span><span class="sxs-lookup"><span data-stu-id="03312-183">Rules are processed in the order they are created.</span></span> <span data-ttu-id="03312-184">Nous vous recommandons de configurer les règles multi-sites avant les règles de base.</span><span class="sxs-lookup"><span data-stu-id="03312-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="03312-185">En configurant les écouteurs multi-sites en premier, cette configuration réduit les risques que le trafic soit acheminé vers le serveur principal inapproprié.</span><span class="sxs-lookup"><span data-stu-id="03312-185">By configuring multi-site listeners first, this configuration reduces the chance that traffic is routed to the inappropriate backend.</span></span> <span data-ttu-id="03312-186">Ce problème d’acheminement peut se produire car la règle de base correspond au trafic basé sur le port avant que la règle multi-site ne soit évaluée.</span><span class="sxs-lookup"><span data-stu-id="03312-186">This routing issue can occur as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="03312-187">**Q. À quoi correspond le champ Hôte pour les sondes personnalisées ?**</span><span class="sxs-lookup"><span data-stu-id="03312-187">**Q. What does the Host field for custom probes signify?**</span></span>

<span data-ttu-id="03312-188">Le champ Hôte indique le nom auquel envoyer la sonde.</span><span class="sxs-lookup"><span data-stu-id="03312-188">Host field specifies the name to send the probe to.</span></span> <span data-ttu-id="03312-189">S’applique uniquement lorsque plusieurs sites sont configurés sur Application Gateway, sinon utilisez '127.0.0.1'.</span><span class="sxs-lookup"><span data-stu-id="03312-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="03312-190">Cette valeur est différente du nom d’hôte de machine virtuelle et se trouve au format suivant : \<protocole\>://\<hôte\>:\<port\>\<chemin d’accès\>.</span><span class="sxs-lookup"><span data-stu-id="03312-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="03312-191">**Q. Puis-je autoriser quelques adresses IP de sources à accéder à Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-191">**Q. Can I whitelist Application Gateway access to a few source IPs?**</span></span>

<span data-ttu-id="03312-192">Ce scénario peut être réalisé en utilisant des groupes de sécurité réseau sur le sous-réseau d’Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="03312-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="03312-193">Les restrictions suivantes doivent être imposées au sous-réseau dans l’ordre de priorité indiqué :</span><span class="sxs-lookup"><span data-stu-id="03312-193">The following restrictions should be put on the subnet in the listed order of priority:</span></span>

* <span data-ttu-id="03312-194">Autoriser le trafic entrant à partir de l’adresse IP ou de la plage d’adresses IP sources.</span><span class="sxs-lookup"><span data-stu-id="03312-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="03312-195">Autoriser les demandes entrantes de toutes sources aux ports 65503-65 534 pour les [communications relatives à l’intégrité backend](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="03312-195">Allow incoming requests from all sources to ports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="03312-196">Autoriser les sondes entrantes d’Azure Load Balancer (balise AzureLoadBalancer) et le trafic réseau virtuel entrant (balise VirtualNetwork) sur le [Groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="03312-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on the [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="03312-197">Bloquer tout autre trafic entrant avec une règle Refuser tout.</span><span class="sxs-lookup"><span data-stu-id="03312-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="03312-198">Autoriser le trafic sortant vers internet pour toutes les destinations.</span><span class="sxs-lookup"><span data-stu-id="03312-198">Allow outbound traffic to the internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="03312-199">Performances</span><span class="sxs-lookup"><span data-stu-id="03312-199">Performance</span></span>

<span data-ttu-id="03312-200">**Q. Comment Application Gateway prend-il en charge la haute disponibilité et l’évolutivité ?**</span><span class="sxs-lookup"><span data-stu-id="03312-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="03312-201">Application Gateway prend en charge les scénarios de haute disponibilité lorsque vous avez deux instances déployées ou plus.</span><span class="sxs-lookup"><span data-stu-id="03312-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="03312-202">Azure distribue ces instances entre les domaines de mise à jour et d’erreur pour garantir que toutes les instances n’échouent pas en même temps.</span><span class="sxs-lookup"><span data-stu-id="03312-202">Azure distributes these instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="03312-203">Application Gateway prend en charge l’évolutivité en ajoutant plusieurs instances de la même passerelle pour partager la charge.</span><span class="sxs-lookup"><span data-stu-id="03312-203">Application Gateway supports scalability by adding multiple instances of the same gateway to share the load.</span></span>

<span data-ttu-id="03312-204">**Q. Comment puis-je obtenir le scénario de récupération d’urgence dans les centres de données avec Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="03312-205">Les clients peuvent utiliser Traffic Manager pour répartir le trafic entre plusieurs Application Gateway dans différents centres de données.</span><span class="sxs-lookup"><span data-stu-id="03312-205">Customers can use Traffic Manager to distribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="03312-206">**Q. La mise à l’échelle automatique est-elle prise en charge ?**</span><span class="sxs-lookup"><span data-stu-id="03312-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="03312-207">Non, mais Application Gateway a une mesure de débit qui peut être utilisée pour vous avertir lorsqu’un seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="03312-207">No, but Application Gateway has a throughput metric that can be used to alert you when a threshold is reached.</span></span> <span data-ttu-id="03312-208">Les opérations d’ajout d’instances ou de modification de la taille effectuées manuellement ne redémarrent pas la passerelle et n’affectent pas le trafic existant.</span><span class="sxs-lookup"><span data-stu-id="03312-208">Manually adding instances or changing size does not restart the gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="03312-209">**Q. Est-ce que les opérations de montée/descente en puissance effectuées manuellement interrompent le service ?**</span><span class="sxs-lookup"><span data-stu-id="03312-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="03312-210">Aucune interruption de service n’a lieu, les instances sont réparties entre les domaines de mise à niveau et les domaines d’erreur.</span><span class="sxs-lookup"><span data-stu-id="03312-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="03312-211">**Q. Puis-je passer d’une taille d’instance moyenne à une taille d’instance grande sans interruption de service ?**</span><span class="sxs-lookup"><span data-stu-id="03312-211">**Q. Can I change instance size from medium to large without disruption?**</span></span>

<span data-ttu-id="03312-212">Oui, Azure distribue les instances entre les domaines de mise à jour et d’erreur pour garantir que toutes les instances n’échouent pas en même temps.</span><span class="sxs-lookup"><span data-stu-id="03312-212">Yes, Azure distributes instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="03312-213">Application Gateway prend en charge la mise à l’échelle en ajoutant plusieurs instances de la même passerelle pour partager la charge.</span><span class="sxs-lookup"><span data-stu-id="03312-213">Application Gateway supports scaling by adding multiple instances of the same gateway to share the load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="03312-214">Configuration SSL</span><span class="sxs-lookup"><span data-stu-id="03312-214">SSL Configuration</span></span>

<span data-ttu-id="03312-215">**Q. Quels sont les certificats pris en charge sur Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="03312-216">Les certificats auto-signés, les certificats d’autorité de certification et les certificats génériques sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="03312-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="03312-217">Les certificats de validation étendue ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="03312-217">EV certs are not supported.</span></span>

<span data-ttu-id="03312-218">**Q. Quelles sont les suites de chiffrement actuellement prises en charge par Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-218">**Q. What are the current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="03312-219">Vous trouverez ci-dessous les suites de chiffrement actuellement prises en charge par Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="03312-219">The following are the current cipher suites supported by application gateway.</span></span> <span data-ttu-id="03312-220">Visitez la page [Configurer les versions de stratégie SSL et les suites de chiffrement sur Application Gateway](application-gateway-configure-ssl-policy-powershell.md) pour apprendre à personnaliser les options SSL.</span><span class="sxs-lookup"><span data-stu-id="03312-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn how to customize SSL options.</span></span>

- <span data-ttu-id="03312-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="03312-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="03312-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="03312-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="03312-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="03312-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="03312-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="03312-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="03312-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="03312-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="03312-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="03312-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="03312-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="03312-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="03312-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="03312-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="03312-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="03312-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="03312-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="03312-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="03312-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="03312-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="03312-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="03312-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="03312-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="03312-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="03312-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="03312-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="03312-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="03312-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="03312-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="03312-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="03312-247">**Q. Application Gateway prend-il également en charge le nouveau chiffrement du trafic vers le serveur principal ?**</span><span class="sxs-lookup"><span data-stu-id="03312-247">**Q. Does Application Gateway also support re-encryption of traffic to the backend?**</span></span>

<span data-ttu-id="03312-248">Oui, Application Gateway prend en charge le déchargement SSL et SSL de bout en bout, qui chiffre à nouveau le trafic vers le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="03312-248">Yes, Application Gateway supports SSL offload, and end to end SSL, which re-encrypts the traffic to the backend.</span></span>

<span data-ttu-id="03312-249">**Q. Puis-je configurer la stratégie SSL pour contrôler les versions du protocole SSL ?**</span><span class="sxs-lookup"><span data-stu-id="03312-249">**Q. Can I configure SSL policy to control SSL Protocol versions?**</span></span>

<span data-ttu-id="03312-250">Oui, vous pouvez configurer Application Gateway pour refuser TLS1.0, TLS1.1 et TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="03312-250">Yes, you can configure Application Gateway to deny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="03312-251">SSL 2.0 et 3.0 sont déjà désactivés par défaut et ne sont pas configurables.</span><span class="sxs-lookup"><span data-stu-id="03312-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="03312-252">**Q. Puis-je configurer les suites de chiffrement et l’ordre de la stratégie ?**</span><span class="sxs-lookup"><span data-stu-id="03312-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="03312-253">Oui, la [configuration des suites de chiffrement](application-gateway-ssl-policy-overview.md) est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="03312-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="03312-254">Lorsque vous définissez une stratégie personnalisée, au moins une des suites de chiffrement suivantes doit être activée.</span><span class="sxs-lookup"><span data-stu-id="03312-254">When defining a custom policy, at least one of the following cipher suites must be enabled.</span></span> <span data-ttu-id="03312-255">Application Gateway utilise SHA256 pour la gestion des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="03312-255">Application gateway uses SHA256 to for backend management.</span></span>

* <span data-ttu-id="03312-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="03312-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="03312-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="03312-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="03312-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="03312-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="03312-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="03312-262">**Q. Quel est le nombre de certificats SSL pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="03312-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="03312-263">20 certificats SSL maximum sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="03312-263">Up to 20 SSL certificates are supported.</span></span>

<span data-ttu-id="03312-264">**Q. Quel est le nombre de certificats d’authentification pour le nouveau chiffrement du backend pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="03312-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="03312-265">10 certificats d’authentification maximum sont pris en charge, dont 5 par défaut.</span><span class="sxs-lookup"><span data-stu-id="03312-265">Up to 10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="03312-266">**Q. Application Gateway s’intègre-t-il à Azure Key Vault en mode natif ?**</span><span class="sxs-lookup"><span data-stu-id="03312-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="03312-267">Non, il n’est pas intégré à Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="03312-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="03312-268">Configuration du pare-feu d’application web</span><span class="sxs-lookup"><span data-stu-id="03312-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="03312-269">**Q. La référence de pare-feu d’application web propose-t-elle toutes les fonctionnalités disponibles avec la référence Standard ?**</span><span class="sxs-lookup"><span data-stu-id="03312-269">**Q. Does the WAF SKU offer all the features available with the Standard SKU?**</span></span>

<span data-ttu-id="03312-270">Oui, le pare-feu d’application web prend en charge toutes les fonctionnalités de la référence Standard.</span><span class="sxs-lookup"><span data-stu-id="03312-270">Yes, WAF supports all the features in the Standard SKU.</span></span>

<span data-ttu-id="03312-271">**Q. Quelle est la version CRS qu’Application Gateway prend en charge ?**</span><span class="sxs-lookup"><span data-stu-id="03312-271">**Q. What is the CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="03312-272">Application Gateway prend en charge CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) et CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="03312-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="03312-273">**Q. Comment puis-je surveiller le pare-feu d’application web ?**</span><span class="sxs-lookup"><span data-stu-id="03312-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="03312-274">Le pare-feu d’application web est surveillé via la journalisation des diagnostics. Vous trouverez plus d’informations sur la journalisation des diagnostics dans l’article [Intégrité du serveur principal, journalisation des diagnostics et métriques pour la passerelle Application Gateway](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="03312-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="03312-275">**Q. Est-ce que le mode de détection bloque le trafic ?**</span><span class="sxs-lookup"><span data-stu-id="03312-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="03312-276">Non, le mode de détection journalise uniquement le trafic, ce qui a déclenché une règle de pare-feu d’application web.</span><span class="sxs-lookup"><span data-stu-id="03312-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="03312-277">**Q. Comment puis-je personnaliser les règles de pare-feu d’application web ?**</span><span class="sxs-lookup"><span data-stu-id="03312-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="03312-278">Oui, les règles WAF sont personnalisables. Pour plus d’informations sur la façon de les personnaliser, rendez-vous sur [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md) (Personnaliser les règles et groupes de règles WAF)</span><span class="sxs-lookup"><span data-stu-id="03312-278">Yes, WAF rules are customizable, for more information on how to customize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="03312-279">**Q. Quelles sont les règles actuellement disponibles ?**</span><span class="sxs-lookup"><span data-stu-id="03312-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="03312-280">Le pare-feu d’application web prend actuellement en charge CRS  [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) et [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), qui fournit la sécurité de ligne de base pour la plupart des 3.0 premières vulnérabilités identifiées par l’OWASP, présentées ici [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013) (10 premières vulnérabilités identifiées par l’OWASP)</span><span class="sxs-lookup"><span data-stu-id="03312-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of the top 10 vulnerabilities identified by the Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="03312-281">Protection contre les injections de code SQL</span><span class="sxs-lookup"><span data-stu-id="03312-281">SQL injection protection</span></span>

* <span data-ttu-id="03312-282">Protection de l’exécution de script de site à site</span><span class="sxs-lookup"><span data-stu-id="03312-282">Cross site scripting protection</span></span>

* <span data-ttu-id="03312-283">Protection contre les attaques web courante comme l’injection de commande, les dissimulations de requêtes HTTP, la séparation de réponse HTTP et les attaques RFI (Remote File Inclusion)</span><span class="sxs-lookup"><span data-stu-id="03312-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="03312-284">Protection contre les violations de protocole HTTP</span><span class="sxs-lookup"><span data-stu-id="03312-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="03312-285">Protection contre les anomalies de protocole HTTP comme un agent-utilisateur hôte manquant et les en-têtes Accept</span><span class="sxs-lookup"><span data-stu-id="03312-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="03312-286">Protection contre les robots, les crawlers et les scanneurs</span><span class="sxs-lookup"><span data-stu-id="03312-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="03312-287">Détection des erreurs de configuration d’application courantes (par exemple, Apache, IIS, etc.)</span><span class="sxs-lookup"><span data-stu-id="03312-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="03312-288">**Q. Le pare-feu d’application web prend-il également en charge la prévention DDoS ?**</span><span class="sxs-lookup"><span data-stu-id="03312-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="03312-289">Non, le pare-feu d’application web ne fournit pas de prévention DDoS.</span><span class="sxs-lookup"><span data-stu-id="03312-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="03312-290">Diagnostics et journalisation</span><span class="sxs-lookup"><span data-stu-id="03312-290">Diagnostics and Logging</span></span>

<span data-ttu-id="03312-291">**Q. Quels sont les types de journaux disponibles avec Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="03312-292">Trois journaux sont disponibles pour Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="03312-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="03312-293">Pour plus d’informations sur ces journaux et d’autres fonctionnalités de diagnostic, consultez l’article [Intégrité backend, journaux des diagnostics et métriques pour la passerelle Application Gateway](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="03312-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="03312-294">**ApplicationGatewayAccessLog** : le journal d’accès contient toutes les demandes envoyées au serveur frontal d’Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="03312-294">**ApplicationGatewayAccessLog** - The access log contains each request submitted to the Application Gateway frontend.</span></span> <span data-ttu-id="03312-295">Les données incluent l’adresse IP de l’appelant, l’URL demandée, la latence de réponse, le code de retour, les octets d’entrée et de sortie. Le journal d’accès est collecté toutes les 300 secondes.</span><span class="sxs-lookup"><span data-stu-id="03312-295">The data includes the caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="03312-296">Ce journal contient un enregistrement par instance Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="03312-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="03312-297">**ApplicationGatewayPerformanceLog** : le journal des performances capture des informations sur les performances par instance, notamment le nombre total de demandes traitées, le débit en octets, le nombre total de demandes présentées, le nombre de demandes ayant échoué, le nombre d’instances du serveur principal correctes et incorrectes.</span><span class="sxs-lookup"><span data-stu-id="03312-297">**ApplicationGatewayPerformanceLog** - The performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="03312-298">**ApplicationGatewayFirewallLog** : le journal des pare-feux contient les demandes consignées via le mode de détection ou de prévention d’une passerelle d’application configuré avec un pare-feu d’application web.</span><span class="sxs-lookup"><span data-stu-id="03312-298">**ApplicationGatewayFirewallLog** - The firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="03312-299">**Q. Comment savoir si les membres de mon pool backend sont intègres ?**</span><span class="sxs-lookup"><span data-stu-id="03312-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="03312-300">Vous pouvez utiliser l’applet de commande PowerShell `Get-AzureRmApplicationGatewayBackendHealth` ou vérifier l’intégrité via le portail en consultant l’article [Intégrité backend, journalisation des diagnostics et métriques pour la passerelle Application Gateway](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="03312-300">You can use the PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through the portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="03312-301">**Q. Quelle est la stratégie de rétention sur les journaux de diagnostic ?**</span><span class="sxs-lookup"><span data-stu-id="03312-301">**Q. What is the retention policy on the diagnostics logs?**</span></span>

<span data-ttu-id="03312-302">Les journaux de diagnostic circulent vers le compte de stockage des clients, et les clients peuvent définir la stratégie de rétention en fonction de leurs préférences.</span><span class="sxs-lookup"><span data-stu-id="03312-302">Diagnostic logs flow to the customers storage account and customers can set the retention policy based on their preference.</span></span> <span data-ttu-id="03312-303">Les journaux de diagnostic peuvent également être envoyés à un Event Hub ou Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="03312-303">Diagnostic logs can also be sent to an Event Hub or Log Analytics.</span></span> <span data-ttu-id="03312-304">Consultez l’article [Intégrité du serveur principal, journalisation des diagnostics et métriques pour la passerelle Application Gateway](application-gateway-diagnostics.md) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="03312-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="03312-305">**Q. Comment puis-je obtenir des journaux d’audit pour Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="03312-306">Les journaux d’audit sont disponibles pour Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="03312-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="03312-307">Dans le portail, cliquez sur **Journal d’activité** dans le panneau de menu d’Application Gateway pour accéder au journal d’audit.</span><span class="sxs-lookup"><span data-stu-id="03312-307">In the portal, click **Activity Log** in the menu blade of an Application Gateway to access the audit log.</span></span> 

<span data-ttu-id="03312-308">**Q. Puis-je définir des alertes avec Application Gateway ?**</span><span class="sxs-lookup"><span data-stu-id="03312-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="03312-309">Oui, Application Gateway prend en charge les alertes ; les alertes sont configurées à partir des mesures.</span><span class="sxs-lookup"><span data-stu-id="03312-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="03312-310">Application Gateway possède actuellement une mesure de « débit », qui peut être configurée pour avertir l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="03312-310">Application Gateway currently has a metric of "throughput", which can be configured to alert.</span></span> <span data-ttu-id="03312-311">Pour en savoir plus sur les alertes, consultez l’article [Réception de notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="03312-311">To learn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="03312-312">**Q. L’intégrité du serveur principal renvoie un état inconnu, à quoi est dû cet état ?**</span><span class="sxs-lookup"><span data-stu-id="03312-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="03312-313">La raison la plus courante est le blocage de l’accès au serveur principal par un groupe de sécurité réseau ou un DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="03312-313">The most common reason is access to the backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="03312-314">Consultez l’article [Intégrité du serveur principal, journalisation des diagnostics et métriques pour la passerelle Application Gateway](application-gateway-diagnostics.md) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="03312-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03312-315">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="03312-315">Next Steps</span></span>

<span data-ttu-id="03312-316">Pour en savoir plus sur Application Gateway, consultez [Vue d’ensemble d’Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="03312-316">To learn more about Application Gateway visit [Introduction to Application Gateway](application-gateway-introduction.md).</span></span>
