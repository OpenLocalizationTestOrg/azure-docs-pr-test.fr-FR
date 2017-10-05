---
title: "Exécuter des tâches en arrière-plan avec les tâches web"
description: "Découvrez comment exécuter des tâches en arrière-plan dans les applications web Azure."
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
ms.openlocfilehash: 3f8ae748e3d9c6b4e342536926a52b4e8f37ee51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="bf109-103">Exécuter des tâches en arrière-plan avec les tâches web</span><span class="sxs-lookup"><span data-stu-id="bf109-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="bf109-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bf109-104">Overview</span></span>
<span data-ttu-id="bf109-105">Vous pouvez exécuter des programmes ou des scripts dans WebJobs au niveau de votre application Web [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) de trois façons : à la demande, de façon continue ou de façon planifiée.</span><span class="sxs-lookup"><span data-stu-id="bf109-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="bf109-106">L’utilisation des tâches web n’entraîne aucun coût supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="bf109-106">There is no additional cost to use WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="bf109-107">Cet article explique comment déployer WebJobs à l’aide du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bf109-107">This article shows how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="bf109-108">Pour plus d’informations sur le déploiement à l’aide de Visual Studio ou d’un processus de diffusion continue, consultez [Déploiement de tâches Web Azure dans Web Apps](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="bf109-108">For information about how to deploy by using Visual Studio or a continuous delivery process, see [How to Deploy Azure WebJobs to Web Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="bf109-109">Le Kit de développement logiciel (SDK) Azure WebJobs simplifie de nombreuses tâches de programmation.</span><span class="sxs-lookup"><span data-stu-id="bf109-109">The Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="bf109-110">Pour plus d’informations, consultez [Présentation du Kit de développement logiciel (SDK) WebJobs Azure](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="bf109-110">For more information, see [What is the WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="bf109-111">Azure Functions fournit une autre façon d’exécuter des scripts et des programmes à partir d’un environnement sans serveur ou d’une application App Service.</span><span class="sxs-lookup"><span data-stu-id="bf109-111">Azure Functions provides another way to run programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="bf109-112">Pour plus d’informations, consultez [Vue d’ensemble d’Azure Functions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf109-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="bf109-113"><a name="acceptablefiles"></a>Types de fichier acceptables pour les scripts ou les programmes</span><span class="sxs-lookup"><span data-stu-id="bf109-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="bf109-114">Les types de fichier suivants sont acceptés :</span><span class="sxs-lookup"><span data-stu-id="bf109-114">The following file types are accepted:</span></span>

* <span data-ttu-id="bf109-115">.cmd, .bat, .exe (en utilisant une commande Windows)</span><span class="sxs-lookup"><span data-stu-id="bf109-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="bf109-116">.ps1 (en utilisant Powershell)</span><span class="sxs-lookup"><span data-stu-id="bf109-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="bf109-117">.sh (en utilisant un interpréteur de commandes)</span><span class="sxs-lookup"><span data-stu-id="bf109-117">.sh (using bash)</span></span>
* <span data-ttu-id="bf109-118">.php (en utilisant PHP)</span><span class="sxs-lookup"><span data-stu-id="bf109-118">.php (using php)</span></span>
* <span data-ttu-id="bf109-119">.py (en utilisant Python)</span><span class="sxs-lookup"><span data-stu-id="bf109-119">.py (using python)</span></span>
* <span data-ttu-id="bf109-120">.js (en utilisant Node)</span><span class="sxs-lookup"><span data-stu-id="bf109-120">.js (using node)</span></span>
* <span data-ttu-id="bf109-121">.jar (en utilisant Java)</span><span class="sxs-lookup"><span data-stu-id="bf109-121">.jar (using java)</span></span>

## <span data-ttu-id="bf109-122"><a name="CreateOnDemand"></a>Création d’une tâche Web à la demande sur le portail</span><span class="sxs-lookup"><span data-stu-id="bf109-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in the portal</span></span>
1. <span data-ttu-id="bf109-123">Dans le panneau **Application web** du [portail Azure](https://portal.azure.com), cliquez sur **Tous les paramètres > Tâches web** pour afficher le panneau **Tâches web**.</span><span class="sxs-lookup"><span data-stu-id="bf109-123">In the **Web App** blade of the [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** to show the **WebJobs** blade.</span></span>
   
    ![Panneau Tâches Web](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="bf109-125">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bf109-125">Click **Add**.</span></span> <span data-ttu-id="bf109-126">La boîte de dialogue **Ajouter une tâche web Azure** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bf109-126">The **Add WebJob** dialog appears.</span></span>
   
    ![Panneau Ajouter une tâche Web](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="bf109-128">Sous **Nom**, indiquez le nom de la tâche Web.</span><span class="sxs-lookup"><span data-stu-id="bf109-128">Under **Name**, provide a name for the WebJob.</span></span> <span data-ttu-id="bf109-129">Le nom doit commencer par une lettre ou un chiffre et ne peut pas contenir de caractères spéciaux, à part les tirets et les traits de soulignement (« - » et « _ »).</span><span class="sxs-lookup"><span data-stu-id="bf109-129">The name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="bf109-130">Dans la zone **Mode d’exécution**, sélectionnez **Exécuter à la demande**.</span><span class="sxs-lookup"><span data-stu-id="bf109-130">In the **How to Run** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="bf109-131">Dans la zone **Téléchargement de fichiers** , cliquez sur l’icône du dossier et recherchez le fichier .zip qui contient votre script.</span><span class="sxs-lookup"><span data-stu-id="bf109-131">In the **File Upload** box, click the folder icon and browse to the zip file that contains your script.</span></span> <span data-ttu-id="bf109-132">Ce fichier .zip doit contenir votre exécutable (.exe .cmd .bat .sh .php .py .js) ainsi que les fichiers de prise en charge requis pour exécuter le programme ou le script.</span><span class="sxs-lookup"><span data-stu-id="bf109-132">The zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed to run the program or script.</span></span>
6. <span data-ttu-id="bf109-133">Cochez la case **Créer** pour télécharger le script dans votre application Web.</span><span class="sxs-lookup"><span data-stu-id="bf109-133">Check **Create** to upload the script to your web app.</span></span> 
   
    <span data-ttu-id="bf109-134">Le nom que vous avez indiqué pour la tâche Web apparaît dans la liste, dans le panneau **Tâches web** .</span><span class="sxs-lookup"><span data-stu-id="bf109-134">The name you specified for the WebJob appears in the list on the **WebJobs** blade.</span></span>
7. <span data-ttu-id="bf109-135">Pour exécuter la tâche Web, cliquez sur son nom dans la liste avec le bouton droit, puis cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="bf109-135">To run the WebJob, right-click its name in the list and click **Run**.</span></span>
   
    ![Exécuter une tâche Web](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="bf109-137"><a name="CreateContinuous"></a>Création d’une tâche Web exécutée en continu</span><span class="sxs-lookup"><span data-stu-id="bf109-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="bf109-138">Pour créer une tâche web exécutée en continu, procédez comme pour la création d’une tâche web à exécution unique, mais dans la zone **Mode d’exécution**, sélectionnez **Exécuter en continu**.</span><span class="sxs-lookup"><span data-stu-id="bf109-138">To create a continuously executing WebJob, follow the same steps for creating a WebJob that runs once, but in the **How to Run** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="bf109-139">Pour démarrer ou arrêter une tâche web exécutée en continu, cliquez avec le bouton droit sur la tâche web dans la liste, puis cliquez sur **Démarrer** ou **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="bf109-139">To start or stop a continuous WebJob, right-click the WebJob in the list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="bf109-140">Si votre application web est exécutée sur plusieurs instances, une tâche web exécutée en continu le sera sur toutes vos instances.</span><span class="sxs-lookup"><span data-stu-id="bf109-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="bf109-141">Les tâches web à la demande et planifiées sont exécutées sur une seule instance sélectionnée pour l’équilibrage de charge par Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bf109-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="bf109-142">Pour que les tâches Web continues s'exécutent de façon fiable sur toutes les instances, activez le paramètre de configuration Toujours actif* de l'application Web. Sinon, elles risquent de s’arrêter si le site de l'hôte SCM reste inactif pendant trop longtemps.</span><span class="sxs-lookup"><span data-stu-id="bf109-142">For Continuous WebJobs to run reliably and on all instances, enable the Always On* configuration setting for the web app otherwise they can stop running when the SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="bf109-143"><a name="CreateScheduledCRON"></a>Créer une tâche web planifiée à l’aide d’une expression CRON</span><span class="sxs-lookup"><span data-stu-id="bf109-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="bf109-144">Cette technique est disponible dans Web Apps s’exécutant en mode De base, Standard ou Premium et suppose que le paramètre **Toujours actif** est activé sur l’application.</span><span class="sxs-lookup"><span data-stu-id="bf109-144">This technique is available to Web Apps running in Basic, Standard or Premium mode, and requires the **Always On** setting to be enabled on the app.</span></span>

<span data-ttu-id="bf109-145">Pour transformer une tâche web à la demande en une tâche web planifiée, il vous suffit d’inclure un fichier `settings.job` à la racine du fichier compressé de la tâche web.</span><span class="sxs-lookup"><span data-stu-id="bf109-145">To turn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at the root of your WebJob zip file.</span></span> <span data-ttu-id="bf109-146">Ce fichier JSON doit inclure une propriété `schedule` avec une [expression CRON](https://en.wikipedia.org/wiki/Cron), comme ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bf109-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="bf109-147">L’expression CRON est composée de 6 champs : `{second} {minute} {hour} {day} {month} {day of the week}`.</span><span class="sxs-lookup"><span data-stu-id="bf109-147">The CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of the week}`.</span></span>

<span data-ttu-id="bf109-148">Par exemple, pour déclencher la tâche web toutes les 15 minutes, le `settings.job` se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf109-148">For example, to trigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="bf109-149">Autres exemples de planification CRON :</span><span class="sxs-lookup"><span data-stu-id="bf109-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="bf109-150">Toutes les heures (autrement dit, chaque fois que le nombre de minutes est 0) : `0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="bf109-150">Every hour (i.e. whenever the count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="bf109-151">Toutes les heures entre 9h et 17h : `0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="bf109-151">Every hour from 9 AM to 5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="bf109-152">À 9h30 tous les jours : `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="bf109-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="bf109-153">À 9h30 tous les jours de la semaine : `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="bf109-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="bf109-154">**Remarque** : quand vous déployez une tâche web à partir de Visual Studio, veillez à marquer les propriétés du fichier `settings.job` comme Copier si plus récent.</span><span class="sxs-lookup"><span data-stu-id="bf109-154">**Note**: when deploying a WebJob from Visual Studio, make sure to mark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="bf109-155"><a name="CreateScheduled"></a>Créer une tâche web planifiée à l’aide d’Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="bf109-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using the Azure Scheduler</span></span>
<span data-ttu-id="bf109-156">L’autre technique ci-après fait appel à Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="bf109-156">The following alternate technique makes use of the Azure Scheduler.</span></span> <span data-ttu-id="bf109-157">Dans ce cas, votre tâche web n’a aucune connaissance directe de la planification.</span><span class="sxs-lookup"><span data-stu-id="bf109-157">In this case, your WebJob does not have any direct knowledge of the schedule.</span></span> <span data-ttu-id="bf109-158">Au lieu de cela, Azure Scheduler est configuré pour déclencher votre tâche web selon une planification.</span><span class="sxs-lookup"><span data-stu-id="bf109-158">Instead, the Azure Scheduler gets configured to trigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="bf109-159">Le portail Azure ne permet pas encore de créer une tâche web planifiée. Pour le moment, vous pouvez utiliser le [portail Classic](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="bf109-159">The Azure Portal doesn't yet have the ability to create a scheduled WebJob, but until that feature is added you can do it by using the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="bf109-160">Sur le [portail Classic](http://manage.windowsazure.com) , accédez à la page des tâches Web, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bf109-160">In the [classic portal](http://manage.windowsazure.com) go to the WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="bf109-161">Dans la zone **Mode d’exécution**, sélectionnez **Exécuter selon une planification**.</span><span class="sxs-lookup"><span data-stu-id="bf109-161">In the **How to Run** box, choose **Run on a schedule**.</span></span>
   
    ![Nouvelle tâche planifiée][NewScheduledJob]
3. <span data-ttu-id="bf109-163">Sélectionnez la **région Scheduler** pour votre tâche, puis cliquez sur la flèche située dans le coin inférieur droit de la boîte de dialogue pour passer à l'écran suivant.</span><span class="sxs-lookup"><span data-stu-id="bf109-163">Choose the **Scheduler Region** for your job, and then click the arrow on the bottom right of the dialog to proceed to the next screen.</span></span>
4. <span data-ttu-id="bf109-164">Dans la boîte de dialogue **Créer une tâche**, sélectionnez un type de **périodicité** : **Tâche ponctuelle** ou **Tâche périodique**.</span><span class="sxs-lookup"><span data-stu-id="bf109-164">In the **Create Job** dialog, choose the type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Périodicité de la planificiation][SchdRecurrence]
5. <span data-ttu-id="bf109-166">Choisissez également une date/heure de **début** : **Maintenant** ou **À une heure spécifique**.</span><span class="sxs-lookup"><span data-stu-id="bf109-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Heure de début de la planification][SchdStart]
6. <span data-ttu-id="bf109-168">Si vous voulez démarrer votre tâche à un moment précis, sélectionnez la date/heure de début sous **Starting On**.</span><span class="sxs-lookup"><span data-stu-id="bf109-168">If you want to start at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Début de la planification à une heure spécifique][SchdStartOn]
7. <span data-ttu-id="bf109-170">Si vous sélectionnez une tâche récurrente, l'option **Survenir chaque** vous permet d'indiquer la fréquence d'occurrence, tandis que l'option **Date de fin** vous permet d'indiquer une date/heure de fin.</span><span class="sxs-lookup"><span data-stu-id="bf109-170">If you chose a recurring job, you have the **Recur Every** option to specify the frequency of occurrence and the **Ending On** option to specify an ending time.</span></span>
   
    ![Périodicité de la planificiation][SchdRecurEvery]
8. <span data-ttu-id="bf109-172">Si vous sélectionnez **Semaines**, vous pouvez sélectionner la zone **Dans une planification donnée** et indiquer les jours de la semaine où vous voulez exécuter la tâche.</span><span class="sxs-lookup"><span data-stu-id="bf109-172">If you choose **Weeks**, you can select the **On a Particular Schedule** box and specify the days of the week that you want the job to run.</span></span>
   
    ![Planifier les jours de la semaine][SchdWeeksOnParticular]
9. <span data-ttu-id="bf109-174">Si vous sélectionnez **Mois** et la zone **Dans une planification donnée**, vous pouvez configurer la tâche pour qu'elle démarre certains **jours** du mois.</span><span class="sxs-lookup"><span data-stu-id="bf109-174">If you choose **Months** and select the **On a Particular Schedule** box, you can set the job to run on particular numbered **Days** in the month.</span></span> 
   
    ![Planifier à des dates spécifiques dans le mois][SchdMonthsOnPartDays]
10. <span data-ttu-id="bf109-176">Si vous sélectionnez **Jours de la semaine**, vous pouvez choisir les jours de la semaine durant lesquels exécuter la tâche.</span><span class="sxs-lookup"><span data-stu-id="bf109-176">If you choose **Week Days**, you can select which day or days of the week in the month you want the job to run on.</span></span>
    
     ![Planifier des jours de semaine spécifiques dans le mois][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="bf109-178">Enfin, vous pouvez également utiliser l'option **Occurrences** pour choisir la semaine du mois (première, deuxième, troisième, etc.) durant laquelle exécuter la tâche, les jours de votre choix.</span><span class="sxs-lookup"><span data-stu-id="bf109-178">Finally, you can also use the **Occurrences** option to choose which week in the month (first, second, third etc.) you want the job to run on the week days you specified.</span></span>
    
    ![Planifier des jours de semaine spécifiques certaines semaines du mois][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="bf109-180">Lorsque vous avez créé une ou plusieurs tâches, leurs noms sont affichés sous l'onglet WebJobs avec leur statut, leur type de planification et d'autres informations.</span><span class="sxs-lookup"><span data-stu-id="bf109-180">After you have created one or more jobs, their names will appear on the WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="bf109-181">L’historique répertorie les 30 dernières tâches web.</span><span class="sxs-lookup"><span data-stu-id="bf109-181">Historical information for the last 30  WebJobs is maintained.</span></span>
    
    ![Liste des tâches][WebJobsListWithSeveralJobs]

### <span data-ttu-id="bf109-183"><a name="Scheduler"></a>Tâches planifiées et Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="bf109-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="bf109-184">Les tâches planifiées peuvent être configurées avec plus de précision sur les pages Azure Scheduler du [portail Classic](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="bf109-184">Scheduled jobs can be further configured in the Azure Scheduler pages of the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="bf109-185">Sur la page WebJobs, cliquez sur le lien **schedule** de la tâche pour accéder à la page du portail d'Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="bf109-185">On the WebJobs page, click the job's **schedule** link to navigate to the Azure Scheduler portal page.</span></span> 
   
   ![Lien vers Azure Scheduler][LinkToScheduler]
2. <span data-ttu-id="bf109-187">Sur la page Scheduler, cliquez sur la tâche.</span><span class="sxs-lookup"><span data-stu-id="bf109-187">On the Scheduler page, click the job.</span></span>
   
    ![Tâches sur la page du portail Scheduler][SchedulerPortal]
3. <span data-ttu-id="bf109-189">La page **Job Action** s'ouvre : vous pouvez y configurer les tâches plus en détail.</span><span class="sxs-lookup"><span data-stu-id="bf109-189">The **Job Action** page opens, where you can further configure the job.</span></span> 
   
    ![Action de tâche PageInScheduler][JobActionPageInScheduler]

## <span data-ttu-id="bf109-191"><a name="ViewJobHistory"></a>Affichage de l’historique des tâches</span><span class="sxs-lookup"><span data-stu-id="bf109-191"><a name="ViewJobHistory"></a>View the job history</span></span>
1. <span data-ttu-id="bf109-192">Pour afficher l’historique d’exécution d’une tâche, notamment celui des tâches créées avec le Kit de développement logiciel (SDK) WebJobs, cliquez sur le lien correspondant sous la colonne **Journaux** du panneau Tâches web.</span><span class="sxs-lookup"><span data-stu-id="bf109-192">To view the execution history of a job, including jobs created with the WebJobs SDK, click  its corresponding link under the **Logs** column of the WebJobs blade.</span></span> <span data-ttu-id="bf109-193">Vous pouvez utiliser l'icône de Presse-papiers pour copier l'URL de la page du fichier journal dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="bf109-193">(You can use the clipboard icon to copy the URL of the log file page to the clipboard if you wish.)</span></span>
   
    ![Lien vers les journaux](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="bf109-195">En cliquant sur le lien, vous ouvrez la page de détail pour la tâche web.</span><span class="sxs-lookup"><span data-stu-id="bf109-195">Clicking the link opens the details page for the WebJob.</span></span> <span data-ttu-id="bf109-196">Cette page permet de savoir le nom de la commande exécutée, la date/heure de sa dernière exécution et si elle a réussi ou échoué.</span><span class="sxs-lookup"><span data-stu-id="bf109-196">This page shows you the name of the command run, the last times it ran, and its success or failure.</span></span> <span data-ttu-id="bf109-197">Sous **Recent job runs**, cliquez une fois pour afficher les détails supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="bf109-197">Under **Recent job runs**, click a time to see further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="bf109-199">La page **WebJob Run Details** apparaît.</span><span class="sxs-lookup"><span data-stu-id="bf109-199">The **WebJob Run Details** page appears.</span></span> <span data-ttu-id="bf109-200">Cliquez sur **Toggle Output** pour afficher le texte du contenu du journal.</span><span class="sxs-lookup"><span data-stu-id="bf109-200">Click **Toggle Output** to see the text of the log contents.</span></span> <span data-ttu-id="bf109-201">Le journal de sortie est au format texte.</span><span class="sxs-lookup"><span data-stu-id="bf109-201">The output log is in text format.</span></span> 
   
    ![Détails d'exécution de la tâche WebJob][WebJobRunDetails]
4. <span data-ttu-id="bf109-203">Pour afficher le texte de sortie dans une nouvelle fenêtre de navigateur, cliquez sur le lien **télécharger** .</span><span class="sxs-lookup"><span data-stu-id="bf109-203">To see the output text in a separate browser window, click the **download** link.</span></span> <span data-ttu-id="bf109-204">Pour télécharger le texte, cliquez avec le bouton droit sur le lien et utilisez les options de votre navigateur pour enregistrer le contenu du fichier.</span><span class="sxs-lookup"><span data-stu-id="bf109-204">To download the text itself, right-click the link and use your browser options to save the file contents.</span></span>
   
    ![Télécharger la sortie du journal][DownloadLogOutput]
5. <span data-ttu-id="bf109-206">Le lien **Tâches web** situé en haut de la page permet d’obtenir une liste des tâches Web sur le tableau de bord d’historique.</span><span class="sxs-lookup"><span data-stu-id="bf109-206">The **WebJobs** link at the top of the page provides a convenient way to get to a list of WebJobs on the history dashboard.</span></span>
   
    ![Lien Tâches Web][WebJobsLinkToDashboardList]
   
    ![Liste des tâches Web dans le tableau de bord d’historique][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="bf109-209">En cliquant sur l'un de ces liens, vous pouvez accéder à la page Détails de WebJob pour la tâche sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="bf109-209">Clicking one of these links takes you to the WebJob Details page for the job you selected.</span></span>

## <span data-ttu-id="bf109-210"><a name="WHPNotes"></a>Remarques</span><span class="sxs-lookup"><span data-stu-id="bf109-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="bf109-211">Les applications web en mode Gratuit peuvent expirer si, pendant 20 minutes, aucune requête à destination du site (de déploiement) SCM et du portail de l'application web n'est ouverte dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bf109-211">Web apps in Free mode can time out after 20 minutes if there are no requests to the scm (deployment) site and the web app's portal is not open in Azure.</span></span> <span data-ttu-id="bf109-212">Cette situation ne sera pas annulée par les requêtes à destination du site actif.</span><span class="sxs-lookup"><span data-stu-id="bf109-212">Requests to the actual site will not reset this.</span></span>
* <span data-ttu-id="bf109-213">Le code d'une tâche en continu doit être écrit pour s'exécuter dans une boucle infinie.</span><span class="sxs-lookup"><span data-stu-id="bf109-213">Code for a continuous job needs to be written to run in an endless loop.</span></span>
* <span data-ttu-id="bf109-214">Les tâches en continu sont uniquement exécutées comme tel lorsque l’application web est opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="bf109-214">Continuous jobs run continuously only when the web app is up.</span></span>
* <span data-ttu-id="bf109-215">Les modes Basique et Standard proposent la fonctionnalité Toujours actif qui, lorsqu’elle est activée, empêche les applications web de devenir inactives.</span><span class="sxs-lookup"><span data-stu-id="bf109-215">Basic and Standard modes offer the Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="bf109-216">Vous pouvez uniquement déboguer les tâches Web qui s’exécutent en continu.</span><span class="sxs-lookup"><span data-stu-id="bf109-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="bf109-217">Le débogage des tâches Web planifiées et à la demande n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="bf109-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="bf109-218"><a name="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bf109-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="bf109-219">Pour plus d’informations, consultez la page [Ressources Azure WebJobs][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="bf109-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

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

