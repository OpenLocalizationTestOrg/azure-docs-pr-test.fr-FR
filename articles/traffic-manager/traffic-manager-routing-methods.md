---
title: "les méthodes de routage du trafic aaaAzure Traffic Manager - | Documents Microsoft"
description: "Cela permet de que comprendre les méthodes de routage de trafic différents hello utilisées par le Gestionnaire de trafic les articles"
services: traffic-manager
documentationcenter: 
author: KumudD
manager: timlt
editor: 
ms.assetid: db1efbf6-6762-4c7a-ac99-675d4eeb54d0
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: kumud
ms.openlocfilehash: b3eeca63ab5f2b9cd4a3a6b6a8fd3e40059e32b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-routing-methods"></a>Méthodes de routage de Traffic Manager

Azure Traffic Manager prend en charge quatre le routage du trafic méthodes toodetermine comment tooroute réseau toohello de trafic différents points de terminaison de service. Traffic Manager applique hello-le routage du trafic méthode tooeach requête DNS qu’il reçoit. méthode de routage du trafic Hello détermine quel point de terminaison retourné dans la réponse DNS hello.

Quatre méthodes de routage du trafic sont disponibles dans Traffic Manager :

* **[Priorité](#priority):** sélectionnez **priorité** lorsque vous souhaitez toouse un point de terminaison de service principal pour tout le trafic et fournir des sauvegardes en cas de hello principal ou les points de terminaison de sauvegarde hello ne sont pas disponibles.
* **[Weighted](#weighted):** sélectionnez **Weighted** lorsque vous souhaitez toodistribute trafic sur un ensemble de points de terminaison, soit uniformément ou tooweights correspondants, que vous définissez.
* **[Performances](#performance):** sélectionnez **performances** lorsque vous avez des points de terminaison dans différents emplacements géographiques et que vous souhaitez que les utilisateurs finaux toouse hello le plus proche » » point de terminaison en termes de latence réseau la plus faible de hello.
* **[Géographique](#geographic):** sélectionnez **géographique** afin que les utilisateurs toospecific dirigée points de terminaison (Azure, externe ou imbriquées) basés quel emplacement géographique leur requête DNS provient. Cela permet des scénarios de tooenable clients Traffic Manager où connaître la région géographique de l’utilisateur et le routage en fonction de qui sont important. Exemples : respect des obligations en matière de souveraineté des données, localisation de contenu et d’expérience utilisateur, mesure du trafic en provenance de différentes régions.

Tous les profils Traffic Manager incluent une surveillance de l’intégrité des points de terminaison et un basculement de point de terminaison automatique. Pour plus d’informations, consultez la rubrique relative à la [surveillance des points de terminaison avec Traffic Manager](traffic-manager-monitoring.md). Un profil Traffic Manager donné ne peut utiliser qu’une seule méthode de routage du trafic. Vous pouvez sélectionner une méthode de routage du trafic différente pour votre profil à tout moment. Les modifications sont appliquées dans la minute, sans aucun temps d’arrêt. Les méthodes de routage du trafic peuvent être combinées dans des profils Traffic Manager imbriqués. Imbrication Active flexibles et élaborées configurations de routage du trafic qui répondent aux besoins hello des applications plus volumineux et complexes. Pour plus d’informations, consultez [Profils Traffic Manager imbriqués](traffic-manager-nested-profiles.md).

## <a name = "priority"></a>Méthode de routage du trafic basé sur la priorité

Souvent, une organisation souhaite fiabilité tooprovide pour ses services en déployant un ou plusieurs services de sauvegarde au cas où leur service principal tombe en panne. méthode Hello 'Priority'-le routage du trafic permet Azure clients tooeasily implémenter ce modèle de basculement.

![Méthode de routage du trafic « Priorité » d’Azure Traffic Manager][1]

Hello profil Traffic Manager contient une liste hiérarchisée de points de terminaison de service. Par défaut, Traffic Manager envoie tout le trafic toohello (priorité la plus élevée) point de terminaison principal. Si le point de terminaison principal hello n’est pas disponible, les itinéraires de Traffic Manager hello trafic toohello deuxième point de terminaison. Si les deux points de terminaison principal et secondaire de hello ne sont pas disponibles, le trafic de hello va toohello troisième, et ainsi de suite. Disponibilité du point de terminaison hello est basée sur état hello configuré (activé ou désactivé) et hello du point de terminaison en cours d’analyse.

### <a name="configuring-endpoints"></a>Configuration de points de terminaison

Avec Azure Resource Manager, vous définissez la priorité de point de terminaison hello explicitement à l’aide de propriété de 'priority' hello pour chaque point de terminaison. Cette propriété est une valeur comprise entre 1 et 1000. Plus la valeur est basse, plus la priorité est élevée. Des points de terminaison ne peuvent pas partager des valeurs de priorité. Définition de propriété de hello est facultative. Il est omis, une priorité par défaut basée sur l’ordre de point de terminaison hello est utilisée.

##<a name = "weighted"></a>Méthode de routage du trafic basé sur la pondération
Hello « Weighted »-le routage du trafic méthode vous permet de toodistribute trafic uniformément ou toouse une pondération prédéfinie.

![Méthode de routage du trafic « Pondéré » d’Azure Traffic Manager][2]

Dans la méthode de routage du trafic pondérée hello, vous affectez un point de terminaison tooeach poids dans la configuration du profil Traffic Manager hello. poids de Hello est un entier compris entre 1 too1000. Ce paramètre est facultatif. En cas d’omission, Traffic Manager utilise la pondération par défaut « 1 ».

Pour chaque requête DNS reçue, Traffic Manager choisit au hasard un point de terminaison disponible. probabilité Hello de choisir un point de terminaison est basée sur le poids hello affectés tooall les points de terminaison disponibles. À l’aide de hello même poids entre tous les points de terminaison entraîne une distribution du trafic même. Sur les points de terminaison spécifiques à l’aide de poids supérieur ou inférieurs provoque ces toobe de points de terminaison renvoyé plus ou moins fréquemment dans les réponses DNS hello.

méthode Hello pondérée permet des scénarios utiles :

* Mise à niveau progressive d’application : allouez un pourcentage de trafic tooroute tooa nouveau point de terminaison et augmentez progressivement le trafic de hello sur too100 % du temps.
* TooAzure de migration d’application : créer un profil avec des points de terminaison Azure et externes. Ajustez le poids hello hello points de terminaison tooprefer hello nouveaux points de terminaison.
* Éclatement de cloud pour une capacité supplémentaire : étendez rapidement un déploiement local dans le cloud de hello en le plaçant derrière un profil Traffic Manager. Lorsque vous avez besoin d’une capacité supplémentaire dans le cloud de hello, vous pouvez ajouter ou activer plusieurs points de terminaison et spécifier quelle portion du trafic passe tooeach le point de terminaison.

Hello portail Gestionnaire de ressources Azure prend en charge la configuration hello de routage du trafic pondéré.  Vous pouvez configurer le poids à l’aide de versions de gestionnaire de ressources hello hello API REST Azure PowerShell et CLI.

Il est important toounderstand que les réponses DNS sont mis en cache par les clients et par les serveurs DNS hello récursive qui hello les clients utilisent les noms DNS tooresolve. Cette mise en cache peut avoir une incidence sur les distributions de trafic pondérées. Si nombre hello de clients et les serveurs DNS récursive est élevé, la distribution du trafic fonctionne comme prévu. Toutefois, lorsque le nombre hello de clients ou aux serveurs DNS récursive est faible, la mise en cache peut fausser distribution du trafic hello.

Les cas d’utilisation courants sont les suivants :

* les environnements de développement et de test ;
* les communications d’application à application ;
* les applications destinées à une base étroite d’utilisateurs qui partagent une infrastructure DNS récursive commune (par exemple, des employés d’une entreprise se connectant via un proxy).

Ces effets de mise en cache DNS sont tooall le trafic DNS routage systèmes courants, pas seulement Azure Traffic Manager. Dans certains cas, l’explicitement effacement hello cache DNS peut fournir une solution de contournement. Dans d’autres cas, une autre méthode de routage du trafic peut être plus appropriée.

## <a name = "performance"></a>Méthode de routage du trafic basé sur les performances

Déploiement des points de terminaison de deux ou plusieurs emplacements de monde hello peut améliorer la réactivité de hello de nombreuses applications par le routage du trafic toohello emplacement tooyou « le plus proche ». méthode de routage du trafic « Performance » de Hello offre cette possibilité.

![Méthode de routage du trafic « Performance » d’Azure Traffic Manager][3]

point de terminaison « le plus proche » Hello n’est pas nécessairement le plus proche, mesurée avec la distance géographique. Au lieu de cela, hello méthode de routage du trafic « Performance » détermine le point de terminaison le plus proche hello en mesurant la latence du réseau. Traffic Manager gère une Table de latence Internet tootrack hello temps d’aller-retour entre les plages d’adresses IP et chaque centre de données Azure.

Traffic Manager recherche adresse hello source de la requête DNS entrante hello Bonjour Table de latence Internet. Traffic Manager choisit un point de terminaison disponible dans hello centre de données Azure qui a la latence la plus faible de hello pour la plage d’adresses IP, puis renvoie ce point de terminaison Bonjour réponse DNS.

Comme expliqué dans [Fonctionnement de Traffic Manager](traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager ne reçoit pas de requêtes DNS provenant directement de clients. Au lieu de cela, les requêtes DNS proviennent que les clients de hello sont toouse configuré le service DNS récursive hello. Par conséquent, hello adresse utilisée toodetermine hello « le plus proche » point de terminaison IP n’est pas hello adresse IP du client, mais il s’agit d’adresse IP de hello du service DNS récursive hello. Dans la pratique, cette adresse IP est un bon proxy pour les clients hello.


Traffic Manager régulièrement mises à jour hello tooaccount de Table de latence Internet les modifications apportées à hello global Internet et nouvelles régions Azure. Toutefois, des performances des applications varient en fonction des variations en temps réel de la charge entre hello Internet. Le routage du trafic Performance ne surveille pas la charge sur un point de terminaison de service donné. En revanche, si un point de terminaison devient indisponible, Traffic Manager ne l’inclut pas dans les réponses aux requêtes DNS.


Points toonote :

* Si votre profil contient plusieurs points de terminaison dans hello même région Azure, puis Traffic Manager distribue le trafic uniformément entre les points de terminaison disponibles hello dans cette région. Si vous préférez une distribution de trafic différente au sein d’une région, vous pouvez utiliser des [profils Traffic Manager imbriqués](traffic-manager-nested-profiles.md).
* Si toutes activées de points de terminaison le plus proche de Bonjour région Azure sont dégradées, Traffic Manager déplace les points de terminaison du trafic toohello dans la région Azure hello le plus proche suivante. Si vous souhaitez toodefine une séquence de basculement par défaut, utilisez [imbriqués profils Traffic Manager](traffic-manager-nested-profiles.md).
* Lors de l’utilisation de méthode de routage du trafic hello performances avec les points de terminaison externes ou imbriquées, vous avez besoin d’emplacement de hello toospecify de ces points de terminaison. Choisissez le déploiement de tooyour le plus proche hello région Azure. Ces emplacements sont des valeurs hello pris en charge par hello Table de latence Internet.
* algorithme Hello qui choisit de point de terminaison hello est déterministe. Répéter les requêtes DNS à partir de hello même client est dirigées vers toohello même point de terminaison. En règle générale, les clients utilisent des serveurs DNS récursifs différents quand ils se déplacent. client de Hello peut être routé tooa autre point de terminaison. Le routage peut aussi être affecté par les mises à jour toohello Table de latence Internet. Par conséquent, hello performances méthode de routage du trafic ne garantit pas qu’un client est toujours routé toohello même point de terminaison.
* Lorsque hello Table de latence Internet change, vous pouvez remarquer que certains clients sont dirigées tooa autre point de terminaison. La précision de ce changement de routage varie en fonction des données de latence en cours. Ces mises à jour sont la précision de hello toomaintain essentielles de performances-le routage du trafic comme hello Qu'internet évolue en permanence.

## <a name = "geographic"></a>Méthode de routage du trafic Geographic (Géographique)

Profils Traffic Manager peuvent être hello toouse configuré provient de l’emplacement géographique de la méthode de routage pour que les utilisateurs sont dirigés de points de terminaison toospecific (Azure, externe ou imbriquées) basées sur quel emplacement géographique, leur requête DNS. Cela permet des scénarios de tooenable clients Traffic Manager où connaître la région géographique de l’utilisateur et le routage en fonction de qui sont important. Exemples : respect des obligations en matière de souveraineté des données, localisation de contenu et d’expérience utilisateur, mesure du trafic en provenance de différentes régions.
Lorsqu’un profil est configuré pour le routage géographique, chaque point de terminaison associé à ce que le profil doit toohave un ensemble de régions géographiques affectées tooit. Une région géographique peut présenter les niveaux de granularité suivants : 
- World (Monde) : n’importe quelle région
- Regional Grouping (Regroupement régional) : Afrique, Moyen-Orient, Australie/Pacifique, etc. 
- Country/Region (Pays/Région) : Irlande, Pérou, Hong Kong (R.A.S.), etc. 
- State/Province (État/Province) : États-Unis-Californie, Australie-Queensland, Canada-Alberta, etc. (Remarque : ce niveau de granularité est pris en charge uniquement pour les états/provinces de l’Australie, du Canada, du Royaume-Uni et des États-Unis.)

Lorsqu’une région ou un ensemble de régions est assigné tooan le point de terminaison, toutes les demandes de ces régions obtient acheminés point de terminaison toothat uniquement. Traffic Manager utilise hello source IP adresse hello DNS toodetermine hello zone de la requête à partir de laquelle un utilisateur effectue une requête à partir de : il s’agit généralement hello adresseIP de résolution DNS local hello effectuant la requête hello pour le compte d’utilisateur de hello.  

![Méthode de routage du trafic « Geographic » (Géographique) d’Azure Traffic Manager](./media/traffic-manager-routing-methods/geographic.png)

Traffic Manager lit l’adresse hello source de la requête DNS de hello et décide de la région géographique d’origine. Il recherche ensuite toosee s’il existe un point de terminaison a tooit de cette région géographique mappée. Cette recherche commence au niveau de granularité le plus bas (État/Province où il est pris en charge, sinon au niveau de pays/région hello) hello et passe toutes les hello atteindre toohello plus haut niveau, qui est **World**. Hello première correspondance trouvée à l’aide de ce parcours est désignée comme tooreturn de point de terminaison hello en réponse à la requête hello. En cas de correspondance avec un point de terminaison de type imbriqué, un point de terminaison de ce profil enfant est renvoyé en fonction de sa méthode de routage. Hello les points suivants est applicables toothis comportement :

- Une région géographique peut être mappé uniquement tooone point de terminaison dans un profil Traffic Manager lorsque le type de routage hello est routage géographique. Cela garantit un routage déterministe du trafic des utilisateurs et permet aux clients de mettre en œuvre des scénarios nécessitant des limites géographiques claires.
- Si la région d’un utilisateur vient mise en correspondance des sous deux différents points de terminaison géographique, Traffic Manager sélectionne un point de terminaison hello avec une granularité plus faible hello et ne tient pas compte acheminer les demandes à partir de ce toohello région autre point de terminaison. Par exemple, considérons un profil présentant le type de routage Geographic (Géographique) et deux points de terminaison, Endpoint1 et Endpoint2. Endpoint1 est configuré trafic tooreceive irlandais et Endpoint2 est configuré trafic tooreceive d’Europe. Si une demande provient d’Irlande, il est toujours tooEndpoint1 routé.
- Dans la mesure où une région peut être mappé uniquement point de terminaison tooone, Traffic Manager retourne indépendamment de si le point de terminaison hello est sain ou non.

    >[!IMPORTANT]
    >Il est fortement recommandé que les clients à l’aide de la méthode de routage géographique hello associez-le hello Nested type points de terminaison a profils enfants contenant au moins deux points de terminaison au sein de chaque.
- Si une point de terminaison correspondance est trouvée, et ce point de terminaison est Bonjour **arrêté** d’état, Traffic Manager renvoie une réponse NODATA. Dans ce cas, aucune autres recherches n’est effectuée plus haut dans la hiérarchie de zone géographique hello. Ce comportement est également applicable pour les types de point de terminaison imbriquées lorsque le profil enfant hello est Bonjour **arrêté** ou **désactivé** état.
- Si un point de terminaison affiche un **désactivé** état, il ne seront pas incluse dans la région de hello processus de correspondance. Ce comportement est applicable pour les types de point de terminaison imbriquées lorsque le point de terminaison hello est hello **désactivé** état.
- Si une requête provient d’une région géographique qui n’a aucun mappage dans ce profil, Traffic Manager renvoie une réponse NODATA. Par conséquent, il est recommandé aux clients d’utiliser le routage géographique avec un point de terminaison, l’idéal est de type imbriqué avec au moins deux points de terminaison dans le profil enfant hello, avec la région de hello **World** affecté tooit. Cela garantit également que les adresses IP qui ne sont pas mappent tooa région sont gérées.

Comme expliqué dans [Fonctionnement de Traffic Manager](traffic-manager-how-traffic-manager-works.md), Traffic Manager ne reçoit pas de requêtes DNS provenant directement de clients. Au lieu de cela, les requêtes DNS proviennent que les clients de hello sont toouse configuré le service DNS récursive hello. Par conséquent, hello IP adresse utilisée toodetermine hello région n’est pas hello l’adresse IP du client, mais il s’agit d’adresse IP de hello du service DNS récursive hello. Dans la pratique, cette adresse IP est un bon proxy pour les clients hello.


## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toodevelop applications de haute disponibilité à l’aide de [surveillance de point de terminaison Traffic Manager](traffic-manager-monitoring.md)

Découvrez comment trop[créer un profil Traffic Manager](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-routing-methods/priority.png
[2]: ./media/traffic-manager-routing-methods/weighted.png
[3]: ./media/traffic-manager-routing-methods/performance.png



