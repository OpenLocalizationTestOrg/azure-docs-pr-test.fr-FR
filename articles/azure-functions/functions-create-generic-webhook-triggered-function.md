---
title: "aaaCreate une fonction dans Azure déclenchée par un webhook générique | Documents Microsoft"
description: "Utilisez les fonctions Azure toocreate une fonction sans serveur qui est appelée par un webhook dans Azure."
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
ms.openlocfilehash: 0a4868da91d216c8d20930ce7ec82eaa059c75ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a><span data-ttu-id="32850-103">Créer une fonction déclenchée par un webhook générique</span><span class="sxs-lookup"><span data-stu-id="32850-103">Create a function triggered by a generic webhook</span></span>

<span data-ttu-id="32850-104">Les fonctions Azure vous permet d’exécuter votre code dans un environnement sans serveur sans avoir toofirst créer une machine virtuelle ou publier une application web.</span><span class="sxs-lookup"><span data-stu-id="32850-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="32850-105">Par exemple, vous pouvez configurer un toobe fonction déclenchée par une alerte déclenchée par le moniteur de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="32850-105">For example, you can configure a function toobe triggered by an alert raised by Azure Monitor.</span></span> <span data-ttu-id="32850-106">Cette rubrique vous montre comment tooexecute code c# lorsqu’un groupe de ressources est ajouté tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="32850-106">This topic shows you how tooexecute C# code when a resource group is added tooyour subscription.</span></span>   

