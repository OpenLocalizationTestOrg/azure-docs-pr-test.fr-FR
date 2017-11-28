---
title: Automatiser les processus Azure Application Insights avec Microsoft Flow
description: "Découvrez comment utiliser Microsoft Flow pour automatiser rapidement des processus reproductibles en utilisant le connecteur Application Insights."
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
ms.openlocfilehash: 510f4f284bbd0dbe4171896899f7ade7dee19e39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="automate-azure-application-insights-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="230ea-103">Automatiser les processus Azure Application Insights avec le connecteur pour Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="230ea-103">Automate Azure Application Insights processes with the connector for Microsoft Flow</span></span>

<span data-ttu-id="230ea-104">Vous devez exécuter à plusieurs reprises les mêmes requêtes sur vos données de télémétrie pour vérifier le bon fonctionnement de votre service ?</span><span class="sxs-lookup"><span data-stu-id="230ea-104">Do you find yourself repeatedly running the same queries on your telemetry data to check that your service is functioning properly?</span></span> <span data-ttu-id="230ea-105">Cherchez-vous à automatiser ces requêtes pour rechercher les tendances et les anomalies, puis générer vos propres flux de travail autour d’elles ?</span><span class="sxs-lookup"><span data-stu-id="230ea-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="230ea-106">Le connecteur Azure Application Insights (préversion) pour Microsoft Flow est l’outil adapté à ces objectifs.</span><span class="sxs-lookup"><span data-stu-id="230ea-106">The Azure Application Insights connector (preview) for Microsoft Flow is the right tool for these purposes.</span></span>

<span data-ttu-id="230ea-107">Avec cette intégration, vous pouvez désormais automatiser de nombreux processus sans écrire la moindre ligne de code.</span><span class="sxs-lookup"><span data-stu-id="230ea-107">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="230ea-108">Après avoir créé un flux à l’aide d’une action Application Insights, le flux exécute automatiquement votre requête Application Insights Analytics.</span><span class="sxs-lookup"><span data-stu-id="230ea-108">After you create a flow by using an Application Insights action, the flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="230ea-109">Vous pouvez également ajouter des actions.</span><span class="sxs-lookup"><span data-stu-id="230ea-109">You can add additional actions as well.</span></span> <span data-ttu-id="230ea-110">Microsoft Flow met à votre disposition des centaines d’actions.</span><span class="sxs-lookup"><span data-stu-id="230ea-110">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="230ea-111">Par exemple, vous pouvez utiliser Microsoft Flow pour envoyer automatiquement une notification par courrier électronique ou créer un bogue dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="230ea-111">For example, you can use Microsoft Flow to automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="230ea-112">Vous pouvez également utiliser l’un des nombreux [modèles](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) disponibles pour le connecteur pour Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="230ea-112">You can also use one of the many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for the connector for Microsoft Flow.</span></span> <span data-ttu-id="230ea-113">Ces modèles accélèrent le processus de création d’un flux.</span><span class="sxs-lookup"><span data-stu-id="230ea-113">These templates speed up the process of creating a flow.</span></span> 

<!--The Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="230ea-114">Créer un flux pour Application Insights</span><span class="sxs-lookup"><span data-stu-id="230ea-114">Create a flow for Application Insights</span></span>

