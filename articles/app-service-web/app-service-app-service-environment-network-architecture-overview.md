---
title: "aaaNetwork Architecture vue d’ensemble des applications Service environnements"
description: "Présentation de l'architecture de la topologie de réseau des environnements App Service."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 13d03a37-1fe2-4e3e-9d57-46dfb330ba52
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 3cbc86883f5687a9ada35a3ab2f577a450a3fa0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-architecture-overview-of-app-service-environments"></a>Présentation de l'architecture réseau des environnements App Service
## <a name="introduction"></a>Introduction
Les environnements App Service sont toujours créés dans un sous-réseau d’un [réseau virtuel] [ virtualnetwork] -applications en cours d’exécution dans un environnement App Service peuvent communiquer avec privé points de terminaison qui trouvent dans hello même virtuel topologie du réseau.  Étant donné que les clients peuvent verrouiller des parties de leur infrastructure réseau virtuel, il est important toounderstand des types de hello de flux de communication réseau qui se produisent avec un environnement App Service.

## <a name="general-network-flow"></a>Flux réseau général
Lorsqu’un environnement App Service (ASE) utilise une adresse IP virtuelle publique (VIP) pour les applications, tout le trafic entrant arrive sur cette adresse IP virtuelle publique.  Cela inclut le trafic HTTP et HTTPS pour les applications, ainsi que le reste du trafic pour les opérations de gestion Azure, les fonctionnalités de débogage à distance et FTP.  Pour obtenir la liste complète de hello des ports spécifiques (requis et facultatifs) qui sont disponibles sur l’adresse IP virtuelle publique de hello consultez l’article de hello sur [contrôler le trafic entrant] [ controllinginboundtraffic] tooan environnement App Service. 

Environnements de Service d’application prennent également en charge en cours d’exécution pour les applications qui sont liées uniquement tooa virtuel réseau adresse interne, également appelée tooas une adresse d’équilibrage de charge interne (équilibrage de charge interne).  Sur un équilibrage de charge interne activé trafic ASE, HTTP et HTTPS pour les applications, ainsi que les appels de débogage à distance, arrivent sur hello adresse d’équilibrage de charge interne.  Pour les configurations d’équilibrage de charge interne-ASE les plus courantes, le trafic FTP/FTPS également parviennent sur hello adresse d’équilibrage de charge interne.  Cependant les opérations de gestion Azure continuent de circuler tooports 454/455 sur hello une adresse IP virtuelle publique d’un équilibrage de charge interne activée ASE.

diagramme Hello ci-dessous montre une vue d’ensemble de hello différents flux réseau entrantes et sortantes pour un environnement App Service où les applications de hello sont les adresse IP virtuelle publique tooa liée :

![Flux de réseau généraux][GeneralNetworkFlows]

Un environnement App Service peut communiquer avec plusieurs points de terminaison client privés.  Par exemple, les applications qui s’exécutent dans un environnement App Service peut se connecter à toodatabase ou les serveurs s’exécutant sur des machines virtuelles IaaS de hello hello même topologie de réseau virtuel.

> [!IMPORTANT]
> En examinant organigramme hello, hello « autres calcul ressources » sont déployés dans un sous-réseau différent de celui de hello environnement App Service. Déploiement de ressources Bonjour même sous-réseau avec hello ASE bloque la connectivité à partir des ressources de toothose ASE (à l’exception spécifique intra-ASE routage). Déployer tooa sous-réseau différent à la place (dans hello même réseau virtuel). Hello environnement App Service sera alors en mesure de tooconnect. Aucune configuration supplémentaire n’est nécessaire.
> 
> 

Les environnements App Service communiquent également avec les ressources BD SQL et stockage Azure nécessaires pour la gestion et l'exploitation d'un environnement App Service.  Certaines des ressources Sql et le stockage hello un environnement App Service avec lequel communique se trouvent dans hello même région que hello environnement App Service, tandis que d’autres sont situés dans des régions Azure à distance.  Par conséquent, connectivité sortante toohello Internet est toujours requis pour une environnement App Service de toofunction correctement. 

Depuis un environnement App Service est déployé dans un sous-réseau, les groupes de sécurité réseau peuvent être utilisé toocontrol sous-réseau toohello de trafic entrant.  Pour plus d’informations sur la façon dont toocontrol entrants trafic tooan environnement App Service, voir hello [article][controllinginboundtraffic].

Pour plus d’informations sur la façon de tooallow une connectivité Internet sortante à partir d’un environnement App Service, consultez hello suivant de l’article sur l’utilisation de [Express Route][ExpressRoute].  Hello même approche décrite dans l’article de hello s’applique lorsque fonctionne avec la connectivité de Site à Site et que vous utilisez le tunneling forcé.

## <a name="outbound-network-addresses"></a>Adresses réseau sortantes
Lorsqu’un environnement App Service effectue des appels sortants, une adresse IP est toujours associée les appels sortants hello.  adresse IP spécifique Hello qui est utilisée varie selon que les point de terminaison hello appelée est situé au sein de la topologie du réseau virtuel hello ou en dehors de la topologie du réseau virtuel hello.

