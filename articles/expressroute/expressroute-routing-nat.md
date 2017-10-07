---
title: NAT pour Azure ExpressRoute | Microsoft Docs
description: "Cette page détaille les conditions nécessaires à la configuration et à la gestion du routage pour les circuits ExpressRoute."
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: osamam
ms.openlocfilehash: 7a8b760df90b545b5fbde2f614aef62dd3985bb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="nat-for-expressroute"></a>NAT pour ExpressRoute

services de cloud computing tooMicrosoft tooconnect à l’aide d’ExpressRoute, vous avez besoin tooset et gérer le routage. Certains fournisseurs de connectivité proposent la configuration et la gestion du routage comme un service géré. Vérifiez auprès de votre toosee de fournisseur de connectivité s’ils offrent de ce service. Si ce n’est pas le cas, vous devez respecter toohello suivant les exigences. 

Consultez toohello [Circuits et domaines de routage](expressroute-circuit-peerings.md) article pour obtenir une description de routage de hello sessions nécessitant toobe défini dans toofacilitate connectivité.

> [!NOTE]
> Microsoft ne prend pas en charge les protocoles de redondance de routeur (HSRP, VRRP, par exemple) pour les configurations à haute disponibilité. Nous nous appuyons sur une paire de sessions BGP par homologation pour la haute disponibilité.
> 
> 

## <a name="ip-addresses-used-for-peerings"></a>Adresses IP utilisées pour les homologations

Vous devez tooreserve quelques blocs de l’adresse IP adresses tooconfigure routage entre votre réseau et les routeurs de bord (MSEEs) d’entreprise de Microsoft. Cette section fournit une liste d’exigences et décrit les règles de hello concernant la manière dont ces adresses IP doivent être acquis et utilisés.

### <a name="ip-addresses-used-for-azure-private-peering"></a>Adresses IP utilisées pour l’homologation privée Azure

Vous pouvez utiliser des adresses IP privées ou homologations d’hello tooconfigure à des adresses IP publiques. plage d’adresses Hello utilisée pour configurer les itinéraires ne doit pas se chevaucher avec adresse plages utilisées toocreate réseaux virtuels dans Azure. 

