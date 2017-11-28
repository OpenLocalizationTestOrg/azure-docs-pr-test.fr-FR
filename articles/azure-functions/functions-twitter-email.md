---
title: "aaaCreate une fonction qui s’intègre à Azure Logic Apps | Documents Microsoft"
description: "Créez une fonction qui s’intègre à Azure Logic Apps et Services cognitifs Azure sentiment de tweet toocategorize et envoyer des notifications lorsque l’opinion est faible."
services: functions, logic-apps, cognitive-services
keywords: "flux de travail, applications cloud, services cloud, processus d’entreprise, intégration de systèmes, intégration d’applications d’entreprise, IAE"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="2d5b3-104">Créer une fonction qui s’intègre avec Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2d5b3-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="2d5b3-105">Les fonctions Azure s’intègre avec Azure Logic Apps Bonjour logique de concepteur d’applications.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-105">Azure Functions integrates with Azure Logic Apps in hello Logic Apps Designer.</span></span> <span data-ttu-id="2d5b3-106">Cette intégration vous permet d’utiliser hello puissance de calcul fonctions dans les orchestrations avec d’autres services Azure et des services tiers.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-106">This integration lets you use hello computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="2d5b3-107">Ce didacticiel vous montre comment toouse fonctionne avec la logique d’applications et Services cognitifs Azure sentiment tooanalyze de billets de Twitter.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-107">This tutorial shows you how toouse Functions with Logic Apps and Azure Cognitive Services tooanalyze sentiment from Twitter posts.</span></span> <span data-ttu-id="2d5b3-108">Une fonction HTTP déclenchée classe tweet en vert, jaune ou rouge en fonction de score d’opinion hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on hello sentiment score.</span></span> <span data-ttu-id="2d5b3-109">Un courrier électronique est envoyé lors de la détection de sentiments négatifs.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-109">An email is sent when poor sentiment is detected.</span></span> 

![Image : deux premières étapes de l’application dans le Concepteur d’applications logiques](media/functions-twitter-email/designer1.png)

<span data-ttu-id="2d5b3-111">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2d5b3-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2d5b3-112">Créez un compte Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="2d5b3-113">Créer une fonction qui classe le sentiment des tweets.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="2d5b3-114">Créer une application de la logique qui se connecte tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-114">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="2d5b3-115">Ajouter une application de sentiment détection toohello logique.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-115">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="2d5b3-116">Se connecter (fonction) toohello application hello logique.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-116">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="2d5b3-117">Envoyer un courrier électronique en fonction de la réponse hello à partir de la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-117">Send an email based on hello response from hello function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d5b3-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2d5b3-118">Prerequisites</span></span>

