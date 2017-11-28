---
title: Diagnostics intelligents des modifications des performances des applications web dans Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: 5e53bc714d89bf6204681349e7890e0b8fbc7046
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="5a187-103">Diagnostiquer les changements soudains dans la télémétrie de votre application</span><span class="sxs-lookup"><span data-stu-id="5a187-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="5a187-104">*Cette fonctionnalité est en version préliminaire.*</span><span class="sxs-lookup"><span data-stu-id="5a187-104">*This feature is in preview.*</span></span>

<span data-ttu-id="5a187-105">Diagnostiquez des changements soudains dans les performances ou l’utilisation de votre application web d’un seul clic !</span><span class="sxs-lookup"><span data-stu-id="5a187-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="5a187-106">La fonctionnalité de diagnostics intelligents est disponible dès que vous créez un graphique de temps dans [Analytics](app-insights-analytics.md) dans [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a187-106">The Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="5a187-107">Dès lors qu’une modification soudaine de l’évolution de vos résultats est détectée (un pic ou un creux d’activité, par exemple), Smart Diagnostics identifie un modèle des dimensions et des valeurs connexes pouvant expliquer cette modification.</span><span class="sxs-lookup"><span data-stu-id="5a187-107">Wherever there is an unusual change from the trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain the change.</span></span> <span data-ttu-id="5a187-108">Cela vous permet de diagnostiquer rapidement le problème.</span><span class="sxs-lookup"><span data-stu-id="5a187-108">This helps you diagnose the problem quickly.</span></span> 

<span data-ttu-id="5a187-109">Dans cet exemple, Smart Diagnostics a identifié un modèle de valeurs de propriété associées à la modification, et met en évidence la différence entre les résultats avec et sans ce modèle :</span><span class="sxs-lookup"><span data-stu-id="5a187-109">In this example, Smart Diagnostics has identified a pattern of property values associated with the change, and highlights the difference between results with and without that pattern:</span></span>

