---
title: "Utilisation des files d’attente Service Bus dans Node.js | Microsoft Docs"
description: "Découvrez comment utiliser les files d’attente Service Bus dans Azure à partir d’une application Node.js."
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
ms.openlocfilehash: fe2c02534996d99c190593a419a4823888f03d31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-nodejs"></a><span data-ttu-id="4962f-103">Utilisation des files d’attente Service Bus avec Node.js</span><span class="sxs-lookup"><span data-stu-id="4962f-103">How to use Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="4962f-104">Cet article décrit l’utilisation des files d’attente Service Bus avec Node.js.</span><span class="sxs-lookup"><span data-stu-id="4962f-104">This article describes how to use Service Bus queues with Node.js.</span></span> <span data-ttu-id="4962f-105">Les exemples sont écrits en JavaScript et utilisent le module Azure Node.js.</span><span class="sxs-lookup"><span data-stu-id="4962f-105">The samples are written in JavaScript and use the Node.js Azure module.</span></span> <span data-ttu-id="4962f-106">Les scénarios couverts dans ce guide sont les suivants : **création de files d’attente**, **envoi et réception de messages** et **suppression de files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="4962f-106">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="4962f-107">Pour plus d’informations sur les files d’attente, consultez la section [Étapes suivantes](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="4962f-107">For more information on queues, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="4962f-108">Création d’une application Node.js</span><span class="sxs-lookup"><span data-stu-id="4962f-108">Create a Node.js application</span></span>
<span data-ttu-id="4962f-109">Créez une application Node.js vide.</span><span class="sxs-lookup"><span data-stu-id="4962f-109">Create a blank Node.js application.</span></span> <span data-ttu-id="4962f-110">Pour obtenir des instructions sur la création d’une application Node.js, voir les pages [Création et déploiement d’une application Node.js sur un site web Azure][Create and deploy a Node.js application to an Azure Website] ou [Service cloud Node.js avec Windows PowerShell][Node.js Cloud Service].</span><span class="sxs-lookup"><span data-stu-id="4962f-110">For instructions on how to create a Node.js application, see [Create and deploy a Node.js application to an Azure Website][Create and deploy a Node.js application to an Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="4962f-111">Configuration de votre application pour l’utilisation de Service Bus</span><span class="sxs-lookup"><span data-stu-id="4962f-111">Configure your application to use Service Bus</span></span>
<span data-ttu-id="4962f-112">Pour utiliser Azure Service Bus, téléchargez et utilisez le package Azure Node.js.</span><span class="sxs-lookup"><span data-stu-id="4962f-112">To use Azure Service Bus, download and use the Node.js Azure package.</span></span> <span data-ttu-id="4962f-113">Ce dernier inclut des bibliothèques permettant de communiquer avec les services REST de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4962f-113">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="4962f-114">Utilisation de Node Package Manager (NPM) pour obtenir le package</span><span class="sxs-lookup"><span data-stu-id="4962f-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="4962f-115">Utilisez la fenêtre de commande **Windows PowerShell for Node.js** pour accéder au dossier **c:\\node\\sbqueues\\WebRole1** dans lequel vous avez créé votre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="4962f-115">Use the **Windows PowerShell for Node.js** command window to navigate to the **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="4962f-116">Tapez **npm install azure** dans la fenêtre de commande, ce qui génère un résultat similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="4962f-116">Type **npm install azure** in the command window, which should result in output similar to the following:</span></span>

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
3. <span data-ttu-id="4962f-117">Vous pouvez exécuter manuellement la commande **ls** pour vérifier que le dossier **node_modules** a été créé.</span><span class="sxs-lookup"><span data-stu-id="4962f-117">You can manually run the **ls** command to verify that a **node_modules** folder was created.</span></span> <span data-ttu-id="4962f-118">Dans ce dossier, recherchez le package **azure**, qui contient les bibliothèques nécessaires pour accéder aux files d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4962f-118">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus queues.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="4962f-119">Importation du module</span><span class="sxs-lookup"><span data-stu-id="4962f-119">Import the module</span></span>
<span data-ttu-id="4962f-120">À l’aide d’un éditeur de texte, comme le Bloc-notes, ajoutez la commande suivante au début du fichier **server.js** de l’application :</span><span class="sxs-lookup"><span data-stu-id="4962f-120">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="4962f-121">Configuration d’une connexion Service Bus Azure</span><span class="sxs-lookup"><span data-stu-id="4962f-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="4962f-122">Le module Azure lit la variable d’environnement `AZURE_SERVICEBUS_CONNECTION_STRING` pour obtenir les informations nécessaires pour se connecter à Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4962f-122">The Azure module reads the environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` to obtain information required to connect to Service Bus.</span></span> <span data-ttu-id="4962f-123">Si cette variable d’environnement n’est pas définie, vous devez spécifier les informations de compte lors de l’appel de `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="4962f-123">If this environment variable is not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="4962f-124">Pour consulter un exemple de paramétrage de variables d’environnement dans un fichier de configuration pour un service cloud Azure, consultez [Service cloud Node.js avec stockage][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="4962f-124">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="4962f-125">Pour un exemple de configuration des variables d’environnement dans le [portail Azure][Azure portal] pour un site web Azure, consultez [Application web Node.js avec stockage][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="4962f-125">For an example of setting the environment variables in the [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="4962f-126">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="4962f-126">Create a queue</span></span>
<span data-ttu-id="4962f-127">L’objet **ServiceBusService** permet d’utiliser des files d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4962f-127">The **ServiceBusService** object enables you to work with Service Bus queues.</span></span> <span data-ttu-id="4962f-128">Le code suivant crée un objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="4962f-128">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="4962f-129">Ajoutez-le vers le début du fichier **server.js**, après l’instruction relative à l’importation du module Azure :</span><span class="sxs-lookup"><span data-stu-id="4962f-129">Add it near the top of the **server.js** file, after the statement to import the Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="4962f-130">En appelant `createQueueIfNotExists` sur l’objet **ServiceBusService**, la file d’attente spécifiée est renvoyée (si elle existe) ou une file d’attente comportant le nom spécifié est créée.</span><span class="sxs-lookup"><span data-stu-id="4962f-130">By calling `createQueueIfNotExists` on the **ServiceBusService** object, the specified queue is returned (if it exists), or a new queue with the specified name is created.</span></span> <span data-ttu-id="4962f-131">Le code suivant utilise `createQueueIfNotExists` pour créer la file d’attente nommée `myqueue` ou s’y connecter :</span><span class="sxs-lookup"><span data-stu-id="4962f-131">The following code uses `createQueueIfNotExists` to create or connect to the queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="4962f-132">La méthode `createServiceBusService` prend également en charge des options supplémentaires, qui vous permettent de remplacer les paramètres de file d’attente par défaut comme la durée de vie du message ou la taille maximale de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="4962f-132">The `createServiceBusService` method also supports additional options, which enable you to override default queue settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="4962f-133">L’exemple suivant définit la taille maximale de la file d’attente sur 5 Go et la durée de vie de message sur 1 minute :</span><span class="sxs-lookup"><span data-stu-id="4962f-133">The following example sets the maximum queue size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="4962f-134">Filtres</span><span class="sxs-lookup"><span data-stu-id="4962f-134">Filters</span></span>
<span data-ttu-id="4962f-135">Des opérations facultatives de filtrage peuvent être appliquées aux opérations exécutées par le biais de **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="4962f-135">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="4962f-136">Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature :</span><span class="sxs-lookup"><span data-stu-id="4962f-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="4962f-137">Après le prétraitement des options de la requête, la méthode doit appeler `next` en passant un rappel avec la signature suivante :</span><span class="sxs-lookup"><span data-stu-id="4962f-137">After doing its pre-processing on the request options, the method must call `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="4962f-138">Dans ce rappel, et après le traitement de `returnObject` (la réponse à la requête du serveur), le rappel doit appeler `next`, s’il existe, pour continuer à traiter d’autres filtres, ou appeler `finalCallback` pour terminer l’appel du service.</span><span class="sxs-lookup"><span data-stu-id="4962f-138">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback must either invoke `next` if it exists to continue processing other filters, or simply invoke `finalCallback`, which ends the service invocation.</span></span>

<span data-ttu-id="4962f-139">Deux filtres, `ExponentialRetryPolicyFilter` et `LinearRetryPolicyFilter`, implémentant une logique de nouvelle tentative sont inclus avec le kit de développement logiciel (SDK) Azure pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="4962f-139">Two filters that implement retry logic are included with the Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="4962f-140">Le code suivant permet de créer un objet `ServiceBusService` utilisant `ExponentialRetryPolicyFilter` :</span><span class="sxs-lookup"><span data-stu-id="4962f-140">The following code creates a `ServiceBusService` object that uses the `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="4962f-141">Envoi de messages à une file d'attente</span><span class="sxs-lookup"><span data-stu-id="4962f-141">Send messages to a queue</span></span>
<span data-ttu-id="4962f-142">Pour envoyer un message à une file d’attente Service Bus, votre application appelle la méthode `sendQueueMessage` sur l’objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="4962f-142">To send a message to a Service Bus queue, your application calls the `sendQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="4962f-143">Les messages envoyés aux files d’attente Service Bus (et reçus de celles-ci) sont les objets **BrokeredMessage**. Ils possèdent un ensemble de propriétés standard (telles que **Label** et **TimeToLive**), un dictionnaire servant à conserver les propriétés personnalisées propres à une application, ainsi qu’un corps de données d’application arbitraires.</span><span class="sxs-lookup"><span data-stu-id="4962f-143">Messages sent to (and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="4962f-144">Une application peut définir le corps du message en passant une chaîne comme message.</span><span class="sxs-lookup"><span data-stu-id="4962f-144">An application can set the body of the message by passing a string as the message.</span></span> <span data-ttu-id="4962f-145">Toutes les propriétés standard requises sont remplies avec les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="4962f-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="4962f-146">L’exemple suivant indique comment envoyer un message test à la file d’attente nommée `myqueue` au moyen de la méthode `sendQueueMessage` :</span><span class="sxs-lookup"><span data-stu-id="4962f-146">The following example demonstrates how to send a test message to the queue named `myqueue` using `sendQueueMessage`:</span></span>

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

<span data-ttu-id="4962f-147">Les files d’attente Service Bus prennent en charge une taille de message maximale de 256 Ko dans le [niveau Standard](service-bus-premium-messaging.md) et d’1 Mo dans le [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="4962f-147">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="4962f-148">L’en-tête, qui comprend les propriétés d’application standard et personnalisées, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="4962f-148">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="4962f-149">Si une file d'attente n'est pas limitée par le nombre de messages qu'elle peut contenir, elle l'est en revanche par la taille totale des messages qu'elle contient.</span><span class="sxs-lookup"><span data-stu-id="4962f-149">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="4962f-150">Cette taille de file d'attente est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="4962f-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="4962f-151">Pour plus d’informations sur les quotas, consultez [Quotas Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="4962f-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="4962f-152">Réception des messages d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="4962f-152">Receive messages from a queue</span></span>
<span data-ttu-id="4962f-153">La méthode `receiveQueueMessage` de l’objet **ServiceBusService** permet de recevoir les messages d’une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="4962f-153">Messages are received from a queue using the `receiveQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="4962f-154">Par défaut, les messages sont supprimés de la file d’attente au fur et à mesure de leur lecture. Cependant, vous pouvez lire et verrouiller le message sans le supprimer de la file d’attente en définissant le paramètre facultatif `isPeekLock` sur **true**.</span><span class="sxs-lookup"><span data-stu-id="4962f-154">By default, messages are deleted from the queue as they are read; however, you can read (peek) and lock the message without deleting it from the queue by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="4962f-155">Le comportement par défaut de lecture et de suppression du message dans le cadre de l’opération de réception est le modèle le plus simple et le mieux adapté aux scénarios dans lesquels une application est capable de tolérer le non-traitement d’un message en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="4962f-155">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="4962f-156">Pour mieux comprendre, imaginez un scénario dans lequel le consommateur émet la demande de réception et subit un incident avant de la traiter.</span><span class="sxs-lookup"><span data-stu-id="4962f-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="4962f-157">Comme Service Bus a marqué le message comme étant consommé, lorsque l’application redémarre et recommence à consommer des messages, elle manque le message consommé avant l’incident.</span><span class="sxs-lookup"><span data-stu-id="4962f-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="4962f-158">Si le paramètre `isPeekLock` est défini sur **true**, la réception devient une opération en deux étapes, qui autorise une prise en charge des applications qui ne peuvent pas tolérer les messages manquants.</span><span class="sxs-lookup"><span data-stu-id="4962f-158">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="4962f-159">Lorsque Service Bus reçoit une demande, il recherche le prochain message à consommer, le verrouille pour empêcher d'autres consommateurs de le recevoir, puis le renvoie à l'application.</span><span class="sxs-lookup"><span data-stu-id="4962f-159">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="4962f-160">Dès lors que l’application a terminé le traitement du message (ou qu’elle l’a stocké de manière fiable pour un traitement ultérieur), elle accomplit la deuxième étape du processus de réception en appelant la méthode `deleteMessage` et en fournissant le message à supprimer sous la forme d’un paramètre.</span><span class="sxs-lookup"><span data-stu-id="4962f-160">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `deleteMessage` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="4962f-161">La méthode `deleteMessage` marque le message comme étant utilisé et le supprime de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="4962f-161">The `deleteMessage` method marks the message as being consumed and removes it from the queue.</span></span>

<span data-ttu-id="4962f-162">L’exemple suivant montre comment recevoir et traiter des messages à l’aide de la méthode `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="4962f-162">The following example demonstrates how to receive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="4962f-163">L’exemple reçoit et supprime un message, reçoit un message en utilisant la méthode `isPeekLock` définie sur **true**, puis supprime le message à l’aide de la méthode `deleteMessage` :</span><span class="sxs-lookup"><span data-stu-id="4962f-163">The example first receives and deletes a message, and then receives a message using `isPeekLock` set to **true**, then deletes the message using `deleteMessage`:</span></span>

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="4962f-164">Gestion des blocages d’application et des messages illisibles</span><span class="sxs-lookup"><span data-stu-id="4962f-164">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="4962f-165">Service Bus intègre des fonctionnalités destinées à faciliter la récupération à la suite d’erreurs survenues dans votre application ou de difficultés à traiter un message.</span><span class="sxs-lookup"><span data-stu-id="4962f-165">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="4962f-166">Si une application réceptrice ne parvient pas à traiter le message pour une raison quelconque, elle appelle la méthode `unlockMessage` pour l’objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="4962f-166">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="4962f-167">Service Bus déverrouille alors le message dans la file d’attente et le rend à nouveau disponible en réception, pour la même application consommatrice ou pour une autre.</span><span class="sxs-lookup"><span data-stu-id="4962f-167">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="4962f-168">De même, il faut savoir qu’un message verrouillé dans une file d’attente est assorti d’un délai d’expiration et que si l’application ne parvient pas à traiter le message dans le temps imparti (par exemple, si l’application subit un incident), Service Bus déverrouille le message automatiquement et le rend à nouveau disponible en réception.</span><span class="sxs-lookup"><span data-stu-id="4962f-168">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="4962f-169">Si l’application subit un incident après le traitement du message, mais avant l’appel de la méthode `deleteMessage`, le message est à nouveau remis à l’application lorsqu’elle redémarre.</span><span class="sxs-lookup"><span data-stu-id="4962f-169">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="4962f-170">Dans ce type de traitement, souvent appelé *Au moins une fois*, chaque message est traité au moins une fois. Toutefois, dans certaines circonstances, un même message peut être remis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="4962f-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="4962f-171">Toutefois, dans certaines circonstances, un même message peut être remis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="4962f-171">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="4962f-172">Pour ce faire, il suffit souvent d’utiliser la propriété **MessageId** du message, qui reste constante pendant les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="4962f-172">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4962f-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4962f-173">Next steps</span></span>
<span data-ttu-id="4962f-174">Pour en savoir plus sur les files d’attente, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="4962f-174">To learn more about queues, see the following resources.</span></span>

* <span data-ttu-id="4962f-175">[Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="4962f-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="4962f-176">Référentiel du [Kit de développement logiciel (SDK) Azure pour Node][Azure SDK for Node] sur GitHub</span><span class="sxs-lookup"><span data-stu-id="4962f-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="4962f-177">Centre pour développeurs Node.js</span><span class="sxs-lookup"><span data-stu-id="4962f-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application to an Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
