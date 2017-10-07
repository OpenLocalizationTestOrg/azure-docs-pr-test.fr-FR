---
title: aaaWhat est Traffic Manager | Documents Microsoft
description: "Cet article vous aidera à comprendre les nouveautés de Traffic Manager, et s’il s’agit des choix de routage de trafic droite hello pour votre application"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a>Vue d’ensemble de Traffic Manager

Microsoft Azure Traffic Manager vous permet de distribution de hello toocontrol du trafic utilisateur pour les points de terminaison de service dans différents centres de données. Les points de terminaison de service pris en charge par Traffic Manager incluent des machines virtuelles Azure, des applications web et des services cloud. Vous pouvez également utiliser Traffic Manager avec des points de terminaison externes non-Azure.

Traffic Manager utilise hello système DNS (Domain Name) toodirect demandes toohello plus approprié point de terminaison client basé sur une méthode de routage du trafic et d’un contrôle d’intégrité hello de points de terminaison hello. Traffic Manager fournit une gamme de [des méthodes de routage de trafic](traffic-manager-routing-methods.md) et [options de surveillance de point de terminaison](traffic-manager-monitoring.md) toosuit une autre application besoins et des modèles de basculement automatique. Traffic Manager est résilient toofailure, y compris échec hello d’un ensemble de la région Azure.

## <a name="traffic-manager-benefits"></a>Avantages de Traffic Manager

Traffic Manager peut vous aider à atteindre les objectifs suivants :

* **Améliorer la disponibilité des applications critiques**

    Traffic Manager vous permet de garantir une haute disponibilité de vos applications en surveillant vos points de terminaison et en fournissant un basculement automatique en cas de panne d’un point de terminaison.

* **Améliorer la réactivité des applications haute performance**

    Azure vous permet de toorun les services de cloud computing ou sites Web dans des centres de données situés monde hello. Traffic Manager permet d’améliorer la réactivité des applications en dirigeant le point de terminaison du trafic toohello avec une latence réseau la plus basse hello pour les clients hello.

* **Gérer les services sans les interrompre**

    Vous pouvez effectuer les opérations de maintenance planifiée sur vos applications sans temps d’arrêt. Traffic Manager dirige les points de terminaison tooalternative le trafic pendant la maintenance de hello.

* **Combiner des applications cloud et locales**

    Traffic Manager prend en charge externe, les points de terminaison non-Azure lui toobe utilisé avec hybride de cloud computing et les scénarios de « basculement au cloud » et les déploiements, y compris hello « croissance dans le cloud, » « migrer dans le cloud, » local.

* **Distribuer le trafic pour des déploiements vastes et complexes**

    À l’aide de [imbriqués profils Traffic Manager](traffic-manager-nested-profiles.md), méthodes de routage du trafic peuvent être combiné toocreate sophistiquées et hello toosupport de règles souples doit des déploiements plus volumineux et plus complexes.

## <a name="how-traffic-manager-works"></a>Fonctionnement de Traffic Manager

Azure Traffic Manager vous permet de distribution de hello toocontrol du trafic entre les points de terminaison de votre application. Un point de terminaison est tout service côté Internet hébergé à l’intérieur ou à l’extérieur d’Azure.

Traffic Manager offre deux principaux avantages :

1. Distribution du trafic en fonction de tooone de plusieurs [des méthodes de routage de trafic](traffic-manager-routing-methods.md)
2. [Analyse continue de l’intégrité des points de terminaison](traffic-manager-monitoring.md) et basculement automatique en cas d’échec des points de terminaison

Lorsqu’un client essaie tooconnect tooa service, il doit tout d’abord résoudre le nom DNS de hello d’adresse IP de hello service tooan. Hello puis se connecte le service hello tooaccess toothat IP adresse.

**toounderstand de point Hello plus important est que Traffic Manager fonctionne au niveau DNS hello.**  Traffic Manager utilise DNS toodirect clients toospecific des points de terminaison en fonction des règles hello de méthode de routage du trafic hello. Les clients connectent de point de terminaison toohello sélectionné **directement**. Traffic Manager n’est pas un proxy ou une passerelle. Traffic Manager ne voit pas de trafic hello entre le client de hello et le service de hello.

### <a name="traffic-manager-example"></a>Exemple Traffic Manager

Contoso Corp a développé un nouveau portail pour ses partenaires. URL de Hello pour ce portail est https://partners.contoso.com/login.aspx. application Hello est hébergée dans trois régions Azure. disponibilité de tooimprove et optimiser les performances globales, ils utilisent Traffic Manager toodistribute trafic toohello le plus proche disponible point de terminaison client.

tooachieve cette configuration, elles terminent hello comme suit :

1. Ils déploient trois instances de leur service. Hello DNS noms de ces déploiements sont « contoso-us.cloudapp .net », « contoso-eu.cloudapp .net », « contoso-asia.cloudapp .net ».
2. Créer un profil Traffic Manager, nommé « contoso.trafficmanager.net » et configurez-le toouse (méthode) hello « Performances »-le routage du trafic entre les points de terminaison hello trois.
* Configurer leur nom de domaine personnel, 'partners.contoso.com' toopoint too'contoso.trafficmanager.net », à l’aide d’un enregistrement DNS CNAME.

![Configuration DNS de Traffic Manager][1]