Si le point de terminaison hello appelée est **en dehors de** de topologie de réseau virtuel hello, puis hello sortant adresse (aka hello sortant NAT) qui est utilisé est hello une adresse IP virtuelle publique de hello environnement App Service.  Cette adresse peut être trouvée dans l’interface utilisateur du portail hello pour hello environnement App Service dans le panneau des propriétés.

![Adresse IP sortante][OutboundIPAddress]

Cette adresse peut également être déterminée pour ASEs possédant uniquement une adresse VIP publique en créant une application Bonjour environnement App Service, puis en effectuant une *nslookup* sur l’adresse de l’application hello. adresse IP de la résultante Hello est hello publique VIP, ainsi que les adresse NAT sortant de l’environnement hello App Service.

Si le point de terminaison hello appelée est **à l’intérieur de** de topologie de réseau virtuel hello, hello sortant de l’application appelante hello est adresse est hello adresse IP interne de ressources de calcul individuelles hello application hello en cours d’exécution.  Toutefois, il n’existe pas un mappage persistant de tooapps des adresses IP internes de réseau virtuel.  Applications peuvent se déplacer entre les ressources de calcul différente, et pool hello disponible des ressources de calcul dans un environnement App Service peut changer en raison d’opérations de tooscaling.

Toutefois, depuis un environnement App Service est toujours situé dans un sous-réseau, vous avez la garantie que les adresse IP interne hello d’une ressource de calcul une application en cours d’exécution seront se trouvent toujours dans la plage CIDR hello du sous-réseau de hello.  Par conséquent, lorsqu’ACL affinées ou groupes de sécurité réseau sont utilisés toosecure accéder aux points de terminaison tooother au sein du réseau virtuel de hello, hello plage de sous-réseau contenant hello environnement App Service besoins toobe accordé l’accès.

Hello diagramme suivant illustre ces concepts plus en détail :

![Adresses réseau sortantes][OutboundNetworkAddresses]

Bonjour diagramme ci-dessus :

* Hello une adresse IP virtuelle publique de hello environnement App Service étant 192.23.1.2, qui est l’adresse IP sortante hello utilisée lors d’appels trop points de terminaison « Internet ».
* Hello la plage CIDR de hello contenant le sous-réseau pour hello environnement App Service est 10.0.1.0/26.  Autres points de terminaison dans hello même infrastructure de réseau virtuel va apparaître dans les appels à partir d’applications provenant de quelque part dans cette plage d’adresses.

## <a name="calls-between-app-service-environments"></a>Appels entre les environnements App Service
Un scénario plus complexe peut se produire si vous déployez plusieurs environnements de Service d’application hello même réseau virtuel et effectuer des appels sortants à partir d’un environnement App Service tooanother environnement App Service.  Ces types d’appels entre les environnements App Service seront également traités comme des appels « Internet ».

Hello suivant schéma montre un exemple d’architecture multiniveau avec les applications sur un environnement App Service (par exemple) Les applications web « Porte ») appelant des applications sur un deuxième environnement App Service (par exemple, les applications d’API principal internes non prévus toobe accessible à partir de hello Internet). 

![Appels entre les environnements App Service][CallsBetweenAppServiceEnvironments] 

Bonjour exemple ci-dessus hello environnement App Service « ASE un » a une adresse IP sortante de 192.23.1.2.  Si une application en cours d’exécution sur cet environnement App Service rend une application de tooan appel sortant en cours d’exécution sur un deuxième environnement App Service (« ASE deux ») situé dans hello virtuel même réseau, hello sortant appel sera traité comme un appel de « Internet ».  Par conséquent le trafic réseau de hello arrivant sur hello deuxième environnement App Service affiche comme provenant de 192.23.1.2 (autrement dit, pas hello sous-réseau plage d’adresses de hello premier environnement App Service).

Bien que les appels entre différents environnements de Service d’application sont traités comme des appels de « Internet », quand les deux environnements de Service d’application sont situés dans hello même région Azure hello le trafic sera disponible sur le réseau Azure hello et ne sera pas physiquement flux sur hello Internet public.  Par conséquent, vous pouvez utiliser un groupe de sécurité réseau sur le sous-réseau hello Hello deuxième environnement App Service tooonly autorisent les appels entrants de hello premier environnement App Service (dont l’adresse IP sortante est 192.23.1.2), afin de garantir une communication sécurisée entre hello Environnements App Service.

## <a name="additional-links-and-information"></a>Informations et liens supplémentaires
Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).

Pour plus d’informations sur entrant des ports utilisés par les environnements App Service et le trafic entrant à l’aide de toocontrol de groupes de sécurité réseau est disponible [ici][controllinginboundtraffic].

Détails sur l’utilisation de défini par l’utilisateur itinéraires toogrant sortant Internet access tooApp environnements de Service est disponible dans cette [article][ExpressRoute]. 

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[controllinginboundtraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[ExpressRoute]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/

<!-- IMAGES -->
[GeneralNetworkFlows]: ./media/app-service-app-service-environment-network-architecture-overview/NetworkOverview-1.png
[OutboundIPAddress]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundIPAddress-1.png
[OutboundNetworkAddresses]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundNetworkAddresses-1.png
[CallsBetweenAppServiceEnvironments]: ./media/app-service-app-service-environment-network-architecture-overview/CallsBetweenEnvironments-1.png

