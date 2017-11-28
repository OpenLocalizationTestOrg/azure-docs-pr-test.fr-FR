---
title: "analyse de rétention aaaUser pour les applications web avec Azure Application Insights | Documents Microsoft"
description: "Nombre d’utilisateurs retourne tooyour application ?"
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
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="04f42-103">Analyse de la rétention utilisateur des applications web avec Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="04f42-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="04f42-104">fonctionnalité de rétention Hello [Azure Application Insights](app-insights-overview.md) vous aide à vous analysez le nombre d’utilisateurs retourner tooyour application, et la fréquence à laquelle effectuer des tâches particulières ou objectifs.</span><span class="sxs-lookup"><span data-stu-id="04f42-104">hello retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return tooyour app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="04f42-105">Par exemple, si vous exécutez un site de jeu, vous pouvez comparer les numéros de hello d’utilisateurs qui retournent des toohello site après la perte d’un jeu avec un nombre de hello retournent après gagnante.</span><span class="sxs-lookup"><span data-stu-id="04f42-105">For example, if you run a game site, you could compare hello numbers of users who return toohello site after losing a game with hello number who return after winning.</span></span> <span data-ttu-id="04f42-106">Cette information peut vous aider à améliorer l’expérience de vos utilisateurs et votre stratégie commerciale.</span><span class="sxs-lookup"><span data-stu-id="04f42-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="04f42-107">Prise en main</span><span class="sxs-lookup"><span data-stu-id="04f42-107">Get started</span></span>

