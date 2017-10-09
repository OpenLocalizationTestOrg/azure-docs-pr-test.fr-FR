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
# <a name="run-background-tasks-with-webjobs"></a>Exécuter des tâches en arrière-plan avec les tâches web
## <a name="overview"></a>Vue d'ensemble
Vous pouvez exécuter des programmes ou des scripts dans WebJobs au niveau de votre application Web [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) de trois façons : à la demande, de façon continue ou de façon planifiée. Il n’existe aucun coût supplémentaire de toouse tâches Web.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Cet article explique comment toodeploy tâches Web à l’aide de hello [Azure Portal](https://portal.azure.com). Pour plus d’informations sur la façon toodeploy à l’aide de Visual Studio ou un processus de livraison continue, consultez [comment tooDeploy Azure WebJobs tooWeb applications](websites-dotnet-deploy-webjobs.md).

Hello Kit de développement logiciel Azure WebJobs simplifie de nombreuses tâches de programmation de tâches Web. Pour plus d’informations, consultez [What ' s hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).

 Les fonctions Azure fournit une autre façon dont les programmes toorun et des scripts à partir d’un environnement sans serveur ou à partir d’une application de Service d’applications. Pour plus d’informations, consultez [Vue d’ensemble d’Azure Functions](../azure-functions/functions-overview.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>Types de fichier acceptables pour les scripts ou les programmes
Hello, les types de fichier suivants est accepté :

* .cmd, .bat, .exe (en utilisant une commande Windows)
* .ps1 (en utilisant Powershell)
* .sh (en utilisant un interpréteur de commandes)
* .php (en utilisant PHP)
* .py (en utilisant Python)
* .js (en utilisant Node)
* .jar (en utilisant Java)

## <a name="CreateOnDemand"></a>Créer une demande suite la tâche Web dans le portail de hello
1. Bonjour **Web App** Panneau de hello [portail Azure](https://portal.azure.com), cliquez sur **tous les paramètres > WebJobs** tooshow hello **WebJobs** panneau.
   
    ![Panneau Tâches Web](./media/web-sites-create-web-jobs/wjblade.png)
2. Cliquez sur **Add**. Hello **ajouter la tâche Web** boîte de dialogue s’affiche.
   
    ![Panneau Ajouter une tâche Web](./media/web-sites-create-web-jobs/addwjblade.png)
3. Sous **nom**, fournissez un nom pour la tâche Web de hello. nom de Hello doit commencer par une lettre ou un chiffre et ne peut pas contenir de caractères spéciaux autres que «- » et « _ ».
4. Bonjour **comment tooRun** , choisissez **exécuter à la demande**.
5. Bonjour **de téléchargement de fichiers** zone, cliquez sur icône du dossier hello et rechercher le fichier zip toohello qui contient votre script. fichier zip de Hello doit contenir votre fichier exécutable (.exe .cmd .bat .sh .php .py .js) ainsi que tous les fichiers de prise en charge nécessaires toorun hello programme ou script.
6. Vérifiez **créer** tooupload hello script tooyour web app. 
   
    Hello nom spécifié pour la tâche Web de hello s’affiche dans la liste hello sur hello **WebJobs** panneau.
7. toorun hello la tâche Web, cliquez sur son nom dans la liste de hello et cliquez sur **exécuter**.
   
    ![Exécuter une tâche Web](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>Création d’une tâche Web exécutée en continu
1. toocreate une tâche Web en cours d’exécution en continu, suivez hello même les étapes de création d’une tâche Web qui s’exécute une fois, mais dans hello **comment tooRun** , choisissez **continu**.
2. toostart ou arrêter une tâche Web continue, avec le bouton droit hello la tâche Web dans la liste de hello et cliquez sur **Démarrer** ou **arrêter**.

> [!NOTE]
> Si votre application web est exécutée sur plusieurs instances, une tâche web exécutée en continu le sera sur toutes vos instances. Les tâches web à la demande et planifiées sont exécutées sur une seule instance sélectionnée pour l’équilibrage de charge par Microsoft Azure.
> 
> Pour les tâches Web continues toorun et de manière fiable sur toutes les instances, activer la hello Always On * de configuration web application hello sinon ils peuvent s’arrêter lorsque le site de hello SCM hôte a été inactif pendant trop longtemps.
> 
> 

## <a name="CreateScheduledCRON"></a>Créer une tâche web planifiée à l’aide d’une expression CRON
Cette technique est disponible tooWeb les applications s’exécutant en mode de base, Standard ou Premium et nécessite hello **Always On** paramètre toobe activée sur l’application hello.

tooturn un sur la demande la tâche Web dans une tâche Web planifiée, incluez simplement une `settings.job` fichier à votre fichier zip de la tâche Web racine hello. Ce fichier JSON doit inclure une propriété `schedule` avec une [expression CRON](https://en.wikipedia.org/wiki/Cron), comme ci-dessous.

Hello expression CRON est composée de 6 champs : `{second} {minute} {hour} {day} {month} {day of hello week}`.

Par exemple, tootrigger votre tâche Web toutes les 15 minutes, votre `settings.job` aurait :

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

Autres exemples de planification CRON :

* Toutes les heures (autrement dit, chaque fois que nombre de minutes de hello est 0) :`0 0 * * * *` 
* Toutes les heures de too5 de 9 : 00 PM :`0 0 9-17 * * *` 
* À 9h30 tous les jours : `0 30 9 * * *`
* À 9h30 tous les jours de la semaine : `0 30 9 * * 1-5`

**Remarque**: lors du déploiement d’une tâche Web à partir de Visual Studio, assurez-vous que toomark votre `settings.job` propriétés du fichier en tant que « Copier si plus récent ».

## <a name="CreateScheduled"></a>Créer une tâche planifiée à l’aide de hello Azure Scheduler
Hello suivant autre technique utilise hello Azure Scheduler. Dans ce cas, votre tâche Web n’a aucune connaissance directe de planification de hello. Au lieu de cela, hello Azure Scheduler obtient tootrigger configuré votre tâche Web selon une planification. 

Hello portail Azure ne dispose pas encore hello capacité toocreate une tâche Web planifiée, mais jusqu'à ce que cette fonctionnalité est ajoutée. vous pouvez le faire à l’aide de hello [portail classic](http://manage.windowsazure.com).

1. Bonjour [portail classique](http://manage.windowsazure.com) atteindre la page de la tâche Web toohello et cliquez sur **ajouter**.
2. Bonjour **comment tooRun** , choisissez **exécuter selon une planification**.
   
    ![Nouvelle tâche planifiée][NewScheduledJob]
3. Choisissez hello **planificateur région** pour votre travail, puis cliquez sur la flèche bas hello à droite de l’écran suivant de hello dialogue tooproceed toohello hello.
4. Bonjour **créer une tâche de** boîte de dialogue, choisissez le type hello de **périodicité** souhaité : **travail unique** ou **périodique travail**.
   
    ![Périodicité de la planificiation][SchdRecurrence]
5. Choisissez également une date/heure de **début** : **Maintenant** ou **À une heure spécifique**.
   
    ![Heure de début de la planification][SchdStart]
6. Si vous souhaitez toostart à un moment donné, choisissez vos valeurs de temps de départ sous **démarrage sur**.
   
    ![Début de la planification à une heure spécifique][SchdStartOn]
7. Si vous avez choisi un travail périodique, vous avez hello **répéter chaque** option fréquence de hello toospecify d’occurrence et hello **fin sur** option toospecify une heure de fin.
   
    ![Périodicité de la planificiation][SchdRecurEvery]
8. Si vous choisissez **semaines**, vous pouvez sélectionner hello **sur une planification particulière** zone, puis spécifiez les jours hello de hello semaine hello toorun de travail.
   
    ![Jours de planification de hello semaine][SchdWeeksOnParticular]
9. Si vous choisissez **mois** et sélectionnez hello **sur une planification particulière** zone, vous pouvez définir hello travail toorun sur particulier numérotée **jours** dans les mois hello. 
   
    ![Planifier des Dates particulier Bonjour mois][SchdMonthsOnPartDays]
10. Si vous choisissez **jours de la semaine**, vous pouvez sélectionner l’ou les jours de semaine de hello hello mois hello travail toorun sur.
    
     ![Planifier des jours de semaine spécifiques dans le mois][SchdMonthsOnPartWeekDays]
11. Enfin, vous pouvez également utiliser hello **Occurrences** option toochoose quelle semaine du mois de hello (premier, deuxième, troisième etc.) souhaité toorun de travail hello sur hello jours de la semaine spécifié.
    
    ![Planifier des jours de semaine spécifiques certaines semaines du mois][SchdMonthsOnPartWeekDaysOccurences]
12. Après avoir créé un ou plusieurs travaux, leurs noms apparaissent sur l’onglet des tâches Web hello avec leur état, type de planification et d’autres informations. Des informations d’historique de 30 tâches Web de la dernière hello sont conservées.
    
    ![Liste des tâches][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>Tâches planifiées et Azure Scheduler
Les tâches planifiées une configuration supplémentaire dans les pages d’Azure Scheduler hello Hello [portail classic](http://manage.windowsazure.com).

1. Hello tâches Web page, cliquez sur la tâche hello **planification** page du portail lien toonavigate toohello Azure Scheduler. 
   
   ![Lien tooAzure du planificateur][LinkToScheduler]
2. Hello planificateur page, cliquez sur le travail de hello.
   
    ![Travail sur la page du portail hello du planificateur][SchedulerPortal]
3. Hello **Action de tâche** page s’ouvre, où vous pouvez configurer les travaux hello. 
   
    ![Action de tâche PageInScheduler][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>Afficher l’historique des travaux de hello
1. l’historique d’exécution hello tooview d’une tâche, y compris les travaux créés par hello WebJobs SDK, cliquez sur le lien correspondant sous hello **journaux** colonne du panneau des tâches Web hello. (Vous pouvez utiliser hello Presse-papiers icône toocopy hello URL du Presse-papiers de toohello page hello journal fichier si vous le souhaitez.)
   
    ![Lien vers les journaux](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. Cliquez sur lien de hello ouvre la page de détails de hello pourquoi la tâche Web. Cette page indique hello de nom de l’exécution de commande hello, hello la dernière fois où il a été exécuté, et sa réussite ou l’échec. Sous **exécutions de tâches récentes**, cliquez sur une heure toosee les détails supplémentaires.
   
    ![WebJobDetails][WebJobDetails]
3. Hello **détails d’exécution de la tâche Web** page s’affiche. Cliquez sur **bascule sortie** texte hello de toosee du contenu du journal hello. le journal de sortie Hello est au format texte. 
   
    ![Détails d'exécution de la tâche WebJob][WebJobRunDetails]
4. texte de sortie toosee hello dans une fenêtre de navigateur distincte, cliquez sur hello **télécharger** lien. toodownload hello texte, cliquez sur le lien de hello et utiliser le contenu de votre fichier de navigateur options toosave hello.
   
    ![Télécharger la sortie du journal][DownloadLogOutput]
5. Hello **WebJobs** lien en hello haut hello fournit une liste de tooa tooget facilement des tâches Web sur le tableau de bord de l’historique hello.
   
    ![Liste de liens tooWebJobs][WebJobsLinkToDashboardList]
   
    ![Liste des tâches Web dans le tableau de bord d’historique][WebJobsListInJobsDashboard]
   
    Cliquant sur un de ces liens vous conduit page Détails de la tâche Web toohello travail hello que vous avez sélectionné.

## <a name="WHPNotes"></a>Remarques
* Les applications Web en mode gratuit peuvent expirer après 20 minutes s’il en existe pas les demandes toohello scm (déploiement) de site et de portail de l’application hello web n’est pas ouvert dans Azure. Demandes toohello réelle du site ne réinitialise pas cela.
* Le code pour une tâche en continu doit toobe écrit toorun dans une boucle sans fin.
* Tâches continues s’exécutent en continu uniquement lorsque l’application hello web fonctionne.
* Base et les modes Standard offre hello toujours sur des fonctionnalités qui, lorsque activé, empêche les applications web de devenir inactif.
* Vous pouvez uniquement déboguer les tâches Web qui s’exécutent en continu. Le débogage des tâches Web planifiées et à la demande n’est pas pris en charge.

## <a name="NextSteps"></a>Étapes suivantes
Pour plus d’informations, consultez la page [Ressources Azure WebJobs][WebJobsRecommendedResources].

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

