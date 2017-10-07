---
title: aaaNested profils Traffic Manager | Documents Microsoft
description: "Cet article explique la fonctionnalité de « Profils imbriqués » hello de Azure Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f1b112c4-a3b1-496e-90eb-41e235a49609
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: e476d58a82ed94d12731156280c9665f980de0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="nested-traffic-manager-profiles"></a>Profils Traffic Manager imbriqués

Traffic Manager inclut un éventail de méthodes de routage du trafic qui vous toocontrol comment Traffic Manager choisit les points de terminaison doit recevoir le trafic à partir de chaque utilisateur final. Pour plus d’informations, consultez la rubrique relative aux [méthodes de routage du trafic dans Traffic Manager](traffic-manager-routing-methods.md).

Chaque profil Traffic Manager spécifie une seule méthode de routage du trafic. Toutefois, il existe des scénarios qui requièrent que le routage hello fournis par un seul profil Traffic Manager le routage du trafic plus sophistiquées. Vous pouvez imbriquer des avantages de hello de toocombine de profils Traffic Manager de plusieurs méthodes de routage du trafic. Profils imbriqués permettent toooverride hello par défaut Traffic Manager comportement toosupport plus volumineux et les déploiements d’applications plus complexes.

Hello suivant exemples illustre comment toouse imbriqués profils Traffic Manager dans divers scénarios.

## <a name="example-1-combining-performance-and-weighted-traffic-routing"></a>Exemple 1: combinaison de routage du trafic « performant (Performance) » et « pondéré (Weighted) »

Supposons que vous avez déployé une application Bonjour suivant des régions Azure : ouest des États-Unis, Europe de l’ouest et Asie orientale. Vous utilisez de Traffic Manager 'Performances' le routage du trafic méthode toodistribute trafic toohello région le plus proche toohello user.

![Profil Traffic Manager unique][4]

Maintenant, supposons que vous souhaitez tootest un service de tooyour de mise à jour avant de le déployer plus largement. Vous souhaitez toouse hello « pondéré »-le routage du trafic méthode toodirect un petit pourcentage du trafic tooyour du déploiement de tests. Pour configurer le déploiement de test hello en même temps que le déploiement de production existant hello en Europe de l’ouest.

Vous ne pouvez pas combiner les routages de trafic « Pondéré » et « Performance » dans un seul profil. toosupport ce scénario, vous créez un profil Traffic Manager à l’aide de points de terminaison hello deux Europe de l’ouest et méthode hello « Weighted »-le routage du trafic. Ensuite, vous ajoutez ce profil 'child' en tant qu’un profil de point de terminaison toohello 'parent'. profil de parent Hello utilise toujours hello méthode de routage du trafic de performances et contient hello autres déploiements comme points de terminaison.

Hello suivant le diagramme illustre cet exemple :

![Profils Traffic Manager imbriqués][2]

Dans cette configuration, le trafic est dirigé via le profil du parent hello répartit le trafic entre les régions normalement. Au sein de l’Europe de l’ouest, hello profil imbriqué distribue le trafic toohello production et test points de terminaison en fonction du poids toohello affectés.