<span data-ttu-id="04f42-108">Si vous ne voyez encore des données dans l’outil de rétention hello dans le portail Application Insights hello, [apprendre comment tooget démarrer avec les outils de l’utilisation de hello](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04f42-108">If you don't yet see data in hello retention tool in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-retention-tool"></a><span data-ttu-id="04f42-109">outil de conservation Hello</span><span class="sxs-lookup"><span data-stu-id="04f42-109">hello Retention tool</span></span>

![Outil de rétention](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="04f42-111">barre d’outils Hello permet aux utilisateurs des rapports de rétention toocreate, ouvrir les rapports existants de rétention, enregistrer le rapport de rétention actuelle ou enregistrer sous, rétablir les modifications apportées toosaved rapports, actualiser les données sur le rapport de hello, partage un rapport par e-mail ou un lien direct et hello d’accès page de la documentation.</span><span class="sxs-lookup"><span data-stu-id="04f42-111">hello toolbar allows users toocreate new retention reports, open existing retention reports, save current retention report or save as, revert changes made toosaved reports, refresh data on hello report, share report via email or direct link, and access hello documentation page.</span></span> 
2. <span data-ttu-id="04f42-112">Par défaut, la rétention affiche tous les utilisateurs qui ont effectué une action, puis sont revenus et ont effectué une autre action sur une période donnée.</span><span class="sxs-lookup"><span data-stu-id="04f42-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="04f42-113">Vous pouvez sélectionner une combinaison différente des événements toonarrow hello se concentrer sur les activités des utilisateurs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="04f42-113">You can select different combination of events toonarrow hello focus on specific user activities.</span></span>
3. <span data-ttu-id="04f42-114">Ajoutez un ou plusieurs filtres sur les propriétés.</span><span class="sxs-lookup"><span data-stu-id="04f42-114">Add one or more filters on properties.</span></span> <span data-ttu-id="04f42-115">Par exemple, vous pouvez cibler les utilisateurs d’un pays ou d’une région spécifique.</span><span class="sxs-lookup"><span data-stu-id="04f42-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="04f42-116">Cliquez sur **mise à jour** après avoir défini les filtres hello.</span><span class="sxs-lookup"><span data-stu-id="04f42-116">Click **Update** after setting hello filters.</span></span> 
4. <span data-ttu-id="04f42-117">Hello graphique de rétention globale affiche un résumé de la rétention de l’utilisateur entre hello période sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="04f42-117">hello overall retention chart shows a summary of user retention across hello selected time period.</span></span> 
5. <span data-ttu-id="04f42-118">grille de Hello montre nombre hello d’utilisateurs retenu conséquente Générateur de requêtes toohello # 2.</span><span class="sxs-lookup"><span data-stu-id="04f42-118">hello grid shows hello number of users retained according toohello query builder in #2.</span></span> <span data-ttu-id="04f42-119">Chaque ligne représente une cohorte d’utilisateurs ayant exécuté n’importe quel événement dans le temps de hello période affichée.</span><span class="sxs-lookup"><span data-stu-id="04f42-119">Each row represents a cohort of users who performed any event in hello time period shown.</span></span> <span data-ttu-id="04f42-120">Chaque cellule dans la ligne de hello montre retournée, combien de que cohorte au moins une fois dans une période ultérieure.</span><span class="sxs-lookup"><span data-stu-id="04f42-120">Each cell in hello row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="04f42-121">Certains utilisateurs peuvent revenir pendant plusieurs périodes.</span><span class="sxs-lookup"><span data-stu-id="04f42-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="04f42-122">les cartes insights Hello affichent les cinq principaux événements initiateur et cinq premiers retournée aux utilisateurs de toogive événements une meilleure compréhension de leur rapport de rétention.</span><span class="sxs-lookup"><span data-stu-id="04f42-122">hello insights cards show top five initiating events, and top five returned events toogive users a better understanding of their retention report.</span></span> 

![Passage de la souris sur la fonction de rétention](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="04f42-124">Les utilisateurs peuvent pointer sur les cellules de bouton de hello rétention outil tooaccess hello analytique et signifie que les info-bulles expliquant quelle cellule hello.</span><span class="sxs-lookup"><span data-stu-id="04f42-124">Users can hover over cells on hello retention tool tooaccess hello analytics button and tool tips explaining what hello cell means.</span></span> <span data-ttu-id="04f42-125">bouton d’Analytique Hello prend outil d’Analytique toohello utilisateurs avec des utilisateurs toogenerate requête prédéfinie à partir de la cellule de hello.</span><span class="sxs-lookup"><span data-stu-id="04f42-125">hello Analytics button takes users toohello Analytics tool with a pre-populated query toogenerate users from hello cell.</span></span> 

## <a name="use-business-events-tootrack-retention"></a><span data-ttu-id="04f42-126">Utiliser la rétention de tootrack événements business</span><span class="sxs-lookup"><span data-stu-id="04f42-126">Use business events tootrack retention</span></span>

<span data-ttu-id="04f42-127">tooget hello plus utiles rétention analysis, des événements de mesures qui représentent des activités d’entreprise importantes.</span><span class="sxs-lookup"><span data-stu-id="04f42-127">tooget hello most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="04f42-128">Par exemple, de nombreux utilisateurs peuvent ouvrir une page dans votre application sans jeu hello qu’il affiche.</span><span class="sxs-lookup"><span data-stu-id="04f42-128">For example, many users might open a page in your app without playing hello game that it displays.</span></span> <span data-ttu-id="04f42-129">Suivi uniquement les vues de page hello fournirait une estimation inexacte de combien de personnes retourne tooplay jeu de hello après elle précédemment.</span><span class="sxs-lookup"><span data-stu-id="04f42-129">Tracking just hello page views would therefore provide an inaccurate estimate of how many people return tooplay hello game after enjoying it previously.</span></span> <span data-ttu-id="04f42-130">tooget une image claire de retourner des lecteurs, votre application doit envoyer un événement personnalisé lorsqu’un utilisateur est lu réellement.</span><span class="sxs-lookup"><span data-stu-id="04f42-130">tooget a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="04f42-131">Il est conseillé toocode des événements personnalisés qui représentent des actions de la clé d’entreprise et les utilisent pour votre analyse de rétention.</span><span class="sxs-lookup"><span data-stu-id="04f42-131">It's good practice toocode custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="04f42-132">résultat de jeu hello toocapture, vous devez toowrite une ligne de code toosend une tooApplication d’événement personnalisé Insights.</span><span class="sxs-lookup"><span data-stu-id="04f42-132">toocapture hello game outcome, you need toowrite a line of code toosend a custom event tooApplication Insights.</span></span> <span data-ttu-id="04f42-133">Si vous l’écrire dans le code de page web hello ou Node.JS, il ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="04f42-133">If you write it in hello web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="04f42-134">Ou dans le code de serveur ASP.NET :</span><span class="sxs-lookup"><span data-stu-id="04f42-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="04f42-135">[Familiarisez-vous avec l’écriture d’événements personnalisés](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="04f42-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="04f42-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="04f42-136">Next steps</span></span>
- <span data-ttu-id="04f42-137">l’utilisation de tooenable rencontre, démarrer l’envoi de [événements personnalisés](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [des consultations de page](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="04f42-137">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="04f42-138">Si vous envoyez déjà hello l’utilisation des outils toolearn Explorer les événements personnalisés ou des vues de la page, comment les utilisateurs utiliser votre service.</span><span class="sxs-lookup"><span data-stu-id="04f42-138">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="04f42-139">Utilisateurs, sessions, événements</span><span class="sxs-lookup"><span data-stu-id="04f42-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="04f42-140">Entonnoirs</span><span class="sxs-lookup"><span data-stu-id="04f42-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="04f42-141">Flux d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="04f42-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="04f42-142">Classeurs</span><span class="sxs-lookup"><span data-stu-id="04f42-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="04f42-143">Ajouter du contexte utilisateur</span><span class="sxs-lookup"><span data-stu-id="04f42-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


