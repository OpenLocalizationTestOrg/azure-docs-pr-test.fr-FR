---
title: "Créer une fonction dans Azure déclenchée par un webhook générique | Microsoft Docs"
description: "Utilisez Azure Functions pour créer une fonction sans serveur qui est appelée par un webhook dans Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/12/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: f283f8d79c5ae5fb6a72c84c9e9edb7bb8de4a83
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a><span data-ttu-id="71fe7-103">Créer une fonction déclenchée par un webhook générique</span><span class="sxs-lookup"><span data-stu-id="71fe7-103">Create a function triggered by a generic webhook</span></span>

<span data-ttu-id="71fe7-104">Azure Functions vous permet d’exécuter votre code dans un environnement sans serveur et sans avoir à créer une machine virtuelle ou à publier une application web au préalable.</span><span class="sxs-lookup"><span data-stu-id="71fe7-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="71fe7-105">Par exemple, vous pouvez configurer qu’une fonction soit déclenchée par une alerte provenant d’Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="71fe7-105">For example, you can configure a function to be triggered by an alert raised by Azure Monitor.</span></span> <span data-ttu-id="71fe7-106">Cette rubrique montre comment exécuter le code C# lorsqu’un groupe de ressources est ajouté à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="71fe7-106">This topic shows you how to execute C# code when a resource group is added to your subscription.</span></span>   

