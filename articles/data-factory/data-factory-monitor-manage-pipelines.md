---
title: "Surveiller et gérer les pipelines à l’aide du portail Azure et de PowerShell | Microsoft Docs"
description: "Découvrez comment utiliser le portail Azure et Azure PowerShell pour surveiller et gérer les fabriques de données et les pipelines Azure que vous avez créés."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 61bb5379cd94dd00814e14420947e7783999ff0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-azure-portal-and-powershell"></a><span data-ttu-id="a9102-103">Surveiller et gérer les pipelines Azure Data Factory à l’aide du portail Azure et de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9102-103">Monitor and manage Azure Data Factory pipelines by using the Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9102-104">Utilisation du portail Azure/d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9102-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="a9102-105">Utilisation de l’application de surveillance et gestion</span><span class="sxs-lookup"><span data-stu-id="a9102-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="a9102-106">L’application de surveillance et gestion favorise la surveillance et la gestion de vos pipelines de données, ainsi que la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="a9102-106">The monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="a9102-107">Pour en savoir plus sur l’utilisation de l’application, consultez [Surveiller et gérer les pipelines Azure Data Factory à l’aide de l’application de surveillance et gestion](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="a9102-107">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="a9102-108">Cet article décrit comment surveiller, gérer et déboguer vos pipelines à l’aide du Portail Azure et de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9102-108">This article describes how to monitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="a9102-109">Il offre également des informations sur la façon de créer des alertes et d’être averti en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="a9102-109">The article also provides information on how to create alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="a9102-110">Présentation des pipelines et des états d’activité</span><span class="sxs-lookup"><span data-stu-id="a9102-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="a9102-111">À l’aide du portail Azure, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="a9102-111">By using the Azure portal, you can:</span></span>

* <span data-ttu-id="a9102-112">Afficher votre fabrique de données sous forme de schéma.</span><span class="sxs-lookup"><span data-stu-id="a9102-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="a9102-113">Afficher les activités à l’intérieur d’un pipeline.</span><span class="sxs-lookup"><span data-stu-id="a9102-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="a9102-114">Afficher des jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="a9102-114">View input and output datasets.</span></span>

<span data-ttu-id="a9102-115">Cette section décrit également comment une tranche de jeu de données passe d’un état à un autre.</span><span class="sxs-lookup"><span data-stu-id="a9102-115">This section also describes how a dataset slice transitions from one state to another state.</span></span>   

### <a name="navigate-to-your-data-factory"></a><span data-ttu-id="a9102-116">Accédez à votre fabrique de données</span><span class="sxs-lookup"><span data-stu-id="a9102-116">Navigate to your data factory</span></span>
1. <span data-ttu-id="a9102-117">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9102-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a9102-118">Cliquer sur **Fabriques de données** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="a9102-118">Click **Data factories** on the menu on the left.</span></span> <span data-ttu-id="a9102-119">Si vous ne voyez pas cette option, cliquez sur **Autres services >**, puis sur **Fabriques de données** dans la catégorie **INTELLIGENCE + ANALYSE**.</span><span class="sxs-lookup"><span data-stu-id="a9102-119">If you don't see it, click **More services >**, and then click **Data factories** under the **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Parcourir tout > Fabriques de données](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="a9102-121">Dans le panneau **Fabriques de données**, sélectionnez la fabrique de données qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="a9102-121">On the **Data factories** blade, select the data factory that you're interested in.</span></span>

    ![Sélectionner une fabrique de données](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="a9102-123">Vous devez voir la page d’accueil de la fabrique de données apparaître.</span><span class="sxs-lookup"><span data-stu-id="a9102-123">You should see the home page for the data factory.</span></span>

   ![Panneau Data Factory](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="a9102-125">Vue schématique de votre fabrique de données</span><span class="sxs-lookup"><span data-stu-id="a9102-125">Diagram view of your data factory</span></span>
<span data-ttu-id="a9102-126">La vue **schématique** d’une fabrique de données est un point unique de surveillance et de gestion de la fabrique de données et de ses ressources.</span><span class="sxs-lookup"><span data-stu-id="a9102-126">The **Diagram** view of a data factory provides a single pane of glass to monitor and manage the data factory and its assets.</span></span> <span data-ttu-id="a9102-127">Cliquez sur **Schématique** sur la page d’accueil de la fabrique de données ci-dessus pour afficher la vue **schématique** de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="a9102-127">To see the **Diagram** view of your data factory, click **Diagram** on the home page for the data factory.</span></span>

![Vue schématique](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="a9102-129">Vous pouvez faire un zoom avant, un zoom arrière, un zoom à 100 %, un zoom pour ajuster l’affichage à la taille de l’écran, figer l’affichage schématique et positionner automatiquement les pipelines et les jeux de données.</span><span class="sxs-lookup"><span data-stu-id="a9102-129">You can zoom in, zoom out, zoom to fit, zoom to 100%, lock the layout of the diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="a9102-130">Vous pouvez également afficher le lignage (c.-à-d. mise en surbrillance des éléments en amont et en aval des éléments sélectionnés).</span><span class="sxs-lookup"><span data-stu-id="a9102-130">You can also see the data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="a9102-131">Activités à l'intérieur d'un pipeline</span><span class="sxs-lookup"><span data-stu-id="a9102-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="a9102-132">Cliquez avec le bouton droit sur le pipeline de votre choix, puis cliquez sur **Ouvrir le pipeline** pour faire apparaître toutes les activités dans le pipeline, ainsi que les jeux de données d’entrée et de sortie des activités.</span><span class="sxs-lookup"><span data-stu-id="a9102-132">Right-click the pipeline, and then click **Open pipeline** to see all activities in the pipeline, along with input and output datasets for the activities.</span></span> <span data-ttu-id="a9102-133">Cette fonctionnalité est utile quand votre pipeline comprend plusieurs activités et que vous souhaitez comprendre le lignage opérationnel d’un seul pipeline.</span><span class="sxs-lookup"><span data-stu-id="a9102-133">This feature is useful when your pipeline includes more than one activity and you want to understand the operational lineage of a single pipeline.</span></span>

    ![Menu Ouvrir un pipeline](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="a9102-135">Dans l’exemple suivant, vous voyez une activité de copie dans le pipeline avec une entrée et une sortie.</span><span class="sxs-lookup"><span data-stu-id="a9102-135">In the following example, you see a copy activity in the pipeline with an input and an output.</span></span> 

    ![Activités à l'intérieur d'un pipeline](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="a9102-137">Vous pouvez revenir à la page d’accueil de la fabrique de données en cliquant sur le lien **Data Factory** dans l’arborescence de navigation située dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="a9102-137">You can navigate back to the home page of the data factory by clicking the **Data factory** link in the breadcrumb at the top-left corner.</span></span>

    ![Revenir à la fabrique de données](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-the-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="a9102-139">Afficher l’état de chaque activité à l’intérieur d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="a9102-139">View the state of each activity inside a pipeline</span></span>
<span data-ttu-id="a9102-140">Vous pouvez afficher l’état actuel d’une activité en consultant l’état de l’un des jeux de données générés par l’activité.</span><span class="sxs-lookup"><span data-stu-id="a9102-140">You can view the current state of an activity by viewing the status of any of the datasets that are produced by the activity.</span></span>

<span data-ttu-id="a9102-141">En double-cliquant sur **OutputBlobTable** dans le **Diagramme**, vous pouvez voir toutes les tranches produites par les différentes exécutions de l’activité à l’intérieur d’un pipeline.</span><span class="sxs-lookup"><span data-stu-id="a9102-141">By double-clicking the **OutputBlobTable** in the **Diagram**, you can see all the slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="a9102-142">Vous pouvez voir que l’activité de copie a été exécutée correctement au cours des huit dernières heures et qu’elle a produit les tranches dont l’état est **Prêt**.</span><span class="sxs-lookup"><span data-stu-id="a9102-142">You can see that the copy activity ran successfully for the last eight hours and produced the slices in the **Ready** state.</span></span>  

![État du pipeline](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="a9102-144">Voici la liste des différents états possibles pour les tranches d’un jeu de données de la fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="a9102-144">The dataset slices in the data factory can have one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="a9102-145">State</span><span class="sxs-lookup"><span data-stu-id="a9102-145">State</span></span></th><th align="left"><span data-ttu-id="a9102-146">Sous-état</span><span class="sxs-lookup"><span data-stu-id="a9102-146">Substate</span></span></th><th align="left"><span data-ttu-id="a9102-147">Description</span><span class="sxs-lookup"><span data-stu-id="a9102-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="a9102-148">En attente</span><span class="sxs-lookup"><span data-stu-id="a9102-148">Waiting</span></span></td><td><span data-ttu-id="a9102-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="a9102-149">ScheduleTime</span></span></td><td><span data-ttu-id="a9102-150">L’heure n’est pas venue pour l’exécution de la tranche.</span><span class="sxs-lookup"><span data-stu-id="a9102-150">The time hasn't come for the slice to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a9102-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="a9102-151">DatasetDependencies</span></span></td><td><span data-ttu-id="a9102-152">Les dépendances en amont ne sont pas prêtes.</span><span class="sxs-lookup"><span data-stu-id="a9102-152">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a9102-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="a9102-153">ComputeResources</span></span></td><td><span data-ttu-id="a9102-154">Les ressources de calcul ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="a9102-154">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a9102-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="a9102-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="a9102-156">Toutes les instances d'activité sont occupées par l'exécution d'autres tranches.</span><span class="sxs-lookup"><span data-stu-id="a9102-156">All the activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a9102-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="a9102-157">ActivityResume</span></span></td><td><span data-ttu-id="a9102-158">L’activité est mise en pause et ne peut pas exécuter les tranches jusqu’à sa reprise.</span><span class="sxs-lookup"><span data-stu-id="a9102-158">The activity is paused and can't run the slices until the activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a9102-159">Retry</span><span class="sxs-lookup"><span data-stu-id="a9102-159">Retry</span></span></td><td><span data-ttu-id="a9102-160">L’exécution de l’activité est retentée.</span><span class="sxs-lookup"><span data-stu-id="a9102-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a9102-161">Validation</span><span class="sxs-lookup"><span data-stu-id="a9102-161">Validation</span></span></td><td><span data-ttu-id="a9102-162">La validation n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="a9102-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a9102-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="a9102-163">ValidationRetry</span></span></td><td><span data-ttu-id="a9102-164">Une nouvelle tentative de validation va avoir lieu.</span><span class="sxs-lookup"><span data-stu-id="a9102-164">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="a9102-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="a9102-165">InProgress</span></span></td><td><span data-ttu-id="a9102-166">Validation</span><span class="sxs-lookup"><span data-stu-id="a9102-166">Validating</span></span></td><td><span data-ttu-id="a9102-167">La validation est en cours.</span><span class="sxs-lookup"><span data-stu-id="a9102-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="a9102-168">La tranche est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="a9102-168">The slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="a9102-169">Échec</span><span class="sxs-lookup"><span data-stu-id="a9102-169">Failed</span></span></td><td><span data-ttu-id="a9102-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="a9102-170">TimedOut</span></span></td><td><span data-ttu-id="a9102-171">L'exécution de l’activité a pris plus de temps que l’activité ne l’autorise.</span><span class="sxs-lookup"><span data-stu-id="a9102-171">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a9102-172">Canceled</span><span class="sxs-lookup"><span data-stu-id="a9102-172">Canceled</span></span></td><td><span data-ttu-id="a9102-173">La tranche a été annulée par l’action de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a9102-173">The slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a9102-174">Validation</span><span class="sxs-lookup"><span data-stu-id="a9102-174">Validation</span></span></td><td><span data-ttu-id="a9102-175">La validation a échoué.</span><span class="sxs-lookup"><span data-stu-id="a9102-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="a9102-176">La validation et/ou la génération de la tranche a échoué.</span><span class="sxs-lookup"><span data-stu-id="a9102-176">The slice failed to be generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="a9102-177">Ready</span><span class="sxs-lookup"><span data-stu-id="a9102-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="a9102-178">La tranche est prête à être consommée.</span><span class="sxs-lookup"><span data-stu-id="a9102-178">The slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a9102-179">Ignoré</span><span class="sxs-lookup"><span data-stu-id="a9102-179">Skipped</span></span></td><td><span data-ttu-id="a9102-180">Aucun</span><span class="sxs-lookup"><span data-stu-id="a9102-180">None</span></span></td><td><span data-ttu-id="a9102-181">La tranche n’est pas en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="a9102-181">The slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a9102-182">Aucun</span><span class="sxs-lookup"><span data-stu-id="a9102-182">None</span></span></td><td>-</td><td><span data-ttu-id="a9102-183">Tranche qui a été réinitialisée alors qu’elle existait avec un état différent.</span><span class="sxs-lookup"><span data-stu-id="a9102-183">A slice used to exist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="a9102-184">Vous pouvez afficher les détails relatifs à une tranche en cliquant sur une entrée de tranche dans le panneau **Tranches mises à jour récemment**.</span><span class="sxs-lookup"><span data-stu-id="a9102-184">You can view the details about a slice by clicking a slice entry on the **Recently Updated Slices** blade.</span></span>

![Détails de la tranche](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="a9102-186">Si la tranche a été exécutée plusieurs fois, plusieurs lignes s’affichent dans la liste **Exécutions d’activité** .</span><span class="sxs-lookup"><span data-stu-id="a9102-186">If the slice has been executed multiple times, you see multiple rows in the **Activity runs** list.</span></span> <span data-ttu-id="a9102-187">Vous pouvez afficher des détails sur une exécution d’activité en cliquant sur l’entrée d’exécution dans la liste **Exécutions de l’activité**.</span><span class="sxs-lookup"><span data-stu-id="a9102-187">You can view details about an activity run by clicking the run entry in the **Activity runs** list.</span></span> <span data-ttu-id="a9102-188">Tous les fichiers journaux, ainsi que le message d’erreur associé, le cas échéant, s’affichent.</span><span class="sxs-lookup"><span data-stu-id="a9102-188">The list shows all the log files, along with an error message if there is one.</span></span> <span data-ttu-id="a9102-189">Cette fonctionnalité est utile et pour cause. Vous visualisez et déboguez les journaux sans le souci de quitter votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="a9102-189">This feature is useful to view and debug logs without having to leave your data factory.</span></span>

![Détails de l'exécution d'activité](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="a9102-191">Si la tranche n’a pas l’état **Prêt**, vous pouvez voir les tranches en amont qui ne sont pas prêtes et qui empêchent l’exécution de la tranche actuelle dans la liste **Tranches en amont qui ne sont pas prêtes**.</span><span class="sxs-lookup"><span data-stu-id="a9102-191">If the slice isn't in the **Ready** state, you can see the upstream slices that aren't ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="a9102-192">Cette fonctionnalité est utile lorsque votre tranche présente l’état **En attente** et que vous voulez connaître les dépendances en amont à l’origine de cette attente.</span><span class="sxs-lookup"><span data-stu-id="a9102-192">This feature is useful when your slice is in **Waiting** state and you want to understand the upstream dependencies that the slice is waiting on.</span></span>

![Tranches en amont qui ne sont pas prêtes](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="a9102-194">Schéma d’état de jeux de données</span><span class="sxs-lookup"><span data-stu-id="a9102-194">Dataset state diagram</span></span>
<span data-ttu-id="a9102-195">Quand vous avez déployé une fabrique de données et que la période d’activation des pipelines est valide, les tranches de données des jeux de données passent d’un état à un autre.</span><span class="sxs-lookup"><span data-stu-id="a9102-195">After you deploy a data factory and the pipelines have a valid active period, the dataset slices transition from one state to another.</span></span> <span data-ttu-id="a9102-196">Actuellement, l’état de la tranche suit le schéma d’état suivant :</span><span class="sxs-lookup"><span data-stu-id="a9102-196">Currently, the slice status follows the following state diagram:</span></span>

![Schéma d'état](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="a9102-198">Le flux de transition d’états des jeux de données de la fabrique de données est le suivant : En attente -> En cours/En cours (Validation) -> Prête/Échec.</span><span class="sxs-lookup"><span data-stu-id="a9102-198">The dataset state transition flow in data factory is the following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="a9102-199">Au départ, la tranche a l’état **En attente**, en attente des conditions requises à respecter avant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="a9102-199">The slice starts in a **Waiting** state, waiting for preconditions to be met before it executes.</span></span> <span data-ttu-id="a9102-200">Ensuite, l’exécution de l’activité commence, et la tranche passe à l’état **En cours**.</span><span class="sxs-lookup"><span data-stu-id="a9102-200">Then, the activity starts executing, and the slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="a9102-201">L’exécution de l’activité peut réussir ou échouer.</span><span class="sxs-lookup"><span data-stu-id="a9102-201">The activity execution might succeed or fail.</span></span> <span data-ttu-id="a9102-202">Selon le résultat de l’exécution, l’état de la tranche est **Prête** ou **Échec**.</span><span class="sxs-lookup"><span data-stu-id="a9102-202">The slice is marked as **Ready** or **Failed**, based on the result of the execution.</span></span>

<span data-ttu-id="a9102-203">Vous pouvez réinitialiser la tranche pour revenir de l’état **Prête** ou **Échec** à l’état **En attente**.</span><span class="sxs-lookup"><span data-stu-id="a9102-203">You can reset the slice to go back from the **Ready** or **Failed** state to the **Waiting** state.</span></span> <span data-ttu-id="a9102-204">Vous pouvez également définir l’état de la tranche sur **Ignorer** pour empêcher l’exécution de l’activité et ne pas traiter la tranche.</span><span class="sxs-lookup"><span data-stu-id="a9102-204">You can also mark the slice state to **Skip**, which prevents the activity from executing and not processing the slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="a9102-205">Suspension et reprise des pipelines</span><span class="sxs-lookup"><span data-stu-id="a9102-205">Pause and resume pipelines</span></span>
<span data-ttu-id="a9102-206">Vous pouvez gérer vos pipelines à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9102-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="a9102-207">Par exemple, vous pouvez suspendre et reprendre les pipelines en exécutant les applets de commande Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9102-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="a9102-208">La vue schématique ne prend pas en charge la suspension et la reprise des pipelines.</span><span class="sxs-lookup"><span data-stu-id="a9102-208">The diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="a9102-209">Si vous souhaitez utiliser une interface utilisateur, utilisez l’application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="a9102-209">If you want to use an user interface, use the monitoring and managing application.</span></span> <span data-ttu-id="a9102-210">Pour en savoir plus sur l’utilisation de l’application, consultez l’article [Surveiller et gérer les pipelines Azure Data Factory à l’aide de l’application de surveillance et gestion](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="a9102-210">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="a9102-211">Vous pouvez suspendre l’exécution des pipelines à l’aide de l’applet de commande PowerShell **Suspend-AzureRmDataFactoryPipeline**.</span><span class="sxs-lookup"><span data-stu-id="a9102-211">You can pause/suspend pipelines by using the **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="a9102-212">Cette applet de commande est utile lorsque vous ne voulez pas exécuter vos pipelines jusqu'à ce qu’un problème est résolu.</span><span class="sxs-lookup"><span data-stu-id="a9102-212">This cmdlet is useful when you don’t want to run your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="a9102-213">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a9102-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="a9102-214">Une fois le problème résolu au niveau du pipeline, vous pouvez reprendre le pipeline suspendu en exécutant la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="a9102-214">After the issue has been fixed with the pipeline, you can resume the suspended pipeline by running the following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="a9102-215">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a9102-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="a9102-216">Débogage de pipelines</span><span class="sxs-lookup"><span data-stu-id="a9102-216">Debug pipelines</span></span>
<span data-ttu-id="a9102-217">Azure Data Factory offre des fonctionnalités exceptionnelles pour déboguer et résoudre les problèmes des pipelines via le portail Azure et Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9102-217">Azure Data Factory provides rich capabilities for you to debug and troubleshoot pipelines by using the Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="a9102-218">[!Remarque} Il est beaucoup plus facile de résoudre les erreurs à l’aide de l’application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="a9102-218">[!NOTE} It is much easier to troubleshot errors using the Monitoring & Management App.</span></span> <span data-ttu-id="a9102-219">Pour en savoir plus sur l’utilisation de l’application, consultez l’article [Surveiller et gérer les pipelines Azure Data Factory à l’aide de l’application de surveillance et gestion](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="a9102-219">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="a9102-220">Recherche d’erreurs dans un pipeline</span><span class="sxs-lookup"><span data-stu-id="a9102-220">Find errors in a pipeline</span></span>
<span data-ttu-id="a9102-221">En cas d’échec d’exécution de l’activité dans un pipeline, le jeu de données généré par celui-ci est alors en état d’erreur.</span><span class="sxs-lookup"><span data-stu-id="a9102-221">If the activity run fails in a pipeline, the dataset that is produced by the pipeline is in an error state because of the failure.</span></span> <span data-ttu-id="a9102-222">Vous pouvez déboguer et corriger les erreurs dans Azure Data Factory à l’aide des méthodes suivantes.</span><span class="sxs-lookup"><span data-stu-id="a9102-222">You can debug and troubleshoot errors in Azure Data Factory by using the following methods.</span></span>

#### <a name="use-the-azure-portal-to-debug-an-error"></a><span data-ttu-id="a9102-223">Utiliser le portail Azure pour déboguer une erreur</span><span class="sxs-lookup"><span data-stu-id="a9102-223">Use the Azure portal to debug an error</span></span>
1. <span data-ttu-id="a9102-224">Dans le panneau **Table**, cliquez sur la tranche qui pose problème, dont **l’état** est défini sur **Échec**.</span><span class="sxs-lookup"><span data-stu-id="a9102-224">On the **Table** blade, click the problem slice that has the **Status** set to **Failed**.</span></span>

   ![Panneau de table avec tranche problématique](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="a9102-226">Dans le panneau **Tranche de données**, cliquez sur l’exécution d’activité qui a échoué.</span><span class="sxs-lookup"><span data-stu-id="a9102-226">On the **Data slice** blade, click the activity run that failed.</span></span>

   ![Tranche de données avec une erreur](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="a9102-228">Dans le panneau **Détails sur l’exécution d’activité**, vous pouvez télécharger les fichiers associés au traitement HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9102-228">On the **Activity run details** blade, you can download the files that are associated with the HDInsight processing.</span></span> <span data-ttu-id="a9102-229">Cliquez sur **Télécharger** pour que Status/stderr télécharge le fichier journal d’erreur qui contient les détails sur l’erreur.</span><span class="sxs-lookup"><span data-stu-id="a9102-229">Click **Download** for Status/stderr to download the error log file that contains details about the error.</span></span>

   ![Panneau de détails sur l’exécution d’activité](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-to-debug-an-error"></a><span data-ttu-id="a9102-231">Utiliser PowerShell pour déboguer une erreur</span><span class="sxs-lookup"><span data-stu-id="a9102-231">Use PowerShell to debug an error</span></span>
1. <span data-ttu-id="a9102-232">Lancez **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a9102-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="a9102-233">Exécutez la commande **Get-AzureRmDataFactorySlice** pour voir les tranches et leur état.</span><span class="sxs-lookup"><span data-stu-id="a9102-233">Run the **Get-AzureRmDataFactorySlice** command to see the slices and their statuses.</span></span> <span data-ttu-id="a9102-234">Une tranche dont l’état est **Échec**devrait apparaître.</span><span class="sxs-lookup"><span data-stu-id="a9102-234">You should see a slice with the status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="a9102-235">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a9102-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="a9102-236">Remplacez **StartDateTime** par l’heure de début de votre pipeline.</span><span class="sxs-lookup"><span data-stu-id="a9102-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="a9102-237">Exécutez maintenant l’applet de commande **Get-AzureRmDataFactoryRun** pour obtenir des détails sur l’exécution de l’activité de la tranche.</span><span class="sxs-lookup"><span data-stu-id="a9102-237">Now, run the **Get-AzureRmDataFactoryRun** cmdlet to get details about the activity run for the slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="a9102-238">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a9102-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="a9102-239">La valeur de StartDateTime est l’heure de début de la tranche qui pose problème/l’erreur que vous avez notée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="a9102-239">The value of StartDateTime is the start time for the error/problem slice that you noted from the previous step.</span></span> <span data-ttu-id="a9102-240">La valeur date-heure doit être entourée de guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="a9102-240">The date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="a9102-241">Vous devez voir la sortie avec les détails sur l’erreur qui est semblable à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="a9102-241">You should see output with details about the error that is similar to the following:</span></span>

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. <span data-ttu-id="a9102-242">Vous pouvez exécuter l’applet de commande **Save-AzureRmDataFactoryLog** avec la valeur d’ID indiquée dans la sortie, et télécharger les fichiers journaux en utilisant le paramètre **-DownloadLogsoption** pour l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a9102-242">You can run the **Save-AzureRmDataFactoryLog** cmdlet with the Id value that you see from the output, and download the log files by using the **-DownloadLogsoption** for the cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="a9102-243">Réexécuter des échecs dans un pipeline</span><span class="sxs-lookup"><span data-stu-id="a9102-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9102-244">Il est plus facile de résoudre les erreurs et de réexécuter les tranches ayant échoué à l’aide de l’application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="a9102-244">It's easier to troubleshoot errors and rerun failed slices by using the Monitoring & Management App.</span></span> <span data-ttu-id="a9102-245">Pour en savoir plus sur l’utilisation de l’application, consultez [Surveiller et gérer les pipelines Azure Data Factory à l’aide de l’application de surveillance et gestion](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="a9102-245">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-the-azure-portal"></a><span data-ttu-id="a9102-246">Utilisation du portail Azure</span><span class="sxs-lookup"><span data-stu-id="a9102-246">Use the Azure portal</span></span>
<span data-ttu-id="a9102-247">Après avoir débogué et résolu les problèmes dans un pipeline, vous pouvez réexécuter ceux-ci en accédant à la tranche qui pose problème, puis en cliquant sur le bouton **Exécuter** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="a9102-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating to the error slice and clicking the **Run** button on the command bar.</span></span>

![Réexécuter une tranche de données ayant échoué](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="a9102-249">En cas d’échec de validation de la tranche à cause d’une erreur de stratégie (p. ex. données indisponibles), vous pouvez résoudre le problème et relancer la validation en cliquant sur le bouton **Valider** de la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="a9102-249">In case the slice has failed validation because of a policy failure (for example, if data isn't available), you can fix the failure and validate again by clicking the **Validate** button on the command bar.</span></span>

![Corriger les erreurs et valider](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="a9102-251">Utilisation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9102-251">Use Azure PowerShell</span></span>
<span data-ttu-id="a9102-252">Vous pouvez réexécuter des problèmes à l’aide de l’applet de commande **Set-AzureRmDataFactorySliceStatus**.</span><span class="sxs-lookup"><span data-stu-id="a9102-252">You can rerun failures by using the **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="a9102-253">Consultez la rubrique [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) pour la syntaxe et pour plus d’informations sur l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a9102-253">See the [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about the cmdlet.</span></span>

<span data-ttu-id="a9102-254">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="a9102-254">**Example:**</span></span>

<span data-ttu-id="a9102-255">L’exemple suivant définit l’état de toutes les tranches de la table « DAWikiAggregatedData » sur « En attente » dans la fabrique de données Azure « WikiADF ».</span><span class="sxs-lookup"><span data-stu-id="a9102-255">The following example sets the status of all slices for the table 'DAWikiAggregatedData' to 'Waiting' in the Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="a9102-256">« UpdateType » est défini sur « UpstreamInPipeline ». Concrètement, l’état « En attente » est défini pour chaque tranche de la table et toutes les tables (en amont) dépendantes.</span><span class="sxs-lookup"><span data-stu-id="a9102-256">The 'UpdateType' is set to 'UpstreamInPipeline', which means that statuses of each slice for the table and all the dependent (upstream) tables are set to 'Waiting'.</span></span> <span data-ttu-id="a9102-257">Sinon, la valeur « Individuel » pour ce paramètre est également possible.</span><span class="sxs-lookup"><span data-stu-id="a9102-257">The other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="a9102-258">Créez des alertes</span><span class="sxs-lookup"><span data-stu-id="a9102-258">Create alerts</span></span>
<span data-ttu-id="a9102-259">Azure consigne les événements utilisateur lorsqu'une ressource Azure (par exemple, une fabrique de données) est créée, mise à jour ou supprimée.</span><span class="sxs-lookup"><span data-stu-id="a9102-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="a9102-260">Vous pouvez créer des alertes relatives à ces événements.</span><span class="sxs-lookup"><span data-stu-id="a9102-260">You can create alerts on these events.</span></span> <span data-ttu-id="a9102-261">Vous pouvez utiliser Data Factory pour capturer différentes mesures et créer des alertes associées.</span><span class="sxs-lookup"><span data-stu-id="a9102-261">You can use Data Factory to capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="a9102-262">Nous vous recommandons d’utiliser les événements pour obtenir une surveillance en temps réel et les mesures à des fins d’historique.</span><span class="sxs-lookup"><span data-stu-id="a9102-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="a9102-263">Alertes relatives à des événements</span><span class="sxs-lookup"><span data-stu-id="a9102-263">Alerts on events</span></span>
<span data-ttu-id="a9102-264">Les événements Azure fournissent des explications utiles sur ce qui se passe dans vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="a9102-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="a9102-265">Lorsque vous utilisez Azure Data Factory, les événements sont générés quand :</span><span class="sxs-lookup"><span data-stu-id="a9102-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="a9102-266">Une fabrique de données est créée, mise à jour ou supprimée.</span><span class="sxs-lookup"><span data-stu-id="a9102-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="a9102-267">Le traitement des données (les « exécutions ») est démarré ou terminé.</span><span class="sxs-lookup"><span data-stu-id="a9102-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="a9102-268">Un cluster HDInsight à la demande est créé ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="a9102-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="a9102-269">Vous pouvez créer des alertes relatives à ces événements utilisateur et les configurer pour envoyer des notifications par courrier électronique à l’administrateur et aux coadministrateurs de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a9102-269">You can create alerts on these user events and configure them to send email notifications to the administrator and coadministrators of the subscription.</span></span> <span data-ttu-id="a9102-270">De plus, vous pouvez spécifier des adresses de messagerie supplémentaires pour les utilisateurs devant recevoir des notifications par courrier électronique lorsque les conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="a9102-270">In addition, you can specify additional email addresses of users who need to receive email notifications when the conditions are met.</span></span> <span data-ttu-id="a9102-271">Cette fonctionnalité est très utile lorsque vous souhaitez être averti en cas d’échec et que vous ne souhaitez pas surveiller en continu votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="a9102-271">This feature is useful when you want to get notified on failures and don’t want to continuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="a9102-272">Actuellement, le portail n’affiche pas les alertes sur les événements.</span><span class="sxs-lookup"><span data-stu-id="a9102-272">Currently, the portal doesn't show alerts on events.</span></span> <span data-ttu-id="a9102-273">Utilisez [l’Application de surveillance et gestion](data-factory-monitor-manage-app.md) pour afficher toutes les alertes.</span><span class="sxs-lookup"><span data-stu-id="a9102-273">Use the [Monitoring and Management app](data-factory-monitor-manage-app.md) to see all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="a9102-274">Spécifier une définition d’alerte</span><span class="sxs-lookup"><span data-stu-id="a9102-274">Specify an alert definition</span></span>
<span data-ttu-id="a9102-275">Pour spécifier une définition d’alerte, vous devez créer un fichier JSON qui décrit les opérations pour lesquelles vous souhaitez être alerté.</span><span class="sxs-lookup"><span data-stu-id="a9102-275">To specify an alert definition, you create a JSON file that describes the operations that you want to be alerted on.</span></span> <span data-ttu-id="a9102-276">Dans l'exemple suivant, l'alerte envoie une notification par courrier électronique pour l’opération RunFinished.</span><span class="sxs-lookup"><span data-stu-id="a9102-276">In the following example, the alert sends an email notification for the RunFinished operation.</span></span> <span data-ttu-id="a9102-277">Pour être plus précis, une notification par courrier électronique est envoyée lorsqu'une exécution de la fabrique de données est terminée en ayant échoué (État = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="a9102-277">To be specific, an email notification is sent when a run in the data factory has completed and the run has failed (Status = FailedExecution).</span></span>

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of the data slices for the Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

<span data-ttu-id="a9102-278">Si vous ne voulez pas recevoir d’alerte relative à un problème spécifique, vous pouvez supprimer **subStatus** de la définition JSON ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a9102-278">You can remove **subStatus** from the JSON definition if you don’t want to be alerted on a specific failure.</span></span>

<span data-ttu-id="a9102-279">L'exemple ci-dessus définit l'alerte de toutes les fabriques de données de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="a9102-279">This example sets up the alert for all data factories in your subscription.</span></span> <span data-ttu-id="a9102-280">Si vous souhaitez configurer l’alerte pour une fabrique de données particulière, vous pouvez spécifier la fabrique de données **resourceUri** dans le bloc **dataSource** :</span><span class="sxs-lookup"><span data-stu-id="a9102-280">If you want the alert to be set up for a particular data factory, you can specify data factory **resourceUri** in the **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="a9102-281">Le tableau suivant dresse la liste des opérations et des états (et états secondaires) disponibles.</span><span class="sxs-lookup"><span data-stu-id="a9102-281">The following table provides the list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="a9102-282">Nom d’opération</span><span class="sxs-lookup"><span data-stu-id="a9102-282">Operation name</span></span> | <span data-ttu-id="a9102-283">État</span><span class="sxs-lookup"><span data-stu-id="a9102-283">Status</span></span> | <span data-ttu-id="a9102-284">État secondaire</span><span class="sxs-lookup"><span data-stu-id="a9102-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9102-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="a9102-285">RunStarted</span></span> |<span data-ttu-id="a9102-286">Démarré</span><span class="sxs-lookup"><span data-stu-id="a9102-286">Started</span></span> |<span data-ttu-id="a9102-287">Starting</span><span class="sxs-lookup"><span data-stu-id="a9102-287">Starting</span></span> |
| <span data-ttu-id="a9102-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="a9102-288">RunFinished</span></span> |<span data-ttu-id="a9102-289">Failed / Succeeded</span><span class="sxs-lookup"><span data-stu-id="a9102-289">Failed / Succeeded</span></span> |<span data-ttu-id="a9102-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="a9102-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="a9102-291">Succeeded</span><span class="sxs-lookup"><span data-stu-id="a9102-291">Succeeded</span></span><br/><br/><span data-ttu-id="a9102-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="a9102-292">FailedExecution</span></span><br/><br/><span data-ttu-id="a9102-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="a9102-293">TimedOut</span></span><br/><br/><span data-ttu-id="a9102-294"><Canceled</span><span class="sxs-lookup"><span data-stu-id="a9102-294"><Canceled</span></span><br/><br/><span data-ttu-id="a9102-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="a9102-295">FailedValidation</span></span><br/><br/><span data-ttu-id="a9102-296">Abandonné</span><span class="sxs-lookup"><span data-stu-id="a9102-296">Abandoned</span></span> |
| <span data-ttu-id="a9102-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="a9102-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="a9102-298">Démarré</span><span class="sxs-lookup"><span data-stu-id="a9102-298">Started</span></span> | |
| <span data-ttu-id="a9102-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="a9102-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="a9102-300">Réussi</span><span class="sxs-lookup"><span data-stu-id="a9102-300">Succeeded</span></span> | |
| <span data-ttu-id="a9102-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="a9102-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="a9102-302">Réussi</span><span class="sxs-lookup"><span data-stu-id="a9102-302">Succeeded</span></span> | |

<span data-ttu-id="a9102-303">Consultez [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) (Créer une règle d’alerte) pour plus d’informations sur les éléments JSON utilisés dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="a9102-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about the JSON elements that are used in the example.</span></span>

#### <a name="deploy-the-alert"></a><span data-ttu-id="a9102-304">Déployer l’alerte</span><span class="sxs-lookup"><span data-stu-id="a9102-304">Deploy the alert</span></span>
<span data-ttu-id="a9102-305">Pour déployer l’alerte, utilisez l’applet de commande Azure PowerShell **New-AzureRmResourceGroupDeployment**, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a9102-305">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="a9102-306">Une fois le déploiement du groupe de ressources terminé, les messages suivants s’affichent :</span><span class="sxs-lookup"><span data-stu-id="a9102-306">After the resource group deployment has finished successfully, you see the following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - The StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts to remove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> <span data-ttu-id="a9102-307">Vous pouvez utiliser l’API REST [Créer une règle d’alerte](https://msdn.microsoft.com/library/azure/dn510366.aspx) pour créer une règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="a9102-307">You can use the [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API to create an alert rule.</span></span> <span data-ttu-id="a9102-308">La charge utile JSON est similaire à l’exemple JSON.</span><span class="sxs-lookup"><span data-stu-id="a9102-308">The JSON payload is similar to the JSON example.</span></span>  


#### <a name="retrieve-the-list-of-azure-resource-group-deployments"></a><span data-ttu-id="a9102-309">Récupérer la liste des déploiements de groupes de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="a9102-309">Retrieve the list of Azure resource group deployments</span></span>
<span data-ttu-id="a9102-310">Pour récupérer la liste des déploiements de groupes de ressources Azure, utilisez l’applet de commande **Get-AzureRmResourceGroupDeployment**, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a9102-310">To retrieve the list of deployed Azure resource group deployments, use the cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="a9102-311">Résoudre les problèmes relatifs aux événements utilisateur</span><span class="sxs-lookup"><span data-stu-id="a9102-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="a9102-312">Vous pouvez voir tous les événements générés après avoir cliqué sur la mosaïque **Mesures et opérations**.</span><span class="sxs-lookup"><span data-stu-id="a9102-312">You can see all the events that are generated after clicking the **Metrics and operations** tile.</span></span>

    ![Vignette Mesures et opérations](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="a9102-314">Cliquez sur la mosaïque **Événements** pour afficher les événements.</span><span class="sxs-lookup"><span data-stu-id="a9102-314">Click the **Events** tile to see the events.</span></span>

    ![Vignette d'événements](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="a9102-316">Dans le panneau **Événements**, vous pouvez consulter des détails sur les événements, les événements filtrés, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="a9102-316">On the **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Panneau Événements](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="a9102-318">Dans la liste des opérations, cliquez sur une **opération** à l’origine d’une erreur.</span><span class="sxs-lookup"><span data-stu-id="a9102-318">Click an **Operation** in the operations list that causes an error.</span></span>

    ![Sélectionner une opération](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="a9102-320">Pour afficher des détails sur l’erreur, cliquez sur un événement **Erreur**.</span><span class="sxs-lookup"><span data-stu-id="a9102-320">Click an **Error** event to see details about the error.</span></span>

    ![Événement erreur](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="a9102-322">Consultez l’article [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) (Applets de commande Azure Insight) pour plus d’informations sur les applets de commande PowerShell que vous pouvez utiliser pour ajouter, obtenir ou supprimer des alertes.</span><span class="sxs-lookup"><span data-stu-id="a9102-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use to add, get, or remove alerts.</span></span> <span data-ttu-id="a9102-323">Voici quelques exemples d’utilisation de l’applet de commande **Get-AlertRule** :</span><span class="sxs-lookup"><span data-stu-id="a9102-323">Here are a few examples of using the **Get-AlertRule** cmdlet:</span></span>

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of the data slices for the Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

<span data-ttu-id="a9102-324">Exécutez les commandes get-help suivantes afinb d’afficher des détails et des exemples pour l'applet de commande Get-AlertRule.</span><span class="sxs-lookup"><span data-stu-id="a9102-324">Run the following get-help commands to see details and examples for the Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="a9102-325">Si des événements de génération d’alertes apparaissent sur le panneau du portail, mais que vous ne recevez pas de notification par courrier électronique, vérifiez que votre adresse e-mail est bien configurée de manière à recevoir des messages de la part d’expéditeurs externes.</span><span class="sxs-lookup"><span data-stu-id="a9102-325">If you see the alert generation events on the portal blade but you don't receive email notifications, check whether the email address that is specified is set to receive emails from external senders.</span></span> <span data-ttu-id="a9102-326">Les alertes par courrier électronique peuvent avoir été bloquées en raison de vos paramètres de messagerie.</span><span class="sxs-lookup"><span data-stu-id="a9102-326">The alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="a9102-327">Alertes relatives à des mesures</span><span class="sxs-lookup"><span data-stu-id="a9102-327">Alerts on metrics</span></span>
<span data-ttu-id="a9102-328">Dans Data Factory, vous pouvez capturer différentes mesures et créer des alertes associées.</span><span class="sxs-lookup"><span data-stu-id="a9102-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="a9102-329">Vous pouvez surveiller et créer des alertes relatives aux mesures suivantes pour les tranches de votre fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="a9102-329">You can monitor and create alerts on the following metrics for the slices in your data factory:</span></span>

* <span data-ttu-id="a9102-330">**Exécutions échouées**</span><span class="sxs-lookup"><span data-stu-id="a9102-330">**Failed Runs**</span></span>
* <span data-ttu-id="a9102-331">**Exécutions réussies**</span><span class="sxs-lookup"><span data-stu-id="a9102-331">**Successful Runs**</span></span>

<span data-ttu-id="a9102-332">Ces mesures sont utiles et vous permettent d’obtenir une vue d’ensemble globale des exécutions réussies et échouées dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="a9102-332">These metrics are useful and help you to get an overview of overall failed and successful runs in the data factory.</span></span> <span data-ttu-id="a9102-333">Des mesures sont émises lors de chaque exécution de tranche de données.</span><span class="sxs-lookup"><span data-stu-id="a9102-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="a9102-334">Toutes les heures, ces mesures sont agrégées et transférées dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a9102-334">At the beginning of the hour, these metrics are aggregated and pushed to your storage account.</span></span> <span data-ttu-id="a9102-335">Pour activer les mesures, configurez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a9102-335">To enable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="a9102-336">Activer les mesures</span><span class="sxs-lookup"><span data-stu-id="a9102-336">Enable metrics</span></span>
<span data-ttu-id="a9102-337">Pour activer les mesures, cliquez sur ce qui suit à partir du panneau **Data Factory** :</span><span class="sxs-lookup"><span data-stu-id="a9102-337">To enable metrics, click the following from the **Data Factory** blade:</span></span>

<span data-ttu-id="a9102-338">**Analyse** > **Mesures** > **Paramètres de diagnostic** > **Diagnostics**</span><span class="sxs-lookup"><span data-stu-id="a9102-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Lien Diagnostics](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="a9102-340">Dans le panneau **Diagnostics**, cliquez sur **Activé**, sélectionnez le compte de stockage, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a9102-340">On the **Diagnostics** blade, click **On**, select the storage account, and click **Save**.</span></span>

![Panneau Diagnostics](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="a9102-342">Vous devrez peut-être attendre une heure maximum avant que les mesures ne soient visibles dans le panneau **Analyse**. En effet, l’agrégation des mesures s’effectue une fois par heure.</span><span class="sxs-lookup"><span data-stu-id="a9102-342">It might take up to one hour for the metrics to be visible on the **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="a9102-343">Configurer une alerte relative à des mesures</span><span class="sxs-lookup"><span data-stu-id="a9102-343">Set up an alert on metrics</span></span>
<span data-ttu-id="a9102-344">Cliquez sur la mosaïque **Mesures de fabrique de données** :</span><span class="sxs-lookup"><span data-stu-id="a9102-344">Click the **Data Factory metrics** tile:</span></span>

![Vignette Mesures de fabrique de données](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="a9102-346">Dans le panneau **Mesures**, dans la barre d’outils, cliquez sur **+ Ajouter une alerte**.</span><span class="sxs-lookup"><span data-stu-id="a9102-346">On the **Metric** blade, click **+ Add alert** on the toolbar.</span></span>
<span data-ttu-id="a9102-347">![Panneau Mesures de fabrique de données > Ajouter une alerte](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="a9102-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="a9102-348">Dans la page **Ajouter une règle d’alerte**, procédez comme suit, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9102-348">On the **Add an alert rule** page, do the following steps, and click **OK**.</span></span>

* <span data-ttu-id="a9102-349">Entrez un nom pour l’alerte (p. ex. « alerte d’échec »).</span><span class="sxs-lookup"><span data-stu-id="a9102-349">Enter a name for the alert (example: "failed alert").</span></span>
* <span data-ttu-id="a9102-350">Entrez une description pour l’alerte (p. ex. « envoyer un courrier électronique en cas d’échec »).</span><span class="sxs-lookup"><span data-stu-id="a9102-350">Enter a description for the alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="a9102-351">Sélectionnez une mesure (« exécutions échouées » ou « exécutions réussies »).</span><span class="sxs-lookup"><span data-stu-id="a9102-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="a9102-352">Spécifiez une condition et une valeur de seuil.</span><span class="sxs-lookup"><span data-stu-id="a9102-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="a9102-353">Spécifiez la période.</span><span class="sxs-lookup"><span data-stu-id="a9102-353">Specify the period of time.</span></span>
* <span data-ttu-id="a9102-354">Spécifiez si un courrier électronique doit être envoyé aux propriétaires, aux collaborateurs et aux lecteurs.</span><span class="sxs-lookup"><span data-stu-id="a9102-354">Specify whether an email should be sent to owners, contributors, and readers.</span></span>

![Panneau Mesures de fabrique de données > Ajouter une règle d’alerte](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="a9102-356">Une fois la règle d’alerte correctement ajoutée, le panneau se ferme et la nouvelle alerte s’affiche dans le panneau **Mesure**.</span><span class="sxs-lookup"><span data-stu-id="a9102-356">After the alert rule is added successfully, the blade closes and you see the new alert on the **Metric** blade.</span></span>

![Panneau Mesures de fabrique de données > Nouvelle alerte ajoutée](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="a9102-358">Vous devez également voir le nombre d’alertes dans la mosaïque **Règles d’alerte**.</span><span class="sxs-lookup"><span data-stu-id="a9102-358">You should also see the number of alerts in the **Alert rules** tile.</span></span> <span data-ttu-id="a9102-359">Cliquez sur la mosaïque **Règles d’alerte**.</span><span class="sxs-lookup"><span data-stu-id="a9102-359">Click the **Alert rules** tile.</span></span>

![Panneau Mesures de fabrique de données - Règles d’alerte](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="a9102-361">Dans le panneau **Règles d’alerte**, vous voyez les alertes existantes.</span><span class="sxs-lookup"><span data-stu-id="a9102-361">On the **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="a9102-362">Pour ajouter une alerte, dans la barre d’outils, cliquez sur **Ajouter une alerte**.</span><span class="sxs-lookup"><span data-stu-id="a9102-362">To add an alert, click **Add alert** on the toolbar.</span></span>

![Panneau Règles d’alerte](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="a9102-364">Notifications d’alerte</span><span class="sxs-lookup"><span data-stu-id="a9102-364">Alert notifications</span></span>
<span data-ttu-id="a9102-365">Une fois que la règle d’alerte correspond à la condition,vous devez recevoir un courrier électronique vous informant que l’alerte est activée.</span><span class="sxs-lookup"><span data-stu-id="a9102-365">After the alert rule matches the condition, you should get an email that says the alert is activated.</span></span> <span data-ttu-id="a9102-366">Une fois que le problème est résolu et que la condition d’alerte est caduque, vous recevez un courrier électronique signalant que l’alerte a été résolue.</span><span class="sxs-lookup"><span data-stu-id="a9102-366">After the issue is resolved and the alert condition doesn’t match anymore, you get an email that says the alert is resolved.</span></span>

<span data-ttu-id="a9102-367">Ce comportement se distingue des événements donnant lieu à l’envoi d’une notification dès qu’un échec correspondant à une règle d’alerte a lieu.</span><span class="sxs-lookup"><span data-stu-id="a9102-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="a9102-368">Déployer des alertes à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9102-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="a9102-369">Vous pouvez déployer des alertes relatives à des mesures de la même façon que vous le faites pour les événements.</span><span class="sxs-lookup"><span data-stu-id="a9102-369">You can deploy alerts for metrics the same way that you do for events.</span></span>

<span data-ttu-id="a9102-370">**Définition d’alerte**</span><span class="sxs-lookup"><span data-stu-id="a9102-370">**Alert definition**</span></span>

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

<span data-ttu-id="a9102-371">Remplacez les valeurs de *subscriptionId*, *resourceGroupName* et *dataFactoryName* figurant dans l’exemple par des valeurs appropriées.</span><span class="sxs-lookup"><span data-stu-id="a9102-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in the sample with appropriate values.</span></span>

<span data-ttu-id="a9102-372">*metricName* prend actuellement en charge deux valeurs :</span><span class="sxs-lookup"><span data-stu-id="a9102-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="a9102-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="a9102-373">FailedRuns</span></span>
* <span data-ttu-id="a9102-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="a9102-374">SuccessfulRuns</span></span>

<span data-ttu-id="a9102-375">**Déployer l’alerte**</span><span class="sxs-lookup"><span data-stu-id="a9102-375">**Deploy the alert**</span></span>

<span data-ttu-id="a9102-376">Pour déployer l’alerte, utilisez l’applet de commande Azure PowerShell **New-AzureRmResourceGroupDeployment**, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a9102-376">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="a9102-377">Le message suivant devrait s’afficher après la réussite du déploiement :</span><span class="sxs-lookup"><span data-stu-id="a9102-377">You should see following message after a successful deployment:</span></span>

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

<span data-ttu-id="a9102-378">Vous pouvez également utiliser l’applet de commande **Add-AlertRule** pour déployer une règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="a9102-378">You can also use the **Add-AlertRule** cmdlet to deploy an alert rule.</span></span> <span data-ttu-id="a9102-379">Consultez la rubrique [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) pour obtenir plus d’informations et des exemples.</span><span class="sxs-lookup"><span data-stu-id="a9102-379">See the [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-to-a-different-resource-group-or-subscription"></a><span data-ttu-id="a9102-380">Déplacer une fabrique de données vers un autre groupe de ressources ou abonnement</span><span class="sxs-lookup"><span data-stu-id="a9102-380">Move a data factory to a different resource group or subscription</span></span>
<span data-ttu-id="a9102-381">Vous pouvez déplacer une fabrique de données vers un autre groupe de ressources ou abonnement à l’aide du bouton de la barre de commandes **Déplacer** situé sur la page d’accueil de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="a9102-381">You can move a data factory to a different resource group or a different subscription by using the **Move** command bar button on the home page of your data factory.</span></span>

![Déplacer la fabrique de données](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="a9102-383">Vous pouvez également déplacer toutes les ressources associées (notamment les alertes associées à la fabrique de données) en même temps que la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="a9102-383">You can also move any related resources (such as alerts that are associated with the data factory), along with the data factory.</span></span>

![Boîte de dialogue Déplacer des ressources](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
