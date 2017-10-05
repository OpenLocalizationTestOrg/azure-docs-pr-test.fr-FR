---
title: "Examiner et de partager des données d’utilisation avec des classeurs interactifs dans Azure Application Insights | Microsoft docs"
description: "Analyse démographique des utilisateurs de votre application web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: 75028b4fbda43d90f56690a33c7eb624fce049c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="4c174-103">Examiner et de partager des données d’utilisation avec des classeurs interactifs dans Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="4c174-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="4c174-104">Les classeurs associent des visualisations de données [Azure Application Insights](app-insights-overview.md), [des requêtes Analytics](app-insights-analytics.md)et du texte dans des documents interactifs.</span><span class="sxs-lookup"><span data-stu-id="4c174-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="4c174-105">Les classeurs sont modifiables par les autres membres de l’équipe ayant accès à la même ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="4c174-105">Workbooks are editable by other team members with access to the same Azure resource.</span></span> <span data-ttu-id="4c174-106">Cela signifie que les requêtes et les contrôles utilisés pour créer un classeur sont à la disposition d’autres personnes consultant ce dernier, ce qui les rend faciles à explorer, à étendre et simplifie les recherches dans ceux-ci.</span><span class="sxs-lookup"><span data-stu-id="4c174-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span></span>

<span data-ttu-id="4c174-107">Les classeurs sont utiles pour :</span><span class="sxs-lookup"><span data-stu-id="4c174-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="4c174-108">Explorer l’utilisation de votre application lorsque vous ne connaissez pas les mesures d’intérêt à l’avance : nombre d’utilisateurs, taux de rétention, taux de conversion, etc. Contrairement à d’autres outils d’analyse d’utilisation d’Application Insights, les classeurs vous permettent de combiner plusieurs types de visualisations et d’analyses, ce qui les rend très utile pour ce type d’exploration sous forme libre.</span><span class="sxs-lookup"><span data-stu-id="4c174-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="4c174-109">Expliquer à votre équipe le fonctionnement d’une toute nouvelle fonctionnalité, en montrant le nombre d’interactions clés et d’autres mesures de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4c174-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="4c174-110">Partager les résultats d’une expérimentation A/B dans votre application avec d’autres membres de votre équipe.</span><span class="sxs-lookup"><span data-stu-id="4c174-110">Sharing the results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="4c174-111">Vous pouvez expliquer les objectifs de l’expérimentation avec le texte, puis montrer chaque mesure d’utilisation et requête Analytics utilisée pour évaluer l’expérimentation, en vous aidant de légendes claires indiquant si chaque mesure se situe au-dessus ou en dessous de la cible.</span><span class="sxs-lookup"><span data-stu-id="4c174-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="4c174-112">Créer des rapports relatifs à l’impact d’une panne sur l’utilisation de votre application, en combinant des données, une explication du texte et une présentation des étapes suivantes pour éviter à l’avenir d’éventuelles interruptions.</span><span class="sxs-lookup"><span data-stu-id="4c174-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="4c174-113">Votre ressource Application Insights doit contenir des vues de page ou des événements personnalisés pour utiliser les classeurs.</span><span class="sxs-lookup"><span data-stu-id="4c174-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span></span> <span data-ttu-id="4c174-114">[Découvrez comment configurer votre application pour collecter des vues de page automatiquement à l’aide du Kit de développement logiciel (SDK) JavaScript Application Insights](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="4c174-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="4c174-115">Modifier, réorganiser, cloner et supprimer des sections de classeur</span><span class="sxs-lookup"><span data-stu-id="4c174-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="4c174-116">Un classeur est composé de sections : visualisations d’utilisation, graphiques, tables, texte ou résultats de requête Analytics modifiables de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="4c174-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="4c174-117">Pour modifier le contenu d’une section de classeur, cliquez sur le bouton **Modifier** ci-dessous et à droite de la section du classeur.</span><span class="sxs-lookup"><span data-stu-id="4c174-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span></span>

