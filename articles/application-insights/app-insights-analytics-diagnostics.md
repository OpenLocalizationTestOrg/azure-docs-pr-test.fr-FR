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
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="e3dae-103">Diagnostiquer les changements soudains dans la télémétrie de votre application</span><span class="sxs-lookup"><span data-stu-id="e3dae-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="e3dae-104">*Cette fonctionnalité est en version préliminaire.*</span><span class="sxs-lookup"><span data-stu-id="e3dae-104">*This feature is in preview.*</span></span>

<span data-ttu-id="e3dae-105">Diagnostiquez des changements soudains dans les performances ou l’utilisation de votre application web d’un seul clic !</span><span class="sxs-lookup"><span data-stu-id="e3dae-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="e3dae-106">fonctionnalité des Diagnostics actives Hello est disponible chaque fois que vous créez un graphique de temps dans [Analytique](app-insights-analytics.md) dans [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e3dae-106">hello Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="e3dae-107">Partout où il existe une modification inhabituelle de tendance hello de vos résultats, par exemple un pic d’activité ou une adresse dip, Diagnostics actives identifie un modèle des dimensions et des valeurs connexes susceptibles d’expliquer les modifications hello.</span><span class="sxs-lookup"><span data-stu-id="e3dae-107">Wherever there is an unusual change from hello trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain hello change.</span></span> <span data-ttu-id="e3dae-108">Cela vous permet de diagnostiquer le problème de hello rapidement.</span><span class="sxs-lookup"><span data-stu-id="e3dae-108">This helps you diagnose hello problem quickly.</span></span> 

<span data-ttu-id="e3dae-109">Dans cet exemple, Smart Diagnostics a identifié un modèle de valeurs de propriété associé hello modification et met en évidence la différence de hello entre les résultats avec et sans ce modèle :</span><span class="sxs-lookup"><span data-stu-id="e3dae-109">In this example, Smart Diagnostics has identified a pattern of property values associated with hello change, and highlights hello difference between results with and without that pattern:</span></span>

