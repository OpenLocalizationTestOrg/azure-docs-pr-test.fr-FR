---
title: aaaApplication carte dans Azure Application Insights | Documents Microsoft
description: "Une présentation visuelle des dépendances de hello entre les composants d’application, soit étiquetée au moyen d’indicateurs de performance clés et les alertes."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a>Mise en correspondance d’applications dans Application Insights
Dans [Azure Application Insights](app-insights-overview.md), mappage d’Application est une présentation visuelle des relations de dépendance hello de composants de votre application. Chaque composant affiche les indicateurs de performance clés telles que toohelp charge, les performances, les échecs et les alertes, vous découvrez un composant à l’origine d’un problème de performances ou l’échec. Vous pouvez cliquer à partir de n’importe quel composant toomore détaillée des diagnostics, comme les événements d’Application Insights. Si votre application utilise des services Azure, vous pouvez également cliquer diagnostics tooAzure, telles que des recommandations de l’Assistant de base de données SQL.

Comme les autres graphiques, vous pouvez épingler un toohello de mappage d’application Azure du tableau de bord, où il est entièrement fonctionnel. 

## <a name="open-hello-application-map"></a>Mappage d’application hello ouvert
Carte hello ouvert à partir du Panneau de vue d’ensemble de hello pour votre application :

![ouvrir la mise en correspondance d’applications](./media/app-insights-app-map/01.png)

![mise en correspondance d’applications](./media/app-insights-app-map/02.png)

carte de Hello montre :

* Tests de disponibilité
* Composant côté client (surveillé par hello SDK JavaScript)
* Composant côté serveur
* Dépendances de composants de client et serveur hello

Vous pouvez développer et réduire les groupes de liens de dépendance :

![réduire](./media/app-insights-app-map/03.png)

Si vous avez de nombreuses dépendances d’un type (SQL, HTTP, etc.), elles peuvent apparaître groupées. 

![dépendances groupées](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a>Détecter les problèmes
Chaque nœud possède des indicateurs de performance appropriés, tels que les taux de défaillance, les performances et la charge hello pour ce composant. 

Les icônes d’avertissement mettent en évidence les problèmes éventuels. Un avertissement orange signifie qu’il existe des défaillances dans les requêtes, les vues de page ou les appels de dépendance. Un avertissement rouge signifie un taux de défaillance de plus de 5 %. Si vous souhaitez tooadjust ces seuils, ouvrez les Options.

![icônes de défaillance](./media/app-insights-app-map/04.png)

En outre, des alertes actives s’affichent : 

![alertes actives](./media/app-insights-app-map/05.png)

Si vous utilisez SQL Azure, une icône vous indique des recommandations éventuelles sur la façon dont vous pouvez améliorer les performances. 

![Recommandation d’Azure](./media/app-insights-app-map/06.png)

Cliquez sur n’importe quel tooget icône plus de détails :

![Recommandation d’Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a>Clics pour le diagnostic
Chacun des nœuds hello sur la carte de hello offre ciblée de clics pour les diagnostics. options de Hello varient en fonction de type hello du nœud de hello.

![options de serveur](./media/app-insights-app-map/09.png)

Pour les composants qui sont hébergées dans Azure, les options de hello incluent des liens directs toothem.

## <a name="filters-and-time-range"></a>Filtres et période
Par défaut, mappage de hello récapitule toutes les données hello disponibles pour hello choisi la plage de temps. Mais vous pouvez le filtrer les noms d’opération spécifique uniquement tooinclude ou les dépendances.

* Nom de l’opération : cela inclut les vues de pages et les types de demandes côté serveur. Avec cette option, hello carte affiche hello indicateur de performance clé sur le nœud du côté serveur/client hello pour les opérations de hello sélectionné uniquement. Il montre les dépendances hello appelés dans le contexte de hello de ces opérations spécifiques.
* Nom de base de dépendance : Cela inclut les dépendances de navigateur hello AJAX et côté serveur. Si vous déclarez la télémétrie des dépendances personnalisées avec hello TrackDependency API, elles apparaissent également ici. Vous pouvez sélectionner tooshow de dépendances hello sur la carte de hello. Actuellement cette sélection ne filtre pas les demandes côté serveur hello ou des vues de page côté client hello.

![Définir les filtres](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a>Enregistrer les filtres
vous avez appliqué des filtres hello toosave, hello du code confidentiel filtré la vue sur un [tableau de bord](app-insights-dashboards.md).

![Code confidentiel toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a>Volet d’erreur
Lorsque vous cliquez sur un nœud dans le mappage de hello, un volet d’erreur s’affiche sur la droite hello résumer les échecs pour ce nœud. Les échecs sont tout d’abord regroupés par ID d’opération, puis par ID de problème.

![Volet d’erreur](./media/app-insights-app-map/error-pane.png)

En cliquant sur un échec vous prend toohello occurrence la plus récente de l’échec.

## <a name="resource-health"></a>Intégrité des ressources
Pour certains types de ressources, l’intégrité des ressources est affichée en haut de hello du volet d’erreur hello. Par exemple, en cliquant sur un nœud de SQL affiche les alertes qui ont déclenché et contrôle d’intégrité de la base de données hello.

![Intégrité des ressources](./media/app-insights-app-map/resource-health.png)

Vous pouvez cliquer sur des métriques hello ressources nom tooview vue d’ensemble standard de cette ressource.

## <a name="end-to-end-system-app-maps"></a>Cartes d’applications système de bout en bout

*Requiert le Kit de développement logiciel (SDK) version 2.3 ou ultérieure*

Si votre application comporte plusieurs composants - par exemple, un service principal en outre l’application web toohello -, puis vous pouvez afficher les tous sur le mappage d’une application intégrée.

![Définir les filtres](./media/app-insights-app-map/multi-component-app-map.png)

mappage d’application Hello recherche des nœuds de serveur en suivant les appels de dépendance HTTP entre les serveurs avec hello Qu'application Insights SDK installé. Chaque ressource Application Insights est supposé toocontain un seul serveur.

### <a name="multi-role-app-map-preview"></a>Mise en correspondance d’applications contenant plusieurs rôles (version préliminaire)

fonctionnalité de mappage plusieurs rôles application Hello préliminaire vous permet de toouse hello application mappés avec plusieurs serveurs d’envoi de données toohello même ressource Application Insights / clé d’instrumentation. Serveurs de mappage de hello sont segmentées par la propriété cloud_RoleName de hello sur les éléments de télémétrie. Définissez *mappage plusieurs rôles d’Application* trop*sur* de hello aperçus panneau tooenable cette configuration.

Cette approche peut s’avérer utile dans une application de services de micro ou dans d’autres scénarios où vous souhaitez que les événements de toocorrelate sur plusieurs serveurs au sein d’une seule ressource Application Insights.

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a>Commentaires
Veuillez fournir vos commentaires via l’option de commentaires portail hello.

![Image MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a>Étapes suivantes

* [portail Azure](https://portal.azure.com)
