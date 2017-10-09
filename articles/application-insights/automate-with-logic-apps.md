---
title: "aaaAutomate Azure Application Insights traite à l’aide de Logic Apps."
description: "Découvrez comment vous pouvez automatiser des processus reproductibles rapidement en ajoutant l’application logique de hello Application Insights connecteur tooyour."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="84e31-103">Automatiser les processus Application Insights en utilisant Logic Apps</span><span class="sxs-lookup"><span data-stu-id="84e31-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="84e31-104">Trouver vous-même exécution répétée hello mêmes requêtes sur votre toocheck de données de télémétrie si votre service fonctionne correctement ?</span><span class="sxs-lookup"><span data-stu-id="84e31-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck whether your service is functioning properly?</span></span> <span data-ttu-id="84e31-105">Est vous tooautomate recherchent ces requêtes pour rechercher des tendances et des anomalies et de générer vos propres workflows autour d’elles ? le connecteur Hello Azure Application Insights (preview) pour les applications de la logique est un outil hello à cet effet.</span><span class="sxs-lookup"><span data-stu-id="84e31-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Logic Apps is hello right tool for this purpose.</span></span>

<span data-ttu-id="84e31-106">Avec cette intégration, vous pouvez automatiser de nombreux processus sans écrire la moindre ligne de code.</span><span class="sxs-lookup"><span data-stu-id="84e31-106">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="84e31-107">Vous pouvez créer une application de logique hello Application Insights connecteur tooquickly automatiser n’importe quel processus d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="84e31-107">You can create a logic app with hello Application Insights connector tooquickly automate any Application Insights process.</span></span> 