![Commandes d’édition de la section Workbooks d’Application Insights](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="4c174-119">Lorsque vous avez fini de modifier une section, cliquez sur **Modifications terminées** dans l’angle inférieur gauche de la section.</span><span class="sxs-lookup"><span data-stu-id="4c174-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span></span>

2. <span data-ttu-id="4c174-120">Pour créer un doublon de section, cliquez sur l’icône **Cloner cette section**.</span><span class="sxs-lookup"><span data-stu-id="4c174-120">To create a duplicate of a section, click the **Clone this section** icon.</span></span> <span data-ttu-id="4c174-121">La création de sections en double est une bonne façon d’itérer sur une requête sans perdre les itérations précédentes.</span><span class="sxs-lookup"><span data-stu-id="4c174-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="4c174-122">Pour déplacer une section vers un classeur, cliquez sur l’icône **Déplacer vers le haut** ou **Déplacer vers le bas**.</span><span class="sxs-lookup"><span data-stu-id="4c174-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="4c174-123">Pour supprimer une section de façon permanente, cliquez sur l’icône **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="4c174-123">To remove a section permanently, click the **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="4c174-124">Ajout de sections de visualisation de données d’utilisation</span><span class="sxs-lookup"><span data-stu-id="4c174-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="4c174-125">Les classeurs proposent quatre types de visualisations d’analyse d’utilisation intégrées.</span><span class="sxs-lookup"><span data-stu-id="4c174-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="4c174-126">Chacune répond à une question courante concernant l’utilisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="4c174-126">Each answers a common question about the usage of your app.</span></span> <span data-ttu-id="4c174-127">Pour ajouter des tables et des graphiques autres que ces quatre sections, ajoutez des sections de requête Analytics (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="4c174-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="4c174-128">Pour ajouter une section Utilisateurs, Sessions, Événements ou Rétention à votre classeur, utilisez **Ajouter des utilisateurs** ou tout autre bouton correspondant au bas du classeur ou d’une section.</span><span class="sxs-lookup"><span data-stu-id="4c174-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span></span>

![Section Utilisateurs dans Workbooks](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="4c174-130">Les sections **Utilisateurs** répondent à la question « Combien d’utilisateurs ont visualisé une page ou utilisé une certaine fonctionnalité de mon site ? »</span><span class="sxs-lookup"><span data-stu-id="4c174-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="4c174-131">Les sections **Sessions** répondent à la question « Combien de sessions les utilisateurs ont-ils passé à afficher une page ou à utiliser certaines fonctionnalités de mon site ? »</span><span class="sxs-lookup"><span data-stu-id="4c174-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="4c174-132">Les sections **Événements** répondent à la question « Combien de fois les utilisateurs ont-ils affiché une page ou utilisé certaines fonctionnalités de mon site ? »</span><span class="sxs-lookup"><span data-stu-id="4c174-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="4c174-133">Chacun de ces types de trois sections propose les mêmes ensembles de commandes et de visualisations :</span><span class="sxs-lookup"><span data-stu-id="4c174-133">Each of these three section types offers the same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="4c174-134">En savoir plus sur la modification des sections Utilisateurs, Sessions et Événements</span><span class="sxs-lookup"><span data-stu-id="4c174-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="4c174-135">Activez/désactivez les visualisations relatives au graphique principal, aux grilles d’histogramme, aux insights automatiques et aux échantillons d’utilisateurs à l’aide des cases à cocher **Afficher le graphique**, **Afficher la grille**, **Afficher les insights**, et **Échantillon de ces utilisateurs** situées en haut de chaque section.</span><span class="sxs-lookup"><span data-stu-id="4c174-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span></span>

![Section Rétention dans Workbooks](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="4c174-137">Les sections **Rétention** répondent à la question « Sur les personnes ayant affiché une page ou utilisé des fonctionnalités un jour ou une semaine donnée, combien sont revenues le jour ou la semaine suivante ? »</span><span class="sxs-lookup"><span data-stu-id="4c174-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="4c174-138">En savoir plus sur la modification des sections Rétention</span><span class="sxs-lookup"><span data-stu-id="4c174-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="4c174-139">Activez/désactivez le graphique facultatif de rétention global à l’aide de la case à cocher **Afficher le graphique de rétention global**située en haut de la section.</span><span class="sxs-lookup"><span data-stu-id="4c174-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="4c174-140">Ajout de sections Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="4c174-140">Adding Application Insights Analytics sections</span></span>

![Section Analytics dans Workbooks](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="4c174-142">Pour ajouter une section Application Insights Analytics à votre classeur, utilisez le bouton **Ajouter une requête Analytics** situé en bas du classeur, ou de chaque section.</span><span class="sxs-lookup"><span data-stu-id="4c174-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span></span>

<span data-ttu-id="4c174-143">Les sections de requête Analytics vous permettent d’ajouter des requêtes arbitraires sur vos données Application Insights dans les classeurs.</span><span class="sxs-lookup"><span data-stu-id="4c174-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="4c174-144">Cette flexibilité signifie que les sections de requête Analytics doivent être votre réponse privilégiée à toute question relative à votre site autre que les quatre répertoriées ci-dessus pour les Utilisateurs, les Sessions, les Événements et la Rétention :</span><span class="sxs-lookup"><span data-stu-id="4c174-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="4c174-145">Combien d’exceptions votre site a levé au cours de la même période en tant que refus d’utilisation ?</span><span class="sxs-lookup"><span data-stu-id="4c174-145">How many exceptions did your site throw during the same time period as a decline in usage?</span></span>
* <span data-ttu-id="4c174-146">Quelle était la répartition des temps de chargement de page pour les utilisateurs affichant une page ?</span><span class="sxs-lookup"><span data-stu-id="4c174-146">What was the distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="4c174-147">Combien d’utilisateurs ont affiché certaines pages de votre site en particulier ?</span><span class="sxs-lookup"><span data-stu-id="4c174-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="4c174-148">Il peut être utile de savoir si des groupes d’utilisateurs utilisent différents sous-ensembles de fonctionnalités de votre site (utilisez l’opérateur `join` avec le modificateur `kind=leftanti` dans le langage de requête Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="4c174-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span></span>

<span data-ttu-id="4c174-149">Utilisez le [document de référence du langage de requête Log Analytics](https://docs.loganalytics.io/) pour en savoir plus sur l’écriture des requêtes.</span><span class="sxs-lookup"><span data-stu-id="4c174-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="4c174-150">Ajout de texte et de sections Markdown</span><span class="sxs-lookup"><span data-stu-id="4c174-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="4c174-151">Le fait d’ajouter des en-têtes, des explications et des commentaires à vos classeurs permet de donner un aspect narratif à un ensemble de tables et de graphiques.</span><span class="sxs-lookup"><span data-stu-id="4c174-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="4c174-152">Les sections de texte des classeurs prennent en charge la [syntaxe Markdown](https://daringfireball.net/projects/markdown/) pour la mise en forme du texte (en-têtes, gras, italique et listes à puces, par exemple).</span><span class="sxs-lookup"><span data-stu-id="4c174-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="4c174-153">Pour ajouter une section de textes à votre classeur, utilisez le bouton **Ajouter du texte** situé en bas du classeur, ou de chaque section.</span><span class="sxs-lookup"><span data-stu-id="4c174-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="4c174-154">Enregistrer et partager des classeurs avec votre équipe</span><span class="sxs-lookup"><span data-stu-id="4c174-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="4c174-155">Les classeurs sont enregistrés au sein d’une ressource Application Insights, soit dans la section **Mes rapports** qui est privée ou dans la section **Rapports partagés** accessible à tous les utilisateurs ayant accès à la ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4c174-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span></span> <span data-ttu-id="4c174-156">Pour afficher tous les classeurs de la ressource, cliquez sur le bouton **Ouvrir** dans la barre d’action.</span><span class="sxs-lookup"><span data-stu-id="4c174-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span></span>

<span data-ttu-id="4c174-157">Pour partager un classeur qui se trouve actuellement dans **Mes rapports** :</span><span class="sxs-lookup"><span data-stu-id="4c174-157">To share a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="4c174-158">Dans la barre d’action, cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="4c174-158">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="4c174-159">Cliquez sur le bouton «... » en regard du classeur que vous souhaitez partager.</span><span class="sxs-lookup"><span data-stu-id="4c174-159">Click the "..." button beside the workbook you want to share</span></span>
3. <span data-ttu-id="4c174-160">Cliquez sur **Déplacer vers les rapports partagés**.</span><span class="sxs-lookup"><span data-stu-id="4c174-160">Click **Move to Shared Reports**.</span></span>

<span data-ttu-id="4c174-161">Pour partager un classeur avec un lien ou par e-mail, cliquez sur **Partager** dans la barre d’action.</span><span class="sxs-lookup"><span data-stu-id="4c174-161">To share a workbook with a link or via email, click **Share** in the action bar.</span></span> <span data-ttu-id="4c174-162">Gardez à l’esprit que les destinataires du lien ont besoin d’accéder à cette ressource dans le portail Azure pour afficher le classeur.</span><span class="sxs-lookup"><span data-stu-id="4c174-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span></span> <span data-ttu-id="4c174-163">Pour apporter des modifications, les destinataires doivent au moins disposer des autorisations de collaborateur pour la ressource.</span><span class="sxs-lookup"><span data-stu-id="4c174-163">To make edits, recipients need at least Contributor permissions for the resource.</span></span>

<span data-ttu-id="4c174-164">Pour épingler un lien à un classeur dans un tableau de bord Azure :</span><span class="sxs-lookup"><span data-stu-id="4c174-164">To pin a link to a workbook to an Azure Dashboard:</span></span>

1. <span data-ttu-id="4c174-165">Dans la barre d’action, cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="4c174-165">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="4c174-166">Cliquez sur le bouton «... » en regard du classeur que vous souhaitez épingler.</span><span class="sxs-lookup"><span data-stu-id="4c174-166">Click the "..." button beside the workbook you want to pin</span></span>
3. <span data-ttu-id="4c174-167">Cliquez sur **Épingler au tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="4c174-167">Click **Pin to dashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c174-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c174-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c174-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c174-169">Next steps</span></span>
- <span data-ttu-id="4c174-170">Pour activer les expériences d’utilisation, commencez à envoyer des [événements personnalisés](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou des [affichages de page](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="4c174-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="4c174-171">Si vous envoyez déjà des événements personnalisés ou des affichages de page, explorez les outils d’utilisation pour savoir comment les utilisateurs emploient votre service.</span><span class="sxs-lookup"><span data-stu-id="4c174-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="4c174-172">Utilisateurs, sessions, événements</span><span class="sxs-lookup"><span data-stu-id="4c174-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="4c174-173">Entonnoirs</span><span class="sxs-lookup"><span data-stu-id="4c174-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="4c174-174">Rétention</span><span class="sxs-lookup"><span data-stu-id="4c174-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="4c174-175">Flux d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="4c174-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="4c174-176">Ajouter du contexte utilisateur</span><span class="sxs-lookup"><span data-stu-id="4c174-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
