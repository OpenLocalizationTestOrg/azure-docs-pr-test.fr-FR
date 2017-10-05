---
title: "Analyse de l’utilisation des applications web avec Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 63b74399790b718e14a5b6e09bc009a336caf928
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="3cbc6-103">Analyse de l’utilisation des applications web avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="3cbc6-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="3cbc6-104">Quelles sont les fonctionnalités de votre application web les plus populaires ?</span><span class="sxs-lookup"><span data-stu-id="3cbc6-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="3cbc6-105">Vos utilisateurs atteignent-ils leurs objectifs avec votre application ?</span><span class="sxs-lookup"><span data-stu-id="3cbc6-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="3cbc6-106">Disparaissent-ils à des stades spécifiques, et reviennent-ils plus tard ?</span><span class="sxs-lookup"><span data-stu-id="3cbc6-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="3cbc6-107">[Azure Application Insights](app-insights-overview.md) vous permet d’obtenir un aperçu utile sur l’utilisation de votre application web.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="3cbc6-108">Chaque fois que vous mettez à jour votre application, vous pouvez évaluer son bon fonctionnement pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="3cbc6-109">Grâce à ces informations, vous pouvez prendre des décisions basées sur des données sur les cycles de développement suivants.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="3cbc6-110">Envoyer des données de télémétrie à partir de votre application</span><span class="sxs-lookup"><span data-stu-id="3cbc6-110">Send telemetry from your app</span></span>

<span data-ttu-id="3cbc6-111">La meilleure expérience est obtenue en installant Application Insights à la fois dans votre code serveur d’applications et dans vos pages web.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-111">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="3cbc6-112">Les composants client et serveur de votre application envoient la télémétrie au portail Azure pour analyse.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-112">The client and server components of your app send telemetry back to the Azure portal for analysis.</span></span>

