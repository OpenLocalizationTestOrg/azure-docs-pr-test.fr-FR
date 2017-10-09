---
title: aaaIntroduction tooApp environnement Service v1
description: "En savoir plus sur la fonctionnalité hello v1 de l’environnement App Service qui fournit des unités d’échelle sûr, appartenant à un réseau virtuel et dédié pour exécuter toutes vos applications."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a><span data-ttu-id="af998-103">Introduction tooApp environnement Service v1</span><span class="sxs-lookup"><span data-stu-id="af998-103">Introduction tooApp Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="af998-104">Cet article porte sur hello environnement App Service v1.</span><span class="sxs-lookup"><span data-stu-id="af998-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="af998-105">Il existe une version plus récente de hello environnement App Service toouse plus facile et s’exécute sur une infrastructure plus puissante.</span><span class="sxs-lookup"><span data-stu-id="af998-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="af998-106">toolearn plus d’informations sur la nouvelle version de hello commencent par Bonjour [Introduction toohello environnement App Service](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="af998-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="af998-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="af998-107">Overview</span></span>
<span data-ttu-id="af998-108">Un environnement App Service est une option de plan de service [Premium][PremiumTier] d’Azure App Service qui fournit un environnement totalement isolé et dédié pour exécuter en toute sécurité des applications Azure App Service de grande envergure, comme [Web Apps][WebApps], [Mobile Apps][MobileApps] et [API Apps][APIApps].</span><span class="sxs-lookup"><span data-stu-id="af998-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="af998-109">Les environnements App Service constituent le meilleur choix pour les charges de travail applicatives avec les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="af998-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="af998-110">Très grande échelle</span><span class="sxs-lookup"><span data-stu-id="af998-110">Very high scale</span></span>
* <span data-ttu-id="af998-111">Isolation et accès réseau sécurisé</span><span class="sxs-lookup"><span data-stu-id="af998-111">Isolation and secure network access</span></span>

<span data-ttu-id="af998-112">Les clients peuvent créer plusieurs environnements App Service au sein d’une même région Azure, ainsi que dans plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="af998-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="af998-113">Les environnements App Service sont donc parfaits pour l’évolution horizontale des applications sans état pour la prise en charge de lourdes charges de travail RPS.</span><span class="sxs-lookup"><span data-stu-id="af998-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="af998-114">Les environnements App Service sont isolé toorunning uniquement les applications d’un client unique et sont toujours déployés dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="af998-114">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="af998-115">Les clients ont un contrôle affiné sur le trafic réseau entrant et sortant des applications et applications peuvent établir des connexions sécurisées à grande vitesse sur les ressources d’entreprise de réseaux virtuels tooon local.</span><span class="sxs-lookup"><span data-stu-id="af998-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="af998-116">Tous les articles et comment-du sur les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="af998-116">All articles and How-To's about App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="af998-117">Pour une vue d’ensemble de l’activer à grande échelle et la sécurisation des environnements App Service accès réseau, consultez hello [approfondie AzureCon] [ AzureConDeepDive] sur les environnements de Service d’application !</span><span class="sxs-lookup"><span data-stu-id="af998-117">For an overview of how App Service Environments enable high scale and secure network access, see hello [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="af998-118">Pour une présentation détaillée sur la mise à l’échelle horizontalement à l’aide de plusieurs environnements de Service d’application voir l’article de hello sur la façon de toosetup un [encombrement de l’application de géo-distribué][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="af998-118">For a deep-dive on horizontally scaling using multiple App Service Environments see hello article on how toosetup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="af998-119">toosee architecture de sécurité hello hello approfondie AzureCon montre la configuration, consultez l’article hello sur l’implémentation d’un [en couches d’architecture de sécurité](app-service-app-service-environment-layered-security.md) avec les environnements de Service d’application.</span><span class="sxs-lookup"><span data-stu-id="af998-119">toosee how hello security architecture shown in hello AzureCon Deep Dive was configured, see hello article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="af998-120">L’accès aux applications qui s’exécutent sur des environnements App Service peut être contrôlé par des appareils en amont tels que les pare-feu d’applications web (WAF).</span><span class="sxs-lookup"><span data-stu-id="af998-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="af998-121">article Hello sur [configuration un WAF pour les environnements de Service d’application](app-service-app-service-environment-web-application-firewall.md) couvre ce scénario.</span><span class="sxs-lookup"><span data-stu-id="af998-121">hello article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="af998-122">Ressources de calcul dédiées</span><span class="sxs-lookup"><span data-stu-id="af998-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="af998-123">Calcul hello les ressources dans un environnement App Service sont tous dédié exclusivement tooa seul abonnement, et un environnement App Service peut être configuré avec des ressources de calcul toofifty (50) pour une utilisation exclusive par une application unique.</span><span class="sxs-lookup"><span data-stu-id="af998-123">All of hello compute resources in an App Service Environment are dedicated exclusively tooa single subscription, and an App Service Environment can be configured with up toofifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="af998-124">Un environnement App Service est composé d’un pool de ressources de calcul frontaux, ainsi que les pools de ressources de calcul un toothree travail.</span><span class="sxs-lookup"><span data-stu-id="af998-124">An App Service Environment is composed of a front-end compute resource pool, as well as one toothree worker compute resource pools.</span></span> 

<span data-ttu-id="af998-125">pool frontal de Hello contient des ressources de calcul responsable de la terminaison SSL en tant que l’équilibrage de charge automatique et de demandes d’application dans un environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="af998-125">hello front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="af998-126">Chaque pool de travail contient des ressources de calcul alloués trop[Plans de Service d’application][AppServicePlan], qui à son tour contenir une ou plusieurs applications de Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="af998-126">Each worker pool contains compute resources allocated too[App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="af998-127">Dans la mesure où il peut y avoir des pools de travail différent toothree dans un environnement App Service, vous avez hello flexibilité toochoose différentes des ressources de calcul pour chaque pool de travail.</span><span class="sxs-lookup"><span data-stu-id="af998-127">Since there can be up toothree different worker pools in an App Service Environment, you have hello flexibility toochoose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="af998-128">Par exemple, cela vous permet toocreate pool d’un travail avec des ressources de calcul moins puissants pour les Plans de Service application conçue pour les applications de développement ou de test.</span><span class="sxs-lookup"><span data-stu-id="af998-128">For example, this allows you toocreate one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="af998-129">Un deuxième (ou même troisième) pool de travaux peut utiliser des ressources de calcul plus puissantes destinées aux plans App Service exécutant des applications de production.</span><span class="sxs-lookup"><span data-stu-id="af998-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="af998-130">Pour plus d’informations sur la quantité de hello de calcul ressources disponibles toohello frontaux et des pools de travail, consultez [comment tooConfigure un environnement App Service][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="af998-130">For more details on hello quantity of compute resources available toohello front-end and worker pools, see [How tooConfigure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="af998-131">Pour plus d’informations sur hello disponible des tailles de ressources pris en charge dans un environnement App Service de calcul, consultez hello [tarification de Service application] [ AppServicePricing] page et passez en revue les options disponibles de hello pour les environnements de Service d’application dans le niveau de tarification hello Premium.</span><span class="sxs-lookup"><span data-stu-id="af998-131">For details on hello available compute resource sizes supported in an App Service Environment, consult hello [App Service Pricing][AppServicePricing] page and review hello available options for App Service Environments in hello Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="af998-132">Prise en charge des réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="af998-132">Virtual Network Support</span></span>
<span data-ttu-id="af998-133">Un environnement App Service peut être créé **soit** dans un réseau virtuel Azure Resource Manager, **ou** dans un réseau virtuel de modèle de déploiement classique ([plus d’informations sur les réseaux virtuels][MoreInfoOnVirtualNetworks]).</span><span class="sxs-lookup"><span data-stu-id="af998-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="af998-134">Depuis un environnement App Service existe toujours dans un réseau virtuel, et plus précisément au sein d’un sous-réseau d’un réseau virtuel, vous pouvez tirer parti des fonctionnalités de sécurité hello de réseaux virtuels toocontrol les communications réseau entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="af998-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage hello security features of virtual networks toocontrol both inbound and outbound network communications.</span></span>  

<span data-ttu-id="af998-135">Un environnement App Service peut être soit accessible sur Internet avec une adresse IP publique, soit accessible en interne avec une adresse d’équilibrage de charge interne (ILB) Azure uniquement.</span><span class="sxs-lookup"><span data-stu-id="af998-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="af998-136">Vous pouvez utiliser [groupes de sécurité réseau] [ NetworkSecurityGroups] toorestrict entrants communications toohello sous-réseau dans lequel un environnement App Service réside.</span><span class="sxs-lookup"><span data-stu-id="af998-136">You can use [network security groups][NetworkSecurityGroups] toorestrict inbound network communications toohello subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="af998-137">Cela vous permet des applications toorun derrière les périphériques en amont et de services tels que les pare-feu d’applications web et les fournisseurs SaaS de réseau.</span><span class="sxs-lookup"><span data-stu-id="af998-137">This allows you toorun apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="af998-138">Les applications doivent également fréquemment tooaccess des ressources d’entreprise telles que les bases de données internes et les services web.</span><span class="sxs-lookup"><span data-stu-id="af998-138">Apps also frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="af998-139">Une approche courante est toomake ces points de terminaison disponibles toointernal uniquement tout trafic réseau au sein d’un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="af998-139">A common approach is toomake these endpoints available only toointernal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="af998-140">Une fois qu’un environnement App Service est toohello joints à un même réseau virtuel en tant que services interne hello, les applications en cours d’exécution dans un environnement de hello peut y accéder, y compris les points de terminaison accessibles via [Site-à-Site] [ SiteToSite]et [Azure ExpressRoute] [ ExpressRoute] connexions.</span><span class="sxs-lookup"><span data-stu-id="af998-140">Once an App Service Environment is joined toohello same virtual network as hello internal services, apps running in hello environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="af998-141">Pour plus d’informations sur le fonctionnement des environnements de Service d’application avec des réseaux virtuels et réseaux locaux consultez hello suivant des articles de [Architecture réseau][NetworkArchitectureOverview], [contrôle de trafic entrant Le trafic][ControllingInboundTraffic], et [tooBackends de connexion en toute sécurité][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="af998-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult hello following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting tooBackends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="af998-142">Prise en main</span><span class="sxs-lookup"><span data-stu-id="af998-142">Getting started</span></span>
<span data-ttu-id="af998-143">tooget démarré avec les environnements de Service d’application, consultez [comment tooCreate un environnement App Service][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="af998-143">tooget started with App Service Environments, see [How tooCreate An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="af998-144">Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="af998-144">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="af998-145">Pour plus d’informations sur la plateforme Azure App Service de hello, consultez [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="af998-145">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="af998-146">Pour une vue d’ensemble de l’architecture en réseau environnement App Service de hello, consultez hello [présentation de l’Architecture réseau] [ NetworkArchitectureOverview] l’article.</span><span class="sxs-lookup"><span data-stu-id="af998-146">For an overview of hello App Service Environment network architecture, see hello [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="af998-147">Pour plus d’informations sur l’utilisation d’un environnement App Service grâce à ExpressRoute, consultez hello l’article suivant [Express Route et les environnements App Service][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="af998-147">For details on using an App Service Environment with ExpressRoute, see hello following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


