---
title: "les files d’attente d’aaaHow toouse Service Bus dans Node.js | Documents Microsoft"
description: "Découvrez comment toouse Service Bus des files d’attente dans Azure à partir d’une application Node.js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a><span data-ttu-id="a78a6-103">Comment toouse Service Bus de files d’attente avec Node.js</span><span class="sxs-lookup"><span data-stu-id="a78a6-103">How toouse Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="a78a6-104">Cet article décrit comment toouse Service Bus de files d’attente avec Node.js.</span><span class="sxs-lookup"><span data-stu-id="a78a6-104">This article describes how toouse Service Bus queues with Node.js.</span></span> <span data-ttu-id="a78a6-105">exemples de Hello sont écrites en JavaScript et utilisent hello module Node.js Azure.</span><span class="sxs-lookup"><span data-stu-id="a78a6-105">hello samples are written in JavaScript and use hello Node.js Azure module.</span></span> <span data-ttu-id="a78a6-106">Hello scénarios abordés incluent **création de files d’attente**, **envoyer et recevoir des messages**, et **la suppression de files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="a78a6-106">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="a78a6-107">Pour plus d’informations sur les files d’attente, consultez hello [étapes](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="a78a6-107">For more information on queues, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="a78a6-108">Création d’une application Node.js</span><span class="sxs-lookup"><span data-stu-id="a78a6-108">Create a Node.js application</span></span>
<span data-ttu-id="a78a6-109">Créez une application Node.js vide.</span><span class="sxs-lookup"><span data-stu-id="a78a6-109">Create a blank Node.js application.</span></span> <span data-ttu-id="a78a6-110">Pour obtenir des instructions sur la façon de toocreate une application Node.js, consultez [créer et déployer un tooan d’application Node.js site Web Azure][Create and deploy a Node.js application tooan Azure Website], ou [Service de cloud computing Node.js] [ Node.js Cloud Service] à l’aide de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a78a6-110">For instructions on how toocreate a Node.js application, see [Create and deploy a Node.js application tooan Azure Website][Create and deploy a Node.js application tooan Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="a78a6-111">Configurer votre toouse application Service Bus</span><span class="sxs-lookup"><span data-stu-id="a78a6-111">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="a78a6-112">toouse Azure Service Bus, téléchargez et utilisez hello package Node.js Azure.</span><span class="sxs-lookup"><span data-stu-id="a78a6-112">toouse Azure Service Bus, download and use hello Node.js Azure package.</span></span> <span data-ttu-id="a78a6-113">Ce package comprend un ensemble de bibliothèques qui communiquent avec les services de Service Bus REST hello.</span><span class="sxs-lookup"><span data-stu-id="a78a6-113">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="a78a6-114">Utiliser le Gestionnaire de Package de nœud (NPM) tooobtain hello package</span><span class="sxs-lookup"><span data-stu-id="a78a6-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="a78a6-115">Hello d’utilisation **Windows PowerShell pour Node.js** commande fenêtre toonavigate toohello **c:\\nœud\\sbqueues\\WebRole1** dossier dans lequel vous avez créé votre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="a78a6-115">Use hello **Windows PowerShell for Node.js** command window toonavigate toohello **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="a78a6-116">Type **npm installer azure** dans la fenêtre de commande hello, qui doivent entraîner suivant toohello similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="a78a6-116">Type **npm install azure** in hello command window, which should result in output similar toohello following:</span></span>

    ```
    azure@0.7.5 node_modules\azure
        ├── dateformat@1.0.2-1.2.3
        ├── xmlbuilder@0.4.2
        ├── node-uuid@1.2.0
        ├── mime@1.2.9
        ├── underscore@1.4.4
        ├── validator@1.1.1
        ├── tunnel@0.0.2
        ├── wns@0.5.3
        ├── xml2js@0.2.7 (sax@0.5.2)
        └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
    ```
