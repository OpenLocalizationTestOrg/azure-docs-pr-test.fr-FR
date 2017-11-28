---
title: aaaWhat est Traffic Manager | Documents Microsoft
description: "Cet article vous aidera à comprendre les nouveautés de Traffic Manager, et s’il s’agit des choix de routage de trafic droite hello pour votre application"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a><span data-ttu-id="74ed7-103">Vue d’ensemble de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="74ed7-103">Overview of Traffic Manager</span></span>

<span data-ttu-id="74ed7-104">Microsoft Azure Traffic Manager vous permet de distribution de hello toocontrol du trafic utilisateur pour les points de terminaison de service dans différents centres de données.</span><span class="sxs-lookup"><span data-stu-id="74ed7-104">Microsoft Azure Traffic Manager allows you toocontrol hello distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="74ed7-105">Les points de terminaison de service pris en charge par Traffic Manager incluent des machines virtuelles Azure, des applications web et des services cloud.</span><span class="sxs-lookup"><span data-stu-id="74ed7-105">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="74ed7-106">Vous pouvez également utiliser Traffic Manager avec des points de terminaison externes non-Azure.</span><span class="sxs-lookup"><span data-stu-id="74ed7-106">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="74ed7-107">Traffic Manager utilise hello système DNS (Domain Name) toodirect demandes toohello plus approprié point de terminaison client basé sur une méthode de routage du trafic et d’un contrôle d’intégrité hello de points de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="74ed7-107">Traffic Manager uses hello Domain Name System (DNS) toodirect client requests toohello most appropriate endpoint based on a traffic-routing method and hello health of hello endpoints.</span></span> <span data-ttu-id="74ed7-108">Traffic Manager fournit une gamme de [des méthodes de routage de trafic](traffic-manager-routing-methods.md) et [options de surveillance de point de terminaison](traffic-manager-monitoring.md) toosuit une autre application besoins et des modèles de basculement automatique.</span><span class="sxs-lookup"><span data-stu-id="74ed7-108">Traffic Manager provides a range of [traffic-routing methods](traffic-manager-routing-methods.md) and [endpoint monitoring options](traffic-manager-monitoring.md) toosuit different application needs and automatic failover models.</span></span> <span data-ttu-id="74ed7-109">Traffic Manager est résilient toofailure, y compris échec hello d’un ensemble de la région Azure.</span><span class="sxs-lookup"><span data-stu-id="74ed7-109">Traffic Manager is resilient toofailure, including hello failure of an entire Azure region.</span></span>

## <a name="traffic-manager-benefits"></a><span data-ttu-id="74ed7-110">Avantages de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="74ed7-110">Traffic Manager benefits</span></span>

<span data-ttu-id="74ed7-111">Traffic Manager peut vous aider à atteindre les objectifs suivants :</span><span class="sxs-lookup"><span data-stu-id="74ed7-111">Traffic Manager can help you:</span></span>

* <span data-ttu-id="74ed7-112">**Améliorer la disponibilité des applications critiques**</span><span class="sxs-lookup"><span data-stu-id="74ed7-112">**Improve availability of critical applications**</span></span>

    <span data-ttu-id="74ed7-113">Traffic Manager vous permet de garantir une haute disponibilité de vos applications en surveillant vos points de terminaison et en fournissant un basculement automatique en cas de panne d’un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="74ed7-113">Traffic Manager delivers high availability for your applications by monitoring your endpoints and providing automatic failover when an endpoint goes down.</span></span>

* <span data-ttu-id="74ed7-114">**Améliorer la réactivité des applications haute performance**</span><span class="sxs-lookup"><span data-stu-id="74ed7-114">**Improve responsiveness for high-performance applications**</span></span>

    <span data-ttu-id="74ed7-115">Azure vous permet de toorun les services de cloud computing ou sites Web dans des centres de données situés monde hello.</span><span class="sxs-lookup"><span data-stu-id="74ed7-115">Azure allows you toorun cloud services or websites in datacenters located around hello world.</span></span> <span data-ttu-id="74ed7-116">Traffic Manager permet d’améliorer la réactivité des applications en dirigeant le point de terminaison du trafic toohello avec une latence réseau la plus basse hello pour les clients hello.</span><span class="sxs-lookup"><span data-stu-id="74ed7-116">Traffic Manager improves application responsiveness by directing traffic toohello endpoint with hello lowest network latency for hello client.</span></span>

