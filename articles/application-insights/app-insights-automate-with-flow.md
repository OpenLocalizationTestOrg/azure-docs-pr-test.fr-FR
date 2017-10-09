---
title: aaaAutomate Azure Application Insights traite avec Microsoft Flow
description: "Découvrez comment vous pouvez utiliser Microsoft Flow tooquickly automatiser des processus reproductibles à l’aide du connecteur d’Application Insights hello."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="767a0-103">Automatiser les processus d’Application Azure Insights avec le connecteur de hello pour Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="767a0-103">Automate Azure Application Insights processes with hello connector for Microsoft Flow</span></span>

<span data-ttu-id="767a0-104">Trouver vous-même exécution répétée des mêmes requêtes hello sur votre toocheck de données de télémétrie votre service fonctionne correctement ?</span><span class="sxs-lookup"><span data-stu-id="767a0-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck that your service is functioning properly?</span></span> <span data-ttu-id="767a0-105">Est vous tooautomate recherchent ces requêtes pour rechercher des tendances et des anomalies et de générer vos propres workflows autour d’elles ? le connecteur Hello Azure Application Insights (preview) pour Microsoft Flow est un outil hello à ces fins.</span><span class="sxs-lookup"><span data-stu-id="767a0-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Microsoft Flow is hello right tool for these purposes.</span></span>

<span data-ttu-id="767a0-106">Avec cette intégration, vous pouvez désormais automatiser de nombreux processus sans écrire la moindre ligne de code.</span><span class="sxs-lookup"><span data-stu-id="767a0-106">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="767a0-107">Après avoir créé un flux à l’aide d’une action d’Application Insights, flux de hello s’exécute automatiquement votre requête d’Application Insights Analytique.</span><span class="sxs-lookup"><span data-stu-id="767a0-107">After you create a flow by using an Application Insights action, hello flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="767a0-108">Vous pouvez également ajouter des actions.</span><span class="sxs-lookup"><span data-stu-id="767a0-108">You can add additional actions as well.</span></span> <span data-ttu-id="767a0-109">Microsoft Flow met à votre disposition des centaines d’actions.</span><span class="sxs-lookup"><span data-stu-id="767a0-109">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="767a0-110">Par exemple, vous pouvez utiliser Microsoft Flow tooautomatically envoyer une notification par courrier électronique ou créer un bogue dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="767a0-110">For example, you can use Microsoft Flow tooautomatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="767a0-111">Vous pouvez également utiliser une des hello nombreux [modèles](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) qui sont disponibles pour le connecteur hello pour Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="767a0-111">You can also use one of hello many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for hello connector for Microsoft Flow.</span></span> <span data-ttu-id="767a0-112">Ces modèles accélèrent hello de création d’un flux.</span><span class="sxs-lookup"><span data-stu-id="767a0-112">These templates speed up hello process of creating a flow.</span></span> 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="767a0-113">Créer un flux pour Application Insights</span><span class="sxs-lookup"><span data-stu-id="767a0-113">Create a flow for Application Insights</span></span>