+ <span data-ttu-id="2d5b3-119">Un compte [Twitter](https://twitter.com/) actif.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="2d5b3-120">Un compte [Outlook.com](https://outlook.com/) (pour l’envoi de notifications).</span><span class="sxs-lookup"><span data-stu-id="2d5b3-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="2d5b3-121">Cette rubrique utilise en tant que ses ressources de hello de point de départ créés dans [créer votre première fonction de hello Azure portal](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="2d5b3-121">This topic uses as its starting point hello resources created in [Create your first function from hello Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="2d5b3-122">Si vous n’avez pas déjà fait, effectuez ces toocreate de maintenant étapes votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-122">If you haven't already done so, complete these steps now toocreate your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="2d5b3-123">Créez un compte Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="2d5b3-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="2d5b3-124">Un compte de Services cognitifs est sentiment de hello toodetect obligatoire de tweets en cours d’analyse.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-124">A Cognitive Services account is required toodetect hello sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="2d5b3-125">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2d5b3-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="2d5b3-126">Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-126">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

3. <span data-ttu-id="2d5b3-127">Cliquez sur **Données + analyse** > **Cognitive Services**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="2d5b3-128">Ensuite, utiliser les paramètres de hello en tant que spécifié dans la table de hello, accepter les termes du contrat de hello et vérifiez **toodashboard du code confidentiel**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-128">Then, use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Panneau Créer un compte Cognitive](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="2d5b3-130">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2d5b3-130">Setting</span></span>      |  <span data-ttu-id="2d5b3-131">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="2d5b3-131">Suggested value</span></span>   | <span data-ttu-id="2d5b3-132">Description</span><span class="sxs-lookup"><span data-stu-id="2d5b3-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="2d5b3-133">**Nom**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-133">**Name**</span></span> | <span data-ttu-id="2d5b3-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="2d5b3-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="2d5b3-135">Choisissez un nom de compte unique.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="2d5b3-136">**Type d’API**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-136">**API type**</span></span> | <span data-ttu-id="2d5b3-137">API Analyse de texte</span><span class="sxs-lookup"><span data-stu-id="2d5b3-137">Text Analytics API</span></span> | <span data-ttu-id="2d5b3-138">API utilisée tooanalyze texte.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-138">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="2d5b3-139">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-139">**Location**</span></span> | <span data-ttu-id="2d5b3-140">Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="2d5b3-140">West US</span></span> | <span data-ttu-id="2d5b3-141">Actuellement, seule la région **États-Unis de l’Ouest** est disponible pour l’analyse de texte.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="2d5b3-142">**Niveau tarifaire**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-142">**Pricing tier**</span></span> | <span data-ttu-id="2d5b3-143">F0</span><span class="sxs-lookup"><span data-stu-id="2d5b3-143">F0</span></span> | <span data-ttu-id="2d5b3-144">Commencer par la couche la plus basse de hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-144">Start with hello lowest tier.</span></span> <span data-ttu-id="2d5b3-145">Si vous manquez d’appels, mettre à l’échelle de niveau supérieur de tooa.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-145">If you run out of calls, scale tooa higher tier.</span></span>|
    | <span data-ttu-id="2d5b3-146">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-146">**Resource group**</span></span> | <span data-ttu-id="2d5b3-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2d5b3-147">myResourceGroup</span></span> | <span data-ttu-id="2d5b3-148">Utilisez hello même groupe de ressources pour tous les services dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-148">Use hello same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="2d5b3-149">Cliquez sur **créer** toocreate votre compte.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-149">Click **Create** toocreate your account.</span></span> <span data-ttu-id="2d5b3-150">Une fois hello compte est créé, cliquez sur Nouveau Services cognitifs compte épinglé toohello tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-150">After hello account is created, click your new Cognitive Services account pinned toohello dashboard.</span></span> 

5. <span data-ttu-id="2d5b3-151">Dans hello compte, cliquez sur **clés**, puis copiez la valeur hello **clé 1** et l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-151">In hello account, click **Keys**, and then copy hello value of **Key 1** and save it.</span></span> <span data-ttu-id="2d5b3-152">Vous utilisez cette logique de clé tooconnect hello application tooyour compte Services cognitifs.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-152">You use this key tooconnect hello logic app tooyour Cognitive Services account.</span></span> 
 
    ![Clés](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a><span data-ttu-id="2d5b3-154">Créer la fonction hello</span><span class="sxs-lookup"><span data-stu-id="2d5b3-154">Create hello function</span></span>

<span data-ttu-id="2d5b3-155">Fonctions fournit un toooffload excellent moyen des tâches de traitement dans un flux de travail applications logique.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-155">Functions provides a great way toooffload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="2d5b3-156">Ce didacticiel utilise un HTTP déclenchée fonction tooprocess tweet sentiment les scores à partir des Services cognitifs et retournent une valeur de catégorie.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-156">This tutorial uses an HTTP triggered function tooprocess tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="2d5b3-157">Développez votre application de la fonction, cliquez sur hello  **+**  bouton ensuite trop**fonctions**, cliquez sur hello **HTTPTrigger** modèle.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-157">Expand your function app, click hello **+** button next too**Functions**, click hello **HTTPTrigger** template.</span></span> <span data-ttu-id="2d5b3-158">Type `CategorizeSentiment` pour la fonction hello **nom** et cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-158">Type `CategorizeSentiment` for hello function **Name** and click **Create**.</span></span>

    ![Panneau Function Apps, Fonctions +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="2d5b3-160">Remplacez contenu hello du fichier de run.csx hello hello suivant de code, puis cliquez sur **enregistrer**:</span><span class="sxs-lookup"><span data-stu-id="2d5b3-160">Replace hello contents of hello run.csx file with hello following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    <span data-ttu-id="2d5b3-161">Le code de cette fonction retourne une catégorie de couleur en fonction de score d’opinion hello reçu dans la demande hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-161">This function code returns a color category based on hello sentiment score received in hello request.</span></span> 

3. <span data-ttu-id="2d5b3-162">fonction de hello tootest, cliquez sur **Test** à onglet hello hello tooexpand plus à droite. Tapez la valeur `0.2` pour hello **corps de la demande**, puis cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-162">tootest hello function, click **Test** at hello far right tooexpand hello Test tab. Type a value of `0.2` for hello **Request body**, and then click **Run**.</span></span> <span data-ttu-id="2d5b3-163">La valeur **rouge** est retourné dans le corps de réponse de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-163">A value of **RED** is returned in hello body of hello response.</span></span> 

    ![Tester la fonction hello Bonjour portail Azure](./media/functions-twitter-email/test.png)

<span data-ttu-id="2d5b3-165">Vous disposez maintenant d’une fonction permettant de classer les scores des sentiments.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="2d5b3-166">Ensuite, créez une application logique qui intègre votre fonction avec vos comptes Twitter et Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="2d5b3-167">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="2d5b3-167">Create a logic app</span></span>   

1. <span data-ttu-id="2d5b3-168">Dans l’hello portail Azure, cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-168">In hello Azure portal, click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="2d5b3-169">Cliquez sur **Intégration d’entreprise** > **Application logique**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="2d5b3-170">Vérifiez ensuite utiliser les paramètres hello comme spécifié dans la table de hello, **code confidentiel toodashboard**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-170">Then, use hello settings as specified in hello table, check **Pin toodashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="2d5b3-171">Ensuite, tapez un **nom** comme `TweetSentiment`, utiliser des paramètres de hello comme spécifié dans la table de hello, acceptez les termes du contrat de hello et vérifier **toodashboard du code confidentiel**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-171">Then, type a **Name** like `TweetSentiment`,  use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Créer l’application logique Bonjour portail Azure](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="2d5b3-173">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2d5b3-173">Setting</span></span>      |  <span data-ttu-id="2d5b3-174">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="2d5b3-174">Suggested value</span></span>   | <span data-ttu-id="2d5b3-175">Description</span><span class="sxs-lookup"><span data-stu-id="2d5b3-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="2d5b3-176">**Nom**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-176">**Name**</span></span> | <span data-ttu-id="2d5b3-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="2d5b3-177">TweetSentiment</span></span> | <span data-ttu-id="2d5b3-178">Choisissez un nom approprié pour votre application.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="2d5b3-179">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-179">**Resource group**</span></span> | <span data-ttu-id="2d5b3-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2d5b3-180">myResourceGroup</span></span> | <span data-ttu-id="2d5b3-181">API utilisée tooanalyze texte.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-181">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="2d5b3-182">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-182">**Location**</span></span> | <span data-ttu-id="2d5b3-183">Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="2d5b3-183">East US</span></span> | <span data-ttu-id="2d5b3-184">Choisissez un tooyou fermer d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-184">Choose a location close tooyou.</span></span> |
    | <span data-ttu-id="2d5b3-185">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-185">**Resource group**</span></span> | <span data-ttu-id="2d5b3-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2d5b3-186">myResourceGroup</span></span> | <span data-ttu-id="2d5b3-187">Choisissez hello le même groupe de ressources existant comme avant.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-187">Choose hello same existing resource group as before.</span></span>|

4. <span data-ttu-id="2d5b3-188">Cliquez sur **créer** toocreate votre application logique.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-188">Click **Create** toocreate your logic app.</span></span> <span data-ttu-id="2d5b3-189">Une fois l’application hello est créée, cliquez sur votre nouveau tableau de bord toohello épinglée d’application logique.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-189">After hello app is created, click your new logic app pinned toohello dashboard.</span></span> <span data-ttu-id="2d5b3-190">Dans le Concepteur d’applications de logique de hello, faites défiler, puis cliquez sur hello **application logique vide** modèle.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-190">Then in hello Logic Apps Designer, scroll down and click hello **Blank Logic App** template.</span></span> 

    ![Modèle d’applications logiques vides](media/functions-twitter-email/blank.png)

<span data-ttu-id="2d5b3-192">Vous pouvez maintenant utiliser le Concepteur d’applications logique tooadd services et des déclencheurs tooyour application hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-192">You can now use hello Logic Apps Designer tooadd services and triggers tooyour app.</span></span>

## <a name="connect-tootwitter"></a><span data-ttu-id="2d5b3-193">Se connecter tooTwitter</span><span class="sxs-lookup"><span data-stu-id="2d5b3-193">Connect tooTwitter</span></span>

<span data-ttu-id="2d5b3-194">Commencez par créer une connexion de tooyour compte Twitter.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-194">First, create a connection tooyour Twitter account.</span></span> <span data-ttu-id="2d5b3-195">Hello logique application interroge tweets, lequel déclenchent hello application toorun.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-195">hello logic app polls for tweets, which trigger hello app toorun.</span></span>

1. <span data-ttu-id="2d5b3-196">Dans le Concepteur de hello, cliquez sur hello **Twitter** de service, puis cliquez sur hello **lors de la validation d’un tweet nouvelle** déclencheur.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-196">In hello designer, click hello **Twitter** service, and click hello **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="2d5b3-197">Connectez-vous à tooyour compte Twitter et autoriser Logic Apps toouse votre compte.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-197">Sign in tooyour Twitter account and authorize Logic Apps toouse your account.</span></span>

2. <span data-ttu-id="2d5b3-198">Utiliser les paramètres de déclencheur hello Twitter comme spécifié dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-198">Use hello Twitter trigger settings as specified in hello table.</span></span> 

    ![Paramètres du connecteur Twitter](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="2d5b3-200">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2d5b3-200">Setting</span></span>      |  <span data-ttu-id="2d5b3-201">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="2d5b3-201">Suggested value</span></span>   | <span data-ttu-id="2d5b3-202">Description</span><span class="sxs-lookup"><span data-stu-id="2d5b3-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="2d5b3-203">**Texte de recherche**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-203">**Search text**</span></span> | <span data-ttu-id="2d5b3-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="2d5b3-204">#Azure</span></span> | <span data-ttu-id="2d5b3-205">Utilisez un #sqlhelp qui est souvent assez utilisé pour toogenerate des tweets nouveau dans l’intervalle de salutation choisie.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-205">Use a hashtag that is popular enough for toogenerate new tweets in hello chosen interval.</span></span> <span data-ttu-id="2d5b3-206">Lorsque l’utilisation de niveau gratuit de hello et votre #sqlhelp est trop populaire, vous pouvez utiliser rapidement les transactions hello dans votre compte de Services cognitifs.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-206">When using hello Free tier and your hashtag is too popular, you can quickly use up hello transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="2d5b3-207">**Fréquence**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-207">**Frequency**</span></span> | <span data-ttu-id="2d5b3-208">Minute</span><span class="sxs-lookup"><span data-stu-id="2d5b3-208">Minute</span></span> | <span data-ttu-id="2d5b3-209">unité de fréquence Hello utilisée pour l’interrogation Twitter.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-209">hello frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="2d5b3-210">**Intervalle**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-210">**Interval**</span></span> | <span data-ttu-id="2d5b3-211">15</span><span class="sxs-lookup"><span data-stu-id="2d5b3-211">15</span></span> | <span data-ttu-id="2d5b3-212">Hello du délai entre les demandes de Twitter, en unités de fréquence.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-212">hello time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="2d5b3-213">Cliquez sur **enregistrer** tooconnect tooyour compte Twitter.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-213">Click **Save** tooconnect tooyour Twitter account.</span></span> 

<span data-ttu-id="2d5b3-214">Votre application est maintenant connecté tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-214">Now your app is connected tooTwitter.</span></span> <span data-ttu-id="2d5b3-215">Ensuite, vous vous connectez sentiment de hello toodetect tootext analytique de tweet collectées.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-215">Next, you connect tootext analytics toodetect hello sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="2d5b3-216">Ajouter la détection de sentiments</span><span class="sxs-lookup"><span data-stu-id="2d5b3-216">Add sentiment detection</span></span>

1. <span data-ttu-id="2d5b3-217">Cliquez sur **Nouvelle étape**, puis sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Nouvelle étape, puis Ajouter une action](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="2d5b3-219">Dans **choisir une action**, cliquez sur **texte Analytique**, puis cliquez sur hello **détecter sentiment** action.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-219">In **Choose an action**, click **Text Analytics**, and then click hello **Detect sentiment** action.</span></span>

    ![Detect Sentiment (Détecter le sentiment)](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="2d5b3-221">Tapez un nom de connexion comme `MyCognitiveServicesConnection`, collez la clé de hello pour vos Services cognitifs compte que vous avez enregistré, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-221">Type a connection name such as `MyCognitiveServicesConnection`, paste hello key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="2d5b3-222">Cliquez sur **texte tooanalyze** > **tweetez-texte**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-222">Click **Text tooanalyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Detect Sentiment (Détecter le sentiment)](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="2d5b3-224">Maintenant que la détection de sentiment est configurée, vous pouvez ajouter une fonction de tooyour de connexion qui consomme la sortie de score d’opinion hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-224">Now that sentiment detection is configured, you can add a connection tooyour function that consumes hello sentiment score output.</span></span>

## <a name="connect-sentiment-output-tooyour-function"></a><span data-ttu-id="2d5b3-225">Connecter la sortie sentiment tooyour (fonction)</span><span class="sxs-lookup"><span data-stu-id="2d5b3-225">Connect sentiment output tooyour function</span></span>

1. <span data-ttu-id="2d5b3-226">Bonjour logique de concepteur d’applications, cliquez sur **nouvelle étape** > **ajouter une action**, puis cliquez sur **Azure fonctions**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-226">In hello Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="2d5b3-227">Cliquez sur **choisissez une fonction d’Azure**, sélectionnez hello **CategorizeSentiment** fonction que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-227">Click **Choose an Azure function**, select hello **CategorizeSentiment** function you created earlier.</span></span>  

    ![Zone Azure Functions montrant Choisir une fonction Azure](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="2d5b3-229">Dans **Corps de la requête**, cliquez sur **Score**, puis sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Score](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="2d5b3-231">À présent, votre fonction est déclenchée lorsqu’un score d’opinion est envoyé à partir de l’application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-231">Now, your function is triggered when a sentiment score is sent from hello logic app.</span></span> <span data-ttu-id="2d5b3-232">Une catégorie de couleur est retournée toohello logique application par fonction hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-232">A color-coded category is returned toohello logic app by hello function.</span></span> <span data-ttu-id="2d5b3-233">Ensuite, vous ajoutez une notification par courrier électronique qui est envoyée lorsqu’une valeur d’indice de sentiment de **rouge** est retournée à partir de la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from hello function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="2d5b3-234">Ajouter des notifications par courrier électronique</span><span class="sxs-lookup"><span data-stu-id="2d5b3-234">Add email notifications</span></span>

<span data-ttu-id="2d5b3-235">Hello dernière partie du flux de travail hello est tootrigger un courrier électronique lors de l’opinion de hello est catégorisée en tant que _rouge_.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-235">hello last part of hello workflow is tootrigger an email when hello sentiment is scored as _RED_.</span></span> <span data-ttu-id="2d5b3-236">Cette rubrique utilise un connecteur Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="2d5b3-237">Vous pouvez effectuer toouse des étapes similaires un connecteur Gmail ou Outlook Office 365.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-237">You can perform similar steps toouse a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="2d5b3-238">Bonjour logique de concepteur d’applications, cliquez sur **nouvelle étape** > **ajouter une condition**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-238">In hello Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="2d5b3-239">Cliquez sur **Choisir une valeur**, puis cliquez sur **Corps**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="2d5b3-240">Sélectionnez **Est égal à**, cliquez sur **Choisir une valeur** et saisissez `RED`, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Ajouter une application de la logique de toohello de condition.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="2d5b3-242">Dans **si Oui, ne rien faire**, cliquez sur **ajouter une action**, recherchez `outlook.com`, cliquez sur **envoyer un courrier électronique**et vous connecter tooyour Outlook.com compte.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in tooyour Outlook.com account.</span></span>
    
    ![Choisissez une action de condition de hello.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="2d5b3-244">Si vous n’avez pas de compte Outlook.com, vous pouvez choisir un autre connecteur, comme Gmail ou Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="2d5b3-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="2d5b3-245">Bonjour **envoyer un courrier électronique** action, utiliser les paramètres de messagerie hello comme spécifié dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-245">In hello **Send an email** action, use hello email settings as specified in hello table.</span></span> 

    ![Configurer la messagerie de hello pour l’envoi de hello une action de courrier électronique.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="2d5b3-247">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2d5b3-247">Setting</span></span>      |  <span data-ttu-id="2d5b3-248">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="2d5b3-248">Suggested value</span></span>   | <span data-ttu-id="2d5b3-249">Description</span><span class="sxs-lookup"><span data-stu-id="2d5b3-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="2d5b3-250">**To**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-250">**To**</span></span> | <span data-ttu-id="2d5b3-251">Saisissez votre adresse de messagerie</span><span class="sxs-lookup"><span data-stu-id="2d5b3-251">Type your email address</span></span> | <span data-ttu-id="2d5b3-252">adresse de messagerie Hello qui reçoit la notification de hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-252">hello email address that receives hello notification.</span></span> |
    | <span data-ttu-id="2d5b3-253">**Objet**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-253">**Subject**</span></span> | <span data-ttu-id="2d5b3-254">Sentiment de tweet négatif détecté</span><span class="sxs-lookup"><span data-stu-id="2d5b3-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="2d5b3-255">ligne d’objet Hello de notification par courrier électronique de hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-255">hello subject line of hello email notification.</span></span>  |
    | <span data-ttu-id="2d5b3-256">**Corps**</span><span class="sxs-lookup"><span data-stu-id="2d5b3-256">**Body**</span></span> | <span data-ttu-id="2d5b3-257">Texte du tweet, Emplacement</span><span class="sxs-lookup"><span data-stu-id="2d5b3-257">Tweet text, Location</span></span> | <span data-ttu-id="2d5b3-258">Cliquez sur hello **tweetez-texte** et **emplacement** paramètres.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-258">Click hello **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="2d5b3-259">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-259">Click **Save**.</span></span>

<span data-ttu-id="2d5b3-260">Maintenant que le flux de travail hello est terminée, vous pouvez activer l’application logique de hello et consultez la fonction hello au travail.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-260">Now that hello workflow is complete, you can enable hello logic app and see hello function at work.</span></span>

## <a name="test-hello-workflow"></a><span data-ttu-id="2d5b3-261">Flux de travail de test hello</span><span class="sxs-lookup"><span data-stu-id="2d5b3-261">Test hello workflow</span></span>

1. <span data-ttu-id="2d5b3-262">Dans le Concepteur d’application logique de hello, cliquez sur **exécuter** toostart hello application.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-262">In hello Logic App Designer, click **Run** toostart hello app.</span></span>

2. <span data-ttu-id="2d5b3-263">Dans la colonne de gauche hello, cliquez sur **vue d’ensemble** état hello toosee application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-263">In hello left column, click **Overview** toosee hello status of hello logic app.</span></span> 
 
    ![État d’exécution de l’application logique](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="2d5b3-265">(Facultatif) Cliquez sur une des hello exécute toosee détails de l’exécution de hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-265">(Optional) Click one of hello runs toosee details of hello execution.</span></span>

4. <span data-ttu-id="2d5b3-266">Fonction, tooyour, afficher les journaux de hello et vérifiez que les valeurs de sentiment reçus et traités.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-266">Go tooyour function, view hello logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Affichez les journaux de fonction](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="2d5b3-268">Lorsqu’un sentiment potentiellement négatif est détecté, vous recevez un courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="2d5b3-269">Si vous n’avez pas reçu un message électronique, vous pouvez modifier chaque fois tooreturn de code de fonction hello rouge :</span><span class="sxs-lookup"><span data-stu-id="2d5b3-269">If you haven't received an email, you can change hello function code tooreturn RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="2d5b3-270">Après avoir vérifié les notifications par courrier électronique, modifier le code d’origine de toohello précédent :</span><span class="sxs-lookup"><span data-stu-id="2d5b3-270">After you have verified email notifications, change back toohello original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="2d5b3-271">Une fois que vous avez terminé ce didacticiel, vous devez désactiver l’application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-271">After you have completed this tutorial, you should disable hello logic app.</span></span> <span data-ttu-id="2d5b3-272">En désactivant l’application hello, vous éviter d’être facturés pour les exécutions et que vous utilisez des transactions hello dans votre compte de Services cognitifs.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-272">By disabling hello app, you avoid being charged for executions and using up hello transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="2d5b3-273">Maintenant, vous savez combien il est facile toointegrate des fonctions dans un flux de travail Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-273">Now you have seen how easy it is toointegrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-hello-logic-app"></a><span data-ttu-id="2d5b3-274">Désactiver l’application logique de hello</span><span class="sxs-lookup"><span data-stu-id="2d5b3-274">Disable hello logic app</span></span>

<span data-ttu-id="2d5b3-275">application de la logique de hello toodisable, cliquez sur **vue d’ensemble** puis cliquez sur **désactiver** haut hello écran hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-275">toodisable hello logic app, click **Overview** and then click **Disable** at hello top of hello screen.</span></span> <span data-ttu-id="2d5b3-276">Cela arrête hello logique application en cours d’exécution et la comptabilisation des frais sans supprimer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-276">This stops hello logic app from running and incurring charges without deleting hello app.</span></span> 

![Journaux de fonction](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="2d5b3-278">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d5b3-278">Next steps</span></span>

<span data-ttu-id="2d5b3-279">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="2d5b3-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2d5b3-280">Créez un compte Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="2d5b3-281">Créer une fonction qui classe le sentiment des tweets.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="2d5b3-282">Créer une application de la logique qui se connecte tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-282">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="2d5b3-283">Ajouter une application de sentiment détection toohello logique.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-283">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="2d5b3-284">Se connecter (fonction) toohello application hello logique.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-284">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="2d5b3-285">Envoyer un courrier électronique en fonction de la réponse hello à partir de la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-285">Send an email based on hello response from hello function.</span></span>

<span data-ttu-id="2d5b3-286">Avancer toolearn de didacticiel suivant toohello comment toocreate une API sans serveur de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="2d5b3-286">Advance toohello next tutorial toolearn how toocreate a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="2d5b3-287">Créer une API sans serveur à l’aide d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="2d5b3-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="2d5b3-288">toolearn en savoir plus sur les applications de la logique, consultez [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="2d5b3-288">toolearn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

