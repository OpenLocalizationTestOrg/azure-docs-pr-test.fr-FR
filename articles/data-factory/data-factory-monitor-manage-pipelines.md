---
title: "aaaMonitor et gérer des pipelines à l’aide de hello portail Azure et PowerShell | Documents Microsoft"
description: "Découvrez comment toouse hello portail Azure et Azure PowerShell toomonitor et gérer des fabriques de données Azure hello et pipelines que vous avez créés."
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
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a><span data-ttu-id="62d20-103">Surveiller et gérer les pipelines Azure Data Factory à l’aide de hello portail Azure et PowerShell</span><span class="sxs-lookup"><span data-stu-id="62d20-103">Monitor and manage Azure Data Factory pipelines by using hello Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62d20-104">Utilisation du portail Azure/d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="62d20-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="62d20-105">Utilisation de l’application de surveillance et gestion</span><span class="sxs-lookup"><span data-stu-id="62d20-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="62d20-106">application de gestion et d’analyse Hello fournit une meilleure prise en charge pour l’analyse et la gestion de vos pipelines de données et les problèmes de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="62d20-106">hello monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="62d20-107">Pour plus d’informations sur l’utilisation d’application hello, consultez [surveiller et gérer des pipelines de fabrique de données à l’aide d’application de gestion et de surveillance hello](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="62d20-107">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="62d20-108">Cet article décrit comment toomonitor, gérer et déboguer vos pipelines à l’aide de PowerShell et le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="62d20-108">This article describes how toomonitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="62d20-109">Hello fournit également des informations sur les alertes toocreate et obtenir informées des échecs.</span><span class="sxs-lookup"><span data-stu-id="62d20-109">hello article also provides information on how toocreate alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="62d20-110">Présentation des pipelines et des états d’activité</span><span class="sxs-lookup"><span data-stu-id="62d20-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="62d20-111">À l’aide de hello portail Azure, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="62d20-111">By using hello Azure portal, you can:</span></span>

* <span data-ttu-id="62d20-112">Afficher votre fabrique de données sous forme de schéma.</span><span class="sxs-lookup"><span data-stu-id="62d20-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="62d20-113">Afficher les activités à l’intérieur d’un pipeline.</span><span class="sxs-lookup"><span data-stu-id="62d20-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="62d20-114">Afficher des jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="62d20-114">View input and output datasets.</span></span>

<span data-ttu-id="62d20-115">Cette section décrit également comment une tranche du jeu de données passe à partir d’un état de tooanother.</span><span class="sxs-lookup"><span data-stu-id="62d20-115">This section also describes how a dataset slice transitions from one state tooanother state.</span></span>   

