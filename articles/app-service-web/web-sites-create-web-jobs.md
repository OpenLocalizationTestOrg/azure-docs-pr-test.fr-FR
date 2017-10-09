---
title: "aaaRun les tâches en arrière-plan avec les tâches Web"
description: "Découvrez comment les applications web toorun les tâches en arrière-plan dans Azure."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2016
ms.author: glenga
ms.openlocfilehash: 96a3d977a806e7192207f0f4da79dfd248694336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="3bd47-103">Exécuter des tâches en arrière-plan avec les tâches web</span><span class="sxs-lookup"><span data-stu-id="3bd47-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="3bd47-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3bd47-104">Overview</span></span>
<span data-ttu-id="3bd47-105">Vous pouvez exécuter des programmes ou des scripts dans WebJobs au niveau de votre application Web [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) de trois façons : à la demande, de façon continue ou de façon planifiée.</span><span class="sxs-lookup"><span data-stu-id="3bd47-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="3bd47-106">Il n’existe aucun coût supplémentaire de toouse tâches Web.</span><span class="sxs-lookup"><span data-stu-id="3bd47-106">There is no additional cost toouse WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="3bd47-107">Cet article explique comment toodeploy tâches Web à l’aide de hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3bd47-107">This article shows how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="3bd47-108">Pour plus d’informations sur la façon toodeploy à l’aide de Visual Studio ou un processus de livraison continue, consultez [comment tooDeploy Azure WebJobs tooWeb applications](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="3bd47-108">For information about how toodeploy by using Visual Studio or a continuous delivery process, see [How tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="3bd47-109">Hello Kit de développement logiciel Azure WebJobs simplifie de nombreuses tâches de programmation de tâches Web.</span><span class="sxs-lookup"><span data-stu-id="3bd47-109">hello Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="3bd47-110">Pour plus d’informations, consultez [What ' s hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="3bd47-110">For more information, see [What is hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="3bd47-111">Les fonctions Azure fournit une autre façon dont les programmes toorun et des scripts à partir d’un environnement sans serveur ou à partir d’une application de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="3bd47-111">Azure Functions provides another way toorun programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="3bd47-112">Pour plus d’informations, consultez [Vue d’ensemble d’Azure Functions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3bd47-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="3bd47-113"><a name="acceptablefiles"></a>Types de fichier acceptables pour les scripts ou les programmes</span><span class="sxs-lookup"><span data-stu-id="3bd47-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="3bd47-114">Hello, les types de fichier suivants est accepté :</span><span class="sxs-lookup"><span data-stu-id="3bd47-114">hello following file types are accepted:</span></span>

* <span data-ttu-id="3bd47-115">.cmd, .bat, .exe (en utilisant une commande Windows)</span><span class="sxs-lookup"><span data-stu-id="3bd47-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="3bd47-116">.ps1 (en utilisant Powershell)</span><span class="sxs-lookup"><span data-stu-id="3bd47-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="3bd47-117">.sh (en utilisant un interpréteur de commandes)</span><span class="sxs-lookup"><span data-stu-id="3bd47-117">.sh (using bash)</span></span>
* <span data-ttu-id="3bd47-118">.php (en utilisant PHP)</span><span class="sxs-lookup"><span data-stu-id="3bd47-118">.php (using php)</span></span>
* <span data-ttu-id="3bd47-119">.py (en utilisant Python)</span><span class="sxs-lookup"><span data-stu-id="3bd47-119">.py (using python)</span></span>
* <span data-ttu-id="3bd47-120">.js (en utilisant Node)</span><span class="sxs-lookup"><span data-stu-id="3bd47-120">.js (using node)</span></span>
* <span data-ttu-id="3bd47-121">.jar (en utilisant Java)</span><span class="sxs-lookup"><span data-stu-id="3bd47-121">.jar (using java)</span></span>

## <span data-ttu-id="3bd47-122"><a name="CreateOnDemand"></a>Créer une demande suite la tâche Web dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="3bd47-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in hello portal</span></span>
1. <span data-ttu-id="3bd47-123">Bonjour **Web App** Panneau de hello [portail Azure](https://portal.azure.com), cliquez sur **tous les paramètres > WebJobs** tooshow hello **WebJobs** panneau.</span><span class="sxs-lookup"><span data-stu-id="3bd47-123">In hello **Web App** blade of hello [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** tooshow hello **WebJobs** blade.</span></span>
   
    ![Panneau Tâches Web](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="3bd47-125">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="3bd47-125">Click **Add**.</span></span> <span data-ttu-id="3bd47-126">Hello **ajouter la tâche Web** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3bd47-126">hello **Add WebJob** dialog appears.</span></span>
   
    ![Panneau Ajouter une tâche Web](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="3bd47-128">Sous **nom**, fournissez un nom pour la tâche Web de hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-128">Under **Name**, provide a name for hello WebJob.</span></span> <span data-ttu-id="3bd47-129">nom de Hello doit commencer par une lettre ou un chiffre et ne peut pas contenir de caractères spéciaux autres que «- » et « _ ».</span><span class="sxs-lookup"><span data-stu-id="3bd47-129">hello name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="3bd47-130">Bonjour **comment tooRun** , choisissez **exécuter à la demande**.</span><span class="sxs-lookup"><span data-stu-id="3bd47-130">In hello **How tooRun** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="3bd47-131">Bonjour **de téléchargement de fichiers** zone, cliquez sur icône du dossier hello et rechercher le fichier zip toohello qui contient votre script.</span><span class="sxs-lookup"><span data-stu-id="3bd47-131">In hello **File Upload** box, click hello folder icon and browse toohello zip file that contains your script.</span></span> <span data-ttu-id="3bd47-132">fichier zip de Hello doit contenir votre fichier exécutable (.exe .cmd .bat .sh .php .py .js) ainsi que tous les fichiers de prise en charge nécessaires toorun hello programme ou script.</span><span class="sxs-lookup"><span data-stu-id="3bd47-132">hello zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed toorun hello program or script.</span></span>
6. <span data-ttu-id="3bd47-133">Vérifiez **créer** tooupload hello script tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="3bd47-133">Check **Create** tooupload hello script tooyour web app.</span></span> 
   
    <span data-ttu-id="3bd47-134">Hello nom spécifié pour la tâche Web de hello s’affiche dans la liste hello sur hello **WebJobs** panneau.</span><span class="sxs-lookup"><span data-stu-id="3bd47-134">hello name you specified for hello WebJob appears in hello list on hello **WebJobs** blade.</span></span>
7. <span data-ttu-id="3bd47-135">toorun hello la tâche Web, cliquez sur son nom dans la liste de hello et cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="3bd47-135">toorun hello WebJob, right-click its name in hello list and click **Run**.</span></span>
   
    ![Exécuter une tâche Web](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="3bd47-137"><a name="CreateContinuous"></a>Création d’une tâche Web exécutée en continu</span><span class="sxs-lookup"><span data-stu-id="3bd47-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="3bd47-138">toocreate une tâche Web en cours d’exécution en continu, suivez hello même les étapes de création d’une tâche Web qui s’exécute une fois, mais dans hello **comment tooRun** , choisissez **continu**.</span><span class="sxs-lookup"><span data-stu-id="3bd47-138">toocreate a continuously executing WebJob, follow hello same steps for creating a WebJob that runs once, but in hello **How tooRun** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="3bd47-139">toostart ou arrêter une tâche Web continue, avec le bouton droit hello la tâche Web dans la liste de hello et cliquez sur **Démarrer** ou **arrêter**.</span><span class="sxs-lookup"><span data-stu-id="3bd47-139">toostart or stop a continuous WebJob, right-click hello WebJob in hello list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="3bd47-140">Si votre application web est exécutée sur plusieurs instances, une tâche web exécutée en continu le sera sur toutes vos instances.</span><span class="sxs-lookup"><span data-stu-id="3bd47-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="3bd47-141">Les tâches web à la demande et planifiées sont exécutées sur une seule instance sélectionnée pour l’équilibrage de charge par Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3bd47-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="3bd47-142">Pour les tâches Web continues toorun et de manière fiable sur toutes les instances, activer la hello Always On * de configuration web application hello sinon ils peuvent s’arrêter lorsque le site de hello SCM hôte a été inactif pendant trop longtemps.</span><span class="sxs-lookup"><span data-stu-id="3bd47-142">For Continuous WebJobs toorun reliably and on all instances, enable hello Always On* configuration setting for hello web app otherwise they can stop running when hello SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="3bd47-143"><a name="CreateScheduledCRON"></a>Créer une tâche web planifiée à l’aide d’une expression CRON</span><span class="sxs-lookup"><span data-stu-id="3bd47-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="3bd47-144">Cette technique est disponible tooWeb les applications s’exécutant en mode de base, Standard ou Premium et nécessite hello **Always On** paramètre toobe activée sur l’application hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-144">This technique is available tooWeb Apps running in Basic, Standard or Premium mode, and requires hello **Always On** setting toobe enabled on hello app.</span></span>

<span data-ttu-id="3bd47-145">tooturn un sur la demande la tâche Web dans une tâche Web planifiée, incluez simplement une `settings.job` fichier à votre fichier zip de la tâche Web racine hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-145">tooturn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at hello root of your WebJob zip file.</span></span> <span data-ttu-id="3bd47-146">Ce fichier JSON doit inclure une propriété `schedule` avec une [expression CRON](https://en.wikipedia.org/wiki/Cron), comme ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3bd47-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="3bd47-147">Hello expression CRON est composée de 6 champs : `{second} {minute} {hour} {day} {month} {day of hello week}`.</span><span class="sxs-lookup"><span data-stu-id="3bd47-147">hello CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span></span>

<span data-ttu-id="3bd47-148">Par exemple, tootrigger votre tâche Web toutes les 15 minutes, votre `settings.job` aurait :</span><span class="sxs-lookup"><span data-stu-id="3bd47-148">For example, tootrigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="3bd47-149">Autres exemples de planification CRON :</span><span class="sxs-lookup"><span data-stu-id="3bd47-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="3bd47-150">Toutes les heures (autrement dit, chaque fois que nombre de minutes de hello est 0) :`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="3bd47-150">Every hour (i.e. whenever hello count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="3bd47-151">Toutes les heures de too5 de 9 : 00 PM :`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="3bd47-151">Every hour from 9 AM too5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="3bd47-152">À 9h30 tous les jours : `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="3bd47-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="3bd47-153">À 9h30 tous les jours de la semaine : `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="3bd47-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="3bd47-154">**Remarque**: lors du déploiement d’une tâche Web à partir de Visual Studio, assurez-vous que toomark votre `settings.job` propriétés du fichier en tant que « Copier si plus récent ».</span><span class="sxs-lookup"><span data-stu-id="3bd47-154">**Note**: when deploying a WebJob from Visual Studio, make sure toomark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="3bd47-155"><a name="CreateScheduled"></a>Créer une tâche planifiée à l’aide de hello Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="3bd47-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using hello Azure Scheduler</span></span>
<span data-ttu-id="3bd47-156">Hello suivant autre technique utilise hello Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="3bd47-156">hello following alternate technique makes use of hello Azure Scheduler.</span></span> <span data-ttu-id="3bd47-157">Dans ce cas, votre tâche Web n’a aucune connaissance directe de planification de hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-157">In this case, your WebJob does not have any direct knowledge of hello schedule.</span></span> <span data-ttu-id="3bd47-158">Au lieu de cela, hello Azure Scheduler obtient tootrigger configuré votre tâche Web selon une planification.</span><span class="sxs-lookup"><span data-stu-id="3bd47-158">Instead, hello Azure Scheduler gets configured tootrigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="3bd47-159">Hello portail Azure ne dispose pas encore hello capacité toocreate une tâche Web planifiée, mais jusqu'à ce que cette fonctionnalité est ajoutée. vous pouvez le faire à l’aide de hello [portail classic](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3bd47-159">hello Azure Portal doesn't yet have hello ability toocreate a scheduled WebJob, but until that feature is added you can do it by using hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="3bd47-160">Bonjour [portail classique](http://manage.windowsazure.com) atteindre la page de la tâche Web toohello et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3bd47-160">In hello [classic portal](http://manage.windowsazure.com) go toohello WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="3bd47-161">Bonjour **comment tooRun** , choisissez **exécuter selon une planification**.</span><span class="sxs-lookup"><span data-stu-id="3bd47-161">In hello **How tooRun** box, choose **Run on a schedule**.</span></span>
   
    ![Nouvelle tâche planifiée][NewScheduledJob]
3. <span data-ttu-id="3bd47-163">Choisissez hello **planificateur région** pour votre travail, puis cliquez sur la flèche bas hello à droite de l’écran suivant de hello dialogue tooproceed toohello hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-163">Choose hello **Scheduler Region** for your job, and then click hello arrow on hello bottom right of hello dialog tooproceed toohello next screen.</span></span>
4. <span data-ttu-id="3bd47-164">Bonjour **créer une tâche de** boîte de dialogue, choisissez le type hello de **périodicité** souhaité : **travail unique** ou **périodique travail**.</span><span class="sxs-lookup"><span data-stu-id="3bd47-164">In hello **Create Job** dialog, choose hello type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Périodicité de la planificiation][SchdRecurrence]
5. <span data-ttu-id="3bd47-166">Choisissez également une date/heure de **début** : **Maintenant** ou **À une heure spécifique**.</span><span class="sxs-lookup"><span data-stu-id="3bd47-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Heure de début de la planification][SchdStart]
6. <span data-ttu-id="3bd47-168">Si vous souhaitez toostart à un moment donné, choisissez vos valeurs de temps de départ sous **démarrage sur**.</span><span class="sxs-lookup"><span data-stu-id="3bd47-168">If you want toostart at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Début de la planification à une heure spécifique][SchdStartOn]
7. <span data-ttu-id="3bd47-170">Si vous avez choisi un travail périodique, vous avez hello **répéter chaque** option fréquence de hello toospecify d’occurrence et hello **fin sur** option toospecify une heure de fin.</span><span class="sxs-lookup"><span data-stu-id="3bd47-170">If you chose a recurring job, you have hello **Recur Every** option toospecify hello frequency of occurrence and hello **Ending On** option toospecify an ending time.</span></span>
   
    ![Périodicité de la planificiation][SchdRecurEvery]
8. <span data-ttu-id="3bd47-172">Si vous choisissez **semaines**, vous pouvez sélectionner hello **sur une planification particulière** zone, puis spécifiez les jours hello de hello semaine hello toorun de travail.</span><span class="sxs-lookup"><span data-stu-id="3bd47-172">If you choose **Weeks**, you can select hello **On a Particular Schedule** box and specify hello days of hello week that you want hello job toorun.</span></span>
   
    ![Jours de planification de hello semaine][SchdWeeksOnParticular]
9. <span data-ttu-id="3bd47-174">Si vous choisissez **mois** et sélectionnez hello **sur une planification particulière** zone, vous pouvez définir hello travail toorun sur particulier numérotée **jours** dans les mois hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-174">If you choose **Months** and select hello **On a Particular Schedule** box, you can set hello job toorun on particular numbered **Days** in hello month.</span></span> 
   
    ![Planifier des Dates particulier Bonjour mois][SchdMonthsOnPartDays]
10. <span data-ttu-id="3bd47-176">Si vous choisissez **jours de la semaine**, vous pouvez sélectionner l’ou les jours de semaine de hello hello mois hello travail toorun sur.</span><span class="sxs-lookup"><span data-stu-id="3bd47-176">If you choose **Week Days**, you can select which day or days of hello week in hello month you want hello job toorun on.</span></span>
    
     ![Planifier des jours de semaine spécifiques dans le mois][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="3bd47-178">Enfin, vous pouvez également utiliser hello **Occurrences** option toochoose quelle semaine du mois de hello (premier, deuxième, troisième etc.) souhaité toorun de travail hello sur hello jours de la semaine spécifié.</span><span class="sxs-lookup"><span data-stu-id="3bd47-178">Finally, you can also use hello **Occurrences** option toochoose which week in hello month (first, second, third etc.) you want hello job toorun on hello week days you specified.</span></span>
    
    ![Planifier des jours de semaine spécifiques certaines semaines du mois][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="3bd47-180">Après avoir créé un ou plusieurs travaux, leurs noms apparaissent sur l’onglet des tâches Web hello avec leur état, type de planification et d’autres informations.</span><span class="sxs-lookup"><span data-stu-id="3bd47-180">After you have created one or more jobs, their names will appear on hello WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="3bd47-181">Des informations d’historique de 30 tâches Web de la dernière hello sont conservées.</span><span class="sxs-lookup"><span data-stu-id="3bd47-181">Historical information for hello last 30  WebJobs is maintained.</span></span>
    
    ![Liste des tâches][WebJobsListWithSeveralJobs]

### <span data-ttu-id="3bd47-183"><a name="Scheduler"></a>Tâches planifiées et Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="3bd47-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="3bd47-184">Les tâches planifiées une configuration supplémentaire dans les pages d’Azure Scheduler hello Hello [portail classic](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3bd47-184">Scheduled jobs can be further configured in hello Azure Scheduler pages of hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="3bd47-185">Hello tâches Web page, cliquez sur la tâche hello **planification** page du portail lien toonavigate toohello Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="3bd47-185">On hello WebJobs page, click hello job's **schedule** link toonavigate toohello Azure Scheduler portal page.</span></span> 
   
   ![Lien tooAzure du planificateur][LinkToScheduler]
2. <span data-ttu-id="3bd47-187">Hello planificateur page, cliquez sur le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-187">On hello Scheduler page, click hello job.</span></span>
   
    ![Travail sur la page du portail hello du planificateur][SchedulerPortal]
3. <span data-ttu-id="3bd47-189">Hello **Action de tâche** page s’ouvre, où vous pouvez configurer les travaux hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-189">hello **Job Action** page opens, where you can further configure hello job.</span></span> 
   
    ![Action de tâche PageInScheduler][JobActionPageInScheduler]

## <span data-ttu-id="3bd47-191"><a name="ViewJobHistory"></a>Afficher l’historique des travaux de hello</span><span class="sxs-lookup"><span data-stu-id="3bd47-191"><a name="ViewJobHistory"></a>View hello job history</span></span>
1. <span data-ttu-id="3bd47-192">l’historique d’exécution hello tooview d’une tâche, y compris les travaux créés par hello WebJobs SDK, cliquez sur le lien correspondant sous hello **journaux** colonne du panneau des tâches Web hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-192">tooview hello execution history of a job, including jobs created with hello WebJobs SDK, click  its corresponding link under hello **Logs** column of hello WebJobs blade.</span></span> <span data-ttu-id="3bd47-193">(Vous pouvez utiliser hello Presse-papiers icône toocopy hello URL du Presse-papiers de toohello page hello journal fichier si vous le souhaitez.)</span><span class="sxs-lookup"><span data-stu-id="3bd47-193">(You can use hello clipboard icon toocopy hello URL of hello log file page toohello clipboard if you wish.)</span></span>
   
    ![Lien vers les journaux](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="3bd47-195">Cliquez sur lien de hello ouvre la page de détails de hello pourquoi la tâche Web.</span><span class="sxs-lookup"><span data-stu-id="3bd47-195">Clicking hello link opens hello details page for hello WebJob.</span></span> <span data-ttu-id="3bd47-196">Cette page indique hello de nom de l’exécution de commande hello, hello la dernière fois où il a été exécuté, et sa réussite ou l’échec.</span><span class="sxs-lookup"><span data-stu-id="3bd47-196">This page shows you hello name of hello command run, hello last times it ran, and its success or failure.</span></span> <span data-ttu-id="3bd47-197">Sous **exécutions de tâches récentes**, cliquez sur une heure toosee les détails supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3bd47-197">Under **Recent job runs**, click a time toosee further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="3bd47-199">Hello **détails d’exécution de la tâche Web** page s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3bd47-199">hello **WebJob Run Details** page appears.</span></span> <span data-ttu-id="3bd47-200">Cliquez sur **bascule sortie** texte hello de toosee du contenu du journal hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-200">Click **Toggle Output** toosee hello text of hello log contents.</span></span> <span data-ttu-id="3bd47-201">le journal de sortie Hello est au format texte.</span><span class="sxs-lookup"><span data-stu-id="3bd47-201">hello output log is in text format.</span></span> 
   
    ![Détails d'exécution de la tâche WebJob][WebJobRunDetails]
4. <span data-ttu-id="3bd47-203">texte de sortie toosee hello dans une fenêtre de navigateur distincte, cliquez sur hello **télécharger** lien.</span><span class="sxs-lookup"><span data-stu-id="3bd47-203">toosee hello output text in a separate browser window, click hello **download** link.</span></span> <span data-ttu-id="3bd47-204">toodownload hello texte, cliquez sur le lien de hello et utiliser le contenu de votre fichier de navigateur options toosave hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-204">toodownload hello text itself, right-click hello link and use your browser options toosave hello file contents.</span></span>
   
    ![Télécharger la sortie du journal][DownloadLogOutput]
5. <span data-ttu-id="3bd47-206">Hello **WebJobs** lien en hello haut hello fournit une liste de tooa tooget facilement des tâches Web sur le tableau de bord de l’historique hello.</span><span class="sxs-lookup"><span data-stu-id="3bd47-206">hello **WebJobs** link at hello top of hello page provides a convenient way tooget tooa list of WebJobs on hello history dashboard.</span></span>
   
    ![Liste de liens tooWebJobs][WebJobsLinkToDashboardList]
   
    ![Liste des tâches Web dans le tableau de bord d’historique][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="3bd47-209">Cliquant sur un de ces liens vous conduit page Détails de la tâche Web toohello travail hello que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3bd47-209">Clicking one of these links takes you toohello WebJob Details page for hello job you selected.</span></span>

## <span data-ttu-id="3bd47-210"><a name="WHPNotes"></a>Remarques</span><span class="sxs-lookup"><span data-stu-id="3bd47-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="3bd47-211">Les applications Web en mode gratuit peuvent expirer après 20 minutes s’il en existe pas les demandes toohello scm (déploiement) de site et de portail de l’application hello web n’est pas ouvert dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3bd47-211">Web apps in Free mode can time out after 20 minutes if there are no requests toohello scm (deployment) site and hello web app's portal is not open in Azure.</span></span> <span data-ttu-id="3bd47-212">Demandes toohello réelle du site ne réinitialise pas cela.</span><span class="sxs-lookup"><span data-stu-id="3bd47-212">Requests toohello actual site will not reset this.</span></span>
* <span data-ttu-id="3bd47-213">Le code pour une tâche en continu doit toobe écrit toorun dans une boucle sans fin.</span><span class="sxs-lookup"><span data-stu-id="3bd47-213">Code for a continuous job needs toobe written toorun in an endless loop.</span></span>
* <span data-ttu-id="3bd47-214">Tâches continues s’exécutent en continu uniquement lorsque l’application hello web fonctionne.</span><span class="sxs-lookup"><span data-stu-id="3bd47-214">Continuous jobs run continuously only when hello web app is up.</span></span>
* <span data-ttu-id="3bd47-215">Base et les modes Standard offre hello toujours sur des fonctionnalités qui, lorsque activé, empêche les applications web de devenir inactif.</span><span class="sxs-lookup"><span data-stu-id="3bd47-215">Basic and Standard modes offer hello Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="3bd47-216">Vous pouvez uniquement déboguer les tâches Web qui s’exécutent en continu.</span><span class="sxs-lookup"><span data-stu-id="3bd47-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="3bd47-217">Le débogage des tâches Web planifiées et à la demande n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3bd47-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="3bd47-218"><a name="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3bd47-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="3bd47-219">Pour plus d’informations, consultez la page [Ressources Azure WebJobs][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="3bd47-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

[PSonWebJobs]:http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx
[WebJobsRecommendedResources]:http://go.microsoft.com/fwlink/?LinkId=390226

[OnDemandWebJob]: ./media/web-sites-create-web-jobs/01aOnDemandWebJob.png
[WebJobsList]: ./media/web-sites-create-web-jobs/02aWebJobsList.png
[NewContinuousJob]: ./media/web-sites-create-web-jobs/03aNewContinuousJob.png
[NewScheduledJob]: ./media/web-sites-create-web-jobs/04aNewScheduledJob.png
[SchdRecurrence]: ./media/web-sites-create-web-jobs/05SchdRecurrence.png
[SchdStart]: ./media/web-sites-create-web-jobs/06SchdStart.png
[SchdStartOn]: ./media/web-sites-create-web-jobs/07SchdStartOn.png
[SchdRecurEvery]: ./media/web-sites-create-web-jobs/08SchdRecurEvery.png
[SchdWeeksOnParticular]: ./media/web-sites-create-web-jobs/09SchdWeeksOnParticular.png
[SchdMonthsOnPartDays]: ./media/web-sites-create-web-jobs/10SchdMonthsOnPartDays.png
[SchdMonthsOnPartWeekDays]: ./media/web-sites-create-web-jobs/11SchdMonthsOnPartWeekDays.png
[SchdMonthsOnPartWeekDaysOccurences]: ./media/web-sites-create-web-jobs/12SchdMonthsOnPartWeekDaysOccurences.png
[RunOnce]: ./media/web-sites-create-web-jobs/13RunOnce.png
[WebJobsListWithSeveralJobs]: ./media/web-sites-create-web-jobs/13WebJobsListWithSeveralJobs.png
[WebJobLogs]: ./media/web-sites-create-web-jobs/14WebJobLogs.png
[WebJobDetails]: ./media/web-sites-create-web-jobs/15WebJobDetails.png
[WebJobRunDetails]: ./media/web-sites-create-web-jobs/16WebJobRunDetails.png
[DownloadLogOutput]: ./media/web-sites-create-web-jobs/17DownloadLogOutput.png
[WebJobsLinkToDashboardList]: ./media/web-sites-create-web-jobs/18WebJobsLinkToDashboardList.png
[WebJobsListInJobsDashboard]: ./media/web-sites-create-web-jobs/19WebJobsListInJobsDashboard.png
[LinkToScheduler]: ./media/web-sites-create-web-jobs/31LinkToScheduler.png
[SchedulerPortal]: ./media/web-sites-create-web-jobs/32SchedulerPortal.png
[JobActionPageInScheduler]: ./media/web-sites-create-web-jobs/33JobActionPageInScheduler.png

