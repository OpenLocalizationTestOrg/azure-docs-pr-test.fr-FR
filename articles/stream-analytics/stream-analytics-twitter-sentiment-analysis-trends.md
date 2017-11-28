---
title: "analyse des sentiments Twitter aaaReal-temps avec Analytique de flux de données Azure | Documents Microsoft"
description: "Découvrez comment toouse Analytique de flux de données pour l’analyse de sentiments Twitter en temps réel. Obtenir des instructions à partir de toodata de génération d’événements dans un tableau de bord en direct."
keywords: "analyse de tendances twitter en temps réel, analyse de sentiments, analyse des réseaux sociaux, exemple d’analyse de tendances"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="1bcf7-105">Analyse de sentiments Twitter en temps réel dans Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1bcf7-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="1bcf7-106">Découvrez comment toobuild analytique sociaux en mettant en temps réel dans une solution d’analyse de l’opinion Twitter événements aux concentrateurs d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-106">Learn how toobuild a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="1bcf7-107">Vous pouvez ensuite écrire les données de salutation tooanalyze une requête Analytique de flux de données Azure et un magasin hello résultats pour une utilisation ultérieure, ou utilisent un tableau de bord et [Power BI](https://powerbi.com/) insights tooprovide en temps réel.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-107">You can then write an Azure Stream Analytics query tooanalyze hello data and either store hello results for later use or use a dashboard and [Power BI](https://powerbi.com/) tooprovide insights in real time.</span></span>

<span data-ttu-id="1bcf7-108">Les outils d’analyse des réseaux sociaux aident les organisations à comprendre les tendances.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="1bcf7-109">Les sujets populaires sont les sujets significatifs et avis apparaissant dans un grand nombre de billets sur les réseaux sociaux.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="1bcf7-110">Analyse des sentiments, également appelé *mining d’avis*, utilise des attitudes sociaux analytique outils toodetermine vers un produit, l’idée et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools toodetermine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="1bcf7-111">Analyse des tendances en temps réel Twitter est un bon exemple d’un outil analytique, comme modèle de hello #sqlhelp abonnement vous permet de toolisten (hashtags) de mots clés toospecific et développer l’analyse des sentiments Hello de flux.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-111">Real-time Twitter trend analysis is a great example of an analytics tool, because hello hashtag subscription model enables you toolisten toospecific keywords (hashtags) and develop sentiment analysis of hello feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="1bcf7-112">Scénario : analyse de sentiments sur les réseaux sociaux en temps réel</span><span class="sxs-lookup"><span data-stu-id="1bcf7-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="1bcf7-113">Une société qui a un site Web de médias est intéressée de gagner un avantage sur ses concurrents en présentant du contenu de site est immédiatement pertinente tooits lecteurs.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant tooits readers.</span></span> <span data-ttu-id="1bcf7-114">société de Hello utilise une analyse sociaux sur des sujets qui sont pertinentes tooreaders en effectuant une analyse des sentiments en temps réel des données de Twitter.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-114">hello company uses social media analysis on topics that are relevant tooreaders by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="1bcf7-115">rubriques de tendances tooidentify en temps réel sur Twitter, hello entreprise besoins d’analytique en temps réel sur le volume de tweet de hello et opinion vis-à-vis des principales rubriques.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-115">tooidentify trending topics in real time on Twitter, hello company needs real-time analytics about hello tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="1bcf7-116">En d’autres termes, hello est un moteur d’analytique sentiment analysis qui repose sur ce flux de médias sociaux.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-116">In other words, hello need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bcf7-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1bcf7-117">Prerequisites</span></span>
<span data-ttu-id="1bcf7-118">Dans ce didacticiel, vous utilisez une application cliente qui se connecte tooTwitter, recherche tweet ayant certaines hashtags (que vous pouvez définir).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-118">In this tutorial, you use a client application that connects tooTwitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="1bcf7-119">Dans l’ordre toorun hello application et analyser hello tweet à l’aide d’Analytique de diffusion en continu d’Azure, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-119">In order toorun hello application and analyze hello tweets using Azure Streaming Analytics, you must have hello following:</span></span>

* <span data-ttu-id="1bcf7-120">Un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="1bcf7-120">An Azure subscription</span></span>
* <span data-ttu-id="1bcf7-121">un compte Twitter ;</span><span class="sxs-lookup"><span data-stu-id="1bcf7-121">A Twitter account</span></span> 
* <span data-ttu-id="1bcf7-122">Une application Twitter et hello [jeton d’accès OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) pour cette application.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-122">A Twitter application, and hello [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="1bcf7-123">Nous fournirons des informations détaillées sur la manière de toocreate une application Twitter plus tard.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-123">We provide high-level instructions for how toocreate a Twitter application later.</span></span>
* <span data-ttu-id="1bcf7-124">flux d’application TwitterWPFClient Hello, qui lit hello Twitter.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-124">hello TwitterWPFClient application, which reads hello Twitter feed.</span></span> <span data-ttu-id="1bcf7-125">tooget cette application, le téléchargement hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) à partir de GitHub et puis décompressez le package de hello dans un dossier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-125">tooget this application, download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip hello package into a folder on your computer.</span></span> <span data-ttu-id="1bcf7-126">Si vous souhaitez toosee hello source code et exécuter l’application hello dans un débogueur, vous pouvez obtenir le code source hello de [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-126">If you want toosee hello source code and run hello application in a debugger, you can get hello source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="1bcf7-127">Créer un concentrateur Event Hub pour l’entrée Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1bcf7-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="1bcf7-128">exemple d’application Hello génère des événements et les transmet un concentrateur d’événements Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-128">hello sample application generates events and pushes them tooan Azure event hub.</span></span> <span data-ttu-id="1bcf7-129">Concentrateurs d’événements Azure constituent la méthode hello préféré ingestion d’événements pour l’Analytique des flux de données.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-129">Azure event hubs are hello preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="1bcf7-130">Pour plus d’informations, consultez hello [documentation d’Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-130">For more information, see hello [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="1bcf7-131">Créer un espace de noms Event Hub et un concentrateur Event Hub</span><span class="sxs-lookup"><span data-stu-id="1bcf7-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="1bcf7-132">Dans cette procédure, vous créez un espace de noms de concentrateur d’événements, et puis vous ajoutez un espace de noms événement hub toothat.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-132">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namespace.</span></span> <span data-ttu-id="1bcf7-133">Espaces de noms de concentrateur événement toologically groupe relatives des instances de bus d’événements.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-133">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="1bcf7-134">Connectez-vous à toohello portail Azure, puis cliquez sur **nouveau** > **Internet of Things** > **concentrateur d’événements**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-134">Log  in toohello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="1bcf7-135">Bonjour **créer l’espace de noms** panneau, entrez un nom d’espace de noms tels que `<yourname>-socialtwitter-eh-ns`.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-135">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="1bcf7-136">Vous pouvez utiliser n’importe quel nom pour l’espace de noms hello, mais le nom de hello doit être valide pour une URL et il doit être unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-136">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="1bcf7-137">Sélectionnez un abonnement, créez ou choisissez un groupe de ressources, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![Créer un espace de noms Event Hub](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="1bcf7-139">Lors de l’espace de noms hello a terminé le déploiement, trouver hello événement hub espace de noms dans votre liste de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-139">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="1bcf7-140">Cliquez sur le nouvel espace de noms hello et dans le panneau espace de noms de hello, cliquez sur  **+ &nbsp;concentrateur d’événements**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-140">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="1bcf7-141">bouton de concentrateur d’événements ajouter Hello pour la création d’un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="1bcf7-141">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="1bcf7-142">Hub d’événements de nom hello `socialtwitter-eh`.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-142">Name hello new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="1bcf7-143">Vous pouvez utiliser un autre nom.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-143">You can use a different name.</span></span> <span data-ttu-id="1bcf7-144">Si vous le faites, prenez note de celui-ci, car vous devez les nom hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-144">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="1bcf7-145">Vous n’avez pas besoin tooset d’autres options pour le concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-145">You don't need tooset any other options for hello event hub.</span></span>

    ![Panneau de création d’un concentrateur Event Hub](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="1bcf7-147">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-147">Click **Create**.</span></span>


### <a name="grant-access-toohello-event-hub"></a><span data-ttu-id="1bcf7-148">Concentrateur d’événements grant access toohello</span><span class="sxs-lookup"><span data-stu-id="1bcf7-148">Grant access toohello event hub</span></span>

<span data-ttu-id="1bcf7-149">Avant d’un processus peut envoyer le concentrateur d’événements de données tooan, concentrateur d’événements hello doit avoir une stratégie qui autorise l’accès approprié.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-149">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="1bcf7-150">stratégie d’accès Hello génère une chaîne de connexion qui inclut les informations d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-150">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="1bcf7-151">Dans le panneau d’espace de noms des événements du hello, cliquez sur **concentrateurs d’événements** puis cliquez sur nom hello de votre hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-151">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="1bcf7-152">Dans le panneau de concentrateur d’événements de hello, cliquez sur **les stratégies d’accès partagé** puis cliquez sur  **+ &nbsp;ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-152">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="1bcf7-153">Assurez-vous que vous travaillez avec un concentrateur d’événements hello, pas hello événement hub espace de noms.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-153">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="1bcf7-154">Ajoutez la stratégie nommée `socialtwitter-access` et, pour **Revendication**, sélectionnez **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![Panneau de création d’une stratégie d’accès au concentrateur Event Hub](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="1bcf7-156">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-156">Click **Create**.</span></span>

5.  <span data-ttu-id="1bcf7-157">Après le déploiement de stratégie de hello, sélectionnez-la dans la liste hello des stratégies d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-157">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="1bcf7-158">Case de hello rechercher **la clé primaire de la chaîne de connexion** et cliquez sur la chaîne de connexion toohello suivant hello copie bouton.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-158">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![Copie la clé de chaîne de connexion principale hello à partir de la stratégie d’accès hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="1bcf7-160">Collez la chaîne de connexion hello dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-160">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="1bcf7-161">Vous devez cette chaîne de connexion pour la section suivante de hello, après avoir apporté quelques tooit de petites modifications.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-161">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="1bcf7-162">chaîne de connexion Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-162">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="1bcf7-163">Notez que chaîne de connexion hello contient plusieurs paires clé-valeur, séparées par des points-virgules : `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, et `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-163">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="1bcf7-164">Pour la sécurité, les parties de la chaîne de connexion hello dans hello exemple ont été supprimés.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-164">For security, parts of hello connection string in hello example have been removed.</span></span>

8.  <span data-ttu-id="1bcf7-165">Dans l’éditeur de texte hello, supprimez hello `EntityPath` paire de chaîne de connexion hello (n’oubliez pas point-virgule hello tooremove qui le précède).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-165">In hello text editor, remove hello `EntityPath` pair from hello connection string (don't forget tooremove hello semicolon that precedes it).</span></span> <span data-ttu-id="1bcf7-166">Lorsque vous avez terminé, la chaîne de connexion hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-166">When you're done, hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a><span data-ttu-id="1bcf7-167">Configurer et démarrer l’application cliente de Twitter hello</span><span class="sxs-lookup"><span data-stu-id="1bcf7-167">Configure and start hello Twitter client application</span></span>
<span data-ttu-id="1bcf7-168">application cliente de Hello Obtient les événements tweet directement à partir de Twitter.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-168">hello client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="1bcf7-169">Dans la commande toodo, il doit hello de toocall autorisation Twitter les API de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-169">In order toodo so, it needs permission toocall hello Twitter Streaming APIs.</span></span> <span data-ttu-id="1bcf7-170">tooconfigure que l’autorisation, que vous créez une application dans Twitter, ce qui génère des informations d’identification uniques (par exemple, un jeton OAuth).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-170">tooconfigure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="1bcf7-171">Vous pouvez ensuite configurer de hello client application toouse ces informations d’identification lorsqu’il émet des appels d’API.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-171">You can then configure hello client application toouse these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="1bcf7-172">Création d'une application Twitter</span><span class="sxs-lookup"><span data-stu-id="1bcf7-172">Create a Twitter application</span></span>
<span data-ttu-id="1bcf7-173">Si vous ne possédez pas encore une application Twitter que vous pouvez utiliser pour ce didacticiel, vous pouvez en créer une.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="1bcf7-174">Vous devez déjà posséder un compte Twitter.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="1bcf7-175">processus exact de Hello dans Twitter pour la création d’une application et l’obtention de jeton, des secrets et des clés de hello peut changer.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-175">hello exact process in Twitter for creating an application and getting hello keys, secrets, and token might change.</span></span> <span data-ttu-id="1bcf7-176">Si ces instructions ne correspondent pas ce que vous voyez sur le site de Twitter hello, consultez la documentation du développeur toohello Twitter.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-176">If these instructions don't match what you see on hello Twitter site, refer toohello Twitter developer documentation.</span></span>

1. <span data-ttu-id="1bcf7-177">Accédez toohello [page de gestion des applications Twitter](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-177">Go toohello [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="1bcf7-178">Créez une application.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-178">Create a new application.</span></span> 

    * <span data-ttu-id="1bcf7-179">Pour l’URL du site Web de hello, spécifiez une URL valide.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-179">For hello website URL, specify a valid URL.</span></span> <span data-ttu-id="1bcf7-180">Il n’a pas toobe un site en direct.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-180">It does not have toobe a live site.</span></span> <span data-ttu-id="1bcf7-181">(Vous ne pouvez pas spécifier simplement `localhost`.)</span><span class="sxs-lookup"><span data-stu-id="1bcf7-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="1bcf7-182">Renseignez le champ de rappel hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-182">Leave hello callback field blank.</span></span> <span data-ttu-id="1bcf7-183">application cliente de Hello que vous utilisez pour ce didacticiel ne requiert pas rappels.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-183">hello client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Création d’une application dans Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="1bcf7-185">Si vous le souhaitez, modifier les autorisations de l’application hello tooread uniquement.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-185">Optionally, change hello application's permissions tooread-only.</span></span>

4. <span data-ttu-id="1bcf7-186">Lors de l’application hello est créée, accédez à toohello **clés et les jetons d’accès** page.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-186">When hello application is created, go toohello **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="1bcf7-187">Cliquez sur hello bouton toogenerate un jeton d’accès et le secret du jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-187">Click hello button toogenerate an access token and access token secret.</span></span>

<span data-ttu-id="1bcf7-188">Gardez les informations utiles, car vous en aurez besoin dans la procédure suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-188">Keep this information handy, because you will need it in hello next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="1bcf7-189">clés de Hello et les secrets pour l’application de Twitter hello fournissent l’accès tooyour Twitter compte.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-189">hello keys and secrets for hello Twitter application provide access tooyour Twitter account.</span></span> <span data-ttu-id="1bcf7-190">Considérer ces informations comme sensibles, même hello comme vous le faites votre mot de passe Twitter.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-190">Treat this information as sensitive, hello same as you do your Twitter password.</span></span> <span data-ttu-id="1bcf7-191">Par exemple, ne pas incorporer ces informations dans une application que vous donnez à tooothers.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-191">For example, don't embed this information in an application that you give tooothers.</span></span> 


### <a name="configure-hello-client-application"></a><span data-ttu-id="1bcf7-192">Configurer l’application cliente de hello</span><span class="sxs-lookup"><span data-stu-id="1bcf7-192">Configure hello client application</span></span>
<span data-ttu-id="1bcf7-193">Nous avons créé une application cliente qui se connecte à l’aide des données tooTwitter [API de diffusion en continu de Twitter](https://dev.twitter.com/streaming/overview) toocollect les événements tweet sur un ensemble spécifique de rubriques.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-193">We've created a client application that connects tooTwitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) toocollect tweet events about a specific set of topics.</span></span> <span data-ttu-id="1bcf7-194">application Hello utilise hello [Sentiment140](http://help.sentiment140.com/) outil open source, qui assigne hello suivant tweet de sentiment valeur tooeach :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-194">hello application uses hello [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns hello following sentiment value tooeach tweet:</span></span>

* <span data-ttu-id="1bcf7-195">0 = négatif</span><span class="sxs-lookup"><span data-stu-id="1bcf7-195">0 = negative</span></span>
* <span data-ttu-id="1bcf7-196">2 = neutre</span><span class="sxs-lookup"><span data-stu-id="1bcf7-196">2 = neutral</span></span>
* <span data-ttu-id="1bcf7-197">4 = positif</span><span class="sxs-lookup"><span data-stu-id="1bcf7-197">4 = positive</span></span>

<span data-ttu-id="1bcf7-198">Une fois que les événements tweet hello ont été attribuées à une valeur d’indice de sentiment, elles sont appliquées concentrateur d’événements toohello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-198">After hello tweet events have been assigned a sentiment value, they are pushed toohello event hub that you created earlier.</span></span>

<span data-ttu-id="1bcf7-199">Avant l’exécution de l’application hello, il requiert certaines informations vous concernant, telles que les clés de Twitter hello et chaîne de connexion de concentrateur événement hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-199">Before hello application runs, it requires certain information from you, like hello Twitter keys and hello event hub connection string.</span></span> <span data-ttu-id="1bcf7-200">Vous pouvez fournir des informations de configuration hello des façons suivantes :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-200">You can provide hello configuration information in these ways:</span></span>

* <span data-ttu-id="1bcf7-201">Exécutez l’application hello, puis utilisez l’application hello à tooenter hello clés, les secrets et chaîne de connexion pour l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-201">Run hello application, and then use hello application's UI tooenter hello keys, secrets, and connection string.</span></span> <span data-ttu-id="1bcf7-202">Si vous le faites, les informations de configuration hello sont utilisées pour la session en cours, mais il n’est pas enregistré.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-202">If you do this, hello configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="1bcf7-203">Modifier le fichier .config de l’application hello et définir des valeurs hello il.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-203">Edit hello application's .config file and set hello values there.</span></span> <span data-ttu-id="1bcf7-204">Cette approche conserve les informations de configuration hello, mais il signifie également que ces informations potentiellement sensibles sont stockées en texte brut sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-204">This approach persists hello configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="1bcf7-205">Hello procédure suivante décrit les deux approches.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-205">hello following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="1bcf7-206">Assurez-vous que vous avez téléchargé et décompressé hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, comme indiqué dans les conditions préalables de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-206">Make sure you've downloaded and unzipped hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in hello prerequisites.</span></span>

2. <span data-ttu-id="1bcf7-207">les valeurs de hello tooset en cours d’exécution (et uniquement pour hello session en cours), exécutez hello `TwitterWPFClient.exe` application.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-207">tooset hello values at run time (and only for hello current session), run hello `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="1bcf7-208">Lors de l’application hello vous y invite, entrez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-208">When hello application prompts you, enter hello following values:</span></span>

    * <span data-ttu-id="1bcf7-209">Hello Twitter consommateur clé (API).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-209">hello Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="1bcf7-210">Hello Twitter question secrète du client (clé secrète API).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-210">hello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="1bcf7-211">Hello jeton d’accès Twitter.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-211">hello Twitter Access Token.</span></span>
    * <span data-ttu-id="1bcf7-212">Hello Secret du jeton accès Twitter.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-212">hello Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="1bcf7-213">informations de chaîne de connexion Hello que vous avez enregistré précédemment.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-213">hello connection string information that you saved earlier.</span></span> <span data-ttu-id="1bcf7-214">Assurez-vous que vous utilisez de chaîne de connexion hello que vous avez supprimé hello `EntityPath` paire clé-valeur à partir de.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-214">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="1bcf7-215">Bonjour mots clés Twitter sentiment toodetermine pour souhaitées.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-215">hello Twitter keywords that you want toodetermine sentiment for.</span></span>

   ![Application TwitterWpfClient en cours d’exécution, affichant des paramètres masqués](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="1bcf7-217">les valeurs hello tooset utilisent de manière permanente, un fichier de texte éditeur tooopen hello TwitterWpfClient.exe.config.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-217">tooset hello values persistently, use a text editor tooopen hello TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="1bcf7-218">Ensuite, dans hello `<appSettings>` élément, cela :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-218">Then in hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="1bcf7-219">Définissez `oauth_consumer_key` toohello Twitter consommateur clé (API).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-219">Set `oauth_consumer_key` toohello Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="1bcf7-220">Définissez `oauth_consumer_secret` toohello Twitter question secrète du client (clé secrète API).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-220">Set `oauth_consumer_secret` toohello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="1bcf7-221">Définissez `oauth_token` toohello jeton d’accès Twitter.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-221">Set `oauth_token` toohello Twitter Access Token.</span></span>
    * <span data-ttu-id="1bcf7-222">Définissez `oauth_token_secret` toohello Secret du jeton accès Twitter.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-222">Set `oauth_token_secret` toohello Twitter Access Token Secret.</span></span>

    <span data-ttu-id="1bcf7-223">Plus loin dans hello `<appSettings>` élément, apporter ces modifications :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-223">Later in hello `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="1bcf7-224">Définissez `EventHubName` nom de hub d’événements toohello (autrement dit, toohello de valeur du chemin d’accès de hello entité).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-224">Set `EventHubName` toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="1bcf7-225">Définissez `EventHubNameConnectionString` chaîne de connexion toohello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-225">Set `EventHubNameConnectionString` toohello connection string.</span></span> <span data-ttu-id="1bcf7-226">Assurez-vous que vous utilisez de chaîne de connexion hello que vous avez supprimé hello `EntityPath` paire clé-valeur à partir de.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-226">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="1bcf7-227">Hello `<appSettings>` section ressemble à hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-227">hello `<appSettings>` section looks like hello following example.</span></span> <span data-ttu-id="1bcf7-228">(Pour des raisons de clarté et de sécurité, nous avons inséré des retours automatiques de ligne et supprimé des caractères.)</span><span class="sxs-lookup"><span data-stu-id="1bcf7-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![Fichier de configuration d’application TwitterWpfClient dans un éditeur de texte, affichant les clés de Twitter hello et des secrets et des informations de chaîne de connexion hello événement hub](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="1bcf7-230">Si vous n’avez pas déjà commencé application hello, exécutez TwitterWpfClient.exe maintenant.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-230">If you didn't already start hello application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="1bcf7-231">Cliquez sur le sentiment social du toocollect bouton vert Démarrer hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-231">Click hello green start button toocollect social sentiment.</span></span> <span data-ttu-id="1bcf7-232">Vous voyez les événements Tweet avec hello **créédans**, **rubrique**, et **SentimentScore** valeurs envoyées tooyour concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-232">You see Tweet events with hello **CreatedAt**, **Topic**, and **SentimentScore** values being sent tooyour event hub.</span></span>

    ![Application TwitterWpfClient en cours d’exécution, affichant une liste de tweets](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="1bcf7-234">Si vous constatez des erreurs, et vous ne voyez pas un flux de données de tweets affiché dans la partie inférieure de hello de fenêtre hello, vérifiez attentivement les secrets et des clés de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-234">If you see errors, and you don't see a stream of tweets displayed in hello lower part of hello window, double-check hello keys and secrets.</span></span> <span data-ttu-id="1bcf7-235">Vérifiez également la chaîne de connexion hello (Assurez-vous qu’il ne comprend pas hello `EntityPath` clé et valeur.)</span><span class="sxs-lookup"><span data-stu-id="1bcf7-235">Also check hello connection string (make sure that it does not include hello `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="1bcf7-236">Création d’un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1bcf7-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="1bcf7-237">Maintenant que les événements tweet sont diffusion en continu en temps réel à partir de Twitter, vous pouvez configurer un tooanalyze de tâche de flux de données Analytique ces événements en temps réel.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job tooanalyze these events in real time.</span></span>

1. <span data-ttu-id="1bcf7-238">Bonjour portail Azure, cliquez sur **nouveau** > **Internet of Things** > **tâche de flux de données Analytique**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-238">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="1bcf7-239">Nom du travail hello `socialtwitter-sa-job` et spécifiez un abonnement, le groupe de ressources et l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-239">Name hello job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="1bcf7-240">Il s’agit d’une bonne idée tooplace hello hello et travail de concentrateur d’événements Bonjour même région pour meilleures performances et que vous ne payez tootransfer données entre les régions.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-240">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![Création d’un travail Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="1bcf7-242">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-242">Click **Create**.</span></span>

    <span data-ttu-id="1bcf7-243">Hello travail est créé et le portail de hello affiche les détails de la tâche.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-243">hello job is created and hello portal displays job details.</span></span>


## <a name="specify-hello-job-input"></a><span data-ttu-id="1bcf7-244">Spécifier une entrée de tâche hello</span><span class="sxs-lookup"><span data-stu-id="1bcf7-244">Specify hello job input</span></span>

1. <span data-ttu-id="1bcf7-245">Dans votre tâche de flux de données Analytique, sous **travail topologie** milieu hello du Panneau de tâche hello, cliquez sur **entrées**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-245">In your Stream Analytics job, under **Job Topology** in hello middle of hello job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="1bcf7-246">Bonjour **entrées** panneau, cliquez sur  **+ &nbsp;ajouter** puis remplissez panneau hello avec ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-246">In hello **Inputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="1bcf7-247">**Alias d’entrée**: utiliser le nom hello `TwitterStream`.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-247">**Input alias**: Use hello name `TwitterStream`.</span></span> <span data-ttu-id="1bcf7-248">Si vous utilisez un autre nom, prenez-en note, car vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="1bcf7-249">**Type de source** : sélectionnez **Flux de données**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="1bcf7-250">**Source** : sélectionnez **Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="1bcf7-251">**Option d’importation** : sélectionnez **Utiliser le hub d’événements de l’abonnement actuel**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="1bcf7-252">**Espace de noms service bus**: sélectionnez hello événement hub namespace que vous avez créé précédemment (`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-252">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="1bcf7-253">**Concentrateur d’événements**: concentrateur d’événements hello Select que vous avez créé précédemment (`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-253">**Event hub**: Select hello event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="1bcf7-254">**Nom de la stratégie hub événement**: sélectionnez la stratégie d’accès hello que vous avez créé précédemment (`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-254">**Event hub policy name**: Select hello access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Créer une entrée pour le travail Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="1bcf7-256">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-256">Click **Create**.</span></span>


## <a name="specify-hello-job-query"></a><span data-ttu-id="1bcf7-257">Spécifiez la requête de travail hello</span><span class="sxs-lookup"><span data-stu-id="1bcf7-257">Specify hello job query</span></span>

<span data-ttu-id="1bcf7-258">Stream Analytics prend en charge un modèle de requête simple et déclaratif pour la description des transformations.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="1bcf7-259">toolearn en savoir plus sur le langage de hello, consultez hello [référence du langage de requête Azure Stream Analytique](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-259">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="1bcf7-260">Ce didacticiel aborde la création et le test de plusieurs requêtes sur des données Twitter.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="1bcf7-261">nombre de hello toocompare de mentionne les rubriques, vous pouvez utiliser un [fenêtre bascule](https://msdn.microsoft.com/library/azure/dn835055.aspx) nombre de hello tooget de mentionne par rubrique toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-261">toocompare hello number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="1bcf7-262">Fermer hello **entrées** panneau si vous n’avez pas encore.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-262">Close hello **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="1bcf7-263">Dans le panneau de tâche hello, cliquez sur hello **requête** boîte.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-263">In hello job blade, click hello **Query** box.</span></span> <span data-ttu-id="1bcf7-264">Azure répertorie les entrées hello et sorties qui sont configurés pour la tâche de hello et vous permet de créer une requête qui vous permet de transforment les flux d’entrée hello lors de leur envoi toohello sortie.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-264">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>

3. <span data-ttu-id="1bcf7-265">Vérifiez que hello TwitterWpfClient application est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-265">Make sure that hello TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="1bcf7-266">Bonjour **requête** panneau, cliquez sur toohello suivant de points hello `TwitterStream` d’entrée, puis sélectionnez **les exemples de données à partir de l’entrée**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-266">In hello **Query** blade, click hello dots next toohello `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![Menu options toouse exemples de données pour hello Analytique de diffusion en continu de la tâche entrée, « Exemples de données à partir de l’entrée « sélectionné](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="1bcf7-268">Cette opération ouvre un panneau qui vous permet de spécifier la quantité tooget de données d’exemple, définie en termes de la durée pendant laquelle le flux d’entrée tooread hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-268">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

4. <span data-ttu-id="1bcf7-269">Définissez **Minutes** too3 puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-269">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    ![Options d’échantillonnage de flux d’entrée de hello, avec « 3 minutes » sélectionnées.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="1bcf7-271">Azure échantillonne les données du flux d’entrée de hello sur 3 minutes et vous avertit lorsque les données d’exemple hello sont prêtes.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-271">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="1bcf7-272">(Cette opération prend quelques instants.)</span><span class="sxs-lookup"><span data-stu-id="1bcf7-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="1bcf7-273">Hello exemples de données sont stockées temporairement et sont disponibles tant que fenêtre de requête hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-273">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="1bcf7-274">Si vous fermez la fenêtre de requête hello, les données d’exemple hello sont ignorées, et vous avez toocreate un nouvel ensemble d’exemples de données.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-274">If you close hello query window, hello sample data is discarded, and you have toocreate a new set of sample data.</span></span> 

5. <span data-ttu-id="1bcf7-275">Modifier la requête hello dans hello code éditeur toohello suivant :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-275">Change hello query in hello code editor toohello following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="1bcf7-276">Si n’avez pas utilisé `TwitterStream` en tant que de hello alias pour l’entrée de hello, remplacez votre alias pour `TwitterStream` dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-276">If didn't use `TwitterStream` as hello alias for hello input, substitute your alias for `TwitterStream` in hello query.</span></span>  

    <span data-ttu-id="1bcf7-277">Cette requête utilise hello **TIMESTAMP BY** mot clé toospecify un champ d’horodatage dans toobe de charge utile hello utilisée dans le calcul de temporelle hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-277">This query uses hello **TIMESTAMP BY** keyword toospecify a timestamp field in hello payload toobe used in hello temporal computation.</span></span> <span data-ttu-id="1bcf7-278">Si ce champ n’est pas spécifié, l’opération de fenêtrage hello est effectuée à l’aide de temps hello chaque événement reçus sur le concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-278">If this field isn't specified, hello windowing operation is performed by using hello time that each event arrived at hello event hub.</span></span> <span data-ttu-id="1bcf7-279">En savoir plus dans la section hello « heure d’arrivée et heure de l’Application » de [référence de flux de requête Analytique](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-279">Learn more in hello "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="1bcf7-280">Cette requête accède également à un horodatage de fin hello de chaque fenêtre à l’aide de hello **System.Timestamp** propriété.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-280">This query also accesses a timestamp for hello end of each window by using hello **System.Timestamp** property.</span></span>

5. <span data-ttu-id="1bcf7-281">Cliquez sur **Test**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-281">Click **Test**.</span></span> <span data-ttu-id="1bcf7-282">requête de Hello s’exécute sur des données hello vous échantillonnées.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-282">hello query runs against hello data that you sampled.</span></span>
    
6. <span data-ttu-id="1bcf7-283">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-283">Click **Save**.</span></span> <span data-ttu-id="1bcf7-284">Cela permet d’économiser les requête hello en tant que partie du travail de diffusion en continu d’Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-284">This saves hello query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="1bcf7-285">(Il n’enregistre pas les données d’exemple hello).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-285">(It doesn't save hello sample data.)</span></span>


## <a name="experiment-using-different-fields-from-hello-stream"></a><span data-ttu-id="1bcf7-286">Expérience à l’aide des différents champs à partir de flux de hello</span><span class="sxs-lookup"><span data-stu-id="1bcf7-286">Experiment using different fields from hello stream</span></span> 

<span data-ttu-id="1bcf7-287">Hello tableau suivant répertorie les champs hello qui font partie de hello diffusion en continu des données JSON.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-287">hello following table lists hello fields that are part of hello JSON streaming data.</span></span> <span data-ttu-id="1bcf7-288">Vous pouvez tooexperiment libre dans l’éditeur de requête hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-288">Feel free tooexperiment in hello query editor.</span></span>

|<span data-ttu-id="1bcf7-289">Propriété JSON</span><span class="sxs-lookup"><span data-stu-id="1bcf7-289">JSON property</span></span> | <span data-ttu-id="1bcf7-290">Définition</span><span class="sxs-lookup"><span data-stu-id="1bcf7-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="1bcf7-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="1bcf7-291">CreatedAt</span></span> | <span data-ttu-id="1bcf7-292">temps de Hello que tweet hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-292">hello time that hello tweet was created</span></span>|
|<span data-ttu-id="1bcf7-293">Rubrique</span><span class="sxs-lookup"><span data-stu-id="1bcf7-293">Topic</span></span> | <span data-ttu-id="1bcf7-294">rubrique Hello qui correspond à hello spécifié (mot clé)</span><span class="sxs-lookup"><span data-stu-id="1bcf7-294">hello topic that matches hello specified keyword</span></span>|
|<span data-ttu-id="1bcf7-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="1bcf7-295">SentimentScore</span></span> | <span data-ttu-id="1bcf7-296">score d’opinion Hello de Sentiment140</span><span class="sxs-lookup"><span data-stu-id="1bcf7-296">hello sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="1bcf7-297">Auteur</span><span class="sxs-lookup"><span data-stu-id="1bcf7-297">Author</span></span> | <span data-ttu-id="1bcf7-298">handle de Twitter Hello qui a envoyé les tweet hello</span><span class="sxs-lookup"><span data-stu-id="1bcf7-298">hello Twitter handle that sent hello tweet</span></span>|
|<span data-ttu-id="1bcf7-299">Texte</span><span class="sxs-lookup"><span data-stu-id="1bcf7-299">Text</span></span> | <span data-ttu-id="1bcf7-300">corps Hello de tweet de hello</span><span class="sxs-lookup"><span data-stu-id="1bcf7-300">hello full body of hello tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="1bcf7-301">Créer un récepteur de sortie</span><span class="sxs-lookup"><span data-stu-id="1bcf7-301">Create an output sink</span></span>

<span data-ttu-id="1bcf7-302">Vous avez ainsi défini un flux d’événements, un tooingest d’entrée de concentrateur d’événements et une requête de tooperform une transformation sur les flux hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-302">You have now defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="1bcf7-303">dernière étape de Hello est toodefine récepteur de sortie pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-303">hello last step is toodefine an output sink for hello job.</span></span>  

<span data-ttu-id="1bcf7-304">Dans ce didacticiel, vous écrivez hello agrégée tweet événements à partir de hello tâche requête tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-304">In this tutorial, you write hello aggregated tweet events from hello job query tooAzure Blob storage.</span></span>  <span data-ttu-id="1bcf7-305">Vous pouvez également transmettre des votre tooAzure de résultats de la base de données SQL, stockage de Table Azure, les concentrateurs d’événements, ou Power BI, en fonction de votre application a besoin.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-305">You can also push your results tooAzure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-hello-job-output"></a><span data-ttu-id="1bcf7-306">Spécifiez la sortie des tâches hello</span><span class="sxs-lookup"><span data-stu-id="1bcf7-306">Specify hello job output</span></span>

1. <span data-ttu-id="1bcf7-307">Bonjour **travail topologie** , cliquez sur hello **sortie** boîte.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-307">In hello **Job Topology** section, click hello **Output** box.</span></span> 

2. <span data-ttu-id="1bcf7-308">Bonjour **sorties** panneau, cliquez sur  **+ &nbsp;ajouter** puis remplissez panneau hello avec ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-308">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="1bcf7-309">**Alias de sortie**: utiliser le nom hello `TwitterStream-Output`.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-309">**Output alias**: Use hello name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="1bcf7-310">**Sink** : sélectionnez **Stockage d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="1bcf7-311">**Options d’importation** : sélectionnez **Utiliser l’objet blob de stockage de l’abonnement actuel**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="1bcf7-312">**Compte de stockage** :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-312">**Storage account**.</span></span> <span data-ttu-id="1bcf7-313">sélectionnez **Créer un compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="1bcf7-314">**Compte de stockage** (seconde zone) :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-314">**Storage account** (second box).</span></span> <span data-ttu-id="1bcf7-315">entrez `YOURNAMEsa`, où `YOURNAME` représente votre nom ou une autre chaîne unique.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="1bcf7-316">nom de Hello peut utiliser que des lettres minuscules et des chiffres, et il doit être unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-316">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="1bcf7-317">**Conteneur** :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-317">**Container**.</span></span> <span data-ttu-id="1bcf7-318">Entrez `socialtwitter`.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="1bcf7-319">nom de compte de stockage Hello et le nom de conteneur sont tooprovide ensemble utilisé un URI pour le stockage d’objets blob hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-319">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Panneau Nouvelle sortie pour le travail Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="1bcf7-321">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-321">Click **Create**.</span></span> 

    <span data-ttu-id="1bcf7-322">Azure crée le compte de stockage hello et génère une clé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-322">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="1bcf7-323">Fermer hello **sorties** panneau.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-323">Close hello **Outputs** blade.</span></span> 


## <a name="start-hello-job"></a><span data-ttu-id="1bcf7-324">Démarrer le travail de hello</span><span class="sxs-lookup"><span data-stu-id="1bcf7-324">Start hello job</span></span>

<span data-ttu-id="1bcf7-325">Une entrée de travail, une requête et une sortie sont spécifiées.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="1bcf7-326">Vous êtes la tâche de flux de données Analytique hello toostart prêt.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-326">You are ready toostart hello Stream Analytics job.</span></span>

1. <span data-ttu-id="1bcf7-327">Vérifiez que hello TwitterWpfClient application est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-327">Make sure that hello TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="1bcf7-328">Dans le panneau de tâche hello, cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-328">In hello job blade, click **Start**.</span></span>

    ![Démarrer la tâche de flux de données Analytique hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="1bcf7-330">Bonjour **Start job** panneau, pour **heure de début de sortie des tâches**, sélectionnez **maintenant** puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-330">In hello **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![Panneau de « Démarrer le travail » pour la tâche de flux de données Analytique hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="1bcf7-332">Azure vous avertit de hello le travail a démarré, et dans le panneau de tâche hello, hello état affiché est **en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-332">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![Travail en cours d’exécution](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="1bcf7-334">Afficher la sortie de l’analyse de sentiments</span><span class="sxs-lookup"><span data-stu-id="1bcf7-334">View output for sentiment analysis</span></span>

<span data-ttu-id="1bcf7-335">Une fois votre travail a démarré en cours d’exécution et traite les flux Twitter en temps réel hello, vous pouvez afficher la sortie hello pour l’analyse de sentiments.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-335">After your job has started running and is processing hello real-time Twitter stream, you can view hello output for sentiment analysis.</span></span>

<span data-ttu-id="1bcf7-336">Vous pouvez utiliser un outil tel que [Azure Storage Explorer](https://http://storageexplorer.com/) ou [Explorateur Azure](http://www.cerebrata.com/products/azure-explorer/introduction) tooview votre tâche de sortie en temps réel.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview your job output in real time.</span></span> <span data-ttu-id="1bcf7-337">À ce stade, vous pouvez utiliser [Power BI](https://powerbi.com/) tooextend votre tooinclude application un tableau de bord personnalisé comme hello celui affiché dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-337">From here, you can use [Power BI](https://powerbi.com/) tooextend your application tooinclude a customized dashboard like hello one shown in hello following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a><span data-ttu-id="1bcf7-339">Créer une autre requête tooidentify les rubriques des tendances</span><span class="sxs-lookup"><span data-stu-id="1bcf7-339">Create another query tooidentify trending topics</span></span>

<span data-ttu-id="1bcf7-340">Une autre requête, vous pouvez utiliser toounderstand Twitter sentiment est basée sur un [fenêtre glissante](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bcf7-340">Another query you can use toounderstand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="1bcf7-341">rubriques de tendances tooidentify, vous recherchez les rubriques qui dépassent un seuil pour mentionne dans un laps de temps.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-341">tooidentify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="1bcf7-342">Pour des raisons de hello de ce didacticiel, vous recherchez les rubriques mentionnées plus de 20 fois Bonjour dernière 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-342">For hello purposes of this tutorial, you check for topics that are mentioned more than 20 times in hello last 5 seconds.</span></span>

1. <span data-ttu-id="1bcf7-343">Dans le panneau de tâche hello, cliquez sur **arrêter** tâche hello de toostop.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-343">In hello job blade, click **Stop** toostop hello job.</span></span> 

2. <span data-ttu-id="1bcf7-344">Bonjour **travail topologie** , cliquez sur hello **requête** boîte.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-344">In hello **Job Topology** section, click hello **Query** box.</span></span> 

3. <span data-ttu-id="1bcf7-345">Modifier les paramètres toohello hello requête suivants :</span><span class="sxs-lookup"><span data-stu-id="1bcf7-345">Change hello query toohello following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="1bcf7-346">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-346">Click **Save**.</span></span>

5. <span data-ttu-id="1bcf7-347">Vérifiez que hello TwitterWpfClient application est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-347">Make sure that hello TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="1bcf7-348">Cliquez sur **Démarrer** tâche hello de toorestart à l’aide de la nouvelle requête de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcf7-348">Click **Start** toorestart hello job using hello new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="1bcf7-349">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="1bcf7-349">Get support</span></span>
<span data-ttu-id="1bcf7-350">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="1bcf7-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bcf7-351">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1bcf7-351">Next steps</span></span>
* [<span data-ttu-id="1bcf7-352">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="1bcf7-352">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1bcf7-353">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1bcf7-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1bcf7-354">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1bcf7-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1bcf7-355">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1bcf7-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1bcf7-356">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1bcf7-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
