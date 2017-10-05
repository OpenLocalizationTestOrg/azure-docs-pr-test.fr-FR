---
title: "Surveiller et gérer les pipelines de données - Azure | Microsoft Docs"
description: "Découvrez comment utiliser l’application de surveillance et gestion pour surveiller et gérer les fabriques de données et les pipelines Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: d5a2d1f3d85b8a2212326cfcfd0ba5d80356b769
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-monitoring-and-management-app"></a><span data-ttu-id="d5446-103">Surveiller et gérer les pipelines Azure Data Factory à l’aide de l’application de surveillance et gestion</span><span class="sxs-lookup"><span data-stu-id="d5446-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5446-104">Utilisation du portail Azure/d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5446-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="d5446-105">Utilisation de l’application de surveillance et gestion</span><span class="sxs-lookup"><span data-stu-id="d5446-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="d5446-106">Cet article explique comment utiliser l’application de surveillance et gestion pour surveiller, gérer et déboguer vos pipelines Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d5446-106">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="d5446-107">Vous obtiendrez également des informations sur la façon de créer des alertes pour être averti en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="d5446-107">It also provides information on how to create alerts to get notified on failures.</span></span> <span data-ttu-id="d5446-108">Vous pouvez commencer à utiliser l’application en regardant la vidéo suivante :</span><span class="sxs-lookup"><span data-stu-id="d5446-108">You can get started with using the application by watching the following video:</span></span>

> [!NOTE]
> <span data-ttu-id="d5446-109">L’interface utilisateur présentée dans la vidéo ne correspondra peut-être pas exactement à ce que vous voyez dans le portail.</span><span class="sxs-lookup"><span data-stu-id="d5446-109">The user interface shown in the video may not exactly match what you see in the portal.</span></span> <span data-ttu-id="d5446-110">Elle est un peu plus ancienne, mais les concepts restent les mêmes.</span><span class="sxs-lookup"><span data-stu-id="d5446-110">It's slightly older, but concepts remain the same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-the-monitoring-and-management-app"></a><span data-ttu-id="d5446-111">Lancement de l’application de surveillance et gestion</span><span class="sxs-lookup"><span data-stu-id="d5446-111">Launch the Monitoring and Management app</span></span>
<span data-ttu-id="d5446-112">Pour lancer l’application de surveillance et gestion, cliquez sur la vignette **Surveiller et gérer** dans le panneau **Data Factory** de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d5446-112">To launch the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span></span>