<span data-ttu-id="230ea-115">Dans ce didacticiel, vous allez apprendre à créer un flux qui utilise l’algorithme de clusters automatiques Analytics aux attributs de groupe dans les données pour une application web.</span><span class="sxs-lookup"><span data-stu-id="230ea-115">In this tutorial, you will learn how to create a flow that uses the Analytics auto-cluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="230ea-116">Ce flux envoie automatiquement les résultats par courrier électronique. Il s’agit d’un exemple de la façon dont vous pouvez utiliser Microsoft Flow et Application Insights Analytics ensemble.</span><span class="sxs-lookup"><span data-stu-id="230ea-116">The flow automatically sends the results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="230ea-117">Étape 1 : Créer un flux</span><span class="sxs-lookup"><span data-stu-id="230ea-117">Step 1: Create a flow</span></span>
1. <span data-ttu-id="230ea-118">Connectez-vous à [Microsoft Flow](http://flow.microsoft.com), puis sélectionnez **Mes flux**.</span><span class="sxs-lookup"><span data-stu-id="230ea-118">Sign in to [Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="230ea-119">Cliquez sur **Créer un flux à partir de rien**.</span><span class="sxs-lookup"><span data-stu-id="230ea-119">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="230ea-120">Étape 2 : Créer un déclencheur pour votre flux</span><span class="sxs-lookup"><span data-stu-id="230ea-120">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="230ea-121">Sélectionnez **Planifier**, puis **Planification - Récurrence**.</span><span class="sxs-lookup"><span data-stu-id="230ea-121">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="230ea-122">Dans la zone **Fréquence**, sélectionnez **Jour** et, dans la zone **Intervalle**, entrez **1**.</span><span class="sxs-lookup"><span data-stu-id="230ea-122">In the **Frequency** box, select **Day**, and in the **Interval** box, enter **1**.</span></span>

    ![Boîte de dialogue du déclencheur de flux Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="230ea-124">Étape 3 : Ajouter une action Application Insights</span><span class="sxs-lookup"><span data-stu-id="230ea-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="230ea-125">Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="230ea-125">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="230ea-126">Recherchez **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="230ea-126">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="230ea-127">Cliquez sur **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights – Visualiser la requête Analytics Préversion).</span><span class="sxs-lookup"><span data-stu-id="230ea-127">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Fenêtre d’exécution de la requête Analytics](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="230ea-129">Étape 4 : Se connecter à une ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="230ea-129">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="230ea-130">Pour cette étape, vous avez besoin d’un ID d’application et d’une clé d’API pour votre ressource.</span><span class="sxs-lookup"><span data-stu-id="230ea-130">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="230ea-131">Vous pouvez les récupérer sur le portail Azure, comme illustré dans le schéma suivant :</span><span class="sxs-lookup"><span data-stu-id="230ea-131">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![ID d’application dans le portail Azure](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="230ea-133">Renseignez le nom de votre connexion, l’ID d’application et la clé d’API.</span><span class="sxs-lookup"><span data-stu-id="230ea-133">Provide a name for your connection, along with the application ID and API key.</span></span>

    ![Fenêtre de connexion Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="230ea-135">Étape 5 : Spécifier le type de requête et de graphique Analytics</span><span class="sxs-lookup"><span data-stu-id="230ea-135">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="230ea-136">Cet exemple de requête sélectionne les requêtes ayant échoué au cours du dernier jour et les met en corrélation avec les exceptions qui se sont produites dans le cadre de l’opération.</span><span class="sxs-lookup"><span data-stu-id="230ea-136">This example query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="230ea-137">Analytics les met en corrélation en fonction de l’identificateur operation_Id.</span><span class="sxs-lookup"><span data-stu-id="230ea-137">Analytics correlates them based on the operation_Id identifier.</span></span> <span data-ttu-id="230ea-138">La requête segmente ensuite les résultats à l’aide de l’algorithme de cluster automatique.</span><span class="sxs-lookup"><span data-stu-id="230ea-138">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="230ea-139">Lorsque vous créez vos propres requêtes, vérifiez qu’elles fonctionnent correctement dans Analytics avant de les ajouter à votre flux.</span><span class="sxs-lookup"><span data-stu-id="230ea-139">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

- <span data-ttu-id="230ea-140">Ajoutez la requête Analytics suivante, puis sélectionnez le type de graphique de tableau HTML.</span><span class="sxs-lookup"><span data-stu-id="230ea-140">Add the following Analytics query, and then select the HTML table chart type.</span></span> 

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

### <a name="step-6-configure-the-flow-to-send-email"></a><span data-ttu-id="230ea-142">Étape 6 : Configurer le flux pour envoyer un courrier électronique</span><span class="sxs-lookup"><span data-stu-id="230ea-142">Step 6: Configure the flow to send email</span></span>

1. <span data-ttu-id="230ea-143">Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="230ea-143">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="230ea-144">Recherchez **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="230ea-144">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="230ea-145">Cliquez sur **Office 365 Outlook – Envoyer un message électronique**.</span><span class="sxs-lookup"><span data-stu-id="230ea-145">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Fenêtre de sélection d’Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="230ea-147">Dans la fenêtre **Envoyer un message électronique**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="230ea-147">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="230ea-148">a.</span><span class="sxs-lookup"><span data-stu-id="230ea-148">a.</span></span> <span data-ttu-id="230ea-149">Tapez l’adresse e-mail du destinataire.</span><span class="sxs-lookup"><span data-stu-id="230ea-149">Type the email address of the recipient.</span></span>

   <span data-ttu-id="230ea-150">b.</span><span class="sxs-lookup"><span data-stu-id="230ea-150">b.</span></span> <span data-ttu-id="230ea-151">Tapez l’objet de l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="230ea-151">Type a subject for the email.</span></span>

   <span data-ttu-id="230ea-152">c.</span><span class="sxs-lookup"><span data-stu-id="230ea-152">c.</span></span> <span data-ttu-id="230ea-153">Cliquez n’importe où dans la zone **Corps**, puis, dans le menu de contenu dynamique qui s’ouvre sur la droite, sélectionnez **Corps**.</span><span class="sxs-lookup"><span data-stu-id="230ea-153">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="230ea-154">d.</span><span class="sxs-lookup"><span data-stu-id="230ea-154">d.</span></span> <span data-ttu-id="230ea-155">Cliquez sur **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="230ea-155">Click **Show advanced options**.</span></span>

    ![Configuration d’Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="230ea-157">Dans le menu de contenu dynamique, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="230ea-157">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="230ea-158">a.</span><span class="sxs-lookup"><span data-stu-id="230ea-158">a.</span></span> <span data-ttu-id="230ea-159">Sélectionnez **Nom de la pièce jointe**.</span><span class="sxs-lookup"><span data-stu-id="230ea-159">Select **Attachment Name**.</span></span>

    <span data-ttu-id="230ea-160">b.</span><span class="sxs-lookup"><span data-stu-id="230ea-160">b.</span></span> <span data-ttu-id="230ea-161">Sélectionnez **Attachment Content** (Contenu de la pièce jointe).</span><span class="sxs-lookup"><span data-stu-id="230ea-161">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="230ea-162">c.</span><span class="sxs-lookup"><span data-stu-id="230ea-162">c.</span></span> <span data-ttu-id="230ea-163">Dans la zone **Is HTML** (Est HTML), sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="230ea-163">In the **Is HTML** box, select **Yes**.</span></span>

    ![Fenêtre de configuration d’e-mail Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="230ea-165">Étape 7 : Enregistrer et tester votre flux</span><span class="sxs-lookup"><span data-stu-id="230ea-165">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="230ea-166">Dans la zone **Nom du flux**, ajoutez un nom pour votre flux, puis cliquez sur **Créer un flux**.</span><span class="sxs-lookup"><span data-stu-id="230ea-166">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Fenêtre de création de flux](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="230ea-168">Vous pouvez attendre que le déclencheur exécute cette action ou vous pouvez exécuter immédiatement le flux en [exécutant le déclencheur à la demande](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="230ea-168">You can wait for the trigger to run this action, or you can run the flow immediately by [running the trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="230ea-169">Lorsque le flux s’exécute, les destinataires que vous avez spécifiés dans la liste des e-mails reçoivent un e-mail similaire à :</span><span class="sxs-lookup"><span data-stu-id="230ea-169">When the flow runs, the recipients you have specified in the email list receive an email message that looks like the following:</span></span>

![Exemple de message électronique](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="230ea-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="230ea-171">Next steps</span></span>

- <span data-ttu-id="230ea-172">Découvrez la création de [requêtes Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="230ea-172">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="230ea-173">Découvrez [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="230ea-173">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





