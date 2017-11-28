---
title: "aaaCreate un tableau de bord personnalisé dans Azure journal Analytique | Documents Microsoft"
description: "Ce guide vous aide à comprendre comment les tableaux de bord Analytique de journal peuvent de visualiser toutes vos recherches enregistrées de journal, ce qui vous donne un seul objectif tooview votre environnement."
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
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="a520f-103">Créer un tableau de bord personnalisé à utiliser dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a520f-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="a520f-104">Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis vous ne pouvez pas créer de nouveaux tableaux de bord ou modifier des tableaux de bord existants.</span><span class="sxs-lookup"><span data-stu-id="a520f-104">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="a520f-105">Ce guide vous aide à comprendre comment les tableaux de bord Analytique de journal peuvent de visualiser toutes vos recherches enregistrées de journal, ce qui vous donne un seul objectif tooview votre environnement.</span><span class="sxs-lookup"><span data-stu-id="a520f-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens tooview your environment.</span></span>

![Exemple de tableau de bord](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="a520f-107">Tous les hello tableaux de bord personnalisés que vous créez dans le portail OMS de hello est également disponibles dans hello application Mobile OMS.</span><span class="sxs-lookup"><span data-stu-id="a520f-107">All hello custom dashboards that you create in hello OMS portal are also available in hello OMS Mobile App.</span></span> <span data-ttu-id="a520f-108">Consultez hello suivant pages pour plus d’informations sur les applications de hello.</span><span class="sxs-lookup"><span data-stu-id="a520f-108">See hello following pages for more information about hello apps.</span></span>

* [<span data-ttu-id="a520f-109">Application mobile OMS à partir de hello Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="a520f-109">OMS mobile app from hello Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="a520f-110">Application mobile OMS d’Apple iTunes</span><span class="sxs-lookup"><span data-stu-id="a520f-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![Tableau de bord mobile](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="a520f-112">Comment créer un tableau de bord ?</span><span class="sxs-lookup"><span data-stu-id="a520f-112">How do I create my dashboard?</span></span>
<span data-ttu-id="a520f-113">toobegin, page de vue d’ensemble d’OMS toohello accédez.</span><span class="sxs-lookup"><span data-stu-id="a520f-113">toobegin, go toohello OMS Overview page.</span></span> <span data-ttu-id="a520f-114">Vous verrez hello **mon tableau de bord** vignette sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="a520f-114">You'll see hello **My Dashboard** tile on hello left.</span></span> <span data-ttu-id="a520f-115">Cliquez dessus toodrill vers le bas dans votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="a520f-115">Click it toodrill down into your dashboard.</span></span>

![Vue d'ensemble](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="a520f-117">Ajout d'une vignette</span><span class="sxs-lookup"><span data-stu-id="a520f-117">Adding a tile</span></span>
<span data-ttu-id="a520f-118">Dans les tableaux de bord, les vignettes sont alimentées par vos recherches de journal enregistrées.</span><span class="sxs-lookup"><span data-stu-id="a520f-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="a520f-119">OMS propose un grand nombre de recherches enregistrées de journal prédéfinies qui vous permettent de commencer tout de suite.</span><span class="sxs-lookup"><span data-stu-id="a520f-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="a520f-120">Ce plan de la façon dont étapes suivantes de hello utilisation toobegin.</span><span class="sxs-lookup"><span data-stu-id="a520f-120">Use hello following steps that outline how toobegin.</span></span>

<span data-ttu-id="a520f-121">Bonjour mon tableau de bord, cliquez simplement sur **personnaliser** tooenter en mode de personnalisation.</span><span class="sxs-lookup"><span data-stu-id="a520f-121">In hello My Dashboard view, simply click **Customize** tooenter customize mode.</span></span>

![Représentation graphique](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="a520f-123">panneau Hello qui s’ouvre sur le côté droit de hello de page de hello montre toutes les recherches de journal enregistrées de votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="a520f-123">hello panel that opens on hello right side of hello page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="a520f-124">toovisualize recherche d’un journal enregistré sous forme de vignette, placez le curseur sur une recherche enregistrée, puis cliquez sur hello **plus** symbole.</span><span class="sxs-lookup"><span data-stu-id="a520f-124">toovisualize a saved log search as a tile,  hover over a saved search and then click hello **plus** symbol.</span></span>

![Ajout de vignettes 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="a520f-126">Lorsque vous cliquez sur hello **plus** symbol, une nouvelle vignette s’affiche dans hello mon tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="a520f-126">When you click hello **plus** symbol, a new tile appears in hello My Dashboard view.</span></span>

![Ajout de vignettes 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="a520f-128">Modification d'une vignette</span><span class="sxs-lookup"><span data-stu-id="a520f-128">Edit a tile</span></span>
<span data-ttu-id="a520f-129">Bonjour mon tableau de bord, cliquez simplement sur **personnaliser** tooenter en mode de personnalisation.</span><span class="sxs-lookup"><span data-stu-id="a520f-129">In hello My Dashboard view, simply click  **Customize** tooenter customize mode.</span></span> <span data-ttu-id="a520f-130">Cliquez sur vignette hello tooedit.</span><span class="sxs-lookup"><span data-stu-id="a520f-130">Click hello tile you want tooedit.</span></span> <span data-ttu-id="a520f-131">le panneau droit Hello modifie tooedit et propose diverses options :</span><span class="sxs-lookup"><span data-stu-id="a520f-131">hello right panel changes tooedit, and gives a selection of options:</span></span>

![Modification d'une vignette](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Modification d'une vignette](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="a520f-134">Visualisations de vignettes</span><span class="sxs-lookup"><span data-stu-id="a520f-134">Tile visualizations</span></span>
<span data-ttu-id="a520f-135">Il existe trois types de toochoose de visualisations de vignette à partir de :</span><span class="sxs-lookup"><span data-stu-id="a520f-135">There are three kinds of tile visualizations toochoose from:</span></span>

| <span data-ttu-id="a520f-136">type de graphique</span><span class="sxs-lookup"><span data-stu-id="a520f-136">chart type</span></span> | <span data-ttu-id="a520f-137">résultat</span><span class="sxs-lookup"><span data-stu-id="a520f-137">what it does</span></span> |
| --- | --- |
| ![Graphique à barres](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="a520f-139">Affiche une chronologie des résultats de vos recherches de journal enregistrées sous forme de graphique à barres, ou une liste de résultats en fonction d’un champ, selon que votre recherche de journal regroupe les résultats par champ ou non.</span><span class="sxs-lookup"><span data-stu-id="a520f-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![métrique](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="a520f-141">Affiche le nombre total d'accès à vos résultats de recherche de journal sous la forme d'un nombre dans une vignette.</span><span class="sxs-lookup"><span data-stu-id="a520f-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="a520f-142">Vignettes de métrique vous permettent de tooset un seuil qui met en surbrillance la vignette de hello lorsque hello seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="a520f-142">Metric tiles allow you tooset a threshold that will highlight hello tile when hello threshold is reached.</span></span> |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="a520f-144">Affiche une chronologie de vos résultats de recherche journal enregistrés, avec des valeurs représentées sous la forme d’un graphique en courbes.</span><span class="sxs-lookup"><span data-stu-id="a520f-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="a520f-145">Seuil</span><span class="sxs-lookup"><span data-stu-id="a520f-145">Threshold</span></span>
<span data-ttu-id="a520f-146">Vous pouvez créer un seuil sur une vignette à l’aide de la visualisation métrique de hello.</span><span class="sxs-lookup"><span data-stu-id="a520f-146">You can create a threshold on a tile using hello Metric visualization.</span></span> <span data-ttu-id="a520f-147">Sélectionnez une valeur de seuil sur la vignette de hello sur toocreate.</span><span class="sxs-lookup"><span data-stu-id="a520f-147">Select on toocreate a threshold value on hello tile.</span></span> <span data-ttu-id="a520f-148">Choisissez si vignette de hello toohighlight lorsque la valeur de hello est supérieure ou inférieure hello choisi seuil, puis valeur hello seuil ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a520f-148">Choose whether toohighlight hello tile when hello value is over or under hello chosen threshold, then set hello threshold value below.</span></span>

## <a name="organizing-hello-dashboard"></a><span data-ttu-id="a520f-149">Organisation hello le tableau de bord</span><span class="sxs-lookup"><span data-stu-id="a520f-149">Organizing hello dashboard</span></span>
<span data-ttu-id="a520f-150">tooorganize votre tableau de bord, naviguer dans Affichage de mon tableau de bord toohello et cliquez sur **personnaliser** tooenter en mode de personnalisation.</span><span class="sxs-lookup"><span data-stu-id="a520f-150">tooorganize your dashboard, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="a520f-151">Cliquez et faites glisser vignette hello souhaité toomove, déplacez-le toowhere vous souhaitez que votre toobe de vignette.</span><span class="sxs-lookup"><span data-stu-id="a520f-151">Click and drag hello tile you want toomove, and move it toowhere you want your tile toobe.</span></span>

![Organisation de votre tableau de bord](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="a520f-153">Suppression d'une vignette</span><span class="sxs-lookup"><span data-stu-id="a520f-153">Remove a tile</span></span>
<span data-ttu-id="a520f-154">tooremove une vignette, accédez vue mon tableau de bord de toohello et cliquez sur **personnaliser** tooenter en mode de personnalisation.</span><span class="sxs-lookup"><span data-stu-id="a520f-154">tooremove a tile, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="a520f-155">Vignette hello sélectionnez vous souhaitez tooremove, puis sur Panneau de droite hello **supprimer une vignette**.</span><span class="sxs-lookup"><span data-stu-id="a520f-155">Select hello tile you want tooremove, then on hello right panel select **Remove Tile**.</span></span>

![Suppression d'une vignette](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="a520f-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a520f-157">Next steps</span></span>
* <span data-ttu-id="a520f-158">Créer [alertes](log-analytics-alerts.md) dans les notifications toogenerate Analytique de journal et des problèmes de tooremediate.</span><span class="sxs-lookup"><span data-stu-id="a520f-158">Create [alerts](log-analytics-alerts.md) in Log Analytics toogenerate notifications and tooremediate problems.</span></span>
