---
title: "aaaSecurely connexion tooBackEnd ressources à partir d’un environnement App Service"
description: "Découvrez comment toosecurely connecter toobackend ressources à partir d’un environnement App Service."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a>En toute sécurité connexion tooBackend ressources à partir d’un environnement App Service
## <a name="overview"></a>Vue d'ensemble
Dans la mesure où un environnement App Service est toujours créé dans **soit** un réseau virtuel Azure Resource Manager, **ou** un modèle de déploiement classique [réseau virtuel] [ virtualnetwork], exclusivement sur le réseau virtuel de hello peuvent transférer des connexions sortantes depuis une ressources principales du tooother environnement App Service.  Suite à une modification récente effectuée en juin 2016, les environnements ASE peuvent également être déployés dans les réseaux virtuels qui utilisent soit des plages d’adresses publiques soit des espaces d’adressage RFC1918 (par exemple, des adresses privées).  

Par exemple, un serveur SQL Server peut être en cours d'exécution sur un cluster de machines virtuelles dont le port 1433 est verrouillé.  point de terminaison Hello peut-être ACLd tooonly autoriser l’accès à d’autres ressources sur hello même réseau virtuel.  

Comme autre exemple, des points de terminaison sensibles peuvent exécuter localement et être tooAzure connecté via une [Site-à-Site] [ SiteToSite] ou [Azure ExpressRoute] [ ExpressRoute] connexions.  Par conséquent, seules les ressources dans des réseaux virtuels connectés toohello Site à Site ou ExpressRoute tunnels sont tooaccess en mesure de points de terminaison de local.

Pour l’ensemble de ces scénarios, les applications s’exécutant sur un environnement App Service être toosecurely en mesure de se connectera toohello divers serveurs et ressources.  Le trafic sortant à partir d’applications qui s’exécutent dans un points de terminaison tooprivate environnement App Service Bonjour même réseau virtuel (ou connecté toohello même réseau virtuel), sera uniquement flux de réseau virtuel hello.  Tooprivate le trafic sortant points de terminaison ne seront pas déborder hello Internet public.

Un inconvénient s’applique toooutbound trafic à partir d’un tooendpoints environnement App Service dans un réseau virtuel.  Environnements de Service d’application ne peut pas atteindre les points de terminaison des machines virtuelles situées dans hello **même** sous-réseau hello environnement App Service.  Cela normalement ne doit pas être un problème tant que les environnements App Service sont déployés dans un sous-réseau réservé pour une utilisation exclusive par uniquement hello environnement App Service.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a>Connectivité sortante et configuration DNS requise
Pour une environnement App Service de toofunction correctement, il requiert points de terminaison de toovarious un accès sortant. Une liste complète des points de terminaison externes hello utilisé par un environnement app service est Bonjour section « Connectivité de réseau requis » Hello [Configuration du réseau pour ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) l’article.

Les environnements App Service nécessitent une infrastructure DNS valide configurée pour le réseau virtuel de hello.  Si pour n’importe quel hello raison configuration DNS est modifiée après la création d’un environnement App Service, les développeurs peuvent forcer un toopick environnement App Service de configuration DNS de la nouvelle hello.  Déclenchement d’un redémarrage environnement propagée à l’aide d’icône « Redémarrer » hello en haut hello Hello environnement App Service blade de gestion dans le portail de hello entraîne toopick d’environnement hello nouvelle configuration de DNS hello.

Il est également recommandé que tous les serveurs DNS personnalisés sur le réseau virtuel de hello être configuré à l’avance toocreating de temps préalable un environnement App Service.  Si la configuration de DNS d’un réseau virtuel est modifiée pendant la création d’un environnement App Service, qui entraîne au basculement de processus de création d’environnement App Service hello.  De la même manière, si un serveur DNS personnalisé existe sur hello autre extrémité d’une passerelle VPN et le serveur DNS de hello est inaccessible ou indisponible, hello environnement App Service processus de création échoue également.

## <a name="connecting-tooa-sql-server"></a>Tooa de connexion SQL Server
Une configuration courante de SQL Server comprend un point de terminaison qui écoute sur le port 1433 :

![Point de terminaison de SQL Server][SqlServerEndpoint]

Il existe deux approches pour restreindre le point de terminaison toothis le trafic :

* [Listes de contrôle d'accès réseau][NetworkAccessControlLists] (ACL réseau)
* [Groupes de sécurité réseau][NetworkSecurityGroups]

## <a name="restricting-access-with-a-network-acl"></a>Restriction de l'accès à l'aide d'une ACL réseau
Le port 1433 peut être sécurisé à l'aide d'une liste de contrôle d'accès réseau.  exemple Hello ci-dessous d’autorisation client résout provenant à l’intérieur d’un réseau virtuel, et bloque l’accès tooall autres clients.

![Exemple de liste de contrôle d'accès réseau][NetworkAccessControlListExample]

Toutes les applications en cours d’exécution dans l’environnement App Service dans hello même réseau virtuel hello SQL Server sera l’instance de SQL Server en mesure de tooconnect toohello à l’aide de hello **réseau virtuel interne** adresse IP pour la machine virtuelle de SQL Server hello.  

chaîne de connexion exemple Hello ci-dessous références hello SQL Server à l’aide de son adresse IP privée.

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

Bien que la machine virtuelle de hello a également un point de terminaison public, des tentatives de connexion à l’aide de l’adresse IP hello seront rejetées en raison de réseau de hello ACL. 

## <a name="restricting-access-with-a-network-security-group"></a>Restriction de l'accès à l'aide d'un groupe de sécurité réseau
Un groupe de sécurité réseau constitue une autre approche de sécurisation de l'accès.  Groupes de sécurité réseau peuvent être appliqué tooindividual virtuels, ou un sous-réseau tooa contenant des machines virtuelles.

Tout d’abord un groupe de sécurité réseau doit toobe créé :

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Restreindre l’accès tooonly le trafic de réseau virtuel interne est très simple avec un groupe de sécurité réseau.  règles par défaut de Hello dans un groupe de sécurité réseau autoriser uniquement l’accès à partir d’autres clients du réseau Bonjour même réseau virtuel.

Par conséquent verrouillage tooSQL d’accès serveur est aussi simple que l’application d’un groupe de sécurité réseau avec ses ordinateurs virtuels par défaut règles tooeither hello exécutant SQL Server, ou un sous-réseau hello contenant des machines virtuelles de hello.

exemple Hello ci-dessous s’applique à un sous-réseau toohello conteneur groupe de sécurité réseau :

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

résultat final de Hello est un ensemble de règles de sécurité qui bloquent l’accès externe, tout en autorisant un accès réseau virtuel interne :

![Règles de sécurité réseau par défaut][DefaultNetworkSecurityRules]

## <a name="getting-started"></a>Prise en main
Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).

tooget démarré avec les environnements de Service d’application, consultez [Introduction tooApp environnement de Service][IntroToAppServiceEnvironment]

Pour plus d’informations sur le contrôle du trafic entrant tooyour environnement App Service, consultez [contrôler le trafic entrant tooan environnement App Service][ControlInboundASE]

Pour plus d’informations sur la plateforme Azure App Service de hello, consultez [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
