---
title: "aaaOverview de métriques dans Microsoft Azure | Documents Microsoft"
description: "Découvrez comment toocustomize analyse graphiques dans Azure."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Vue d’ensemble des mesures dans Microsoft Azure
Tous les services Azure suivre les métriques clés qui permettent le contrôle d’intégrité de toomonitor hello, performances, disponibilité et l’utilisation de vos services. Vous pouvez afficher ces mesures Bonjour portail Azure, et vous pouvez également utiliser hello [API REST](https://msdn.microsoft.com/library/azure/dn931930.aspx) ou [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello jeu complet de métriques par programmation.

Pour certains services, vous devrez peut-être tooturn des diagnostics dans l’ordre toosee les métriques. Pour d’autres, telles que des ordinateurs virtuels, vous obtenez un ensemble de mesures de base, mais devez tooenable hello métriques de haute fréquence ensemble. Consultez [activation de la surveillance et de diagnostics](insights-how-to-use-diagnostics.md) toolearn plus.

## <a name="using-monitoring-charts"></a>Utilisation des graphiques de surveillance
Vous pouvez représenter des métriques de hello leur sur une période de temps que vous choisissez.

1. Bonjour [Azure Portal](https://portal.azure.com/), cliquez sur **Parcourir**, et ensuite une ressource que vous souhaitez analyser.
2. Hello **analyse** section contient des métriques les plus importantes hello pour chaque ressource Azure. Une application Web dispose, par exemple, de l’option **Demandes et erreurs**, alors qu’une machine virtuelle posséderait **Pourcentage UC** et **Lecture et écriture sur le disque :** ![Filtre Monitoring](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)
3. En cliquant sur tout graphique affichera vous hello **métrique** panneau. Dans Panneau de hello, en outre toohello graphique, est un tableau répertoriant les agrégations de métriques hello (par exemple, moyenne, minimale et maximale sur la plage de temps hello). Ci-dessous, qui est hello règles d’alerte pour les ressources hello.
    ![Volet Metric](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)
4. lignes hello toocustomize qui s’affiche, cliquez sur hello **modifier** bouton graphique de hello ou hello **modifier le graphique** commande sur le panneau de métrique hello.
5. Sur le panneau de modifier la requête hello, vous pouvez effectuer trois opérations :
   
   * Modifier la plage de temps hello
   * Basculer l’aspect hello entre barre et ligne
   * Choisir d’autres mesures ![Modifier la requête](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)
6. Modifier la plage de temps hello est aussi simple que la sélection d’une plage différente (tel que **dernière heure**) et en cliquant sur **enregistrer** bas hello du Panneau de hello. Vous pouvez également choisir **personnalisé**, ce qui vous permet de toochoose une période de temps sur hello cours des 2 dernières semaines. Par exemple, vous pouvez voir hello ensemble deux semaines ou simplement 1 heure d’hier. Tapez dans tooenter de zone de texte hello une autre heure.
    ![Intervalle de temps personnalisé](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)
7. Sous intervalle de temps hello, canal vous choisissez un nombre quelconque de tooshow métriques sur le graphique de hello.
8. Dès lors que vous cliquerez sur Enregistrer, vos modifications seront enregistrées pour cette ressource. Par exemple, si vous avez deux ordinateurs virtuels et que vous modifiez un graphique sur l’un, elle ne nuise pas hello autres.

## <a name="creating-side-by-side-charts"></a>Création de graphiques côte à côte
Personnalisation de puissantes hello dans le portail de hello, vous pouvez ajouter autant de graphiques que vous le souhaitez.

1. Bonjour **...**  menu en haut de hello de hello, cliquez sur panneau **ajouter des vignettes**:  
    ![Ajouter un menu](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. Ensuite, vous pouvez sélectionnez un graphique à partir de hello **galerie** sur le côté droit de hello de votre écran : ![la galerie](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. Si vous ne voyez pas métrique hello souhaité, vous pouvez toujours ajouter un des hello présélection des mesures, et **modifier** hello métrique de hello tooshow graphique dont vous avez besoin.

## <a name="monitoring-usage-quotas"></a>Surveillance des quotas d'utilisation
La plupart des mesures vous indiquent les tendances au fil du temps, mais certaines données, telles que les quotas d'utilisation, sont des informations limitées dans le temps et disposant d’un seuil.

Vous pouvez également voir des quotas d’utilisation sur le panneau hello pour les ressources qui ont des quotas :

![Usage](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

Comme avec les mesures, vous pouvez utiliser hello [API REST](https://msdn.microsoft.com/library/azure/dn931963.aspx) ou [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello ensemble complet des quotas d’utilisation par programmation.

## <a name="next-steps"></a>Étapes suivantes
* [Réception de notifications d'alerte](insights-receive-alert-notifications.md) lorsqu'une mesure dépasse un seuil.
* [Activation de la surveillance et de diagnostics](insights-how-to-use-diagnostics.md) toocollect détaillée des métriques de haute fréquence sur votre service.
* [Mettre automatiquement à l’échelle le nombre d’instances](insights-how-to-scale.md) toomake que votre service est disponible et réactive.
* [Surveiller les performances de l’application](../application-insights/app-insights-azure-web-apps.md) si vous souhaitez toounderstand exactement comment votre code s’exécute dans le cloud de hello.
* Utilisez [Application Insights pour les applications JavaScript avec des pages web](../application-insights/app-insights-web-track-usage.md) analytique de client tooget sur les navigateurs hello visiter une page web.
* [Surveillance de la disponibilité et de la réactivité des pages Web](../application-insights/app-insights-monitor-web-app-availability.md) avec Application Insights pour déterminer si vos pages sont inactives.

