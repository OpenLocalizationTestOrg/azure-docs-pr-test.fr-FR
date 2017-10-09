---
title: "fichier Lisez-moi d’aaaAzure environnement App Service"
description: "Répertorie la documentation hello qui décrit l’environnement Azure App Service"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 6edc74804ded7497e70c31c9e08252257add4415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="74929-103">Documentation sur App Service Environment</span><span class="sxs-lookup"><span data-stu-id="74929-103">App Service environment documentation</span></span>
 <span data-ttu-id="74929-104">Azure App Service Environment est une fonctionnalité d’Azure App Service qui fournit un environnement totalement isolé et dédié pour l’exécution sécurisée de vos applications App Service à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="74929-104">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="74929-105">Il permet d’héberger vos [applications web][webapps], vos [applications mobiles][mobileapps], vos [applications API][APIApps] et vos [fonctions][Functions].</span><span class="sxs-lookup"><span data-stu-id="74929-105">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIApps], and [functions][Functions].</span></span>

<span data-ttu-id="74929-106">Les environnements App Service Environment (ASE) constituent le meilleur choix pour les charges de travail applicatives présentant les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="74929-106">App Service environments (ASEs) are ideal for application workloads that require:</span></span>

* <span data-ttu-id="74929-107">Très grande échelle.</span><span class="sxs-lookup"><span data-stu-id="74929-107">Very high scale.</span></span>
* <span data-ttu-id="74929-108">Isolation et accès réseau sécurisé.</span><span class="sxs-lookup"><span data-stu-id="74929-108">Isolation and secure network access.</span></span>

<span data-ttu-id="74929-109">Les clients peuvent créer plusieurs environnements ASE au sein d’une même région Azure, ainsi que dans plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="74929-109">Customers can create multiple ASEs within a single Azure region and across multiple Azure regions.</span></span> <span data-ttu-id="74929-110">Grâce à cette polyvalence, les environnements ASE sont parfaits pour l’évolution horizontale des applications sans état pour la prise en charge de lourdes charges de travail RPS.</span><span class="sxs-lookup"><span data-stu-id="74929-110">This versatility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="74929-111">ASEs sont isolé toorunning uniquement les applications d’un client unique et sont toujours déployés dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="74929-111">ASEs are isolated toorunning only a single customer's applications and are always deployed into an Azure virtual network.</span></span> <span data-ttu-id="74929-112">Les clients peuvent contrôler précisément le trafic réseau entrant et sortant des applications à l’aide des [groupes de sécurité réseau][NSGs].</span><span class="sxs-lookup"><span data-stu-id="74929-112">Customers have fine-grained control over inbound and outbound application network traffic by using [Network Security Groups][NSGs].</span></span> <span data-ttu-id="74929-113">Applications peuvent également établir des connexions sécurisées à grande vitesse sur les ressources d’entreprise de réseaux virtuels tooon local.</span><span class="sxs-lookup"><span data-stu-id="74929-113">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="74929-114">Les applications ont souvent besoin tooaccess des ressources d’entreprise, telles que les bases de données internes et les services web.</span><span class="sxs-lookup"><span data-stu-id="74929-114">Apps frequently need tooaccess corporate resources, such as internal databases and web services.</span></span> <span data-ttu-id="74929-115">Les applications qui s’exécutent dans des environnements ASE peuvent accéder aux ressources via des connexions VPN [site-à-site][SiteToSite] et [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="74929-115">Apps that run on ASEs can access resources via [site-to-site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* <span data-ttu-id="74929-116">[Qu’est-ce qu’un environnement App Service Environment ?][Intro]</span><span class="sxs-lookup"><span data-stu-id="74929-116">[What is an App Service environment?][Intro]</span></span>
* <span data-ttu-id="74929-117">[Créer un environnement App Service Environment][MakeExternalASE]</span><span class="sxs-lookup"><span data-stu-id="74929-117">[Create an App Service environment][MakeExternalASE]</span></span>
* <span data-ttu-id="74929-118">[Créer un environnement App Service Environment avec équilibreur de charge interne][MakeILBASE]</span><span class="sxs-lookup"><span data-stu-id="74929-118">[Create an internal load balancer App Service environment][MakeILBASE]</span></span>
* <span data-ttu-id="74929-119">[Utiliser un environnement App Service Environment][UsingASE]</span><span class="sxs-lookup"><span data-stu-id="74929-119">[Use an App Service environment][UsingASE]</span></span>
* <span data-ttu-id="74929-120">[Considérations relatives à la mise en réseau et hello environnement App Service][ASENetwork]</span><span class="sxs-lookup"><span data-stu-id="74929-120">[Networking considerations and hello App Service environment][ASENetwork]</span></span>
* <span data-ttu-id="74929-121">[Créer un environnement App Service Environment à partir d’un modèle][MakeASEfromTemplate]</span><span class="sxs-lookup"><span data-stu-id="74929-121">[Create an App Service environment from a template][MakeASEfromTemplate]</span></span>


## <a name="videos"></a><span data-ttu-id="74929-122">Vidéos</span><span class="sxs-lookup"><span data-stu-id="74929-122">Videos</span></span>
<span data-ttu-id="74929-123">PaaS moderne de master pour hello entreprise avec le Service d’application Azure</span><span class="sxs-lookup"><span data-stu-id="74929-123">Master Modern PaaS for hello Enterprise with Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

<span data-ttu-id="74929-124">Déploiement d’applications hautement évolutives et sécurisées</span><span class="sxs-lookup"><span data-stu-id="74929-124">Deploying Highly Scalable and Secure Apps</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

<span data-ttu-id="74929-125">Exécution d’applications web et mobiles d’entreprise sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="74929-125">Running Enterprise Web and Mobile Apps on Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="74929-126">Environnement App Service v1</span><span class="sxs-lookup"><span data-stu-id="74929-126">App Service Environment v1</span></span> ##
<span data-ttu-id="74929-127">Il existe deux versions d’App Service Environment : ASEv1 et ASEv2.</span><span class="sxs-lookup"><span data-stu-id="74929-127">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="74929-128">Pour plus d’informations sur ASEv1, consultez la [documentation sur App Service Environment v1][ASEv1README].</span><span class="sxs-lookup"><span data-stu-id="74929-128">For information on ASEv1, see [App Service Environment v1 documentation][ASEv1README].</span></span>


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
