---
title: Utilisation des rubriques et abonnements Azure Service Bus avec Node.js | Microsoft Docs
description: "Découvrez comment utiliser les rubriques et abonnements Service Bus dans Azure à partir d’une application Node.js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 24ae9b80f75531c5e4a84c3b4a6666a6f8a83d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="a1f75-103">Utilisation des rubriques et abonnements Service Bus avec Node.js</span><span class="sxs-lookup"><span data-stu-id="a1f75-103">How to Use Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="a1f75-104">Ce guide décrit l’utilisation des rubriques et des abonnements Service Bus depuis les applications Node.js.</span><span class="sxs-lookup"><span data-stu-id="a1f75-104">This guide describes how to use Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="a1f75-105">Les scénarios couverts incluent la **création de rubriques et d’abonnements**, la **création de filtres d’abonnement**, **l’envoi de messages à une rubrique**, la **réception de messages en provenance d’un abonnement** et enfin la **suppression de rubriques et d’abonnements**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-105">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="a1f75-106">Pour plus d’informations sur les rubriques et les abonnements, consultez la section [Étapes suivantes](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="a1f75-106">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="a1f75-107">Création d’une application Node.js</span><span class="sxs-lookup"><span data-stu-id="a1f75-107">Create a Node.js application</span></span>
<span data-ttu-id="a1f75-108">Créez une application Node.js vide.</span><span class="sxs-lookup"><span data-stu-id="a1f75-108">Create a blank Node.js application.</span></span> <span data-ttu-id="a1f75-109">Pour obtenir les instructions permettant de créer une application Node.js, consultez les pages [Création et déploiement d’une application Node.js dans un site web Azure], [Service cloud Node.js][Node.js Cloud Service] avec Windows PowerShell ou Site Web avec WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="a1f75-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to an Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="a1f75-110">Configuration de votre application pour l’utilisation de Service Bus</span><span class="sxs-lookup"><span data-stu-id="a1f75-110">Configure your application to use Service Bus</span></span>
<span data-ttu-id="a1f75-111">Pour utiliser Service Bus, téléchargez le package Azure Node.js.</span><span class="sxs-lookup"><span data-stu-id="a1f75-111">To use Service Bus, download the Node.js Azure package.</span></span> <span data-ttu-id="a1f75-112">Ce dernier inclut des bibliothèques permettant de communiquer avec les services REST de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a1f75-112">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="a1f75-113">Utilisation de Node Package Manager (NPM) pour obtenir le package</span><span class="sxs-lookup"><span data-stu-id="a1f75-113">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="a1f75-114">Utilisez une interface de ligne de commande telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix) pour accéder au dossier dans lequel vous avez créé votre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="a1f75-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="a1f75-115">Tapez **npm install azure** dans la fenêtre de commande, ce qui génère la sortie suivante :</span><span class="sxs-lookup"><span data-stu-id="a1f75-115">Type **npm install azure** in the command window, which should result in the following output:</span></span>

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
3. <span data-ttu-id="a1f75-116">Vous pouvez exécuter manuellement la commande **ls** pour vérifier que le dossier **node\_modules** a été créé.</span><span class="sxs-lookup"><span data-stu-id="a1f75-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="a1f75-117">Dans ce dossier, recherchez le package **azure**, qui contient les bibliothèques nécessaires pour accéder aux rubriques de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a1f75-117">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus topics.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="a1f75-118">Importation du module</span><span class="sxs-lookup"><span data-stu-id="a1f75-118">Import the module</span></span>
<span data-ttu-id="a1f75-119">À l’aide d’un éditeur de texte, comme le Bloc-notes, ajoutez la commande suivante au début du fichier **server.js** de l’application :</span><span class="sxs-lookup"><span data-stu-id="a1f75-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="a1f75-120">Configuration d’une connexion Service Bus</span><span class="sxs-lookup"><span data-stu-id="a1f75-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="a1f75-121">Le module Azure lit les variables d’environnement `AZURE_SERVICEBUS_NAMESPACE` et `AZURE_SERVICEBUS_ACCESS_KEY` pour obtenir les informations nécessaires pour se connecter à Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a1f75-121">The Azure module reads the environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required to connect to Service Bus.</span></span> <span data-ttu-id="a1f75-122">Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte lors de l’appel de `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="a1f75-122">If these environment variables are not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="a1f75-123">Pour obtenir un exemple de paramétrage des variables d’environnement pour un service cloud Azure, consultez [Service cloud Node.js avec stockage][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="a1f75-123">For an example of setting the environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="a1f75-124">Pour obtenir un exemple de configuration des variables d’environnement pour un site web Azure, consultez [Application web Node.js avec stockage][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="a1f75-124">For an example of setting the environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="a1f75-125">Création d'une rubrique</span><span class="sxs-lookup"><span data-stu-id="a1f75-125">Create a topic</span></span>
<span data-ttu-id="a1f75-126">L’objet **ServiceBusService** permet d’utiliser des rubriques.</span><span class="sxs-lookup"><span data-stu-id="a1f75-126">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="a1f75-127">Le code suivant crée un objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="a1f75-128">Ajoutez-le vers le début du fichier **server.js** , après l'instruction relative à l'importation du module Azure :</span><span class="sxs-lookup"><span data-stu-id="a1f75-128">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="a1f75-129">En appelant `createTopicIfNotExists` dans l’objet **ServiceBusService**, la rubrique spécifiée est renvoyée (si elle existe) ou une nouvelle rubrique comportant le nom spécifié est créée.</span><span class="sxs-lookup"><span data-stu-id="a1f75-129">By calling `createTopicIfNotExists` on the **ServiceBusService** object, the specified topic will be returned (if it exists,) or a new topic with the specified name will be created.</span></span> <span data-ttu-id="a1f75-130">Le code suivant utilise `createTopicIfNotExists` pour créer la rubrique nommée `MyTopic` ou s’y connecter :</span><span class="sxs-lookup"><span data-stu-id="a1f75-130">The following code uses `createTopicIfNotExists` to create or connect to the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="a1f75-131">La méthode `createServiceBusService` prend également en charge des options supplémentaires, qui vous permettent de remplacer les paramètres de rubrique par défaut, comme la durée de vie du message ou la taille maximale de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="a1f75-131">The `createServiceBusService` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="a1f75-132">L’exemple suivant définit la taille maximale de la rubrique sur 5 Go et la durée de vie de message sur 1 minute :</span><span class="sxs-lookup"><span data-stu-id="a1f75-132">The following example sets the maximum topic size to 5GB with a time to live of 1 minute:</span></span>

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="a1f75-133">Filtres</span><span class="sxs-lookup"><span data-stu-id="a1f75-133">Filters</span></span>
<span data-ttu-id="a1f75-134">Des opérations facultatives de filtrage peuvent être appliquées aux opérations exécutées par le biais de **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-134">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="a1f75-135">Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature :</span><span class="sxs-lookup"><span data-stu-id="a1f75-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="a1f75-136">Après le prétraitement des options de la requête, la méthode appelle `next` en passant un rappel avec la signature suivante :</span><span class="sxs-lookup"><span data-stu-id="a1f75-136">After performing preprocessing on the request options, the method calls `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="a1f75-137">Dans ce rappel, et après le traitement de `returnObject` (la réponse de la requête au serveur), le rappel doit appeler la fonction next, si elle existe, pour continuer à traiter d’autres filtres ou simplement appeler `finalCallback` pour terminer l’utilisation du service.</span><span class="sxs-lookup"><span data-stu-id="a1f75-137">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or invoke `finalCallback` otherwise, to end the service invocation.</span></span>

<span data-ttu-id="a1f75-138">Deux filtres qui implémentent la logique de relance sont inclus dans le Kit de développement logiciel (SDK) Azure pour Node.js : **ExponentialRetryPolicyFilter** et **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="a1f75-139">Le code suivant crée un objet **ServiceBusService** qui utilise le filtre **ExponentialRetryPolicyFilter** :</span><span class="sxs-lookup"><span data-stu-id="a1f75-139">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="a1f75-140">Création d’abonnements</span><span class="sxs-lookup"><span data-stu-id="a1f75-140">Create subscriptions</span></span>
<span data-ttu-id="a1f75-141">Les abonnements de rubrique sont également créés à l’aide de l’objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-141">Topic subscriptions are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="a1f75-142">Les abonnements sont nommés et peuvent être assortis d'un filtre facultatif qui limite l'ensemble des messages transmis à la file d'attente virtuelle de l'abonnement.</span><span class="sxs-lookup"><span data-stu-id="a1f75-142">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="a1f75-143">Les abonnements sont persistants et continuent à exister jusqu’à leur suppression ou celle de la rubrique à laquelle ils sont associés.</span><span class="sxs-lookup"><span data-stu-id="a1f75-143">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="a1f75-144">Si votre application contient une logique pour la création d’un abonnement, elle doit d’abord vérifier si l’abonnement existe déjà en utilisant la méthode `getSubscription`.</span><span class="sxs-lookup"><span data-stu-id="a1f75-144">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="a1f75-145">Création d’un abonnement avec le filtre par défaut (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="a1f75-145">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="a1f75-146">Le filtre **MatchAll** est le filtre utilisé par défaut si aucun filtre n’est spécifié lors de la création d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="a1f75-146">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="a1f75-147">Lorsque le filtre **MatchAll** est utilisé, tous les messages publiés dans la rubrique sont placés dans la file d’attente virtuelle de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a1f75-147">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="a1f75-148">Dans l’exemple suivant, l’abonnement « AllMessages » qui est créé utilise le filtre par défaut **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-148">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="a1f75-149">Création d’abonnements avec des filtres</span><span class="sxs-lookup"><span data-stu-id="a1f75-149">Create subscriptions with filters</span></span>
<span data-ttu-id="a1f75-150">Vous pouvez également créer des filtres pour spécifier quels sont les messages, parmi ceux envoyés à une rubrique, qui doivent apparaître dans un abonnement de rubrique spécifique.</span><span class="sxs-lookup"><span data-stu-id="a1f75-150">You can also create filters that allow you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="a1f75-151">Parmi les types de filtre pris en charge par les abonnements, **SqlFilter** est le plus flexible. Il implémente un sous-ensemble de SQL92.</span><span class="sxs-lookup"><span data-stu-id="a1f75-151">The most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="a1f75-152">Les filtres SQL opèrent au niveau des propriétés des messages publiés dans la rubrique.</span><span class="sxs-lookup"><span data-stu-id="a1f75-152">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="a1f75-153">Pour plus de détails sur les expressions utilisables avec un filtre SQL, examinez la syntaxe [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="a1f75-153">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="a1f75-154">Il est possible d’ajouter des filtres à un abonnement en utilisant la méthode `createRule` de l’objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-154">Filters can be added to a subscription by using the `createRule` method of the **ServiceBusService** object.</span></span> <span data-ttu-id="a1f75-155">Cette méthode vous permet d’ajouter de nouveaux filtres à un abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="a1f75-155">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a1f75-156">Comme le filtre par défaut est appliqué automatiquement à tous les nouveaux abonnements, vous devez commencer par supprimer le filtre par défaut, sans quoi le filtre **MatchAll** remplace tous les autres filtres spécifiés.</span><span class="sxs-lookup"><span data-stu-id="a1f75-156">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="a1f75-157">Vous pouvez supprimer la règle par défaut en utilisant la méthode `deleteRule` de l’objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-157">You can remove the default rule by using the `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="a1f75-158">L’exemple suivant crée l’abonnement `HighMessages` avec un objet **SqlFilter** qui ne sélectionne que les messages dont la propriété personnalisée `messagenumber` a une valeur supérieure à 3 :</span><span class="sxs-lookup"><span data-stu-id="a1f75-158">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="a1f75-159">De même, l’exemple suivant crée l’abonnement `LowMessages` avec un objet **SqlFilter** qui ne sélectionne que les messages dont la propriété `messagenumber` a une valeur inférieure ou égale à 3 :</span><span class="sxs-lookup"><span data-stu-id="a1f75-159">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="a1f75-160">Désormais, quand un message est envoyé à `MyTopic`, il est toujours remis aux destinataires abonnés à l’abonnement de rubrique `AllMessages`, et est remis de manière sélective aux destinataires abonnés aux abonnements de rubrique `HighMessages` et `LowMessages` (en fonction du contenu du message).</span><span class="sxs-lookup"><span data-stu-id="a1f75-160">When a message is now sent to `MyTopic`, it will always be delivered to receivers subscribed to the `AllMessages` topic subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` topic subscriptions (depending upon the message content).</span></span>

## <a name="how-to-send-messages-to-a-topic"></a><span data-ttu-id="a1f75-161">Envoi de messages à une rubrique</span><span class="sxs-lookup"><span data-stu-id="a1f75-161">How to send messages to a topic</span></span>
<span data-ttu-id="a1f75-162">Pour envoyer un message à une rubrique Service Bus, votre application doit utiliser la méthode `sendTopicMessage` de l’objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-162">To send a message to a Service Bus topic, your application must use the `sendTopicMessage` method of the **ServiceBusService** object.</span></span>
<span data-ttu-id="a1f75-163">Les messages envoyés aux rubriques Service Bus sont des objets **BrokeredMessage**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-163">Messages sent to Service Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="a1f75-164">Les objets **BrokeredMessage** possèdent un ensemble de propriétés standard (telles que `Label` et `TimeToLive`), un dictionnaire servant à conserver les propriétés personnalisées propres à une application, ainsi qu’un corps de données de chaîne.</span><span class="sxs-lookup"><span data-stu-id="a1f75-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="a1f75-165">Une application peut définir le corps du message en transmettant une valeur de chaîne à la méthode `sendTopicMessage` pour remplir toutes les propriétés standard requises avec les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="a1f75-165">An application can set the body of the message by passing a string value to the `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="a1f75-166">L’exemple suivant montre comment envoyer cinq messages de test à `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="a1f75-166">The following example demonstrates how to send five test messages to `MyTopic`.</span></span> <span data-ttu-id="a1f75-167">Notez que la valeur de la propriété `messagenumber` de chaque message varie au niveau de l’itération de la boucle (détermine les abonnements qui le reçoivent) :</span><span class="sxs-lookup"><span data-stu-id="a1f75-167">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

<span data-ttu-id="a1f75-168">Les rubriques Service Bus prennent en charge une taille de message maximale de 256 Ko dans le [niveau Standard](service-bus-premium-messaging.md) et de 1 Mo dans le [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="a1f75-168">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="a1f75-169">L’en-tête, qui comprend les propriétés d’application standard et personnalisées, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="a1f75-169">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="a1f75-170">Si une rubrique n'est pas limitée par le nombre de messages qu'elle peut contenir, elle l'est en revanche par la taille totale des messages qu'elle contient.</span><span class="sxs-lookup"><span data-stu-id="a1f75-170">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="a1f75-171">Cette taille de rubrique est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="a1f75-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="a1f75-172">Réception des messages d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="a1f75-172">Receive messages from a subscription</span></span>
<span data-ttu-id="a1f75-173">La méthode `receiveSubscriptionMessage` de l’objet **ServiceBusService** permet de recevoir les messages d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="a1f75-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="a1f75-174">Par défaut, les messages sont supprimés de l’abonnement au fur et à mesure de leur lecture. Cependant, vous pouvez lire et verrouiller le message sans le supprimer de l’abonnement en définissant le paramètre facultatif `isPeekLock` sur **true**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-174">By default, messages are deleted from the subscription as they are read; however, you can read (peek) and lock the message without deleting it from the subscription by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="a1f75-175">Le comportement par défaut de lecture et de suppression du message dans le cadre de l’opération de réception est le modèle le plus simple et le mieux adapté aux scénarios dans lesquels une application est capable de tolérer le non-traitement d’un message en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="a1f75-175">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="a1f75-176">Pour mieux comprendre, imaginez un scénario dans lequel le consommateur émet la demande de réception et subit un incident avant de la traiter.</span><span class="sxs-lookup"><span data-stu-id="a1f75-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="a1f75-177">Comme Service Bus a marqué le message comme étant consommé, lorsque l’application redémarre et recommence à consommer des messages, elle manque le message consommé avant l’incident.</span><span class="sxs-lookup"><span data-stu-id="a1f75-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="a1f75-178">Si le paramètre `isPeekLock` est défini sur **true**, la réception devient une opération en deux étapes, qui autorise une prise en charge des applications qui ne peuvent pas tolérer les messages manquants.</span><span class="sxs-lookup"><span data-stu-id="a1f75-178">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="a1f75-179">Lorsque Service Bus reçoit une demande, il recherche le prochain message à consommer, le verrouille pour empêcher d'autres consommateurs de le recevoir, puis le renvoie à l'application.</span><span class="sxs-lookup"><span data-stu-id="a1f75-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span>
<span data-ttu-id="a1f75-180">Dès lors que l’application a terminé le traitement du message (ou qu’elle l’a stocké de manière fiable pour un traitement ultérieur), elle accomplit la deuxième étape du processus de réception en appelant la méthode **deleteMessage** et en fournissant le message à supprimer sous la forme d’un paramètre.</span><span class="sxs-lookup"><span data-stu-id="a1f75-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="a1f75-181">La méthode **deleteMessage** marque le message comme étant consommé et le supprime de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a1f75-181">The **deleteMessage** method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="a1f75-182">L’exemple suivant montre comment les messages peuvent être reçus et traités à l’aide de `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="a1f75-182">The following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="a1f75-183">Dans l’exemple, le message est d’abord réceptionné, puis supprimé de l’abonnement « LowMessages ». Un message envoyé par l’abonnement « HighMessages » est ensuite réceptionné en définissant `isPeekLock` sur true.</span><span class="sxs-lookup"><span data-stu-id="a1f75-183">The example first receives and deletes a message from the 'LowMessages' subscription, and then receives a message from the 'HighMessages' subscription using `isPeekLock` set to true.</span></span> <span data-ttu-id="a1f75-184">La suppression du message s’effectue ensuite à l’aide de `deleteMessage` :</span><span class="sxs-lookup"><span data-stu-id="a1f75-184">It then deletes the message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="a1f75-185">Gestion des blocages d’application et des messages illisibles</span><span class="sxs-lookup"><span data-stu-id="a1f75-185">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="a1f75-186">Service Bus intègre des fonctionnalités destinées à faciliter la récupération à la suite d’erreurs survenues dans votre application ou de difficultés à traiter un message.</span><span class="sxs-lookup"><span data-stu-id="a1f75-186">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="a1f75-187">Si une application réceptrice ne parvient pas à traiter le message pour une raison quelconque, elle appelle la méthode `unlockMessage` pour l’objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="a1f75-187">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="a1f75-188">Cela amène Service Bus à déverrouiller le message dans l’abonnement et à le rendre à nouveau disponible en réception, pour la même application consommatrice ou pour une autre.</span><span class="sxs-lookup"><span data-stu-id="a1f75-188">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="a1f75-189">De même, il faut savoir qu’un message verrouillé dans un abonnement est assorti d’un délai d’expiration et que si l’application ne parvient pas à traiter le message dans le temps imparti (par exemple, si l’application subit un incident), Service Bus déverrouille le message automatiquement et le rend à nouveau disponible en réception.</span><span class="sxs-lookup"><span data-stu-id="a1f75-189">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="a1f75-190">Si l’application subit un incident après le traitement du message, mais avant l’appel de la méthode `deleteMessage`, le message est à nouveau remis à l’application lorsqu’elle redémarre.</span><span class="sxs-lookup"><span data-stu-id="a1f75-190">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="a1f75-191">Dans ce type de traitement, souvent appelé *Au moins une fois*, chaque message est traité au moins une fois. Toutefois, dans certaines circonstances, un même message peut être remis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="a1f75-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="a1f75-192">Toutefois, dans certaines circonstances, un même message peut être remis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="a1f75-192">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="a1f75-193">Pour ce faire, il suffit souvent d’utiliser la propriété **MessageId** du message, qui reste constante pendant les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="a1f75-193">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="a1f75-194">Suppression de rubriques et d'abonnements</span><span class="sxs-lookup"><span data-stu-id="a1f75-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="a1f75-195">Les rubriques et les abonnements sont persistants et doivent être supprimés de façon explicite par le biais du [portail Azure][Azure portal] ou par programme.</span><span class="sxs-lookup"><span data-stu-id="a1f75-195">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="a1f75-196">L’exemple suivant montre comment supprimer la rubrique `MyTopic` :</span><span class="sxs-lookup"><span data-stu-id="a1f75-196">The following example demonstrates how to delete the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="a1f75-197">La suppression d’une rubrique a également pour effet de supprimer les abonnements inscrits au niveau de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="a1f75-197">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="a1f75-198">Les abonnements peuvent aussi être supprimés de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="a1f75-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="a1f75-199">L’exemple suivant montre comment supprimer l’abonnement `HighMessages` de la rubrique `MyTopic` :</span><span class="sxs-lookup"><span data-stu-id="a1f75-199">The following example shows how to delete a subscription named `HighMessages` from the `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="a1f75-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a1f75-200">Next Steps</span></span>
<span data-ttu-id="a1f75-201">Maintenant que vous avez appris les principes de base des rubriques Service Bus, consultez ces liens pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="a1f75-201">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="a1f75-202">Consultez [Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="a1f75-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="a1f75-203">Référence d’API pour [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="a1f75-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="a1f75-204">Accédez au référentiel du [Kit de développement logiciel (SDK) Azure pour Node][Azure SDK for Node] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a1f75-204">Visit the [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Création et déploiement d’une application Node.js dans un site web Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