* <span data-ttu-id="74ed7-117">**Gérer les services sans les interrompre**</span><span class="sxs-lookup"><span data-stu-id="74ed7-117">**Perform service maintenance without downtime**</span></span>

    <span data-ttu-id="74ed7-118">Vous pouvez effectuer les opérations de maintenance planifiée sur vos applications sans temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="74ed7-118">You can perform planned maintenance operations on your applications without downtime.</span></span> <span data-ttu-id="74ed7-119">Traffic Manager dirige les points de terminaison tooalternative le trafic pendant la maintenance de hello.</span><span class="sxs-lookup"><span data-stu-id="74ed7-119">Traffic Manager directs traffic tooalternative endpoints while hello maintenance is in progress.</span></span>

* <span data-ttu-id="74ed7-120">**Combiner des applications cloud et locales**</span><span class="sxs-lookup"><span data-stu-id="74ed7-120">**Combine on-premises and Cloud-based applications**</span></span>

    <span data-ttu-id="74ed7-121">Traffic Manager prend en charge externe, les points de terminaison non-Azure lui toobe utilisé avec hybride de cloud computing et les scénarios de « basculement au cloud » et les déploiements, y compris hello « croissance dans le cloud, » « migrer dans le cloud, » local.</span><span class="sxs-lookup"><span data-stu-id="74ed7-121">Traffic Manager supports external, non-Azure endpoints enabling it toobe used with hybrid cloud and on-premises deployments, including hello "burst-to-cloud," "migrate-to-cloud," and "failover-to-cloud" scenarios.</span></span>

* <span data-ttu-id="74ed7-122">**Distribuer le trafic pour des déploiements vastes et complexes**</span><span class="sxs-lookup"><span data-stu-id="74ed7-122">**Distribute traffic for large, complex deployments**</span></span>

    <span data-ttu-id="74ed7-123">À l’aide de [imbriqués profils Traffic Manager](traffic-manager-nested-profiles.md), méthodes de routage du trafic peuvent être combiné toocreate sophistiquées et hello toosupport de règles souples doit des déploiements plus volumineux et plus complexes.</span><span class="sxs-lookup"><span data-stu-id="74ed7-123">Using [nested Traffic Manager profiles](traffic-manager-nested-profiles.md), traffic-routing methods can be combined toocreate sophisticated and flexible rules toosupport hello needs of larger, more complex deployments.</span></span>

## <a name="how-traffic-manager-works"></a><span data-ttu-id="74ed7-124">Fonctionnement de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="74ed7-124">How Traffic Manager works</span></span>

<span data-ttu-id="74ed7-125">Azure Traffic Manager vous permet de distribution de hello toocontrol du trafic entre les points de terminaison de votre application.</span><span class="sxs-lookup"><span data-stu-id="74ed7-125">Azure Traffic Manager enables you toocontrol hello distribution of traffic across your application endpoints.</span></span> <span data-ttu-id="74ed7-126">Un point de terminaison est tout service côté Internet hébergé à l’intérieur ou à l’extérieur d’Azure.</span><span class="sxs-lookup"><span data-stu-id="74ed7-126">An endpoint is any Internet-facing service hosted inside or outside of Azure.</span></span>

<span data-ttu-id="74ed7-127">Traffic Manager offre deux principaux avantages :</span><span class="sxs-lookup"><span data-stu-id="74ed7-127">Traffic Manager provides two key benefits:</span></span>

