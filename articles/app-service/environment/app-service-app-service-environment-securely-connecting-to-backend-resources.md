---
title: "Connexion sécurisée à des ressources de backend à partir d'un environnement App Service"
description: "Découvrez comment connecter de façon sécurisée des ressources de backend à partir d'un environnement App Service."
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
ms.openlocfilehash: a43d88d64710b95dd753c19f02582f22accac8b6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a>Connexion sécurisée à des ressources de backend à partir d'un environnement App Service
## <a name="overview"></a>Vue d'ensemble
Étant donné qu’un environnement App Service est toujours créé **soit** dans un réseau virtuel Azure Resource Manager **ou** un [réseau virtuel][virtualnetwork] de modèle de déploiement classique, les connexions sortantes d’un environnement App Service à destination d’autres ressources de back-end peuvent passer exclusivement sur le réseau virtuel.  Suite à une modification récente effectuée en juin 2016, les environnements ASE peuvent également être déployés dans les réseaux virtuels qui utilisent soit des plages d’adresses publiques soit des espaces d’adressage RFC1918 (par exemple, des adresses privées).  

Par exemple, un serveur SQL Server peut être en cours d'exécution sur un cluster de machines virtuelles dont le port 1433 est verrouillé.  Le point de terminaison peut être placé dans une liste de contrôle d'accès pour autoriser uniquement l'accès à partir d'autres ressources se trouvant sur le même réseau virtuel.  

De même, les points de terminaison sensibles peuvent s'exécuter localement et être connectés à Azure via des connexions [de site à site][SiteToSite] ou [Azure ExpressRoute][ExpressRoute].  Par conséquent, seules les ressources des réseaux virtuels connectés aux tunnels site à site ou ExpressRoute peuvent accéder aux points de terminaison locaux.

Pour tous ces scénarios, les applications s'exécutant dans un environnement App Service peuvent se connecter de façon sécurisée aux différents serveurs et aux différentes ressources.  Le trafic sortant à partir d'applications qui s'exécutent dans un environnement App Service vers des points de terminaison privés se trouvant sur le même réseau virtuel (ou connectés au même réseau virtuel) circulent uniquement sur le réseau virtuel.  Le trafic sortant vers des points de terminaison privés ne circule pas via le réseau Internet public.

L’inconvénient est que le trafic sortant à partir d’un environnement App Service circule vers des points de terminaison se trouvant sur un réseau virtuel .  Les environnements App Service ne peuvent pas atteindre les points de terminaison de machines virtuelles situées dans le **même** sous-réseau que l'environnement App Service.  Cela ne devrait normalement pas poser de problème tant que les environnements App Service sont déployés dans un sous-réseau réservé à un usage exclusif par l'environnement App Service.

[!INCLUDE [app-service-web-to-api-and-mobile](../../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a>Connectivité sortante et configuration DNS requise
Pour qu’un environnement App Service fonctionne correctement, il requiert un accès sortant à différents points de terminaison. Une liste complète des points de terminaison externes utilisés par un ASE est disponible dans la section « Connectivité réseau requise » de l’article [Configuration réseau pour ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) .

Les environnements App Service nécessitent une infrastructure DNS valide configurée pour le réseau virtuel.  Si, pour une raison quelconque, la configuration DNS est modifiée après la création d'un environnement App Service, les développeurs peuvent forcer un environnement App Service à récupérer la nouvelle configuration DNS.  Le déclenchement d'un redémarrage d'un environnement propagé à l'aide de l'icône « Redémarrer » située en haut du panneau de gestion de l'environnement App Service du portail force l'environnement à récupérer la nouvelle configuration DNS.

Il est également recommandé de configurer les serveurs DNS personnalisés sur le réseau virtuel à l'avance, avant de créer un environnement App Service.  Si la configuration DNS d'un réseau virtuel est modifiée pendant la création d'un environnement App Service, alors le processus de création de l'environnement App Service échouera.  De même, s’il existe un serveur DNS personnalisé à l’autre extrémité d’une passerelle VPN et que le serveur DNS n’est pas accessible ou disponible, le processus de création d’un environnement App Service échoue également.

## <a name="connecting-to-a-sql-server"></a>Connexion à un serveur SQL Server
Une configuration courante de SQL Server comprend un point de terminaison qui écoute sur le port 1433 :

![Point de terminaison de SQL Server][SqlServerEndpoint]

Pour limiter le trafic sur ce point de terminaison, vous avez le choix entre deux approches :

* [Listes de contrôle d'accès réseau][NetworkAccessControlLists] (ACL réseau)
* [Groupes de sécurité réseau][NetworkSecurityGroups]

## <a name="restricting-access-with-a-network-acl"></a>Restriction de l'accès à l'aide d'une ACL réseau
Le port 1433 peut être sécurisé à l'aide d'une liste de contrôle d'accès réseau.  L'exemple ci-dessous place dans une liste approuvée les adresses de clients provenant d'un réseau virtuel, et bloque l'accès à tous les autres clients.

![Exemple de liste de contrôle d'accès réseau][NetworkAccessControlListExample]

Toutes les applications s'exécutant dans un environnement App Service du même réseau virtuel que le serveur SQL Server peuvent se connecter à l'instance SQL Server à l'aide de l'adresse IP de **réseau virtuel interne** de la machine virtuelle SQL Server.  

L'exemple de chaîne de connexion ci-dessous fait référence au serveur SQL Server en utilisant son adresse IP privée.

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

Même si la machine virtuelle possède également un point de terminaison public, les tentatives de connexion à l'aide de l'adresse IP publique sont rejetées en raison de l'ACL réseau. 

## <a name="restricting-access-with-a-network-security-group"></a>Restriction de l'accès à l'aide d'un groupe de sécurité réseau
Un groupe de sécurité réseau constitue une autre approche de sécurisation de l'accès.  Les groupes de sécurité réseau peuvent être appliqués à des machines virtuelles individuelles ou à un sous-réseau comprenant des machines virtuelles.

Un groupe de sécurité réseau doit tout d'abord être créé :

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Il est très simple de restreindre l'accès exclusivement au trafic d'un réseau virtuel interne à l'aide d'un groupe de sécurité réseau.  Les règles par défaut d'un groupe de sécurité réseau autorisent l'accès uniquement à partir d'autres clients réseau du même réseau virtuel.

Par conséquent, il est aussi simple de verrouiller l'accès à SQL Server que d'appliquer un groupe de sécurité réseau avec ses règles par défaut aux machines virtuelles exécutant SQL Server ou au sous-réseau comprenant des machines virtuelles.

L'exemple ci-dessous applique un groupe de sécurité réseau au sous-réseau conteneur :

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

Le résultat final est un ensemble de règles de sécurité qui bloquent l'accès externe, tout en autorisant l'accès au réseau virtuel interne :

![Règles de sécurité réseau par défaut][DefaultNetworkSecurityRules]

## <a name="getting-started"></a>Prise en main
Pour bien démarrer avec les environnements App Service, consultez [Présentation de l’environnement App Service][IntroToAppServiceEnvironment]

Pour plus d'informations sur le contrôle du trafic entrant vers votre environnement App Service, consultez [Contrôle du trafic entrant vers un environnement App Service][ControlInboundASE]

[!INCLUDE [app-service-web-try-app-service](../../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  app-service-app-service-environment-control-inbound-traffic.md
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  app-service-app-service-environment-intro.md
[ControlInboundASE]:  app-service-app-service-environment-control-inbound-traffic.md

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
