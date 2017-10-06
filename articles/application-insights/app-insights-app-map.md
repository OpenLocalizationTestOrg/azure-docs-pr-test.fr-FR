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
# <a name="application-map-in-application-insights"></a><span data-ttu-id="f9fb0-103">Mise en correspondance d’applications dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="f9fb0-103">Application Map in Application Insights</span></span>
<span data-ttu-id="f9fb0-104">Dans [Azure Application Insights](app-insights-overview.md), mappage d’Application est une présentation visuelle des relations de dépendance hello de composants de votre application.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of hello dependency relationships of your application components.</span></span> <span data-ttu-id="f9fb0-105">Chaque composant affiche les indicateurs de performance clés telles que toohelp charge, les performances, les échecs et les alertes, vous découvrez un composant à l’origine d’un problème de performances ou l’échec.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-105">Each component shows KPIs such as load, performance, failures, and alerts, toohelp you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="f9fb0-106">Vous pouvez cliquer à partir de n’importe quel composant toomore détaillée des diagnostics, comme les événements d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-106">You can click through from any component toomore detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="f9fb0-107">Si votre application utilise des services Azure, vous pouvez également cliquer diagnostics tooAzure, telles que des recommandations de l’Assistant de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-107">If your app uses Azure services, you can also click through tooAzure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="f9fb0-108">Comme les autres graphiques, vous pouvez épingler un toohello de mappage d’application Azure du tableau de bord, où il est entièrement fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-108">Like other charts, you can pin an application map toohello Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-hello-application-map"></a><span data-ttu-id="f9fb0-109">Mappage d’application hello ouvert</span><span class="sxs-lookup"><span data-stu-id="f9fb0-109">Open hello application map</span></span>
<span data-ttu-id="f9fb0-110">Carte hello ouvert à partir du Panneau de vue d’ensemble de hello pour votre application :</span><span class="sxs-lookup"><span data-stu-id="f9fb0-110">Open hello map from hello overview blade for your application:</span></span>

![ouvrir la mise en correspondance d’applications](./media/app-insights-app-map/01.png)

![mise en correspondance d’applications](./media/app-insights-app-map/02.png)

<span data-ttu-id="f9fb0-113">carte de Hello montre :</span><span class="sxs-lookup"><span data-stu-id="f9fb0-113">hello map shows:</span></span>

* <span data-ttu-id="f9fb0-114">Tests de disponibilité</span><span class="sxs-lookup"><span data-stu-id="f9fb0-114">Availability tests</span></span>
* <span data-ttu-id="f9fb0-115">Composant côté client (surveillé par hello SDK JavaScript)</span><span class="sxs-lookup"><span data-stu-id="f9fb0-115">Client-side component (monitored with hello JavaScript SDK)</span></span>
* <span data-ttu-id="f9fb0-116">Composant côté serveur</span><span class="sxs-lookup"><span data-stu-id="f9fb0-116">Server-side component</span></span>
* <span data-ttu-id="f9fb0-117">Dépendances de composants de client et serveur hello</span><span class="sxs-lookup"><span data-stu-id="f9fb0-117">Dependencies of hello client and server components</span></span>

<span data-ttu-id="f9fb0-118">Vous pouvez développer et réduire les groupes de liens de dépendance :</span><span class="sxs-lookup"><span data-stu-id="f9fb0-118">You can expand and collapse dependency link groups:</span></span>

![réduire](./media/app-insights-app-map/03.png)

<span data-ttu-id="f9fb0-120">Si vous avez de nombreuses dépendances d’un type (SQL, HTTP, etc.), elles peuvent apparaître groupées.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![dépendances groupées](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="f9fb0-122">Détecter les problèmes</span><span class="sxs-lookup"><span data-stu-id="f9fb0-122">Spot problems</span></span>
<span data-ttu-id="f9fb0-123">Chaque nœud possède des indicateurs de performance appropriés, tels que les taux de défaillance, les performances et la charge hello pour ce composant.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-123">Each node has relevant performance indicators, such as hello load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="f9fb0-124">Les icônes d’avertissement mettent en évidence les problèmes éventuels.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="f9fb0-125">Un avertissement orange signifie qu’il existe des défaillances dans les requêtes, les vues de page ou les appels de dépendance.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="f9fb0-126">Un avertissement rouge signifie un taux de défaillance de plus de 5 %.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="f9fb0-127">Si vous souhaitez tooadjust ces seuils, ouvrez les Options.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-127">If you want tooadjust these thresholds, open Options.</span></span>

![icônes de défaillance](./media/app-insights-app-map/04.png)

<span data-ttu-id="f9fb0-129">En outre, des alertes actives s’affichent :</span><span class="sxs-lookup"><span data-stu-id="f9fb0-129">Active alerts also show up:</span></span> 

![alertes actives](./media/app-insights-app-map/05.png)

<span data-ttu-id="f9fb0-131">Si vous utilisez SQL Azure, une icône vous indique des recommandations éventuelles sur la façon dont vous pouvez améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Recommandation d’Azure](./media/app-insights-app-map/06.png)

