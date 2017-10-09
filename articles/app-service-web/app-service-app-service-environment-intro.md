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
# <a name="introduction-tooapp-service-environment-v1"></a>Introduction tooApp environnement Service v1

> [!NOTE]
> Cet article porte sur hello environnement App Service v1.  Il existe une version plus récente de hello environnement App Service toouse plus facile et s’exécute sur une infrastructure plus puissante. toolearn plus d’informations sur la nouvelle version de hello commencent par Bonjour [Introduction toohello environnement App Service](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Vue d'ensemble
Un environnement App Service est une option de plan de service [Premium][PremiumTier] d’Azure App Service qui fournit un environnement totalement isolé et dédié pour exécuter en toute sécurité des applications Azure App Service de grande envergure, comme [Web Apps][WebApps], [Mobile Apps][MobileApps] et [API Apps][APIApps].  

Les environnements App Service constituent le meilleur choix pour les charges de travail applicatives avec les exigences suivantes :

* Très grande échelle
* Isolation et accès réseau sécurisé

Les clients peuvent créer plusieurs environnements App Service au sein d’une même région Azure, ainsi que dans plusieurs régions Azure.  Les environnements App Service sont donc parfaits pour l’évolution horizontale des applications sans état pour la prise en charge de lourdes charges de travail RPS.

Les environnements App Service sont isolé toorunning uniquement les applications d’un client unique et sont toujours déployés dans un réseau virtuel.  Les clients ont un contrôle affiné sur le trafic réseau entrant et sortant des applications et applications peuvent établir des connexions sécurisées à grande vitesse sur les ressources d’entreprise de réseaux virtuels tooon local.

Tous les articles et comment-du sur les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).

Pour une vue d’ensemble de l’activer à grande échelle et la sécurisation des environnements App Service accès réseau, consultez hello [approfondie AzureCon] [ AzureConDeepDive] sur les environnements de Service d’application !

Pour une présentation détaillée sur la mise à l’échelle horizontalement à l’aide de plusieurs environnements de Service d’application voir l’article de hello sur la façon de toosetup un [encombrement de l’application de géo-distribué][GeodistributedAppFootprint].

toosee architecture de sécurité hello hello approfondie AzureCon montre la configuration, consultez l’article hello sur l’implémentation d’un [en couches d’architecture de sécurité](app-service-app-service-environment-layered-security.md) avec les environnements de Service d’application.

L’accès aux applications qui s’exécutent sur des environnements App Service peut être contrôlé par des appareils en amont tels que les pare-feu d’applications web (WAF).  article Hello sur [configuration un WAF pour les environnements de Service d’application](app-service-app-service-environment-web-application-firewall.md) couvre ce scénario. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>Ressources de calcul dédiées
Calcul hello les ressources dans un environnement App Service sont tous dédié exclusivement tooa seul abonnement, et un environnement App Service peut être configuré avec des ressources de calcul toofifty (50) pour une utilisation exclusive par une application unique.

Un environnement App Service est composé d’un pool de ressources de calcul frontaux, ainsi que les pools de ressources de calcul un toothree travail. 

pool frontal de Hello contient des ressources de calcul responsable de la terminaison SSL en tant que l’équilibrage de charge automatique et de demandes d’application dans un environnement App Service. 

Chaque pool de travail contient des ressources de calcul alloués trop[Plans de Service d’application][AppServicePlan], qui à son tour contenir une ou plusieurs applications de Service d’applications Azure.  Dans la mesure où il peut y avoir des pools de travail différent toothree dans un environnement App Service, vous avez hello flexibilité toochoose différentes des ressources de calcul pour chaque pool de travail.  

Par exemple, cela vous permet toocreate pool d’un travail avec des ressources de calcul moins puissants pour les Plans de Service application conçue pour les applications de développement ou de test.  Un deuxième (ou même troisième) pool de travaux peut utiliser des ressources de calcul plus puissantes destinées aux plans App Service exécutant des applications de production.

Pour plus d’informations sur la quantité de hello de calcul ressources disponibles toohello frontaux et des pools de travail, consultez [comment tooConfigure un environnement App Service][HowToConfigureanAppServiceEnvironment].  

Pour plus d’informations sur hello disponible des tailles de ressources pris en charge dans un environnement App Service de calcul, consultez hello [tarification de Service application] [ AppServicePricing] page et passez en revue les options disponibles de hello pour les environnements de Service d’application dans le niveau de tarification hello Premium.

## <a name="virtual-network-support"></a>Prise en charge des réseaux virtuels
Un environnement App Service peut être créé **soit** dans un réseau virtuel Azure Resource Manager, **ou** dans un réseau virtuel de modèle de déploiement classique ([plus d’informations sur les réseaux virtuels][MoreInfoOnVirtualNetworks]).  Depuis un environnement App Service existe toujours dans un réseau virtuel, et plus précisément au sein d’un sous-réseau d’un réseau virtuel, vous pouvez tirer parti des fonctionnalités de sécurité hello de réseaux virtuels toocontrol les communications réseau entrantes et sortantes.  

Un environnement App Service peut être soit accessible sur Internet avec une adresse IP publique, soit accessible en interne avec une adresse d’équilibrage de charge interne (ILB) Azure uniquement.

Vous pouvez utiliser [groupes de sécurité réseau] [ NetworkSecurityGroups] toorestrict entrants communications toohello sous-réseau dans lequel un environnement App Service réside.  Cela vous permet des applications toorun derrière les périphériques en amont et de services tels que les pare-feu d’applications web et les fournisseurs SaaS de réseau.

Les applications doivent également fréquemment tooaccess des ressources d’entreprise telles que les bases de données internes et les services web.  Une approche courante est toomake ces points de terminaison disponibles toointernal uniquement tout trafic réseau au sein d’un réseau virtuel Azure.  Une fois qu’un environnement App Service est toohello joints à un même réseau virtuel en tant que services interne hello, les applications en cours d’exécution dans un environnement de hello peut y accéder, y compris les points de terminaison accessibles via [Site-à-Site] [ SiteToSite]et [Azure ExpressRoute] [ ExpressRoute] connexions.

Pour plus d’informations sur le fonctionnement des environnements de Service d’application avec des réseaux virtuels et réseaux locaux consultez hello suivant des articles de [Architecture réseau][NetworkArchitectureOverview], [contrôle de trafic entrant Le trafic][ControllingInboundTraffic], et [tooBackends de connexion en toute sécurité][SecurelyConnectingToBackends]. 

## <a name="getting-started"></a>Prise en main
tooget démarré avec les environnements de Service d’application, consultez [comment tooCreate un environnement App Service][HowToCreateAnAppServiceEnvironment]

Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).

Pour plus d’informations sur la plateforme Azure App Service de hello, consultez [Azure App Service][AzureAppService].

Pour une vue d’ensemble de l’architecture en réseau environnement App Service de hello, consultez hello [présentation de l’Architecture réseau] [ NetworkArchitectureOverview] l’article.

Pour plus d’informations sur l’utilisation d’un environnement App Service grâce à ExpressRoute, consultez hello l’article suivant [Express Route et les environnements App Service][NetworkConfigDetailsForExpressRoute].

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