3. <span data-ttu-id="a78a6-117">Vous pouvez exécuter manuellement hello **ls** tooverify de commande qui un **node_modules** dossier a été créé.</span><span class="sxs-lookup"><span data-stu-id="a78a6-117">You can manually run hello **ls** command tooverify that a **node_modules** folder was created.</span></span> <span data-ttu-id="a78a6-118">À l’intérieur de ce hello de recherche du dossier **azure** package qui contient les bibliothèques hello vous devez tooaccess files d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a78a6-118">Inside that folder find hello **azure** package, which contains hello libraries you need tooaccess Service Bus queues.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="a78a6-119">Module d’importation hello</span><span class="sxs-lookup"><span data-stu-id="a78a6-119">Import hello module</span></span>
<span data-ttu-id="a78a6-120">Utilisez le bloc-notes ou un autre éditeur de texte, ajoutez hello suivant en haut de toohello de hello **server.js** fichier de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="a78a6-120">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="a78a6-121">Configuration d’une connexion Service Bus Azure</span><span class="sxs-lookup"><span data-stu-id="a78a6-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="a78a6-122">module Windows Azure Hello lit variable d’environnement hello `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain informations requis tooconnect tooService Bus.</span><span class="sxs-lookup"><span data-stu-id="a78a6-122">hello Azure module reads hello environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain information required tooconnect tooService Bus.</span></span> <span data-ttu-id="a78a6-123">Si cette variable d’environnement n’est pas définie, vous devez spécifier les informations de compte hello lors de l’appel `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="a78a6-123">If this environment variable is not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="a78a6-124">Pour obtenir un exemple de la configuration des variables d’environnement hello dans un fichier de configuration pour un Service Cloud Azure, consultez [Service de Cloud Node.js avec stockage][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="a78a6-124">For an example of setting hello environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="a78a6-125">Pour obtenir un exemple de la définition de variables d’environnement hello Bonjour [portail Azure] [ Azure portal] pour un site Web Azure, consultez [Node.js d’Application Web avec stockage] [ Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="a78a6-125">For an example of setting hello environment variables in hello [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="a78a6-126">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="a78a6-126">Create a queue</span></span>
<span data-ttu-id="a78a6-127">Hello **ServiceBusService** objet vous permet de toowork avec les files d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a78a6-127">hello **ServiceBusService** object enables you toowork with Service Bus queues.</span></span> <span data-ttu-id="a78a6-128">Hello de code suivant crée un **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="a78a6-128">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="a78a6-129">Ajoutez-le haut hello Hello **server.js** fichier, après hello de tooimport hello instruction module Windows Azure :</span><span class="sxs-lookup"><span data-stu-id="a78a6-129">Add it near hello top of hello **server.js** file, after hello statement tooimport hello Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="a78a6-130">En appelant `createQueueIfNotExists` sur hello **ServiceBusService** objet, hello spécifié de file d’attente est retourné (si elle existe) ou une file d’attente avec le nom spécifié de hello est créé.</span><span class="sxs-lookup"><span data-stu-id="a78a6-130">By calling `createQueueIfNotExists` on hello **ServiceBusService** object, hello specified queue is returned (if it exists), or a new queue with hello specified name is created.</span></span> <span data-ttu-id="a78a6-131">code Hello suivant utilise `createQueueIfNotExists` toocreate ou connectez-vous de file d’attente toohello nommée `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="a78a6-131">hello following code uses `createQueueIfNotExists` toocreate or connect toohello queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="a78a6-132">Hello `createServiceBusService` méthode prend également en charge des options supplémentaires, qui permettent de paramètres de file d’attente par défaut toooverride comme taille de file d’attente toolive ou une valeur maximale de temps de message.</span><span class="sxs-lookup"><span data-stu-id="a78a6-132">hello `createServiceBusService` method also supports additional options, which enable you toooverride default queue settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="a78a6-133">Hello exemple suivant définit hello file d’attente maximale taille too5 Go et heure toolive (TTL) de 1 minute :</span><span class="sxs-lookup"><span data-stu-id="a78a6-133">hello following example sets hello maximum queue size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="a78a6-134">Filtres</span><span class="sxs-lookup"><span data-stu-id="a78a6-134">Filters</span></span>
<span data-ttu-id="a78a6-135">Les opérations de filtrage facultatif peuvent être appliquées toooperations effectuées à l’aide **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="a78a6-135">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="a78a6-136">Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature de hello :</span><span class="sxs-lookup"><span data-stu-id="a78a6-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="a78a6-137">Après son traitement préalable sur les options de demande hello, méthode hello doit appeler `next`, en passant un rappel avec hello après signature :</span><span class="sxs-lookup"><span data-stu-id="a78a6-137">After doing its pre-processing on hello request options, hello method must call `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="a78a6-138">Dans ce rappel et après traitement hello `returnObject` (hello réponse hello demande toohello serveur), le rappel de hello doit appeler `next` si elle existe toocontinue le traitement des autres filtres, ou simplement appeler `finalCallback`, qui se termine à appel de service Hello.</span><span class="sxs-lookup"><span data-stu-id="a78a6-138">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback must either invoke `next` if it exists toocontinue processing other filters, or simply invoke `finalCallback`, which ends hello service invocation.</span></span>