![exemple de résultat de diagnostic analytique](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="5a187-111">Diagnostiquer les modifications de données</span><span class="sxs-lookup"><span data-stu-id="5a187-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="5a187-112">Exécutez une requête dans Analytics et affichez-la sous la forme d’un graphique de temps.</span><span class="sxs-lookup"><span data-stu-id="5a187-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="5a187-113">Cliquez sur l’un des points représentant un pic d’activité, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="5a187-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![point représentant un pic d’activité](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="5a187-115">Le diagnostic met quelques secondes à identifier un modèle.</span><span class="sxs-lookup"><span data-stu-id="5a187-115">Diagnostics takes a few seconds to discover a pattern.</span></span>

3. <span data-ttu-id="5a187-116">L’onglet des résultats du diagnostic affiche un modèle pouvant expliquer la discontinuité de vos données.</span><span class="sxs-lookup"><span data-stu-id="5a187-116">The Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="5a187-118">Le texte montre les valeurs de dimension qui semblent être en corrélation avec le décalage.</span><span class="sxs-lookup"><span data-stu-id="5a187-118">The text shows the dimension values that appear to correlate with the shift.</span></span> <span data-ttu-id="5a187-119">Dans cet exemple, il est associé à une requête et à une version de navigateur spécifiques.</span><span class="sxs-lookup"><span data-stu-id="5a187-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="5a187-120">Notez également les deux composants du graphique, avec un filtre true et false.</span><span class="sxs-lookup"><span data-stu-id="5a187-120">Notice also the two components of the chart, with the filter true and false.</span></span> <span data-ttu-id="5a187-121">Le composant false indique une tendance inchangée.</span><span class="sxs-lookup"><span data-stu-id="5a187-121">The false component shows an unchanged trend.</span></span> <span data-ttu-id="5a187-122">En d’autres termes, il n’y a aucune modification des résultats de télémétrie, si l’on exclut la combinaison problématique de dimensions identifiée par Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="5a187-122">In other words, there is no change in the telemetry results, if we exclude the problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="5a187-123">En revanche, les résultats de cette combinaison montrent une modification très importante dans la zone d’investigation sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5a187-123">By contrast, the results within that combination do show a dramatic change within the highlighted area of investigation.</span></span> <span data-ttu-id="5a187-124">Cela indique que Diagnostics a trouvé une combinaison de propriétés expliquant cette modification.</span><span class="sxs-lookup"><span data-stu-id="5a187-124">This shows that Diagnostics has found a combination of properties that explains the change.</span></span>

4.  <span data-ttu-id="5a187-125">Si le modèle est complexe, vous devrez passer la souris sur **Afficher tout** pour voir les dimensions.</span><span class="sxs-lookup"><span data-stu-id="5a187-125">If the pattern is complex, you need to hover over **Show all** to see the dimensions.</span></span>

    ![afficher tout](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="5a187-127">Si Diagnostics ne trouve aucun modèle significatif, la page « aucun résultat » s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5a187-127">In case Diagnostics finds no significant pattern to notify about, the ‘no results’ page will be presented.</span></span> <span data-ttu-id="5a187-128">À ce stade, vous pouvez modifier votre requête.</span><span class="sxs-lookup"><span data-stu-id="5a187-128">At this point, you may change your query.</span></span> <span data-ttu-id="5a187-129">Par exemple, vous pouvez limiter l’intervalle de temps et compartimenter la requête Analytics, pour une analyse plus approfondie et obtenir potentiellement de meilleurs résultats.</span><span class="sxs-lookup"><span data-stu-id="5a187-129">For example, you could narrow the time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="5a187-130">Maintenant que vous savez qu’une page spécifique de votre site web a un problème sur un navigateur en particulier, vous pouvez désormais accéder directement à la page en question et examiner les modifications récentes.</span><span class="sxs-lookup"><span data-stu-id="5a187-130">Armed with the knowledge that a particular page of your website has a problem on a particular browser, you can now go straight to the problem page, and investigate recent changes.</span></span>

## <a name="try-the-demo"></a><span data-ttu-id="5a187-131">Essayer la démonstration</span><span class="sxs-lookup"><span data-stu-id="5a187-131">Try the demo</span></span>

<span data-ttu-id="5a187-132">[Cliquez ici pour voir une démonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) sur un échantillon de données.</span><span class="sxs-lookup"><span data-stu-id="5a187-132">[Click here to see a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="5a187-133">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="5a187-133">How it works</span></span>

<span data-ttu-id="5a187-134">Smart Diagnostics utilise un algorithme Machine Learning non supervisé avancé basé sur l’opération [DiffPatterns](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5a187-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on the [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="5a187-135">Il recherche les modèles susceptibles d’expliquer la modification des données.</span><span class="sxs-lookup"><span data-stu-id="5a187-135">It looks for candidate patterns that might explain the data change.</span></span> <span data-ttu-id="5a187-136">Il analyse l’impact de chaque modèle sur la mesure et affiche le modèle qui correspond le mieux à la modification.</span><span class="sxs-lookup"><span data-stu-id="5a187-136">It analyses the impact of each candidate on the metric, and shows the pattern that best correlates with the change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="5a187-137">Aucun diagnostic n’est donné ?</span><span class="sxs-lookup"><span data-stu-id="5a187-137">No diagnostic points?</span></span>

<span data-ttu-id="5a187-138">Smart Diagnostics fonctionne uniquement lorsque les critères suivants sont réunis :</span><span class="sxs-lookup"><span data-stu-id="5a187-138">Smart Diagnostics only works when the following criteria are satisfied:</span></span>

 * <span data-ttu-id="5a187-139">Le paramètre Smart Diagnostics est activé.</span><span class="sxs-lookup"><span data-stu-id="5a187-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="5a187-140">Recherchez l’icône Paramètres dans Analytics.</span><span class="sxs-lookup"><span data-stu-id="5a187-140">Look under the Settings icon in Analytics.</span></span>
 * <span data-ttu-id="5a187-141">L’option Smart Diagnostics dans les paramètres d’Analytics est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5a187-141">The Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="5a187-142">Axe du temps : l’axe des abscisses du graphique doit être de type `datetime`.</span><span class="sxs-lookup"><span data-stu-id="5a187-142">Time axis: The X-axis of the chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="5a187-143">Graphique en courbes ou en aires : Diagnostics fonctionne uniquement avec ces types de graphique.</span><span class="sxs-lookup"><span data-stu-id="5a187-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="5a187-144">Utilisez `| render timechart` ou `| render areachart` à la fin de votre requête, ou sélectionnez Graphique en courbes ou en aires dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="5a187-144">Use `| render timechart` or `| render areachart` at the end of your query; or select Line or Area Chart from the drop-down selector.</span></span>
 * <span data-ttu-id="5a187-145">Discontinuité : la discontinuité des données doit être significative.</span><span class="sxs-lookup"><span data-stu-id="5a187-145">Discontinuity: There must be a significant discontinuity in the data.</span></span>
 * <span data-ttu-id="5a187-146">Suffisamment de points à analyser.</span><span class="sxs-lookup"><span data-stu-id="5a187-146">Sufficient points to analyze.</span></span>
 * <span data-ttu-id="5a187-147">Pas plus d’une clause de synthèse dans la requête.</span><span class="sxs-lookup"><span data-stu-id="5a187-147">No more than one summarize clause in the query.</span></span>
 * <span data-ttu-id="5a187-148">Aucune clause de projet qui contient une définition de nom avant la clause de synthèse.</span><span class="sxs-lookup"><span data-stu-id="5a187-148">No project clause that contains a name definition before the summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="5a187-149">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="5a187-149">Related articles</span></span>

 * [<span data-ttu-id="5a187-150">Didacticiel Analytics</span><span class="sxs-lookup"><span data-stu-id="5a187-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="5a187-151">[Détection intelligente](app-insights-proactive-diagnostics.md) vous avertit automatiquement en cas de problèmes de performances.</span><span class="sxs-lookup"><span data-stu-id="5a187-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you to performance issues.</span></span>