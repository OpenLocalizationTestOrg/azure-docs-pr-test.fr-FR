---
title: "Présentation d’App Service Environment v1"
description: "Découvrez la fonctionnalité App Service Environment v1, qui fournit des unités d’échelle sécurisées, dédiées et appartenant à un réseau virtuel pour exécuter toutes vos applications."
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
ms.openlocfilehash: 38cb79eb32bd61cdbfb6da91d50e6713d71a2b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-app-service-environment-v1"></a><span data-ttu-id="f8ee9-103">Présentation d’App Service Environment v1</span><span class="sxs-lookup"><span data-stu-id="f8ee9-103">Introduction to App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="f8ee9-104">Cet article traite de l’environnement App Service v1.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="f8ee9-105">Il existe une version plus récente de l’environnement App Service Environment, plus facile à utiliser et qui s’exécute sur des infrastructures plus puissantes.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="f8ee9-106">Pour en savoir plus sur la nouvelle version, commencez par la section [Présentation de l’environnement App Service Environment](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="f8ee9-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="f8ee9-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f8ee9-107">Overview</span></span>
<span data-ttu-id="f8ee9-108">Un environnement App Service est une option de plan de service [Premium][PremiumTier] d’Azure App Service qui fournit un environnement totalement isolé et dédié pour exécuter en toute sécurité des applications Azure App Service de grande envergure, comme [Web Apps][WebApps], [Mobile Apps][MobileApps] et [API Apps][APIApps].</span><span class="sxs-lookup"><span data-stu-id="f8ee9-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="f8ee9-109">Les environnements App Service constituent le meilleur choix pour les charges de travail applicatives avec les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="f8ee9-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="f8ee9-110">Très grande échelle</span><span class="sxs-lookup"><span data-stu-id="f8ee9-110">Very high scale</span></span>
* <span data-ttu-id="f8ee9-111">Isolation et accès réseau sécurisé</span><span class="sxs-lookup"><span data-stu-id="f8ee9-111">Isolation and secure network access</span></span>