1. <span data-ttu-id="74ed7-128">Distribution du trafic en fonction de tooone de plusieurs [des méthodes de routage de trafic](traffic-manager-routing-methods.md)</span><span class="sxs-lookup"><span data-stu-id="74ed7-128">Distribution of traffic according tooone of several [traffic-routing methods](traffic-manager-routing-methods.md)</span></span>
2. <span data-ttu-id="74ed7-129">[Analyse continue de l’intégrité des points de terminaison](traffic-manager-monitoring.md) et basculement automatique en cas d’échec des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="74ed7-129">[Continuous monitoring of endpoint health](traffic-manager-monitoring.md) and automatic failover when endpoints fail</span></span>

<span data-ttu-id="74ed7-130">Lorsqu’un client essaie tooconnect tooa service, il doit tout d’abord résoudre le nom DNS de hello d’adresse IP de hello service tooan.</span><span class="sxs-lookup"><span data-stu-id="74ed7-130">When a client attempts tooconnect tooa service, it must first resolve hello DNS name of hello service tooan IP address.</span></span> <span data-ttu-id="74ed7-131">Hello puis se connecte le service hello tooaccess toothat IP adresse.</span><span class="sxs-lookup"><span data-stu-id="74ed7-131">hello client then connects toothat IP address tooaccess hello service.</span></span>

<span data-ttu-id="74ed7-132">**toounderstand de point Hello plus important est que Traffic Manager fonctionne au niveau DNS hello.**</span><span class="sxs-lookup"><span data-stu-id="74ed7-132">**hello most important point toounderstand is that Traffic Manager works at hello DNS level.**</span></span>  <span data-ttu-id="74ed7-133">Traffic Manager utilise DNS toodirect clients toospecific des points de terminaison en fonction des règles hello de méthode de routage du trafic hello.</span><span class="sxs-lookup"><span data-stu-id="74ed7-133">Traffic Manager uses DNS toodirect clients toospecific service endpoints based on hello rules of hello traffic-routing method.</span></span> <span data-ttu-id="74ed7-134">Les clients connectent de point de terminaison toohello sélectionné **directement**.</span><span class="sxs-lookup"><span data-stu-id="74ed7-134">Clients connect toohello selected endpoint **directly**.</span></span> <span data-ttu-id="74ed7-135">Traffic Manager n’est pas un proxy ou une passerelle.</span><span class="sxs-lookup"><span data-stu-id="74ed7-135">Traffic Manager is not a proxy or a gateway.</span></span> <span data-ttu-id="74ed7-136">Traffic Manager ne voit pas de trafic hello entre le client de hello et le service de hello.</span><span class="sxs-lookup"><span data-stu-id="74ed7-136">Traffic Manager does not see hello traffic passing between hello client and hello service.</span></span>

### <a name="traffic-manager-example"></a><span data-ttu-id="74ed7-137">Exemple Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="74ed7-137">Traffic Manager example</span></span>

<span data-ttu-id="74ed7-138">Contoso Corp a développé un nouveau portail pour ses partenaires.</span><span class="sxs-lookup"><span data-stu-id="74ed7-138">Contoso Corp have developed a new partner portal.</span></span> <span data-ttu-id="74ed7-139">URL de Hello pour ce portail est https://partners.contoso.com/login.aspx.</span><span class="sxs-lookup"><span data-stu-id="74ed7-139">hello URL for this portal is https://partners.contoso.com/login.aspx.</span></span> <span data-ttu-id="74ed7-140">application Hello est hébergée dans trois régions Azure.</span><span class="sxs-lookup"><span data-stu-id="74ed7-140">hello application is hosted in three regions of Azure.</span></span> <span data-ttu-id="74ed7-141">disponibilité de tooimprove et optimiser les performances globales, ils utilisent Traffic Manager toodistribute trafic toohello le plus proche disponible point de terminaison client.</span><span class="sxs-lookup"><span data-stu-id="74ed7-141">tooimprove availability and maximize global performance, they use Traffic Manager toodistribute client traffic toohello closest available endpoint.</span></span>

<span data-ttu-id="74ed7-142">tooachieve cette configuration, elles terminent hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="74ed7-142">tooachieve this configuration, they complete hello following steps:</span></span>

