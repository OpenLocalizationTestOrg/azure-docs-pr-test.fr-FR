---
title: "aaaSmart détection dans Azure Application Insights | Documents Microsoft"
description: "Application Insights réalise une analyse télémétrique approfondie automatique de votre application et vous avertit des éventuels problèmes de performances."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="e7e1e-103">Détection intelligente dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="e7e1e-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="e7e1e-104">La détection intelligente vous informe automatiquement des éventuels problèmes de performances dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="e7e1e-105">Il effectue une analyse proactive de télémétrie hello que votre application envoie trop[Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7e1e-105">It performs proactive analysis of hello telemetry that your app sends too[Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="e7e1e-106">S’ils détectent une augmentation soudaine du taux d’échec, ou des modèles anormaux de performances client ou serveur, vous recevez une alerte.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="e7e1e-107">Cette fonctionnalité ne nécessite aucune configuration.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-107">This feature needs no configuration.</span></span> <span data-ttu-id="e7e1e-108">Elle fonctionne si votre application envoie suffisamment de données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="e7e1e-109">Vous pouvez accéder à des alertes de détection actives à la fois à partir de messages hello et à partir du Panneau de Smart détection hello.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-109">You can access Smart Detection alerts both from hello emails you receive, and from hello Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="e7e1e-110">Passer en revue vos détections intelligentes</span><span class="sxs-lookup"><span data-stu-id="e7e1e-110">Review your Smart Detections</span></span>
<span data-ttu-id="e7e1e-111">Vous pouvez découvrir des détections de deux manières :</span><span class="sxs-lookup"><span data-stu-id="e7e1e-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="e7e1e-112">**Vous recevez un message électronique** de la part d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="e7e1e-113">Voici un exemple typique :</span><span class="sxs-lookup"><span data-stu-id="e7e1e-113">Here's a typical example:</span></span>
  
    ![Alerte par courrier électronique](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="e7e1e-115">Cliquez sur hello grand bouton tooopen plus en détail dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-115">Click hello big button tooopen more detail in hello portal.</span></span>
* <span data-ttu-id="e7e1e-116">**vignette de détection actives Hello** sur une vue d’ensemble de votre application panneau affiche un nombre d’alertes récentes.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-116">**hello Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="e7e1e-117">Cliquez sur hello vignette toosee une liste des alertes récentes.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-117">Click hello tile toosee a list of recent alerts.</span></span>

![Afficher les détections récentes](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="e7e1e-119">Sélectionnez une alerte toosee ses détails.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-119">Select an alert toosee its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="e7e1e-120">Quels sont les problèmes détectés ?</span><span class="sxs-lookup"><span data-stu-id="e7e1e-120">What problems are detected?</span></span>
<span data-ttu-id="e7e1e-121">Il existe trois types de détection :</span><span class="sxs-lookup"><span data-stu-id="e7e1e-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="e7e1e-122">[Détection intelligente des anomalies de type échec](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="e7e1e-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="e7e1e-123">Nous utilisons apprentissage tooset les taux de hello attendu de demandes ayant échoué pour votre application, la mise en corrélation avec la charge et d’autres facteurs.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-123">We use machine learning tooset hello expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="e7e1e-124">Si le taux d’échec hello est en dehors de l’enveloppe attendu de hello, nous envoyer une alerte.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-124">If hello failure rate goes outside hello expected envelope, we send an alert.</span></span>
* <span data-ttu-id="e7e1e-125">[Détection intelligente des anomalies de performances](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="e7e1e-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="e7e1e-126">Pour obtenir des notifications si le temps de réponse d’une durée de l’opération ou la dépendance est ralentissent toohistorical comparés de ligne de base ou si nous d’identifier un modèle anormal dans le temps de réponse ou de temps de chargement de page.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-126">You get notifications if response time of an operation or dependency duration is slowing down compared toohistorical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="e7e1e-127">[Détection intelligente - Dépannage de problèmes de service cloud Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="e7e1e-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="e7e1e-128">Vous recevez des alertes si votre application est hébergée dans Azure Cloud Services et qu’une instance de rôle présente des échecs de démarrage, un recyclage fréquent ou des erreurs d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="e7e1e-129">(liens d’aide hello dans chaque notification vous prennent les articles pertinents toohello.)</span><span class="sxs-lookup"><span data-stu-id="e7e1e-129">(hello help links in each notification take you toohello relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="e7e1e-130">Vidéo</span><span class="sxs-lookup"><span data-stu-id="e7e1e-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="e7e1e-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e7e1e-131">Next steps</span></span>
<span data-ttu-id="e7e1e-132">Ces outils de diagnostic vous aident à inspecter les données de télémétrie hello à partir de votre application :</span><span class="sxs-lookup"><span data-stu-id="e7e1e-132">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="e7e1e-133">Metrics Explorer</span><span class="sxs-lookup"><span data-stu-id="e7e1e-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="e7e1e-134">Navigateur de recherche</span><span class="sxs-lookup"><span data-stu-id="e7e1e-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="e7e1e-135">Analytics : un puissant langage de requête</span><span class="sxs-lookup"><span data-stu-id="e7e1e-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="e7e1e-136">La détection intelligente est entièrement automatique.</span><span class="sxs-lookup"><span data-stu-id="e7e1e-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="e7e1e-137">Mais peut-être voudriez-vous tooset certaines alertes plus ?</span><span class="sxs-lookup"><span data-stu-id="e7e1e-137">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="e7e1e-138">Alertes de mesures configurées manuellement</span><span class="sxs-lookup"><span data-stu-id="e7e1e-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="e7e1e-139">Tests web de disponibilité</span><span class="sxs-lookup"><span data-stu-id="e7e1e-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

