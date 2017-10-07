---
title: "état d’aaaCheck, configurez la journalisation et recevoir des alertes - Azure Logic Apps | Documents Microsoft"
description: "Surveiller l’état et les performances des applications logiques, journaliser les données de diagnostic et configurer les alertes"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="36f84-103">Surveiller l’état, configurer la journalisation des diagnostics et activer les alertes pour Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="36f84-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="36f84-104">Après avoir [créé et exécuté une application logique](../logic-apps/logic-apps-create-a-logic-app.md), vous pouvez vérifier son historique d’exécutions, son historique du déclencheur, son état et ses performances.</span><span class="sxs-lookup"><span data-stu-id="36f84-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="36f84-105">Pour une surveillance des événements en temps réel et un débogage enrichi, configurez une [journalisation des diagnostics](#azure-diagnostics) pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="36f84-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="36f84-106">De cette façon, vous pouvez [rechercher et consulter des événements](#find-events), tels que des événements de déclencheur, des événements d’exécution et des événements d’action.</span><span class="sxs-lookup"><span data-stu-id="36f84-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="36f84-107">Vous pouvez également utiliser ces [données de diagnostic avec d’autres services](#extend-diagnostic-data), tels que Stockage Azure et Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="36f84-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="36f84-108">configurer des notifications tooget sur les erreurs ou d’autres problèmes possibles, [alertes](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="36f84-108">tooget notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="36f84-109">Par exemple, vous pouvez créer une alerte qui détecte quand plus de cinq exécutions échouent en une heure.</span><span class="sxs-lookup"><span data-stu-id="36f84-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="36f84-110">Vous pouvez également configurer la surveillance, le suivi et journalisation par programme à l’aide des [Paramètres et propriétés d’événements de Diagnostics Azure](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="36f84-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="36f84-111">Afficher l’historique des exécutions et du déclencheur pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="36f84-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="36f84-112">toofind votre application logique Bonjour [portail Azure](https://portal.azure.com), on hello menu Azure principal, choisissez **davantage de services**.</span><span class="sxs-lookup"><span data-stu-id="36f84-112">toofind your logic app in hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **More services**.</span></span> <span data-ttu-id="36f84-113">Dans la zone de recherche de hello, recherchez « logic apps », puis choisissez **Logic apps**.</span><span class="sxs-lookup"><span data-stu-id="36f84-113">In hello search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Trouver votre application logique](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="36f84-115">Hello portail Azure affiche toutes les applications de la logique de hello qui sont associées à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="36f84-115">hello Azure portal shows all hello logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="36f84-116">Sélectionnez votre application logique, puis choisissez **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="36f84-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="36f84-117">Hello portail Azure affiche l’historique de l’hello s’exécute et déclencheur pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="36f84-117">hello Azure portal shows hello runs history and trigger history for your logic app.</span></span> <span data-ttu-id="36f84-118">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="36f84-118">For example:</span></span>

   ![Historique des exécutions et l’historique du déclencheur de l’application logique](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="36f84-120">**Exécute l’historique** montre toutes les séries de hello pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="36f84-120">**Runs history** shows all hello runs for your logic app.</span></span> 
   * <span data-ttu-id="36f84-121">**Déclencher l’historique** montre toutes les activités de déclencheur hello pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="36f84-121">**Trigger History** shows all hello trigger activity for your logic app.</span></span>

   <span data-ttu-id="36f84-122">Pour des descriptions d’état, voir [Dépanner votre application logique](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="36f84-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="36f84-123">Si vous ne trouvez pas les données de salutation que vous attendez, sur la barre d’outils de hello, choisissez **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="36f84-123">If you don't find hello data that you expect, on hello toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="36f84-124">tooview hello d’étapes à partir d’une exécution spécifique, sous **exécute historique**, sélectionnez qui s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="36f84-124">tooview hello steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="36f84-125">Hello moniteur affiche chaque étape dans cette série.</span><span class="sxs-lookup"><span data-stu-id="36f84-125">hello monitor view shows each step in that run.</span></span> <span data-ttu-id="36f84-126">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="36f84-126">For example:</span></span>

   ![Actions d’une exécution spécifique](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="36f84-128">Choisissez de plus de détails sur hello exécuter, tooget **détails de l’exécution**.</span><span class="sxs-lookup"><span data-stu-id="36f84-128">tooget more details about hello run, choose **Run Details**.</span></span> <span data-ttu-id="36f84-129">Ces informations résume les étapes de hello, état, les entrées et sorties hello pour les exécuter.</span><span class="sxs-lookup"><span data-stu-id="36f84-129">This information summarizes hello steps, status, inputs, and outputs for hello run.</span></span> 

   ![Choisir « Détails de l’exécution »](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="36f84-131">Par exemple, vous pouvez obtenir hello d’exécution **ID de corrélation**, dont vous pouvez avoir besoin lorsque vous utilisez hello [API REST pour Logic Apps](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="36f84-131">For example, you can get hello run's **Correlation ID**, which you might need when you use hello [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="36f84-132">tooget plus d’informations sur une étape spécifique, cliquez sur cette étape.</span><span class="sxs-lookup"><span data-stu-id="36f84-132">tooget details about a specific step, choose that step.</span></span> <span data-ttu-id="36f84-133">Vous pouvez maintenant examiner des détails tels que les entrées, les sorties et les erreurs qui se sont produites pour cette étape.</span><span class="sxs-lookup"><span data-stu-id="36f84-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="36f84-134">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="36f84-134">For example:</span></span>

   ![Détails de l’étape](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="36f84-136">Tous les événements et les détails de l’exécution sont chiffrées dans hello service de Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="36f84-136">All runtime details and events are encrypted within hello Logic Apps service.</span></span> <span data-ttu-id="36f84-137">Elles sont déchiffrées uniquement lorsqu’un utilisateur demande tooview ces données.</span><span class="sxs-lookup"><span data-stu-id="36f84-137">They are decrypted only when a user requests tooview that data.</span></span> <span data-ttu-id="36f84-138">Vous pouvez également contrôler les événements d’accès aux toothese avec [du contrôle d’accès (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="36f84-138">You can also control access toothese events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="36f84-139">tooget plus d’informations sur un événement déclencheur spécifique, revenez en arrière toohello **vue d’ensemble** volet.</span><span class="sxs-lookup"><span data-stu-id="36f84-139">tooget details about a specific trigger event, go back toohello **Overview** pane.</span></span> <span data-ttu-id="36f84-140">Sous **déclencher l’historique**, sélectionnez d’événements déclencheurs hello.</span><span class="sxs-lookup"><span data-stu-id="36f84-140">Under **Trigger history**, select hello trigger event.</span></span> <span data-ttu-id="36f84-141">Vous pouvez maintenant examiner des détails tels que les entrées et sorties, par exemple :</span><span class="sxs-lookup"><span data-stu-id="36f84-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Détails de sortie d’événement déclencheur](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="36f84-143">Activer la journalisation des diagnostics pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="36f84-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="36f84-144">Pour un débogage enrichi avec des détails et événements d’exécution, vous pouvez configurer la journalisation des diagnostics avec [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36f84-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="36f84-145">Analytique de journal est un service de [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) qui surveille votre cloud et locales toohelp environnements vous maintenir leur disponibilité et les performances.</span><span class="sxs-lookup"><span data-stu-id="36f84-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments toohelp you maintain their availability and performance.</span></span> 

<span data-ttu-id="36f84-146">Avant de commencer, vous devez toohave un espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="36f84-146">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="36f84-147">En savoir plus [comment toocreate un espace de travail OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="36f84-147">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="36f84-148">Bonjour [portail Azure](https://portal.azure.com), recherchez et sélectionnez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="36f84-148">In hello [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="36f84-149">Sur le menu de panneau application hello logique, sous **analyse**, choisissez **Diagnostics** > **les paramètres de Diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="36f84-149">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Accédez tooMonitoring, Diagnostics, les paramètres de Diagnostic](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="36f84-151">Sous **Paramètres de diagnostic**, choisissez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="36f84-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Activer les journaux de diagnostic](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="36f84-153">Sélectionnez maintenant hello OMS espace de travail et les événements catégorie journalisation comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="36f84-153">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="36f84-154">Sélectionnez **envoyer tooLog Analytique**.</span><span class="sxs-lookup"><span data-stu-id="36f84-154">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="36f84-155">Sous **Log Analytics**, choisissez **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="36f84-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="36f84-156">Sous **espaces de travail OMS**, sélectionnez toouse d’espace de travail OMS hello pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="36f84-156">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="36f84-157">Sous **journal**, sélectionnez hello **WorkflowRuntime** catégorie.</span><span class="sxs-lookup"><span data-stu-id="36f84-157">Under **Log**, select hello **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="36f84-158">Choisir l’intervalle de métrique hello.</span><span class="sxs-lookup"><span data-stu-id="36f84-158">Choose hello metric interval.</span></span>
   6. <span data-ttu-id="36f84-159">Une fois ces opérations effectuées, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="36f84-159">When you're done, choose **Save**.</span></span>

   ![Sélectionner l’espace de travail OMS et les données à journaliser](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="36f84-161">À présent, vous pouvez trouver des événements et d’autres données pour des événements déclencheurs, des événements d’exécution et des événements d’action.</span><span class="sxs-lookup"><span data-stu-id="36f84-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="36f84-162">Rechercher des événements et des données pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="36f84-162">Find events and data for your logic app</span></span>

<span data-ttu-id="36f84-163">toofind et affichage des événements dans votre application logique, telles que les événements déclencheurs, exécuter des événements et les événements d’action, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="36f84-163">toofind and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="36f84-164">Bonjour [portail Azure](https://portal.azure.com), choisissez **plus Services**.</span><span class="sxs-lookup"><span data-stu-id="36f84-164">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="36f84-165">Recherchez « log analytics », puis choisissez **Log Analytics** comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="36f84-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Choisir « Log Analytics »](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="36f84-167">Sous **Log Analytics**, recherchez et sélectionnez votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="36f84-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Sélectionner votre espace de travail OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="36f84-169">Sous **Gestion**, choisissez **Portail OMS**.</span><span class="sxs-lookup"><span data-stu-id="36f84-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![Choisir « Portail OMS »](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="36f84-171">Dans votre page d’accueil d’OMS, choisissez **Recherche dans les journaux**.</span><span class="sxs-lookup"><span data-stu-id="36f84-171">On your OMS home page, choose **Log Search**.</span></span>

   ![Dans votre page d’accueil d’OMS, choisissez « Recherche dans les journaux »](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="36f84-173">-ou-</span><span class="sxs-lookup"><span data-stu-id="36f84-173">-or-</span></span>

   ![Menu hello OMS, choisissez « Recherche de journal »](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="36f84-175">Dans la zone de recherche de hello, spécifier un champ que vous souhaitez toofind, puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="36f84-175">In hello search box, specify a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="36f84-176">Lorsque vous commencez à taper, OMS affiche les correspondances possibles et les opérations que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="36f84-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="36f84-177">Par exemple, toofind hello 10 premiers événements qui se sont produites, entrez et sélectionner cette requête de recherche : **catégorie = WorkflowRuntime | top 10**</span><span class="sxs-lookup"><span data-stu-id="36f84-177">For example, toofind hello top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Entrer une chaîne de recherche](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="36f84-179">En savoir plus sur [comment toofind les données dans le journal Analytique](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="36f84-179">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="36f84-180">Sur la page de résultats hello, dans la barre de gauche hello, choisissez hello laps de temps que vous souhaitez tooview.</span><span class="sxs-lookup"><span data-stu-id="36f84-180">On hello results page, in hello left bar, choose hello timeframe that you want tooview.</span></span>
<span data-ttu-id="36f84-181">Choisissez de votre requête en ajoutant un filtre, toorefine **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="36f84-181">toorefine your query by adding a filter, choose **+Add**.</span></span>

   ![Choisir un plage de temps pour les résultats de la requête](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="36f84-183">Sous **ajouter des filtres**, entrez le nom du filtre hello afin que vous puissiez rechercher hello du filtre.</span><span class="sxs-lookup"><span data-stu-id="36f84-183">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="36f84-184">Sélectionnez le filtre de hello, puis choisissez **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="36f84-184">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="36f84-185">Cet exemple utilise hello word « état » toofind Échec d’événements sous **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="36f84-185">This example uses hello word "status" toofind failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="36f84-186">Hello ici de filtre pour **status_s** est déjà sélectionné.</span><span class="sxs-lookup"><span data-stu-id="36f84-186">Here hello filter for **status_s** is already selected.</span></span>

   ![Sélectionner le filtre](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="36f84-188">Dans la barre de gauche hello, sélectionnez valeur hello du filtre que vous souhaitez toouse, choisissez **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="36f84-188">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   ![Sélectionner la valeur de filtre, choisir « Appliquer »](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="36f84-190">Requête toohello retournent désormais que vous générez.</span><span class="sxs-lookup"><span data-stu-id="36f84-190">Now return toohello query that you're building.</span></span> <span data-ttu-id="36f84-191">Votre requête est mis à jour avec le filtre et la valeur sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="36f84-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="36f84-192">Vos résultats précédents sont à présent également filtrés.</span><span class="sxs-lookup"><span data-stu-id="36f84-192">Your previous results are now filtered too.</span></span>

   ![Retourne la requête tooyour résultats filtrés](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="36f84-194">Choisissez de votre requête pour une utilisation ultérieure toosave **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="36f84-194">toosave your query for future use, choose **Save**.</span></span> <span data-ttu-id="36f84-195">En savoir plus [comment toosave votre requête](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="36f84-195">Learn [how toosave your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="36f84-196">Étendre la manière dont vous utilisez les données de diagnostic et l’emplacement où vous les utilisez avec d’autres services</span><span class="sxs-lookup"><span data-stu-id="36f84-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="36f84-197">Avec Azure Log Analytics, vous pouvez étendre le mode d’utilisation des données de diagnostic de votre application logique avec d’autres services Azure, par exemple :</span><span class="sxs-lookup"><span data-stu-id="36f84-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="36f84-198">Archivage des journaux de diagnostic Azure</span><span class="sxs-lookup"><span data-stu-id="36f84-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="36f84-199">Flux de données des journaux de Diagnostics Azure tooAzure concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="36f84-199">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="36f84-200">Vous pouvez ensuite obtenir une surveillance en temps réel en utilisant les ressources de télémétrie et d’analyse d’autres services, tels que [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) et [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="36f84-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="36f84-201">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="36f84-201">For example:</span></span>

* [<span data-ttu-id="36f84-202">Données de flux de données à partir de concentrateurs d’événements tooStream Analytique</span><span class="sxs-lookup"><span data-stu-id="36f84-202">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="36f84-203">Analyser les données de diffusion avec Stream Analytics et créer un tableau de bord analytique en temps réel dans Power BI</span><span class="sxs-lookup"><span data-stu-id="36f84-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="36f84-204">Selon les options de hello que vous voulez configurer, assurez-vous que vous première [créer un compte de stockage Azure](../storage/common/storage-create-storage-account.md) ou [créer un concentrateur d’événements Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="36f84-204">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="36f84-205">Puis sélectionnez les options de hello où vous souhaitez toosend les données de diagnostic :</span><span class="sxs-lookup"><span data-stu-id="36f84-205">Then select hello options for where you want toosend diagnostic data:</span></span>

![Envoyer des données tooAzure stockage compte ou événement un concentrateur](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="36f84-207">Périodes de rétention s’appliquent uniquement lorsque vous choisissez un compte de stockage toouse.</span><span class="sxs-lookup"><span data-stu-id="36f84-207">Retention periods apply only when you choose toouse a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="36f84-208">Configurer des alertes pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="36f84-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="36f84-209">toomonitor des métriques spécifiques ou dépassement des seuils pour votre application logique, configurez [alertes dans Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="36f84-209">toomonitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="36f84-210">En savoir plus sur les [métriques dans Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="36f84-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="36f84-211">tooset des alertes sans [Analytique de journal Azure](../log-analytics/log-analytics-overview.md), procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="36f84-211">tooset up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="36f84-212">Pour des critères et actions d’alertes plus avancés, [configurez également Log Analytics](#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="36f84-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="36f84-213">Sur le menu de panneau application hello logique, sous **analyse**, choisissez **Diagnostics** > **règles d’alerte** > **ajouter une alerte**comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="36f84-213">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Ajouter une alerte pour votre application logique](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="36f84-215">Sur hello **ajouter une règle d’alerte** panneau, créer votre alerte comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="36f84-215">On hello **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="36f84-216">Sous **Ressource**, sélectionnez votre application logique si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="36f84-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="36f84-217">Donnez un nom et une description à votre alerte.</span><span class="sxs-lookup"><span data-stu-id="36f84-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="36f84-218">Sélectionnez un **métrique** ou l’événement que vous souhaitez tootrack.</span><span class="sxs-lookup"><span data-stu-id="36f84-218">Select a **Metric** or event that you want tootrack.</span></span>
   4. <span data-ttu-id="36f84-219">Sélectionnez un **Condition**, spécifiez un **seuil** pour la métrique de hello et sélectionnez hello **période** pour l’analyse de cette mesure.</span><span class="sxs-lookup"><span data-stu-id="36f84-219">Select a **Condition**, specify a **Threshold** for hello metric, and select hello **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="36f84-220">Indiquez si toosend de messagerie pour l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="36f84-220">Select whether toosend mail for hello alert.</span></span> 
   6. <span data-ttu-id="36f84-221">Spécifiez des adresses de messagerie pour l’envoi d’une alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="36f84-221">Specify any other email addresses for sending hello alert.</span></span> 
   <span data-ttu-id="36f84-222">Vous pouvez également spécifier une URL webhook où vous souhaitez l’alerte de hello toosend.</span><span class="sxs-lookup"><span data-stu-id="36f84-222">You can also specify a webhook URL where you want toosend hello alert.</span></span>

   <span data-ttu-id="36f84-223">Par exemple, cette règle envoie une alerte quand cinq exécutions ou plus échouent par heure :</span><span class="sxs-lookup"><span data-stu-id="36f84-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Créer une règle d’alerte de métrique](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="36f84-225">toorun une application de la logique d’une alerte, vous pouvez inclure hello [déclencheur de demande](../connectors/connectors-native-reqres.md) dans votre flux de travail, ce qui vous permet d’effectuer des tâches telles que les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="36f84-225">toorun a logic app from an alert, you can include hello [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="36f84-226">Post tooSlack</span><span class="sxs-lookup"><span data-stu-id="36f84-226">Post tooSlack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="36f84-227">Envoyer un texte</span><span class="sxs-lookup"><span data-stu-id="36f84-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="36f84-228">Ajouter une file d’attente de messages tooa</span><span class="sxs-lookup"><span data-stu-id="36f84-228">Add a message tooa queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="36f84-229">Paramètres et détails d’événements Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="36f84-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="36f84-230">Chaque événement de diagnostic a plus d’informations sur votre application logique et que l’événement, par exemple, l’état hello, heure de début, heure de fin et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="36f84-230">Each diagnostic event has details about your logic app and that event, for example, hello status, start time, end time, and so on.</span></span> <span data-ttu-id="36f84-231">tooprogrammatically configurer la surveillance, le suivi et la journalisation, vous pouvez utiliser ces informations avec hello [API REST pour Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) et hello [API REST pour les Diagnostics Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="36f84-231">tooprogrammatically set up monitoring, tracking, and logging, ou can use these details with hello [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and hello [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="36f84-232">Par exemple, hello `ActionCompleted` événement a hello `clientTrackingId` et `trackedProperties` les propriétés que vous pouvez utiliser pour le suivi et l’analyse :</span><span class="sxs-lookup"><span data-stu-id="36f84-232">For example, hello `ActionCompleted` event has hello `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* <span data-ttu-id="36f84-233">`clientTrackingId`: Si ce n’est pas fourni, Azure génère cet ID et met en corrélation des événements dans une application logique s’exécuter automatiquement, y compris les workflows imbriqués qui sont appelées à partir de l’application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="36f84-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from hello logic app.</span></span> <span data-ttu-id="36f84-234">Vous pouvez spécifier manuellement cet ID à partir d’un déclencheur en passant un `x-ms-client-tracking-id` en-tête avec votre valeur d’ID personnalisé dans la demande de déclencheur hello.</span><span class="sxs-lookup"><span data-stu-id="36f84-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in hello trigger request.</span></span> <span data-ttu-id="36f84-235">Vous pouvez utiliser un déclencheur de demande, un déclencheur HTTP ou un déclencheur de webhook.</span><span class="sxs-lookup"><span data-stu-id="36f84-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="36f84-236">`trackedProperties`: tootrack entrées ou des sorties dans les données de diagnostic, vous pouvez ajouter les propriétés suivies tooactions dans la définition de JSON de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="36f84-236">`trackedProperties`: tootrack inputs or outputs in diagnostics data, you can add tracked properties tooactions in your logic app's JSON definition.</span></span> <span data-ttu-id="36f84-237">Les propriétés suivies peuvent suivre seulement une seule action entrées et sorties, mais vous pouvez utiliser hello `correlation` propriétés de toocorrelate d’événements entre les actions dans une série de tests.</span><span class="sxs-lookup"><span data-stu-id="36f84-237">Tracked properties can track only a single action's inputs and outputs, but you can use hello `correlation` properties of events toocorrelate across actions in a run.</span></span>

  <span data-ttu-id="36f84-238">tootrack une ou plusieurs propriétés, ajouter hello `trackedProperties` section et hello propriétés toohello définition d’action.</span><span class="sxs-lookup"><span data-stu-id="36f84-238">tootrack one or more properties, add hello `trackedProperties` section and hello properties you want toohello action definition.</span></span> <span data-ttu-id="36f84-239">Par exemple, vous souhaitez que des données de tootrack comme un « ID de commande » de votre télémétrie :</span><span class="sxs-lookup"><span data-stu-id="36f84-239">For example, suppose you want tootrack data like an "order ID" in your telemetry:</span></span>

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="36f84-240">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36f84-240">Next steps</span></span>

* [<span data-ttu-id="36f84-241">Création de modèles pour le déploiement d’applications logiques et la gestion des versions</span><span class="sxs-lookup"><span data-stu-id="36f84-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="36f84-242">Scénarios B2B et communication avec Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="36f84-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="36f84-243">Surveiller les messages B2B</span><span class="sxs-lookup"><span data-stu-id="36f84-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)