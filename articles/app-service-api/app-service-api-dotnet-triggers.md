---
title: "Déclencheurs d’application API App Service | Microsoft Docs"
description: "Comment implémenter des déclencheurs dans une application API dans Azure App Service"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 3ddfb142e7f1a47e2a8564387da785acf36fa61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="0eebc-103">Déclencheurs des applications API Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0eebc-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="0eebc-104">Cette version de l’article s’applique à la version du schéma 2014-12-01-preview API Apps.</span><span class="sxs-lookup"><span data-stu-id="0eebc-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="0eebc-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0eebc-105">Overview</span></span>
<span data-ttu-id="0eebc-106">Cet article explique comment implémenter des déclencheurs d'application API et comment les utiliser à partir d'une application logique.</span><span class="sxs-lookup"><span data-stu-id="0eebc-106">This article explains how to implement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="0eebc-107">Tous les extraits de code de cette rubrique sont copiés depuis l’ [exemple de code de l’application API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="0eebc-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="0eebc-108">Notez que vous devez télécharger le package NuGet suivant pour que le code de cet article puisse être généré et s'exécuter : [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="0eebc-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="0eebc-109">Que sont les déclencheurs des applications API ?</span><span class="sxs-lookup"><span data-stu-id="0eebc-109">What are API app triggers?</span></span>
<span data-ttu-id="0eebc-110">C'est un scénario courant pour une application API que de déclencher un événement, afin que les clients de l'application API puissent effectuer les actions appropriées en réponse à l'événement.</span><span class="sxs-lookup"><span data-stu-id="0eebc-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span></span> <span data-ttu-id="0eebc-111">Le mécanisme basé sur l'API REST qui prend en charge ce scénario est appelé un déclencheur d'application API.</span><span class="sxs-lookup"><span data-stu-id="0eebc-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="0eebc-112">Par exemple, supposons que votre code client utilise l' [application API du connecteur Twitter](../connectors/connectors-create-api-twitter.md) et que votre code doit exécuter une action basée sur les nouveaux tweets contenant des mots spécifiques.</span><span class="sxs-lookup"><span data-stu-id="0eebc-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="0eebc-113">Dans ce cas, vous pouvez définir un déclencheur d’émission ou de collecte pour répondre facilement à ce besoin.</span><span class="sxs-lookup"><span data-stu-id="0eebc-113">In this case, you might set up a poll or push trigger to facilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="0eebc-114">Déclencheur d'interrogation et déclencheur d'émission</span><span class="sxs-lookup"><span data-stu-id="0eebc-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="0eebc-115">Deux types de déclencheurs sont actuellement pris en charge :</span><span class="sxs-lookup"><span data-stu-id="0eebc-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="0eebc-116">Déclencheur d'interrogation : le client collecte auprès de l'application API les notifications de déclenchement d'un événement.</span><span class="sxs-lookup"><span data-stu-id="0eebc-116">Poll trigger - Client polls the API app for notification of an event having been fired</span></span>
* <span data-ttu-id="0eebc-117">Déclencheur d'émission : le client est notifié par l'application API quand un événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="0eebc-117">Push trigger - Client is notified by the API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="0eebc-118">Déclencheur d'interrogation :</span><span class="sxs-lookup"><span data-stu-id="0eebc-118">Poll trigger</span></span>
<span data-ttu-id="0eebc-119">Un déclencheur d'interrogation est implémenté sous la forme d'une API REST normale et il attend que ses clients (comme une application Logic) l'interrogent pour obtenir une notification.</span><span class="sxs-lookup"><span data-stu-id="0eebc-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span></span> <span data-ttu-id="0eebc-120">Alors que le client est susceptible de gérer les états, le déclencheur d'interrogation lui-même est sans état.</span><span class="sxs-lookup"><span data-stu-id="0eebc-120">While the client may maintain state, the poll trigger itself is stateless.</span></span>

<span data-ttu-id="0eebc-121">Les informations suivantes concernant les paquets de demande et de réponse montrent certains aspects essentiels du contrat du déclencheur d'interrogation :</span><span class="sxs-lookup"><span data-stu-id="0eebc-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span></span>

* <span data-ttu-id="0eebc-122">Demande</span><span class="sxs-lookup"><span data-stu-id="0eebc-122">Request</span></span>
  * <span data-ttu-id="0eebc-123">Méthode HTTP : GET</span><span class="sxs-lookup"><span data-stu-id="0eebc-123">HTTP method: GET</span></span>
  * <span data-ttu-id="0eebc-124">Paramètres</span><span class="sxs-lookup"><span data-stu-id="0eebc-124">Parameters</span></span>
    * <span data-ttu-id="0eebc-125">triggerState : ce paramètre facultatif permet aux clients de spécifier leur état, afin que le déclencheur d'interrogation puisse décider correctement s'il faut ou non retourner la notification, en fonction de l'état spécifié.</span><span class="sxs-lookup"><span data-stu-id="0eebc-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span></span>
    * <span data-ttu-id="0eebc-126">Paramètres spécifiques de l'API</span><span class="sxs-lookup"><span data-stu-id="0eebc-126">API-specific parameters</span></span>
* <span data-ttu-id="0eebc-127">Réponse</span><span class="sxs-lookup"><span data-stu-id="0eebc-127">Response</span></span>
  * <span data-ttu-id="0eebc-128">Code d'état **200** : la demande est valide et il existe une notification provenant du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="0eebc-128">Status code **200** - Request is valid and there is a notification from the trigger.</span></span> <span data-ttu-id="0eebc-129">Le contenu de la notification sera le corps de la réponse.</span><span class="sxs-lookup"><span data-stu-id="0eebc-129">The content of the notification will be the response body.</span></span> <span data-ttu-id="0eebc-130">Un en-tête « Retry-After » dans la réponse indique que des données de notification supplémentaires doivent être récupérées avec un appel de demande suivant.</span><span class="sxs-lookup"><span data-stu-id="0eebc-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="0eebc-131">Code d'état **202** : la demande est valide, mais il n'existe pas de nouvelle notification provenant du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="0eebc-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span></span>
  * <span data-ttu-id="0eebc-132">Code d'état **4xx** : la demande n'est pas valide.</span><span class="sxs-lookup"><span data-stu-id="0eebc-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="0eebc-133">Le client ne doit pas recommencer la demande.</span><span class="sxs-lookup"><span data-stu-id="0eebc-133">The client should not retry the request.</span></span>
  * <span data-ttu-id="0eebc-134">Code d'état **5xx** : la demande a entraîné une erreur de serveur interne et/ou un problème temporaire.</span><span class="sxs-lookup"><span data-stu-id="0eebc-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="0eebc-135">Le client doit recommencer la demande.</span><span class="sxs-lookup"><span data-stu-id="0eebc-135">The client should retry the request.</span></span>

<span data-ttu-id="0eebc-136">L'extrait de code suivant est un exemple de la façon d'implémenter un déclencheur d'interrogation.</span><span class="sxs-lookup"><span data-stu-id="0eebc-136">The following code snippet is an example of how to implement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="0eebc-137">Pour tester ce déclencheur d'interrogation, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0eebc-137">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="0eebc-138">Déployez l'application API avec un paramètre d'authentification **anonyme public**.</span><span class="sxs-lookup"><span data-stu-id="0eebc-138">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="0eebc-139">Appelez l'opération **touch** pour toucher un fichier.</span><span class="sxs-lookup"><span data-stu-id="0eebc-139">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="0eebc-140">L'illustration suivante montre un exemple de demande via Postman.</span><span class="sxs-lookup"><span data-stu-id="0eebc-140">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="0eebc-141">![Appeler une opération Touch via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="0eebc-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="0eebc-142">Appelez le déclencheur d'interrogation avec le paramètre **triggerState** défini avec un horodatage antérieur à l'étape 2.</span><span class="sxs-lookup"><span data-stu-id="0eebc-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span></span> <span data-ttu-id="0eebc-143">L'illustration suivante montre un exemple de demande via Postman.</span><span class="sxs-lookup"><span data-stu-id="0eebc-143">The following image shows the sample request via Postman.</span></span>
   <span data-ttu-id="0eebc-144">![Appeler un déclencheur d'interrogation via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="0eebc-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="0eebc-145">Déclencheurs d'émission :</span><span class="sxs-lookup"><span data-stu-id="0eebc-145">Push trigger</span></span>
<span data-ttu-id="0eebc-146">Un déclencheur d'émission est implémenté sous la forme d'une API REST normale, qui envoie des notifications aux clients qui se sont inscrits pour être notifiés quand des événements spécifiques se déclenchent.</span><span class="sxs-lookup"><span data-stu-id="0eebc-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span></span>

<span data-ttu-id="0eebc-147">Les informations suivantes concernant les paquets de demande et de réponse montrent certains aspects essentiels du contrat du déclencheur d'interrogation :</span><span class="sxs-lookup"><span data-stu-id="0eebc-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span></span>

* <span data-ttu-id="0eebc-148">Demande</span><span class="sxs-lookup"><span data-stu-id="0eebc-148">Request</span></span>
  * <span data-ttu-id="0eebc-149">Méthode HTTP : PUT</span><span class="sxs-lookup"><span data-stu-id="0eebc-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="0eebc-150">Paramètres</span><span class="sxs-lookup"><span data-stu-id="0eebc-150">Parameters</span></span>
    * <span data-ttu-id="0eebc-151">triggerId : obligatoire. Chaîne Opaque (comme un GUID) qui représente l'inscription d'un déclencheur d'émission.</span><span class="sxs-lookup"><span data-stu-id="0eebc-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span></span>
    * <span data-ttu-id="0eebc-152">callbackUrl : obligatoire. URL du rappel à appeler quand l'événement se déclenche.</span><span class="sxs-lookup"><span data-stu-id="0eebc-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span></span> <span data-ttu-id="0eebc-153">L'appel est un simple appel HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="0eebc-153">The invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="0eebc-154">Paramètres spécifiques de l'API</span><span class="sxs-lookup"><span data-stu-id="0eebc-154">API-specific parameters</span></span>
* <span data-ttu-id="0eebc-155">Réponse</span><span class="sxs-lookup"><span data-stu-id="0eebc-155">Response</span></span>
  * <span data-ttu-id="0eebc-156">Code d'état **200** : la demande d'inscription du client a réussi.</span><span class="sxs-lookup"><span data-stu-id="0eebc-156">Status code **200** - Request to register client successful.</span></span>
  * <span data-ttu-id="0eebc-157">Code d'état **4xx** : la demande n'est pas valide.</span><span class="sxs-lookup"><span data-stu-id="0eebc-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="0eebc-158">Le client ne doit pas recommencer la demande.</span><span class="sxs-lookup"><span data-stu-id="0eebc-158">The client should not retry the request.</span></span>
  * <span data-ttu-id="0eebc-159">Code d'état **5xx** : la demande a entraîné une erreur de serveur interne et/ou un problème temporaire.</span><span class="sxs-lookup"><span data-stu-id="0eebc-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="0eebc-160">Le client doit recommencer la demande.</span><span class="sxs-lookup"><span data-stu-id="0eebc-160">The client should retry the request.</span></span>
* <span data-ttu-id="0eebc-161">Rappel</span><span class="sxs-lookup"><span data-stu-id="0eebc-161">Callback</span></span>
  * <span data-ttu-id="0eebc-162">Méthode HTTP : POST</span><span class="sxs-lookup"><span data-stu-id="0eebc-162">HTTP method: POST</span></span>
  * <span data-ttu-id="0eebc-163">Corps de la demande : contenu de la notification.</span><span class="sxs-lookup"><span data-stu-id="0eebc-163">Request body: Notification content.</span></span>

<span data-ttu-id="0eebc-164">L'extrait de code suivant est un exemple de la façon d'implémenter un déclencheur d'émission.</span><span class="sxs-lookup"><span data-stu-id="0eebc-164">The following code snippet is an example of how to implement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="0eebc-165">Pour tester ce déclencheur d'interrogation, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0eebc-165">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="0eebc-166">Déployez l'application API avec un paramètre d'authentification **anonyme public**.</span><span class="sxs-lookup"><span data-stu-id="0eebc-166">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="0eebc-167">Accédez à [http://requestb.in/](http://requestb.in/) pour créer un élément RequestBin qui vous servira d'URL de rappel.</span><span class="sxs-lookup"><span data-stu-id="0eebc-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="0eebc-168">Appelez le déclencheur d’émission avec un GUID pour **triggerId** et l’URL de l’élément RequestBin pour **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="0eebc-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="0eebc-169">![Appeler un déclencheur d'émission via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="0eebc-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="0eebc-170">Appelez l'opération **touch** pour toucher un fichier.</span><span class="sxs-lookup"><span data-stu-id="0eebc-170">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="0eebc-171">L'illustration suivante montre un exemple de demande via Postman.</span><span class="sxs-lookup"><span data-stu-id="0eebc-171">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="0eebc-172">![Appeler une opération Touch via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="0eebc-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="0eebc-173">Vérifiez l'élément RequestBin pour confirmer que le rappel du déclencheur d'émission est appelé avec une sortie de propriété.</span><span class="sxs-lookup"><span data-stu-id="0eebc-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="0eebc-174">![Appeler un déclencheur d’interrogation via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="0eebc-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="0eebc-175">Décrire des déclencheurs dans une définition d'API</span><span class="sxs-lookup"><span data-stu-id="0eebc-175">Describe triggers in API definition</span></span>
<span data-ttu-id="0eebc-176">Après avoir implémenté les déclencheurs et déployé votre application API dans Azure, accédez au panneau **Définition d’API** dans le portail Azure en version préliminaire. Vous y voyez que les déclencheurs sont automatiquement reconnus dans l’interface utilisateur, qui repose sur la définition de l’API Swagger 2.0 de l’application API.</span><span class="sxs-lookup"><span data-stu-id="0eebc-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span></span>

![Panneau Définition de l'API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="0eebc-178">Si vous cliquez sur le bouton **Télécharger Swagger** et que vous ouvrez le fichier JSON, vous verrez des résultats similaires à ceci :</span><span class="sxs-lookup"><span data-stu-id="0eebc-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span></span>

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

<span data-ttu-id="0eebc-179">La propriété d'extension **x-ms-schedular-trigger** indique comment les déclencheurs sont décrits dans la définition de l'API, et elle est automatiquement ajoutée à la passerelle d'application API quand vous demandez la définition de l'API via la passerelle, si la demande satisfait à un des critères suivants.</span><span class="sxs-lookup"><span data-stu-id="0eebc-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span></span> <span data-ttu-id="0eebc-180">(Vous pouvez également ajouter cette propriété manuellement.)</span><span class="sxs-lookup"><span data-stu-id="0eebc-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="0eebc-181">Déclencheur d'interrogation :</span><span class="sxs-lookup"><span data-stu-id="0eebc-181">Poll trigger</span></span>
  * <span data-ttu-id="0eebc-182">Si la méthode HTTP est **GET**.</span><span class="sxs-lookup"><span data-stu-id="0eebc-182">If the HTTP method is **GET**.</span></span>
  * <span data-ttu-id="0eebc-183">Si la propriété **operationId** contient la chaîne **trigger**.</span><span class="sxs-lookup"><span data-stu-id="0eebc-183">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="0eebc-184">Si la propriété **parameters** inclut un paramètre avec une propriété **name** définie sur **triggerState**.</span><span class="sxs-lookup"><span data-stu-id="0eebc-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span></span>
* <span data-ttu-id="0eebc-185">Déclencheurs d'émission :</span><span class="sxs-lookup"><span data-stu-id="0eebc-185">Push trigger</span></span>
  * <span data-ttu-id="0eebc-186">Si la méthode HTTP est **PUT**.</span><span class="sxs-lookup"><span data-stu-id="0eebc-186">If the HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="0eebc-187">Si la propriété **operationId** contient la chaîne **trigger**.</span><span class="sxs-lookup"><span data-stu-id="0eebc-187">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="0eebc-188">Si la propriété **parameters** inclut un paramètre avec une propriété **name** définie sur **triggerId**.</span><span class="sxs-lookup"><span data-stu-id="0eebc-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="0eebc-189">Utiliser des déclencheurs d'application API dans les applications logiques</span><span class="sxs-lookup"><span data-stu-id="0eebc-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a><span data-ttu-id="0eebc-190">Répertorier et configurer des déclencheurs d'application API dans le concepteur d'applications logiques</span><span class="sxs-lookup"><span data-stu-id="0eebc-190">List and configure API app triggers in the Logic apps designer</span></span>
<span data-ttu-id="0eebc-191">Si vous créez une application logique dans le même groupe de ressources que l'application API, vous pourrez l'ajouter au canevas du concepteur simplement en cliquant dessus.</span><span class="sxs-lookup"><span data-stu-id="0eebc-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span></span> <span data-ttu-id="0eebc-192">Les images suivantes illustrent ce principe :</span><span class="sxs-lookup"><span data-stu-id="0eebc-192">The following images illustrate this:</span></span>

![Déclencheurs dans le concepteur d'applications logiques](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configurer un déclencheur d'interrogation dans le concepteur d'applications logiques](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configurer un déclencheur d'émission dans le concepteur d'applications logiques](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="0eebc-196">Optimiser les déclencheurs d'application API pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="0eebc-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="0eebc-197">Après avoir ajouté des déclencheurs à une application API, vous pouvez faire un certain nombre de choses pour améliorer l'expérience de l'utilisation de l'application API dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="0eebc-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span></span>

<span data-ttu-id="0eebc-198">Par exemple, le paramètre **triggerState** pour les déclencheurs d'interrogation doit être défini avec l'expression suivante dans l'application logique.</span><span class="sxs-lookup"><span data-stu-id="0eebc-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span></span> <span data-ttu-id="0eebc-199">Cette expression doit évaluer le dernier appel du déclencheur depuis l'application logique et retourner cette valeur.</span><span class="sxs-lookup"><span data-stu-id="0eebc-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="0eebc-200">REMARQUE : pour une explication des fonctions utilisées dans l'expression ci-dessus, reportez-vous à la documentation sur le [Langage de définition des flux de travail des applications logiques](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="0eebc-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="0eebc-201">Les utilisateurs d'applications logiques devraient ainsi fournir l'expression ci-dessus pour le paramètre **triggerState** lors de l'utilisation du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="0eebc-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span></span> <span data-ttu-id="0eebc-202">Il est possible de faire prédéfinir cette valeur par le concepteur d'applications logiques via la propriété d'extension **x-ms-scheduler-recommendation**.</span><span class="sxs-lookup"><span data-stu-id="0eebc-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="0eebc-203">La propriété d'extension **x-ms-visibility** peut être définie avec une valeur *internal* , de façon à ce que le paramètre lui-même ne soit pas affiché sur le concepteur.</span><span class="sxs-lookup"><span data-stu-id="0eebc-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span></span>  <span data-ttu-id="0eebc-204">L'extrait de code suivant montre ceci.</span><span class="sxs-lookup"><span data-stu-id="0eebc-204">The following snippet illustrates that.</span></span>

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

<span data-ttu-id="0eebc-205">Pour les déclencheurs d'émission, le paramètre **triggerId** doit identifier de façon univoque l'application logique.</span><span class="sxs-lookup"><span data-stu-id="0eebc-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span></span> <span data-ttu-id="0eebc-206">Une pratique recommandée consiste à définir cette propriété avec le nom du flux de travail en utilisant l'expression suivante :</span><span class="sxs-lookup"><span data-stu-id="0eebc-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span></span>

    @workflow().name

<span data-ttu-id="0eebc-207">À l’aide des propriétés d’extension **x-ms-scheduler-recommendation** et **x-ms-visibility** dans sa définition d’API, l’application API peut indiquer au concepteur d’applications logiques de définir automatiquement cette expression pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0eebc-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="0eebc-208">Ajouter des propriétés d'extension dans la définition de l'API</span><span class="sxs-lookup"><span data-stu-id="0eebc-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="0eebc-209">Des informations de métadonnées supplémentaires, comme les propriétés d’extension **x-ms-scheduler-recommendation** et **x-ms-visibility**, peuvent être ajoutées dans la définition de l’API de deux façons : statique ou dynamique.</span><span class="sxs-lookup"><span data-stu-id="0eebc-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="0eebc-210">Pour les métadonnées statiques, vous pouvez modifier directement le fichier */metadata/apiDefinition.swagger.json* dans votre projet et y ajouter les propriétés manuellement.</span><span class="sxs-lookup"><span data-stu-id="0eebc-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span></span>

<span data-ttu-id="0eebc-211">Pour les applications API utilisant des métadonnées dynamiques, vous pouvez modifier le fichier SwaggerConfig.cs pour y ajouter un filtre d'opération qui peut ajouter ces extensions.</span><span class="sxs-lookup"><span data-stu-id="0eebc-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="0eebc-212">Voici un exemple de la façon dont cette classe peut être implémentée pour faciliter le scénario des métadonnées dynamiques.</span><span class="sxs-lookup"><span data-stu-id="0eebc-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span></span>

    // Add extension properties on the triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