Lorsque le profil de parent hello utilise la méthode de routage du trafic « Performance » hello, chaque point de terminaison doit être affecté à un emplacement. emplacement de Hello est attribué lorsque vous configurez le point de terminaison hello. Choisissez le déploiement de tooyour le plus proche hello région Azure. Hello régions Azure sont les valeurs d’emplacement hello pris en charge par hello Table de latence Internet. Pour plus d’informations, voir [Méthode de routage du trafic « Performance » d’Azure Traffic Manager](traffic-manager-routing-methods.md#performance).

## <a name="example-2-endpoint-monitoring-in-nested-profiles"></a>Exemple 2 : analyse de points de terminaison dans des profils imbriqués

Traffic Manager surveille activement l’intégrité de hello de chaque point de terminaison de service. Si un point de terminaison n’est pas sain, Traffic Manager dirige les utilisateurs tooalternative points de terminaison toopreserve hello disponibilité de votre service. Ce comportement de surveillance et de basculement de point de terminaison applique des méthodes de routage du trafic tooall. (pour plus d’informations, voir la rubrique relative à la [surveillance des points de terminaison avec Traffic Manager](traffic-manager-monitoring.md)) ; La surveillance des points de terminaison fonctionne différemment pour les profils imbriqués. Avec des profils imbriqués, profil parent de hello n’effectue pas les vérifications d’intégrité sur les enfants hello directement. Au lieu de cela, intégrité hello de points de terminaison du profil hello enfant est utilisé toocalculate hello l’intégrité globale du profil de hello enfant. Ces informations d’intégrité sont propagées vers la hiérarchie de profil hello imbriqué. Hello profil parent utilise cette toodetermine d’intégrité agrégé indique si le profil toodirect trafic toohello enfant. Consultez hello [FAQ](traffic-manager-FAQs.md#traffic-manager-nested-profiles) pour plus d’informations sur le contrôle d’intégrité des profils imbriqués.

Retourne l’exemple précédent de toohello, supposons que le déploiement de production hello en Europe de l’ouest échoue. Par défaut, le profil de 'child' hello dirige tous les déploiement de test toohello le trafic. Si le déploiement de test hello échoue également, profil parent de hello détermine que le profil enfant hello ne doit pas recevoir le trafic depuis tous les points de terminaison enfant ne sont pas intègres. Profil de parent hello distribue ensuite, le trafic toohello autres régions.

![Basculement de profil imbriqué (comportement par défaut)][3]

Il se peut que vous soyez satisfait de cette organisation. Ou vous pouvez être concerné que tout le trafic pour l’Europe de l’ouest va maintenant le déploiement de test toohello au lieu d’un trafic sous-ensemble limité. Quel que soit le contrôle d’intégrité hello Hello tester le déploiement, vous toofail sur toohello autres régions en cas d’échec du déploiement de production hello en Europe de l’ouest. tooenable ce basculement, vous pouvez spécifier hello 'MinChildEndpoints' paramètre lorsque vous configurez le profil enfant hello comme point de terminaison dans le profil de hello parent. paramètre Hello détermine le nombre minimal de hello de points de terminaison disponibles dans le profil enfant hello. valeur par défaut de Hello est '1'. Pour ce scénario, vous définissez hello MinChildEndpoints valeur too2. Sous ce seuil, profil parent de hello considère hello tout enfant profil toobe indisponible et dirige le trafic toohello autres points de terminaison.

Hello figure ci-dessous illustre cette configuration :

![Basculement de profil imbriqué avec « MinChildEndpoints » = 2][4]

> [!NOTE]
> Hello, méthode de routage du trafic 'Priority' distribue tout le trafic tooa seul point de terminaison. Il est par conséquent peu utile de définir un paramètre MinChildEndpoints autre que « 1 » pour un profil enfant.

## <a name="example-3-prioritized-failover-regions-in-performance-traffic-routing"></a>Exemple 3 : basculement hiérarchisé des régions dans le routage du trafic de type « Performance »

par défaut Hello pour hello méthode de routage du trafic « Performance » est conçue tooavoid trop forte chargement hello ensuite le plus proche du point de terminaison et à l’origine d’une série en cascade d’échecs. En cas d’échec d’un point de terminaison, tout le trafic qui aurait été dirigé toothat le point de terminaison est uniformément distribuées toohello autres points de terminaison dans toutes les régions.

![Routage du trafic « Performance » avec basculement par défaut][5]

Toutefois, supposons que vous préférez hello Europe de l’ouest trafic basculement tooWest nous, seule directe des régions tooother le trafic lorsque les deux points de terminaison ne sont pas disponibles. Vous pouvez créer cette solution à l’aide d’un profil enfant avec hello méthode de routage du trafic 'Priority'.

![Routage du trafic « Performance » avec basculement préférentiel][6]

Étant donné que le point de terminaison hello Europe de l’Ouest a une priorité plus élevée que le point de terminaison hello ouest des États-Unis, tout le trafic est envoyé de point de terminaison toohello Europe de l’ouest lorsque les deux points de terminaison sont en ligne. En cas d’Europe de l’ouest, le trafic est dirigé tooWest des États-Unis. Avec le profil de hello imbriqué, le trafic est dirigé tooEast Asie lors de l’échouent de l’Europe de l’ouest et ouest des États-Unis.

Vous pouvez répéter ce modèle pour toutes les régions. Remplacez toutes les trois points de terminaison dans le profil de parent hello trois profils enfants, chacun appliquant une séquence classée par priorité de basculement.

## <a name="example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-hello-same-region"></a>Exemple 4 : Contrôle de trafic « Performance » le routage entre plusieurs points de terminaison Bonjour même région

Supposons que hello 'Performances' méthode de routage du trafic est utilisée dans un profil qui a plus d’un point de terminaison dans une région particulière. Par défaut, le trafic dirigé toothat région est distribuée uniformément entre tous les points de terminaison disponibles dans cette région.

![Distribution du trafic au sein d’une région dans le cadre d’un routage du trafic « Performance » (comportement par défaut)][7]

Au que plusieurs points de terminaison soient ajoutés en Europe de l’Ouest, ces points de terminaison sont regroupés dans un profil enfant distinct. le profil enfant Hello est ajouté toohello parent en tant que point de terminaison uniquement hello en Europe de l’ouest. paramètres Hello sur le profil enfant hello peuvent contrôler la distribution de trafic de hello avec Europe de l’ouest en activant le routage du trafic pondéré ou basée sur des priorités au sein de cette région.

![Routage du trafic « Performance » avec distribution personnalisée du trafic au sein de la région][8]

## <a name="example-5-per-endpoint-monitoring-settings"></a>Exemple 5 : paramètres de surveillance par point de terminaison

Supposons que vous utilisez Traffic Manager toosmoothly migrer le trafic depuis une hérité local site web tooa nouvelle nuage version hébergée dans Azure. Site hérité de hello, vous voulez toouse hello page d’accueil URI toomonitor l’intégrité des sites. Mais pour la version de nuage nouvelle hello, vous implémentez une page de surveillance personnalisée (chemin d’accès ' / monitor.aspx') qui inclut des vérifications supplémentaires.

![Surveillance des points de terminaison Traffic Manager (comportement par défaut)][9]

paramètres d’analyse Hello dans un profil Traffic Manager s’appliquent tooall de points de terminaison dans un seul profil. Avec des profils imbriqués, vous utilisez un profil de différents enfants par toodefine site différent paramètres d’analyse.

![Surveillance des points de terminaison Traffic Manager avec paramétrage par point de terminaison][10]

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur les [profils Traffic Manager](traffic-manager-overview.md)

Découvrez comment trop[créer un profil Traffic Manager](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-nested-profiles/figure-1.png
[2]: ./media/traffic-manager-nested-profiles/figure-2.png
[3]: ./media/traffic-manager-nested-profiles/figure-3.png
[4]: ./media/traffic-manager-nested-profiles/figure-4.png
[5]: ./media/traffic-manager-nested-profiles/figure-5.png
[6]: ./media/traffic-manager-nested-profiles/figure-6.png
[7]: ./media/traffic-manager-nested-profiles/figure-7.png
[8]: ./media/traffic-manager-nested-profiles/figure-8.png
[9]: ./media/traffic-manager-nested-profiles/figure-9.png
[10]: ./media/traffic-manager-nested-profiles/figure-10.png