<span data-ttu-id="f9fb0-133">Cliquez sur n’importe quel tooget icône plus de détails :</span><span class="sxs-lookup"><span data-stu-id="f9fb0-133">Click any icon tooget more details:</span></span>

![Recommandation d’Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="f9fb0-135">Clics pour le diagnostic</span><span class="sxs-lookup"><span data-stu-id="f9fb0-135">Diagnostic click through</span></span>
<span data-ttu-id="f9fb0-136">Chacun des nœuds hello sur la carte de hello offre ciblée de clics pour les diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-136">Each of hello nodes on hello map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="f9fb0-137">options de Hello varient en fonction de type hello du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-137">hello options vary depending on hello type of hello node.</span></span>

![options de serveur](./media/app-insights-app-map/09.png)

<span data-ttu-id="f9fb0-139">Pour les composants qui sont hébergées dans Azure, les options de hello incluent des liens directs toothem.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-139">For components that are hosted in Azure, hello options include direct links toothem.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="f9fb0-140">Filtres et période</span><span class="sxs-lookup"><span data-stu-id="f9fb0-140">Filters and time range</span></span>
<span data-ttu-id="f9fb0-141">Par défaut, mappage de hello récapitule toutes les données hello disponibles pour hello choisi la plage de temps.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-141">By default, hello map summarizes all hello data available for hello chosen time range.</span></span> <span data-ttu-id="f9fb0-142">Mais vous pouvez le filtrer les noms d’opération spécifique uniquement tooinclude ou les dépendances.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-142">But you can filter it tooinclude only specific operation names or dependencies.</span></span>

* <span data-ttu-id="f9fb0-143">Nom de l’opération : cela inclut les vues de pages et les types de demandes côté serveur.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="f9fb0-144">Avec cette option, hello carte affiche hello indicateur de performance clé sur le nœud du côté serveur/client hello pour les opérations de hello sélectionné uniquement.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-144">With this option, hello map shows hello KPI on hello server/client-side node for hello selected operations only.</span></span> <span data-ttu-id="f9fb0-145">Il montre les dépendances hello appelés dans le contexte de hello de ces opérations spécifiques.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-145">It shows hello dependencies called in hello context of those specific operations.</span></span>
* <span data-ttu-id="f9fb0-146">Nom de base de dépendance : Cela inclut les dépendances de navigateur hello AJAX et côté serveur.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-146">Dependency base name: This includes hello AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="f9fb0-147">Si vous déclarez la télémétrie des dépendances personnalisées avec hello TrackDependency API, elles apparaissent également ici.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-147">If you report custom dependency telemetry with hello TrackDependency API, they also appear here.</span></span> <span data-ttu-id="f9fb0-148">Vous pouvez sélectionner tooshow de dépendances hello sur la carte de hello.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-148">You can select hello dependencies tooshow on hello map.</span></span> <span data-ttu-id="f9fb0-149">Actuellement cette sélection ne filtre pas les demandes côté serveur hello ou des vues de page côté client hello.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-149">Currently this selection does not filter hello server-side requests, or hello client-side page views.</span></span>

![Définir les filtres](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="f9fb0-151">Enregistrer les filtres</span><span class="sxs-lookup"><span data-stu-id="f9fb0-151">Save filters</span></span>
<span data-ttu-id="f9fb0-152">vous avez appliqué des filtres hello toosave, hello du code confidentiel filtré la vue sur un [tableau de bord](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="f9fb0-152">toosave hello filters you have applied, pin hello filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Code confidentiel toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="f9fb0-154">Volet d’erreur</span><span class="sxs-lookup"><span data-stu-id="f9fb0-154">Error pane</span></span>
<span data-ttu-id="f9fb0-155">Lorsque vous cliquez sur un nœud dans le mappage de hello, un volet d’erreur s’affiche sur la droite hello résumer les échecs pour ce nœud.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-155">When you click a node in hello map, an error pane is displayed on hello right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="f9fb0-156">Les échecs sont tout d’abord regroupés par ID d’opération, puis par ID de problème.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Volet d’erreur](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="f9fb0-158">En cliquant sur un échec vous prend toohello occurrence la plus récente de l’échec.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-158">Clicking on a failure takes you toohello most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="f9fb0-159">Intégrité des ressources</span><span class="sxs-lookup"><span data-stu-id="f9fb0-159">Resource health</span></span>
<span data-ttu-id="f9fb0-160">Pour certains types de ressources, l’intégrité des ressources est affichée en haut de hello du volet d’erreur hello.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-160">For some resource types, resource health is displayed at hello top of hello error pane.</span></span> <span data-ttu-id="f9fb0-161">Par exemple, en cliquant sur un nœud de SQL affiche les alertes qui ont déclenché et contrôle d’intégrité de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-161">For example, clicking a SQL node will show hello database health and any alerts that have fired.</span></span>

![Intégrité des ressources](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="f9fb0-163">Vous pouvez cliquer sur des métriques hello ressources nom tooview vue d’ensemble standard de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-163">You can click hello resource name tooview standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="f9fb0-164">Cartes d’applications système de bout en bout</span><span class="sxs-lookup"><span data-stu-id="f9fb0-164">End-to-end system app maps</span></span>

<span data-ttu-id="f9fb0-165">*Requiert le Kit de développement logiciel (SDK) version 2.3 ou ultérieure*</span><span class="sxs-lookup"><span data-stu-id="f9fb0-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="f9fb0-166">Si votre application comporte plusieurs composants - par exemple, un service principal en outre l’application web toohello -, puis vous pouvez afficher les tous sur le mappage d’une application intégrée.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-166">If your application has several components - for example, a back-end service in addition toohello web app - then you can show them all on one integrated app map.</span></span>

![Définir les filtres](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="f9fb0-168">mappage d’application Hello recherche des nœuds de serveur en suivant les appels de dépendance HTTP entre les serveurs avec hello Qu'application Insights SDK installé.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-168">hello app map finds server nodes by following any HTTP dependency calls made between servers with hello Application Insights SDK installed.</span></span> <span data-ttu-id="f9fb0-169">Chaque ressource Application Insights est supposé toocontain un seul serveur.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-169">Each Application Insights resource is assumed toocontain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="f9fb0-170">Mise en correspondance d’applications contenant plusieurs rôles (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="f9fb0-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="f9fb0-171">fonctionnalité de mappage plusieurs rôles application Hello préliminaire vous permet de toouse hello application mappés avec plusieurs serveurs d’envoi de données toohello même ressource Application Insights / clé d’instrumentation.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-171">hello preview multi-role app map feature allows you toouse hello app map with multiple servers sending data toohello same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="f9fb0-172">Serveurs de mappage de hello sont segmentées par la propriété cloud_RoleName de hello sur les éléments de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-172">Servers in hello map are segmented by hello cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="f9fb0-173">Définissez *mappage plusieurs rôles d’Application* trop*sur* de hello aperçus panneau tooenable cette configuration.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-173">Set *Multi-role Application Map* too*On* from hello Previews blade tooenable this configuration.</span></span>

<span data-ttu-id="f9fb0-174">Cette approche peut s’avérer utile dans une application de services de micro ou dans d’autres scénarios où vous souhaitez que les événements de toocorrelate sur plusieurs serveurs au sein d’une seule ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-174">This approach may be desired in a micro-services application, or in other scenarios where you want toocorrelate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="f9fb0-175">Vidéo</span><span class="sxs-lookup"><span data-stu-id="f9fb0-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="f9fb0-176">Commentaires</span><span class="sxs-lookup"><span data-stu-id="f9fb0-176">Feedback</span></span>
<span data-ttu-id="f9fb0-177">Veuillez fournir vos commentaires via l’option de commentaires portail hello.</span><span class="sxs-lookup"><span data-stu-id="f9fb0-177">Please provide feedback through hello portal feedback option.</span></span>

![Image MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="f9fb0-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9fb0-179">Next steps</span></span>

* [<span data-ttu-id="f9fb0-180">portail Azure</span><span class="sxs-lookup"><span data-stu-id="f9fb0-180">Azure portal</span></span>](https://portal.azure.com)
