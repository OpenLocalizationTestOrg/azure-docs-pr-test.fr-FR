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
# <a name="app-service-environment-documentation"></a>Documentation sur App Service Environment
 Azure App Service Environment est une fonctionnalité d’Azure App Service qui fournit un environnement totalement isolé et dédié pour l’exécution sécurisée de vos applications App Service à grande échelle. Il permet d’héberger vos [applications web][webapps], vos [applications mobiles][mobileapps], vos [applications API][APIApps] et vos [fonctions][Functions].

Les environnements App Service Environment (ASE) constituent le meilleur choix pour les charges de travail applicatives présentant les exigences suivantes :

* Très grande échelle.
* Isolation et accès réseau sécurisé.

Les clients peuvent créer plusieurs environnements ASE au sein d’une même région Azure, ainsi que dans plusieurs régions Azure. Grâce à cette polyvalence, les environnements ASE sont parfaits pour l’évolution horizontale des applications sans état pour la prise en charge de lourdes charges de travail RPS.

ASEs sont isolé toorunning uniquement les applications d’un client unique et sont toujours déployés dans un réseau virtuel Azure. Les clients peuvent contrôler précisément le trafic réseau entrant et sortant des applications à l’aide des [groupes de sécurité réseau][NSGs]. Applications peuvent également établir des connexions sécurisées à grande vitesse sur les ressources d’entreprise de réseaux virtuels tooon local.

Les applications ont souvent besoin tooaccess des ressources d’entreprise, telles que les bases de données internes et les services web. Les applications qui s’exécutent dans des environnements ASE peuvent accéder aux ressources via des connexions VPN [site-à-site][SiteToSite] et [Azure ExpressRoute][ExpressRoute].

* [Qu’est-ce qu’un environnement App Service Environment ?][Intro]
* [Créer un environnement App Service Environment][MakeExternalASE]
* [Créer un environnement App Service Environment avec équilibreur de charge interne][MakeILBASE]
* [Utiliser un environnement App Service Environment][UsingASE]
* [Considérations relatives à la mise en réseau et hello environnement App Service][ASENetwork]
* [Créer un environnement App Service Environment à partir d’un modèle][MakeASEfromTemplate]


## <a name="videos"></a>Vidéos
PaaS moderne de master pour hello entreprise avec le Service d’application Azure
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

Déploiement d’applications hautement évolutives et sécurisées
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

Exécution d’applications web et mobiles d’entreprise sur Azure App Service
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a>Environnement App Service v1 ##
Il existe deux versions d’App Service Environment : ASEv1 et ASEv2. Pour plus d’informations sur ASEv1, consultez la [documentation sur App Service Environment v1][ASEv1README].


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