![exemple de résultat de diagnostic analytique](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="e3dae-111">Diagnostiquer les modifications de données</span><span class="sxs-lookup"><span data-stu-id="e3dae-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="e3dae-112">Exécutez une requête dans Analytics et affichez-la sous la forme d’un graphique de temps.</span><span class="sxs-lookup"><span data-stu-id="e3dae-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="e3dae-113">Cliquez sur l’un des points représentant un pic d’activité, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="e3dae-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![point représentant un pic d’activité](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="e3dae-115">Diagnostics prend quelques secondes toodiscover un modèle.</span><span class="sxs-lookup"><span data-stu-id="e3dae-115">Diagnostics takes a few seconds toodiscover a pattern.</span></span>

3. <span data-ttu-id="e3dae-116">onglet des résultats de Diagnostics Hello affiche alors un modèle qui peut expliquer discontinuité de vos données.</span><span class="sxs-lookup"><span data-stu-id="e3dae-116">hello Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="e3dae-118">texte Hello montre les valeurs de dimension hello apparaissant toocorrelate avec la touche MAJ enfoncée hello.</span><span class="sxs-lookup"><span data-stu-id="e3dae-118">hello text shows hello dimension values that appear toocorrelate with hello shift.</span></span> <span data-ttu-id="e3dae-119">Dans cet exemple, il est associé à une requête et à une version de navigateur spécifiques.</span><span class="sxs-lookup"><span data-stu-id="e3dae-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="e3dae-120">Notez également les composants hello deux de hello graphique, avec hello filtre true et false.</span><span class="sxs-lookup"><span data-stu-id="e3dae-120">Notice also hello two components of hello chart, with hello filter true and false.</span></span> <span data-ttu-id="e3dae-121">composant de false Hello indique une tendance inchangée.</span><span class="sxs-lookup"><span data-stu-id="e3dae-121">hello false component shows an unchanged trend.</span></span> <span data-ttu-id="e3dae-122">En d’autres termes, il n’existe aucune modification dans les résultats de télémétrie hello, si nous excluez la combinaison de problématique hello de dimensions Diagnostics a identifié.</span><span class="sxs-lookup"><span data-stu-id="e3dae-122">In other words, there is no change in hello telemetry results, if we exclude hello problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="e3dae-123">En revanche, les résultats de hello dans cette combinaison s’affichent une modification importante au sein de la zone hello mis en surbrillance d’enquête.</span><span class="sxs-lookup"><span data-stu-id="e3dae-123">By contrast, hello results within that combination do show a dramatic change within hello highlighted area of investigation.</span></span> <span data-ttu-id="e3dae-124">Cela indique que les Diagnostics a trouvé une combinaison des propriétés qui explique la modification de hello.</span><span class="sxs-lookup"><span data-stu-id="e3dae-124">This shows that Diagnostics has found a combination of properties that explains hello change.</span></span>

4.  <span data-ttu-id="e3dae-125">Si le modèle de hello est complexe, vous devez toohover sur **afficher tout** dimensions de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="e3dae-125">If hello pattern is complex, you need toohover over **Show all** toosee hello dimensions.</span></span>

    ![afficher tout](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="e3dae-127">En cas de Diagnostics ne recherche aucun toonotify modèle significatif sur hello que page de « aucun résultat » s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e3dae-127">In case Diagnostics finds no significant pattern toonotify about, hello ‘no results’ page will be presented.</span></span> <span data-ttu-id="e3dae-128">À ce stade, vous pouvez modifier votre requête.</span><span class="sxs-lookup"><span data-stu-id="e3dae-128">At this point, you may change your query.</span></span> <span data-ttu-id="e3dae-129">Par exemple, vous pouvez affiner la plage de temps hello et placement dans la requête Analytique, pour une analyse plus approfondie et potentiellement de meilleurs résultats.</span><span class="sxs-lookup"><span data-stu-id="e3dae-129">For example, you could narrow hello time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="e3dae-130">Grâce à la base de connaissances hello qu’une page spécifique de votre site Web a un problème sur un navigateur particulier, vous pouvez désormais accéder à droite toohello problème page et examiner les modifications récentes.</span><span class="sxs-lookup"><span data-stu-id="e3dae-130">Armed with hello knowledge that a particular page of your website has a problem on a particular browser, you can now go straight toohello problem page, and investigate recent changes.</span></span>

## <a name="try-hello-demo"></a><span data-ttu-id="e3dae-131">Essayez hello démonstration</span><span class="sxs-lookup"><span data-stu-id="e3dae-131">Try hello demo</span></span>

<span data-ttu-id="e3dae-132">[Cliquez ici une démonstration de toosee](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) sur les exemples de données.</span><span class="sxs-lookup"><span data-stu-id="e3dae-132">[Click here toosee a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="e3dae-133">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="e3dae-133">How it works</span></span>

<span data-ttu-id="e3dae-134">Diagnostics intelligente utilise un algorithme d’apprentissage non supervisé avancées en fonction de hello [DiffPatterns](app-insights-analytics-reference.md) opération.</span><span class="sxs-lookup"><span data-stu-id="e3dae-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on hello [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="e3dae-135">Il recherche des modèles candidats susceptibles d’expliquer hello modification des données.</span><span class="sxs-lookup"><span data-stu-id="e3dae-135">It looks for candidate patterns that might explain hello data change.</span></span> <span data-ttu-id="e3dae-136">Il analyse l’impact hello de chaque candidat sur métrique de hello et montre le modèle de hello que mieux met en corrélation avec la modification de hello.</span><span class="sxs-lookup"><span data-stu-id="e3dae-136">It analyses hello impact of each candidate on hello metric, and shows hello pattern that best correlates with hello change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="e3dae-137">Aucun diagnostic n’est donné ?</span><span class="sxs-lookup"><span data-stu-id="e3dae-137">No diagnostic points?</span></span>

<span data-ttu-id="e3dae-138">Diagnostics actives ne fonctionne que lorsque hello suivant des critères est satisfait :</span><span class="sxs-lookup"><span data-stu-id="e3dae-138">Smart Diagnostics only works when hello following criteria are satisfied:</span></span>

 * <span data-ttu-id="e3dae-139">Le paramètre Smart Diagnostics est activé.</span><span class="sxs-lookup"><span data-stu-id="e3dae-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="e3dae-140">Regardez sous l’icône Paramètres hello Analytique.</span><span class="sxs-lookup"><span data-stu-id="e3dae-140">Look under hello Settings icon in Analytics.</span></span>
 * <span data-ttu-id="e3dae-141">Hello option Diagnostics actives dans les paramètres de l’Analytique est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e3dae-141">hello Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="e3dae-142">Axe du temps : hello axe des abscisses du graphique de hello doit être de type `datetime`.</span><span class="sxs-lookup"><span data-stu-id="e3dae-142">Time axis: hello X-axis of hello chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="e3dae-143">Graphique en courbes ou en aires : Diagnostics fonctionne uniquement avec ces types de graphique.</span><span class="sxs-lookup"><span data-stu-id="e3dae-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="e3dae-144">Utilisez `| render timechart` ou `| render areachart` à fin hello de votre requête ; ou sélectionnez la ligne ou la zone de graphique à partir du sélecteur de liste déroulante hello.</span><span class="sxs-lookup"><span data-stu-id="e3dae-144">Use `| render timechart` or `| render areachart` at hello end of your query; or select Line or Area Chart from hello drop-down selector.</span></span>
 * <span data-ttu-id="e3dae-145">Discontinuité : Il doit exister une discontinuité significative dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="e3dae-145">Discontinuity: There must be a significant discontinuity in hello data.</span></span>
 * <span data-ttu-id="e3dae-146">Suffisamment tooanalyze de points.</span><span class="sxs-lookup"><span data-stu-id="e3dae-146">Sufficient points tooanalyze.</span></span>
 * <span data-ttu-id="e3dae-147">Ne plusieurs résument la clause de la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="e3dae-147">No more than one summarize clause in hello query.</span></span>
 * <span data-ttu-id="e3dae-148">Aucune clause de projet qui contient une définition de nom avant hello ne résument la clause.</span><span class="sxs-lookup"><span data-stu-id="e3dae-148">No project clause that contains a name definition before hello summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="e3dae-149">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="e3dae-149">Related articles</span></span>

 * [<span data-ttu-id="e3dae-150">Didacticiel Analytics</span><span class="sxs-lookup"><span data-stu-id="e3dae-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="e3dae-151">[Active la détection](app-insights-proactive-diagnostics.md) vous avertit automatiquement les problèmes de tooperformance.</span><span class="sxs-lookup"><span data-stu-id="e3dae-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you tooperformance issues.</span></span>