<span data-ttu-id="f8ee9-112">Les clients peuvent créer plusieurs environnements App Service au sein d’une même région Azure, ainsi que dans plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="f8ee9-113">Les environnements App Service sont donc parfaits pour l’évolution horizontale des applications sans état pour la prise en charge de lourdes charges de travail RPS.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="f8ee9-114">Les environnements App Service sont isolés de façon à exécuter les applications d’un seul client et ils sont toujours déployés dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-114">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="f8ee9-115">Les clients ont un contrôle affiné sur le trafic réseau entrant et sortant des applications, et les applications peuvent établir des connexions sécurisées à haut débit sur les réseaux virtuels avec les ressources d’entreprise locales.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="f8ee9-116">Tous les articles et procédures concernant les environnements App Service sont disponibles dans le [fichier Lisez-moi des environnements App Service](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="f8ee9-116">All articles and How-To's about App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="f8ee9-117">Pour avoir une idée générale de la façon dont les environnements App Service permettent l’accès réseau sécurisé à grande échelle, consultez la vidéo [AzureCon Deep Dive][AzureConDeepDive] sur les environnements App Service.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-117">For an overview of how App Service Environments enable high scale and secure network access, see the [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="f8ee9-118">Pour une exploration approfondie de la mise à l’échelle horizontale à l’aide de plusieurs environnements App Service, consultez l’article sur la configuration d’une [empreinte d’application géo-distribuée][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="f8ee9-118">For a deep-dive on horizontally scaling using multiple App Service Environments see the article on how to setup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="f8ee9-119">Pour afficher la configuration de l’architecture de sécurité illustrée dans AzureCon Deep Dive, consultez l’article sur l’implémentation d’une [architecture de sécurité en couches](app-service-app-service-environment-layered-security.md) avec les environnements App Service.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-119">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="f8ee9-120">L’accès aux applications qui s’exécutent sur des environnements App Service peut être contrôlé par des appareils en amont tels que les pare-feu d’applications web (WAF).</span><span class="sxs-lookup"><span data-stu-id="f8ee9-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="f8ee9-121">Ce scénario est traité dans l’article sur la [configuration d’un pare-feu d’application web pour les environnements App Service](app-service-app-service-environment-web-application-firewall.md) .</span><span class="sxs-lookup"><span data-stu-id="f8ee9-121">The article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="f8ee9-122">Ressources de calcul dédiées</span><span class="sxs-lookup"><span data-stu-id="f8ee9-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="f8ee9-123">Toutes les ressources de calcul d’un environnement App Service sont exclusivement dédiées à un seul abonnement, et il est possible de configurer un environnement App Service avec jusqu’à cinquante (50) ressources de calcul pour une seule application.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-123">All of the compute resources in an App Service Environment are dedicated exclusively to a single subscription, and an App Service Environment can be configured with up to fifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="f8ee9-124">Un environnement App Service se compose d’un pool de ressources de calcul frontal, ainsi que de un à trois pools de ressources de calcul de travail.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-124">An App Service Environment is composed of a front-end compute resource pool, as well as one to three worker compute resource pools.</span></span> 

<span data-ttu-id="f8ee9-125">Le pool frontal contient des ressources de calcul responsables de l'arrêt SSL ainsi que de l'équilibrage de charge automatique des demandes d'application dans un environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-125">The front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="f8ee9-126">Chaque pool de travaux contient des ressources de calcul allouées à des [plans App Service][AppServicePlan], qui, eux-mêmes, contiennent une ou plusieurs applications Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-126">Each worker pool contains compute resources allocated to [App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="f8ee9-127">Étant donné qu'un environnement App Service peut comprendre jusqu'à trois pools de travaux différents, vous pouvez choisir des ressources de calcul différentes pour chaque pool de travaux.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-127">Since there can be up to three different worker pools in an App Service Environment, you have the flexibility to choose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="f8ee9-128">Cela vous permet, par exemple, de créer un pool de travaux avec des ressources de calcul moins puissantes pour les plans App Service destinés aux applications de développement ou de test.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-128">For example, this allows you to create one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="f8ee9-129">Un deuxième (ou même troisième) pool de travaux peut utiliser des ressources de calcul plus puissantes destinées aux plans App Service exécutant des applications de production.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="f8ee9-130">Pour plus d'informations sur la quantité de ressources de calcul disponibles pour les pools frontaux et de travail, consultez [Comment configurer un environnement App Service][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="f8ee9-130">For more details on the quantity of compute resources available to the front-end and worker pools, see [How To Configure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="f8ee9-131">Pour plus d'informations sur les tailles de ressources de calcul disponibles prises en charge dans un environnement App Service, consultez la page [Service d'application Tarification][AppServicePricing] et passez en revue les options disponibles pour les environnements App Service dans le niveau de tarification Premium.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-131">For details on the available compute resource sizes supported in an App Service Environment, consult the [App Service Pricing][AppServicePricing] page and review the available options for App Service Environments in the Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="f8ee9-132">Prise en charge des réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="f8ee9-132">Virtual Network Support</span></span>
<span data-ttu-id="f8ee9-133">Un environnement App Service peut être créé **soit** dans un réseau virtuel Azure Resource Manager, **ou** dans un réseau virtuel de modèle de déploiement classique ([plus d’informations sur les réseaux virtuels][MoreInfoOnVirtualNetworks]).</span><span class="sxs-lookup"><span data-stu-id="f8ee9-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="f8ee9-134">Étant donné qu'il existe toujours un environnement App Service sur un réseau virtuel, et plus précisément sur un sous-réseau d'un réseau virtuel, vous pouvez exploiter les fonctionnalités de sécurité des réseaux virtuels pour contrôler les communications réseau entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage the security features of virtual networks to control both inbound and outbound network communications.</span></span>  

<span data-ttu-id="f8ee9-135">Un environnement App Service peut être soit accessible sur Internet avec une adresse IP publique, soit accessible en interne avec une adresse d’équilibrage de charge interne (ILB) Azure uniquement.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="f8ee9-136">Vous pouvez utiliser des [groupes de sécurité réseau][NetworkSecurityGroups] pour restreindre les communications réseau entrantes vers le sous-réseau sur lequel réside un environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-136">You can use [network security groups][NetworkSecurityGroups] to restrict inbound network communications to the subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="f8ee9-137">Cela vous permet d'exécuter des applications derrière des appareils et services en amont tels des pare-feu d'applications web, ainsi que des fournisseurs SaaS réseau.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-137">This allows you to run apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="f8ee9-138">Les applications doivent souvent accéder à des ressources d'entreprise telles que des bases de données internes et des services web.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-138">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="f8ee9-139">Une approche courante consiste à rendre ces points de terminaison disponibles uniquement au trafic réseau interne circulant au sein d'un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="f8ee9-139">A common approach is to make these endpoints available only to internal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="f8ee9-140">Une fois qu'un environnement App Service est joint au même réseau virtuel que les services internes, les applications s'exécutant dans l'environnement peuvent y accéder, notamment les points de terminaison accessibles via des connexions [site à site][SiteToSite] et [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="f8ee9-140">Once an App Service Environment is joined to the same virtual network as the internal services, apps running in the environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="f8ee9-141">Pour plus d’informations sur le fonctionnement des environnements App Service avec les réseaux virtuels et les réseaux locaux, consultez les articles suivants sur l’[architecture réseau][NetworkArchitectureOverview], le [contrôle du trafic entrant][ControllingInboundTraffic] et la [connexion sécurisée aux serveurs principaux][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="f8ee9-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult the following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting to Backends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="f8ee9-142">Prise en main</span><span class="sxs-lookup"><span data-stu-id="f8ee9-142">Getting started</span></span>
<span data-ttu-id="f8ee9-143">Pour prendre en main les environnements App Service, consultez [Comment créer un environnement App Service][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="f8ee9-143">To get started with App Service Environments, see [How To Create An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="f8ee9-144">Tous les articles et procédures concernant les environnements App Service sont disponibles dans le [fichier Lisez-moi des environnements App Service](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="f8ee9-144">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="f8ee9-145">Pour plus d’informations sur la plateforme Azure App Service, consultez la rubrique [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="f8ee9-145">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="f8ee9-146">Pour obtenir une vue d’ensemble de l’architecture réseau de l’environnement App Service, consultez l’article [Présentation de l’architecture réseau][NetworkArchitectureOverview].</span><span class="sxs-lookup"><span data-stu-id="f8ee9-146">For an overview of the App Service Environment network architecture, see the [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="f8ee9-147">Pour plus d’informations sur l’utilisation d’un environnement App Service avec ExpressRoute, consultez l’article suivant sur [ExpressRoute et environnements App Service][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="f8ee9-147">For details on using an App Service Environment with ExpressRoute, see the following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

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


