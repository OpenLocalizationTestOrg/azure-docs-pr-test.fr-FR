---
title: "Analyse de la rétention utilisateur des applications web avec Azure Application Insights | Microsoft Docs"
description: "Combien d’utilisateurs reviennent vers votre application ?"
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
ms.openlocfilehash: 7f7ca19ab171278bbd82f68e3822bc650b25373d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="f7a8c-103">Analyse de la rétention utilisateur des applications web avec Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="f7a8c-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="f7a8c-104">La fonction de rétention [d’Azure Application Insights](app-insights-overview.md) vous aide à analyser le nombre d’utilisateurs qui reviennent vers votre application et la fréquence à laquelle ils exécutent des tâches particulières ou atteignent des objectifs.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-104">The retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return to your app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="f7a8c-105">Par exemple, si vous exécutez un site de jeu, vous pouvez comparer le nombre d’utilisateurs qui reviennent sur le site après avoir perdu à un jeu avec le nombre d’utilisateurs qui reviennent après avoir gagné.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-105">For example, if you run a game site, you could compare the numbers of users who return to the site after losing a game with the number who return after winning.</span></span> <span data-ttu-id="f7a8c-106">Cette information peut vous aider à améliorer l’expérience de vos utilisateurs et votre stratégie commerciale.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="f7a8c-107">Prise en main</span><span class="sxs-lookup"><span data-stu-id="f7a8c-107">Get started</span></span>

