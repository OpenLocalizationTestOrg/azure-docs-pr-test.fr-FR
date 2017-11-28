---
title: Automatisez les processus Azure Application Insights en utilisant Logic Apps.
description: "Découvrez comment automatiser rapidement des processus reproductibles en ajoutant le connecteur Application Insights à votre application logique."
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
ms.openlocfilehash: 36df5bc0a019f4197d40fd6fa5a2a9957820c8b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="e7a14-103">Automatiser les processus Application Insights en utilisant Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e7a14-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="e7a14-104">Vous devez exécuter à plusieurs reprises les mêmes requêtes sur vos données de télémétrie pour vérifier le bon fonctionnement de votre service ?</span><span class="sxs-lookup"><span data-stu-id="e7a14-104">Do you find yourself repeatedly running the same queries on your telemetry data to check whether your service is functioning properly?</span></span> <span data-ttu-id="e7a14-105">Cherchez-vous à automatiser ces requêtes pour rechercher les tendances et les anomalies, puis générer vos propres flux de travail autour d’elles ?</span><span class="sxs-lookup"><span data-stu-id="e7a14-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="e7a14-106">Le connecteur Azure Application Insights (préversion) pour Logic Apps est l’outil qu’il vous faut pour atteindre cet objectif.</span><span class="sxs-lookup"><span data-stu-id="e7a14-106">The Azure Application Insights connector (preview) for Logic Apps is the right tool for this purpose.</span></span>

<span data-ttu-id="e7a14-107">Avec cette intégration, vous pouvez automatiser de nombreux processus sans écrire la moindre ligne de code.</span><span class="sxs-lookup"><span data-stu-id="e7a14-107">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="e7a14-108">Vous pouvez créer une application logique avec le connecteur Application Insights pour automatiser rapidement tous les processus Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e7a14-108">You can create a logic app with the Application Insights connector to quickly automate any Application Insights process.</span></span> 

<span data-ttu-id="e7a14-109">Vous pouvez également ajouter des actions.</span><span class="sxs-lookup"><span data-stu-id="e7a14-109">You can add additional actions as well.</span></span> <span data-ttu-id="e7a14-110">La fonctionnalité Logic Apps d’Azure App Service met à votre disposition des centaines d’actions possibles.</span><span class="sxs-lookup"><span data-stu-id="e7a14-110">The Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="e7a14-111">Par exemple, en utilisant une application logique, vous pouvez automatiquement envoyer une notification par e-mail ou créer un bogue dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e7a14-111">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="e7a14-112">Vous pouvez également utiliser l’un des nombreux [modèles](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) disponibles pour contribuer à accélérer le processus de création de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="e7a14-112">You can also use one of the many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) to help speed up the process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="e7a14-113">Créer une application logique pour Application Insights</span><span class="sxs-lookup"><span data-stu-id="e7a14-113">Create a logic app for Application Insights</span></span>