* Vous devez réserver un sous-réseau /29 ou deux sous-réseaux /30 pour les interfaces de routage.
* utilisé pour le routage des sous-réseaux Hello peuvent être des adresses IP privées ou adresses IP publiques.
* les sous-réseaux Hello n’a pas doivent en conflit avec la plage de hello réservée par le client hello pour une utilisation dans le cloud de Microsoft hello.
* Si un sous-réseau /29 est utilisé, il est subdivisé en deux sous-réseaux /30. 
  * tout d’abord de Hello/30 sous-réseau sera utilisé pour le lien principal de hello et hello /30 deuxième sous-réseau sera utilisé pour le lien secondaire de hello.
  * Pour chacun des sous-réseaux de hello /30, vous devez utiliser hello première adresse IP du sous-réseau de hello /30 sur votre routeur. Microsoft n’utilisera pas hello deuxième adresse IP de tooset de sous-réseau hello /30 une session BGP.
  * Vous devez définir les deux sessions BGP pour notre [contrat SLA de disponibilité](https://azure.microsoft.com/support/legal/sla/) toobe valide.  

#### <a name="example-for-private-peering"></a>Exemple pour l’homologation privée

Si vous choisissez tooset de a.b.c.d/29 toouse des hello d’homologation, il doit être fractionné en deux /30 sous-réseaux. Dans l’exemple hello ci-dessous, nous allons nous intéresser à l’utilisation de sous-réseau de a.b.c.d/29 hello. 

a.b.c.d/29 sera fractionné tooa.b.c.d/30 et a.b.c.d+4/30 et transmis en aval tooMicrosoft via hello API de configuration. Vous allez utiliser a.b.c.d+1 comme hello VRF IP pour hello PE principal et Microsoft consommera a.b.c.d+2 comme hello IP VRF pour hello MSEE principal. Vous allez utiliser a.b.c.d+5 comme hello VRF IP pour hello secondaire PE et Microsoft va utiliser a.b.c.d+6 comme hello IP VRF pour hello MSEE secondaire.

Considérez un cas où vous sélectionnez tooset 192.168.100.128/29 d’homologation privée. 192.168.100.128/29 inclut les adresses de 192.168.100.128 too192.168.100.135, parmi lesquelles :

* 192.168.100.128/30 sera attribué toolink1, avec le fournisseur à l’aide de 192.168.100.129 et Microsoft à l’aide de 192.168.100.130.
* 192.168.100.132/30 sera attribué toolink2, avec le fournisseur à l’aide de 192.168.100.133 et Microsoft à l’aide de 192.168.100.134.

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a>Adresses IP utilisées pour les homologations publiques Azure et Microsoft

Vous devez utiliser des adresses IP publiques que vous possédez pour configurer des sessions BGP hello. Microsoft doit être la propriété de hello tooverify en mesure d’adresses IP de hello via Internet, les registres de routage et les registres de routage Internet. 

* Vous devez utiliser un unique/29 sous-réseau ou tooset deux /30 sous-réseaux des hello BGP d’homologation pour chaque homologation par circuit ExpressRoute (si vous avez plusieurs). 
* Si un sous-réseau /29 est utilisé, il est subdivisé en deux sous-réseaux /30. 
  * tout d’abord de Hello/30 sous-réseau sera utilisé pour le lien principal de hello et hello /30 deuxième sous-réseau sera utilisé pour le lien secondaire de hello.
  * Pour chacun des sous-réseaux de hello /30, vous devez utiliser hello première adresse IP du sous-réseau de hello /30 sur votre routeur. Microsoft n’utilisera pas hello deuxième adresse IP de tooset de sous-réseau hello /30 une session BGP.
  * Vous devez définir les deux sessions BGP pour notre [contrat SLA de disponibilité](https://azure.microsoft.com/support/legal/sla/) toobe valide.

## <a name="public-ip-address-requirement"></a>Spécification d’adresse IP publique

### <a name="private-peering"></a>Homologation privée

Vous pouvez choisir toouse les adresses IPv4 publiques ou privées pour l’homologation privée. Nous fournissons une isolation de bout en bout du trafic. Ainsi, le chevauchement des adresses avec d’autres clients n’est pas possible dans le cas de l’homologation privée. Ces adresses ne sont pas publié tooInternet. 

### <a name="public-peering"></a>Homologation publique

Hello chemin d’accès d’homologation publique Azure permet de vous tooconnect tooall services hébergés dans Azure sur les adresses IP publiques. Notamment les services répertoriés dans hello [ExpessRoute FAQ](expressroute-faqs.md) et tous les services hébergés par les éditeurs de logiciels indépendants sur Microsoft Azure. Connectivité tooMicrosoft Azure services publics d’homologation est toujours lancée à partir de votre réseau dans le réseau de Microsoft hello. Vous devez utiliser des adresses IP publiques pour le réseau de destination tooMicrosoft hello du trafic.

### <a name="microsoft-peering"></a>Homologation Microsoft

chemin d’accès d’homologation de Hello Microsoft vous permet de connecter des services de cloud computing tooMicrosoft qui ne sont pas pris en charge via hello chemin d’accès d’homologation publique Azure. liste Hello des services inclut les services Office 365, telles que Exchange Online, SharePoint Online, Skype entreprise et Dynamics 365. Microsoft prend en charge la connectivité bidirectionnelle sur l’homologation, Microsoft hello. Les services de cloud de tooMicrosoft le trafic destiné doivent utiliser des adresses IPv4 publiques valides avant leur entrée hello Microsoft réseau.

Assurez-vous que votre adresse IP et en tant que nombre sont tooyou inscrit dans un des registres hello répertoriées ci-dessous.

* [ARIN](https://www.arin.net/)
* [APNIC](https://www.apnic.net/)
* [AFRINIC](https://www.afrinic.net/)
* [LACNIC](http://www.lacnic.net/)
* [RIPENCC](https://www.ripe.net/)
* [RADB](http://www.radb.net/)
* [ALTDB](http://altdb.net/)

> [!IMPORTANT]
> Adresse IP publique adresses publiés tooMicrosoft via ExpressRoute ne doit pas être publié toohello Internet. Cela peut interrompre les services de connectivité de Microsoft tooother. Toutefois, les adresses IP publiques utilisées par les serveurs de votre réseau qui communiquent avec les points de terminaison O365 au sein de Microsoft peuvent être publiées via ExpressRoute. 
> 
> 

## <a name="dynamic-route-exchange"></a>Échange de routage dynamique

L’échange de routage s’effectuera via le protocole eBGP. Les sessions EBGP sont établies entre vos routeurs et pare-feu hello MSEEs. L’authentification des sessions BGP n’est pas obligatoire. Si nécessaire, un hachage MD5 peut être configuré. Consultez hello [configurer le routage](expressroute-howto-routing-classic.md) et [Circuit de mise en service de flux de travail et les États de circuit](expressroute-workflows.md) pour plus d’informations sur la configuration de sessions BGP.

## <a name="autonomous-system-numbers"></a>Numéros système autonomes

Microsoft utilisera le numéro AS 12076 pour les homologations publiques Azure, privées Azure et Microsoft. Nous avons réservée homologations de 65515 too65520 à un usage interne. Les numéros AS 16 bits et 32 bits sont pris en charge.

Il n’existe aucune exigence concernant une symétrie de transfert des données. chemins d’accès vers l’avant et retour Hello peuvent parcourir les paires de routeur différents. Les routages identiques doivent être publiés des deux côtés sur plusieurs paires de circuits vous appartenant. Métrique de routage n’est pas requis toobe identiques.

## <a name="route-aggregation-and-prefix-limits"></a>Agrégation de routages et limites de préfixes

Nous prenons en charge des too4000 préfixes publiés toous via hello homologation privée Azure. Cela peut être augmenté des too10, 000 préfixes si le module complémentaire de hello ExpressRoute premium est activé. Nous acceptons les préfixes too200 par session BGP pour Azure public et homologation Microsoft. 

session BGP Hello est supprimée si nombre hello de préfixes dépasse la limite de hello. Nous acceptons les itinéraires par défaut sur hello privés d’homologation lien uniquement. Fournisseur doit filtrer l’itinéraire par défaut et les adresses IP privées (RFC 1918) à partir de hello Azure publique et les chemins d’accès d’homologation de Microsoft. 

## <a name="transit-routing-and-cross-region-routing"></a>Routage de transit et routage entre régions

ExpressRoute ne peut pas être configuré comme des routeurs de transit. Vous devez toorely sur votre fournisseur de connectivité pour les services de routage de transit.

## <a name="advertising-default-routes"></a>Publication des routages par défaut

Les routages par défaut sont autorisés uniquement sur les sessions d’homologation privées Azure. Dans ce cas, nous achemine tout le trafic réseau de tooyour hello réseaux virtuels associés. Publication d’itinéraires par défaut dans l’homologation privée entraîne hello internet chemin d’accès Azure bloqué. Vous devez compter sur votre trafic tooroute de bord d’entreprise à partir d’et toohello internet pour les services hébergés dans Azure. 

 tooenable connectivité tooother Azure services et les services d’infrastructure, vous devez vous assurer d’un des éléments suivants de hello est en place :

* L’homologation publique Azure est activé tooroute trafic toopublic points de terminaison
* Vous utilisez connecté à internet tooallow définie par l’utilisateur routage pour chaque connexion Internet nécessitant de sous-réseau.

> [!NOTE]
> La publication des routages par défaut arrête Windows et toute autre activation de licence de machine virtuelle. Suivez les instructions [ici](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) toowork contourner ce problème.
> 
> 

## <a name="support-for-bgp-communities-preview"></a>Prise en charge des communautés BGP (version préliminaire)

Cette section fournit une vue d'ensemble de l'utilisation des communautés BGP avec ExpressRoute. Microsoft se publier d’itinéraires dans hello public et les chemins d’accès d’homologation de Microsoft avec les itinéraires marqués avec des valeurs de la Communauté approprié. Hello raisonnement pour ce faire, et hello plus d’informations sur la Communauté, les valeurs sont décrites ci-dessous. Microsoft, toutefois, ne respecteront pas toute communauté tooroutes avec balises de valeurs publiés tooMicrosoft.

Si vous vous connectez tooMicrosoft via ExpressRoute à n’importe quel emplacement d’homologation une dans une région géopolitique, avoir accès tooall Microsoft cloud services toutes les régions dans les limites géopolitiques hello. 

Par exemple, si vous connecté tooMicrosoft à Amsterdam via ExpressRoute, avoir accès tooall Microsoft cloud services hébergés dans Europe du Nord et Europe de l’ouest. 

Consultez toohello [ExpressRoute partenaires et les emplacements d’homologation](expressroute-locations.md) page pour une liste détaillée des régions géopolitiques, les régions Azure associées et correspondante ExpressRoute d’homologation emplacements.

Vous pouvez acheter plusieurs circuits ExpressRoute par région géopolitique. Connexions multiples vous offre des avantages significatifs sur la haute disponibilité toogeo-redondance échéance. Dans les cas où vous avez plusieurs circuits ExpressRoute, vous recevrez hello même ensemble de préfixes publié à partir de Microsoft sur l’homologation publique, hello et d’homologation de chemins d’accès. Cela signifie que vous disposez de plusieurs chemins de votre réseau vers Microsoft. Cela peut entraîner optimales toobe décisions de routage au sein de votre réseau. Par conséquent, vous pouvez rencontrer des services de connectivité non optimale des expériences toodifferent. 

Microsoft permet d’identifier les préfixes publiés via l’homologation publique et Microsoft d’homologation avec les valeurs de communauté BGP appropriées indiquant les préfixes de hello hello région est hébergé dans. Vous pouvez vous fier hello Communauté valeurs toomake approprié routage décisions toooffer [optimale toocustomers routage](expressroute-optimize-routing.md).

| **Région géopolitique** | **Région Microsoft Azure** | **Valeur de communauté BGP** |
| --- | --- | --- |
| **Amérique du Nord** | | |
| Est des États-Unis |12076:51004 | |
| Est des États-Unis 2 |12076:51005 | |
| Ouest des États-Unis |12076:51006 | |
| Ouest des États-Unis 2 |12076:51026 | |
| Centre-Ouest des États-Unis |12076:51027 | |
| États-Unis - partie centrale septentrionale |12076:51007 | |
| États-Unis - partie centrale méridionale |12076:51008 | |
| Centre des États-Unis |12076:51009 | |
| Centre du Canada |12076:51020 | |
| Est du Canada |12076:51021 | |
| **Amérique du Sud** | | |
| Sud du Brésil |12076:51014 | |
| **Europe** | | |
| Europe du Nord |12076:51003 | |
| Europe de l’Ouest |12076:51002 | |
| **Asie-Pacifique** | | |
| Est de l’Asie |12076:51010 | |
| Asie du Sud-Est |12076:51011 | |
| **Japon** | | |
| Est du Japon |12076:51012 | |
| Ouest du Japon |12076:51013 | |
| **Australie** | | |
| Est de l’Australie |12076:51015 | |
| Sud-est de l’Australie |12076:51016 | |
| **Inde** | | |
| Sud de l’Inde |12076:51019 | |
| Inde-Ouest |12076:51018 | |
| Inde-Centre |12076:51017 | |

Tous les itinéraires annoncés par Microsoft seront marqués avec la valeur de communauté approprié hello. 

> [!IMPORTANT]
> Les préfixes globaux seront marqués avec une valeur de communauté appropriée et seront publiés uniquement lorsque le module complémentaire Premium ExpressRoute est activé.
> 
> 

En outre toohello ci-dessus, Microsoft sera également baliser des préfixes basés sur service hello qu'auquel ils appartiennent. Cela s’applique d’homologation Microsoft toohello uniquement. tableau Hello ci-dessous fournit un mappage de valeur de communauté tooBGP de service.

| **Service** | **Valeur de communauté BGP** |
| --- | --- |
| **Microsoft Exchange** |12076:5010 |
| **SharePoint** |12076:5020 |
| **Skype Entreprise** |12076:5030 |
| **Dynamics 365** |12076:5040 |
| **Autres services Office 365** |12076:5100 |

> [!NOTE]
> Microsoft ne respecte pas les valeurs de communauté BGP que vous définissez sur tooMicrosoft publié des itinéraires de hello.
> 
> 

## <a name="next-steps"></a>Étapes suivantes

* Configurez votre connexion ExpressRoute.
  
  * [Créer un circuit ExpressRoute pour le modèle de déploiement classique hello](expressroute-howto-circuit-classic.md) ou [créer et modifier un circuit ExpressRoute à l’aide du Gestionnaire de ressources Azure](expressroute-howto-circuit-arm.md)
  * [Configurer le routage pour le modèle de déploiement classique hello](expressroute-howto-routing-classic.md) ou [configurer le routage pour le modèle de déploiement du Gestionnaire de ressources hello](expressroute-howto-routing-arm.md)
  * [Lier un tooan de réseau virtuel classique circuit ExpressRoute](expressroute-howto-linkvnet-classic.md) ou [lier un circuit ExpressRoute de tooan le Gestionnaire de ressources VNet](expressroute-howto-linkvnet-arm.md)

