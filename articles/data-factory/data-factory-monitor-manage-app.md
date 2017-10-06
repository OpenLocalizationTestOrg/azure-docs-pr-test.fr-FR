---
title: "aaaMonitor et gérer des pipelines de données - Azure | Documents Microsoft"
description: "Découvrez comment toouse hello toomonitor d’application de gestion et de surveillance et de gérer les pipelines et les fabriques de données Azure."
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
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a><span data-ttu-id="f71e1-103">Surveiller et gérer les pipelines Azure Data Factory à l’aide d’application de gestion et de surveillance hello</span><span class="sxs-lookup"><span data-stu-id="f71e1-103">Monitor and manage Azure Data Factory pipelines by using hello Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f71e1-104">Utilisation du portail Azure/d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f71e1-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="f71e1-105">Utilisation de l’application de surveillance et gestion</span><span class="sxs-lookup"><span data-stu-id="f71e1-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="f71e1-106">Cet article décrit comment toouse hello toomonitor d’application de surveillance et de gestion, gérer et déboguer vos pipelines de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="f71e1-106">This article describes how toouse hello Monitoring and Management app toomonitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="f71e1-107">Il fournit également des informations sur comment toocreate tooget informé sur les échecs des alertes.</span><span class="sxs-lookup"><span data-stu-id="f71e1-107">It also provides information on how toocreate alerts tooget notified on failures.</span></span> <span data-ttu-id="f71e1-108">Vous pouvez commencer à utiliser à l’aide d’application hello en hello regarder suivant vidéo :</span><span class="sxs-lookup"><span data-stu-id="f71e1-108">You can get started with using hello application by watching hello following video:</span></span>

> [!NOTE]
> <span data-ttu-id="f71e1-109">interface utilisateur de Hello illustré hello vidéo peut correspondre pas exactement à ce que vous voyez dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-109">hello user interface shown in hello video may not exactly match what you see in hello portal.</span></span> <span data-ttu-id="f71e1-110">Il est légèrement plus anciens, mais les concepts restent hello même.</span><span class="sxs-lookup"><span data-stu-id="f71e1-110">It's slightly older, but concepts remain hello same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a><span data-ttu-id="f71e1-111">Lancer l’application de gestion et de surveillance hello</span><span class="sxs-lookup"><span data-stu-id="f71e1-111">Launch hello Monitoring and Management app</span></span>
<span data-ttu-id="f71e1-112">toolaunch hello moniteur et l’application de gestion, cliquez sur hello **analyse et gestion** vignette sur hello **Data Factory** Panneau de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="f71e1-112">toolaunch hello Monitor and Management app, click hello **Monitor & Manage** tile on hello **Data Factory** blade for your data factory.</span></span>