<span data-ttu-id="e7a14-114">Dans ce didacticiel, vous allez apprendre à créer une application logique qui utilise l’algorithme de cluster automatique Analytics pour regrouper des attributs dans les données pour une application web.</span><span class="sxs-lookup"><span data-stu-id="e7a14-114">In this tutorial, you learn how to create a logic app that uses the Analytics autocluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="e7a14-115">Ce flux envoie automatiquement les résultats par courrier électronique. Il s’agit d’un exemple de la façon dont vous pouvez utiliser Application Insights Analytics et Logic Apps ensemble.</span><span class="sxs-lookup"><span data-stu-id="e7a14-115">The flow automatically sends the results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="e7a14-116">Étape 1 : Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="e7a14-116">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="e7a14-117">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e7a14-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e7a14-118">Dans le volet **Nouveau**, sélectionnez **Web + mobile**, puis **Application logique**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-118">In the **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Fenêtre Nouvelle application logique](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="e7a14-120">Étape 2 : Créer un déclencheur pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="e7a14-120">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="e7a14-121">Dans la fenêtre **Concepteur d’application logique**, sous **Démarrer avec un déclencheur courant**, sélectionnez **Récurrence**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-121">In the **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Fenêtre Concepteur d’application logique](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="e7a14-123">Dans la zone **Fréquence**, sélectionnez **Jour**, puis, dans la zone **Intervalle**, tapez **1**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-123">In the **Frequency** box, select **Day** and then, in the **Interval** box, type **1**.</span></span>

    ![Fenêtre « Récurrence » du Concepteur d’application logique](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="e7a14-125">Étape 3 : Ajouter une action Application Insights</span><span class="sxs-lookup"><span data-stu-id="e7a14-125">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="e7a14-126">Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-126">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="e7a14-127">Dans la zone de recherche **Choisir une action**, tapez **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-127">In the **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="e7a14-128">Sous **Actions**, cliquez sur **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights – Visualiser la requête Analytics Préversion).</span><span class="sxs-lookup"><span data-stu-id="e7a14-128">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Fenêtre de « Choisir une action » du Concepteur d’application logique](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="e7a14-130">Étape 4 : Se connecter à une ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="e7a14-130">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="e7a14-131">Pour cette étape, vous avez besoin d’un ID d’application et d’une clé d’API pour votre ressource.</span><span class="sxs-lookup"><span data-stu-id="e7a14-131">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="e7a14-132">Vous pouvez les récupérer sur le portail Azure, comme illustré dans le schéma suivant :</span><span class="sxs-lookup"><span data-stu-id="e7a14-132">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![ID d’application dans le portail Azure](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="e7a14-134">Renseignez le nom de votre connexion, l’ID d’application et la clé d’API.</span><span class="sxs-lookup"><span data-stu-id="e7a14-134">Provide a name for your connection, the application ID, and the API key.</span></span>

![Fenêtre de connexion de flux du Concepteur d’application logique](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="e7a14-136">Étape 5 : Spécifier le type de requête et de graphique Analytics</span><span class="sxs-lookup"><span data-stu-id="e7a14-136">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="e7a14-137">Dans l’exemple suivant, la requête sélectionne les requêtes ayant échoué au cours du dernier jour et les met en corrélation avec les exceptions qui se sont produites dans le cadre de l’opération.</span><span class="sxs-lookup"><span data-stu-id="e7a14-137">In the following example, the query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="e7a14-138">Analytics met en corrélation les requêtes ayant échoué en fonction de l’identificateur operation_Id.</span><span class="sxs-lookup"><span data-stu-id="e7a14-138">Analytics correlates the failed requests, based on the operation_Id identifier.</span></span> <span data-ttu-id="e7a14-139">La requête segmente ensuite les résultats à l’aide de l’algorithme de cluster automatique.</span><span class="sxs-lookup"><span data-stu-id="e7a14-139">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="e7a14-140">Lorsque vous créez vos propres requêtes, vérifiez qu’elles fonctionnent correctement dans Analytics avant de les ajouter à votre flux.</span><span class="sxs-lookup"><span data-stu-id="e7a14-140">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

1. <span data-ttu-id="e7a14-141">Dans la zone **Requête**, ajoutez la requête Analytics suivante :</span><span class="sxs-lookup"><span data-stu-id="e7a14-141">In the **Query** box, add the following Analytics query:</span></span> 

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

2. <span data-ttu-id="e7a14-142">Dans la zone **Type de graphique**, sélectionnez **Table HTML**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-142">In the **Chart Type** box, select **Html Table**.</span></span>

    ![Fenêtre de configuration de requête Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-the-logic-app-to-send-email"></a><span data-ttu-id="e7a14-144">Étape 6 : Configurer l’application logique pour envoyer un e-mail</span><span class="sxs-lookup"><span data-stu-id="e7a14-144">Step 6: Configure the logic app to send email</span></span>

1. <span data-ttu-id="e7a14-145">Cliquez sur **Nouvelle étape**, puis sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-145">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="e7a14-146">Dans la zone de recherche, tapez **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-146">In the search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="e7a14-147">Cliquez sur **Office 365 Outlook – Envoyer un message électronique**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-147">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Sélection d’Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="e7a14-149">Dans la fenêtre **Envoyer un message électronique**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e7a14-149">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="e7a14-150">a.</span><span class="sxs-lookup"><span data-stu-id="e7a14-150">a.</span></span> <span data-ttu-id="e7a14-151">Tapez l’adresse e-mail du destinataire.</span><span class="sxs-lookup"><span data-stu-id="e7a14-151">Type the email address of the recipient.</span></span>

   <span data-ttu-id="e7a14-152">b.</span><span class="sxs-lookup"><span data-stu-id="e7a14-152">b.</span></span> <span data-ttu-id="e7a14-153">Tapez l’objet de l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="e7a14-153">Type a subject for the email.</span></span>

   <span data-ttu-id="e7a14-154">c.</span><span class="sxs-lookup"><span data-stu-id="e7a14-154">c.</span></span> <span data-ttu-id="e7a14-155">Cliquez n’importe où dans la zone **Corps**, puis, dans le menu de contenu dynamique qui s’ouvre sur la droite, sélectionnez **Corps**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-155">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="e7a14-156">d.</span><span class="sxs-lookup"><span data-stu-id="e7a14-156">d.</span></span> <span data-ttu-id="e7a14-157">Cliquez sur **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-157">Click **Show advanced options**.</span></span>

      ![Configuration d’Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="e7a14-159">Dans le menu de contenu dynamique, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e7a14-159">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="e7a14-160">a.</span><span class="sxs-lookup"><span data-stu-id="e7a14-160">a.</span></span> <span data-ttu-id="e7a14-161">Sélectionnez **Nom de la pièce jointe**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-161">Select **Attachment Name**.</span></span>

    <span data-ttu-id="e7a14-162">b.</span><span class="sxs-lookup"><span data-stu-id="e7a14-162">b.</span></span> <span data-ttu-id="e7a14-163">Sélectionnez **Attachment Content** (Contenu de la pièce jointe).</span><span class="sxs-lookup"><span data-stu-id="e7a14-163">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="e7a14-164">c.</span><span class="sxs-lookup"><span data-stu-id="e7a14-164">c.</span></span> <span data-ttu-id="e7a14-165">Dans la zone **Is HTML** (Est HTML), sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-165">In the **Is HTML** box, select **Yes**.</span></span>

      ![Écran de configuration d’e-mail Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="e7a14-167">Étape 7 : Enregistrer et tester votre application logique</span><span class="sxs-lookup"><span data-stu-id="e7a14-167">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="e7a14-168">Cliquez sur **Enregistrer** pour enregistrer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="e7a14-168">Click **Save** to save your changes.</span></span>

<span data-ttu-id="e7a14-169">Vous pouvez attendre que le déclencheur exécute l’application logique ou vous pouvez l’exécuter immédiatement en sélectionnant **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="e7a14-169">You can wait for the trigger to run the logic app, or you can run the logic app immediately by selecting **Run**.</span></span>

![Écran de création d’application logique](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="e7a14-171">Lorsque votre application logique s’exécute, les destinataires que vous avez spécifiés dans la liste des e-mails reçoivent un e-mail similaire à :</span><span class="sxs-lookup"><span data-stu-id="e7a14-171">When your logic app runs, the recipients you specified in the email list will receive an email that looks like the following:</span></span>

![Message électronique de l’application logique](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="e7a14-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e7a14-173">Next steps</span></span>

- <span data-ttu-id="e7a14-174">Apprenez-en plus sur la création de [requêtes Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="e7a14-174">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="e7a14-175">Découvrez plus en détail les [applications logiques](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="e7a14-175">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