<span data-ttu-id="84e31-108">Vous pouvez également ajouter des actions.</span><span class="sxs-lookup"><span data-stu-id="84e31-108">You can add additional actions as well.</span></span> <span data-ttu-id="84e31-109">fonctionnalité de Logic Apps Hello du Service d’applications Azure rend des centaines d’actions disponibles.</span><span class="sxs-lookup"><span data-stu-id="84e31-109">hello Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="84e31-110">Par exemple, en utilisant une application logique, vous pouvez automatiquement envoyer une notification par e-mail ou créer un bogue dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="84e31-110">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="84e31-111">Vous pouvez également utiliser une des hello nombreux disponible [modèles](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp accélérer hello de créer votre logique d’application.</span><span class="sxs-lookup"><span data-stu-id="84e31-111">You can also use one of hello many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp speed up hello process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="84e31-112">Créer une application logique pour Application Insights</span><span class="sxs-lookup"><span data-stu-id="84e31-112">Create a logic app for Application Insights</span></span>

<span data-ttu-id="84e31-113">Dans ce didacticiel, vous découvrez comment toocreate une application de logique qui utilise hello Analytique autocluster algorithme toogroup les attributs dans les données de salutation pour une application web.</span><span class="sxs-lookup"><span data-stu-id="84e31-113">In this tutorial, you learn how toocreate a logic app that uses hello Analytics autocluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="84e31-114">flux de Hello envoie automatiquement les résultats de hello par courrier électronique, qu’un exemple de comment vous pouvez utiliser Application Insights Analytique et Logic Apps ensemble.</span><span class="sxs-lookup"><span data-stu-id="84e31-114">hello flow automatically sends hello results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="84e31-115">Étape 1 : Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="84e31-115">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="84e31-116">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84e31-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="84e31-117">Bonjour **nouveau** volet, sélectionnez **Web + Mobile**, puis sélectionnez **application logique**.</span><span class="sxs-lookup"><span data-stu-id="84e31-117">In hello **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Fenêtre Nouvelle application logique](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="84e31-119">Étape 2 : Créer un déclencheur pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="84e31-119">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="84e31-120">Bonjour **Concepteur d’application logique** fenêtre, sous **commencer par un déclencheur commun**, sélectionnez **périodicité**.</span><span class="sxs-lookup"><span data-stu-id="84e31-120">In hello **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Fenêtre Concepteur d’application logique](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="84e31-122">Bonjour **fréquence** boîte, sélectionnez **jour** , puis, dans hello **intervalle** , tapez **1**.</span><span class="sxs-lookup"><span data-stu-id="84e31-122">In hello **Frequency** box, select **Day** and then, in hello **Interval** box, type **1**.</span></span>

    ![Fenêtre « Récurrence » du Concepteur d’application logique](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="84e31-124">Étape 3 : Ajouter une action Application Insights</span><span class="sxs-lookup"><span data-stu-id="84e31-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="84e31-125">Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="84e31-125">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="84e31-126">Bonjour **choisir une action** zone de recherche, tapez **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="84e31-126">In hello **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="84e31-127">Sous **Actions**, cliquez sur **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights – Visualiser la requête Analytics Préversion).</span><span class="sxs-lookup"><span data-stu-id="84e31-127">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Fenêtre de « Choisir une action » du Concepteur d’application logique](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="84e31-129">Étape 4 : Connecter des ressources d’Application Insights tooan</span><span class="sxs-lookup"><span data-stu-id="84e31-129">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="84e31-130">toocomplete cette étape, vous avez besoin d’un ID d’application et une clé d’API pour votre ressource.</span><span class="sxs-lookup"><span data-stu-id="84e31-130">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="84e31-131">Vous pouvez les récupérer à partir de hello portail Azure, comme indiqué dans hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="84e31-131">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![ID d’application Bonjour portail Azure](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="84e31-133">Fournissez un nom pour votre connexion, un ID de l’application hello et une clé d’API hello.</span><span class="sxs-lookup"><span data-stu-id="84e31-133">Provide a name for your connection, hello application ID, and hello API key.</span></span>

![Fenêtre de connexion de flux du Concepteur d’application logique](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="84e31-135">Étape 5 : Spécifier hello les requête Analytique et type de graphique</span><span class="sxs-lookup"><span data-stu-id="84e31-135">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="84e31-136">Bonjour l’exemple suivant, les requêtes hello sélectionne des demandes de hello a échoué dans le dernier jour de hello et les met en corrélation avec les exceptions qui se sont produites dans le cadre de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="84e31-136">In hello following example, hello query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="84e31-137">Analytique met en corrélation les demandes hello a échoué, basées sur l’identificateur hello identifiant_opération.</span><span class="sxs-lookup"><span data-stu-id="84e31-137">Analytics correlates hello failed requests, based on hello operation_Id identifier.</span></span> <span data-ttu-id="84e31-138">requête de Hello puis segmente les résultats de hello en utilisant l’algorithme d’autocluster hello.</span><span class="sxs-lookup"><span data-stu-id="84e31-138">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="84e31-139">Lorsque vous créez vos propres requêtes, vérifier qu’ils fonctionnent correctement dans Analytique avant d’ajouter celui-ci tooyour flux.</span><span class="sxs-lookup"><span data-stu-id="84e31-139">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

1. <span data-ttu-id="84e31-140">Bonjour **requête** zone, ajouter hello suivant les requête Analytique :</span><span class="sxs-lookup"><span data-stu-id="84e31-140">In hello **Query** box, add hello following Analytics query:</span></span> 

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

2. <span data-ttu-id="84e31-141">Bonjour **Type de graphique** boîte, sélectionnez **Html Table**.</span><span class="sxs-lookup"><span data-stu-id="84e31-141">In hello **Chart Type** box, select **Html Table**.</span></span>

    ![Fenêtre de configuration de requête Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a><span data-ttu-id="84e31-143">Étape 6 : Configurer la messagerie de toosend application hello logique</span><span class="sxs-lookup"><span data-stu-id="84e31-143">Step 6: Configure hello logic app toosend email</span></span>

1. <span data-ttu-id="84e31-144">Cliquez sur **Nouvelle étape**, puis sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="84e31-144">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="84e31-145">Dans la zone de recherche de hello, tapez **Outlook Office 365**.</span><span class="sxs-lookup"><span data-stu-id="84e31-145">In hello search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="84e31-146">Cliquez sur **Office 365 Outlook – Envoyer un message électronique**.</span><span class="sxs-lookup"><span data-stu-id="84e31-146">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Sélection d’Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="84e31-148">Bonjour **envoyer un courrier électronique** fenêtre, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="84e31-148">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="84e31-149">a.</span><span class="sxs-lookup"><span data-stu-id="84e31-149">a.</span></span> <span data-ttu-id="84e31-150">Tapez l’adresse de messagerie hello du destinataire de hello.</span><span class="sxs-lookup"><span data-stu-id="84e31-150">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="84e31-151">b.</span><span class="sxs-lookup"><span data-stu-id="84e31-151">b.</span></span> <span data-ttu-id="84e31-152">Entrez un objet pour le courrier électronique de hello.</span><span class="sxs-lookup"><span data-stu-id="84e31-152">Type a subject for hello email.</span></span>

   <span data-ttu-id="84e31-153">c.</span><span class="sxs-lookup"><span data-stu-id="84e31-153">c.</span></span> <span data-ttu-id="84e31-154">Cliquez n’importe où dans hello **corps** zone, hello dynamique contenu menu qui s’ouvre à droite de hello, puis **corps**.</span><span class="sxs-lookup"><span data-stu-id="84e31-154">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="84e31-155">d.</span><span class="sxs-lookup"><span data-stu-id="84e31-155">d.</span></span> <span data-ttu-id="84e31-156">Cliquez sur **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="84e31-156">Click **Show advanced options**.</span></span>

      ![Configuration d’Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="84e31-158">Dans le menu de contenu dynamique hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="84e31-158">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="84e31-159">a.</span><span class="sxs-lookup"><span data-stu-id="84e31-159">a.</span></span> <span data-ttu-id="84e31-160">Sélectionnez **Nom de la pièce jointe**.</span><span class="sxs-lookup"><span data-stu-id="84e31-160">Select **Attachment Name**.</span></span>

    <span data-ttu-id="84e31-161">b.</span><span class="sxs-lookup"><span data-stu-id="84e31-161">b.</span></span> <span data-ttu-id="84e31-162">Sélectionnez **Attachment Content** (Contenu de la pièce jointe).</span><span class="sxs-lookup"><span data-stu-id="84e31-162">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="84e31-163">c.</span><span class="sxs-lookup"><span data-stu-id="84e31-163">c.</span></span> <span data-ttu-id="84e31-164">Bonjour **HTML** boîte, sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="84e31-164">In hello **Is HTML** box, select **Yes**.</span></span>

      ![Écran de configuration d’e-mail Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="84e31-166">Étape 7 : Enregistrer et tester votre application logique</span><span class="sxs-lookup"><span data-stu-id="84e31-166">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="84e31-167">Cliquez sur **enregistrer** toosave vos modifications.</span><span class="sxs-lookup"><span data-stu-id="84e31-167">Click **Save** toosave your changes.</span></span>

<span data-ttu-id="84e31-168">Vous pouvez attendre d’application logique de hello déclencheur toorun hello, ou vous pouvez exécuter immédiatement hello logique application en sélectionnant **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="84e31-168">You can wait for hello trigger toorun hello logic app, or you can run hello logic app immediately by selecting **Run**.</span></span>

![Écran de création d’application logique](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="84e31-170">Lorsque votre application logique s’exécute, les destinataires hello que vous avez spécifié dans la liste de messagerie hello recevra un e-mail qui ressemble à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="84e31-170">When your logic app runs, hello recipients you specified in hello email list will receive an email that looks like hello following:</span></span>

![Message électronique de l’application logique](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="84e31-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84e31-172">Next steps</span></span>

- <span data-ttu-id="84e31-173">Apprenez-en plus sur la création de [requêtes Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="84e31-173">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="84e31-174">Découvrez plus en détail les [applications logiques](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="84e31-174">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