1. <span data-ttu-id="74ed7-143">Ils déploient trois instances de leur service.</span><span class="sxs-lookup"><span data-stu-id="74ed7-143">Deploy three instances of their service.</span></span> <span data-ttu-id="74ed7-144">Hello DNS noms de ces déploiements sont « contoso-us.cloudapp .net », « contoso-eu.cloudapp .net », « contoso-asia.cloudapp .net ».</span><span class="sxs-lookup"><span data-stu-id="74ed7-144">hello DNS names of these deployments are 'contoso-us.cloudapp.net', 'contoso-eu.cloudapp.net', and 'contoso-asia.cloudapp.net'.</span></span>
2. <span data-ttu-id="74ed7-145">Créer un profil Traffic Manager, nommé « contoso.trafficmanager.net » et configurez-le toouse (méthode) hello « Performances »-le routage du trafic entre les points de terminaison hello trois.</span><span class="sxs-lookup"><span data-stu-id="74ed7-145">Create a Traffic Manager profile, named 'contoso.trafficmanager.net', and configure it toouse hello 'Performance' traffic-routing method across hello three endpoints.</span></span>
* <span data-ttu-id="74ed7-146">Configurer leur nom de domaine personnel, 'partners.contoso.com' toopoint too'contoso.trafficmanager.net », à l’aide d’un enregistrement DNS CNAME.</span><span class="sxs-lookup"><span data-stu-id="74ed7-146">Configure their vanity domain name, 'partners.contoso.com', toopoint too'contoso.trafficmanager.net', using a DNS CNAME record.</span></span>

![Configuration DNS de Traffic Manager][1]

> [!NOTE]
> <span data-ttu-id="74ed7-148">Lorsque vous utilisez un domaine personnel avec Azure Traffic Manager, vous devez utiliser un toopoint CNAME votre nom de domaine personnel domaine nom tooyour Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="74ed7-148">When using a vanity domain with Azure Traffic Manager, you must use a CNAME toopoint your vanity domain name tooyour Traffic Manager domain name.</span></span> <span data-ttu-id="74ed7-149">Les normes DNS ne vous permettent pas toocreate un enregistrement CNAME à hello 'apex' (ou racine) d’un domaine.</span><span class="sxs-lookup"><span data-stu-id="74ed7-149">DNS standards do not allow you toocreate a CNAME at hello 'apex' (or root) of a domain.</span></span> <span data-ttu-id="74ed7-150">Par conséquent, vous ne pouvez pas créer d’enregistrement CNAME pour « contoso.com » (parfois appelé un domaine « nu »).</span><span class="sxs-lookup"><span data-stu-id="74ed7-150">Thus you cannot create a CNAME for 'contoso.com' (sometimes called a 'naked' domain).</span></span> <span data-ttu-id="74ed7-151">Vous pouvez uniquement créer un enregistrement CNAME pour un domaine sous « contoso.com », tel que « www.contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="74ed7-151">You can only create a CNAME for a domain under 'contoso.com', such as 'www.contoso.com'.</span></span> <span data-ttu-id="74ed7-152">toowork contourner cette limitation, nous recommandons d’utiliser un simples demandes toodirect de redirection HTTP pour « contoso.com » tooan autre nom tel que « www.contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="74ed7-152">toowork around this limitation, we recommend using a simple HTTP redirect toodirect requests for 'contoso.com' tooan alternative name such as 'www.contoso.com'.</span></span>

### <a name="how-clients-connect-using-traffic-manager"></a><span data-ttu-id="74ed7-153">Connexion des clients à l’aide de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="74ed7-153">How clients connect using Traffic Manager</span></span>

<span data-ttu-id="74ed7-154">Reprenons l’exemple précédent de hello, lorsqu’un client demande hello page https://partners.contoso.com/login.aspx, le client de hello effectue hello suivant le nom DNS d’étapes tooresolve hello et établir une connexion :</span><span class="sxs-lookup"><span data-stu-id="74ed7-154">Continuing from hello previous example, when a client requests hello page https://partners.contoso.com/login.aspx, hello client performs hello following steps tooresolve hello DNS name and establish a connection:</span></span>

