---
title: "aaaNetwork détails de Configuration pour l’utilisation des Express Route"
description: "Détails de la configuration réseau pour les environnements de Service d’application en cours d’exécution dans des réseaux virtuels connectés tooan ExpressRoute Circuit."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 34b49178-2595-4d32-9b41-110c96dde6bf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/14/2016
ms.author: stefsch
ms.openlocfilehash: 85bbc45cfed619485957ee2a898aa0a7604173cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-configuration-details-for-app-service-environments-with-expressroute"></a>Détails de la configuration réseau pour les environnements App Service avec ExpressRoute
## <a name="overview"></a>Vue d'ensemble
Les clients peuvent se connecter une [Azure ExpressRoute] [ ExpressRoute] infrastructure de réseau virtuel tootheir du circuit, en étendant leur tooAzure de réseau local.  Vous pouvez créer un environnement App Service dans un sous-réseau de cette infrastructure de [réseau virtuel][virtualnetwork].  Applications qui s’exécutent sur hello environnement App Service peuvent établir puis les ressources tooback-fin de connexions sécurisées accessibles uniquement via hello connexion ExpressRoute.  

Un environnement App Service peut être créé **soit** dans un réseau virtuel Azure Resource Manager, **soit** dans un réseau virtuel de modèle de déploiement classique.  Suite à une modification récente effectuée en juin 2016, les ASE peuvent désormais être déployés dans les réseaux virtuels qui utilisent soit des plages d’adresses publiques soit des espaces d’adressage RFC1918 (par exemple, des adresses privées). 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="required-network-connectivity"></a>Connectivité réseau requise
Il existe des exigences de connectivité réseau pour les environnements de Service d’application qui ne peuvent pas être satisfaites initialement dans un réseau virtuel connecté de tooan ExpressRoute.  Les environnements App Service requièrent hello qui suit dans l’ordre toofunction correctement :

* Réseau sortant connectivité tooAzure stockage points de terminaison dans le monde sur les ports 80 et 443.  Cela inclut les points de terminaison situés dans hello même région que hello environnement App Service, ainsi que les points de terminaison de stockage situés dans **autres** régions Azure.  Résoudre les points de terminaison de stockage Azure sous hello suivant domaines DNS : *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net* et *file.core.windows.net*.  
* Toohello de connectivité réseau sortant des services de fichiers Azure sur le port 445.
* Points de terminaison tooSql base de données de connectivité réseau sortant situé dans hello même région de hello environnement App Service.  Résoudre les points de terminaison de base de données SQL sous hello suivant du domaine : *database.windows.net*.  Cela requiert l’ouverture des accès tooports 1433, 11000-11999 et 14000-14999.  Pour plus d’informations, consultez [cet article portant sur l’utilisation du port V12 de la base de données SQL](../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).
* Réseau sortant connectivité toohello Azure Gestion plan points de terminaison (points de terminaison ASM et ARM).  Cela inclut la connectivité sortante tooboth *management.core.windows.net* et *management.azure.com*. 
* Sortant trop de connectivité réseau*ocsp.msocsp.com*, *mscrl.microsoft.com* et *crl.microsoft.com*.  Il s’agit des fonctionnalités SSL toosupport nécessaires.
* configuration du DNS pour le réseau virtuel de hello Hello doit être capable de résoudre tous les points de terminaison hello et domaines mentionné dans hello points précédents.  Si ces points de terminaison ne peuvent pas être résolus, les tentatives de création d'environnement App Service échoueront et les environnements App Service existants seront marqués comme non intègres.
* L’accès sortant sur le port 53 est nécessaire pour la communication avec des serveurs DNS.
* Si un serveur DNS personnalisé existe sur hello l’autre extrémité d’une passerelle VPN, le serveur DNS de hello doit être accessible à partir du sous-réseau hello contenant hello environnement App Service. 
* chemin d’accès réseau sortant de Hello ne peut pas traverser des proxys d’entreprise internes, ni peut-elle être force tunneled tooon local.  Cette opération modifications hello efficace adresse NAT de trafic réseau sortant à partir de l’environnement App Service de hello.  La modification adresse NAT hello du trafic réseau sortant d’un environnement App Service entraînera la connectivité réduire des échecs de points de terminaison hello répertorié ci-dessus.  Cela entraîne des échecs de création d'environnement App Service, ainsi que la désignation comme non intègres des environnements App Service précédemment considérés comme intègres.  
* Trafic entrant de ports de toorequired d’accès réseau pour les environnements App Service doit être autorisées comme décrit dans cette [article][requiredports].

