---
title: "analyse d’aaaUsage pour les applications web avec Azure Application Insights | Documents Microsoft"
description: "Comprenez vos utilisateurs et ce qu’ils font avec votre application web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="dabed-103">Analyse de l’utilisation des applications web avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="dabed-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="dabed-104">Quelles sont les fonctionnalités de votre application web les plus populaires ?</span><span class="sxs-lookup"><span data-stu-id="dabed-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="dabed-105">Vos utilisateurs atteignent-ils leurs objectifs avec votre application ?</span><span class="sxs-lookup"><span data-stu-id="dabed-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="dabed-106">Disparaissent-ils à des stades spécifiques, et reviennent-ils plus tard ?</span><span class="sxs-lookup"><span data-stu-id="dabed-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="dabed-107">[Azure Application Insights](app-insights-overview.md) vous permet d’obtenir un aperçu utile sur l’utilisation de votre application web.</span><span class="sxs-lookup"><span data-stu-id="dabed-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="dabed-108">Chaque fois que vous mettez à jour votre application, vous pouvez évaluer son bon fonctionnement pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dabed-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="dabed-109">Grâce à ces informations, vous pouvez prendre des décisions basées sur des données sur les cycles de développement suivants.</span><span class="sxs-lookup"><span data-stu-id="dabed-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="dabed-110">Envoyer des données de télémétrie à partir de votre application</span><span class="sxs-lookup"><span data-stu-id="dabed-110">Send telemetry from your app</span></span>

<span data-ttu-id="dabed-111">meilleure expérience de Hello est obtenu en installant l’Application Insights à la fois dans le code de votre serveur d’application et vos pages web.</span><span class="sxs-lookup"><span data-stu-id="dabed-111">hello best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="dabed-112">Hello composants client et serveur de votre application d’envoi toohello arrière de télémétrie portail Azure pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="dabed-112">hello client and server components of your app send telemetry back toohello Azure portal for analysis.</span></span>

