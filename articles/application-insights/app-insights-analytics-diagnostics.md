---
title: "diagnostics d’aaaSmart des changements de performances d’application web dans Azure Application Insights | Documents Microsoft"
description: "Diagnostic automatique des pics d’activité ou des étapes de la télémétrie relative aux performances depuis votre application web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a>Diagnostiquer les changements soudains dans la télémétrie de votre application

*Cette fonctionnalité est en version préliminaire.*

Diagnostiquez des changements soudains dans les performances ou l’utilisation de votre application web d’un seul clic ! fonctionnalité des Diagnostics actives Hello est disponible chaque fois que vous créez un graphique de temps dans [Analytique](app-insights-analytics.md) dans [Application Insights](app-insights-overview.md). Partout où il existe une modification inhabituelle de tendance hello de vos résultats, par exemple un pic d’activité ou une adresse dip, Diagnostics actives identifie un modèle des dimensions et des valeurs connexes susceptibles d’expliquer les modifications hello. Cela vous permet de diagnostiquer le problème de hello rapidement. 

Dans cet exemple, Smart Diagnostics a identifié un modèle de valeurs de propriété associé hello modification et met en évidence la différence de hello entre les résultats avec et sans ce modèle :

![exemple de résultat de diagnostic analytique](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a>Diagnostiquer les modifications de données

1.  Exécutez une requête dans Analytics et affichez-la sous la forme d’un graphique de temps. 
2.  Cliquez sur l’un des points représentant un pic d’activité, le cas échéant.
 
    ![point représentant un pic d’activité](./media/app-insights-analytics-diagnostics/peak.png)

    Diagnostics prend quelques secondes toodiscover un modèle.

3. onglet des résultats de Diagnostics Hello affiche alors un modèle qui peut expliquer discontinuité de vos données.

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    texte Hello montre les valeurs de dimension hello apparaissant toocorrelate avec la touche MAJ enfoncée hello. Dans cet exemple, il est associé à une requête et à une version de navigateur spécifiques.

    Notez également les composants hello deux de hello graphique, avec hello filtre true et false. composant de false Hello indique une tendance inchangée. En d’autres termes, il n’existe aucune modification dans les résultats de télémétrie hello, si nous excluez la combinaison de problématique hello de dimensions Diagnostics a identifié. En revanche, les résultats de hello dans cette combinaison s’affichent une modification importante au sein de la zone hello mis en surbrillance d’enquête. Cela indique que les Diagnostics a trouvé une combinaison des propriétés qui explique la modification de hello.

4.  Si le modèle de hello est complexe, vous devez toohover sur **afficher tout** dimensions de hello toosee.

    ![afficher tout](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  En cas de Diagnostics ne recherche aucun toonotify modèle significatif sur hello que page de « aucun résultat » s’affiche. À ce stade, vous pouvez modifier votre requête. Par exemple, vous pouvez affiner la plage de temps hello et placement dans la requête Analytique, pour une analyse plus approfondie et potentiellement de meilleurs résultats.

Grâce à la base de connaissances hello qu’une page spécifique de votre site Web a un problème sur un navigateur particulier, vous pouvez désormais accéder à droite toohello problème page et examiner les modifications récentes.

## <a name="try-hello-demo"></a>Essayez hello démonstration

[Cliquez ici une démonstration de toosee](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) sur les exemples de données.

## <a name="how-it-works"></a>Fonctionnement

Diagnostics intelligente utilise un algorithme d’apprentissage non supervisé avancées en fonction de hello [DiffPatterns](app-insights-analytics-reference.md) opération. Il recherche des modèles candidats susceptibles d’expliquer hello modification des données. Il analyse l’impact hello de chaque candidat sur métrique de hello et montre le modèle de hello que mieux met en corrélation avec la modification de hello.

## <a name="no-diagnostic-points"></a>Aucun diagnostic n’est donné ?

Diagnostics actives ne fonctionne que lorsque hello suivant des critères est satisfait :

 * Le paramètre Smart Diagnostics est activé. Regardez sous l’icône Paramètres hello Analytique.
 * Hello option Diagnostics actives dans les paramètres de l’Analytique est sélectionné. 
 * Axe du temps : hello axe des abscisses du graphique de hello doit être de type `datetime`.
 * Graphique en courbes ou en aires : Diagnostics fonctionne uniquement avec ces types de graphique. Utilisez `| render timechart` ou `| render areachart` à fin hello de votre requête ; ou sélectionnez la ligne ou la zone de graphique à partir du sélecteur de liste déroulante hello.
 * Discontinuité : Il doit exister une discontinuité significative dans les données de salutation.
 * Suffisamment tooanalyze de points.
 * Ne plusieurs résument la clause de la requête de hello.
 * Aucune clause de projet qui contient une définition de nom avant hello ne résument la clause.

 
 ## <a name="related-articles"></a>Articles connexes

 * [Didacticiel Analytics](app-insights-analytics-tour.md)
 * [Active la détection](app-insights-proactive-diagnostics.md) vous avertit automatiquement les problèmes de tooperformance.