![Mosaïque Surveillance sur la page d’accueil de Data Factory](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="d5446-114">L’application de surveillance et gestion devrait s’ouvrir dans une nouvelle fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d5446-114">You should see the Monitoring and Management app open in a separate window.</span></span>  

![Application de surveillance et gestion](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="d5446-116">Si vous voyez que le navigateur web est bloqué au niveau « Autorisation ... », désactivez la case à cocher **Bloquer les cookies et les données de site tiers** ou laissez cette option sélectionnée, créez une exception pour **login.microsoftonline.com**, puis réessayez d’ouvrir l’application.</span><span class="sxs-lookup"><span data-stu-id="d5446-116">If you see that the web browser is stuck at "Authorizing...", clear the **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try to open the app again.</span></span>


<span data-ttu-id="d5446-117">Dans la liste Activity Windows (Fenêtres d’activité), dans le volet central, vous pouvez voir une fenêtre d’activité pour chaque exécution d’une activité.</span><span class="sxs-lookup"><span data-stu-id="d5446-117">In the Activity Windows list in the middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="d5446-118">Par exemple, si l’activité est planifiée pour s’exécuter toutes les heures pendant cinq heures, vous voyez cinq fenêtres d’activité associées à cinq tranches de données.</span><span class="sxs-lookup"><span data-stu-id="d5446-118">For example, if you have the activity scheduled to run hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="d5446-119">Si vous ne voyez pas de fenêtre d’activité dans la liste du bas, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d5446-119">If you don't see activity windows in the list at the bottom, do the following:</span></span>
 
- <span data-ttu-id="d5446-120">Mettez à jour les filtres **Heure de départ** et **Heure de fin** en haut de la fenêtre pour adapter les heures de départ et de fin de votre pipeline, puis cliquez sur le bouton **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="d5446-120">Update the **start time** and **end time** filters at the top to match the start and end times of your pipeline, and then click the **Apply** button.</span></span>  
- <span data-ttu-id="d5446-121">La liste Activity Windows (Fenêtres d’activité) n’est pas actualisée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d5446-121">The Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="d5446-122">Cliquez sur le bouton **Actualiser** dans la barre d’outils de la liste **Activity Windows** (Fenêtres d’activité).</span><span class="sxs-lookup"><span data-stu-id="d5446-122">Click the **Refresh** button on the toolbar in the **Activity Windows** list.</span></span>  

<span data-ttu-id="d5446-123">Si vous ne disposez pas d’une application de fabrique de données pour tester ces étapes, suivez ce didacticiel : [Copie de données de Stockage Blob vers SQL Database à l’aide de Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d5446-123">If you don't have a Data Factory application to test these steps with, do the tutorial: [copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-the-monitoring-and-management-app"></a><span data-ttu-id="d5446-124">Présentation de l’application de surveillance et gestion</span><span class="sxs-lookup"><span data-stu-id="d5446-124">Understand the Monitoring and Management app</span></span>
<span data-ttu-id="d5446-125">Trois onglets sont disponibles sur le côté gauche : **Explorateur de ressources**, **Vues de surveillance** et **Alertes**.</span><span class="sxs-lookup"><span data-stu-id="d5446-125">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="d5446-126">Le premier onglet (**Explorateur de ressources**) est sélectionné par défaut.</span><span class="sxs-lookup"><span data-stu-id="d5446-126">The first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="d5446-127">Explorateur de ressources</span><span class="sxs-lookup"><span data-stu-id="d5446-127">Resource Explorer</span></span>
<span data-ttu-id="d5446-128">Vous voyez l'affichage suivant :</span><span class="sxs-lookup"><span data-stu-id="d5446-128">You see the following:</span></span>

* <span data-ttu-id="d5446-129">L’**arborescence** de l’Explorateur de ressources dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="d5446-129">The Resource Explorer **tree view** in the left pane.</span></span>
* <span data-ttu-id="d5446-130">Le **vue schématique** en haut du volet central.</span><span class="sxs-lookup"><span data-stu-id="d5446-130">The **Diagram View** at the top in the middle pane.</span></span>
* <span data-ttu-id="d5446-131">La liste d’**activités Windows** en bas du volet central.</span><span class="sxs-lookup"><span data-stu-id="d5446-131">The **Activity Windows** list at the bottom in the middle pane.</span></span>
* <span data-ttu-id="d5446-132">Les onglets **Propriétés**, **Explorateur de fenêtres d’activités** et **Script** dans le volet de droite.</span><span class="sxs-lookup"><span data-stu-id="d5446-132">The **Properties**, **Activity Window Explorer**, and **Script** tabs in the right pane.</span></span>

<span data-ttu-id="d5446-133">Dans l’explorateur de ressources, vous pouvez voir toutes les ressources (pipelines, groupes de données, services liés) organisées en arborescence dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d5446-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span></span> <span data-ttu-id="d5446-134">Lorsque vous sélectionnez un objet dans l’Explorateur de ressources :</span><span class="sxs-lookup"><span data-stu-id="d5446-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="d5446-135">L’entité Data Factory associée est mise en surbrillance dans la vue schématique.</span><span class="sxs-lookup"><span data-stu-id="d5446-135">The associated Data Factory entity is highlighted in the Diagram View.</span></span>
* <span data-ttu-id="d5446-136">Les [fenêtres d’activité associées](data-factory-scheduling-and-execution.md) sont mises en évidence dans la liste des fenêtres d’activité en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="d5446-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span></span>  
* <span data-ttu-id="d5446-137">Les propriétés de l’objet sélectionné s’affichent dans la fenêtre Propriétés du volet droit.</span><span class="sxs-lookup"><span data-stu-id="d5446-137">The properties of the selected object are shown in the Properties window in the right pane.</span></span>
* <span data-ttu-id="d5446-138">La définition JSON de l’objet sélectionné apparaît, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="d5446-138">The JSON definition of the selected object is shown, if applicable.</span></span> <span data-ttu-id="d5446-139">Par exemple : un service lié, un jeu de données ou un pipeline.</span><span class="sxs-lookup"><span data-stu-id="d5446-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Explorateur de ressources](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="d5446-141">Consultez l’article [Planification et exécution](data-factory-scheduling-and-execution.md) pour obtenir des informations conceptuelles détaillées sur les fenêtres d’activité.</span><span class="sxs-lookup"><span data-stu-id="d5446-141">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="d5446-142">Vue schématique</span><span class="sxs-lookup"><span data-stu-id="d5446-142">Diagram View</span></span>
<span data-ttu-id="d5446-143">La vue schématique d'une fabrique de données est un point unique de surveillance et de gestion d’une fabrique de données et de ses ressources.</span><span class="sxs-lookup"><span data-stu-id="d5446-143">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span></span> <span data-ttu-id="d5446-144">Lorsque vous sélectionnez une entité Data Factory (jeu de données/pipeline) dans la vue schématique :</span><span class="sxs-lookup"><span data-stu-id="d5446-144">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span></span>

* <span data-ttu-id="d5446-145">L’entité Data Factory est sélectionnée dans l’arborescence.</span><span class="sxs-lookup"><span data-stu-id="d5446-145">The data factory entity is selected in the tree view.</span></span>
* <span data-ttu-id="d5446-146">Les fenêtres d’activité associées sont mises en surbrillance dans la liste des fenêtres d’activité.</span><span class="sxs-lookup"><span data-stu-id="d5446-146">The associated activity windows are highlighted in the Activity Windows list.</span></span>
* <span data-ttu-id="d5446-147">Les propriétés de l’objet sélectionné s’affichent dans la fenêtre Propriétés.</span><span class="sxs-lookup"><span data-stu-id="d5446-147">The properties of the selected object are shown in the Properties window.</span></span>

<span data-ttu-id="d5446-148">Lorsque le pipeline est activé (il n’est alors pas en pause), la barre de sa mosaïque est verte :</span><span class="sxs-lookup"><span data-stu-id="d5446-148">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Pipeline en cours d’exécution](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="d5446-150">Vous pouvez suspendre, reprendre ou arrêter un pipeline en le sélectionnant dans la vue schématique et en utilisant les boutons de la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="d5446-150">You can pause, resume, or terminate a pipeline by selecting it in the diagram view and using the buttons on the command bar.</span></span>

![Mettre en pause/relancer depuis la barre de commandes](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="d5446-152">La vue schématique comporte trois boutons de barre de commandes dédiés au pipeline.</span><span class="sxs-lookup"><span data-stu-id="d5446-152">There are three command bar buttons for the pipeline in the Diagram View.</span></span> <span data-ttu-id="d5446-153">Vous pouvez utiliser le deuxième bouton pour mettre en pause le pipeline.</span><span class="sxs-lookup"><span data-stu-id="d5446-153">You can use the second button to pause the pipeline.</span></span> <span data-ttu-id="d5446-154">La mise en pause n’interrompt pas les activités en cours et les laisse se terminer.</span><span class="sxs-lookup"><span data-stu-id="d5446-154">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span></span> <span data-ttu-id="d5446-155">Le troisième bouton permet de mettre en pause le pipeline et d’interrompre ses activités en cours.</span><span class="sxs-lookup"><span data-stu-id="d5446-155">The third button pauses the pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="d5446-156">Le premier bouton permet de relancer le pipeline.</span><span class="sxs-lookup"><span data-stu-id="d5446-156">The first button resumes the pipeline.</span></span> <span data-ttu-id="d5446-157">Lorsque votre pipeline est suspendu, il change de couleur.</span><span class="sxs-lookup"><span data-stu-id="d5446-157">When your pipeline is paused, the color of the pipeline changes.</span></span> <span data-ttu-id="d5446-158">Par exemple, un pipeline suspendu se présente comme illustré ci-après :</span><span class="sxs-lookup"><span data-stu-id="d5446-158">For example, a paused pipeline looks like in the following image:</span></span> 

![Pipeline suspendu](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="d5446-160">Vous pouvez sélectionner deux pipelines ou plus en maintenant la touche Ctrl enfoncée.</span><span class="sxs-lookup"><span data-stu-id="d5446-160">You can multi-select two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="d5446-161">Pour mettre en pause/relancer plusieurs pipelines simultanément, utilisez les boutons de la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="d5446-161">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="d5446-162">Vous pouvez également cliquer sur un pipeline avec le bouton droit et sélectionner les options appropriées pour le suspendre, le reprendre ou l’arrêter.</span><span class="sxs-lookup"><span data-stu-id="d5446-162">You can also right-click a pipeline and select options to suspend, resume, or terminate a pipeline.</span></span> 

![Menu contextuel pour un pipeline](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="d5446-164">Cliquez sur l’option **Ouvrir le pipeline** pour afficher toutes les activités dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="d5446-164">Click the **Open pipeline** option to see all the activities in the pipeline.</span></span> 

![Menu Ouvrir un pipeline](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="d5446-166">Dans la vue du pipeline ouvert, vous voyez toutes les activités dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="d5446-166">In the opened pipeline view, you see all activities in the pipeline.</span></span> <span data-ttu-id="d5446-167">Dans cet exemple, le pipeline ne contient qu’une seule activité : une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d5446-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Pipeline ouvert](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="d5446-169">Pour revenir à la vue précédente, cliquez sur le nom de la fabrique de données dans le menu de navigation en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="d5446-169">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span></span>

<span data-ttu-id="d5446-170">Dans la vue du pipeline, lorsque vous sélectionnez un jeu de données de sortie ou que vous le survolez avec la souris, la fenêtre contextuelle d’activité correspondante s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d5446-170">In the pipeline view, when you select an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span></span>

![Fenêtre contextuelle d’activité Windows](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="d5446-172">Vous pouvez cliquer sur une fenêtre d’activité pour afficher ses détails dans la fenêtre **Propriétés** du volet droit.</span><span class="sxs-lookup"><span data-stu-id="d5446-172">You can click an activity window to see details for it in the **Properties** window in the right pane.</span></span>

![Propriétés des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="d5446-174">Dans le volet droit, affichez l’onglet **Explorateur de fenêtres d’activité** pour afficher plus de détails.</span><span class="sxs-lookup"><span data-stu-id="d5446-174">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span></span>

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="d5446-176">Vous voyez également les **variables résolues** pour chaque tentative d’exécution d’une activité dans la section **Tentatives**.</span><span class="sxs-lookup"><span data-stu-id="d5446-176">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span></span>

![Variables résolues](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="d5446-178">Affichez l’onglet **Script** pour afficher la définition du script JSON pour l’objet sélectionné.</span><span class="sxs-lookup"><span data-stu-id="d5446-178">Switch to the **Script** tab to see the JSON script definition for the selected object.</span></span>   

![Onglet Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="d5446-180">Les fenêtres d’activité s’affichent à trois emplacements différents :</span><span class="sxs-lookup"><span data-stu-id="d5446-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="d5446-181">La fenêtre contextuelle d’activité dans la vue schématique (volet central).</span><span class="sxs-lookup"><span data-stu-id="d5446-181">The Activity Windows pop-up in the Diagram View (middle pane).</span></span>
* <span data-ttu-id="d5446-182">L’Explorateur de fenêtres d’activité dans le volet droit.</span><span class="sxs-lookup"><span data-stu-id="d5446-182">The Activity Window Explorer in the right pane.</span></span>
* <span data-ttu-id="d5446-183">La liste des fenêtres d’activité dans le volet inférieur.</span><span class="sxs-lookup"><span data-stu-id="d5446-183">The Activity Windows list in the bottom pane.</span></span>

<span data-ttu-id="d5446-184">Dans la fenêtre contextuelle et l’Explorateur de fenêtres d’activité, vous pouvez passer à la semaine précédente ou suivante à l’aide des flèches gauche et droite.</span><span class="sxs-lookup"><span data-stu-id="d5446-184">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span></span>

![Flèches gauche/droite de l’Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="d5446-186">En bas de la vue schématique, vous trouverez des boutons pour effectuer un zoom avant ou arrière, zoomer pour ajuster, effectuer un Zoom à 100 % et verrouiller la disposition.</span><span class="sxs-lookup"><span data-stu-id="d5446-186">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="d5446-187">Le bouton **Verrouiller la disposition** vous empêche de déplacer accidentellement des tables et des pipelines dans la vue schématique.</span><span class="sxs-lookup"><span data-stu-id="d5446-187">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span></span> <span data-ttu-id="d5446-188">L’option est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="d5446-188">It's on by default.</span></span> <span data-ttu-id="d5446-189">Vous pouvez la désactiver et déplacer des entités dans la vue schématique.</span><span class="sxs-lookup"><span data-stu-id="d5446-189">You can turn it off and move entities around in the diagram.</span></span> <span data-ttu-id="d5446-190">Lorsque vous la désactivez, vous pouvez utiliser le dernier bouton pour positionner automatiquement les tables et les pipelines.</span><span class="sxs-lookup"><span data-stu-id="d5446-190">When you turn it off, you can use the last button to automatically position tables and pipelines.</span></span> <span data-ttu-id="d5446-191">Vous pouvez également effectuer des zooms avant et arrière à l’aide de la roulette de la souris.</span><span class="sxs-lookup"><span data-stu-id="d5446-191">You can also zoom in or out by using the mouse wheel.</span></span>

![Commandes de zoom de la vue schématique](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="d5446-193">Liste des fenêtres d’activité</span><span class="sxs-lookup"><span data-stu-id="d5446-193">Activity Windows list</span></span>
<span data-ttu-id="d5446-194">La liste des fenêtres d’activité dans la partie inférieure du volet central affiche toutes les fenêtres d’activité du jeu de données que vous avez sélectionné dans l’Explorateur de ressources ou la vue schématique.</span><span class="sxs-lookup"><span data-stu-id="d5446-194">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span></span> <span data-ttu-id="d5446-195">Par défaut, la liste est en ordre décroissant, ce qui signifie que la fenêtre d’activité la plus récente s’affiche en premier.</span><span class="sxs-lookup"><span data-stu-id="d5446-195">By default, the list is in descending order, which means that you see the latest activity window at the top.</span></span>

![Liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="d5446-197">Cette liste ne s’actualise pas automatiquement. Pour l’actualiser manuellement, utilisez le bouton d’actualisation de la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="d5446-197">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span></span>  

<span data-ttu-id="d5446-198">Les fenêtres d’activité peuvent avoir l’un des statuts suivants :</span><span class="sxs-lookup"><span data-stu-id="d5446-198">Activity windows can be in one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="d5446-199">État</span><span class="sxs-lookup"><span data-stu-id="d5446-199">Status</span></span></th><th align="left"><span data-ttu-id="d5446-200">État secondaire</span><span class="sxs-lookup"><span data-stu-id="d5446-200">Substatus</span></span></th><th align="left"><span data-ttu-id="d5446-201">Description</span><span class="sxs-lookup"><span data-stu-id="d5446-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="d5446-202">En attente</span><span class="sxs-lookup"><span data-stu-id="d5446-202">Waiting</span></span></td><td><span data-ttu-id="d5446-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="d5446-203">ScheduleTime</span></span></td><td><span data-ttu-id="d5446-204">L’heure d’exécution de la fenêtre d’activité n’est pas encore venue.</span><span class="sxs-lookup"><span data-stu-id="d5446-204">The time hasn't come for the activity window to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5446-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="d5446-205">DatasetDependencies</span></span></td><td><span data-ttu-id="d5446-206">Les dépendances en amont ne sont pas prêtes.</span><span class="sxs-lookup"><span data-stu-id="d5446-206">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5446-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="d5446-207">ComputeResources</span></span></td><td><span data-ttu-id="d5446-208">Les ressources de calcul ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="d5446-208">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5446-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="d5446-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="d5446-210">Toutes les instances d’activité sont occupées par l’exécution d’autres fenêtres d’activité.</span><span class="sxs-lookup"><span data-stu-id="d5446-210">All the activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5446-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="d5446-211">ActivityResume</span></span></td><td><span data-ttu-id="d5446-212">L’activité est mise en pause et ne peut pas exécuter les fenêtres d’activité jusqu’à sa reprise.</span><span class="sxs-lookup"><span data-stu-id="d5446-212">The activity is paused and can't run the activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5446-213">Retry</span><span class="sxs-lookup"><span data-stu-id="d5446-213">Retry</span></span></td><td><span data-ttu-id="d5446-214">L’exécution de l’activité est retentée.</span><span class="sxs-lookup"><span data-stu-id="d5446-214">The activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5446-215">Validation</span><span class="sxs-lookup"><span data-stu-id="d5446-215">Validation</span></span></td><td><span data-ttu-id="d5446-216">La validation n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="d5446-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5446-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="d5446-217">ValidationRetry</span></span></td><td><span data-ttu-id="d5446-218">Une nouvelle tentative de validation va avoir lieu.</span><span class="sxs-lookup"><span data-stu-id="d5446-218">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="d5446-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="d5446-219">InProgress</span></span></td><td><span data-ttu-id="d5446-220">Validation</span><span class="sxs-lookup"><span data-stu-id="d5446-220">Validating</span></span></td><td><span data-ttu-id="d5446-221">La validation est en cours.</span><span class="sxs-lookup"><span data-stu-id="d5446-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="d5446-222">La fenêtre d’activité est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="d5446-222">The activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="d5446-223">Échec</span><span class="sxs-lookup"><span data-stu-id="d5446-223">Failed</span></span></td><td><span data-ttu-id="d5446-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="d5446-224">TimedOut</span></span></td><td><span data-ttu-id="d5446-225">L'exécution de l’activité a pris plus de temps que l’activité ne l’autorise.</span><span class="sxs-lookup"><span data-stu-id="d5446-225">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5446-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="d5446-226">Canceled</span></span></td><td><span data-ttu-id="d5446-227">La fenêtre d’activité a été annulée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5446-227">The activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5446-228">Validation</span><span class="sxs-lookup"><span data-stu-id="d5446-228">Validation</span></span></td><td><span data-ttu-id="d5446-229">La validation a échoué.</span><span class="sxs-lookup"><span data-stu-id="d5446-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="d5446-230">La génération ou la validation de la fenêtre d’activité ont échoué.</span><span class="sxs-lookup"><span data-stu-id="d5446-230">The activity window failed to be generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="d5446-231">Ready</span><span class="sxs-lookup"><span data-stu-id="d5446-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="d5446-232">La fenêtre d’activité est prête à être consommée.</span><span class="sxs-lookup"><span data-stu-id="d5446-232">The activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5446-233">Ignoré</span><span class="sxs-lookup"><span data-stu-id="d5446-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="d5446-234">La fenêtre d’activité n’a pas été traitée.</span><span class="sxs-lookup"><span data-stu-id="d5446-234">The activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5446-235">Aucun</span><span class="sxs-lookup"><span data-stu-id="d5446-235">None</span></span></td><td>-</td><td><span data-ttu-id="d5446-236">Fenêtre d’activité qui a été réinitialisée alors qu’elle existait avec un statut différent.</span><span class="sxs-lookup"><span data-stu-id="d5446-236">An activity window used to exist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="d5446-237">Quand vous cliquez sur une fenêtre d’activité dans la liste, les détails la concernant s’affichent dans **l’Explorateur de fenêtres d’activité** ou dans la fenêtre **Propriétés** sur la droite.</span><span class="sxs-lookup"><span data-stu-id="d5446-237">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span></span>

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="d5446-239">Actualiser les fenêtres d’activité</span><span class="sxs-lookup"><span data-stu-id="d5446-239">Refresh activity windows</span></span>
<span data-ttu-id="d5446-240">Les détails ne sont pas automatiquement actualisés. Pour actualiser manuellement la liste des fenêtres d’activité, utilisez le bouton Actualiser (le deuxième) dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="d5446-240">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="d5446-241">Fenêtre Propriétés</span><span class="sxs-lookup"><span data-stu-id="d5446-241">Properties window</span></span>
<span data-ttu-id="d5446-242">La fenêtre Propriétés se trouve dans le volet situé tout à droite de l’application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="d5446-242">The Properties window is in the right-most pane of the Monitoring and Management app.</span></span>

![Fenêtre Propriétés](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="d5446-244">Elle affiche les propriétés de l’élément que vous avez sélectionné dans l’Explorateur de ressources (arborescence), la vue schématique ou la liste des fenêtres d’activité.</span><span class="sxs-lookup"><span data-stu-id="d5446-244">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="d5446-245">Explorateur de fenêtres d’activité</span><span class="sxs-lookup"><span data-stu-id="d5446-245">Activity Window Explorer</span></span>
<span data-ttu-id="d5446-246">L**’Explorateur de fenêtres d’activité** se trouve dans le volet situé tout à droite de l’application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="d5446-246">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span></span> <span data-ttu-id="d5446-247">Il affiche des détails sur la fenêtre d’activité que vous avez sélectionnée dans la fenêtre contextuelle ou la liste des fenêtres d’activité.</span><span class="sxs-lookup"><span data-stu-id="d5446-247">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span></span>

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="d5446-249">Vous pouvez passer à une autre fenêtre d’activité en cliquant dessus dans la vue calendaire en haut de l’écran.</span><span class="sxs-lookup"><span data-stu-id="d5446-249">You can switch to another activity window by clicking it in the calendar view at the top.</span></span> <span data-ttu-id="d5446-250">Vous pouvez également utiliser les boutons flèche gauche/flèche droite en haut de l’écran pour afficher les fenêtres d’activité de la semaine précédente ou suivante.</span><span class="sxs-lookup"><span data-stu-id="d5446-250">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span></span>

<span data-ttu-id="d5446-251">Vous pouvez utiliser les boutons de la barre d’outils dans le volet inférieur pour réexécuter la fenêtre d’activité ou actualiser les détails affichés dans le volet.</span><span class="sxs-lookup"><span data-stu-id="d5446-251">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span></span>

### <a name="script"></a><span data-ttu-id="d5446-252">Script</span><span class="sxs-lookup"><span data-stu-id="d5446-252">Script</span></span>
<span data-ttu-id="d5446-253">Vous pouvez utiliser l’onglet **Script** pour afficher la définition JSON de l’entité Data Factory sélectionnée (service lié, jeu de données et pipeline).</span><span class="sxs-lookup"><span data-stu-id="d5446-253">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Onglet Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="d5446-255">Utiliser les vues système</span><span class="sxs-lookup"><span data-stu-id="d5446-255">Use system views</span></span>
<span data-ttu-id="d5446-256">L’application de surveillance et gestion inclut des vues système intégrées (**Fenêtres d’activité récentes**, **Fenêtres d’activité ayant échoué**, **Fenêtres d’activité en cours**), qui vous permettent d’afficher les fenêtres d’activité (récentes, ayant échoué et en cours) de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d5446-256">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="d5446-257">Affichez l’onglet **Vues de surveillance** sur la gauche en cliquant dessus.</span><span class="sxs-lookup"><span data-stu-id="d5446-257">Switch to the **Monitoring Views** tab on the left by clicking it.</span></span>

![Onglet Vues de surveillance](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="d5446-259">Actuellement, trois vues système sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="d5446-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="d5446-260">Sélectionnez une option pour afficher les fenêtres d’activité récentes, ayant échoué, ou en cours dans la liste des fenêtres d’activité (en bas du volet central).</span><span class="sxs-lookup"><span data-stu-id="d5446-260">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span></span>

<span data-ttu-id="d5446-261">Quand vous sélectionnez l’option **Fenêtres d’activité récentes**, toutes les fenêtres d’activité récentes s’affichent dans l’ordre décroissant en fonction de **l’heure de la dernière tentative**.</span><span class="sxs-lookup"><span data-stu-id="d5446-261">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span></span>

<span data-ttu-id="d5446-262">Vous pouvez utiliser la vue **Fenêtres d’activité ayant échoué** pour afficher toutes les fenêtres d’activité de la liste qui ont échoué.</span><span class="sxs-lookup"><span data-stu-id="d5446-262">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span></span> <span data-ttu-id="d5446-263">Dans la liste, sélectionnez une fenêtre d’activité ayant échoué pour afficher les détails la concernant dans la fenêtre **Propriétés** ou dans **l’Explorateur de fenêtres d’activité**.</span><span class="sxs-lookup"><span data-stu-id="d5446-263">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span></span> <span data-ttu-id="d5446-264">Vous pouvez également télécharger tous les journaux d’une fenêtre d’activité ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="d5446-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="d5446-265">Trier et filtrer les fenêtres d’activité</span><span class="sxs-lookup"><span data-stu-id="d5446-265">Sort and filter activity windows</span></span>
<span data-ttu-id="d5446-266">Pour filtrer les fenêtres d’activité, modifiez les paramètres **d’heure de début** et **d’heure de fin** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="d5446-266">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span></span> <span data-ttu-id="d5446-267">Après avoir modifié les heures de début et de fin, cliquez sur le bouton en regard de l’heure de fin pour actualiser la liste des fenêtres d’activité.</span><span class="sxs-lookup"><span data-stu-id="d5446-267">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span></span>

![Heures de début et de fin](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="d5446-269">Pour l’instant, toutes les heures de l’application de surveillance et gestion sont au format UTC.</span><span class="sxs-lookup"><span data-stu-id="d5446-269">Currently, all times are in UTC format in the Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="d5446-270">Dans la **liste des fenêtres d’activité**, cliquez sur le nom d’une colonne (par exemple, Statut).</span><span class="sxs-lookup"><span data-stu-id="d5446-270">In the **Activity Windows list**, click the name of a column (for example: Status).</span></span>

![Menu déroulant de la liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="d5446-272">Vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d5446-272">You can do the following:</span></span>

* <span data-ttu-id="d5446-273">Trier dans l’ordre croissant.</span><span class="sxs-lookup"><span data-stu-id="d5446-273">Sort in ascending order.</span></span>
* <span data-ttu-id="d5446-274">Trier dans l’ordre décroissant.</span><span class="sxs-lookup"><span data-stu-id="d5446-274">Sort in descending order.</span></span>
* <span data-ttu-id="d5446-275">Filtrer selon une ou plusieurs valeurs (Prêt, En attente, etc.).</span><span class="sxs-lookup"><span data-stu-id="d5446-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="d5446-276">Lorsque vous spécifiez un filtre sur une colonne, vous voyez que le bouton de filtrage est activé pour cette colonne afin d’indiquer que les valeurs filtrées sont celles de cette colonne.</span><span class="sxs-lookup"><span data-stu-id="d5446-276">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span></span>

![Filtrer sur une colonne de la liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="d5446-278">Vous pouvez utiliser la même fenêtre contextuelle pour effacer les filtres.</span><span class="sxs-lookup"><span data-stu-id="d5446-278">You can use the same pop-up window to clear filters.</span></span> <span data-ttu-id="d5446-279">Pour effacer tous les filtres de la liste des fenêtres d’activité, cliquez sur le bouton Effacer le filtre dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="d5446-279">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span></span>

![Effacer tous les filtres de la liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="d5446-281">Exécuter des opérations de traitement par lot</span><span class="sxs-lookup"><span data-stu-id="d5446-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="d5446-282">Réexécuter les fenêtres d’activité sélectionnées</span><span class="sxs-lookup"><span data-stu-id="d5446-282">Rerun selected activity windows</span></span>
<span data-ttu-id="d5446-283">Sélectionnez une fenêtre d’activité, cliquez sur la flèche vers le bas du premier bouton de la barre de commandes et sélectionnez **Réexécuter** / **Réexécuter avec les fenêtres en amont dans le pipeline**.</span><span class="sxs-lookup"><span data-stu-id="d5446-283">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="d5446-284">L’option **Réexécuter avec les fenêtres en amont dans le pipeline** permet de réexécuter également toutes les fenêtres d’activité en amont.</span><span class="sxs-lookup"><span data-stu-id="d5446-284">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="d5446-285">![Réexécuter une fenêtre d’activité](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="d5446-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="d5446-286">Vous pouvez également sélectionner plusieurs fenêtres d’activité dans la liste et les réexécuter simultanément.</span><span class="sxs-lookup"><span data-stu-id="d5446-286">You can also select multiple activity windows in the list and rerun them at the same time.</span></span> <span data-ttu-id="d5446-287">Vous pouvez filtrer les fenêtres d’activité en fonction de leur statut (par exemple, **Échec**), puis réexécuter celles qui ont échoué après avoir corrigé le problème à l’origine de cet échec.</span><span class="sxs-lookup"><span data-stu-id="d5446-287">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span></span> <span data-ttu-id="d5446-288">Pour en savoir plus sur le filtrage des fenêtres d’activité dans la liste, consultez la section suivante.</span><span class="sxs-lookup"><span data-stu-id="d5446-288">See the following section for details about filtering activity windows in the list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="d5446-289">Mettre en pause/relancer plusieurs pipelines</span><span class="sxs-lookup"><span data-stu-id="d5446-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="d5446-290">Vous pouvez sélectionner 2 pipelines ou plus en maintenant la touche Ctrl enfoncée.</span><span class="sxs-lookup"><span data-stu-id="d5446-290">You can multiselect two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="d5446-291">Pour les mettre en pause/les relancer, utilisez les boutons de la barre de commandes (mis en évidence dans le rectangle rouge de l’image suivante).</span><span class="sxs-lookup"><span data-stu-id="d5446-291">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span></span>

![Mettre en pause/relancer depuis la barre de commandes](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="d5446-293">Créez des alertes</span><span class="sxs-lookup"><span data-stu-id="d5446-293">Create alerts</span></span>
<span data-ttu-id="d5446-294">La page **Alertes** vous permet de créer une alerte et d’afficher, de modifier ou de supprimer des alertes existantes.</span><span class="sxs-lookup"><span data-stu-id="d5446-294">The **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="d5446-295">Vous pouvez également désactiver ou activer une alerte.</span><span class="sxs-lookup"><span data-stu-id="d5446-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="d5446-296">Cliquez sur l’onglet **Alertes** pour afficher la page du même nom.</span><span class="sxs-lookup"><span data-stu-id="d5446-296">To see the Alerts page, click the **Alerts** tab.</span></span>

![Onglet Alertes](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="to-create-an-alert"></a><span data-ttu-id="d5446-298">Pour créer une alerte</span><span class="sxs-lookup"><span data-stu-id="d5446-298">To create an alert</span></span>
1. <span data-ttu-id="d5446-299">Pour ajouter une alerte, cliquez sur **Ajouter une alerte** .</span><span class="sxs-lookup"><span data-stu-id="d5446-299">Click **Add Alert** to add an alert.</span></span> <span data-ttu-id="d5446-300">La page **Détails** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d5446-300">You see the **Details** page.</span></span>

    ![Créer des alertes - page Détails](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="d5446-302">Spécifiez le **nom** et la **description** de l’alerte, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d5446-302">Specify the **Name** and **Description** for the alert, and click **Next**.</span></span> <span data-ttu-id="d5446-303">La page **Filtres** doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="d5446-303">You should see the **Filters** page.</span></span>

    ![Créer des alertes - page Filtres](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="d5446-305">Sélectionnez **l’événement**, l’**état** et l**’état secondaire** (facultatif) dont vous souhaitez que le service Data Factory vous informe, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d5446-305">Select the **event**, **status**, and **substatus** (optional) that you want to create a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="d5446-306">La page **Destinataires** doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="d5446-306">You should see the **Recipients** page.</span></span>

    ![Créer des alertes - page Destinataires](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="d5446-308">Sélectionnez l’option **Administrateurs d’abonnement par courrier électronique** et/ou entrez une **adresse de messagerie électronique d’administrateur supplémentaire**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="d5446-308">Select the **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="d5446-309">L’alerte doit apparaître dans la liste.</span><span class="sxs-lookup"><span data-stu-id="d5446-309">You should see the alert in the list.</span></span>

    ![Liste des alertes](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="d5446-311">Dans la liste des alertes, utilisez les boutons associés à l’alerte pour modifier, supprimer, désactiver ou activer une alerte.</span><span class="sxs-lookup"><span data-stu-id="d5446-311">In the Alerts list, use the buttons that are associated with the alert to edit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="d5446-312">Événement/statut/état secondaire</span><span class="sxs-lookup"><span data-stu-id="d5446-312">Event/status/substatus</span></span>
<span data-ttu-id="d5446-313">Le tableau suivant dresse la liste des événements et des statuts (et états secondaires) disponibles.</span><span class="sxs-lookup"><span data-stu-id="d5446-313">The following table provides the list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="d5446-314">Nom de l'événement</span><span class="sxs-lookup"><span data-stu-id="d5446-314">Event name</span></span> | <span data-ttu-id="d5446-315">État</span><span class="sxs-lookup"><span data-stu-id="d5446-315">Status</span></span> | <span data-ttu-id="d5446-316">État secondaire</span><span class="sxs-lookup"><span data-stu-id="d5446-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5446-317">Exécution de l’activité démarrée</span><span class="sxs-lookup"><span data-stu-id="d5446-317">Activity Run Started</span></span> |<span data-ttu-id="d5446-318">Démarré</span><span class="sxs-lookup"><span data-stu-id="d5446-318">Started</span></span> |<span data-ttu-id="d5446-319">Démarrage en cours</span><span class="sxs-lookup"><span data-stu-id="d5446-319">Starting</span></span> |
| <span data-ttu-id="d5446-320">Exécution de l’activité terminée</span><span class="sxs-lookup"><span data-stu-id="d5446-320">Activity Run Finished</span></span> |<span data-ttu-id="d5446-321">Réussi</span><span class="sxs-lookup"><span data-stu-id="d5446-321">Succeeded</span></span> |<span data-ttu-id="d5446-322">Réussi</span><span class="sxs-lookup"><span data-stu-id="d5446-322">Succeeded</span></span> |
| <span data-ttu-id="d5446-323">Exécution de l’activité terminée</span><span class="sxs-lookup"><span data-stu-id="d5446-323">Activity Run Finished</span></span> |<span data-ttu-id="d5446-324">Ayant échoué</span><span class="sxs-lookup"><span data-stu-id="d5446-324">Failed</span></span> |<span data-ttu-id="d5446-325">Échec de l’allocation des ressources</span><span class="sxs-lookup"><span data-stu-id="d5446-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="d5446-326">Échec de l’exécution</span><span class="sxs-lookup"><span data-stu-id="d5446-326">Failed Execution</span></span><br/><br/><span data-ttu-id="d5446-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="d5446-327">Timed Out</span></span><br/><br/><span data-ttu-id="d5446-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="d5446-328">Failed Validation</span></span><br/><br/><span data-ttu-id="d5446-329">Abandonné</span><span class="sxs-lookup"><span data-stu-id="d5446-329">Abandoned</span></span> |
| <span data-ttu-id="d5446-330">Création d’un cluster HDI à la demande démarrée</span><span class="sxs-lookup"><span data-stu-id="d5446-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="d5446-331">Démarré</span><span class="sxs-lookup"><span data-stu-id="d5446-331">Started</span></span> |-|
| <span data-ttu-id="d5446-332">Cluster HDI à la demande créé correctement</span><span class="sxs-lookup"><span data-stu-id="d5446-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="d5446-333">Réussi</span><span class="sxs-lookup"><span data-stu-id="d5446-333">Succeeded</span></span> |-|
| <span data-ttu-id="d5446-334">Cluster HDI à la demande supprimé</span><span class="sxs-lookup"><span data-stu-id="d5446-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="d5446-335">Réussi</span><span class="sxs-lookup"><span data-stu-id="d5446-335">Succeeded</span></span> |-|

### <a name="to-edit-delete-or-disable-an-alert"></a><span data-ttu-id="d5446-336">Pour modifier, supprimer ou désactiver une alerte</span><span class="sxs-lookup"><span data-stu-id="d5446-336">To edit, delete, or disable an alert</span></span>

<span data-ttu-id="d5446-337">Utilisez les boutons suivants (en rouge) pour modifier, supprimer ou désactiver une alerte.</span><span class="sxs-lookup"><span data-stu-id="d5446-337">Use the following buttons (highlighted in red) to edit, delete, or disable an alert.</span></span>

![Boutons d’alertes](./media/data-factory-monitor-manage-app/AlertButtons.png)
