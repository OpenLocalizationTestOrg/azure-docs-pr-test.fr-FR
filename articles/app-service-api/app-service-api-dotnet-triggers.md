---
title: "aaaApp API du Service application déclencheurs | Documents Microsoft"
description: "Comment tooimplement déclenche dans une application API dans Azure App Service"
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
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="9a772-103">Déclencheurs des applications API Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9a772-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="9a772-104">Cette version de l’article de hello s’applique la version du schéma tooAPI applications 2014-12-01-preview.</span><span class="sxs-lookup"><span data-stu-id="9a772-104">This version of hello article applies tooAPI apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="9a772-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9a772-105">Overview</span></span>
<span data-ttu-id="9a772-106">Cet article explique comment tooimplement API application déclenche et les consommer à partir d’une application logique.</span><span class="sxs-lookup"><span data-stu-id="9a772-106">This article explains how tooimplement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="9a772-107">Tous les extraits de code hello dans cette rubrique sont copiés à partir de hello [exemple de code d’application d’API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="9a772-107">All of hello code snippets in this topic are copied from hello [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="9a772-108">Notez que vous devez hello toodownload suivant du package nuget pour le code dans cet article de toobuild hello et exécutez : [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="9a772-108">Note that you'll need toodownload hello following nuget package for hello code in this article toobuild and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="9a772-109">Que sont les déclencheurs des applications API ?</span><span class="sxs-lookup"><span data-stu-id="9a772-109">What are API app triggers?</span></span>
<span data-ttu-id="9a772-110">Il est un scénario courant pour un toofire d’application API un événement afin que les clients de l’application d’API hello prendre les mesures appropriées de hello dans l’événement toohello de réponse.</span><span class="sxs-lookup"><span data-stu-id="9a772-110">It's a common scenario for an API app toofire an event so that clients of hello API app can take hello appropriate action in response toohello event.</span></span> <span data-ttu-id="9a772-111">Hello mécanisme d’API REST en fonction qui prend en charge ce scénario est appelé un déclencheur d’application API.</span><span class="sxs-lookup"><span data-stu-id="9a772-111">hello REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="9a772-112">Par exemple, supposons que votre code client à l’aide de hello [application API de connecteur Twitter](../connectors/connectors-create-api-twitter.md) et votre code doit être tooperform une action en fonction de la nouvelle tweets qui contiennent des mots spécifiques.</span><span class="sxs-lookup"><span data-stu-id="9a772-112">For example, let's say your client code is using hello [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs tooperform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="9a772-113">Dans ce cas, vous pouvez configurer un toofacilitate de déclencheur d’interrogation ou de push ce besoin.</span><span class="sxs-lookup"><span data-stu-id="9a772-113">In this case, you might set up a poll or push trigger toofacilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="9a772-114">Déclencheur d'interrogation et déclencheur d'émission</span><span class="sxs-lookup"><span data-stu-id="9a772-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="9a772-115">Deux types de déclencheurs sont actuellement pris en charge :</span><span class="sxs-lookup"><span data-stu-id="9a772-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="9a772-116">Déclencheur d’interrogation - Client interroge application d’API hello pour la notification d’un événement a été déclenché.</span><span class="sxs-lookup"><span data-stu-id="9a772-116">Poll trigger - Client polls hello API app for notification of an event having been fired</span></span>
* <span data-ttu-id="9a772-117">Déclencheur d’émission - Client est averti par application hello API lorsqu’un événement est déclenché</span><span class="sxs-lookup"><span data-stu-id="9a772-117">Push trigger - Client is notified by hello API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="9a772-118">Déclencheur d'interrogation :</span><span class="sxs-lookup"><span data-stu-id="9a772-118">Poll trigger</span></span>
<span data-ttu-id="9a772-119">Un déclencheur de sondage est implémenté comme une API REST régulière et attend son toopoll clients (par exemple, une application logique) dans la commande tooget notification.</span><span class="sxs-lookup"><span data-stu-id="9a772-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) toopoll it in order tooget notification.</span></span> <span data-ttu-id="9a772-120">Pendant que le client de hello peut-être conserver l’état, le déclencheur de sondage de hello lui-même est sans état.</span><span class="sxs-lookup"><span data-stu-id="9a772-120">While hello client may maintain state, hello poll trigger itself is stateless.</span></span>

<span data-ttu-id="9a772-121">Hello informations concernant les paquets de demande et de réponse hello suivantes illustre certains aspects clés de contrat de déclencheur d’interrogation hello :</span><span class="sxs-lookup"><span data-stu-id="9a772-121">hello following information regarding hello request and response packets illustrate some key aspects of hello poll trigger contract:</span></span>

* <span data-ttu-id="9a772-122">Demande</span><span class="sxs-lookup"><span data-stu-id="9a772-122">Request</span></span>
  * <span data-ttu-id="9a772-123">Méthode HTTP : GET</span><span class="sxs-lookup"><span data-stu-id="9a772-123">HTTP method: GET</span></span>
  * <span data-ttu-id="9a772-124">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9a772-124">Parameters</span></span>
    * <span data-ttu-id="9a772-125">triggerState - ce paramètre facultatif permet aux clients toospecify leur état afin que hello déclencheur d’interrogation peut correctement décider si tooreturn notification ou pas selon hello état spécifié.</span><span class="sxs-lookup"><span data-stu-id="9a772-125">triggerState - This optional parameter allows clients toospecify their state so that hello poll trigger can properly decide whether tooreturn notification or not based on hello specified state.</span></span>
    * <span data-ttu-id="9a772-126">Paramètres spécifiques de l'API</span><span class="sxs-lookup"><span data-stu-id="9a772-126">API-specific parameters</span></span>
* <span data-ttu-id="9a772-127">Réponse</span><span class="sxs-lookup"><span data-stu-id="9a772-127">Response</span></span>
  * <span data-ttu-id="9a772-128">Code d’état **200** - demande est valide et qu’il existe une notification de déclencheur de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-128">Status code **200** - Request is valid and there is a notification from hello trigger.</span></span> <span data-ttu-id="9a772-129">le contenu de la notification de hello Hello sera corps de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-129">hello content of hello notification will be hello response body.</span></span> <span data-ttu-id="9a772-130">Un en-tête « Retry-After » dans la réponse de hello indique que les données de notification supplémentaires doivent être récupérées avec un appel de la demande suivante.</span><span class="sxs-lookup"><span data-stu-id="9a772-130">A "Retry-After" header in hello response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="9a772-131">Code d’état **202** - la demande est valide, mais il n’existe aucune nouvelle notification de déclencheur de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-131">Status code **202** - Request is valid, but there is no new notification from hello trigger.</span></span>
  * <span data-ttu-id="9a772-132">Code d'état **4xx** : la demande n'est pas valide.</span><span class="sxs-lookup"><span data-stu-id="9a772-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="9a772-133">client de Hello doit réessayer pas de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-133">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="9a772-134">Code d'état **5xx** : la demande a entraîné une erreur de serveur interne et/ou un problème temporaire.</span><span class="sxs-lookup"><span data-stu-id="9a772-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="9a772-135">client de Hello doit réessayer la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-135">hello client should retry hello request.</span></span>

<span data-ttu-id="9a772-136">Hello suivant extrait de code est un exemple de comment déclencher des tooimplement une interrogation.</span><span class="sxs-lookup"><span data-stu-id="9a772-136">hello following code snippet is an example of how tooimplement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="9a772-137">tootest ce sondage déclencher, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9a772-137">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="9a772-138">Déployer hello API application avec un paramètre d’authentification de **public anonyme**.</span><span class="sxs-lookup"><span data-stu-id="9a772-138">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="9a772-139">Appelez hello **touch** opération tootouch un fichier.</span><span class="sxs-lookup"><span data-stu-id="9a772-139">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="9a772-140">Hello suivant image montre un exemple de demande via Postman.</span><span class="sxs-lookup"><span data-stu-id="9a772-140">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="9a772-141">![Appeler une opération Touch via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="9a772-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="9a772-142">Appeler hello interrogation avec hello **triggerState** paramètre défini tooa temps horodatage préalable tooStep #2.</span><span class="sxs-lookup"><span data-stu-id="9a772-142">Call hello poll trigger with hello **triggerState** parameter set tooa time stamp prior tooStep #2.</span></span> <span data-ttu-id="9a772-143">Hello image suivante illustre demande d’exemple hello via Postman.</span><span class="sxs-lookup"><span data-stu-id="9a772-143">hello following image shows hello sample request via Postman.</span></span>
   <span data-ttu-id="9a772-144">![Appeler un déclencheur d'interrogation via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="9a772-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="9a772-145">Déclencheurs d'émission :</span><span class="sxs-lookup"><span data-stu-id="9a772-145">Push trigger</span></span>
<span data-ttu-id="9a772-146">Un déclencheur d’émission est implémenté comme une réguliers API REST qui exécute un push de tooclients de notifications qui ont inscrit toobe averti lorsque des événements spécifiques se déclenchent.</span><span class="sxs-lookup"><span data-stu-id="9a772-146">A push trigger is implemented as a regular REST API that pushes notifications tooclients who have registered toobe notified when specific events fire.</span></span>

<span data-ttu-id="9a772-147">Hello informations concernant les paquets de demande et de réponse hello suivantes illustre certains aspects clés de contrat de déclencheur hello par émission de données.</span><span class="sxs-lookup"><span data-stu-id="9a772-147">hello following information regarding hello request and response packets illustrate some key aspects of hello push trigger contract.</span></span>

* <span data-ttu-id="9a772-148">Demande</span><span class="sxs-lookup"><span data-stu-id="9a772-148">Request</span></span>
  * <span data-ttu-id="9a772-149">Méthode HTTP : PUT</span><span class="sxs-lookup"><span data-stu-id="9a772-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="9a772-150">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9a772-150">Parameters</span></span>
    * <span data-ttu-id="9a772-151">triggerId : requis - Opaque chaîne (par exemple, un GUID) que représente hello d’inscription d’un déclencheur par émission de données.</span><span class="sxs-lookup"><span data-stu-id="9a772-151">triggerId: required - Opaque string (such as a GUID) that represents hello registration of a push trigger.</span></span>
    * <span data-ttu-id="9a772-152">callbackUrl : requise : URL de hello rappel tooinvoke lors du déclenche de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-152">callbackUrl: required - URL of hello callback tooinvoke when hello event fires.</span></span> <span data-ttu-id="9a772-153">appel de Hello est un simple appel HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="9a772-153">hello invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="9a772-154">Paramètres spécifiques de l'API</span><span class="sxs-lookup"><span data-stu-id="9a772-154">API-specific parameters</span></span>
* <span data-ttu-id="9a772-155">Réponse</span><span class="sxs-lookup"><span data-stu-id="9a772-155">Response</span></span>
  * <span data-ttu-id="9a772-156">Code d’état **200** -client de tooregister demande réussie.</span><span class="sxs-lookup"><span data-stu-id="9a772-156">Status code **200** - Request tooregister client successful.</span></span>
  * <span data-ttu-id="9a772-157">Code d'état **4xx** : la demande n'est pas valide.</span><span class="sxs-lookup"><span data-stu-id="9a772-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="9a772-158">client de Hello doit réessayer pas de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-158">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="9a772-159">Code d'état **5xx** : la demande a entraîné une erreur de serveur interne et/ou un problème temporaire.</span><span class="sxs-lookup"><span data-stu-id="9a772-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="9a772-160">client de Hello doit réessayer la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-160">hello client should retry hello request.</span></span>
* <span data-ttu-id="9a772-161">Rappel</span><span class="sxs-lookup"><span data-stu-id="9a772-161">Callback</span></span>
  * <span data-ttu-id="9a772-162">Méthode HTTP : POST</span><span class="sxs-lookup"><span data-stu-id="9a772-162">HTTP method: POST</span></span>
  * <span data-ttu-id="9a772-163">Corps de la demande : contenu de la notification.</span><span class="sxs-lookup"><span data-stu-id="9a772-163">Request body: Notification content.</span></span>

<span data-ttu-id="9a772-164">Hello suivant extrait de code est un exemple de comment tooimplement push de déclencheur :</span><span class="sxs-lookup"><span data-stu-id="9a772-164">hello following code snippet is an example of how tooimplement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
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
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="9a772-165">tootest ce sondage déclencher, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9a772-165">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="9a772-166">Déployer hello API application avec un paramètre d’authentification de **public anonyme**.</span><span class="sxs-lookup"><span data-stu-id="9a772-166">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="9a772-167">Parcourir trop[http://requestb.in/](http://requestb.in/) toocreate un RequestBin qui servira de votre URL de rappel.</span><span class="sxs-lookup"><span data-stu-id="9a772-167">Browse too[http://requestb.in/](http://requestb.in/) toocreate a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="9a772-168">Appeler le déclencheur d’émission hello avec un GUID en tant que **triggerId** et hello URL RequestBin **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="9a772-168">Call hello push trigger with a GUID as **triggerId** and hello RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="9a772-169">![Appeler un déclencheur d'émission via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="9a772-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="9a772-170">Appelez hello **touch** opération tootouch un fichier.</span><span class="sxs-lookup"><span data-stu-id="9a772-170">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="9a772-171">Hello suivant image montre un exemple de demande via Postman.</span><span class="sxs-lookup"><span data-stu-id="9a772-171">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="9a772-172">![Appeler une opération Touch via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="9a772-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="9a772-173">Vérifiez que hello RequestBin tooconfirm qui hello push déclencheur rappel est appelé avec la sortie de la propriété.</span><span class="sxs-lookup"><span data-stu-id="9a772-173">Check hello RequestBin tooconfirm that hello push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="9a772-174">![Appeler un déclencheur d'interrogation via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="9a772-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="9a772-175">Décrire des déclencheurs dans une définition d'API</span><span class="sxs-lookup"><span data-stu-id="9a772-175">Describe triggers in API definition</span></span>
<span data-ttu-id="9a772-176">Après l’implémentation de déclencheurs de hello et en déployant votre tooAzure d’application API, accédez à toohello **définition d’API** panneau dans le portail Azure en version préliminaire de hello et vous verrez que les déclencheurs sont automatiquement reconnus Bonjour interface utilisateur, qui est déterminée par les Hello définition Swagger 2.0 API de l’application hello API.</span><span class="sxs-lookup"><span data-stu-id="9a772-176">After implementing hello triggers and deploying your API app tooAzure, navigate toohello **API Definition** blade in hello Azure preview portal and you'll see that triggers are automatically recognized in hello UI, which is driven by hello Swagger 2.0 API definition of hello API app.</span></span>

![Panneau Définition de l'API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="9a772-178">Si vous cliquez sur hello **télécharger Swagger** bouton et le fichier JSON de hello ouvert, vous verrez toohello similaire de résultats suivant :</span><span class="sxs-lookup"><span data-stu-id="9a772-178">If you click hello **Download Swagger** button and open hello JSON file, you'll see results similar toohello following:</span></span>

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

<span data-ttu-id="9a772-179">propriété d’extension de Hello **x-ms-programmation-le déclencheur** est la façon dont les déclencheurs sont décrites dans la définition de l’API et est automatiquement ajoutée par la passerelle d’application hello API lorsque vous demandez une définition hello API via une passerelle de hello hello demande tooone de Hello suivant des critères.</span><span class="sxs-lookup"><span data-stu-id="9a772-179">hello extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by hello API app gateway when you request hello API definition via hello gateway if hello request tooone of hello following criteria.</span></span> <span data-ttu-id="9a772-180">(Vous pouvez également ajouter cette propriété manuellement.)</span><span class="sxs-lookup"><span data-stu-id="9a772-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="9a772-181">Déclencheur d'interrogation :</span><span class="sxs-lookup"><span data-stu-id="9a772-181">Poll trigger</span></span>
  * <span data-ttu-id="9a772-182">Si la méthode HTTP de hello est **obtenir**.</span><span class="sxs-lookup"><span data-stu-id="9a772-182">If hello HTTP method is **GET**.</span></span>
  * <span data-ttu-id="9a772-183">Si hello **operationId** propriété contient la chaîne de hello **déclencheur**.</span><span class="sxs-lookup"><span data-stu-id="9a772-183">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="9a772-184">Si hello **paramètres** propriété inclut un paramètre avec un **nom** propriété trop**triggerState**.</span><span class="sxs-lookup"><span data-stu-id="9a772-184">If hello **parameters** property includes a parameter with a **name** property set too**triggerState**.</span></span>
* <span data-ttu-id="9a772-185">Déclencheurs d'émission :</span><span class="sxs-lookup"><span data-stu-id="9a772-185">Push trigger</span></span>
  * <span data-ttu-id="9a772-186">Si la méthode HTTP de hello est **PUT**.</span><span class="sxs-lookup"><span data-stu-id="9a772-186">If hello HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="9a772-187">Si hello **operationId** propriété contient la chaîne de hello **déclencheur**.</span><span class="sxs-lookup"><span data-stu-id="9a772-187">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="9a772-188">Si hello **paramètres** propriété inclut un paramètre avec un **nom** propriété trop**triggerId**.</span><span class="sxs-lookup"><span data-stu-id="9a772-188">If hello **parameters** property includes a parameter with a **name** property set too**triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="9a772-189">Utiliser des déclencheurs d'application API dans les applications logiques</span><span class="sxs-lookup"><span data-stu-id="9a772-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a><span data-ttu-id="9a772-190">Répertorier et configurer des déclencheurs d’application API dans le Concepteur d’applications hello logique</span><span class="sxs-lookup"><span data-stu-id="9a772-190">List and configure API app triggers in hello Logic apps designer</span></span>
<span data-ttu-id="9a772-191">Si vous créez une application logique Bonjour même groupe de ressources que hello application API, vous serez en mesure de tooadd il canevas de concepteur toohello simplement en cliquant dessus.</span><span class="sxs-lookup"><span data-stu-id="9a772-191">If you create a Logic app in hello same resource group as hello API app, you will be able tooadd it toohello designer canvas simply by clicking it.</span></span> <span data-ttu-id="9a772-192">Hello suivant des images pour illustrer ce propos :</span><span class="sxs-lookup"><span data-stu-id="9a772-192">hello following images illustrate this:</span></span>

![Déclencheurs dans le concepteur d'applications logiques](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configurer un déclencheur d'interrogation dans le concepteur d'applications logiques](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configurer un déclencheur d'émission dans le concepteur d'applications logiques](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="9a772-196">Optimiser les déclencheurs d'application API pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="9a772-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="9a772-197">Après avoir ajouté des déclencheurs tooan API app, il existe quelques opérations réalisables expérience de hello tooimprove lors de l’utilisation d’application hello API dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="9a772-197">After you add triggers tooan API app, there are a few things you can do tooimprove hello experience when using hello API app in a Logic app.</span></span>

<span data-ttu-id="9a772-198">Par exemple, hello **triggerState** pour les déclencheurs d’interrogation doit être défini toohello expression dans l’application logique de hello suivante.</span><span class="sxs-lookup"><span data-stu-id="9a772-198">For instance, hello **triggerState** parameter for poll triggers should be set toohello following expression in hello Logic app.</span></span> <span data-ttu-id="9a772-199">Cette expression doit évaluer hello dernière invocation du déclencheur hello à partir de l’application logique de hello et retourne cette valeur.</span><span class="sxs-lookup"><span data-stu-id="9a772-199">This expression should evaluate hello last invocation of hello trigger from hello Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="9a772-200">Remarque : Pour obtenir une explication des fonctions hello utilisé dans l’expression hello ci-dessus, consultez la documentation du toohello sur [langage de définition de flux de travail logique d’application](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="9a772-200">NOTE: For an explanation of hello functions used in hello expression above, refer toohello documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="9a772-201">Expression de hello tooprovide au-dessus de l’utilisateur d’application logique a besoin pour hello **triggerState** paramètre lors de l’utilisation de déclencheur de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-201">Logic app users would need tooprovide hello expression above for hello **triggerState** parameter while using hello trigger.</span></span> <span data-ttu-id="9a772-202">Il est possible de toohave cette valeur prédéfinie par le Concepteur d’application hello logique via la propriété d’extension hello **x-ms-planificateur-recommandation**.</span><span class="sxs-lookup"><span data-stu-id="9a772-202">It is possible toohave this value preset by hello Logic app designer through hello extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="9a772-203">Hello **x-ms-visibilité** propriété d’extension peut être valeur tooa *interne* afin que le paramètre hello lui-même n’est pas visible sur le Concepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-203">hello **x-ms-visibility** extension property can be set tooa value of *internal* so that hello parameter itself is not shown on hello designer.</span></span>  <span data-ttu-id="9a772-204">Hello suivant extrait de code illustre.</span><span class="sxs-lookup"><span data-stu-id="9a772-204">hello following snippet illustrates that.</span></span>

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

<span data-ttu-id="9a772-205">Pour les déclencheurs de push, hello **triggerId** paramètre doit identifier de façon unique application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-205">For push triggers, hello **triggerId** parameter must uniquely identify hello Logic app.</span></span> <span data-ttu-id="9a772-206">Meilleure pratique recommandée est tooset ce nom toohello de propriété de flux de travail hello à l’aide de hello l’expression suivante :</span><span class="sxs-lookup"><span data-stu-id="9a772-206">A recommended best practice is tooset this property toohello name of hello workflow by using hello following expression:</span></span>

    @workflow().name

<span data-ttu-id="9a772-207">À l’aide de hello **x-ms-planificateur-recommandation** et **x-ms-visibilité** propriétés d’extension dans sa définition d’API, hello application API peuvent transmettre toohello logique application concepteur tooautomatically définie expression pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-207">Using hello **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, hello API app can convey toohello Logic app designer tooautomatically set this expression for hello user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="9a772-208">Ajouter des propriétés d'extension dans la définition de l'API</span><span class="sxs-lookup"><span data-stu-id="9a772-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="9a772-209">Informations de métadonnées supplémentaires telles que les propriétés d’extension hello - **x-ms-planificateur-recommandation** et **x-ms-visibilité** -peuvent être ajoutées dans la définition de hello API dans un des deux façons : statique ou dynamique.</span><span class="sxs-lookup"><span data-stu-id="9a772-209">Additional metadata information - such as hello extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in hello API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="9a772-210">Pour les métadonnées statiques, vous pouvez modifier directement hello */metadata/apiDefinition.swagger.json* dans votre projet et ajouter manuellement les propriétés de hello.</span><span class="sxs-lookup"><span data-stu-id="9a772-210">For static metadata, you can directly edit hello */metadata/apiDefinition.swagger.json* file in your project and add hello properties manually.</span></span>

<span data-ttu-id="9a772-211">Pour les applications API en utilisant les métadonnées dynamique, vous pouvez modifier hello SwaggerConfig.cs fichier tooadd un filtre d’opération qui peut ajouter ces extensions.</span><span class="sxs-lookup"><span data-stu-id="9a772-211">For API apps using dynamic metadata, you can edit hello SwaggerConfig.cs file tooadd an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="9a772-212">Hello Voici un exemple de la manière dont cette classe peut être scénario de métadonnées dynamique hello toofacilitate implémenté.</span><span class="sxs-lookup"><span data-stu-id="9a772-212">hello following is an example of how this class can be implemented toofacilitate hello dynamic metadata scenario.</span></span>

    // Add extension properties on hello triggerState parameter
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
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