![Établissement de la connexion à l’aide de Traffic Manager][2]

1. <span data-ttu-id="74ed7-156">Hello en envoyant une récursive de tooits configuré de requête DNS DNS service tooresolve hello nom 'partners.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="74ed7-156">hello client sends a DNS query tooits configured recursive DNS service tooresolve hello name 'partners.contoso.com'.</span></span> <span data-ttu-id="74ed7-157">Un service DNS récursif, parfois appelé service « DNS local », n’héberge pas directement de domaines DNS.</span><span class="sxs-lookup"><span data-stu-id="74ed7-157">A recursive DNS service, sometimes called a 'local DNS' service, does not host DNS domains directly.</span></span> <span data-ttu-id="74ed7-158">Au lieu de cela, les clients hello transfère le travail de hello de contact hello DNS faisant autorité différents services sur hello Internet nécessaire tooresolve un nom DNS.</span><span class="sxs-lookup"><span data-stu-id="74ed7-158">Rather, hello client off-loads hello work of contacting hello various authoritative DNS services across hello Internet needed tooresolve a DNS name.</span></span>
2. <span data-ttu-id="74ed7-159">nom DNS de hello tooresolve, du service DNS récursive hello recherche des serveurs de noms hello pour le domaine « contoso.com » de hello.</span><span class="sxs-lookup"><span data-stu-id="74ed7-159">tooresolve hello DNS name, hello recursive DNS service finds hello name servers for hello 'contoso.com' domain.</span></span> <span data-ttu-id="74ed7-160">Il contacte ensuite ces enregistrement DNS de nom serveurs toorequest hello 'partners.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="74ed7-160">It then contacts those name servers toorequest hello 'partners.contoso.com' DNS record.</span></span> <span data-ttu-id="74ed7-161">les serveurs DNS contoso.com Hello replacer hello CNAME qui pointe toocontoso.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="74ed7-161">hello contoso.com DNS servers return hello CNAME record that points toocontoso.trafficmanager.net.</span></span>
3. <span data-ttu-id="74ed7-162">Ensuite, le service DNS hello récursive recherche des serveurs de noms hello pour domaine hello 'trafficmanager.net', qui sont fournies par hello Azure Traffic Manager service.</span><span class="sxs-lookup"><span data-stu-id="74ed7-162">Next, hello recursive DNS service finds hello name servers for hello 'trafficmanager.net' domain, which are provided by hello Azure Traffic Manager service.</span></span> <span data-ttu-id="74ed7-163">Il envoie ensuite une demande de hello 'contoso.trafficmanager.net' DNS record toothose serveurs DNS.</span><span class="sxs-lookup"><span data-stu-id="74ed7-163">It then sends a request for hello 'contoso.trafficmanager.net' DNS record toothose DNS servers.</span></span>
4. <span data-ttu-id="74ed7-164">serveurs de noms de Traffic Manager Hello recevoir la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="74ed7-164">hello Traffic Manager name servers receive hello request.</span></span> <span data-ttu-id="74ed7-165">Ils choisissent un point de terminaison en fonction des critères suivants :</span><span class="sxs-lookup"><span data-stu-id="74ed7-165">They choose an endpoint based on:</span></span>

    - <span data-ttu-id="74ed7-166">état Hello configuré de chaque point de terminaison (les points de terminaison désactivés ne sont pas retournées)</span><span class="sxs-lookup"><span data-stu-id="74ed7-166">hello configured state of each endpoint (disabled endpoints are not returned)</span></span>
    - <span data-ttu-id="74ed7-167">Hello actuel de chaque point de terminaison, comme déterminé par le contrôle d’intégrité de Traffic Manager hello vérifications.</span><span class="sxs-lookup"><span data-stu-id="74ed7-167">hello current health of each endpoint, as determined by hello Traffic Manager health checks.</span></span> <span data-ttu-id="74ed7-168">(pour plus d’informations, voir la rubrique relative à la [surveillance des points de terminaison avec Traffic Manager](traffic-manager-monitoring.md)) ;</span><span class="sxs-lookup"><span data-stu-id="74ed7-168">For more information, see [Traffic Manager Endpoint Monitoring](traffic-manager-monitoring.md).</span></span>
    - <span data-ttu-id="74ed7-169">Hello choisi la méthode de routage du trafic.</span><span class="sxs-lookup"><span data-stu-id="74ed7-169">hello chosen traffic-routing method.</span></span> <span data-ttu-id="74ed7-170">(pour plus d’informations, voir [Méthodes de routage de Traffic Manager](traffic-manager-routing-methods.md)).</span><span class="sxs-lookup"><span data-stu-id="74ed7-170">For more information, see [Traffic Manager Routing Methods](traffic-manager-routing-methods.md).</span></span>