![Analyse de la vignette sur la page d’accueil de Data Factory hello](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="f71e1-114">Vous devez voir hello surveillance et gestion d’application à ouvrir dans une fenêtre distincte.</span><span class="sxs-lookup"><span data-stu-id="f71e1-114">You should see hello Monitoring and Management app open in a separate window.</span></span>  

![Application de surveillance et gestion](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="f71e1-116">Si vous voyez ce navigateur hello est bloqué au niveau de « Autorisation... », désactivez hello **bloquer les cookies tiers et les données de site** --ou les conserver ce fait, créez une exception pour **login.microsoftonline.com** , puis essayez à nouveau tooopen hello application.</span><span class="sxs-lookup"><span data-stu-id="f71e1-116">If you see that hello web browser is stuck at "Authorizing...", clear hello **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>


<span data-ttu-id="f71e1-117">Dans la liste des activités Windows hello dans le volet du milieu hello, vous consultez une fenêtre d’activité pour chaque exécution d’une activité.</span><span class="sxs-lookup"><span data-stu-id="f71e1-117">In hello Activity Windows list in hello middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="f71e1-118">Par exemple, si vous disposez de toutes les heures hello activité planifiée toorun de cinq heures, vous consultez cinq windows d’activité associés à des tranches de données de cinq.</span><span class="sxs-lookup"><span data-stu-id="f71e1-118">For example, if you have hello activity scheduled toorun hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="f71e1-119">Si vous ne voyez pas windows d’activité dans la liste hello bas hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f71e1-119">If you don't see activity windows in hello list at hello bottom, do hello following:</span></span>
 
- <span data-ttu-id="f71e1-120">Hello de mise à jour **l’heure de début** et **heure de fin** filtres à Bonjour toomatch supérieur Bonjour début et fin de votre pipeline, puis cliquez sur hello **appliquer** bouton.</span><span class="sxs-lookup"><span data-stu-id="f71e1-120">Update hello **start time** and **end time** filters at hello top toomatch hello start and end times of your pipeline, and then click hello **Apply** button.</span></span>  
- <span data-ttu-id="f71e1-121">liste des activités Windows Hello n’est pas actualisée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f71e1-121">hello Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="f71e1-122">Cliquez sur hello **Actualiser** bouton de barre d’outils hello hello **Windows de l’activité** liste.</span><span class="sxs-lookup"><span data-stu-id="f71e1-122">Click hello **Refresh** button on hello toolbar in hello **Activity Windows** list.</span></span>  

<span data-ttu-id="f71e1-123">Si vous n’avez un tootest d’application Data Factory ces étapes avec, hello didacticiel : [copier les données de stockage d’objets Blob tooSQL de base de données à l’aide de la fabrique de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f71e1-123">If you don't have a Data Factory application tootest these steps with, do hello tutorial: [copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-hello-monitoring-and-management-app"></a><span data-ttu-id="f71e1-124">Comprendre hello analyse et la gestion d’application</span><span class="sxs-lookup"><span data-stu-id="f71e1-124">Understand hello Monitoring and Management app</span></span>
<span data-ttu-id="f71e1-125">Il existe trois onglets sur hello gauche : **l’Explorateur de ressources**, **affichages analyse**, et **alertes**.</span><span class="sxs-lookup"><span data-stu-id="f71e1-125">There are three tabs on hello left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="f71e1-126">premier onglet de Hello (**l’Explorateur de ressources**) est sélectionnée par défaut.</span><span class="sxs-lookup"><span data-stu-id="f71e1-126">hello first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="f71e1-127">Explorateur de ressources</span><span class="sxs-lookup"><span data-stu-id="f71e1-127">Resource Explorer</span></span>
<span data-ttu-id="f71e1-128">Il affiche hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="f71e1-128">You see hello following:</span></span>

* <span data-ttu-id="f71e1-129">l’Explorateur de ressources de Hello **arborescence** dans le volet gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-129">hello Resource Explorer **tree view** in hello left pane.</span></span>
* <span data-ttu-id="f71e1-130">Hello **vue de diagramme** haut hello, dans le volet du milieu hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-130">hello **Diagram View** at hello top in hello middle pane.</span></span>
* <span data-ttu-id="f71e1-131">Hello **Windows de l’activité** liste à la fin de hello dans le volet du milieu hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-131">hello **Activity Windows** list at hello bottom in hello middle pane.</span></span>
* <span data-ttu-id="f71e1-132">Hello **propriétés**, **activité fenêtre Explorateur**, et **Script** onglets dans le volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-132">hello **Properties**, **Activity Window Explorer**, and **Script** tabs in hello right pane.</span></span>

<span data-ttu-id="f71e1-133">Dans l’Explorateur de ressources, vous consultez toutes les ressources (pipelines, des groupes de données, les services liés) dans la fabrique de données hello dans une arborescence.</span><span class="sxs-lookup"><span data-stu-id="f71e1-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in hello data factory in a tree view.</span></span> <span data-ttu-id="f71e1-134">Lorsque vous sélectionnez un objet dans l’Explorateur de ressources :</span><span class="sxs-lookup"><span data-stu-id="f71e1-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="f71e1-135">Hello associé à l’entité est mis en surbrillance dans la vue de diagramme de hello de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="f71e1-135">hello associated Data Factory entity is highlighted in hello Diagram View.</span></span>
* <span data-ttu-id="f71e1-136">[Associés windows de l’activité](data-factory-scheduling-and-execution.md) sont mises en surbrillance dans la liste des activités Windows hello bas hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in hello Activity Windows list at hello bottom.</span></span>  
* <span data-ttu-id="f71e1-137">propriétés Hello de l’objet sélectionné de hello sont affichées dans la fenêtre de propriétés hello dans le volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-137">hello properties of hello selected object are shown in hello Properties window in hello right pane.</span></span>
* <span data-ttu-id="f71e1-138">Hello définition JSON de l’objet sélectionné de hello est indiqué, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="f71e1-138">hello JSON definition of hello selected object is shown, if applicable.</span></span> <span data-ttu-id="f71e1-139">Par exemple : un service lié, un jeu de données ou un pipeline.</span><span class="sxs-lookup"><span data-stu-id="f71e1-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Explorateur de ressources](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="f71e1-141">Consultez hello [de planification et de l’exécution](data-factory-scheduling-and-execution.md) article pour plus d’informations sur les fenêtres de l’activité.</span><span class="sxs-lookup"><span data-stu-id="f71e1-141">See hello [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="f71e1-142">Vue du diagramme</span><span class="sxs-lookup"><span data-stu-id="f71e1-142">Diagram View</span></span>
<span data-ttu-id="f71e1-143">Hello, vue de diagramme d’une fabrique de données fournit un volet de verre toomonitor et gérer une fabrique de données et ses composants.</span><span class="sxs-lookup"><span data-stu-id="f71e1-143">hello Diagram View of a data factory provides a single pane of glass toomonitor and manage a data factory and its assets.</span></span> <span data-ttu-id="f71e1-144">Lorsque vous sélectionnez une entité de la fabrique de données (jeu de données/pipeline) dans la vue de diagramme de hello :</span><span class="sxs-lookup"><span data-stu-id="f71e1-144">When you select a Data Factory entity (dataset/pipeline) in hello Diagram View:</span></span>

* <span data-ttu-id="f71e1-145">entité de fabrique de données Hello est sélectionnée dans la vue de l’arborescence hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-145">hello data factory entity is selected in hello tree view.</span></span>
* <span data-ttu-id="f71e1-146">Hello associé à l’activité windows sont mises en surbrillance dans la liste des activités Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-146">hello associated activity windows are highlighted in hello Activity Windows list.</span></span>
* <span data-ttu-id="f71e1-147">propriétés Hello de l’objet sélectionné de hello sont affichées dans la fenêtre de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-147">hello properties of hello selected object are shown in hello Properties window.</span></span>

<span data-ttu-id="f71e1-148">Lorsque le pipeline de hello est activé (pas dans un état suspendu), il est indiqué par une ligne verte :</span><span class="sxs-lookup"><span data-stu-id="f71e1-148">When hello pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Pipeline en cours d’exécution](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="f71e1-150">Vous pouvez suspendre, reprendre ou terminer un pipeline en la sélectionnant dans la vue de diagramme hello et à l’aide des boutons de hello sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-150">You can pause, resume, or terminate a pipeline by selecting it in hello diagram view and using hello buttons on hello command bar.</span></span>

![Pause/reprise sur la barre de commandes hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="f71e1-152">Il existe trois boutons de barre de commandes pour le pipeline hello Bonjour vue de diagramme.</span><span class="sxs-lookup"><span data-stu-id="f71e1-152">There are three command bar buttons for hello pipeline in hello Diagram View.</span></span> <span data-ttu-id="f71e1-153">Vous pouvez utiliser le pipeline de hello deuxième bouton toopause hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-153">You can use hello second button toopause hello pipeline.</span></span> <span data-ttu-id="f71e1-154">Suspension ne terminer hello activités en cours d’exécution et leur permet de continuer toocompletion.</span><span class="sxs-lookup"><span data-stu-id="f71e1-154">Pausing doesn't terminate hello currently running activities and lets them proceed toocompletion.</span></span> <span data-ttu-id="f71e1-155">troisième bouton de Hello suspend pipeline de hello et s’arrête ses activités existantes.</span><span class="sxs-lookup"><span data-stu-id="f71e1-155">hello third button pauses hello pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="f71e1-156">bouton de première Hello reprend le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-156">hello first button resumes hello pipeline.</span></span> <span data-ttu-id="f71e1-157">Lorsque votre pipeline est suspendu, hello du pipeline de hello devient.</span><span class="sxs-lookup"><span data-stu-id="f71e1-157">When your pipeline is paused, hello color of hello pipeline changes.</span></span> <span data-ttu-id="f71e1-158">Par exemple, un pipeline suspendu ressemble dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="f71e1-158">For example, a paused pipeline looks like in hello following image:</span></span> 

![Pipeline suspendu](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="f71e1-160">Vous pouvez sélections plusieurs pipelines de deux ou plusieurs en utilisant la touche Ctrl de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-160">You can multi-select two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="f71e1-161">Vous pouvez utiliser des boutons de barre pour hello commande toopause/reprise plusieurs pipelines à la fois.</span><span class="sxs-lookup"><span data-stu-id="f71e1-161">You can use hello command bar buttons toopause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="f71e1-162">Vous pouvez également cliquer sur un pipeline toosuspend de sélectionner des options, reprendre et arrêter un pipeline.</span><span class="sxs-lookup"><span data-stu-id="f71e1-162">You can also right-click a pipeline and select options toosuspend, resume, or terminate a pipeline.</span></span> 

![Menu contextuel pour un pipeline](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="f71e1-164">Cliquez sur hello **ouvrir pipeline** option toosee toutes les activités de hello dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-164">Click hello **Open pipeline** option toosee all hello activities in hello pipeline.</span></span> 

![Menu Ouvrir un pipeline](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="f71e1-166">Dans la vue du pipeline hello ouvert, vous voyez toutes les activités dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-166">In hello opened pipeline view, you see all activities in hello pipeline.</span></span> <span data-ttu-id="f71e1-167">Dans cet exemple, le pipeline ne contient qu’une seule activité : une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="f71e1-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Pipeline ouvert](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="f71e1-169">toogo sauvegarder toohello de vue précédente, cliquez sur le nom de fabrique de données hello dans le menu de navigation hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-169">toogo back toohello previous view, click hello data factory name in hello breadcrumb menu at hello top.</span></span>

<span data-ttu-id="f71e1-170">Dans la vue du pipeline hello, lorsque vous sélectionnez un jeu de données de sortie ou lorsque vous déplacez votre souris sur le dataset de sortie hello, vous consultez fenêtre contextuelle d’activité Windows hello pour ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="f71e1-170">In hello pipeline view, when you select an output dataset or when you move your mouse over hello output dataset, you see hello Activity Windows pop-up window for that dataset.</span></span>

![Fenêtre contextuelle d’activité Windows](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="f71e1-172">Vous pouvez également cliquer sur Détails de toosee fenêtre de l’activité pour qu’il Bonjour **propriétés** fenêtre dans le volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-172">You can click an activity window toosee details for it in hello **Properties** window in hello right pane.</span></span>

![Propriétés des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="f71e1-174">Dans le volet droit de hello, basculez toohello **activité fenêtre Explorateur** onglet toosee plus de détails.</span><span class="sxs-lookup"><span data-stu-id="f71e1-174">In hello right pane, switch toohello **Activity Window Explorer** tab toosee more details.</span></span>

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="f71e1-176">Vous voyez également **résolu variables** à chaque tentative d’exécution d’une activité dans hello **tentatives** section.</span><span class="sxs-lookup"><span data-stu-id="f71e1-176">You also see **resolved variables** for each run attempt for an activity in hello **Attempts** section.</span></span>

![Variables résolues](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="f71e1-178">Commutateur toohello **Script** onglet Définition de script toosee hello JSON pour l’objet sélectionné de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-178">Switch toohello **Script** tab toosee hello JSON script definition for hello selected object.</span></span>   

![Onglet Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="f71e1-180">Les fenêtres d’activité s’affichent à trois emplacements différents :</span><span class="sxs-lookup"><span data-stu-id="f71e1-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="f71e1-181">Hello Windows activité contextuel Bonjour vue de diagramme (volet central).</span><span class="sxs-lookup"><span data-stu-id="f71e1-181">hello Activity Windows pop-up in hello Diagram View (middle pane).</span></span>
* <span data-ttu-id="f71e1-182">Hello Explorer de fenêtre d’activité dans le volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-182">hello Activity Window Explorer in hello right pane.</span></span>
* <span data-ttu-id="f71e1-183">liste d’activités Windows Hello dans le volet du bas hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-183">hello Activity Windows list in hello bottom pane.</span></span>

<span data-ttu-id="f71e1-184">Dans fenêtre contextuelle d’activité Windows hello et Explorer de fenêtre d’activité, vous pouvez faire défiler toohello semaine précédente et hello semaine suivante à l’aide de hello flèches droite et gauche.</span><span class="sxs-lookup"><span data-stu-id="f71e1-184">In hello Activity Windows pop-up and Activity Window Explorer, you can scroll toohello previous week and hello next week by using hello left and right arrows.</span></span>

![Flèches gauche/droite de l’Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="f71e1-186">Bas hello hello vue de diagramme, vous voyez ces boutons : zoom avant, Zoom arrière, Zoom tooFit, effectuer un Zoom de 100 %, la mise en forme de verrou.</span><span class="sxs-lookup"><span data-stu-id="f71e1-186">At hello bottom of hello Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom tooFit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="f71e1-187">Hello **mise en forme de verrou** bouton vous empêche de déplacer accidentellement des tables et des pipelines Bonjour vue de diagramme.</span><span class="sxs-lookup"><span data-stu-id="f71e1-187">hello **Lock layout** button prevents you from accidentally moving tables and pipelines in hello Diagram View.</span></span> <span data-ttu-id="f71e1-188">L’option est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="f71e1-188">It's on by default.</span></span> <span data-ttu-id="f71e1-189">Vous pouvez désactiver cette option et déplacer des entités dans le diagramme de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-189">You can turn it off and move entities around in hello diagram.</span></span> <span data-ttu-id="f71e1-190">Lorsque vous le désactivez, vous pouvez utiliser des pipelines et les tables de position hello derniers bouton tooautomatically.</span><span class="sxs-lookup"><span data-stu-id="f71e1-190">When you turn it off, you can use hello last button tooautomatically position tables and pipelines.</span></span> <span data-ttu-id="f71e1-191">Vous pouvez également effectuer un zoom ou de sortie à l’aide de la roulette de souris hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-191">You can also zoom in or out by using hello mouse wheel.</span></span>

![Commandes de zoom de la vue schématique](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="f71e1-193">Liste des fenêtres d’activité</span><span class="sxs-lookup"><span data-stu-id="f71e1-193">Activity Windows list</span></span>
<span data-ttu-id="f71e1-194">liste des activités Windows Hello bas hello du volet du milieu hello affiche toutes les fenêtres d’activité pour hello dataset que vous avez sélectionné dans hello l’Explorateur de ressources ou hello vue de diagramme.</span><span class="sxs-lookup"><span data-stu-id="f71e1-194">hello Activity Windows list at hello bottom of hello middle pane displays all activity windows for hello dataset that you selected in hello Resource Explorer or hello Diagram View.</span></span> <span data-ttu-id="f71e1-195">Par défaut, la liste de hello est dans l’ordre décroissant, ce qui signifie que vous voyez dernière fenêtre d’activité hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-195">By default, hello list is in descending order, which means that you see hello latest activity window at hello top.</span></span>

![Liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="f71e1-197">Cette liste n’actualise pas automatiquement, afin d’utiliser hello sur bouton Actualiser de hello barre d’outils toomanually Actualiser.</span><span class="sxs-lookup"><span data-stu-id="f71e1-197">This list doesn't refresh automatically, so use hello refresh button on hello toolbar toomanually refresh it.</span></span>  

<span data-ttu-id="f71e1-198">Windows de l’activité peuvent être dans un des hello suivant des États :</span><span class="sxs-lookup"><span data-stu-id="f71e1-198">Activity windows can be in one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="f71e1-199">État</span><span class="sxs-lookup"><span data-stu-id="f71e1-199">Status</span></span></th><th align="left"><span data-ttu-id="f71e1-200">État secondaire</span><span class="sxs-lookup"><span data-stu-id="f71e1-200">Substatus</span></span></th><th align="left"><span data-ttu-id="f71e1-201">Description</span><span class="sxs-lookup"><span data-stu-id="f71e1-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="f71e1-202">En attente</span><span class="sxs-lookup"><span data-stu-id="f71e1-202">Waiting</span></span></td><td><span data-ttu-id="f71e1-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="f71e1-203">ScheduleTime</span></span></td><td><span data-ttu-id="f71e1-204">temps de Hello n’a pas encore être motivée par de toorun de fenêtre d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-204">hello time hasn't come for hello activity window toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f71e1-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="f71e1-205">DatasetDependencies</span></span></td><td><span data-ttu-id="f71e1-206">les dépendances en amont Hello ne sont pas prêts.</span><span class="sxs-lookup"><span data-stu-id="f71e1-206">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f71e1-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="f71e1-207">ComputeResources</span></span></td><td><span data-ttu-id="f71e1-208">ressources de calcul Hello ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="f71e1-208">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f71e1-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="f71e1-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="f71e1-210">Toutes les instances d’activité hello sont occupés autres fenêtres de l’activité en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f71e1-210">All hello activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f71e1-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="f71e1-211">ActivityResume</span></span></td><td><span data-ttu-id="f71e1-212">activité Hello est suspendue et ne peut pas exécuter windows d’activité hello jusqu'à sa reprise.</span><span class="sxs-lookup"><span data-stu-id="f71e1-212">hello activity is paused and can't run hello activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f71e1-213">Retry</span><span class="sxs-lookup"><span data-stu-id="f71e1-213">Retry</span></span></td><td><span data-ttu-id="f71e1-214">exécution de l’activité Hello est renouvelée.</span><span class="sxs-lookup"><span data-stu-id="f71e1-214">hello activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f71e1-215">Validation</span><span class="sxs-lookup"><span data-stu-id="f71e1-215">Validation</span></span></td><td><span data-ttu-id="f71e1-216">La validation n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="f71e1-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f71e1-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="f71e1-217">ValidationRetry</span></span></td><td><span data-ttu-id="f71e1-218">La validation est toobe en attente une nouvelle tentée.</span><span class="sxs-lookup"><span data-stu-id="f71e1-218">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="f71e1-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="f71e1-219">InProgress</span></span></td><td><span data-ttu-id="f71e1-220">Validation</span><span class="sxs-lookup"><span data-stu-id="f71e1-220">Validating</span></span></td><td><span data-ttu-id="f71e1-221">La validation est en cours.</span><span class="sxs-lookup"><span data-stu-id="f71e1-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="f71e1-222">fenêtre d’activité Hello est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="f71e1-222">hello activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="f71e1-223">Échec</span><span class="sxs-lookup"><span data-stu-id="f71e1-223">Failed</span></span></td><td><span data-ttu-id="f71e1-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="f71e1-224">TimedOut</span></span></td><td><span data-ttu-id="f71e1-225">exécution de l’activité Hello a pris plus de temps que ce qui est autorisé par activité hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-225">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f71e1-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="f71e1-226">Canceled</span></span></td><td><span data-ttu-id="f71e1-227">fenêtre d’activité Hello a été annulée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f71e1-227">hello activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f71e1-228">Validation</span><span class="sxs-lookup"><span data-stu-id="f71e1-228">Validation</span></span></td><td><span data-ttu-id="f71e1-229">La validation a échoué.</span><span class="sxs-lookup"><span data-stu-id="f71e1-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="f71e1-230">fenêtre d’activité Hello échec toobe généré ou validé.</span><span class="sxs-lookup"><span data-stu-id="f71e1-230">hello activity window failed toobe generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="f71e1-231">Ready</span><span class="sxs-lookup"><span data-stu-id="f71e1-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="f71e1-232">fenêtre d’activité Hello est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="f71e1-232">hello activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f71e1-233">Ignoré</span><span class="sxs-lookup"><span data-stu-id="f71e1-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="f71e1-234">fenêtre d’activité Hello n’a pas été traitée.</span><span class="sxs-lookup"><span data-stu-id="f71e1-234">hello activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f71e1-235">Aucun</span><span class="sxs-lookup"><span data-stu-id="f71e1-235">None</span></span></td><td>-</td><td><span data-ttu-id="f71e1-236">Une fenêtre d’activité tooexist avec un état différent, mais a été réinitialisée.</span><span class="sxs-lookup"><span data-stu-id="f71e1-236">An activity window used tooexist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="f71e1-237">Lorsque vous cliquez sur une fenêtre d’activité dans la liste de hello, vous consultez des informations à son Bonjour **l’Explorateur Windows activité** ou hello **propriétés** fenêtre sur hello droite.</span><span class="sxs-lookup"><span data-stu-id="f71e1-237">When you click an activity window in hello list, you see details about it in hello **Activity Windows Explorer** or hello **Properties** window on hello right.</span></span>

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="f71e1-239">Actualiser les fenêtres d’activité</span><span class="sxs-lookup"><span data-stu-id="f71e1-239">Refresh activity windows</span></span>
<span data-ttu-id="f71e1-240">Détails de Hello ne sont pas automatiquement actualisées, alors utilisez le bouton d’actualisation hello (hello deuxième bouton) sur la liste de windows toomanually actualisation hello activité de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-240">hello details aren't automatically refreshed, so use hello refresh button (hello second button) on hello command bar toomanually refresh hello activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="f71e1-241">Fenêtre Propriétés</span><span class="sxs-lookup"><span data-stu-id="f71e1-241">Properties window</span></span>
<span data-ttu-id="f71e1-242">fenêtre de propriétés Hello est volet le plus à droite de hello d’application de gestion et de surveillance hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-242">hello Properties window is in hello right-most pane of hello Monitoring and Management app.</span></span>

![Fenêtre Propriétés](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="f71e1-244">Il affiche les propriétés de l’élément hello que vous avez sélectionné dans hello l’Explorateur de ressources (arborescence), vue de diagramme ou la liste des activités Windows.</span><span class="sxs-lookup"><span data-stu-id="f71e1-244">It displays properties for hello item that you selected in hello Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="f71e1-245">Explorateur de fenêtres d’activité</span><span class="sxs-lookup"><span data-stu-id="f71e1-245">Activity Window Explorer</span></span>
<span data-ttu-id="f71e1-246">Hello **activité fenêtre Explorateur** fenêtre est en volet le plus à droite de hello d’application de gestion et de surveillance hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-246">hello **Activity Window Explorer** window is in hello right-most pane of hello Monitoring and Management app.</span></span> <span data-ttu-id="f71e1-247">Il affiche les détails de la fenêtre d’activité hello que vous avez sélectionné dans la fenêtre contextuelle d’activité Windows hello ou une liste d’activités Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-247">It displays details about hello activity window that you selected in hello Activity Windows pop-up window or hello Activity Windows list.</span></span>

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="f71e1-249">Vous pouvez basculer la fenêtre d’activité tooanother en cliquant dessus dans l’affichage du calendrier hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-249">You can switch tooanother activity window by clicking it in hello calendar view at hello top.</span></span> <span data-ttu-id="f71e1-250">Vous pouvez également utiliser les boutons flèche gauche/droite hello à fenêtres activité hello toosee supérieur hello semaine précédente ou hello semaine suivante.</span><span class="sxs-lookup"><span data-stu-id="f71e1-250">You can also use hello left arrow/right arrow buttons at hello top toosee activity windows from hello previous week or hello next week.</span></span>

<span data-ttu-id="f71e1-251">Vous pouvez utiliser les boutons de barre d’outils hello dans la fenêtre d’activité hello bas volet toorerun hello ou actualiser les détails de hello dans le volet de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-251">You can use hello toolbar buttons in hello bottom pane toorerun hello activity window or refresh hello details in hello pane.</span></span>

### <a name="script"></a><span data-ttu-id="f71e1-252">Script</span><span class="sxs-lookup"><span data-stu-id="f71e1-252">Script</span></span>
<span data-ttu-id="f71e1-253">Vous pouvez utiliser hello **Script** hello de tooview onglet Définition JSON de hello sélectionné entity Data Factory (service lié, dataset ou pipeline).</span><span class="sxs-lookup"><span data-stu-id="f71e1-253">You can use hello **Script** tab tooview hello JSON definition of hello selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Onglet Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="f71e1-255">Utiliser les vues système</span><span class="sxs-lookup"><span data-stu-id="f71e1-255">Use system views</span></span>
<span data-ttu-id="f71e1-256">Surveillance et gestion de l’application Hello inclut les vues système intégrées (**windows d’activité récente**, **Échec de windows de l’activité**, **windows de l’activité en cours**) qui permettent de windows les activités récentes/échec/en cours de tooview de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="f71e1-256">hello Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you tooview recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="f71e1-257">Commutateur toohello **affichages analyse** onglet sur la gauche hello en cliquant dessus.</span><span class="sxs-lookup"><span data-stu-id="f71e1-257">Switch toohello **Monitoring Views** tab on hello left by clicking it.</span></span>

![Onglet Vues de surveillance](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="f71e1-259">Actuellement, trois vues système sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="f71e1-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="f71e1-260">Sélectionnez une option toosee récente activité windows, windows de l’activité qui a échoué ou les activités en cours d’exécution windows dans la liste des activités Windows hello (bas hello du volet du milieu hello).</span><span class="sxs-lookup"><span data-stu-id="f71e1-260">Select an option toosee recent activity windows, failed activity windows, or in-progress activity windows in hello Activity Windows list (at hello bottom of hello middle pane).</span></span>

<span data-ttu-id="f71e1-261">Lorsque vous sélectionnez hello **windows d’activité récente** option, vous voyez toutes les fenêtres d’activité récente dans l’ordre décroissant de hello **heure de la dernière tentative**.</span><span class="sxs-lookup"><span data-stu-id="f71e1-261">When you select hello **Recent activity windows** option, you see all recent activity windows in descending order of hello **last attempt time**.</span></span>

<span data-ttu-id="f71e1-262">Vous pouvez utiliser hello **Échec de windows de l’activité** afficher toosee tout échoué de l’activité windows dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-262">You can use hello **Failed activity windows** view toosee all failed activity windows in hello list.</span></span> <span data-ttu-id="f71e1-263">Sélectionnez une fenêtre d’activité ayant échoué dans hello liste toosee plus d’informations sur elle Bonjour **propriétés** fenêtre ou hello **activité fenêtre Explorateur**.</span><span class="sxs-lookup"><span data-stu-id="f71e1-263">Select a failed activity window in hello list toosee details about it in hello **Properties** window or hello **Activity Window Explorer**.</span></span> <span data-ttu-id="f71e1-264">Vous pouvez également télécharger tous les journaux d’une fenêtre d’activité ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="f71e1-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="f71e1-265">Trier et filtrer les fenêtres d’activité</span><span class="sxs-lookup"><span data-stu-id="f71e1-265">Sort and filter activity windows</span></span>
<span data-ttu-id="f71e1-266">Hello de modification **l’heure de début** et **heure de fin** paramètres dans windows d’activité toofilter de barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-266">Change hello **start time** and **end time** settings in hello command bar toofilter activity windows.</span></span> <span data-ttu-id="f71e1-267">Après avoir modifié l’heure de début hello et l’heure de fin, cliquez sur hello bouton suivant toohello fin heure toorefresh hello Windows de l’activité de la liste.</span><span class="sxs-lookup"><span data-stu-id="f71e1-267">After you change hello start time and end time, click hello button next toohello end time toorefresh hello Activity Windows list.</span></span>

![Heures de début et de fin](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="f71e1-269">Actuellement, toutes les heures sont au format UTC dans l’application de gestion et de surveillance hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-269">Currently, all times are in UTC format in hello Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="f71e1-270">Bonjour **liste activité Windows**, cliquez sur le nom hello d’une colonne (par exemple : état).</span><span class="sxs-lookup"><span data-stu-id="f71e1-270">In hello **Activity Windows list**, click hello name of a column (for example: Status).</span></span>

![Menu déroulant de la liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="f71e1-272">Vous pouvez effectuer les suivant hello :</span><span class="sxs-lookup"><span data-stu-id="f71e1-272">You can do hello following:</span></span>

* <span data-ttu-id="f71e1-273">Trier dans l’ordre croissant.</span><span class="sxs-lookup"><span data-stu-id="f71e1-273">Sort in ascending order.</span></span>
* <span data-ttu-id="f71e1-274">Trier dans l’ordre décroissant.</span><span class="sxs-lookup"><span data-stu-id="f71e1-274">Sort in descending order.</span></span>
* <span data-ttu-id="f71e1-275">Filtrer selon une ou plusieurs valeurs (Prêt, En attente, etc.).</span><span class="sxs-lookup"><span data-stu-id="f71e1-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="f71e1-276">Lorsque vous spécifiez un filtre sur une colonne, vous voyez le bouton Filtrer hello activé pour cette colonne, ce qui indique que les valeurs hello dans la colonne de hello sont les valeurs filtrées.</span><span class="sxs-lookup"><span data-stu-id="f71e1-276">When you specify a filter on a column, you see hello filter button enabled for that column, which indicates that hello values in hello column are filtered values.</span></span>

![Filtrer sur une colonne de la liste des activités Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="f71e1-278">Vous pouvez utiliser hello mêmes filtres tooclear de fenêtre indépendante.</span><span class="sxs-lookup"><span data-stu-id="f71e1-278">You can use hello same pop-up window tooclear filters.</span></span> <span data-ttu-id="f71e1-279">tooclear tous les filtres pour la liste activité Windows hello, cliquez sur bouton Effacer le filtre de hello sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-279">tooclear all filters for hello Activity Windows list, click hello clear filter button on hello command bar.</span></span>

![Effacer tous les filtres de la liste des activités Windows hello](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="f71e1-281">Exécuter des opérations de traitement par lot</span><span class="sxs-lookup"><span data-stu-id="f71e1-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="f71e1-282">Réexécuter les fenêtres d’activité sélectionnées</span><span class="sxs-lookup"><span data-stu-id="f71e1-282">Rerun selected activity windows</span></span>
<span data-ttu-id="f71e1-283">Sélectionnez une fenêtre d’activité et cliquez sur hello flèche bas pour le premier bouton de barre de commande hello, sélectionnez **réexécuter** / **réexécuter avec situés en amont dans le pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f71e1-283">Select an activity window, click hello down arrow for hello first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="f71e1-284">Lorsque vous sélectionnez hello **réexécuter avec situés en amont dans le pipeline** option, elle exécute à nouveau toutes les fenêtres d’activité en amont ainsi.</span><span class="sxs-lookup"><span data-stu-id="f71e1-284">When you select hello **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="f71e1-285">![Réexécuter une fenêtre d’activité](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="f71e1-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="f71e1-286">Vous pouvez également sélectionner plusieurs fenêtres d’activité dans la liste de hello et réexécuter à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="f71e1-286">You can also select multiple activity windows in hello list and rerun them at hello same time.</span></span> <span data-ttu-id="f71e1-287">Vous pourriez windows d’activité toofilter basés sur l’état de hello (par exemple : **n’a pas pu**)--hello échoué de l’activité windows puis exécutez à nouveau après avoir corrigé le problème hello hello activité windows toofail.</span><span class="sxs-lookup"><span data-stu-id="f71e1-287">You might want toofilter activity windows based on hello status (for example: **Failed**)--and then rerun hello failed activity windows after correcting hello issue that causes hello activity windows toofail.</span></span> <span data-ttu-id="f71e1-288">Consultez hello section suivante pour plus d’informations sur le filtrage windows d’activité dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-288">See hello following section for details about filtering activity windows in hello list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="f71e1-289">Mettre en pause/relancer plusieurs pipelines</span><span class="sxs-lookup"><span data-stu-id="f71e1-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="f71e1-290">Vous pouvez sélectionner plusieurs pipelines de deux ou plusieurs en utilisant la touche Ctrl de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-290">You can multiselect two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="f71e1-291">Vous pouvez utiliser les boutons de barre de commandes hello (qui sont mises en surbrillance dans le rectangle de hello rouge de hello suivant image) toopause/reprise les.</span><span class="sxs-lookup"><span data-stu-id="f71e1-291">You can use hello command bar buttons (which are highlighted in hello red rectangle in hello following image) toopause/resume them.</span></span>

![Pause/reprise sur la barre de commandes hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="f71e1-293">Créez des alertes</span><span class="sxs-lookup"><span data-stu-id="f71e1-293">Create alerts</span></span>
<span data-ttu-id="f71e1-294">Hello **alertes** page vous permet de créer une alerte et afficher/modifier/supprimer des alertes existantes.</span><span class="sxs-lookup"><span data-stu-id="f71e1-294">hello **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="f71e1-295">Vous pouvez également désactiver ou activer une alerte.</span><span class="sxs-lookup"><span data-stu-id="f71e1-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="f71e1-296">toosee hello page alertes, cliquez sur hello **alertes** onglet.</span><span class="sxs-lookup"><span data-stu-id="f71e1-296">toosee hello Alerts page, click hello **Alerts** tab.</span></span>

![Onglet Alertes](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a><span data-ttu-id="f71e1-298">toocreate une alerte</span><span class="sxs-lookup"><span data-stu-id="f71e1-298">toocreate an alert</span></span>
1. <span data-ttu-id="f71e1-299">Cliquez sur **ajouter une alerte** tooadd une alerte.</span><span class="sxs-lookup"><span data-stu-id="f71e1-299">Click **Add Alert** tooadd an alert.</span></span> <span data-ttu-id="f71e1-300">Vous consultez hello **détails** page.</span><span class="sxs-lookup"><span data-stu-id="f71e1-300">You see hello **Details** page.</span></span>

    ![Créer des alertes - page Détails](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="f71e1-302">Spécifiez hello **nom** et **Description** alerte de hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="f71e1-302">Specify hello **Name** and **Description** for hello alert, and click **Next**.</span></span> <span data-ttu-id="f71e1-303">Vous devez voir hello **filtres** page.</span><span class="sxs-lookup"><span data-stu-id="f71e1-303">You should see hello **Filters** page.</span></span>

    ![Créer des alertes - page Filtres](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="f71e1-305">Sélectionnez hello **événement**, **état**, et **sous-état** (facultatif) que vous souhaitez toocreate un service de fabrique de données pour des alertes, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="f71e1-305">Select hello **event**, **status**, and **substatus** (optional) that you want toocreate a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="f71e1-306">Vous devez voir hello **destinataires** page.</span><span class="sxs-lookup"><span data-stu-id="f71e1-306">You should see hello **Recipients** page.</span></span>

    ![Créer des alertes - page Destinataires](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="f71e1-308">Sélectionnez hello **envoyer par courrier électronique les administrateurs d’abonnements** option et/ou entrez un **par courrier électronique des administrateurs supplémentaires**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="f71e1-308">Select hello **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="f71e1-309">Vous devez voir l’alerte hello dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="f71e1-309">You should see hello alert in hello list.</span></span>

    ![Liste des alertes](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="f71e1-311">Dans la liste des alertes hello, utilisez les boutons de hello associés hello alerte tooedit/delete/désactiver/activer une alerte.</span><span class="sxs-lookup"><span data-stu-id="f71e1-311">In hello Alerts list, use hello buttons that are associated with hello alert tooedit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="f71e1-312">Événement/statut/état secondaire</span><span class="sxs-lookup"><span data-stu-id="f71e1-312">Event/status/substatus</span></span>
<span data-ttu-id="f71e1-313">Hello tableau suivant fournit hello liste des événements disponibles et les États (sous-états).</span><span class="sxs-lookup"><span data-stu-id="f71e1-313">hello following table provides hello list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="f71e1-314">Nom de l'événement</span><span class="sxs-lookup"><span data-stu-id="f71e1-314">Event name</span></span> | <span data-ttu-id="f71e1-315">État</span><span class="sxs-lookup"><span data-stu-id="f71e1-315">Status</span></span> | <span data-ttu-id="f71e1-316">État secondaire</span><span class="sxs-lookup"><span data-stu-id="f71e1-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f71e1-317">Exécution de l’activité démarrée</span><span class="sxs-lookup"><span data-stu-id="f71e1-317">Activity Run Started</span></span> |<span data-ttu-id="f71e1-318">Démarré</span><span class="sxs-lookup"><span data-stu-id="f71e1-318">Started</span></span> |<span data-ttu-id="f71e1-319">Démarrage en cours</span><span class="sxs-lookup"><span data-stu-id="f71e1-319">Starting</span></span> |
| <span data-ttu-id="f71e1-320">Exécution de l’activité terminée</span><span class="sxs-lookup"><span data-stu-id="f71e1-320">Activity Run Finished</span></span> |<span data-ttu-id="f71e1-321">Réussi</span><span class="sxs-lookup"><span data-stu-id="f71e1-321">Succeeded</span></span> |<span data-ttu-id="f71e1-322">Réussi</span><span class="sxs-lookup"><span data-stu-id="f71e1-322">Succeeded</span></span> |
| <span data-ttu-id="f71e1-323">Exécution de l’activité terminée</span><span class="sxs-lookup"><span data-stu-id="f71e1-323">Activity Run Finished</span></span> |<span data-ttu-id="f71e1-324">Ayant échoué</span><span class="sxs-lookup"><span data-stu-id="f71e1-324">Failed</span></span> |<span data-ttu-id="f71e1-325">Échec de l’allocation des ressources</span><span class="sxs-lookup"><span data-stu-id="f71e1-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="f71e1-326">Échec de l’exécution</span><span class="sxs-lookup"><span data-stu-id="f71e1-326">Failed Execution</span></span><br/><br/><span data-ttu-id="f71e1-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="f71e1-327">Timed Out</span></span><br/><br/><span data-ttu-id="f71e1-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="f71e1-328">Failed Validation</span></span><br/><br/><span data-ttu-id="f71e1-329">Abandonné</span><span class="sxs-lookup"><span data-stu-id="f71e1-329">Abandoned</span></span> |
| <span data-ttu-id="f71e1-330">Création d’un cluster HDI à la demande démarrée</span><span class="sxs-lookup"><span data-stu-id="f71e1-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="f71e1-331">Démarré</span><span class="sxs-lookup"><span data-stu-id="f71e1-331">Started</span></span> |-|
| <span data-ttu-id="f71e1-332">Cluster HDI à la demande créé correctement</span><span class="sxs-lookup"><span data-stu-id="f71e1-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="f71e1-333">Réussi</span><span class="sxs-lookup"><span data-stu-id="f71e1-333">Succeeded</span></span> |-|
| <span data-ttu-id="f71e1-334">Cluster HDI à la demande supprimé</span><span class="sxs-lookup"><span data-stu-id="f71e1-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="f71e1-335">Réussi</span><span class="sxs-lookup"><span data-stu-id="f71e1-335">Succeeded</span></span> |-|

### <a name="tooedit-delete-or-disable-an-alert"></a><span data-ttu-id="f71e1-336">tooedit, supprimer ou désactiver une alerte</span><span class="sxs-lookup"><span data-stu-id="f71e1-336">tooedit, delete, or disable an alert</span></span>

<span data-ttu-id="f71e1-337">Utilisez hello suivant tooedit de boutons (mis en surbrillance en rouge), supprimer ou désactiver une alerte.</span><span class="sxs-lookup"><span data-stu-id="f71e1-337">Use hello following buttons (highlighted in red) tooedit, delete, or disable an alert.</span></span>

![Boutons d’alertes](./media/data-factory-monitor-manage-app/AlertButtons.png)