![Générique webhook a déclenché la fonction Bonjour portail Azure](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a><span data-ttu-id="32850-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="32850-108">Prerequisites</span></span> 

<span data-ttu-id="32850-109">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="32850-109">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="32850-110">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="32850-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="32850-111">Création d’une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="32850-111">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="32850-112">Ensuite, créez une fonction dans hello une nouvelle application de fonction.</span><span class="sxs-lookup"><span data-stu-id="32850-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="32850-113"><a name="create-function"></a>Créer une fonction déclenchée par un webhook générique</span><span class="sxs-lookup"><span data-stu-id="32850-113"><a name="create-function"></a>Create a generic webhook triggered function</span></span>

1. <span data-ttu-id="32850-114">Développez votre application de la fonction et cliquez sur hello  **+**  bouton ensuite trop**fonctions**.</span><span class="sxs-lookup"><span data-stu-id="32850-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="32850-115">Si cette fonction est hello dans votre application de la fonction, sélectionnez **fonction personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="32850-115">If this function is hello first one in your function app, select **Custom function**.</span></span> <span data-ttu-id="32850-116">Cela affiche le jeu complet de hello des modèles de fonction.</span><span class="sxs-lookup"><span data-stu-id="32850-116">This displays hello complete set of function templates.</span></span>

    ![Page de démarrage rapide de fonctions Bonjour portail Azure](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="32850-118">Sélectionnez hello **WebHook - générique c#** modèle.</span><span class="sxs-lookup"><span data-stu-id="32850-118">Select hello **Generic WebHook - C#** template.</span></span> <span data-ttu-id="32850-119">Donnez un nom à votre fonction C#, puis sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="32850-119">Type a name for your C# function, then select **Create**.</span></span>

     ![Créer une fonction générique webhook déclenchée Bonjour portail Azure](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. <span data-ttu-id="32850-121">Dans votre nouvelle fonction, cliquez sur **<> / Get fonction URL**, puis copiez et enregistrez la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="32850-121">In your new function, click **</> Get function URL**, then copy and save hello value.</span></span> <span data-ttu-id="32850-122">Vous utilisez ce webhook de hello tooconfigure valeur.</span><span class="sxs-lookup"><span data-stu-id="32850-122">You use this value tooconfigure hello webhook.</span></span> 

    ![Passez en revue le code de la fonction hello](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
<span data-ttu-id="32850-124">Créez ensuite un point de terminaison webhook dans une alerte de journal d’activité dans Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="32850-124">Next, you create a webhook endpoint in an activity log alert in Azure Monitor.</span></span> 

## <a name="create-an-activity-log-alert"></a><span data-ttu-id="32850-125">Créer une alerte de journal d’activité</span><span class="sxs-lookup"><span data-stu-id="32850-125">Create an activity log alert</span></span>

1. <span data-ttu-id="32850-126">Dans hello portail Azure, accédez toohello **moniteur** service, sélectionnez **alertes**, puis cliquez sur **ajouter une alerte journal activité**.</span><span class="sxs-lookup"><span data-stu-id="32850-126">In hello Azure portal, navigate toohello **Monitor** service, select **Alerts**, and click **Add activity log alert**.</span></span>   

    ![Surveiller](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. <span data-ttu-id="32850-128">Utiliser les paramètres de hello comme spécifié dans la table de hello :</span><span class="sxs-lookup"><span data-stu-id="32850-128">Use hello settings as specified in hello table:</span></span>

    ![Créer une alerte de journal d’activité](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | <span data-ttu-id="32850-130">Paramètre</span><span class="sxs-lookup"><span data-stu-id="32850-130">Setting</span></span>      |  <span data-ttu-id="32850-131">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="32850-131">Suggested value</span></span>   | <span data-ttu-id="32850-132">Description</span><span class="sxs-lookup"><span data-stu-id="32850-132">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="32850-133">**Nom de l’alerte de journal d’activité**</span><span class="sxs-lookup"><span data-stu-id="32850-133">**Activity log alert name**</span></span> | <span data-ttu-id="32850-134">resource-group-create-alert</span><span class="sxs-lookup"><span data-stu-id="32850-134">resource-group-create-alert</span></span> | <span data-ttu-id="32850-135">Nom de l’alerte de journal d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="32850-135">Name of hello activity log alert.</span></span> |
    | <span data-ttu-id="32850-136">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="32850-136">**Subscription**</span></span> | <span data-ttu-id="32850-137">Votre abonnement</span><span class="sxs-lookup"><span data-stu-id="32850-137">Your subscription</span></span> | <span data-ttu-id="32850-138">abonnement Hello que vous utilisez pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="32850-138">hello subscription you are using for this tutorial.</span></span> | 
    |  <span data-ttu-id="32850-139">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="32850-139">**Resource Group**</span></span> | <span data-ttu-id="32850-140">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="32850-140">myResourceGroup</span></span> | <span data-ttu-id="32850-141">groupe de ressources Hello déployés pour avertir les ressources hello.</span><span class="sxs-lookup"><span data-stu-id="32850-141">hello resource group that hello alert resources are deployed to.</span></span> <span data-ttu-id="32850-142">À l’aide de hello le même groupe de ressources comme votre application de la fonction rend plus facile tooclean après avoir terminé le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="32850-142">Using hello same resource group as your function app makes it easier tooclean up after you complete hello tutorial.</span></span> |
    | <span data-ttu-id="32850-143">**Catégorie d’événement**</span><span class="sxs-lookup"><span data-stu-id="32850-143">**Event category**</span></span> | <span data-ttu-id="32850-144">Administratif</span><span class="sxs-lookup"><span data-stu-id="32850-144">Administrative</span></span> | <span data-ttu-id="32850-145">Cette catégorie inclut les modifications apportées aux ressources de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="32850-145">This category includes changes made tooAzure resources.</span></span>  |
    | <span data-ttu-id="32850-146">**Type de ressource**</span><span class="sxs-lookup"><span data-stu-id="32850-146">**Resource type**</span></span> | <span data-ttu-id="32850-147">Groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="32850-147">Resource groups</span></span> | <span data-ttu-id="32850-148">Filtre les activités de groupe tooresource alertes.</span><span class="sxs-lookup"><span data-stu-id="32850-148">Filters alerts tooresource group activities.</span></span> |
    | <span data-ttu-id="32850-149">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="32850-149">**Resource Group**</span></span><br/><span data-ttu-id="32850-150">et **Ressource**</span><span class="sxs-lookup"><span data-stu-id="32850-150">and **Resource**</span></span> | <span data-ttu-id="32850-151">Tout</span><span class="sxs-lookup"><span data-stu-id="32850-151">All</span></span> | <span data-ttu-id="32850-152">Surveille toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="32850-152">Monitor all resources.</span></span> |
    | <span data-ttu-id="32850-153">**Nom d’opération**</span><span class="sxs-lookup"><span data-stu-id="32850-153">**Operation name**</span></span> | <span data-ttu-id="32850-154">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="32850-154">Create Resource Group</span></span> | <span data-ttu-id="32850-155">Filtre les opérations de toocreate d’alertes.</span><span class="sxs-lookup"><span data-stu-id="32850-155">Filters alerts toocreate operations.</span></span> |
    | <span data-ttu-id="32850-156">**Niveau**</span><span class="sxs-lookup"><span data-stu-id="32850-156">**Level**</span></span> | <span data-ttu-id="32850-157">Informations</span><span class="sxs-lookup"><span data-stu-id="32850-157">Informational</span></span> | <span data-ttu-id="32850-158">Incluez les alertes de niveau d’informations.</span><span class="sxs-lookup"><span data-stu-id="32850-158">Include informational level alerts.</span></span> | 
    | <span data-ttu-id="32850-159">**État**</span><span class="sxs-lookup"><span data-stu-id="32850-159">**Status**</span></span> | <span data-ttu-id="32850-160">Réussi</span><span class="sxs-lookup"><span data-stu-id="32850-160">Succeeded</span></span> | <span data-ttu-id="32850-161">Filtres tooactions alertes qui ont été effectuées avec succès.</span><span class="sxs-lookup"><span data-stu-id="32850-161">Filters alerts tooactions that have completed successfully.</span></span> |
    | <span data-ttu-id="32850-162">**Groupe d’actions**</span><span class="sxs-lookup"><span data-stu-id="32850-162">**Action group**</span></span> | <span data-ttu-id="32850-163">Nouveau</span><span class="sxs-lookup"><span data-stu-id="32850-163">New</span></span> | <span data-ttu-id="32850-164">Créer un nouveau groupe d’action, qui définit l’action hello se lorsqu’une alerte est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="32850-164">Create a new action group, which defines hello action takes when an alert is raised.</span></span> |
    | <span data-ttu-id="32850-165">**Nom du groupe d’actions**</span><span class="sxs-lookup"><span data-stu-id="32850-165">**Action group name**</span></span> | <span data-ttu-id="32850-166">function-webhook</span><span class="sxs-lookup"><span data-stu-id="32850-166">function-webhook</span></span> | <span data-ttu-id="32850-167">Un groupe d’actions nom tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="32850-167">A name tooidentify hello action group.</span></span>  | 
    | <span data-ttu-id="32850-168">**Nom court**</span><span class="sxs-lookup"><span data-stu-id="32850-168">**Short name**</span></span> | <span data-ttu-id="32850-169">funcwebhook</span><span class="sxs-lookup"><span data-stu-id="32850-169">funcwebhook</span></span> | <span data-ttu-id="32850-170">Un nom court pour le groupe d’actions hello.</span><span class="sxs-lookup"><span data-stu-id="32850-170">A short name for hello action group.</span></span> |  

3. <span data-ttu-id="32850-171">Dans **Actions**, ajoutez une action à l’aide des paramètres de hello comme spécifié dans la table de hello :</span><span class="sxs-lookup"><span data-stu-id="32850-171">In **Actions**, add an action using hello settings as specified in hello table:</span></span> 

    ![Ajouter un groupe d’actions](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | <span data-ttu-id="32850-173">Paramètre</span><span class="sxs-lookup"><span data-stu-id="32850-173">Setting</span></span>      |  <span data-ttu-id="32850-174">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="32850-174">Suggested value</span></span>   | <span data-ttu-id="32850-175">Description</span><span class="sxs-lookup"><span data-stu-id="32850-175">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="32850-176">**Name**</span><span class="sxs-lookup"><span data-stu-id="32850-176">**Name**</span></span> | <span data-ttu-id="32850-177">CallFunctionWebhook</span><span class="sxs-lookup"><span data-stu-id="32850-177">CallFunctionWebhook</span></span> | <span data-ttu-id="32850-178">Un nom pour l’action de hello.</span><span class="sxs-lookup"><span data-stu-id="32850-178">A name for hello action.</span></span> |
    | <span data-ttu-id="32850-179">**Type d’action**</span><span class="sxs-lookup"><span data-stu-id="32850-179">**Action type**</span></span> | <span data-ttu-id="32850-180">webhook</span><span class="sxs-lookup"><span data-stu-id="32850-180">Webhook</span></span> | <span data-ttu-id="32850-181">alerte de toohello Hello réponse est que l’URL du Webhook est appelée.</span><span class="sxs-lookup"><span data-stu-id="32850-181">hello response toohello alert is that a Webhook URL is called.</span></span> |
    | <span data-ttu-id="32850-182">**Détails**</span><span class="sxs-lookup"><span data-stu-id="32850-182">**Details**</span></span> | <span data-ttu-id="32850-183">URL de la fonction</span><span class="sxs-lookup"><span data-stu-id="32850-183">Function URL</span></span> | <span data-ttu-id="32850-184">Collez l’URL du webhook hello de fonction hello que vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="32850-184">Paste in hello webhook URL of hello function that you copied earlier.</span></span> |<span data-ttu-id="32850-185">v</span><span class="sxs-lookup"><span data-stu-id="32850-185">v</span></span>

4. <span data-ttu-id="32850-186">Cliquez sur **OK** toocreate hello alerte et action le groupe.</span><span class="sxs-lookup"><span data-stu-id="32850-186">Click **OK** toocreate hello alert and action group.</span></span>  

<span data-ttu-id="32850-187">Hello webhook est maintenant appelé lorsqu’un groupe de ressources est créé dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="32850-187">hello webhook is now called when a resource group is created in your subscription.</span></span> <span data-ttu-id="32850-188">Ensuite, vous mettre à jour hello code dans votre hello toohandle de fonction JSON journal données hello corps de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="32850-188">Next, you update hello code in your function toohandle hello JSON log data in hello body of hello request.</span></span>   

## <a name="update-hello-function-code"></a><span data-ttu-id="32850-189">Mettre à jour le code de la fonction hello</span><span class="sxs-lookup"><span data-stu-id="32850-189">Update hello function code</span></span>

1. <span data-ttu-id="32850-190">Accédez d’application de fonction tooyour précédent dans le portail de hello et développez votre fonction.</span><span class="sxs-lookup"><span data-stu-id="32850-190">Navigate back tooyour function app in hello portal, and expand your function.</span></span> 

2. <span data-ttu-id="32850-191">Remplacez le code de script hello c# dans la fonction hello dans le portail de hello hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="32850-191">Replace hello C# script code in hello function in hello portal with hello following code:</span></span>

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get hello activityLog object from hello JSON in hello message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if hello resource in hello activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about hello created resource group toohello streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

<span data-ttu-id="32850-192">Vous pouvez maintenant tester la fonction hello en créant un nouveau groupe de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="32850-192">Now you can test hello function by creating a new resource group in your subscription.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="32850-193">Fonction hello de test</span><span class="sxs-lookup"><span data-stu-id="32850-193">Test hello function</span></span>

1. <span data-ttu-id="32850-194">Cliquez sur icône de groupe de ressources hello en hello portail Azure, sélectionnez à gauche hello **+ ajouter**, tapez un **nom de groupe de ressources**, puis sélectionnez **créer** toocreate un groupe de ressources vide.</span><span class="sxs-lookup"><span data-stu-id="32850-194">Click hello resource group icon in hello left of hello Azure portal, select **+ Add**, type a **Resource group name**, and select **Create** toocreate an empty resource group.</span></span>
    
    ![Créez un groupe de ressources.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. <span data-ttu-id="32850-196">Revenir en arrière tooyour fonction et développez hello **journaux** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="32850-196">Go back tooyour function and expand hello **Logs** window.</span></span> <span data-ttu-id="32850-197">Après la création de groupe de ressources hello, webhook hello hello alerte déclencheurs de journal d’activité et hello fonction s’exécute.</span><span class="sxs-lookup"><span data-stu-id="32850-197">After hello resource group is created, hello activity log alert triggers hello webhook and hello function executes.</span></span> <span data-ttu-id="32850-198">Vous voyez le nom hello du nouveau groupe de ressources hello écrit des journaux de toohello.</span><span class="sxs-lookup"><span data-stu-id="32850-198">You see hello name of hello new resource group written toohello logs.</span></span>  

    ![Ajoutez un paramètre d’application de test.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. <span data-ttu-id="32850-200">(Facultatif) Revenir en arrière et supprimer le groupe de ressources hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="32850-200">(Optional) Go back and delete hello resource group that you created.</span></span> <span data-ttu-id="32850-201">Notez que cette activité ne déclenche pas fonction hello.</span><span class="sxs-lookup"><span data-stu-id="32850-201">Note that this activity doesn't trigger hello function.</span></span> <span data-ttu-id="32850-202">C’est parce que delete opérations sont filtrées par l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="32850-202">This is because delete operations are filtered out by hello alert.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="32850-203">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="32850-203">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="32850-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="32850-204">Next steps</span></span>

<span data-ttu-id="32850-205">Vous avez créé une fonction qui s’exécute lorsqu’une requête est reçue à partir d’un webhook générique.</span><span class="sxs-lookup"><span data-stu-id="32850-205">You have created a function that runs when a request is received from a generic webhook.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="32850-206">Pour en savoir plus sur les déclencheurs webhook, consultez la page [Liaisons HTTP et webhook d’Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="32850-206">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span> <span data-ttu-id="32850-207">toolearn plus sur le développement de fonctions en langage c#, consultez [référence du développeur Azure fonctions C# script](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="32850-207">toolearn more about developing functions in C#, see [Azure Functions C# script developer reference](functions-reference-csharp.md).</span></span>