configuration requise du DNS Hello peut être remplie en garantissant une infrastructure DNS valide est configurée et gérée pour le réseau virtuel de hello.  Si pour n’importe quel hello raison configuration DNS est modifiée après la création d’un environnement App Service, les développeurs peuvent forcer un toopick environnement App Service de configuration DNS de la nouvelle hello.  Déclenchement d’un redémarrage environnement propagée à l’aide de hello « Redémarrer » située en haut de hello du Panneau de gestion d’environnement App Service hello Bonjour [portail Azure] [ NewPortal] entraîne hello environnement toopick la nouvelle configuration du DNS hello.

Hello exigences d’accès réseau entrant peuvent être remplies en configurant un [groupe de sécurité réseau] [ NetworkSecurityGroups] sur sous-réseau tooallow hello requis l’accès l’environnement Service hello application comme décrit dans cette [article][requiredports].

## <a name="enabling-outbound-network-connectivity-for-an-app-service-environment"></a>Activation de la connectivité réseau sortante pour un environnement App Service
Par défaut, un circuit ExpressRoute nouvellement créé publie un itinéraire par défaut qui autorise la connectivité Internet sortante.  Avec cette configuration, un environnement de Service d’application seront en mesure de tooconnect tooother points de terminaison Azure.

Toutefois, une configuration de client commune est toodefine leurs propres itinéraire par défaut (0.0.0.0/0), ce qui force le flux tooinstead de trafic Internet sortant en local.  Ce flux de trafic sauts immanquablement les environnements App Service, car le trafic sortant de hello est bloqué localement ou NAT qui a recours à ensemble non reconnaissable de tooan d’adresses qui ne fonctionnent plus avec différents points de terminaison Azure.

solution de Hello est toodefine une (ou plus) des itinéraires définis par l’utilisateur (UDRs) sur le sous-réseau hello contenant hello environnement App Service.  Un UDR définit les itinéraires de sous-réseau spécifique qui seront respectées au lieu de l’itinéraire par défaut hello.

Si possible, il est recommandé de hello toouse configuration suivante :

* configuration de ExpressRoute Hello annonce 0.0.0.0/0 et par défaut force tunnels tout le trafic sortant sur site.
* Hello UDR appliqué toohello sous-réseau contenant hello environnement App Service définit 0.0.0.0/0 avec un type de tronçon suivant d’Internet (Ceci est plu bas dans cet article).

Bonjour effets combinés de ces étapes est qu’au niveau du sous-réseau hello UDR ont priorité sur hello ExpressRoute forcé tunneling, garantissant ainsi un accès Internet sortant à partir de l’environnement App Service de hello.

> [!IMPORTANT]
> Hello itinéraires définis dans un UDR **doit** être suffisamment trop ont priorité sur les itinéraires annoncés par hello ExpressRoute configuration.  exemple Hello ci-dessous utilise la plage d’adresses 0.0.0.0/0 large hello et en tant que tel peut potentiellement être accidentellement remplacée par les annonces d’itinéraire à l’aide de plages d’adresses plus spécifiques.
> 
> Environnements de Service d’application ne sont pas pris en charge avec des configurations de ExpressRoute qui **cross-publier des routes de hello publics d’homologation toohello privés d’homologation chemin**.  Les configurations ExpressRoute ayant une homologation publique configurée reçoivent les annonces de routage depuis Microsoft pour un grand ensemble de plages d'adresses IP Microsoft Azure.  Si ces plages d’adresses sont publiés entre sur le chemin d’accès d’homologation privée hello, hello résulte que tous les paquets réseau sortant à partir du sous-réseau de l’environnement Service hello application sera infrastructure de réseau local du client tooa de tunneled en vigueur.  Ce flux de réseau n’est actuellement pas pris en charge par les environnements App Service.  Un problème de toothis de solution est toostop les itinéraires de publication croisée de hello publics d’homologation toohello privés d’homologation chemin d’accès.
> 
> 

Vous trouverez des informations générales sur les itinéraires définis par l'utilisateur dans cette [présentation][UDROverview].  

Pour plus d’informations sur la création et en configurant des itinéraires définis par l’utilisateur n’est disponible dans cette [comment tooGuide][UDRHowTo].

## <a name="example-udr-configuration-for-an-app-service-environment"></a>Exemple de configuration d'itinéraire défini par l'utilisateur pour un environnement App Service
**Conditions préalables**

1. Installez Azure Powershell à partir de hello [page de téléchargements Azure] [ AzureDownloads] (date d’effet juin 2015 ou version ultérieure).  Sous « Outils de ligne de commande », il existe un lien « Installer » sous « Windows Powershell » qui va installer les applets de commande Powershell dernière hello.
2. Nous vous recommandons de créer un sous-réseau unique pour un usage exclusif par un environnement App Service.  Cela garantit que ce sous-réseau de toohello hello UDRs appliquées s’ouvre uniquement le trafic sortant pour hello environnement App Service.
3. **Important**: ne déployez pas hello environnement App Service jusqu'à ce que **après** hello suivant les étapes de configuration est suivie.  Cela garantit que la connectivité réseau sortant est disponible avant d’essayer de toodeploy un environnement App Service.

