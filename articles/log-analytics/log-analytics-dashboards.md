---
title: "Créer un tableau de bord personnalisé dans Azure Log Analytics | Microsoft Docs"
description: "Ce guide vous aide à comprendre comment les tableaux de bord Log Analytics permettent d’afficher l’ensemble de vos recherches de journal enregistrées en proposant une vue unique de votre environnement."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a90d9c620221bffbb225fb060b997af2f5e90390
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="a2e1c-103">Créer un tableau de bord personnalisé à utiliser dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a2e1c-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="a2e1c-104">Si votre espace de travail a été mis à niveau pour utiliser le [nouveau langage de requête Log Analytics](log-analytics-log-search-upgrade.md), vous ne pouvez pas créer de nouveaux tableaux de bord ni modifier des tableaux de bord existants.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-104">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="a2e1c-105">Ce guide vous aide à comprendre comment les tableaux de bord Log Analytics permettent d’afficher l’ensemble de vos recherches de journal enregistrées en proposant une vue unique de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.</span></span>

![Exemple de tableau de bord](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="a2e1c-107">Tous les tableaux de bord personnalisés que vous créez dans le portail OMS sont également disponibles dans l’application Mobile OMS.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-107">All the custom dashboards that you create in the OMS portal are also available in the OMS Mobile App.</span></span> <span data-ttu-id="a2e1c-108">Pour plus d’informations sur les applications, voir les pages suivantes.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-108">See the following pages for more information about the apps.</span></span>

* [<span data-ttu-id="a2e1c-109">Application mobile OMS de la Boutique Microsoft </span><span class="sxs-lookup"><span data-stu-id="a2e1c-109">OMS mobile app from the Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="a2e1c-110">Application mobile OMS d’Apple iTunes</span><span class="sxs-lookup"><span data-stu-id="a2e1c-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![Tableau de bord mobile](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="a2e1c-112">Comment créer un tableau de bord ?</span><span class="sxs-lookup"><span data-stu-id="a2e1c-112">How do I create my dashboard?</span></span>
<span data-ttu-id="a2e1c-113">Pour commencer, accédez à la page de présentation d’OMS.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-113">To begin, go to the OMS Overview page.</span></span> <span data-ttu-id="a2e1c-114">La vignette **Mon tableau de bord** s’affiche sur la gauche.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-114">You'll see the **My Dashboard** tile on the left.</span></span> <span data-ttu-id="a2e1c-115">Cliquez dessus pour explorer les détails de votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-115">Click it to drill down into your dashboard.</span></span>

![Vue d'ensemble](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="a2e1c-117">Ajout d'une vignette</span><span class="sxs-lookup"><span data-stu-id="a2e1c-117">Adding a tile</span></span>
<span data-ttu-id="a2e1c-118">Dans les tableaux de bord, les vignettes sont alimentées par vos recherches de journal enregistrées.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="a2e1c-119">OMS propose un grand nombre de recherches enregistrées de journal prédéfinies qui vous permettent de commencer tout de suite.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="a2e1c-120">Suivez les étapes suivantes pour commencer.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-120">Use the following steps that outline how to begin.</span></span>

<span data-ttu-id="a2e1c-121">Dans la vue Mon tableau de bord, cliquez simplement sur **Personnaliser** pour passer en mode de personnalisation.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-121">In the My Dashboard view, simply click **Customize** to enter customize mode.</span></span>

![Représentation graphique](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="a2e1c-123">Le panneau de configuration qui s'ouvre sur le côté droit de la page affiche toutes les recherches de journal enregistrées de votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-123">The panel that opens on the right side of the page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="a2e1c-124">Pour visualiser une recherche de journal enregistrée sous forme de vignette, pointez sur une recherche enregistrée, puis cliquez sur le signe **plus**.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-124">To visualize a saved log search as a tile,  hover over a saved search and then click the **plus** symbol.</span></span>

![Ajout de vignettes 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="a2e1c-126">Lorsque vous cliquez sur le signe **plus**, une nouvelle vignette s’affiche dans la vue Mon tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-126">When you click the **plus** symbol, a new tile appears in the My Dashboard view.</span></span>

![Ajout de vignettes 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="a2e1c-128">Modification d'une vignette</span><span class="sxs-lookup"><span data-stu-id="a2e1c-128">Edit a tile</span></span>
<span data-ttu-id="a2e1c-129">Dans la vue Mon tableau de bord, cliquez simplement sur  **Personnaliser** pour passer en mode de personnalisation.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-129">In the My Dashboard view, simply click  **Customize** to enter customize mode.</span></span> <span data-ttu-id="a2e1c-130">Cliquez sur la vignette que vous voulez modifier.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-130">Click the tile you want to edit.</span></span> <span data-ttu-id="a2e1c-131">Le volet droit devient le volet d'édition, et propose une sélection d'options :</span><span class="sxs-lookup"><span data-stu-id="a2e1c-131">The right panel changes to edit, and gives a selection of options:</span></span>

![Modification d'une vignette](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Modification d'une vignette](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="a2e1c-134">Visualisations de vignettes</span><span class="sxs-lookup"><span data-stu-id="a2e1c-134">Tile visualizations</span></span>
<span data-ttu-id="a2e1c-135">Vous avez le choix entre deux sortes de visualisations de vignettes :</span><span class="sxs-lookup"><span data-stu-id="a2e1c-135">There are three kinds of tile visualizations to choose from:</span></span>

| <span data-ttu-id="a2e1c-136">type de graphique</span><span class="sxs-lookup"><span data-stu-id="a2e1c-136">chart type</span></span> | <span data-ttu-id="a2e1c-137">résultat</span><span class="sxs-lookup"><span data-stu-id="a2e1c-137">what it does</span></span> |
| --- | --- |
| ![Graphique à barres](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="a2e1c-139">Affiche une chronologie des résultats de vos recherches de journal enregistrées sous forme de graphique à barres, ou une liste de résultats en fonction d’un champ, selon que votre recherche de journal regroupe les résultats par champ ou non.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![métrique](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="a2e1c-141">Affiche le nombre total d'accès à vos résultats de recherche de journal sous la forme d'un nombre dans une vignette.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="a2e1c-142">Les vignettes de métrique vous permettent de définir un seuil qui met en surbrillance la vignette lorsque ce seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-142">Metric tiles allow you to set a threshold that will highlight the tile when the threshold is reached.</span></span> |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="a2e1c-144">Affiche une chronologie de vos résultats de recherche journal enregistrés, avec des valeurs représentées sous la forme d’un graphique en courbes.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="a2e1c-145">Seuil</span><span class="sxs-lookup"><span data-stu-id="a2e1c-145">Threshold</span></span>
<span data-ttu-id="a2e1c-146">Vous pouvez créer un seuil sur une vignette à l'aide de la visualisation Métrique.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-146">You can create a threshold on a tile using the Metric visualization.</span></span> <span data-ttu-id="a2e1c-147">Sélectionnez « Activé » pour créer une valeur de seuil sur la vignette.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-147">Select on to create a threshold value on the tile.</span></span> <span data-ttu-id="a2e1c-148">Choisissez si la vignette doit être mise en surbrillance lorsque la valeur est supérieure ou inférieure au seuil sélectionné, puis définissez la valeur de seuil au-dessous.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-148">Choose whether to highlight the tile when the value is over or under the chosen threshold, then set the threshold value below.</span></span>

## <a name="organizing-the-dashboard"></a><span data-ttu-id="a2e1c-149">Organisation du tableau de bord</span><span class="sxs-lookup"><span data-stu-id="a2e1c-149">Organizing the dashboard</span></span>
<span data-ttu-id="a2e1c-150">Pour organiser votre tableau de bord, accédez à la vue Mon tableau de bord, puis cliquez sur **Personnaliser** pour passer en mode de personnalisation.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-150">To organize your dashboard, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="a2e1c-151">Cliquez sur la vignette que vous voulez déplacer et faites-la glisser vers l'emplacement souhaité.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-151">Click and drag the tile you want to move, and move it to where you want your tile to be.</span></span>

![Organisation de votre tableau de bord](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="a2e1c-153">Suppression d'une vignette</span><span class="sxs-lookup"><span data-stu-id="a2e1c-153">Remove a tile</span></span>
<span data-ttu-id="a2e1c-154">Pour supprimer une vignette, accédez à la vue Mon tableau de bord, puis cliquez sur **Personnaliser** pour passer en mode de personnalisation.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-154">To remove a tile, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="a2e1c-155">Sélectionnez la vignette à supprimer, puis dans le volet droit, sélectionnez **Supprimer une vignette**.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-155">Select the tile you want to remove, then on the right panel select **Remove Tile**.</span></span>

![Suppression d'une vignette](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="a2e1c-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a2e1c-157">Next steps</span></span>
* <span data-ttu-id="a2e1c-158">Créez des [alertes](log-analytics-alerts.md) dans Log Analytics pour générer des notifications et corriger les problèmes.</span><span class="sxs-lookup"><span data-stu-id="a2e1c-158">Create [alerts](log-analytics-alerts.md) in Log Analytics to generate notifications and to remediate problems.</span></span>
