---
title: Environnement App Service| Microsoft Docs
description: "Qu’est-ce qu’un environnement Azure App Service ? Présentation de l’environnement App Service."
keywords: "environnement azure app service, réseau virtuel, sécurisation des réseaux"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 1db5c057-3c56-4537-b580-cdd21fe3f3a7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: stefsch
ms.openlocfilehash: 1de3f2c513f4f5ce6fd2ab2b57514122955a9a98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="e306b-105">Documentation sur l’environnement App Service</span><span class="sxs-lookup"><span data-stu-id="e306b-105">App Service Environment Documentation</span></span>
<span data-ttu-id="e306b-106">Un environnement App Service est une option de plan de service [Premium][PremiumTier] d’Azure App Service qui fournit un environnement totalement isolé et dédié pour exécuter en toute sécurité des applications Azure App Service de grande envergure, comme [Web Apps][WebApps], [Mobile Apps][MobileApps] et [API Apps][APIApps].</span><span class="sxs-lookup"><span data-stu-id="e306b-106">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="e306b-107">Les environnements App Service constituent le meilleur choix pour les charges de travail applicatives avec les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="e306b-107">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="e306b-108">Très grande échelle</span><span class="sxs-lookup"><span data-stu-id="e306b-108">Very high scale</span></span>
* <span data-ttu-id="e306b-109">Isolation et accès réseau sécurisé</span><span class="sxs-lookup"><span data-stu-id="e306b-109">Isolation and secure network access</span></span>

<span data-ttu-id="e306b-110">Les clients peuvent créer plusieurs environnements App Service au sein d’une même région Azure, ainsi que dans plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="e306b-110">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="e306b-111">Les environnements App Service sont donc parfaits pour l’évolution horizontale des applications sans état pour la prise en charge de lourdes charges de travail RPS.</span><span class="sxs-lookup"><span data-stu-id="e306b-111">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="e306b-112">Les environnements App Service sont isolés de façon à exécuter les applications d’un seul client et ils sont toujours déployés dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e306b-112">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="e306b-113">Les clients peuvent contrôler précisément le trafic réseau entrant et sortant des applications à l’aide des [groupes de sécurité réseau][NetworkSecurityGroups].</span><span class="sxs-lookup"><span data-stu-id="e306b-113">Customers have fine-grained control over both inbound and outbound application network traffic using [network security groups][NetworkSecurityGroups].</span></span>  <span data-ttu-id="e306b-114">Les applications peuvent également établir des connexions sécurisées à haute vitesse via des réseaux virtuels aux ressources d’entreprise locales.</span><span class="sxs-lookup"><span data-stu-id="e306b-114">Applications can also establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="e306b-115">Les applications doivent souvent accéder à des ressources d’entreprise telles que des bases de données internes et des services web.</span><span class="sxs-lookup"><span data-stu-id="e306b-115">Apps frequently need to access corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="e306b-116">Les applications s’exécutant dans des environnements App Service peuvent accéder aux ressources joignables via des connexions VPN [site à site][SiteToSite] et [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="e306b-116">Apps running on App Service Environments can access resources reachable via [Site-to-Site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* [<span data-ttu-id="e306b-117">Qu'est-ce qu'un environnement App Service ?</span><span class="sxs-lookup"><span data-stu-id="e306b-117">What is an App Service Environment?</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
* [<span data-ttu-id="e306b-118">Création d'un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="e306b-118">Creating an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="e306b-119">Création d'applications dans un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="e306b-119">Creating Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="e306b-120">Création et utilisation d’un équilibreur de charge interne avec des environnements App Service</span><span class="sxs-lookup"><span data-stu-id="e306b-120">Creating and Using an Internal Load Balancer with App Service Environments</span></span>](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [<span data-ttu-id="e306b-121">Configuration d'un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="e306b-121">Configuring an App Service Environment</span></span>](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [<span data-ttu-id="e306b-122">Mise à l'échelle des applications dans un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="e306b-122">Scaling Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [<span data-ttu-id="e306b-123">Architecture et sécurité du réseau</span><span class="sxs-lookup"><span data-stu-id="e306b-123">Network Security and Architecture</span></span>](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a><span data-ttu-id="e306b-124">Conseils pratiques</span><span class="sxs-lookup"><span data-stu-id="e306b-124">How To's</span></span>
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a><span data-ttu-id="e306b-125">Vidéos</span><span class="sxs-lookup"><span data-stu-id="e306b-125">Videos</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]



<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