**Étape 1 : Créer une table d’itinéraires nommée**

Hello extrait de code suivant crée une table de routage appelée « DirectInternetRouteTable » dans la région Ouest nous Azure hello :

    New-AzureRouteTable -Name 'DirectInternetRouteTable' -Location uswest

**Étape 2 : Créer un ou plusieurs itinéraires dans la table d’itinéraires hello**

Vous devez tooadd une ou plusieurs itinéraires toohello itinéraire dans l’ordre tooenable accéder à Internet.  

Hello recommandé approche pour la configuration toohello un accès sortant Qu'internet est toodefine un itinéraire pour 0.0.0.0/0 comme indiqué ci-dessous.

    Get-AzureRouteTable -Name 'DirectInternetRouteTable' | Set-AzureRoute -RouteName 'Direct Internet Range 0' -AddressPrefix 0.0.0.0/0 -NextHopType Internet

N’oubliez pas que 0.0.0.0/0 est une plage d’adresses d’étendue, en tant que tel sont remplacées par les plages d’adresses plus spécifiques publiés par hello ExpressRoute.  toore-itérer hello recommandation antérieure, un UDR avec un itinéraire 0.0.0.0/0 doit être utilisée conjointement avec une configuration ExressRoute qui seulement publie également 0.0.0.0/0. 

Comme alternative, vous pouvez télécharger une liste complète et mise à jour des plages CIDR utilisées par Azure.  Hello fichier Xml qui contient toutes les plages d’adresses IP Azure hello est disponible à partir de hello [Microsoft Download Center][DownloadCenterAddressRanges].  

Notez cependant que ces plages changent au fil du temps, d'où la nécessité des mises à jour manuelles périodique toohello définis tookeep itinéraires synchronisés.  Également, car il en existe une valeur par défaut est supérieur limite de 100 itinéraires dans un seul UDR, vous devez trop » résume « adresse d’IP Azure hello plages toofit au sein de la limite d’itinéraire hello 100, en n’oubliant pas que UDR itinéraires définis doivent toobe plus spécifique que les itinéraires hello publiés par votre ExpressRoute.  

**Étape 3 : Associer hello itinéraire table toohello sous-réseau contenant hello environnement App Service**

dernière étape de configuration Hello est le sous-réseau toohello table tooassociate hello itinéraire où hello environnement App Service sera déployé.  Hello commande suivant associe hello « DirectInternetRouteTable » toohello « ASESubnet » qui contiendra un environnement App Service.

    Set-AzureSubnetRouteTable -VirtualNetworkName 'YourVirtualNetworkNameHere' -SubnetName 'ASESubnet' -RouteTableName 'DirectInternetRouteTable'


**Étape 4 : Étapes finales**

Une fois la table d’itinéraires hello toohello lié sous-réseau, il est recommandé de toofirst test et confirmer hello destinée à effet.  Par exemple, déployez un ordinateur virtuel dans le sous-réseau de hello et vérifiez que :

* Le trafic sortant tooboth Azure et les points de terminaison non-Azure mentionnés précédemment dans cet article est **pas** circuler vers le bas hello circuit ExpressRoute.  Il est très important tooverify ce comportement, étant donné que si le trafic sortant à partir du sous-réseau de hello est toujours contraints tunneled localement, création d’un environnement de Service d’application est toujours échouent. 
* Les recherches DNS pour les points de terminaison hello mentionné plus haut sont tous résout correctement. 

Une fois que hello étapes ci-dessus sont confirmées, vous devez toodelete hello virtual machine, car le sous-réseau de hello doit toobe « vide » à hello de temps hello Qu'environnement App Service est créé.

Puis, passez à la création d'un environnement App Service !

## <a name="getting-started"></a>Prise en main
Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).

tooget démarré avec les environnements de Service d’application, consultez [Introduction tooApp environnement de Service][IntroToAppServiceEnvironment]

Pour plus d’informations sur la plateforme Azure App Service de hello, consultez [Azure App Service][AzureAppService].

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[requiredports]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[NetworkSecurityGroups]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[UDROverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-overview/
[UDRHowTo]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-how-to/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureDownloads]: http://azure.microsoft.com/en-us/downloads/ 
[DownloadCenterAddressRanges]: http://www.microsoft.com/download/details.aspx?id=41653  
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[NewPortal]:  https://portal.azure.com


<!-- IMAGES -->