### <a name="navigate-tooyour-data-factory"></a><span data-ttu-id="62d20-116">Accédez de fabrique de données tooyour</span><span class="sxs-lookup"><span data-stu-id="62d20-116">Navigate tooyour data factory</span></span>
1. <span data-ttu-id="62d20-117">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="62d20-117">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="62d20-118">Cliquez sur **fabriques de données** dans menu hello hello gauche.</span><span class="sxs-lookup"><span data-stu-id="62d20-118">Click **Data factories** on hello menu on hello left.</span></span> <span data-ttu-id="62d20-119">Si vous ne le voyez pas, cliquez sur **davantage de services >**, puis cliquez sur **fabriques de données** sous hello **INTELLIGENCE + ANALYTICS** catégorie.</span><span class="sxs-lookup"><span data-stu-id="62d20-119">If you don't see it, click **More services >**, and then click **Data factories** under hello **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Parcourir tout > Fabriques de données](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="62d20-121">Sur hello **fabriques de données** panneau, la fabrique de données Sélectionnez hello qui vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="62d20-121">On hello **Data factories** blade, select hello data factory that you're interested in.</span></span>

    ![Sélectionner une fabrique de données](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="62d20-123">Vous devez voir la page d’accueil hello de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-123">You should see hello home page for hello data factory.</span></span>

   ![Panneau Data Factory](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="62d20-125">Vue schématique de votre fabrique de données</span><span class="sxs-lookup"><span data-stu-id="62d20-125">Diagram view of your data factory</span></span>
<span data-ttu-id="62d20-126">Hello **diagramme** vue d’une fabrique de données fournit un volet de verre toomonitor et gérer hello data factory et ses composants.</span><span class="sxs-lookup"><span data-stu-id="62d20-126">hello **Diagram** view of a data factory provides a single pane of glass toomonitor and manage hello data factory and its assets.</span></span> <span data-ttu-id="62d20-127">toosee hello **diagramme** afficher votre fabrique de données, cliquez sur **diagramme** sur la page d’accueil hello de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-127">toosee hello **Diagram** view of your data factory, click **Diagram** on hello home page for hello data factory.</span></span>

![Vue schématique](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="62d20-129">Vous pouvez faire un zoom, effectuer un zoom arrière, zoom toofit, zoom too100 %, disposition de hello de verrou de schéma de hello et positionnez automatiquement les pipelines et les jeux de données.</span><span class="sxs-lookup"><span data-stu-id="62d20-129">You can zoom in, zoom out, zoom toofit, zoom too100%, lock hello layout of hello diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="62d20-130">Vous pouvez également voir les informations de lignage des données hello (autrement dit, afficher les éléments en amont et en aval des éléments sélectionnés).</span><span class="sxs-lookup"><span data-stu-id="62d20-130">You can also see hello data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="62d20-131">Activités à l'intérieur d'un pipeline</span><span class="sxs-lookup"><span data-stu-id="62d20-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="62d20-132">Pipeline de hello d’avec le bouton droit, puis cliquez sur **ouvrir pipeline** toosee toutes les activités de hello de pipeline, ainsi que des jeux de données d’entrée et de sortie pour les activités de hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-132">Right-click hello pipeline, and then click **Open pipeline** toosee all activities in hello pipeline, along with input and output datasets for hello activities.</span></span> <span data-ttu-id="62d20-133">Cette fonctionnalité est utile lorsque votre pipeline inclut plusieurs activités et que vous souhaitez lignage opérationnelle de hello toounderstand d’un pipeline unique.</span><span class="sxs-lookup"><span data-stu-id="62d20-133">This feature is useful when your pipeline includes more than one activity and you want toounderstand hello operational lineage of a single pipeline.</span></span>

    ![Menu Ouvrir un pipeline](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="62d20-135">Dans l’exemple suivant de hello, vous voyez une activité de copie dans le pipeline hello avec une entrée et une sortie.</span><span class="sxs-lookup"><span data-stu-id="62d20-135">In hello following example, you see a copy activity in hello pipeline with an input and an output.</span></span> 

    ![Activités à l'intérieur d'un pipeline](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="62d20-137">Vous pouvez naviguer de page d’accueil toohello arrière hello fabrique de données en cliquant sur hello **Data factory** lien dans la barre de navigation hello en haut à gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-137">You can navigate back toohello home page of hello data factory by clicking hello **Data factory** link in hello breadcrumb at hello top-left corner.</span></span>

    ![Accédez toodata arrière fabrique](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="62d20-139">État d’affichage hello de chaque activité à l’intérieur d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="62d20-139">View hello state of each activity inside a pipeline</span></span>
<span data-ttu-id="62d20-140">Vous pouvez afficher l’état actuel de hello d’une activité en consultant l’état hello de hello des jeux de données qui est produites par l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-140">You can view hello current state of an activity by viewing hello status of any of hello datasets that are produced by hello activity.</span></span>

<span data-ttu-id="62d20-141">En double-cliquant sur hello **OutputBlobTable** Bonjour **diagramme**, vous pouvez voir toutes les tranches hello produites par les exécutions d’activité différente à l’intérieur d’un pipeline.</span><span class="sxs-lookup"><span data-stu-id="62d20-141">By double-clicking hello **OutputBlobTable** in hello **Diagram**, you can see all hello slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="62d20-142">Vous pouvez voir que l’activité de copie hello a été correctement exécuté pour hello huit dernières heures et produits tranches hello Bonjour **prêt** état.</span><span class="sxs-lookup"><span data-stu-id="62d20-142">You can see that hello copy activity ran successfully for hello last eight hours and produced hello slices in hello **Ready** state.</span></span>  

![État du pipeline de hello](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="62d20-144">tranches de dataset Hello dans la fabrique de données hello peuvent prendre de hello suivant des États :</span><span class="sxs-lookup"><span data-stu-id="62d20-144">hello dataset slices in hello data factory can have one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="62d20-145">State</span><span class="sxs-lookup"><span data-stu-id="62d20-145">State</span></span></th><th align="left"><span data-ttu-id="62d20-146">Sous-état</span><span class="sxs-lookup"><span data-stu-id="62d20-146">Substate</span></span></th><th align="left"><span data-ttu-id="62d20-147">Description</span><span class="sxs-lookup"><span data-stu-id="62d20-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="62d20-148">En attente</span><span class="sxs-lookup"><span data-stu-id="62d20-148">Waiting</span></span></td><td><span data-ttu-id="62d20-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="62d20-149">ScheduleTime</span></span></td><td><span data-ttu-id="62d20-150">temps de Hello n’a pas encore être motivée par de hello tranche toorun.</span><span class="sxs-lookup"><span data-stu-id="62d20-150">hello time hasn't come for hello slice toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="62d20-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="62d20-151">DatasetDependencies</span></span></td><td><span data-ttu-id="62d20-152">les dépendances en amont Hello ne sont pas prêts.</span><span class="sxs-lookup"><span data-stu-id="62d20-152">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="62d20-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="62d20-153">ComputeResources</span></span></td><td><span data-ttu-id="62d20-154">ressources de calcul Hello ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="62d20-154">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="62d20-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="62d20-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="62d20-156">Toutes les instances d’activité hello sont occupés à exécuter d’autres tranches.</span><span class="sxs-lookup"><span data-stu-id="62d20-156">All hello activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="62d20-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="62d20-157">ActivityResume</span></span></td><td><span data-ttu-id="62d20-158">activité Hello est suspendue et ne peut pas exécuter les tranches hello jusqu'à ce que l’activité hello est reprise.</span><span class="sxs-lookup"><span data-stu-id="62d20-158">hello activity is paused and can't run hello slices until hello activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="62d20-159">Retry</span><span class="sxs-lookup"><span data-stu-id="62d20-159">Retry</span></span></td><td><span data-ttu-id="62d20-160">L’exécution de l’activité est retentée.</span><span class="sxs-lookup"><span data-stu-id="62d20-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="62d20-161">Validation</span><span class="sxs-lookup"><span data-stu-id="62d20-161">Validation</span></span></td><td><span data-ttu-id="62d20-162">La validation n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="62d20-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="62d20-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="62d20-163">ValidationRetry</span></span></td><td><span data-ttu-id="62d20-164">La validation est toobe en attente une nouvelle tentée.</span><span class="sxs-lookup"><span data-stu-id="62d20-164">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="62d20-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="62d20-165">InProgress</span></span></td><td><span data-ttu-id="62d20-166">Validation</span><span class="sxs-lookup"><span data-stu-id="62d20-166">Validating</span></span></td><td><span data-ttu-id="62d20-167">La validation est en cours.</span><span class="sxs-lookup"><span data-stu-id="62d20-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="62d20-168">la tranche de Hello est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="62d20-168">hello slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="62d20-169">Échec</span><span class="sxs-lookup"><span data-stu-id="62d20-169">Failed</span></span></td><td><span data-ttu-id="62d20-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="62d20-170">TimedOut</span></span></td><td><span data-ttu-id="62d20-171">exécution de l’activité Hello a pris plus de temps que ce qui est autorisé par activité hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-171">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="62d20-172">Canceled</span><span class="sxs-lookup"><span data-stu-id="62d20-172">Canceled</span></span></td><td><span data-ttu-id="62d20-173">la tranche de Hello a été annulée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="62d20-173">hello slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="62d20-174">Validation</span><span class="sxs-lookup"><span data-stu-id="62d20-174">Validation</span></span></td><td><span data-ttu-id="62d20-175">La validation a échoué.</span><span class="sxs-lookup"><span data-stu-id="62d20-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="62d20-176">Échec de la tranche de Hello toobe généré et/ou validé.</span><span class="sxs-lookup"><span data-stu-id="62d20-176">hello slice failed toobe generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="62d20-177">Ready</span><span class="sxs-lookup"><span data-stu-id="62d20-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="62d20-178">tranche de Hello est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="62d20-178">hello slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="62d20-179">Ignoré</span><span class="sxs-lookup"><span data-stu-id="62d20-179">Skipped</span></span></td><td><span data-ttu-id="62d20-180">Aucun</span><span class="sxs-lookup"><span data-stu-id="62d20-180">None</span></span></td><td><span data-ttu-id="62d20-181">la tranche de Hello n’est pas en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="62d20-181">hello slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="62d20-182">Aucun</span><span class="sxs-lookup"><span data-stu-id="62d20-182">None</span></span></td><td>-</td><td><span data-ttu-id="62d20-183">Une tranche utilisé tooexist avec un état différent, mais il a été réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="62d20-183">A slice used tooexist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="62d20-184">Vous pouvez afficher les détails de hello sur une section en cliquant sur une entrée de la tranche sur hello **récemment mis à jour les tranches** panneau.</span><span class="sxs-lookup"><span data-stu-id="62d20-184">You can view hello details about a slice by clicking a slice entry on hello **Recently Updated Slices** blade.</span></span>

![Détails de la tranche](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="62d20-186">Si la tranche de hello a été exécutée plusieurs fois, vous voyez plusieurs lignes Bonjour **activité s’exécute** liste.</span><span class="sxs-lookup"><span data-stu-id="62d20-186">If hello slice has been executed multiple times, you see multiple rows in hello **Activity runs** list.</span></span> <span data-ttu-id="62d20-187">Vous pouvez afficher des détails sur une activité à exécuter en cliquant sur entrée hello exécuter Bonjour **activité s’exécute** liste.</span><span class="sxs-lookup"><span data-stu-id="62d20-187">You can view details about an activity run by clicking hello run entry in hello **Activity runs** list.</span></span> <span data-ttu-id="62d20-188">liste de Hello montre tous les fichiers journaux hello, ainsi que d’un message d’erreur si elle existe.</span><span class="sxs-lookup"><span data-stu-id="62d20-188">hello list shows all hello log files, along with an error message if there is one.</span></span> <span data-ttu-id="62d20-189">Cette fonctionnalité est utiles journaux tooview et de débogage sans avoir tooleave votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="62d20-189">This feature is useful tooview and debug logs without having tooleave your data factory.</span></span>

![Détails de l'exécution d'activité](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="62d20-191">Si la tranche de hello n’est pas Bonjour **prêt** état, vous pouvez voir les tranches en amont hello qui ne sont pas prêts et bloquent tranche à partir de l’exécution dans hello hello **tranches en amont qui ne sont pas prêtes** liste.</span><span class="sxs-lookup"><span data-stu-id="62d20-191">If hello slice isn't in hello **Ready** state, you can see hello upstream slices that aren't ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="62d20-192">Cette fonctionnalité est utile lorsque votre tranche est dans **attente** état et que vous souhaitez toounderstand hello en amont dépendances hello tranche est en attente.</span><span class="sxs-lookup"><span data-stu-id="62d20-192">This feature is useful when your slice is in **Waiting** state and you want toounderstand hello upstream dependencies that hello slice is waiting on.</span></span>

![Tranches en amont qui ne sont pas prêtes](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="62d20-194">Schéma d’état de jeux de données</span><span class="sxs-lookup"><span data-stu-id="62d20-194">Dataset state diagram</span></span>
<span data-ttu-id="62d20-195">Une fois que vous déployez une fabrique de données et les pipelines hello ont une période active valide, hello dataset tranches transition à partir d’un état tooanother.</span><span class="sxs-lookup"><span data-stu-id="62d20-195">After you deploy a data factory and hello pipelines have a valid active period, hello dataset slices transition from one state tooanother.</span></span> <span data-ttu-id="62d20-196">Actuellement, état de la tranche hello suit hello suivant le diagramme d’état :</span><span class="sxs-lookup"><span data-stu-id="62d20-196">Currently, hello slice status follows hello following state diagram:</span></span>

![Schéma d'état](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="62d20-198">jeu de données des flux de transition d’état dans la fabrique de données Hello sont suivant de hello : en attente -> en cours/en cours (validation) -> Échec prêt.</span><span class="sxs-lookup"><span data-stu-id="62d20-198">hello dataset state transition flow in data factory is hello following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="62d20-199">la tranche de Hello démarre dans un **en attente** état, en attente de toobe les conditions préalables remplie avant qu’elle s’exécute.</span><span class="sxs-lookup"><span data-stu-id="62d20-199">hello slice starts in a **Waiting** state, waiting for preconditions toobe met before it executes.</span></span> <span data-ttu-id="62d20-200">Ensuite, activité hello commence à s’exécuter et tranche de hello sont placées dans un **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="62d20-200">Then, hello activity starts executing, and hello slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="62d20-201">exécution de l’activité Hello peut réussissent ou échouent.</span><span class="sxs-lookup"><span data-stu-id="62d20-201">hello activity execution might succeed or fail.</span></span> <span data-ttu-id="62d20-202">la tranche de Hello est marquée comme **prêt** ou **n’a pas pu**, en fonction de résultats de l’exécution de hello hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-202">hello slice is marked as **Ready** or **Failed**, based on hello result of hello execution.</span></span>

<span data-ttu-id="62d20-203">Vous pouvez réinitialiser toogo de tranche hello de hello **prêt** ou **n’a pas pu** état toohello **attente** état.</span><span class="sxs-lookup"><span data-stu-id="62d20-203">You can reset hello slice toogo back from hello **Ready** or **Failed** state toohello **Waiting** state.</span></span> <span data-ttu-id="62d20-204">Vous pouvez également marquer l’état de tranche hello trop**ignorer**, ce qui empêche l’activité hello à partir de l’exécution et ne traite ne pas les tranches hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-204">You can also mark hello slice state too**Skip**, which prevents hello activity from executing and not processing hello slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="62d20-205">Suspension et reprise des pipelines</span><span class="sxs-lookup"><span data-stu-id="62d20-205">Pause and resume pipelines</span></span>
<span data-ttu-id="62d20-206">Vous pouvez gérer vos pipelines à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62d20-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="62d20-207">Par exemple, vous pouvez suspendre et reprendre les pipelines en exécutant les applets de commande Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62d20-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="62d20-208">affichage des diagrammes Hello ne prend pas en charge la suspension et reprise des pipelines.</span><span class="sxs-lookup"><span data-stu-id="62d20-208">hello diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="62d20-209">Si vous souhaitez toouse une interface utilisateur, utilisez hello analyse et la gestion d’application.</span><span class="sxs-lookup"><span data-stu-id="62d20-209">If you want toouse an user interface, use hello monitoring and managing application.</span></span> <span data-ttu-id="62d20-210">Pour plus d’informations sur l’utilisation d’application hello, consultez [surveiller et gérer des pipelines de fabrique de données à l’aide d’application de gestion et de surveillance hello](data-factory-monitor-manage-app.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="62d20-210">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="62d20-211">Vous pouvez suspendre/suspendre pipelines à l’aide de hello **Suspend-AzureRmDataFactoryPipeline** applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62d20-211">You can pause/suspend pipelines by using hello **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="62d20-212">Cette applet de commande est utile lorsque vous ne souhaitez pas que toorun vos pipelines jusqu'à ce qu’un problème est résolu.</span><span class="sxs-lookup"><span data-stu-id="62d20-212">This cmdlet is useful when you don’t want toorun your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="62d20-213">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="62d20-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="62d20-214">Après que hello problème résolu avec le pipeline de hello, vous pouvez reprendre le pipeline de hello suspendu en exécutant hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="62d20-214">After hello issue has been fixed with hello pipeline, you can resume hello suspended pipeline by running hello following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="62d20-215">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="62d20-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="62d20-216">Débogage de pipelines</span><span class="sxs-lookup"><span data-stu-id="62d20-216">Debug pipelines</span></span>
<span data-ttu-id="62d20-217">Azure Data Factory fournit des fonctionnalités enrichies vous toodebug et résoudre les problèmes de pipelines à l’aide de hello portail Azure et Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62d20-217">Azure Data Factory provides rich capabilities for you toodebug and troubleshoot pipelines by using hello Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="62d20-218">[! Notez} il est beaucoup plus facile tootroubleshot erreurs à l’aide de hello analyse & application de gestion.</span><span class="sxs-lookup"><span data-stu-id="62d20-218">[!NOTE} It is much easier tootroubleshot errors using hello Monitoring & Management App.</span></span> <span data-ttu-id="62d20-219">Pour plus d’informations sur l’utilisation d’application hello, consultez [surveiller et gérer des pipelines de fabrique de données à l’aide d’application de gestion et de surveillance hello](data-factory-monitor-manage-app.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="62d20-219">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="62d20-220">Recherche d’erreurs dans un pipeline</span><span class="sxs-lookup"><span data-stu-id="62d20-220">Find errors in a pipeline</span></span>
<span data-ttu-id="62d20-221">En cas d’exécution de l’activité hello dans un pipeline, hello de jeu de données qui est généré par le pipeline de hello est dans un état d’erreur en raison de l’échec de hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-221">If hello activity run fails in a pipeline, hello dataset that is produced by hello pipeline is in an error state because of hello failure.</span></span> <span data-ttu-id="62d20-222">Vous pouvez déboguer et résoudre les erreurs dans Azure Data Factory à l’aide des méthodes suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-222">You can debug and troubleshoot errors in Azure Data Factory by using hello following methods.</span></span>

#### <a name="use-hello-azure-portal-toodebug-an-error"></a><span data-ttu-id="62d20-223">Utilisez hello toodebug portail Azure une erreur</span><span class="sxs-lookup"><span data-stu-id="62d20-223">Use hello Azure portal toodebug an error</span></span>
1. <span data-ttu-id="62d20-224">Sur hello **Table** panneau, cliquez sur le secteur problème hello a hello **état** défini trop**n’a pas pu**.</span><span class="sxs-lookup"><span data-stu-id="62d20-224">On hello **Table** blade, click hello problem slice that has hello **Status** set too**Failed**.</span></span>

   ![Panneau de table avec tranche problématique](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="62d20-226">Sur hello **tranche de données** panneau, cliquez sur activité hello qui a échoué.</span><span class="sxs-lookup"><span data-stu-id="62d20-226">On hello **Data slice** blade, click hello activity run that failed.</span></span>

   ![Tranche de données avec une erreur](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="62d20-228">Sur hello **détails de l’exécution activité** panneau, vous pouvez télécharger les fichiers de hello qui sont associés au traitement de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-228">On hello **Activity run details** blade, you can download hello files that are associated with hello HDInsight processing.</span></span> <span data-ttu-id="62d20-229">Cliquez sur **télécharger** état/stderr toodownload hello fichier journal des erreurs qui contient des détails sur l’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-229">Click **Download** for Status/stderr toodownload hello error log file that contains details about hello error.</span></span>

   ![Panneau de détails sur l’exécution d’activité](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a><span data-ttu-id="62d20-231">Utilisez PowerShell toodebug une erreur</span><span class="sxs-lookup"><span data-stu-id="62d20-231">Use PowerShell toodebug an error</span></span>
1. <span data-ttu-id="62d20-232">Lancez **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="62d20-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="62d20-233">Exécutez hello **Get-AzureRmDataFactorySlice** commande tranches de hello toosee et leurs États.</span><span class="sxs-lookup"><span data-stu-id="62d20-233">Run hello **Get-AzureRmDataFactorySlice** command toosee hello slices and their statuses.</span></span> <span data-ttu-id="62d20-234">Vous devez voir une tranche dont l’état hello **n’a pas pu**.</span><span class="sxs-lookup"><span data-stu-id="62d20-234">You should see a slice with hello status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="62d20-235">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="62d20-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="62d20-236">Remplacez **StartDateTime** par l’heure de début de votre pipeline.</span><span class="sxs-lookup"><span data-stu-id="62d20-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="62d20-237">Exécutez maintenant hello **Get-AzureRmDataFactoryRun** tooget détails sur l’activité hello exécuter de la tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-237">Now, run hello **Get-AzureRmDataFactoryRun** cmdlet tooget details about hello activity run for hello slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="62d20-238">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="62d20-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="62d20-239">valeur Hello %StartDateTime;) est heure de début hello pour tranche d’erreur/problème hello que vous avez noté à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-239">hello value of StartDateTime is hello start time for hello error/problem slice that you noted from hello previous step.</span></span> <span data-ttu-id="62d20-240">Hello date-heure doit être entourée de guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="62d20-240">hello date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="62d20-241">Sortie avec des détails sur l’erreur de hello est similaire toohello suivant doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="62d20-241">You should see output with details about hello error that is similar toohello following:</span></span>

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
5. <span data-ttu-id="62d20-242">Vous pouvez exécuter hello **Save-AzureRmDataFactoryLog** applet de commande avec hello valeur d’Id que vous consultez à partir de la sortie de hello et téléchargez les fichiers de journaux hello à l’aide de hello **- DownloadLogsoption** pour l’applet de commande hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-242">You can run hello **Save-AzureRmDataFactoryLog** cmdlet with hello Id value that you see from hello output, and download hello log files by using hello **-DownloadLogsoption** for hello cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="62d20-243">Réexécuter des échecs dans un pipeline</span><span class="sxs-lookup"><span data-stu-id="62d20-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62d20-244">Il est plus facile tootroubleshoot erreurs et réexécuter tranches ayant échouées à l’aide de hello analyse & application de gestion.</span><span class="sxs-lookup"><span data-stu-id="62d20-244">It's easier tootroubleshoot errors and rerun failed slices by using hello Monitoring & Management App.</span></span> <span data-ttu-id="62d20-245">Pour plus d’informations sur l’utilisation d’application hello, consultez [surveiller et gérer des pipelines de fabrique de données à l’aide d’application de gestion et de surveillance hello](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="62d20-245">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-hello-azure-portal"></a><span data-ttu-id="62d20-246">Utilisez hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="62d20-246">Use hello Azure portal</span></span>
<span data-ttu-id="62d20-247">Après avoir résoudre les problèmes et déboguer les erreurs dans un pipeline, vous pouvez réexécuter des échecs par tranche d’erreur toohello en cliquant sur hello **exécuter** bouton de barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating toohello error slice and clicking hello **Run** button on hello command bar.</span></span>

![Réexécuter une tranche de données ayant échoué](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="62d20-249">Dans le cas de tranche de hello Échec de la validation en raison d’un échec de la stratégie (par exemple, si des données n’est pas disponibles), vous pouvez corriger l’échec de hello et valider de nouveau en cliquant sur hello **Validate** bouton de barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-249">In case hello slice has failed validation because of a policy failure (for example, if data isn't available), you can fix hello failure and validate again by clicking hello **Validate** button on hello command bar.</span></span>

![Corriger les erreurs et valider](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="62d20-251">Utilisation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="62d20-251">Use Azure PowerShell</span></span>
<span data-ttu-id="62d20-252">Vous pouvez réexécuter les défaillances à l’aide de hello **Set-AzureRmDataFactorySliceStatus** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="62d20-252">You can rerun failures by using hello **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="62d20-253">Consultez hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) rubrique pour la syntaxe et d’autres détails sur l’applet de commande hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-253">See hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about hello cmdlet.</span></span>

<span data-ttu-id="62d20-254">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="62d20-254">**Example:**</span></span>

<span data-ttu-id="62d20-255">exemple Hello définit état hello de toutes les tranches pour hello table 'DAWikiAggregatedData' too'Waiting' dans la fabrique de données Azure hello 'WikiADF'.</span><span class="sxs-lookup"><span data-stu-id="62d20-255">hello following example sets hello status of all slices for hello table 'DAWikiAggregatedData' too'Waiting' in hello Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="62d20-256">Hello 'Type' a la valeur too'UpstreamInPipeline ', ce qui signifie que les États de chaque secteur pour la table de hello et toutes les tables (en amont) dépendants hello sont définies too'Waiting'.</span><span class="sxs-lookup"><span data-stu-id="62d20-256">hello 'UpdateType' is set too'UpstreamInPipeline', which means that statuses of each slice for hello table and all hello dependent (upstream) tables are set too'Waiting'.</span></span> <span data-ttu-id="62d20-257">Bonjour autre valeur possible pour ce paramètre est « Individuel ».</span><span class="sxs-lookup"><span data-stu-id="62d20-257">hello other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="62d20-258">Créez des alertes</span><span class="sxs-lookup"><span data-stu-id="62d20-258">Create alerts</span></span>
<span data-ttu-id="62d20-259">Azure consigne les événements utilisateur lorsqu'une ressource Azure (par exemple, une fabrique de données) est créée, mise à jour ou supprimée.</span><span class="sxs-lookup"><span data-stu-id="62d20-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="62d20-260">Vous pouvez créer des alertes relatives à ces événements.</span><span class="sxs-lookup"><span data-stu-id="62d20-260">You can create alerts on these events.</span></span> <span data-ttu-id="62d20-261">Vous pouvez utiliser Data Factory toocapture diverses métriques et créer des alertes sur des métriques.</span><span class="sxs-lookup"><span data-stu-id="62d20-261">You can use Data Factory toocapture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="62d20-262">Nous vous recommandons d’utiliser les événements pour obtenir une surveillance en temps réel et les mesures à des fins d’historique.</span><span class="sxs-lookup"><span data-stu-id="62d20-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="62d20-263">Alertes relatives à des événements</span><span class="sxs-lookup"><span data-stu-id="62d20-263">Alerts on events</span></span>
<span data-ttu-id="62d20-264">Les événements Azure fournissent des explications utiles sur ce qui se passe dans vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="62d20-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="62d20-265">Lorsque vous utilisez Azure Data Factory, les événements sont générés quand :</span><span class="sxs-lookup"><span data-stu-id="62d20-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="62d20-266">Une fabrique de données est créée, mise à jour ou supprimée.</span><span class="sxs-lookup"><span data-stu-id="62d20-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="62d20-267">Le traitement des données (les « exécutions ») est démarré ou terminé.</span><span class="sxs-lookup"><span data-stu-id="62d20-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="62d20-268">Un cluster HDInsight à la demande est créé ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="62d20-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="62d20-269">Vous pouvez créer des alertes sur ces événements utilisateur et les configurer à l’administrateur de toohello toosend par courrier électronique des notifications et coadministrators d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-269">You can create alerts on these user events and configure them toosend email notifications toohello administrator and coadministrators of hello subscription.</span></span> <span data-ttu-id="62d20-270">En outre, vous pouvez spécifier des adresses de messagerie supplémentaires des utilisateurs qui ont besoin de notifications par courrier électronique de tooreceive lorsque hello conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="62d20-270">In addition, you can specify additional email addresses of users who need tooreceive email notifications when hello conditions are met.</span></span> <span data-ttu-id="62d20-271">Cette fonctionnalité est utile quand vous voulez tooget informé sur les échecs et que vous ne souhaitez pas que toocontinuously analyse votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="62d20-271">This feature is useful when you want tooget notified on failures and don’t want toocontinuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="62d20-272">Actuellement, le portail de hello n’affiche pas les alertes sur les événements.</span><span class="sxs-lookup"><span data-stu-id="62d20-272">Currently, hello portal doesn't show alerts on events.</span></span> <span data-ttu-id="62d20-273">Hello d’utilisation [analyse et gestion d’application](data-factory-monitor-manage-app.md) toosee toutes les alertes.</span><span class="sxs-lookup"><span data-stu-id="62d20-273">Use hello [Monitoring and Management app](data-factory-monitor-manage-app.md) toosee all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="62d20-274">Spécifier une définition d’alerte</span><span class="sxs-lookup"><span data-stu-id="62d20-274">Specify an alert definition</span></span>
<span data-ttu-id="62d20-275">toospecify une définition d’alerte, vous créez un fichier JSON qui décrit les opérations hello toobe alerté sur souhaitées.</span><span class="sxs-lookup"><span data-stu-id="62d20-275">toospecify an alert definition, you create a JSON file that describes hello operations that you want toobe alerted on.</span></span> <span data-ttu-id="62d20-276">Dans l’exemple suivant de hello, alerte de hello envoie une notification par courrier électronique pour hello RunFinished opération.</span><span class="sxs-lookup"><span data-stu-id="62d20-276">In hello following example, hello alert sends an email notification for hello RunFinished operation.</span></span> <span data-ttu-id="62d20-277">toobe spécifique, une notification par courrier électronique est envoyée lorsqu’une exécution dans la fabrique de données hello est terminée et hello exécuter a échoué (état = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="62d20-277">toobe specific, an email notification is sent when a run in hello data factory has completed and hello run has failed (Status = FailedExecution).</span></span>

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
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
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

<span data-ttu-id="62d20-278">Vous pouvez supprimer **sous-état** de hello définition JSON si vous ne souhaitez pas toobe averti en cas d’échec spécifique.</span><span class="sxs-lookup"><span data-stu-id="62d20-278">You can remove **subStatus** from hello JSON definition if you don’t want toobe alerted on a specific failure.</span></span>

<span data-ttu-id="62d20-279">Cet exemple configure alerte hello pour toutes les fabriques de données dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="62d20-279">This example sets up hello alert for all data factories in your subscription.</span></span> <span data-ttu-id="62d20-280">Si vous souhaitez hello alerte toobe est défini pour une fabrique de données particulière, vous pouvez spécifier la fabrique de données **resourceUri** Bonjour **source de données**:</span><span class="sxs-lookup"><span data-stu-id="62d20-280">If you want hello alert toobe set up for a particular data factory, you can specify data factory **resourceUri** in hello **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="62d20-281">Hello tableau suivant fournit hello liste des opérations disponibles et les États (sous-états).</span><span class="sxs-lookup"><span data-stu-id="62d20-281">hello following table provides hello list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="62d20-282">Nom d’opération</span><span class="sxs-lookup"><span data-stu-id="62d20-282">Operation name</span></span> | <span data-ttu-id="62d20-283">État</span><span class="sxs-lookup"><span data-stu-id="62d20-283">Status</span></span> | <span data-ttu-id="62d20-284">État secondaire</span><span class="sxs-lookup"><span data-stu-id="62d20-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62d20-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="62d20-285">RunStarted</span></span> |<span data-ttu-id="62d20-286">Démarré</span><span class="sxs-lookup"><span data-stu-id="62d20-286">Started</span></span> |<span data-ttu-id="62d20-287">Starting</span><span class="sxs-lookup"><span data-stu-id="62d20-287">Starting</span></span> |
| <span data-ttu-id="62d20-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="62d20-288">RunFinished</span></span> |<span data-ttu-id="62d20-289">Failed / Succeeded</span><span class="sxs-lookup"><span data-stu-id="62d20-289">Failed / Succeeded</span></span> |<span data-ttu-id="62d20-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="62d20-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="62d20-291">Succeeded</span><span class="sxs-lookup"><span data-stu-id="62d20-291">Succeeded</span></span><br/><br/><span data-ttu-id="62d20-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="62d20-292">FailedExecution</span></span><br/><br/><span data-ttu-id="62d20-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="62d20-293">TimedOut</span></span><br/><br/><span data-ttu-id="62d20-294"><Canceled</span><span class="sxs-lookup"><span data-stu-id="62d20-294"><Canceled</span></span><br/><br/><span data-ttu-id="62d20-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="62d20-295">FailedValidation</span></span><br/><br/><span data-ttu-id="62d20-296">Abandonné</span><span class="sxs-lookup"><span data-stu-id="62d20-296">Abandoned</span></span> |
| <span data-ttu-id="62d20-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="62d20-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="62d20-298">Démarré</span><span class="sxs-lookup"><span data-stu-id="62d20-298">Started</span></span> | |
| <span data-ttu-id="62d20-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="62d20-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="62d20-300">Réussi</span><span class="sxs-lookup"><span data-stu-id="62d20-300">Succeeded</span></span> | |
| <span data-ttu-id="62d20-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="62d20-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="62d20-302">Réussi</span><span class="sxs-lookup"><span data-stu-id="62d20-302">Succeeded</span></span> | |

<span data-ttu-id="62d20-303">Consultez [créer une règle d’alerte](https://msdn.microsoft.com/library/azure/dn510366.aspx) pour plus d’informations sur les éléments JSON hello qui sont utilisés dans l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about hello JSON elements that are used in hello example.</span></span>

#### <a name="deploy-hello-alert"></a><span data-ttu-id="62d20-304">Déployer l’alerte de hello</span><span class="sxs-lookup"><span data-stu-id="62d20-304">Deploy hello alert</span></span>
<span data-ttu-id="62d20-305">alerte de hello toodeploy, applet de commande Azure PowerShell utilisez hello **New-AzureRmResourceGroupDeployment**, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="62d20-305">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="62d20-306">Une fois le déploiement de groupe de ressources hello terminée avec succès, vous voyez hello suivant des messages :</span><span class="sxs-lookup"><span data-stu-id="62d20-306">After hello resource group deployment has finished successfully, you see hello following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
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
> <span data-ttu-id="62d20-307">Vous pouvez utiliser hello [créer une règle d’alerte](https://msdn.microsoft.com/library/azure/dn510366.aspx) API REST toocreate une règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="62d20-307">You can use hello [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate an alert rule.</span></span> <span data-ttu-id="62d20-308">charge utile JSON de Hello est un exemple JSON toohello similaire.</span><span class="sxs-lookup"><span data-stu-id="62d20-308">hello JSON payload is similar toohello JSON example.</span></span>  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a><span data-ttu-id="62d20-309">Récupérer la liste de hello de déploiements de groupes de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="62d20-309">Retrieve hello list of Azure resource group deployments</span></span>
<span data-ttu-id="62d20-310">liste de hello tooretrieve des déployé des déploiements de groupes de ressources Azure, utilisez l’applet de commande hello **Get-AzureRmResourceGroupDeployment**, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="62d20-310">tooretrieve hello list of deployed Azure resource group deployments, use hello cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

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

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="62d20-311">Résoudre les problèmes relatifs aux événements utilisateur</span><span class="sxs-lookup"><span data-stu-id="62d20-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="62d20-312">Vous pouvez voir tous les événements de hello qui sont générés après avoir cliqué sur hello **métriques et les opérations** vignette.</span><span class="sxs-lookup"><span data-stu-id="62d20-312">You can see all hello events that are generated after clicking hello **Metrics and operations** tile.</span></span>

    ![Vignette Mesures et opérations](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="62d20-314">Cliquez sur hello **événements** vignette événements de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="62d20-314">Click hello **Events** tile toosee hello events.</span></span>

    ![Vignette d'événements](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="62d20-316">Sur hello **événements** panneau, vous pouvez voir les détails sur les événements, événements filtrés et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="62d20-316">On hello **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Panneau Événements](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="62d20-318">Cliquez sur un **opération** dans la liste des opérations hello qui provoque une erreur.</span><span class="sxs-lookup"><span data-stu-id="62d20-318">Click an **Operation** in hello operations list that causes an error.</span></span>

    ![Sélectionner une opération](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="62d20-320">Cliquez sur un **erreur** toosee détails de l’événement sur l’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-320">Click an **Error** event toosee details about hello error.</span></span>

    ![Événement erreur](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="62d20-322">Consultez [applets de commande Azure Insight](https://msdn.microsoft.com/library/mt282452.aspx) pour les applets de commande PowerShell que vous pouvez utiliser tooadd, obtenir ou supprimer des alertes.</span><span class="sxs-lookup"><span data-stu-id="62d20-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use tooadd, get, or remove alerts.</span></span> <span data-ttu-id="62d20-323">Voici quelques exemples d’utilisation de hello **Get-AlertRule** applet de commande :</span><span class="sxs-lookup"><span data-stu-id="62d20-323">Here are a few examples of using hello **Get-AlertRule** cmdlet:</span></span>

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
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
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

<span data-ttu-id="62d20-324">Exécutez hello suivant get-help commandes toosee détails et des exemples d’applet de commande Get-AlertRule hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-324">Run hello following get-help commands toosee details and examples for hello Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="62d20-325">Si vous voyez des événements de génération d’alertes de hello sur hello panneau portail, mais vous ne recevez pas de notifications par courrier électronique, vérifier si l’adresse de messagerie hello est spécifié a des messages électroniques tooreceive des expéditeurs externes.</span><span class="sxs-lookup"><span data-stu-id="62d20-325">If you see hello alert generation events on hello portal blade but you don't receive email notifications, check whether hello email address that is specified is set tooreceive emails from external senders.</span></span> <span data-ttu-id="62d20-326">Il se peuvent que des messages d’alerte Hello ont été bloqués par vos paramètres de messagerie.</span><span class="sxs-lookup"><span data-stu-id="62d20-326">hello alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="62d20-327">Alertes relatives à des mesures</span><span class="sxs-lookup"><span data-stu-id="62d20-327">Alerts on metrics</span></span>
<span data-ttu-id="62d20-328">Dans Data Factory, vous pouvez capturer différentes mesures et créer des alertes associées.</span><span class="sxs-lookup"><span data-stu-id="62d20-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="62d20-329">Vous pouvez analyser et créer des alertes sur hello suivant métriques pour les tranches hello dans votre fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="62d20-329">You can monitor and create alerts on hello following metrics for hello slices in your data factory:</span></span>

* <span data-ttu-id="62d20-330">**Exécutions échouées**</span><span class="sxs-lookup"><span data-stu-id="62d20-330">**Failed Runs**</span></span>
* <span data-ttu-id="62d20-331">**Exécutions réussies**</span><span class="sxs-lookup"><span data-stu-id="62d20-331">**Successful Runs**</span></span>

<span data-ttu-id="62d20-332">Ces mesures sont utiles et vous aider à tooget qu'une vue d’ensemble de globale ayant réussi et s’exécute dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-332">These metrics are useful and help you tooget an overview of overall failed and successful runs in hello data factory.</span></span> <span data-ttu-id="62d20-333">Des mesures sont émises lors de chaque exécution de tranche de données.</span><span class="sxs-lookup"><span data-stu-id="62d20-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="62d20-334">Au début de hello d’heure de hello, ces mesures sont agrégées et placé le compte de stockage tooyour.</span><span class="sxs-lookup"><span data-stu-id="62d20-334">At hello beginning of hello hour, these metrics are aggregated and pushed tooyour storage account.</span></span> <span data-ttu-id="62d20-335">mesures tooenable, configurer un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="62d20-335">tooenable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="62d20-336">Activer les mesures</span><span class="sxs-lookup"><span data-stu-id="62d20-336">Enable metrics</span></span>
<span data-ttu-id="62d20-337">tooenable des mesures, cliquez sur suivant hello de hello **Data Factory** panneau :</span><span class="sxs-lookup"><span data-stu-id="62d20-337">tooenable metrics, click hello following from hello **Data Factory** blade:</span></span>

<span data-ttu-id="62d20-338">**Analyse** > **Mesures** > **Paramètres de diagnostic** > **Diagnostics**</span><span class="sxs-lookup"><span data-stu-id="62d20-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Lien Diagnostics](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="62d20-340">Sur hello **Diagnostics** panneau, cliquez sur **sur**, sélectionnez le compte de stockage hello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="62d20-340">On hello **Diagnostics** blade, click **On**, select hello storage account, and click **Save**.</span></span>

![Panneau Diagnostics](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="62d20-342">Elle peut prendre heure tooone toobe de métriques hello visible sur hello **analyse** panneau parce que l’agrégation de mesures se produit toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="62d20-342">It might take up tooone hour for hello metrics toobe visible on hello **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="62d20-343">Configurer une alerte relative à des mesures</span><span class="sxs-lookup"><span data-stu-id="62d20-343">Set up an alert on metrics</span></span>
<span data-ttu-id="62d20-344">Cliquez sur hello **les métriques de Data Factory** vignette :</span><span class="sxs-lookup"><span data-stu-id="62d20-344">Click hello **Data Factory metrics** tile:</span></span>

![Vignette Mesures de fabrique de données](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="62d20-346">Sur hello **métrique** panneau, cliquez sur **+ ajouter une alerte** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-346">On hello **Metric** blade, click **+ Add alert** on hello toolbar.</span></span>
<span data-ttu-id="62d20-347">![Panneau Mesures de fabrique de données &gt; Ajouter une alerte](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="62d20-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="62d20-348">Sur hello **ajouter une règle d’alerte** page, procédez comme hello comme suit, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="62d20-348">On hello **Add an alert rule** page, do hello following steps, and click **OK**.</span></span>

* <span data-ttu-id="62d20-349">Entrez un nom pour l’alerte de hello (exemple : « Échec de l’alerte »).</span><span class="sxs-lookup"><span data-stu-id="62d20-349">Enter a name for hello alert (example: "failed alert").</span></span>
* <span data-ttu-id="62d20-350">Entrez une description de l’alerte de hello (exemple : « envoyer un courrier électronique lorsqu’une défaillance se produit »).</span><span class="sxs-lookup"><span data-stu-id="62d20-350">Enter a description for hello alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="62d20-351">Sélectionnez une mesure (« exécutions échouées » ou « exécutions réussies »).</span><span class="sxs-lookup"><span data-stu-id="62d20-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="62d20-352">Spécifiez une condition et une valeur de seuil.</span><span class="sxs-lookup"><span data-stu-id="62d20-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="62d20-353">Spécifier la période hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-353">Specify hello period of time.</span></span>
* <span data-ttu-id="62d20-354">Spécifiez si un message électronique doit être envoyé tooowners, les collaborateurs et les lecteurs.</span><span class="sxs-lookup"><span data-stu-id="62d20-354">Specify whether an email should be sent tooowners, contributors, and readers.</span></span>

![Panneau Mesures de fabrique de données > Ajouter une règle d’alerte](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="62d20-356">Une fois que la règle d’alerte hello est ajoutée avec succès, panneau de hello se ferme et vous voyez nouvelle alerte de hello sur hello **métrique** panneau.</span><span class="sxs-lookup"><span data-stu-id="62d20-356">After hello alert rule is added successfully, hello blade closes and you see hello new alert on hello **Metric** blade.</span></span>

![Panneau Mesures de fabrique de données > Nouvelle alerte ajoutée](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="62d20-358">Vous devez également voir le nombre de hello d’alertes hello **règles d’alerte** vignette.</span><span class="sxs-lookup"><span data-stu-id="62d20-358">You should also see hello number of alerts in hello **Alert rules** tile.</span></span> <span data-ttu-id="62d20-359">Cliquez sur hello **règles d’alerte** vignette.</span><span class="sxs-lookup"><span data-stu-id="62d20-359">Click hello **Alert rules** tile.</span></span>

![Panneau Mesures de fabrique de données - Règles d’alerte](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="62d20-361">Sur hello **alertes règles** panneau, vous voyez les alertes existantes.</span><span class="sxs-lookup"><span data-stu-id="62d20-361">On hello **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="62d20-362">tooadd une alerte, cliquez sur **ajouter une alerte** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-362">tooadd an alert, click **Add alert** on hello toolbar.</span></span>

![Panneau Règles d’alerte](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="62d20-364">Notifications d’alerte</span><span class="sxs-lookup"><span data-stu-id="62d20-364">Alert notifications</span></span>
<span data-ttu-id="62d20-365">Une fois que la règle d’alerte hello correspond à la condition de hello, vous devez obtenir un message électronique indiquant que l’alerte de hello est activée.</span><span class="sxs-lookup"><span data-stu-id="62d20-365">After hello alert rule matches hello condition, you should get an email that says hello alert is activated.</span></span> <span data-ttu-id="62d20-366">Une fois résolu hello et condition d’alerte hello ne correspond pas à plus, vous obtenez un message électronique indiquant que hello alerte est résolue.</span><span class="sxs-lookup"><span data-stu-id="62d20-366">After hello issue is resolved and hello alert condition doesn’t match anymore, you get an email that says hello alert is resolved.</span></span>

<span data-ttu-id="62d20-367">Ce comportement se distingue des événements donnant lieu à l’envoi d’une notification dès qu’un échec correspondant à une règle d’alerte a lieu.</span><span class="sxs-lookup"><span data-stu-id="62d20-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="62d20-368">Déployer des alertes à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="62d20-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="62d20-369">Vous pouvez déployer des alertes pour les métriques hello même manière que pour les événements.</span><span class="sxs-lookup"><span data-stu-id="62d20-369">You can deploy alerts for metrics hello same way that you do for events.</span></span>

<span data-ttu-id="62d20-370">**Définition d’alerte**</span><span class="sxs-lookup"><span data-stu-id="62d20-370">**Alert definition**</span></span>

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

<span data-ttu-id="62d20-371">Remplacez *subscriptionId*, *resourceGroupName*, et *dataFactoryName* dans l’exemple hello avec les valeurs appropriées.</span><span class="sxs-lookup"><span data-stu-id="62d20-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in hello sample with appropriate values.</span></span>

<span data-ttu-id="62d20-372">*metricName* prend actuellement en charge deux valeurs :</span><span class="sxs-lookup"><span data-stu-id="62d20-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="62d20-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="62d20-373">FailedRuns</span></span>
* <span data-ttu-id="62d20-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="62d20-374">SuccessfulRuns</span></span>

<span data-ttu-id="62d20-375">**Déployer l’alerte de hello**</span><span class="sxs-lookup"><span data-stu-id="62d20-375">**Deploy hello alert**</span></span>

<span data-ttu-id="62d20-376">alerte de hello toodeploy, applet de commande Azure PowerShell utilisez hello **New-AzureRmResourceGroupDeployment**, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="62d20-376">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="62d20-377">Le message suivant devrait s’afficher après la réussite du déploiement :</span><span class="sxs-lookup"><span data-stu-id="62d20-377">You should see following message after a successful deployment:</span></span>

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

<span data-ttu-id="62d20-378">Vous pouvez également utiliser hello **Add-AlertRule** toodeploy de l’applet de commande une règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="62d20-378">You can also use hello **Add-AlertRule** cmdlet toodeploy an alert rule.</span></span> <span data-ttu-id="62d20-379">Consultez hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) rubrique pour plus d’informations et des exemples.</span><span class="sxs-lookup"><span data-stu-id="62d20-379">See hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a><span data-ttu-id="62d20-380">Déplacer un groupe de ressources différent de données fabrique tooa ou un abonnement</span><span class="sxs-lookup"><span data-stu-id="62d20-380">Move a data factory tooa different resource group or subscription</span></span>
<span data-ttu-id="62d20-381">Vous pouvez déplacer un groupe de ressources différent de données fabrique tooa ou un autre abonnement à l’aide de hello **déplacer** barre bouton sur la page d’accueil hello votre fabrique de données de commandes.</span><span class="sxs-lookup"><span data-stu-id="62d20-381">You can move a data factory tooa different resource group or a different subscription by using hello **Move** command bar button on hello home page of your data factory.</span></span>

![Déplacer la fabrique de données](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="62d20-383">Vous pouvez également déplacer toutes les ressources associées (tels que les alertes associées à la fabrique de données hello), ainsi que de la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="62d20-383">You can also move any related resources (such as alerts that are associated with hello data factory), along with hello data factory.</span></span>

![Boîte de dialogue Déplacer des ressources](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