> [!NOTE]
> Lorsque vous utilisez un domaine personnel avec Azure Traffic Manager, vous devez utiliser un toopoint CNAME votre nom de domaine personnel domaine nom tooyour Traffic Manager. Les normes DNS ne vous permettent pas toocreate un enregistrement CNAME à hello 'apex' (ou racine) d’un domaine. Par conséquent, vous ne pouvez pas créer d’enregistrement CNAME pour « contoso.com » (parfois appelé un domaine « nu »). Vous pouvez uniquement créer un enregistrement CNAME pour un domaine sous « contoso.com », tel que « www.contoso.com ». toowork contourner cette limitation, nous recommandons d’utiliser un simples demandes toodirect de redirection HTTP pour « contoso.com » tooan autre nom tel que « www.contoso.com ».

### <a name="how-clients-connect-using-traffic-manager"></a>Connexion des clients à l’aide de Traffic Manager

Reprenons l’exemple précédent de hello, lorsqu’un client demande hello page https://partners.contoso.com/login.aspx, le client de hello effectue hello suivant le nom DNS d’étapes tooresolve hello et établir une connexion :

![Établissement de la connexion à l’aide de Traffic Manager][2]

1. Hello en envoyant une récursive de tooits configuré de requête DNS DNS service tooresolve hello nom 'partners.contoso.com'. Un service DNS récursif, parfois appelé service « DNS local », n’héberge pas directement de domaines DNS. Au lieu de cela, les clients hello transfère le travail de hello de contact hello DNS faisant autorité différents services sur hello Internet nécessaire tooresolve un nom DNS.
2. nom DNS de hello tooresolve, du service DNS récursive hello recherche des serveurs de noms hello pour le domaine « contoso.com » de hello. Il contacte ensuite ces enregistrement DNS de nom serveurs toorequest hello 'partners.contoso.com'. les serveurs DNS contoso.com Hello replacer hello CNAME qui pointe toocontoso.trafficmanager.net.
3. Ensuite, le service DNS hello récursive recherche des serveurs de noms hello pour domaine hello 'trafficmanager.net', qui sont fournies par hello Azure Traffic Manager service. Il envoie ensuite une demande de hello 'contoso.trafficmanager.net' DNS record toothose serveurs DNS.
4. serveurs de noms de Traffic Manager Hello recevoir la demande de hello. Ils choisissent un point de terminaison en fonction des critères suivants :

    - état Hello configuré de chaque point de terminaison (les points de terminaison désactivés ne sont pas retournées)
    - Hello actuel de chaque point de terminaison, comme déterminé par le contrôle d’intégrité de Traffic Manager hello vérifications. (pour plus d’informations, voir la rubrique relative à la [surveillance des points de terminaison avec Traffic Manager](traffic-manager-monitoring.md)) ;
    - Hello choisi la méthode de routage du trafic. (pour plus d’informations, voir [Méthodes de routage de Traffic Manager](traffic-manager-routing-methods.md)).

5. point de terminaison Hello choisi est retourné en tant qu’un autre enregistrement CNAME DNS. Dans ce cas, supposons que contoso-us.cloudapp.net est retourné.
6. Ensuite, le service DNS hello récursive recherche des serveurs de noms hello pour le domaine de 'cloudapp.net' hello. Il contacte ces hello de toorequest de serveurs de nom « contoso-us.cloudapp .net » enregistrement DNS. Un enregistrement DNS 'A' contenant l’adresse IP de hello du point de terminaison de service basé sur des États-Unis hello est retourné.
7. le service DNS Hello récursive consolide les résultats hello et retourne un seul client toohello de réponse DNS.
8. client de Hello reçoit les résultats DNS hello et connecte toohello les adresse IP donnée. Hello client connecte point de terminaison de service toohello application directement, non par le biais du Gestionnaire de trafic. Dans la mesure où il s’agit d’un point de terminaison HTTPS, client de hello effectue la négociation SSL/TLS nécessaire hello et puis effectue une demande HTTP GET pour hello ' / login.aspx' page.

le service DNS Hello récursive met en cache les réponses DNS hello qu’il reçoit. la résolution DNS Hello sur hello client met également en cache le résultat de hello. Mise en cache permet toobe de requêtes DNS ultérieur ayant obtenu une réponse plus rapidement en utilisant des données à partir du cache de hello au lieu d’interroger d’autres serveurs de noms. durée de Hello du cache de hello est déterminée par hello 'time-to-live' propriété (TTL) de chaque enregistrement DNS. Les valeurs plus courtes entraînent d’expiration de cache plus rapide et donc davantage d’allers-retours toohello Traffic Manager nom de serveurs. Des valeurs plus signifient que peut prendre plus de temps toodirect le trafic en dehors d’un point de terminaison ayant échoué. Traffic Manager vous permet de tooconfigure hello TTL utilisé dans toobe des réponses DNS Traffic Manager aussi faible que 0 seconde et aussi élevée que 2 147 483 647 secondes (hello plage maximale conforme [-la norme RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)), l’activation de valeur de hello toochoose qui équilibre mieux besoins hello de votre application.

## <a name="pricing"></a>Tarification

Pour des informations sur les prix, consultez [Tarification Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager/).

## <a name="faq"></a>Forum Aux Questions

Pour connaître les questions fréquemment posées, consultez la page [Forum Aux Questions (FAQ) relatif à Traffic Manager](traffic-manager-FAQs.md).

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur le [basculement automatique et la surveillance des points de terminaison](traffic-manager-monitoring.md)de Traffic Manager.

En savoir plus sur les [méthodes de routage du trafic](traffic-manager-routing-methods.md)de Traffic Manager.

En savoir plus sur certaines des hello autre clé [fonctionnalités de réseau](../networking/networking-overview.md) de Azure.

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png