<span data-ttu-id="a78a6-139">Deux filtres qui implémentent la logique de nouvelle tentative sont incluses avec hello Azure SDK pour Node.js, `ExponentialRetryPolicyFilter` et `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="a78a6-139">Two filters that implement retry logic are included with hello Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="a78a6-140">Hello de code suivant crée un `ServiceBusService` objet qui utilise hello `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="a78a6-140">hello following code creates a `ServiceBusService` object that uses hello `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="a78a6-141">Envoyer la file d’attente de messages tooa</span><span class="sxs-lookup"><span data-stu-id="a78a6-141">Send messages tooa queue</span></span>
<span data-ttu-id="a78a6-142">toosend une file d’attente Service Bus de messages tooa, votre application appelle hello `sendQueueMessage` méthode sur hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="a78a6-142">toosend a message tooa Service Bus queue, your application calls hello `sendQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="a78a6-143">Trop envoyée (et reçues à partir de) Service Bus sont des files d’attente de messages **BrokeredMessage** , et qu’un ensemble de propriétés standard (tels que **étiquette** et **TimeToLive**), un dictionnaire qui est utilisé toohold des propriétés personnalisées spécifiques à l’application et un corps de données d’application arbitraire.</span><span class="sxs-lookup"><span data-stu-id="a78a6-143">Messages sent too(and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="a78a6-144">Une application peut définir le corps de hello du message de type hello en passant une chaîne en tant que message de type hello.</span><span class="sxs-lookup"><span data-stu-id="a78a6-144">An application can set hello body of hello message by passing a string as hello message.</span></span> <span data-ttu-id="a78a6-145">Toutes les propriétés standard requises sont remplies avec les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="a78a6-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="a78a6-146">Hello exemple suivant montre comment toosend une file d’attente toohello test nommé `myqueue` à l’aide de `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="a78a6-146">hello following example demonstrates how toosend a test message toohello queue named `myqueue` using `sendQueueMessage`:</span></span>

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

<span data-ttu-id="a78a6-147">Les files d’attente Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="a78a6-147">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="a78a6-148">en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="a78a6-148">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="a78a6-149">Il n’existe aucune limite du nombre de hello de messages dans une file d’attente mais hello de taille totale des messages hello détenus par une file d’attente est une extrémité de fin.</span><span class="sxs-lookup"><span data-stu-id="a78a6-149">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="a78a6-150">Cette taille de file d'attente est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="a78a6-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="a78a6-151">Pour plus d’informations sur les quotas, consultez [Quotas Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="a78a6-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="a78a6-152">Réception des messages d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="a78a6-152">Receive messages from a queue</span></span>
<span data-ttu-id="a78a6-153">Les messages sont reçus à partir d’une file d’attente à l’aide de hello `receiveQueueMessage` méthode sur hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="a78a6-153">Messages are received from a queue using hello `receiveQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="a78a6-154">Par défaut, les messages sont supprimés de la file d’attente hello lorsqu’elles sont lues ; Toutefois, vous pouvez lire (aperçu) et verrouiller le message de type hello sans le supprimer de la file d’attente hello en définissant le paramètre facultatif hello `isPeekLock` trop**true**.</span><span class="sxs-lookup"><span data-stu-id="a78a6-154">By default, messages are deleted from hello queue as they are read; however, you can read (peek) and lock hello message without deleting it from hello queue by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="a78a6-155">Hello le comportement par défaut de la lecture et de suppression de message de type hello comme partie de hello opération de réception est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec.</span><span class="sxs-lookup"><span data-stu-id="a78a6-155">hello default behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="a78a6-156">toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter.</span><span class="sxs-lookup"><span data-stu-id="a78a6-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="a78a6-157">Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.</span><span class="sxs-lookup"><span data-stu-id="a78a6-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="a78a6-158">Si hello `isPeekLock` paramètre est défini trop**true**, hello réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants.</span><span class="sxs-lookup"><span data-stu-id="a78a6-158">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="a78a6-159">Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="a78a6-159">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="a78a6-160">Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant `deleteMessage` (méthode) et en fournissant des toobe de message hello supprimé en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="a78a6-160">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `deleteMessage` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="a78a6-161">Hello `deleteMessage` méthode marque le message de type hello comme ayant été consommé et supprime celui-ci de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="a78a6-161">hello `deleteMessage` method marks hello message as being consumed and removes it from hello queue.</span></span>

<span data-ttu-id="a78a6-162">Hello exemple suivant montre comment tooreceive et processus de messages à l’aide de `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="a78a6-162">hello following example demonstrates how tooreceive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="a78a6-163">Hello exemple reçoit d’abord et supprime un message, puis reçoit un message à l’aide de `isPeekLock` défini trop**true**, puis supprime hello à l’aide du message `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="a78a6-163">hello example first receives and deletes a message, and then receives a message using `isPeekLock` set too**true**, then deletes hello message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="a78a6-164">Comment toohandle application tombe en panne et messages illisibles</span><span class="sxs-lookup"><span data-stu-id="a78a6-164">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="a78a6-165">Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message.</span><span class="sxs-lookup"><span data-stu-id="a78a6-165">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="a78a6-166">Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlockMessage` méthode sur hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="a78a6-166">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="a78a6-167">Cette opération provoquent Service Bus toounlock le message dans la file d’attente hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.</span><span class="sxs-lookup"><span data-stu-id="a78a6-167">This will cause Service Bus toounlock the message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="a78a6-168">Il existe également un délai d’attente d’un message verrouillé dans la file d’attente hello, et si l’échec de l’application hello tooprocess hello message avant hello délai d’attente de verrou expire (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.</span><span class="sxs-lookup"><span data-stu-id="a78a6-168">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="a78a6-169">Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `deleteMessage` méthode est appelée, puis le message de type hello sera redistribué toohello application lors de son redémarrage.</span><span class="sxs-lookup"><span data-stu-id="a78a6-169">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="a78a6-170">Cela est souvent appelé *au moins une fois le traitement*, autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué.</span><span class="sxs-lookup"><span data-stu-id="a78a6-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="a78a6-171">Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message.</span><span class="sxs-lookup"><span data-stu-id="a78a6-171">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="a78a6-172">Cela est souvent obtenue à l’aide de hello **MessageId** propriété de message de type hello, qui reste constante entre les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="a78a6-172">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a78a6-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a78a6-173">Next steps</span></span>
<span data-ttu-id="a78a6-174">toolearn en savoir plus sur les files d’attente, consultez hello suivant des ressources.</span><span class="sxs-lookup"><span data-stu-id="a78a6-174">toolearn more about queues, see hello following resources.</span></span>

* <span data-ttu-id="a78a6-175">[Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="a78a6-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="a78a6-176">Référentiel du [Kit de développement logiciel (SDK) Azure pour Node][Azure SDK for Node] sur GitHub</span><span class="sxs-lookup"><span data-stu-id="a78a6-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="a78a6-177">Centre pour développeurs Node.js</span><span class="sxs-lookup"><span data-stu-id="a78a6-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