<span data-ttu-id="767a0-114">Dans ce didacticiel, vous allez apprendre comment toocreate un flux qui utilise hello Analytique auto-cluster algorithme toogroup les attributs dans les données de salutation pour une application web.</span><span class="sxs-lookup"><span data-stu-id="767a0-114">In this tutorial, you will learn how toocreate a flow that uses hello Analytics auto-cluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="767a0-115">flux de Hello envoie automatiquement les résultats de hello par courrier électronique, qu’un exemple de la façon dont vous pouvez utiliser Microsoft Flow et Application Insights Analytique ensemble.</span><span class="sxs-lookup"><span data-stu-id="767a0-115">hello flow automatically sends hello results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="767a0-116">Étape 1 : Créer un flux</span><span class="sxs-lookup"><span data-stu-id="767a0-116">Step 1: Create a flow</span></span>
1. <span data-ttu-id="767a0-117">Connectez-vous trop[Microsoft Flow](http://flow.microsoft.com), puis sélectionnez **flux Mes**.</span><span class="sxs-lookup"><span data-stu-id="767a0-117">Sign in too[Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="767a0-118">Cliquez sur **Créer un flux à partir de rien**.</span><span class="sxs-lookup"><span data-stu-id="767a0-118">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="767a0-119">Étape 2 : Créer un déclencheur pour votre flux</span><span class="sxs-lookup"><span data-stu-id="767a0-119">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="767a0-120">Sélectionnez **Planifier**, puis **Planification - Récurrence**.</span><span class="sxs-lookup"><span data-stu-id="767a0-120">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="767a0-121">Bonjour **fréquence** boîte, sélectionnez **jour**et Bonjour **intervalle** , entrez **1**.</span><span class="sxs-lookup"><span data-stu-id="767a0-121">In hello **Frequency** box, select **Day**, and in hello **Interval** box, enter **1**.</span></span>

    ![Boîte de dialogue du déclencheur de flux Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="767a0-123">Étape 3 : Ajouter une action Application Insights</span><span class="sxs-lookup"><span data-stu-id="767a0-123">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="767a0-124">Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="767a0-124">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="767a0-125">Recherchez **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="767a0-125">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="767a0-126">Cliquez sur **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights – Visualiser la requête Analytics Préversion).</span><span class="sxs-lookup"><span data-stu-id="767a0-126">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Fenêtre d’exécution de la requête Analytics](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="767a0-128">Étape 4 : Connecter des ressources d’Application Insights tooan</span><span class="sxs-lookup"><span data-stu-id="767a0-128">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="767a0-129">toocomplete cette étape, vous avez besoin d’un ID d’application et une clé d’API pour votre ressource.</span><span class="sxs-lookup"><span data-stu-id="767a0-129">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="767a0-130">Vous pouvez les récupérer à partir de hello portail Azure, comme indiqué dans hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="767a0-130">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![ID d’application Bonjour portail Azure](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="767a0-132">Fournissez un nom pour votre connexion, ainsi que de la clé API et ID d’application hello.</span><span class="sxs-lookup"><span data-stu-id="767a0-132">Provide a name for your connection, along with hello application ID and API key.</span></span>

    ![Fenêtre de connexion Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="767a0-134">Étape 5 : Spécifier hello les requête Analytique et type de graphique</span><span class="sxs-lookup"><span data-stu-id="767a0-134">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="767a0-135">Cet exemple de requête sélectionne des demandes de hello a échoué dans le dernier jour de hello et les met en corrélation avec les exceptions qui se sont produites dans le cadre de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="767a0-135">This example query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="767a0-136">Analytique les met en corrélation basée sur l’identificateur hello identifiant_opération.</span><span class="sxs-lookup"><span data-stu-id="767a0-136">Analytics correlates them based on hello operation_Id identifier.</span></span> <span data-ttu-id="767a0-137">requête de Hello puis segmente les résultats de hello en utilisant l’algorithme d’autocluster hello.</span><span class="sxs-lookup"><span data-stu-id="767a0-137">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="767a0-138">Lorsque vous créez vos propres requêtes, vérifier qu’ils fonctionnent correctement dans Analytique avant d’ajouter celui-ci tooyour flux.</span><span class="sxs-lookup"><span data-stu-id="767a0-138">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

- <span data-ttu-id="767a0-139">Ajouter hello suivant la requête de l’Analytique, puis sélectionnez le type de graphique de table HTML hello.</span><span class="sxs-lookup"><span data-stu-id="767a0-139">Add hello following Analytics query, and then select hello HTML table chart type.</span></span> 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Fenêtre de configuration de requête Analytics](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a><span data-ttu-id="767a0-141">Étape 6 : Configurer la messagerie de hello flux toosend</span><span class="sxs-lookup"><span data-stu-id="767a0-141">Step 6: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="767a0-142">Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="767a0-142">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="767a0-143">Recherchez **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="767a0-143">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="767a0-144">Cliquez sur **Office 365 Outlook – Envoyer un message électronique**.</span><span class="sxs-lookup"><span data-stu-id="767a0-144">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Fenêtre de sélection d’Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="767a0-146">Bonjour **envoyer un courrier électronique** fenêtre, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="767a0-146">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="767a0-147">a.</span><span class="sxs-lookup"><span data-stu-id="767a0-147">a.</span></span> <span data-ttu-id="767a0-148">Tapez l’adresse de messagerie hello du destinataire de hello.</span><span class="sxs-lookup"><span data-stu-id="767a0-148">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="767a0-149">b.</span><span class="sxs-lookup"><span data-stu-id="767a0-149">b.</span></span> <span data-ttu-id="767a0-150">Entrez un objet pour le courrier électronique de hello.</span><span class="sxs-lookup"><span data-stu-id="767a0-150">Type a subject for hello email.</span></span>

   <span data-ttu-id="767a0-151">c.</span><span class="sxs-lookup"><span data-stu-id="767a0-151">c.</span></span> <span data-ttu-id="767a0-152">Cliquez n’importe où dans hello **corps** zone, hello dynamique contenu menu qui s’ouvre à droite de hello, puis **corps**.</span><span class="sxs-lookup"><span data-stu-id="767a0-152">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="767a0-153">d.</span><span class="sxs-lookup"><span data-stu-id="767a0-153">d.</span></span> <span data-ttu-id="767a0-154">Cliquez sur **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="767a0-154">Click **Show advanced options**.</span></span>

    ![Configuration d’Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="767a0-156">Dans le menu de contenu dynamique hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="767a0-156">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="767a0-157">a.</span><span class="sxs-lookup"><span data-stu-id="767a0-157">a.</span></span> <span data-ttu-id="767a0-158">Sélectionnez **Nom de la pièce jointe**.</span><span class="sxs-lookup"><span data-stu-id="767a0-158">Select **Attachment Name**.</span></span>

    <span data-ttu-id="767a0-159">b.</span><span class="sxs-lookup"><span data-stu-id="767a0-159">b.</span></span> <span data-ttu-id="767a0-160">Sélectionnez **Attachment Content** (Contenu de la pièce jointe).</span><span class="sxs-lookup"><span data-stu-id="767a0-160">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="767a0-161">c.</span><span class="sxs-lookup"><span data-stu-id="767a0-161">c.</span></span> <span data-ttu-id="767a0-162">Bonjour **HTML** boîte, sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="767a0-162">In hello **Is HTML** box, select **Yes**.</span></span>

    ![Fenêtre de configuration d’e-mail Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="767a0-164">Étape 7 : Enregistrer et tester votre flux</span><span class="sxs-lookup"><span data-stu-id="767a0-164">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="767a0-165">Bonjour **nom de flux** zone, ajouter un nom pour votre flux, puis cliquez sur **créer un flux**.</span><span class="sxs-lookup"><span data-stu-id="767a0-165">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Fenêtre de création de flux](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="767a0-167">Vous pouvez attendre hello déclencheur toorun cette action, ou vous pouvez exécuter des flux de hello immédiatement par [le déclencheur hello en cours d’exécution de la demande](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="767a0-167">You can wait for hello trigger toorun this action, or you can run hello flow immediately by [running hello trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="767a0-168">Exécution de flux de hello hello que vous avez spécifié dans la liste de messagerie hello destinataires un message électronique qui ressemble à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="767a0-168">When hello flow runs, hello recipients you have specified in hello email list receive an email message that looks like hello following:</span></span>

![Exemple de message électronique](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="767a0-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="767a0-170">Next steps</span></span>

- <span data-ttu-id="767a0-171">Découvrez la création de [requêtes Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="767a0-171">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="767a0-172">Découvrez [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="767a0-172">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