![Fonction déclenchée par un webhook générique dans le portail Azure](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a><span data-ttu-id="71fe7-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="71fe7-108">Prerequisites</span></span> 

<span data-ttu-id="71fe7-109">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="71fe7-109">To complete this tutorial:</span></span>

+ <span data-ttu-id="71fe7-110">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="71fe7-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="71fe7-111">Création d’une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="71fe7-111">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="71fe7-112">Créez ensuite une fonction dans la nouvelle Function App.</span><span class="sxs-lookup"><span data-stu-id="71fe7-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="71fe7-113"><a name="create-function"></a>Créer une fonction déclenchée par un webhook générique</span><span class="sxs-lookup"><span data-stu-id="71fe7-113"><a name="create-function"></a>Create a generic webhook triggered function</span></span>

1. <span data-ttu-id="71fe7-114">Développez votre Function App, puis cliquez sur le bouton **+** en regard de **Fonctions**.</span><span class="sxs-lookup"><span data-stu-id="71fe7-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="71fe7-115">Si cette fonction est la première de votre application de fonction, sélectionnez **Fonction personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="71fe7-115">If this function is the first one in your function app, select **Custom function**.</span></span> <span data-ttu-id="71fe7-116">Cela affiche l’ensemble complet des modèles de fonction.</span><span class="sxs-lookup"><span data-stu-id="71fe7-116">This displays the complete set of function templates.</span></span>

    ![Page de démarrage rapide des fonctions sur le portail Azure](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="71fe7-118">Sélectionnez le modèle **Webhook générique - C#**.</span><span class="sxs-lookup"><span data-stu-id="71fe7-118">Select the **Generic WebHook - C#** template.</span></span> <span data-ttu-id="71fe7-119">Donnez un nom à votre fonction C#, puis sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="71fe7-119">Type a name for your C# function, then select **Create**.</span></span>

     ![Créer une fonction déclenchée par un webhook générique dans le portail Azure](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. <span data-ttu-id="71fe7-121">Dans votre nouvelle fonction, cliquez sur **</> Obtenir l’URL de fonction**, puis copiez et enregistrez la valeur.</span><span class="sxs-lookup"><span data-stu-id="71fe7-121">In your new function, click **</> Get function URL**, then copy and save the value.</span></span> <span data-ttu-id="71fe7-122">Vous utilisez cette valeur pour configurer le webhook.</span><span class="sxs-lookup"><span data-stu-id="71fe7-122">You use this value to configure the webhook.</span></span> 

    ![Examiner le code de fonction](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
<span data-ttu-id="71fe7-124">Créez ensuite un point de terminaison webhook dans une alerte de journal d’activité dans Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="71fe7-124">Next, you create a webhook endpoint in an activity log alert in Azure Monitor.</span></span> 

## <a name="create-an-activity-log-alert"></a><span data-ttu-id="71fe7-125">Créer une alerte de journal d’activité</span><span class="sxs-lookup"><span data-stu-id="71fe7-125">Create an activity log alert</span></span>

1. <span data-ttu-id="71fe7-126">Dans le portail Azure, accédez au service **Surveillance**, sélectionnez **Alertes**, puis cliquez sur **Ajouter une alerte de journal d’activité**.</span><span class="sxs-lookup"><span data-stu-id="71fe7-126">In the Azure portal, navigate to the **Monitor** service, select **Alerts**, and click **Add activity log alert**.</span></span>   

    ![Surveiller](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. <span data-ttu-id="71fe7-128">Utilisez les paramètres spécifiés dans le tableau :</span><span class="sxs-lookup"><span data-stu-id="71fe7-128">Use the settings as specified in the table:</span></span>

    ![Créer une alerte de journal d’activité](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | <span data-ttu-id="71fe7-130">Paramètre</span><span class="sxs-lookup"><span data-stu-id="71fe7-130">Setting</span></span>      |  <span data-ttu-id="71fe7-131">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="71fe7-131">Suggested value</span></span>   | <span data-ttu-id="71fe7-132">Description</span><span class="sxs-lookup"><span data-stu-id="71fe7-132">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="71fe7-133">**Nom de l’alerte de journal d’activité**</span><span class="sxs-lookup"><span data-stu-id="71fe7-133">**Activity log alert name**</span></span> | <span data-ttu-id="71fe7-134">resource-group-create-alert</span><span class="sxs-lookup"><span data-stu-id="71fe7-134">resource-group-create-alert</span></span> | <span data-ttu-id="71fe7-135">Nom de l’alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="71fe7-135">Name of the activity log alert.</span></span> |
    | <span data-ttu-id="71fe7-136">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="71fe7-136">**Subscription**</span></span> | <span data-ttu-id="71fe7-137">Votre abonnement</span><span class="sxs-lookup"><span data-stu-id="71fe7-137">Your subscription</span></span> | <span data-ttu-id="71fe7-138">L’abonnement que vous utilisez pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="71fe7-138">The subscription you are using for this tutorial.</span></span> | 
    |  <span data-ttu-id="71fe7-139">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="71fe7-139">**Resource Group**</span></span> | <span data-ttu-id="71fe7-140">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="71fe7-140">myResourceGroup</span></span> | <span data-ttu-id="71fe7-141">Le groupe de ressources dans lequel les ressources d’alerte sont déployées.</span><span class="sxs-lookup"><span data-stu-id="71fe7-141">The resource group that the alert resources are deployed to.</span></span> <span data-ttu-id="71fe7-142">L’utilisation du même groupe de ressources que votre application de fonction facilite le nettoyage une fois le didacticiel terminé.</span><span class="sxs-lookup"><span data-stu-id="71fe7-142">Using the same resource group as your function app makes it easier to clean up after you complete the tutorial.</span></span> |
    | <span data-ttu-id="71fe7-143">**Catégorie d’événement**</span><span class="sxs-lookup"><span data-stu-id="71fe7-143">**Event category**</span></span> | <span data-ttu-id="71fe7-144">Administratif</span><span class="sxs-lookup"><span data-stu-id="71fe7-144">Administrative</span></span> | <span data-ttu-id="71fe7-145">Cette catégorie inclut les modifications apportées aux ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="71fe7-145">This category includes changes made to Azure resources.</span></span>  |
    | <span data-ttu-id="71fe7-146">**Type de ressource**</span><span class="sxs-lookup"><span data-stu-id="71fe7-146">**Resource type**</span></span> | <span data-ttu-id="71fe7-147">Groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="71fe7-147">Resource groups</span></span> | <span data-ttu-id="71fe7-148">Filtre les alertes pour les activités du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="71fe7-148">Filters alerts to resource group activities.</span></span> |
    | <span data-ttu-id="71fe7-149">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="71fe7-149">**Resource Group**</span></span><br/><span data-ttu-id="71fe7-150">et **Ressource**</span><span class="sxs-lookup"><span data-stu-id="71fe7-150">and **Resource**</span></span> | <span data-ttu-id="71fe7-151">Tout</span><span class="sxs-lookup"><span data-stu-id="71fe7-151">All</span></span> | <span data-ttu-id="71fe7-152">Surveille toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="71fe7-152">Monitor all resources.</span></span> |
    | <span data-ttu-id="71fe7-153">**Nom d’opération**</span><span class="sxs-lookup"><span data-stu-id="71fe7-153">**Operation name**</span></span> | <span data-ttu-id="71fe7-154">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="71fe7-154">Create Resource Group</span></span> | <span data-ttu-id="71fe7-155">Filtre les alertes pour créer des opérations.</span><span class="sxs-lookup"><span data-stu-id="71fe7-155">Filters alerts to create operations.</span></span> |
    | <span data-ttu-id="71fe7-156">**Niveau**</span><span class="sxs-lookup"><span data-stu-id="71fe7-156">**Level**</span></span> | <span data-ttu-id="71fe7-157">Informations</span><span class="sxs-lookup"><span data-stu-id="71fe7-157">Informational</span></span> | <span data-ttu-id="71fe7-158">Incluez les alertes de niveau d’informations.</span><span class="sxs-lookup"><span data-stu-id="71fe7-158">Include informational level alerts.</span></span> | 
    | <span data-ttu-id="71fe7-159">**État**</span><span class="sxs-lookup"><span data-stu-id="71fe7-159">**Status**</span></span> | <span data-ttu-id="71fe7-160">Réussi</span><span class="sxs-lookup"><span data-stu-id="71fe7-160">Succeeded</span></span> | <span data-ttu-id="71fe7-161">Filtre les alertes aux actions qui ont réussi.</span><span class="sxs-lookup"><span data-stu-id="71fe7-161">Filters alerts to actions that have completed successfully.</span></span> |
    | <span data-ttu-id="71fe7-162">**Groupe d’actions**</span><span class="sxs-lookup"><span data-stu-id="71fe7-162">**Action group**</span></span> | <span data-ttu-id="71fe7-163">Nouveau</span><span class="sxs-lookup"><span data-stu-id="71fe7-163">New</span></span> | <span data-ttu-id="71fe7-164">Créez un nouveau groupe d’actions, qui définit l’action effectuée lorsqu’une alerte est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="71fe7-164">Create a new action group, which defines the action takes when an alert is raised.</span></span> |
    | <span data-ttu-id="71fe7-165">**Nom du groupe d’actions**</span><span class="sxs-lookup"><span data-stu-id="71fe7-165">**Action group name**</span></span> | <span data-ttu-id="71fe7-166">function-webhook</span><span class="sxs-lookup"><span data-stu-id="71fe7-166">function-webhook</span></span> | <span data-ttu-id="71fe7-167">Nom destiné à identifier le groupe d’actions.</span><span class="sxs-lookup"><span data-stu-id="71fe7-167">A name to identify the action group.</span></span>  | 
    | <span data-ttu-id="71fe7-168">**Nom court**</span><span class="sxs-lookup"><span data-stu-id="71fe7-168">**Short name**</span></span> | <span data-ttu-id="71fe7-169">funcwebhook</span><span class="sxs-lookup"><span data-stu-id="71fe7-169">funcwebhook</span></span> | <span data-ttu-id="71fe7-170">Nom court du groupe d’actions.</span><span class="sxs-lookup"><span data-stu-id="71fe7-170">A short name for the action group.</span></span> |  

3. <span data-ttu-id="71fe7-171">Dans **Actions**, ajoutez une action à l’aide des paramètres spécifiés dans la table :</span><span class="sxs-lookup"><span data-stu-id="71fe7-171">In **Actions**, add an action using the settings as specified in the table:</span></span> 

    ![Ajouter un groupe d’actions](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | <span data-ttu-id="71fe7-173">Paramètre</span><span class="sxs-lookup"><span data-stu-id="71fe7-173">Setting</span></span>      |  <span data-ttu-id="71fe7-174">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="71fe7-174">Suggested value</span></span>   | <span data-ttu-id="71fe7-175">Description</span><span class="sxs-lookup"><span data-stu-id="71fe7-175">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="71fe7-176">**Name**</span><span class="sxs-lookup"><span data-stu-id="71fe7-176">**Name**</span></span> | <span data-ttu-id="71fe7-177">CallFunctionWebhook</span><span class="sxs-lookup"><span data-stu-id="71fe7-177">CallFunctionWebhook</span></span> | <span data-ttu-id="71fe7-178">Nom de l’action.</span><span class="sxs-lookup"><span data-stu-id="71fe7-178">A name for the action.</span></span> |
    | <span data-ttu-id="71fe7-179">**Type d’action**</span><span class="sxs-lookup"><span data-stu-id="71fe7-179">**Action type**</span></span> | <span data-ttu-id="71fe7-180">webhook</span><span class="sxs-lookup"><span data-stu-id="71fe7-180">Webhook</span></span> | <span data-ttu-id="71fe7-181">La réponse à l’alerte est qu’une URL de webhook est appelée.</span><span class="sxs-lookup"><span data-stu-id="71fe7-181">The response to the alert is that a Webhook URL is called.</span></span> |
    | <span data-ttu-id="71fe7-182">**Détails**</span><span class="sxs-lookup"><span data-stu-id="71fe7-182">**Details**</span></span> | <span data-ttu-id="71fe7-183">URL de la fonction</span><span class="sxs-lookup"><span data-stu-id="71fe7-183">Function URL</span></span> | <span data-ttu-id="71fe7-184">Collez l’URL de webhook de la fonction que vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="71fe7-184">Paste in the webhook URL of the function that you copied earlier.</span></span> |<span data-ttu-id="71fe7-185">v</span><span class="sxs-lookup"><span data-stu-id="71fe7-185">v</span></span>

4. <span data-ttu-id="71fe7-186">Cliquez sur **OK** pour créer l’alerte et le groupe d’actions.</span><span class="sxs-lookup"><span data-stu-id="71fe7-186">Click **OK** to create the alert and action group.</span></span>  

<span data-ttu-id="71fe7-187">Le webhook est maintenant appelé lorsqu’un groupe de ressources est créé dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="71fe7-187">The webhook is now called when a resource group is created in your subscription.</span></span> <span data-ttu-id="71fe7-188">Ensuite, vous mettez à jour le code dans votre fonction pour gérer les données de journal JSON dans le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="71fe7-188">Next, you update the code in your function to handle the JSON log data in the body of the request.</span></span>   

## <a name="update-the-function-code"></a><span data-ttu-id="71fe7-189">Mettre à jour le code de fonction</span><span class="sxs-lookup"><span data-stu-id="71fe7-189">Update the function code</span></span>

1. <span data-ttu-id="71fe7-190">Revenez à votre application de fonction sur le portail et développez votre fonction.</span><span class="sxs-lookup"><span data-stu-id="71fe7-190">Navigate back to your function app in the portal, and expand your function.</span></span> 

2. <span data-ttu-id="71fe7-191">Remplacez le code de script C# dans la fonction sur le portail par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="71fe7-191">Replace the C# script code in the function in the portal with the following code:</span></span>

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get the activityLog object from the JSON in the message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if the resource in the activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about the created resource group to the streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

<span data-ttu-id="71fe7-192">Vous pouvez maintenant tester la fonction en créant un nouveau groupe de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="71fe7-192">Now you can test the function by creating a new resource group in your subscription.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="71fe7-193">Tester la fonction</span><span class="sxs-lookup"><span data-stu-id="71fe7-193">Test the function</span></span>

1. <span data-ttu-id="71fe7-194">Cliquez sur l’icône du groupe de ressources à gauche du portail Azure, sélectionnez **+ Ajouter**, saisissez un **Nom de groupe de ressources**, puis sélectionnez **Créer** pour créer un groupe de ressources vide.</span><span class="sxs-lookup"><span data-stu-id="71fe7-194">Click the resource group icon in the left of the Azure portal, select **+ Add**, type a **Resource group name**, and select **Create** to create an empty resource group.</span></span>
    
    ![Créez un groupe de ressources.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. <span data-ttu-id="71fe7-196">Revenez à votre fonction et développez la fenêtre **Journaux**.</span><span class="sxs-lookup"><span data-stu-id="71fe7-196">Go back to your function and expand the **Logs** window.</span></span> <span data-ttu-id="71fe7-197">Une fois le groupe de ressources créé, l’alerte de journal d’activité déclenche le webhook et la fonction est exécutée.</span><span class="sxs-lookup"><span data-stu-id="71fe7-197">After the resource group is created, the activity log alert triggers the webhook and the function executes.</span></span> <span data-ttu-id="71fe7-198">Le nom du nouveau groupe de ressources est écrit dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="71fe7-198">You see the name of the new resource group written to the logs.</span></span>  

    ![Ajoutez un paramètre d’application de test.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. <span data-ttu-id="71fe7-200">(Facultatif) Revenez en arrière et supprimez le groupe de ressources que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="71fe7-200">(Optional) Go back and delete the resource group that you created.</span></span> <span data-ttu-id="71fe7-201">Notez que cette activité ne déclenche pas la fonction.</span><span class="sxs-lookup"><span data-stu-id="71fe7-201">Note that this activity doesn't trigger the function.</span></span> <span data-ttu-id="71fe7-202">Ceci est dû au fait que les opérations de suppression sont filtrées par l’alerte.</span><span class="sxs-lookup"><span data-stu-id="71fe7-202">This is because delete operations are filtered out by the alert.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="71fe7-203">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="71fe7-203">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="71fe7-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71fe7-204">Next steps</span></span>

<span data-ttu-id="71fe7-205">Vous avez créé une fonction qui s’exécute lorsqu’une requête est reçue à partir d’un webhook générique.</span><span class="sxs-lookup"><span data-stu-id="71fe7-205">You have created a function that runs when a request is received from a generic webhook.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="71fe7-206">Pour en savoir plus sur les déclencheurs webhook, consultez la page [Liaisons HTTP et webhook d’Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="71fe7-206">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span> <span data-ttu-id="71fe7-207">Pour en savoir plus sur le développement de fonctions en C#, consultez [Informations de référence pour les développeurs de scripts C# Azure Functions](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="71fe7-207">To learn more about developing functions in C#, see [Azure Functions C# script developer reference](functions-reference-csharp.md).</span></span>