<span data-ttu-id="f7a8c-108">Si aucune donnée n’apparaît dans l’outil de rétention du portail Application Insights, [découvrez comment prendre en main les outils d’utilisation](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7a8c-108">If you don't yet see data in the retention tool in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-retention-tool"></a><span data-ttu-id="f7a8c-109">Outil de rétention</span><span class="sxs-lookup"><span data-stu-id="f7a8c-109">The Retention tool</span></span>

![Outil de rétention](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="f7a8c-111">La barre d’outils permet aux utilisateurs de créer des rapports de rétention, d’ouvrir les rapports de rétention existants, d’enregistrer le rapport de rétention en cours directement ou à un autre emplacement, d’annuler les modifications apportées aux rapports enregistrés, d’actualiser les données du rapport, de partager des rapports par e-mail ou lien direct, et d’accéder à la page de documentation.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-111">The toolbar allows users to create new retention reports, open existing retention reports, save current retention report or save as, revert changes made to saved reports, refresh data on the report, share report via email or direct link, and access the documentation page.</span></span> 
2. <span data-ttu-id="f7a8c-112">Par défaut, la rétention affiche tous les utilisateurs qui ont effectué une action, puis sont revenus et ont effectué une autre action sur une période donnée.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="f7a8c-113">Vous pouvez choisir une combinaison différente d’événements afin de filtrer des activités utilisateur particulières.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-113">You can select different combination of events to narrow the focus on specific user activities.</span></span>
3. <span data-ttu-id="f7a8c-114">Ajoutez un ou plusieurs filtres sur les propriétés.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-114">Add one or more filters on properties.</span></span> <span data-ttu-id="f7a8c-115">Par exemple, vous pouvez cibler les utilisateurs d’un pays ou d’une région spécifique.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="f7a8c-116">Cliquez sur **Mettre à jour** après avoir défini les filtres.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-116">Click **Update** after setting the filters.</span></span> 
4. <span data-ttu-id="f7a8c-117">Le graphique de rétention globale récapitule la rétention utilisateur sur la période sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-117">The overall retention chart shows a summary of user retention across the selected time period.</span></span> 
5. <span data-ttu-id="f7a8c-118">La grille affiche le nombre d’utilisateurs conservés en fonction du générateur de requêtes au point 2.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-118">The grid shows the number of users retained according to the query builder in #2.</span></span> <span data-ttu-id="f7a8c-119">Chaque ligne représente une cohorte d’utilisateurs ayant effectué l’un des événements pendant la période de temps indiquée.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-119">Each row represents a cohort of users who performed any event in the time period shown.</span></span> <span data-ttu-id="f7a8c-120">Chaque cellule de la ligne indique combien de cette cohorte sont revenus au moins une fois pendant une période ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-120">Each cell in the row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="f7a8c-121">Certains utilisateurs peuvent revenir pendant plusieurs périodes.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="f7a8c-122">Les cartes d’aperçu affichent les cinq principaux événements de lancement et les cinq principaux événements renvoyés pour aider les utilisateurs à mieux comprendre leur rapport de rétention.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-122">The insights cards show top five initiating events, and top five returned events to give users a better understanding of their retention report.</span></span> 

![Passage de la souris sur la fonction de rétention](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="f7a8c-124">Les utilisateurs peuvent survoler les cellules de l’outil de rétention pour accéder au bouton Analytics ainsi qu’à des info-bulles qui expliquent la signification de la cellule.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-124">Users can hover over cells on the retention tool to access the analytics button and tool tips explaining what the cell means.</span></span> <span data-ttu-id="f7a8c-125">Le bouton Analytics redirige les utilisateurs vers l’outil Analytics avec une requête prédéfinie pour générer des utilisateurs à partir de la cellule.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-125">The Analytics button takes users to the Analytics tool with a pre-populated query to generate users from the cell.</span></span> 

## <a name="use-business-events-to-track-retention"></a><span data-ttu-id="f7a8c-126">Utiliser des événements commerciaux pour suivre la rétention</span><span class="sxs-lookup"><span data-stu-id="f7a8c-126">Use business events to track retention</span></span>

<span data-ttu-id="f7a8c-127">Pour obtenir l’analyse de rétention la plus utile, mesurez les événements qui représentent des activités commerciales significatives.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-127">To get the most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="f7a8c-128">Par exemple, un grand nombre d’utilisateurs peuvent ouvrir une page dans votre application sans jouer au jeu qu’elle affiche.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-128">For example, many users might open a page in your app without playing the game that it displays.</span></span> <span data-ttu-id="f7a8c-129">Le suivi des vues de pages uniquement fournit ainsi une estimation inexacte du nombre de personnes qui reviennent pour jouer au jeu auquel ont déjà joué.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-129">Tracking just the page views would therefore provide an inaccurate estimate of how many people return to play the game after enjoying it previously.</span></span> <span data-ttu-id="f7a8c-130">Pour obtenir une vision claire des lecteurs qui reviennent, votre application doit envoyer un événement personnalisé lorsqu’un utilisateur joue réellement.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-130">To get a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="f7a8c-131">Il est recommandé de coder les événements personnalisés qui représentent des actions commerciales clés et de les utiliser pour votre analyse de rétention.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-131">It's good practice to code custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="f7a8c-132">Pour capturer le résultat du jeu, vous devez écrire une ligne de code pour envoyer un événement personnalisé à Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-132">To capture the game outcome, you need to write a line of code to send a custom event to Application Insights.</span></span> <span data-ttu-id="f7a8c-133">Si vous l’écrivez dans le code de page web ou en Node.JS, voici à quoi il ressemble :</span><span class="sxs-lookup"><span data-stu-id="f7a8c-133">If you write it in the web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="f7a8c-134">Ou dans le code de serveur ASP.NET :</span><span class="sxs-lookup"><span data-stu-id="f7a8c-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="f7a8c-135">[Familiarisez-vous avec l’écriture d’événements personnalisés](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="f7a8c-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="f7a8c-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f7a8c-136">Next steps</span></span>
- <span data-ttu-id="f7a8c-137">Pour activer les expériences d’utilisation, commencez à envoyer des [événements personnalisés](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou des [affichages de page](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="f7a8c-137">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="f7a8c-138">Si vous envoyez déjà des événements personnalisés ou des affichages de page, explorez les outils d’utilisation pour savoir comment les utilisateurs emploient votre service.</span><span class="sxs-lookup"><span data-stu-id="f7a8c-138">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="f7a8c-139">Utilisateurs, sessions, événements</span><span class="sxs-lookup"><span data-stu-id="f7a8c-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="f7a8c-140">Entonnoirs</span><span class="sxs-lookup"><span data-stu-id="f7a8c-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="f7a8c-141">Flux d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="f7a8c-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="f7a8c-142">Classeurs</span><span class="sxs-lookup"><span data-stu-id="f7a8c-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="f7a8c-143">Ajouter du contexte utilisateur</span><span class="sxs-lookup"><span data-stu-id="f7a8c-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