1. <span data-ttu-id="dabed-113">**Code de serveur :** module approprié hello d’installation pour votre [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), ou [autres](app-insights-platforms.md) application.</span><span class="sxs-lookup"><span data-stu-id="dabed-113">**Server code:** Install hello appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="dabed-114">*Code de serveur tooinstall ne voulez pas ? Vous pouvez simplement [créer une ressource Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="dabed-114">*Don't want tooinstall server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="dabed-115">**Code de page Web :** hello ouvrir [portail Azure](https://portal.azure.com), ouvrez la ressource d’Application Insights hello pour votre application, puis ouvrez **prise en main > analyse et diagnostiquer côté Client**.</span><span class="sxs-lookup"><span data-stu-id="dabed-115">**Web page code:** Open hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Copiez les script hello head hello de votre page web master.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="dabed-117">**Obtenez la télémétrie :** exécuter votre projet en mode débogage pendant quelques minutes, puis examinez les résultats dans le panneau de vue d’ensemble de hello dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="dabed-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in hello Overview blade in Application Insights.</span></span>

    <span data-ttu-id="dabed-118">Publier votre application toomonitor les performances de votre application et de savoir ce que font vos utilisateurs avec votre application.</span><span class="sxs-lookup"><span data-stu-id="dabed-118">Publish your app toomonitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="dabed-119">Inclure l’ID d’utilisateur et l’ID de session dans votre télémétrie</span><span class="sxs-lookup"><span data-stu-id="dabed-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="dabed-120">utilisateurs tootrack au fil du temps, Application Insights requiert un tooidentify de façon les.</span><span class="sxs-lookup"><span data-stu-id="dabed-120">tootrack users over time, Application Insights requires a way tooidentify them.</span></span> <span data-ttu-id="dabed-121">Événements de Hello est de l’outil hello seul outil d’utilisation qui ne nécessite pas un ID d’utilisateur ou un ID de session.</span><span class="sxs-lookup"><span data-stu-id="dabed-121">hello Events tool is hello only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="dabed-122">Commencez à envoyer ces ID [ici](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="dabed-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="dabed-123">Explorer des données démographiques et des statistiques de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="dabed-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="dabed-124">Découvrez quand des personnes utilisent votre application, les pages qui les intéressent le plus, où vos utilisateurs se trouvent, les navigateurs et les systèmes d’exploitation qu’ils utilisent.</span><span class="sxs-lookup"><span data-stu-id="dabed-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="dabed-125">rapports d’utilisateurs et des Sessions Hello filtrer vos données par les pages ou des événements personnalisés et les segment par propriétés, telles que l’emplacement, l’environnement et page.</span><span class="sxs-lookup"><span data-stu-id="dabed-125">hello Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="dabed-126">Vous pouvez également ajouter vos propres filtres.</span><span class="sxs-lookup"><span data-stu-id="dabed-126">You can also add your own filters.</span></span>

![Utilisateurs](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="dabed-128">Des informations sur la droite de hello souligner des motifs intéressants dans le jeu de hello de données.</span><span class="sxs-lookup"><span data-stu-id="dabed-128">Insights on hello right point out interesting patterns in hello set of data.</span></span>  

* <span data-ttu-id="dabed-129">Hello **utilisateurs** rapport nombres hello d’utilisateurs uniques qui accèdent à vos pages au sein de vos périodes de temps choisie.</span><span class="sxs-lookup"><span data-stu-id="dabed-129">hello **Users** report counts hello numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="dabed-130">(Les utilisateurs sont comptés avec les cookies.</span><span class="sxs-lookup"><span data-stu-id="dabed-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="dabed-131">Si un utilisateur accède à votre site avec différents navigateurs ou ordinateurs clients, ou efface ses cookies, il sera compté plusieurs fois.)</span><span class="sxs-lookup"><span data-stu-id="dabed-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="dabed-132">Hello **Sessions** rapport nombre hello de sessions utilisateur qui accèdent à votre site.</span><span class="sxs-lookup"><span data-stu-id="dabed-132">hello **Sessions** report counts hello number of user sessions that access your site.</span></span> <span data-ttu-id="dabed-133">Une session est une période d’activité d’un utilisateur, qui se termine par une période d’inactivité de plus d’une demi-heure.</span><span class="sxs-lookup"><span data-stu-id="dabed-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="dabed-134">En savoir plus sur les outils d’utilisateurs, les Sessions et les événements hello</span><span class="sxs-lookup"><span data-stu-id="dabed-134">More about hello Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="dabed-135">Affichages de page</span><span class="sxs-lookup"><span data-stu-id="dabed-135">Page views</span></span>

<span data-ttu-id="dabed-136">À partir du Panneau de l’utilisation de hello, parcourez tooget de vignette de vues de Page hello une répartition de vos pages les plus populaires :</span><span class="sxs-lookup"><span data-stu-id="dabed-136">From hello Usage blade, click through hello Page Views tile tooget a breakdown of your most popular pages:</span></span>

![À partir du Panneau de vue d’ensemble de hello, cliquez sur hello graphique de vues de Page](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="dabed-138">exemple Hello ci-dessus est d’un site web de jeux.</span><span class="sxs-lookup"><span data-stu-id="dabed-138">hello example above is from a games web site.</span></span> <span data-ttu-id="dabed-139">À partir de graphiques de hello, nous pouvons voir instantanément :</span><span class="sxs-lookup"><span data-stu-id="dabed-139">From hello charts, we can instantly see:</span></span>

* <span data-ttu-id="dabed-140">L’utilisation n’a pas encore améliorées dans hello semaine dernière.</span><span class="sxs-lookup"><span data-stu-id="dabed-140">Usage hasn't improved in hello past week.</span></span> <span data-ttu-id="dabed-141">Peut-être que nous devrions envisager une optimisation pour les moteurs de recherche ?</span><span class="sxs-lookup"><span data-stu-id="dabed-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="dabed-142">Raquettes est la page de jeu les plus populaires hello.</span><span class="sxs-lookup"><span data-stu-id="dabed-142">Tennis is hello most popular game page.</span></span> <span data-ttu-id="dabed-143">Concentrons-nous sur la page de toothis d’améliorations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="dabed-143">Let's focus on further improvements toothis page.</span></span>
* <span data-ttu-id="dabed-144">En moyenne, les utilisateurs, visitez hello Tennis page environ trois fois par semaine.</span><span class="sxs-lookup"><span data-stu-id="dabed-144">On average, users visit hello Tennis page about three times per week.</span></span> <span data-ttu-id="dabed-145">(Il y a près de trois fois plus de sessions que d’utilisateurs.)</span><span class="sxs-lookup"><span data-stu-id="dabed-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="dabed-146">La plupart des utilisateurs le site hello au cours de la semaine de travail hello des États-Unis et les heures de travail.</span><span class="sxs-lookup"><span data-stu-id="dabed-146">Most users visit hello site during hello U.S. working week, and in working hours.</span></span> <span data-ttu-id="dabed-147">Par exemple, nous devons fournir un bouton « Masquer rapide » sur la page web de hello.</span><span class="sxs-lookup"><span data-stu-id="dabed-147">Perhaps we should provide a "quick hide" button on hello web page.</span></span>
* <span data-ttu-id="dabed-148">Hello [annotations](app-insights-annotations.md) sur le graphique de hello s’affichent lorsque les nouvelles versions du site Web de hello ont été déployées.</span><span class="sxs-lookup"><span data-stu-id="dabed-148">hello [annotations](app-insights-annotations.md) on hello chart show when new versions of hello website were deployed.</span></span> <span data-ttu-id="dabed-149">Aucun des déploiements récents de hello a un effet notable sur l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="dabed-149">None of hello recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="dabed-150">Que se passe-t-il si vous souhaitez des sites à tooyour tooinvestigate hello trafic plus en détail, telles que le fractionnement d’une propriété personnalisée, que votre site expédie dans son télémétrie des consultations de page ?</span><span class="sxs-lookup"><span data-stu-id="dabed-150">What if you want tooinvestigate hello traffic tooyour site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="dabed-151">Ouvrez hello **événements** outil dans le menu de ressource Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="dabed-151">Open hello **Events** tool in hello Application Insights resource menu.</span></span> <span data-ttu-id="dabed-152">Cet outil vous permet d’analyser combien de pages consultées et d’événements personnalisés ont été envoyés à partir de votre application, sur la base des différentes options de filtrage, cohorte et segmentation.</span><span class="sxs-lookup"><span data-stu-id="dabed-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="dabed-153">Bonjour « Qui a utilisé » la liste déroulante, sélectionnez « N’importe quelle Page de vue ».</span><span class="sxs-lookup"><span data-stu-id="dabed-153">In hello "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="dabed-154">Dans la liste déroulante de « Fractionnement par » hello, sélectionnez une propriété qui toosplit votre page Afficher télémétrie.</span><span class="sxs-lookup"><span data-stu-id="dabed-154">In hello "Split by" dropdown, select a property by which toosplit your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="dabed-155">Rétention - Combien d’utilisateurs reviennent ?</span><span class="sxs-lookup"><span data-stu-id="dabed-155">Retention - how many users come back?</span></span>

<span data-ttu-id="dabed-156">Rétention vous permet de comprendre la fréquence à laquelle vos utilisateurs retournent toouse leur application basée sur les cohortes d’utilisateurs qui a exécuté une action entreprise pendant un certain intervalle de planification.</span><span class="sxs-lookup"><span data-stu-id="dabed-156">Retention helps you understand how often your users return toouse their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="dabed-157">Comprendre les fonctionnalités spécifiques entraînent l’arrière toocome plus que d’autres utilisateurs</span><span class="sxs-lookup"><span data-stu-id="dabed-157">Understand what specific features cause users toocome back more than others</span></span> 
- <span data-ttu-id="dabed-158">Formuler des hypothèses en fonction des données utilisateur réel</span><span class="sxs-lookup"><span data-stu-id="dabed-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="dabed-159">Déterminer si la rétention est un problème dans votre produit</span><span class="sxs-lookup"><span data-stu-id="dabed-159">Determine whether retention is a problem in your product</span></span> 

![Rétention](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="dabed-161">contrôles de rétention de Hello haut permettent de vous toodefine des événements spécifiques et rétention de toocalculate de plage de temps.</span><span class="sxs-lookup"><span data-stu-id="dabed-161">hello retention controls on top allow you toodefine specific events and time range toocalculate retention.</span></span> <span data-ttu-id="dabed-162">graphique de milieu de hello Hello donne une représentation visuelle de hello du pourcentage de rétention globale par hello plage de temps spécifié.</span><span class="sxs-lookup"><span data-stu-id="dabed-162">hello graph in hello middle gives a visual representation of hello overall retention percentage by hello time range specified.</span></span> <span data-ttu-id="dabed-163">graphique de Hello sous hello représente rétention individuel dans une période donnée.</span><span class="sxs-lookup"><span data-stu-id="dabed-163">hello graph on hello bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="dabed-164">Ce niveau de détail vous permet de toounderstand votre quels utilisateurs et ce qui peut affecter les utilisateurs le retour à une granularité plus détaillée.</span><span class="sxs-lookup"><span data-stu-id="dabed-164">This level of detail allows you toounderstand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="dabed-165">Plus d’informations sur l’outil de conservation hello</span><span class="sxs-lookup"><span data-stu-id="dabed-165">More about hello Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="dabed-166">Événements personnalisés</span><span class="sxs-lookup"><span data-stu-id="dabed-166">Custom business events</span></span>

<span data-ttu-id="dabed-167">tooget conscience de ce que les utilisateurs à votre application web, il s’agit des lignes tooinsert utile des événements personnalisés toolog de code.</span><span class="sxs-lookup"><span data-stu-id="dabed-167">tooget a clear understanding of what users do with your web app, it's useful tooinsert lines of code toolog custom events.</span></span> <span data-ttu-id="dabed-168">Ces événements peuvent suivre quoi que ce soit à partir d’actions utilisateur détaillé en cliquant sur les boutons, événements d’importants de l’activité de toomore tels que d’un achat ou gagnante d’un jeu.</span><span class="sxs-lookup"><span data-stu-id="dabed-168">These events can track anything from detailed user actions such as clicking specific buttons, toomore significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="dabed-169">Bien que les pages consultées puissent représenter des événements utiles, cela n’est en général pas le cas.</span><span class="sxs-lookup"><span data-stu-id="dabed-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="dabed-170">Un utilisateur peut ouvrir une page de produit sans acheter le produit de hello.</span><span class="sxs-lookup"><span data-stu-id="dabed-170">A user can open a product page without buying hello product.</span></span> 

<span data-ttu-id="dabed-171">Grâce aux événements spécifiques, vous pouvez représenter la progression de vos utilisateurs sur votre site.</span><span class="sxs-lookup"><span data-stu-id="dabed-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="dabed-172">Vous pouvez connaître leurs préférences sur les différentes options et où ils abandonnent ou rencontrent des difficultés.</span><span class="sxs-lookup"><span data-stu-id="dabed-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="dabed-173">Avec cette base de connaissances, vous prendre des décisions sur les priorités de hello dans votre backlog de développement.</span><span class="sxs-lookup"><span data-stu-id="dabed-173">With this knowledge, you can make informed decisions about hello priorities in your development backlog.</span></span>

<span data-ttu-id="dabed-174">Événements peuvent être enregistrés dans la page web de hello :</span><span class="sxs-lookup"><span data-stu-id="dabed-174">Events can be logged in hello web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="dabed-175">Ou côté serveur hello hello web app :</span><span class="sxs-lookup"><span data-stu-id="dabed-175">Or in hello server side of hello web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="dabed-176">Vous pouvez joindre des événements de toothese de valeurs de propriété, afin que vous pouvez filtrer ou fractionner des événements hello lorsque vous examinez les dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="dabed-176">You can attach property values toothese events, so that you can filter or split hello events when you inspect them in hello portal.</span></span> <span data-ttu-id="dabed-177">En outre, un ensemble standard de propriétés est attaché tooeach événement, telles que des ID d’utilisateur anonyme, ce qui vous permet de séquence de hello tootrace des activités d’un utilisateur individuel.</span><span class="sxs-lookup"><span data-stu-id="dabed-177">In addition, a standard set of properties is attached tooeach event, such as anonymous user ID, which allows you tootrace hello sequence of activities of an individual user.</span></span>

<span data-ttu-id="dabed-178">En savoir plus sur les [événements personnalisés](app-insights-api-custom-events-metrics.md#trackevent) et les [propriétés](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="dabed-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="dabed-179">Segmenter et traiter les événements</span><span class="sxs-lookup"><span data-stu-id="dabed-179">Slice and dice events</span></span>

<span data-ttu-id="dabed-180">Dans les outils d’utilisateurs, les Sessions et les événements de hello, vous pouvez découper et manipulent des événements personnalisés par utilisateur, nom de l’événement et propriétés.</span><span class="sxs-lookup"><span data-stu-id="dabed-180">In hello Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="dabed-181">![Utilisateurs](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="dabed-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-hello-telemetry-with-hello-app"></a><span data-ttu-id="dabed-182">Télémétrie hello de conception avec l’application hello</span><span class="sxs-lookup"><span data-stu-id="dabed-182">Design hello telemetry with hello app</span></span>

<span data-ttu-id="dabed-183">Lorsque vous concevez chaque fonctionnalité de votre application, pensez comment vous allez toomeasure son succès avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dabed-183">When you are designing each feature of your app, consider how you are going toomeasure its success with your users.</span></span> <span data-ttu-id="dabed-184">Décider ce que vous devez toorecord et le code hello de suivi des appels pour les événements dans votre application à partir de hello des événements commerciaux Démarrer.</span><span class="sxs-lookup"><span data-stu-id="dabed-184">Decide what business events you need toorecord, and code hello tracking calls for those events into your app from hello start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="dabed-185">Test A | B</span><span class="sxs-lookup"><span data-stu-id="dabed-185">A | B Testing</span></span>
<span data-ttu-id="dabed-186">Si vous ne connaissez pas variante d’une fonctionnalité sera plus efficace, relâchez les deux, rendre chaque toodifferent accessible.</span><span class="sxs-lookup"><span data-stu-id="dabed-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible toodifferent users.</span></span> <span data-ttu-id="dabed-187">Mesurer la réussite de hello de chacun, puis déplacez les version unifiée tooa.</span><span class="sxs-lookup"><span data-stu-id="dabed-187">Measure hello success of each, and then move tooa unified version.</span></span>

<span data-ttu-id="dabed-188">Cette technique, vous attacher propriété distinctes valeurs tooall hello données de télémétrie envoyé par chaque version de votre application.</span><span class="sxs-lookup"><span data-stu-id="dabed-188">For this technique, you attach distinct property values tooall hello telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="dabed-189">C’est également en définissant des propriétés Bonjour TelemetryContext active.</span><span class="sxs-lookup"><span data-stu-id="dabed-189">You can do that by defining properties in hello active TelemetryContext.</span></span> <span data-ttu-id="dabed-190">Ces propriétés par défaut sont ajoutées au message de télémétrie tooevery hello application envoie - non seulement vos messages personnalisés, mais également les télémétrie standard hello.</span><span class="sxs-lookup"><span data-stu-id="dabed-190">These default properties are added tooevery telemetry message that hello application sends - not just your custom messages, but hello standard telemetry as well.</span></span>

<span data-ttu-id="dabed-191">Dans le portail Application Insights hello, filtrer et diviser vos données sur des valeurs de propriété hello, ainsi que les différentes versions de toocompare hello.</span><span class="sxs-lookup"><span data-stu-id="dabed-191">In hello Application Insights portal, filter and split your data on hello property values, so as toocompare hello different versions.</span></span>

<span data-ttu-id="dabed-192">toodo, [configurer un initialiseur de télémétrie](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="dabed-192">toodo this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="dabed-193">Dans l’initialiseur d’application hello web tels que Global.asax.cs :</span><span class="sxs-lookup"><span data-stu-id="dabed-193">In hello web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="dabed-194">TelemetryClients de nouveau tous les ajoute automatiquement la valeur de propriété hello que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="dabed-194">All new TelemetryClients automatically add hello property value you specify.</span></span> <span data-ttu-id="dabed-195">Événements de télémétrie individuels peuvent remplacer les valeurs par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="dabed-195">Individual telemetry events can override hello default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dabed-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dabed-196">Next steps</span></span>
   - [<span data-ttu-id="dabed-197">Utilisateurs, sessions, événements</span><span class="sxs-lookup"><span data-stu-id="dabed-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="dabed-198">Entonnoirs</span><span class="sxs-lookup"><span data-stu-id="dabed-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="dabed-199">Rétention</span><span class="sxs-lookup"><span data-stu-id="dabed-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="dabed-200">Flux d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="dabed-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="dabed-201">Classeurs</span><span class="sxs-lookup"><span data-stu-id="dabed-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="dabed-202">Ajouter du contexte utilisateur</span><span class="sxs-lookup"><span data-stu-id="dabed-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
