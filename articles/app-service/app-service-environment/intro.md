---
title: environnements App Service aaaIntroduction tooAzure
description: "Vue d’ensemble rapide des environnements Azure App Service"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 9261041333cf59374974a039edf89c4983c45cdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environments"></a>Environnements de Service Introduction tooApp #
 
## <a name="overview"></a>Vue d'ensemble ##

Azure App Service Environment est une fonctionnalité d’Azure App Service qui fournit un environnement totalement isolé et dédié pour l’exécution sécurisée de vos applications App Service à grande échelle. Cette fonctionnalité peut héberger vos [applications web][webapps], [applications mobiles][mobileapps], [applications d’API][APIapps] et [fonctions][Functions].

Les environnements App Service (ASE) conviennent aux charges de travail d’application qui nécessitent :

- Une très grande échelle.
- Une isolation et un accès réseau sécurisé.
- Une utilisation élevée de la mémoire.

Les clients peuvent créer plusieurs environnements App Service au sein d’une même région Azure ou dans plusieurs régions Azure. Grâce à cette souplesse, les environnements ASE sont parfaits pour l’évolution horizontale des niveaux d’application sans état pour la prise en charge de lourdes charges de travail RPS.

ASEs sont isolé toorunning uniquement les applications d’un client unique et sont toujours déployés dans un réseau virtuel. Les clients peuvent contrôler précisément le trafic réseau entrant et sortant des applications. Les applications peuvent établir des connexions de sécurisé à grande vitesse sur les ressources d’entreprise de réseaux privés virtuels tooon local.

Tous les articles et procédure-tooinstructions sur ASEs sont disponibles dans hello [fichier Lisezmoi pour les environnements App Service][ASEReadme]:

* Les environnements App Service autorisent l’hébergement d’application à grande échelle avec un accès réseau sécurisé. Pour plus d’informations, consultez hello [approfondie AzureCon](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) sur ASEs.
* Plusieurs ASEs peuvent être utilisé tooscale horizontalement. Pour plus d’informations, consultez [comment tooset d’un encombrement de l’application de géo-distribué](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/).
* ASEs peuvent être utilisé tooconfigure architecture de sécurité, comme indiqué dans hello approfondie AzureCon. toosee comment l’architecture de sécurité hello illustré hello approfondie AzureCon a été configuré, consultez hello [l’article sur la façon de tooimplement une architecture de sécurité en couches](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) avec les environnements App Service.
* L’accès aux applications qui s’exécutent sur des environnements App Service peut être contrôlé par des appareils en amont tels que les pare-feu d’applications web (WAF). Pour plus d’informations, consultez [Configuration d’un pare-feu d’applications Web (WAF) pour un environnement App Service](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall).

## <a name="dedicated-environment"></a>Environnement dédié ##

Un environnement app service est dédié exclusivement tooa seul abonnement et peuvent héberger des instances de 100. plage de Hello peut s’étendre sur 100 instances dans un seul Service d’applications plan too100 à instance unique du Service d’applications les plans et tous les éléments entre les deux.

Un environnement App Service est composé de frontends et de workers. Les frontends sont responsables de la terminaison du protocole HTTP/HTTPS et de l’équilibrage de charge automatique des demandes d’application dans un environnement App Service. Frontaux est automatiquement ajoutés en tant que hello plans App Service dans hello ASE sont monté en charge.

Les workers sont des rôles qui hébergent des applications clientes. Ils sont disponibles dans trois tailles fixes :

* Un cœur /3,5 Go de RAM
* Deux cœurs/7 Go de RAM
* Quatre cœurs/14 Go de RAM

Les clients n’avez pas besoin des travailleurs et frontaux toomanage. Toute infrastructure est automatiquement ajoutée à mesure que les clients augmentent l’échelle de leurs plans App Service. En tant que Service d’application plans sont créés ou mis à l’échelle dans un environnement app service, hello requis infrastructure est ajoutée ou supprimée comme il convient.

Il est un taux mensuel fixes pour ASE paie pour l’infrastructure de hello et ne change pas avec une taille de hello ASE hello. Chaque cœur de plan App Service présente aussi un coût. Toutes les applications hébergées dans un environnement app service sont Bonjour isolé tarification référence (SKU). Pour plus d’informations sur la tarification pour un environnement app service, consultez hello [tarification du Service d’applications] [ Pricing] page et passez en revue les options disponibles de hello pour ASEs.

## <a name="virtual-network-support"></a>Prise en charge des réseaux virtuels ##

Un environnement App Service peut être créé uniquement dans un réseau virtuel Azure Resource Manager. toolearn en savoir plus sur les réseaux virtuels Azure, consultez hello [Forum aux questions sur les réseaux Azure virtuel](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/). Un environnement App Service existe toujours dans un réseau virtuel, et plus précisément un sous-réseau d’un réseau virtuel. Vous pouvez utiliser les fonctionnalités de sécurité hello de réseaux virtuels toocontrol entrant et sortant réseau des communications pour vos applications.

Un environnement App Service peut être soit accessible sur Internet avec une adresse IP publique, soit accessible en interne avec uniquement une adresse d’équilibreur de charge interne (ILB) Azure.

[Groupes de sécurité réseau] [ NSGs] restreindre entrant communications toohello sous-réseau dans lequel un environnement app service réside. Vous pouvez utiliser des groupes de sécurité réseau des applications de toorun derrière les périphériques en amont et de services tels que WAFs et fournisseurs SaaS de réseau.

Les applications doivent également fréquemment tooaccess des ressources d’entreprise telles que les bases de données internes et les services web. Si vous déployez ASE hello dans un réseau virtuel qui dispose d’un réseau local VPN connexion toohello, applications hello Bonjour ASE accessible hello des ressources locales. Cette fonctionnalité est vrai que hello VPN soit ou non un [site-à-site](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) ou [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.

Pour plus d’informations sur le fonctionnement des environnements App Service avec des réseaux virtuels et des réseaux locaux, consultez [Considérations sur les réseaux d’environnement App Service][ASENetwork].

## <a name="app-service-environment-v1"></a>Environnement App Service v1 ##

L’environnement App Service est disponible en deux versions : ASEv1 et ASEv2. Hello informations précédentes était basé sur ASEv2. Cette indique la section hello de différences entre ASEv1 et ASEv2. 

Dans ASEv1, vous devez toomanage toutes les ressources de hello manuellement. Qui inclut frontaux hello, aux employés et les adresses IP utilisées pour SSL basée sur IP. Avant que vous pouvez faire évoluer votre plan App Service, vous devez toofirst évoluer hello worker pool dans lequel toohost il.

Les versions ASEv1 et ASEv2 utilisent un modèle de tarification différent. Dans ASEv1, vous payez pour chaque cœur alloué. Cela inclut les cœurs utilisés pour les frontends ou les workers qui n’hébergent pas de charges de travail. Dans ASEv1, taille de l’échelle de la valeur maximale par défaut hello d’un environnement app service est 55 nombre total d’hôtes. dont les workers et les frontends. Un avantage tooASEv1 est qu’il peut être déployé dans un réseau virtuel classique et un réseau virtuel du Gestionnaire de ressources. toolearn en savoir plus sur ASEv1, consultez [introduction de v1 environnement App Service][ASEv1Intro].

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