1. <span data-ttu-id="3cbc6-113">**Code serveur :** installez le module approprié pour votre [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md) ou une [autre](app-insights-platforms.md) application.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-113">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="3cbc6-114">*Vous ne voulez pas installer de code serveur ? Vous pouvez simplement [créer une ressource Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="3cbc6-114">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="3cbc6-115">**Code de page Web :** ouvrez le [portail Azure](https://portal.azure.com), ouvrez la ressource Application Insights pour votre application, puis ouvrez **Mise en route > Monitor and Diagnose Client-Side (Surveiller et diagnostiquer côté client)**.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-115">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Copiez le script dans l’en-tête de votre page web maître.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="3cbc6-117">**Obtenir la télémétrie :** exécutez votre projet en mode débogage pendant quelques minutes, puis examinez les résultats dans le panneau Vue d’ensemble dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span></span>

    <span data-ttu-id="3cbc6-118">Publiez votre application pour surveiller les performances de votre application et découvrir ce que vos utilisateurs font avec votre application.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-118">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="3cbc6-119">Inclure l’ID d’utilisateur et l’ID de session dans votre télémétrie</span><span class="sxs-lookup"><span data-stu-id="3cbc6-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="3cbc6-120">Pour effectuer le suivi des utilisateurs au fil du temps, Application Insights nécessite un moyen de les identifier.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-120">To track users over time, Application Insights requires a way to identify them.</span></span> <span data-ttu-id="3cbc6-121">L’outil Événements est le seul outil d’utilisation qui ne nécessite pas d’ID d’utilisateur ni d’ID de session.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-121">The Events tool is the only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="3cbc6-122">Commencez à envoyer ces ID [ici](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="3cbc6-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="3cbc6-123">Explorer des données démographiques et des statistiques de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="3cbc6-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="3cbc6-124">Découvrez quand des personnes utilisent votre application, les pages qui les intéressent le plus, où vos utilisateurs se trouvent, les navigateurs et les systèmes d’exploitation qu’ils utilisent.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="3cbc6-125">Les rapports Utilisateurs et sessions filtrent vos données par pages ou événements personnalisés, et les segmentent par propriétés telles que l’emplacement, l’environnement et la page.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-125">The Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="3cbc6-126">Vous pouvez également ajouter vos propres filtres.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-126">You can also add your own filters.</span></span>

![Utilisateurs](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="3cbc6-128">Aperçu des modèles intéressants appropriés dans le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-128">Insights on the right point out interesting patterns in the set of data.</span></span>  

* <span data-ttu-id="3cbc6-129">Le rapport **Utilisateurs** compte le nombre d’utilisateurs uniques qui accèdent à vos pages dans les délais que vous avez choisis.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-129">The **Users** report counts the numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="3cbc6-130">(Les utilisateurs sont comptés avec les cookies.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="3cbc6-131">Si un utilisateur accède à votre site avec différents navigateurs ou ordinateurs clients, ou efface ses cookies, il sera compté plusieurs fois.)</span><span class="sxs-lookup"><span data-stu-id="3cbc6-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="3cbc6-132">Le rapport **Sessions** compte le nombre de sessions utilisateur qui accèdent à votre site.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-132">The **Sessions** report counts the number of user sessions that access your site.</span></span> <span data-ttu-id="3cbc6-133">Une session est une période d’activité d’un utilisateur, qui se termine par une période d’inactivité de plus d’une demi-heure.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="3cbc6-134">En savoir plus sur les outils Utilisateurs, Sessions et Événements</span><span class="sxs-lookup"><span data-stu-id="3cbc6-134">More about the Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="3cbc6-135">Affichages de page</span><span class="sxs-lookup"><span data-stu-id="3cbc6-135">Page views</span></span>

<span data-ttu-id="3cbc6-136">Dans le panneau Utilisation, cliquez sur la mosaïque Pages consultées pour découvrir une répartition de vos pages les plus populaires :</span><span class="sxs-lookup"><span data-stu-id="3cbc6-136">From the Usage blade, click through the Page Views tile to get a breakdown of your most popular pages:</span></span>

![Dans le panneau Vue d'ensemble, cliquez sur le graphique des pages vues.](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="3cbc6-138">L'exemple ci-dessus vient d’un site web de jeux.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-138">The example above is from a games web site.</span></span> <span data-ttu-id="3cbc6-139">Dans les graphiques, nous pouvons voir instantanément :</span><span class="sxs-lookup"><span data-stu-id="3cbc6-139">From the charts, we can instantly see:</span></span>

* <span data-ttu-id="3cbc6-140">L'utilisation ne s'est pas améliorée au cours de la semaine écoulée.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-140">Usage hasn't improved in the past week.</span></span> <span data-ttu-id="3cbc6-141">Peut-être que nous devrions envisager une optimisation pour les moteurs de recherche ?</span><span class="sxs-lookup"><span data-stu-id="3cbc6-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="3cbc6-142">Tennis est la page de jeu la plus populaire.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-142">Tennis is the most popular game page.</span></span> <span data-ttu-id="3cbc6-143">Concentrons-nous sur d’autres améliorations de cette page.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-143">Let's focus on further improvements to this page.</span></span>
* <span data-ttu-id="3cbc6-144">En moyenne, les utilisateurs visitent la page Tennis environ trois fois par semaine.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-144">On average, users visit the Tennis page about three times per week.</span></span> <span data-ttu-id="3cbc6-145">(Il y a près de trois fois plus de sessions que d’utilisateurs.)</span><span class="sxs-lookup"><span data-stu-id="3cbc6-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="3cbc6-146">La plupart des utilisateurs visitent le site au cours de la semaine de travail aux États-Unis, et pendant les heures de travail.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-146">Most users visit the site during the U.S. working week, and in working hours.</span></span> <span data-ttu-id="3cbc6-147">Il serait peut-être envisageable de fournir un bouton de masquage rapide sur la page web.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-147">Perhaps we should provide a "quick hide" button on the web page.</span></span>
* <span data-ttu-id="3cbc6-148">Les [annotations](app-insights-annotations.md) sur le graphique montrent à quel moment les nouvelles versions du site web ont été déployées.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-148">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span></span> <span data-ttu-id="3cbc6-149">Aucun des déploiements récents n’a eu d’effet notable sur l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-149">None of the recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="3cbc6-150">Qu’en est-il si vous souhaitez examiner plus en détails le trafic vers votre site, comme le fractionnement par une propriété personnalisée que votre site envoie dans sa télémétrie d’affichage de page ?</span><span class="sxs-lookup"><span data-stu-id="3cbc6-150">What if you want to investigate the traffic to your site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="3cbc6-151">Ouvrez l’outil **Événements** dans le menu de la ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-151">Open the **Events** tool in the Application Insights resource menu.</span></span> <span data-ttu-id="3cbc6-152">Cet outil vous permet d’analyser combien de pages consultées et d’événements personnalisés ont été envoyés à partir de votre application, sur la base des différentes options de filtrage, cohorte et segmentation.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="3cbc6-153">Dans la liste déroulante « Qui a utilisé », sélectionnez « N’importe quelle page consultée ».</span><span class="sxs-lookup"><span data-stu-id="3cbc6-153">In the "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="3cbc6-154">Dans la liste déroulante « Fractionner par », sélectionnez une propriété selon laquelle fractionner votre télémétrie d’affichage de page.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-154">In the "Split by" dropdown, select a property by which to split your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="3cbc6-155">Rétention - Combien d’utilisateurs reviennent ?</span><span class="sxs-lookup"><span data-stu-id="3cbc6-155">Retention - how many users come back?</span></span>

<span data-ttu-id="3cbc6-156">La rétention vous permet de comprendre la fréquence à laquelle vos utilisateurs reviennent utiliser leur application, en fonction des cohortes d’utilisateurs qui ont effectué une action pendant une période donnée.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-156">Retention helps you understand how often your users return to use their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="3cbc6-157">Comprendre quelles fonctionnalités spécifiques font revenir les utilisateurs plus que d’autres</span><span class="sxs-lookup"><span data-stu-id="3cbc6-157">Understand what specific features cause users to come back more than others</span></span> 
- <span data-ttu-id="3cbc6-158">Formuler des hypothèses en fonction des données utilisateur réel</span><span class="sxs-lookup"><span data-stu-id="3cbc6-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="3cbc6-159">Déterminer si la rétention est un problème dans votre produit</span><span class="sxs-lookup"><span data-stu-id="3cbc6-159">Determine whether retention is a problem in your product</span></span> 

![Rétention](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="3cbc6-161">Les commandes de rétention en haut vous permettent de définir des événements spécifiques et un intervalle de temps pour calculer la rétention.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-161">The retention controls on top allow you to define specific events and time range to calculate retention.</span></span> <span data-ttu-id="3cbc6-162">Le graphique au centre fournit une représentation visuelle du pourcentage de rétention globale sur l’intervalle de temps spécifié.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-162">The graph in the middle gives a visual representation of the overall retention percentage by the time range specified.</span></span> <span data-ttu-id="3cbc6-163">Le graphique en bas représente la rétention sur une période de temps donnée.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-163">The graph on the bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="3cbc6-164">Ce niveau de détail vous permet de comprendre de manière plus approfondie ce que font vos utilisateurs et ce qui les peut amener à revenir.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-164">This level of detail allows you to understand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="3cbc6-165">En savoir plus sur l’outil de rétention</span><span class="sxs-lookup"><span data-stu-id="3cbc6-165">More about the Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="3cbc6-166">Événements personnalisés</span><span class="sxs-lookup"><span data-stu-id="3cbc6-166">Custom business events</span></span>

<span data-ttu-id="3cbc6-167">Pour bien comprendre ce que font les utilisateurs avec votre application web, il est utile d’insérer des lignes de code pour enregistrer des événements personnalisés.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-167">To get a clear understanding of what users do with your web app, it's useful to insert lines of code to log custom events.</span></span> <span data-ttu-id="3cbc6-168">Ces événements permettent de suivre toute activité, des actions détaillées des utilisateurs comme un clic sur un bouton, aux événements plus significatifs comme un de faire un achat ou de gagner à un jeu.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-168">These events can track anything from detailed user actions such as clicking specific buttons, to more significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="3cbc6-169">Bien que les pages consultées puissent représenter des événements utiles, cela n’est en général pas le cas.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="3cbc6-170">Un utilisateur peut ouvrir une page produit sans acheter le produit.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-170">A user can open a product page without buying the product.</span></span> 

<span data-ttu-id="3cbc6-171">Grâce aux événements spécifiques, vous pouvez représenter la progression de vos utilisateurs sur votre site.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="3cbc6-172">Vous pouvez connaître leurs préférences sur les différentes options et où ils abandonnent ou rencontrent des difficultés.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="3cbc6-173">Grâce à ces informations, vous pouvez prendre des décisions avisées sur les priorités de vos travaux de développement en souffrance.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-173">With this knowledge, you can make informed decisions about the priorities in your development backlog.</span></span>

<span data-ttu-id="3cbc6-174">Les événements peuvent être enregistrés dans la page web :</span><span class="sxs-lookup"><span data-stu-id="3cbc6-174">Events can be logged in the web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="3cbc6-175">Ou sur le côté serveur de l’application web :</span><span class="sxs-lookup"><span data-stu-id="3cbc6-175">Or in the server side of the web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="3cbc6-176">Vous pouvez joindre des valeurs de propriété à ces événements, afin de pouvoir filtrer ou fractionner les événements lorsque vous les étudiez dans le portail.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-176">You can attach property values to these events, so that you can filter or split the events when you inspect them in the portal.</span></span> <span data-ttu-id="3cbc6-177">Un ensemble standard de propriétés est également associé à chaque événement, comme des ID d’utilisateur anonymes, vous permettant ainsi de suivre la séquence d’activités d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-177">In addition, a standard set of properties is attached to each event, such as anonymous user ID, which allows you to trace the sequence of activities of an individual user.</span></span>

<span data-ttu-id="3cbc6-178">En savoir plus sur les [événements personnalisés](app-insights-api-custom-events-metrics.md#trackevent) et les [propriétés](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="3cbc6-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="3cbc6-179">Segmenter et traiter les événements</span><span class="sxs-lookup"><span data-stu-id="3cbc6-179">Slice and dice events</span></span>

<span data-ttu-id="3cbc6-180">Dans les outils Utilisateurs, Sessions et Événements, vous pouvez segmenter et traiter des événements personnalisés par utilisateur, nom d’événement et propriétés.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-180">In the Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="3cbc6-181">![Utilisateurs](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="3cbc6-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-the-telemetry-with-the-app"></a><span data-ttu-id="3cbc6-182">Concevoir la télémétrie avec l’application</span><span class="sxs-lookup"><span data-stu-id="3cbc6-182">Design the telemetry with the app</span></span>

<span data-ttu-id="3cbc6-183">Lorsque vous concevez chaque fonctionnalité de votre application, prenez en compte comment vous allez mesurer son succès auprès de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-183">When you are designing each feature of your app, consider how you are going to measure its success with your users.</span></span> <span data-ttu-id="3cbc6-184">Choisissez les événements à enregistrer et coder les appels de suivi de ces événements dans votre application dès le début.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-184">Decide what business events you need to record, and code the tracking calls for those events into your app from the start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="3cbc6-185">Test A | B</span><span class="sxs-lookup"><span data-stu-id="3cbc6-185">A | B Testing</span></span>
<span data-ttu-id="3cbc6-186">Si vous ne savez pas quelle variante de la fonctionnalité sera la plus efficace, publiez les deux versions et mettez-les à disposition de différents utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span></span> <span data-ttu-id="3cbc6-187">Mesurer le taux de réussite de chaque version et créez-en une version unifiée.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-187">Measure the success of each, and then move to a unified version.</span></span>

<span data-ttu-id="3cbc6-188">Pour cette technique, vous joignez des valeurs de propriétés distinctes à toute la télémétrie envoyée par chaque version de votre application.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-188">For this technique, you attach distinct property values to all the telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="3cbc6-189">Pour cela, vous définissez des propriétés dans le contexte TelemetryContext actif.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-189">You can do that by defining properties in the active TelemetryContext.</span></span> <span data-ttu-id="3cbc6-190">Ces propriétés par défaut sont ajoutées à chaque message de télémétrie que l'application envoie, non seulement vos messages personnalisés, mais aussi la télémétrie standard.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-190">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span></span>

<span data-ttu-id="3cbc6-191">Dans le portail Application Insights, filtrez et segmentez vos données sur les valeurs de propriétés, afin de comparer les différentes versions.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-191">In the Application Insights portal, filter and split your data on the property values, so as to compare the different versions.</span></span>

<span data-ttu-id="3cbc6-192">Pour ce faire, [configurez un initialiseur de télémétrie](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer) :</span><span class="sxs-lookup"><span data-stu-id="3cbc6-192">To do this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

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

<span data-ttu-id="3cbc6-193">Dans l’initialiseur de l’application web, par exemple Global.asax.cs :</span><span class="sxs-lookup"><span data-stu-id="3cbc6-193">In the web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="3cbc6-194">Tous les nouveaux TelemetryClients ajoutent automatiquement la valeur de propriété que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-194">All new TelemetryClients automatically add the property value you specify.</span></span> <span data-ttu-id="3cbc6-195">Les événements de télémétrie individuels peuvent remplacer les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="3cbc6-195">Individual telemetry events can override the default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cbc6-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3cbc6-196">Next steps</span></span>
   - [<span data-ttu-id="3cbc6-197">Utilisateurs, sessions, événements</span><span class="sxs-lookup"><span data-stu-id="3cbc6-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="3cbc6-198">Entonnoirs</span><span class="sxs-lookup"><span data-stu-id="3cbc6-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="3cbc6-199">Rétention</span><span class="sxs-lookup"><span data-stu-id="3cbc6-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="3cbc6-200">Flux d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="3cbc6-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="3cbc6-201">Classeurs</span><span class="sxs-lookup"><span data-stu-id="3cbc6-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="3cbc6-202">Ajouter du contexte utilisateur</span><span class="sxs-lookup"><span data-stu-id="3cbc6-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