5. <span data-ttu-id="74ed7-171">point de terminaison Hello choisi est retourné en tant qu’un autre enregistrement CNAME DNS.</span><span class="sxs-lookup"><span data-stu-id="74ed7-171">hello chosen endpoint is returned as another DNS CNAME record.</span></span> <span data-ttu-id="74ed7-172">Dans ce cas, supposons que contoso-us.cloudapp.net est retourné.</span><span class="sxs-lookup"><span data-stu-id="74ed7-172">In this case, let us suppose contoso-us.cloudapp.net is returned.</span></span>
6. <span data-ttu-id="74ed7-173">Ensuite, le service DNS hello récursive recherche des serveurs de noms hello pour le domaine de 'cloudapp.net' hello.</span><span class="sxs-lookup"><span data-stu-id="74ed7-173">Next, hello recursive DNS service finds hello name servers for hello 'cloudapp.net' domain.</span></span> <span data-ttu-id="74ed7-174">Il contacte ces hello de toorequest de serveurs de nom « contoso-us.cloudapp .net » enregistrement DNS.</span><span class="sxs-lookup"><span data-stu-id="74ed7-174">It contacts those name servers toorequest hello 'contoso-us.cloudapp.net' DNS record.</span></span> <span data-ttu-id="74ed7-175">Un enregistrement DNS 'A' contenant l’adresse IP de hello du point de terminaison de service basé sur des États-Unis hello est retourné.</span><span class="sxs-lookup"><span data-stu-id="74ed7-175">A DNS 'A' record containing hello IP address of hello US-based service endpoint is returned.</span></span>
7. <span data-ttu-id="74ed7-176">le service DNS Hello récursive consolide les résultats hello et retourne un seul client toohello de réponse DNS.</span><span class="sxs-lookup"><span data-stu-id="74ed7-176">hello recursive DNS service consolidates hello results and returns a single DNS response toohello client.</span></span>
8. <span data-ttu-id="74ed7-177">client de Hello reçoit les résultats DNS hello et connecte toohello les adresse IP donnée.</span><span class="sxs-lookup"><span data-stu-id="74ed7-177">hello client receives hello DNS results and connects toohello given IP address.</span></span> <span data-ttu-id="74ed7-178">Hello client connecte point de terminaison de service toohello application directement, non par le biais du Gestionnaire de trafic.</span><span class="sxs-lookup"><span data-stu-id="74ed7-178">hello client connects toohello application service endpoint directly, not through Traffic Manager.</span></span> <span data-ttu-id="74ed7-179">Dans la mesure où il s’agit d’un point de terminaison HTTPS, client de hello effectue la négociation SSL/TLS nécessaire hello et puis effectue une demande HTTP GET pour hello ' / login.aspx' page.</span><span class="sxs-lookup"><span data-stu-id="74ed7-179">Since it is an HTTPS endpoint, hello client performs hello necessary SSL/TLS handshake, and then makes an HTTP GET request for hello '/login.aspx' page.</span></span>

