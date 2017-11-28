---
title: "aaaGet main d’Azure Scheduler dans le portail Azure | Documents Microsoft"
description: "Prise en main d’Azure Scheduler dans le portail Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="ce6b7-103">Prise en main d’Azure Scheduler dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ce6b7-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="ce6b7-104">Il est facile toocreate planifié des travaux dans Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-104">It's easy toocreate scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="ce6b7-105">Dans ce didacticiel, vous allez apprendre comment toocreate un travail.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-105">In this tutorial, you'll learn how toocreate a job.</span></span> <span data-ttu-id="ce6b7-106">Vous y découvrirez également les fonctionnalités de gestion et de surveillance de Scheduler.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="ce6b7-107">Création d’un travail</span><span class="sxs-lookup"><span data-stu-id="ce6b7-107">Create a job</span></span>
1. <span data-ttu-id="ce6b7-108">Connectez-vous trop[portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ce6b7-108">Sign in too[Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="ce6b7-109">Cliquez sur **+ nouveau** > type *planificateur* dans la zone de recherche hello > sélectionnez **planificateur** dans les résultats > cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-109">Click **+New** > type *Scheduler* in hello search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="ce6b7-110">Nous allons créer un travail qui accède simplement à http://www.microsoft.com/ avec une demande GET.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="ce6b7-111">Bonjour **tâche du planificateur** écran, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ce6b7-111">In hello **Scheduler Job** screen, enter hello following information:</span></span>
   
   1. <span data-ttu-id="ce6b7-112">**Nom :**`getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="ce6b7-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="ce6b7-113">**Abonnement :** votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="ce6b7-114">**Collection de tâches :** sélectionnez une collection de tâches existante, ou cliquez sur **Créer** et entrez un nom.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="ce6b7-115">Ensuite, dans **paramètres d’Action**, définir hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="ce6b7-115">Next, in **Action Settings**, define hello following values:</span></span>
   
   1. <span data-ttu-id="ce6b7-116">**Type d’action :**` HTTP`</span><span class="sxs-lookup"><span data-stu-id="ce6b7-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="ce6b7-117">**Méthode :**`GET`</span><span class="sxs-lookup"><span data-stu-id="ce6b7-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="ce6b7-118">**URL :**` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="ce6b7-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="ce6b7-119">Pour finir, nous allons définir une planification.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="ce6b7-120">travail de Hello peut être défini comme un travail ponctuel, mais nous allons sélectionner une planification périodique :</span><span class="sxs-lookup"><span data-stu-id="ce6b7-120">hello job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="ce6b7-121">**Récurrence** : `Recurring`</span><span class="sxs-lookup"><span data-stu-id="ce6b7-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="ce6b7-122">**Début**: date du jour</span><span class="sxs-lookup"><span data-stu-id="ce6b7-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="ce6b7-123">**Répéter toutes les** : `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="ce6b7-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="ce6b7-124">**Fin**: deux jours à compter de la date du jour</span><span class="sxs-lookup"><span data-stu-id="ce6b7-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="ce6b7-125">Cliquez sur **Créer**</span><span class="sxs-lookup"><span data-stu-id="ce6b7-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="ce6b7-126">Gestion et surveillance des travaux</span><span class="sxs-lookup"><span data-stu-id="ce6b7-126">Manage and monitor jobs</span></span>
<span data-ttu-id="ce6b7-127">Une fois qu’une tâche est créée, elle s’affiche dans le tableau de bord Azure hello principal.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-127">Once a job is created, it appears in hello main Azure dashboard.</span></span> <span data-ttu-id="ce6b7-128">Cliquez sur le travail de hello et une nouvelle fenêtre s’ouvre avec hello suivant onglets :</span><span class="sxs-lookup"><span data-stu-id="ce6b7-128">Click hello job and a new window opens with hello following tabs:</span></span>

1. <span data-ttu-id="ce6b7-129">Propriétés</span><span class="sxs-lookup"><span data-stu-id="ce6b7-129">Properties</span></span>  
2. <span data-ttu-id="ce6b7-130">Paramètres d’action</span><span class="sxs-lookup"><span data-stu-id="ce6b7-130">Action Settings</span></span>  
3. <span data-ttu-id="ce6b7-131">Planification</span><span class="sxs-lookup"><span data-stu-id="ce6b7-131">Schedule</span></span>  
4. <span data-ttu-id="ce6b7-132">Historique</span><span class="sxs-lookup"><span data-stu-id="ce6b7-132">History</span></span>
5. <span data-ttu-id="ce6b7-133">Utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ce6b7-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="ce6b7-134">Propriétés</span><span class="sxs-lookup"><span data-stu-id="ce6b7-134">Properties</span></span>
<span data-ttu-id="ce6b7-135">Ces propriétés en lecture seule décrivent les métadonnées de gestion hello pour la tâche du planificateur hello.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-135">These read-only properties describe hello management metadata for hello Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="ce6b7-136">Paramètres d’action</span><span class="sxs-lookup"><span data-stu-id="ce6b7-136">Action settings</span></span>
<span data-ttu-id="ce6b7-137">En cliquant sur un travail Bonjour **travaux** écran vous permet de tooconfigure de la tâche.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-137">Clicking on a job in hello **Jobs** screen allows you tooconfigure that job.</span></span> <span data-ttu-id="ce6b7-138">Cela vous permet de configurer les paramètres avancés, si vous n’avez pas les configurer dans hello Assistant de création rapide.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-138">This lets you configure advanced settings, if you didn't configure them in hello quick-create wizard.</span></span>

<span data-ttu-id="ce6b7-139">Pour tous les types d’action, vous pouvez modifier la stratégie de nouvelle tentative hello et action d’erreur hello.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-139">For all action types, you may change hello retry policy and hello error action.</span></span>

<span data-ttu-id="ce6b7-140">Pour les types d’action de tâche HTTP et HTTPS, vous pouvez modifier tooany de méthode hello autorisé le verbe HTTP.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-140">For HTTP and HTTPS job action types, you may change hello method tooany allowed HTTP verb.</span></span> <span data-ttu-id="ce6b7-141">Vous pouvez également ajouter, supprimer ou modifier les en-têtes de hello et les informations d’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-141">You may also add, delete, or change hello headers and basic authentication information.</span></span>

<span data-ttu-id="ce6b7-142">Pour les types d’action de file d’attente de stockage, vous pouvez modifier le compte de stockage hello, nom de la file d’attente, un jeton SAS et corps.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-142">For storage queue action types, you may change hello storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="ce6b7-143">Pour les types d’action service bus, vous pouvez modifier l’espace de noms hello, chemin d’accès de rubrique/file d’attente, les paramètres d’authentification, type de transport, les propriétés de message et le corps du message.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-143">For service bus action types, you may change hello namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="ce6b7-144">Planification</span><span class="sxs-lookup"><span data-stu-id="ce6b7-144">Schedule</span></span>
<span data-ttu-id="ce6b7-145">Cela vous permet de reconfigurer la planification de hello, si vous souhaitez que la planification de hello toochange que vous avez créé dans hello Assistant de création rapide.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-145">This lets you reconfigure hello schedule, if you'd like toochange hello schedule you created in hello quick-create wizard.</span></span>

<span data-ttu-id="ce6b7-146">Il s’agit d’une opportunité toobuild [planifications complexes et périodicité avancée dans votre travail](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="ce6b7-146">This is an opportunity toobuild [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="ce6b7-147">Vous pouvez modifier la date de début hello et le temps, la planification de périodicité et hello date de fin et l’heure (si le travail de hello est périodique).</span><span class="sxs-lookup"><span data-stu-id="ce6b7-147">You may change hello start date and time, recurrence schedule, and hello end date and time (if hello job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="ce6b7-148">Historique</span><span class="sxs-lookup"><span data-stu-id="ce6b7-148">History</span></span>
<span data-ttu-id="ce6b7-149">Hello **historique** onglet affiche les métriques sélectionnées pour chaque exécution du travail dans le système hello pour la tâche sélectionnée de hello.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-149">hello **History** tab displays selected metrics for every job execution in hello system for hello selected job.</span></span> <span data-ttu-id="ce6b7-150">Ces métriques fournissent des valeurs en temps réel concernant la santé de votre planificateur hello :</span><span class="sxs-lookup"><span data-stu-id="ce6b7-150">These metrics provide real-time values regarding hello health of your Scheduler:</span></span>

1. <span data-ttu-id="ce6b7-151">État</span><span class="sxs-lookup"><span data-stu-id="ce6b7-151">Status</span></span>  
2. <span data-ttu-id="ce6b7-152">Détails</span><span class="sxs-lookup"><span data-stu-id="ce6b7-152">Details</span></span>  
3. <span data-ttu-id="ce6b7-153">Nouvelles tentatives</span><span class="sxs-lookup"><span data-stu-id="ce6b7-153">Retry attempts</span></span>
4. <span data-ttu-id="ce6b7-154">Occurrence : 1er, 2e, 3e, etc.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="ce6b7-155">Heure de début de l’exécution</span><span class="sxs-lookup"><span data-stu-id="ce6b7-155">Start time of execution</span></span>  
6. <span data-ttu-id="ce6b7-156">Heure de fin de l’exécution</span><span class="sxs-lookup"><span data-stu-id="ce6b7-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="ce6b7-157">Vous pouvez cliquer sur une exécution tooview son **détails de l’historique**, y compris la réponse entière de hello pour chaque exécution.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-157">You can click on a run tooview its **History Details**, including hello whole response for every execution.</span></span> <span data-ttu-id="ce6b7-158">Cette boîte de dialogue vous permet également de Presse-papiers de toohello toocopy hello réponse.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-158">This dialog box also allows you toocopy hello response toohello clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="ce6b7-159">Utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ce6b7-159">Users</span></span>
<span data-ttu-id="ce6b7-160">Le contrôle d’accès en fonction du rôle (RBAC) Azure permet une gestion précise de l’accès pour Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="ce6b7-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="ce6b7-161">toolearn comment toouse hello onglet utilisateurs, référence trop[du contrôle d’accès](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="ce6b7-161">toolearn how toouse hello Users tab, refer too[Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="ce6b7-162">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ce6b7-162">See also</span></span>
 [<span data-ttu-id="ce6b7-163">Présentation d'Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="ce6b7-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="ce6b7-164">Concepts, terminologie et hiérarchie d’entités de Scheduler</span><span class="sxs-lookup"><span data-stu-id="ce6b7-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="ce6b7-165">Plans et facturation dans Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="ce6b7-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="ce6b7-166">Comment toobuild complexe planifie et périodicité avancée avec Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="ce6b7-166">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="ce6b7-167">Informations de référence sur l’API REST de Scheduler</span><span class="sxs-lookup"><span data-stu-id="ce6b7-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="ce6b7-168">Informations de référence sur les applets de commande PowerShell de Scheduler</span><span class="sxs-lookup"><span data-stu-id="ce6b7-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="ce6b7-169">Haute disponibilité et fiabilité de Scheduler</span><span class="sxs-lookup"><span data-stu-id="ce6b7-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="ce6b7-170">Limites, valeurs par défaut et codes d’erreur de Scheduler</span><span class="sxs-lookup"><span data-stu-id="ce6b7-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="ce6b7-171">Authentification sortante de Scheduler</span><span class="sxs-lookup"><span data-stu-id="ce6b7-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