<span data-ttu-id="74ed7-180">le service DNS Hello récursive met en cache les réponses DNS hello qu’il reçoit.</span><span class="sxs-lookup"><span data-stu-id="74ed7-180">hello recursive DNS service caches hello DNS responses it receives.</span></span> <span data-ttu-id="74ed7-181">la résolution DNS Hello sur hello client met également en cache le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="74ed7-181">hello DNS resolver on hello client device also caches hello result.</span></span> <span data-ttu-id="74ed7-182">Mise en cache permet toobe de requêtes DNS ultérieur ayant obtenu une réponse plus rapidement en utilisant des données à partir du cache de hello au lieu d’interroger d’autres serveurs de noms.</span><span class="sxs-lookup"><span data-stu-id="74ed7-182">Caching enables subsequent DNS queries toobe answered more quickly by using data from hello cache rather than querying other name servers.</span></span> <span data-ttu-id="74ed7-183">durée de Hello du cache de hello est déterminée par hello 'time-to-live' propriété (TTL) de chaque enregistrement DNS.</span><span class="sxs-lookup"><span data-stu-id="74ed7-183">hello duration of hello cache is determined by hello 'time-to-live' (TTL) property of each DNS record.</span></span> <span data-ttu-id="74ed7-184">Les valeurs plus courtes entraînent d’expiration de cache plus rapide et donc davantage d’allers-retours toohello Traffic Manager nom de serveurs.</span><span class="sxs-lookup"><span data-stu-id="74ed7-184">Shorter values result in faster cache expiry and thus more round-trips toohello Traffic Manager name servers.</span></span> <span data-ttu-id="74ed7-185">Des valeurs plus signifient que peut prendre plus de temps toodirect le trafic en dehors d’un point de terminaison ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="74ed7-185">Longer values mean that it can take longer toodirect traffic away from a failed endpoint.</span></span> <span data-ttu-id="74ed7-186">Traffic Manager vous permet de tooconfigure hello TTL utilisé dans toobe des réponses DNS Traffic Manager aussi faible que 0 seconde et aussi élevée que 2 147 483 647 secondes (hello plage maximale conforme [-la norme RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)), l’activation de valeur de hello toochoose qui équilibre mieux besoins hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="74ed7-186">Traffic Manager allows you tooconfigure hello TTL used in Traffic Manager DNS responses toobe as low as 0 seconds and as high as 2,147,483,647 seconds (hello maximum range compliant with [RFC-1035](https://www.ietf.org/rfc/rfc1035.txt)), enabling you toochoose hello value that best balances hello needs of your application.</span></span>

## <a name="pricing"></a><span data-ttu-id="74ed7-187">Tarification</span><span class="sxs-lookup"><span data-stu-id="74ed7-187">Pricing</span></span>

<span data-ttu-id="74ed7-188">Pour des informations sur les prix, consultez [Tarification Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="74ed7-188">For pricing information, see [Traffic Manager Pricing](https://azure.microsoft.com/pricing/details/traffic-manager/).</span></span>

## <a name="faq"></a><span data-ttu-id="74ed7-189">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="74ed7-189">FAQ</span></span>

<span data-ttu-id="74ed7-190">Pour connaître les questions fréquemment posées, consultez la page [Forum Aux Questions (FAQ) relatif à Traffic Manager](traffic-manager-FAQs.md).</span><span class="sxs-lookup"><span data-stu-id="74ed7-190">For frequently asked questions about Traffic Manager, see [Traffic Manager FAQs](traffic-manager-FAQs.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="74ed7-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="74ed7-191">Next steps</span></span>

<span data-ttu-id="74ed7-192">En savoir plus sur le [basculement automatique et la surveillance des points de terminaison](traffic-manager-monitoring.md)de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="74ed7-192">Learn more about Traffic Manager [endpoint monitoring and automatic failover](traffic-manager-monitoring.md).</span></span>

<span data-ttu-id="74ed7-193">En savoir plus sur les [méthodes de routage du trafic](traffic-manager-routing-methods.md)de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="74ed7-193">Learn more about Traffic Manager [traffic routing methods](traffic-manager-routing-methods.md).</span></span>

<span data-ttu-id="74ed7-194">En savoir plus sur certaines des hello autre clé [fonctionnalités de réseau](../networking/networking-overview.md) de Azure.</span><span class="sxs-lookup"><span data-stu-id="74ed7-194">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png
