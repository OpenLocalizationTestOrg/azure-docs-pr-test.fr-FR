---
title: aaaHow toouse Azure Service Bus rubriques et les abonnements avec Node.js | Documents Microsoft
description: "Découvrez comment toouse Service Bus rubriques et abonnements dans Azure à partir d’une application Node.js."
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
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="32d3f-103">Comment tooUse Service Bus rubriques et les abonnements avec Node.js</span><span class="sxs-lookup"><span data-stu-id="32d3f-103">How tooUse Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="32d3f-104">Ce guide décrit comment toouse Service Bus rubriques et abonnements à partir d’applications Node.js.</span><span class="sxs-lookup"><span data-stu-id="32d3f-104">This guide describes how toouse Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="32d3f-105">Hello scénarios abordés incluent **création de rubriques et abonnements**, **création de filtres d’abonnement**, **envoi de messages** tooa rubrique, **réception les messages à partir d’un abonnement**, et **suppression des rubriques et abonnements**.</span><span class="sxs-lookup"><span data-stu-id="32d3f-105">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="32d3f-106">Pour plus d’informations sur les rubriques et les abonnements, consultez hello [étapes](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="32d3f-106">For more information about topics and subscriptions, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="32d3f-107">Création d’une application Node.js</span><span class="sxs-lookup"><span data-stu-id="32d3f-107">Create a Node.js application</span></span>
<span data-ttu-id="32d3f-108">Créez une application Node.js vide.</span><span class="sxs-lookup"><span data-stu-id="32d3f-108">Create a blank Node.js application.</span></span> <span data-ttu-id="32d3f-109">Pour obtenir des instructions sur la création d’une application Node.js, consultez [créer et déployer un tooan d’application Node.js Site Web Azure], [Service de cloud computing Node.js] [ Node.js Cloud Service] à l’aide de Windows PowerShell, ou un Site Web avec WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="32d3f-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooan Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="32d3f-110">Configurer votre toouse application Service Bus</span><span class="sxs-lookup"><span data-stu-id="32d3f-110">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="32d3f-111">toouse Service Bus, téléchargez hello package Node.js Azure.</span><span class="sxs-lookup"><span data-stu-id="32d3f-111">toouse Service Bus, download hello Node.js Azure package.</span></span> <span data-ttu-id="32d3f-112">Ce package comprend un ensemble de bibliothèques qui communiquent avec les services de Service Bus REST hello.</span><span class="sxs-lookup"><span data-stu-id="32d3f-112">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="32d3f-113">Utiliser le Gestionnaire de Package de nœud (NPM) tooobtain hello package</span><span class="sxs-lookup"><span data-stu-id="32d3f-113">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="32d3f-114">Utiliser une interface de ligne de commande comme **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), accédez dossier toohello où vous avez créé votre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="32d3f-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="32d3f-115">Type **npm installer azure** dans la fenêtre de commande hello, qui doivent entraîner hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="32d3f-115">Type **npm install azure** in hello command window, which should result in hello following output:</span></span>

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
3. <span data-ttu-id="32d3f-116">Vous pouvez exécuter manuellement hello **ls** tooverify de commande qui un **nœud\_modules** dossier a été créé.</span><span class="sxs-lookup"><span data-stu-id="32d3f-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="32d3f-117">Dans ce dossier de trouver la **azure** package qui contient les bibliothèques hello vous devez tooaccess rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="32d3f-117">Inside that folder find the **azure** package, which contains hello libraries you need tooaccess Service Bus topics.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="32d3f-118">Module d’importation hello</span><span class="sxs-lookup"><span data-stu-id="32d3f-118">Import hello module</span></span>
<span data-ttu-id="32d3f-119">Utilisez le bloc-notes ou un autre éditeur de texte, ajoutez hello suivant en haut de toohello de hello **server.js** fichier de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="32d3f-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="32d3f-120">Configuration d’une connexion Service Bus</span><span class="sxs-lookup"><span data-stu-id="32d3f-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="32d3f-121">Bonjour Azure module lit les variables d’environnement hello `AZURE_SERVICEBUS_NAMESPACE` et `AZURE_SERVICEBUS_ACCESS_KEY` pour plus d’informations obligatoires tooconnect tooService Bus.</span><span class="sxs-lookup"><span data-stu-id="32d3f-121">hello Azure module reads hello environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required tooconnect tooService Bus.</span></span> <span data-ttu-id="32d3f-122">Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello lors de l’appel `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="32d3f-122">If these environment variables are not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="32d3f-123">Pour obtenir un exemple de la configuration des variables d’environnement hello pour un Service Cloud Azure, consultez [Service de Cloud Node.js avec stockage][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="32d3f-123">For an example of setting hello environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="32d3f-124">Pour obtenir un exemple de la définition de variables d’environnement hello pour un site Web Azure, consultez [Node.js d’Application Web avec stockage][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="32d3f-124">For an example of setting hello environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="32d3f-125">Création d'une rubrique</span><span class="sxs-lookup"><span data-stu-id="32d3f-125">Create a topic</span></span>
<span data-ttu-id="32d3f-126">Hello **ServiceBusService** objet vous permet de toowork aux rubriques.</span><span class="sxs-lookup"><span data-stu-id="32d3f-126">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="32d3f-127">Le code suivant crée un objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="32d3f-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="32d3f-128">Ajouter au début de hello **server.js** fichier, après le module de hello instruction tooimport hello azure :</span><span class="sxs-lookup"><span data-stu-id="32d3f-128">Add it near the top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="32d3f-129">En appelant `createTopicIfNotExists` sur hello **ServiceBusService** de l’objet, hello spécifié rubrique sera retournée (si elle existe), ou une rubrique avec le nom spécifié de hello sera créée.</span><span class="sxs-lookup"><span data-stu-id="32d3f-129">By calling `createTopicIfNotExists` on hello **ServiceBusService** object, hello specified topic will be returned (if it exists,) or a new topic with hello specified name will be created.</span></span> <span data-ttu-id="32d3f-130">code Hello suivant utilise `createTopicIfNotExists` toocreate ou connectez-vous rubrique toohello nommée `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="32d3f-130">hello following code uses `createTopicIfNotExists` toocreate or connect toohello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="32d3f-131">Hello `createServiceBusService` méthode prend également en charge des options supplémentaires, qui vous permettent de paramètres de rubrique toooverride par défaut tels que la durée de vie du message ou de la taille maximale de rubrique.</span><span class="sxs-lookup"><span data-stu-id="32d3f-131">hello `createServiceBusService` method also supports additional options, which enable you toooverride default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="32d3f-132">Hello exemple suivant définit too5GB de taille maximale de rubrique hello avec une heure toolive de 1 minute :</span><span class="sxs-lookup"><span data-stu-id="32d3f-132">hello following example sets hello maximum topic size too5GB with a time toolive of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="32d3f-133">Filtres</span><span class="sxs-lookup"><span data-stu-id="32d3f-133">Filters</span></span>
<span data-ttu-id="32d3f-134">Les opérations de filtrage facultatif peuvent être appliquées toooperations effectuées à l’aide **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="32d3f-134">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="32d3f-135">Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature de hello :</span><span class="sxs-lookup"><span data-stu-id="32d3f-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="32d3f-136">Après avoir effectué sur les options de demande hello de prétraitement, hello appels de méthode `next`, en passant un rappel avec hello après signature :</span><span class="sxs-lookup"><span data-stu-id="32d3f-136">After performing preprocessing on hello request options, hello method calls `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="32d3f-137">Dans ce rappel et après traitement hello `returnObject` (hello réponse hello demande toohello serveur), rappel de hello doit tooeither appeler ensuite s’il existe des toocontinue du traitement des autres filtres ou appeler `finalCallback` dans le cas contraire, tooend hello appel de service.</span><span class="sxs-lookup"><span data-stu-id="32d3f-137">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or invoke `finalCallback` otherwise, tooend hello service invocation.</span></span>

<span data-ttu-id="32d3f-138">Deux filtres qui implémentent la logique de nouvelle tentative sont incluses avec hello Azure SDK pour Node.js, **ExponentialRetryPolicyFilter** et **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="32d3f-138">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="32d3f-139">Hello suivante permet de créer un **ServiceBusService** objet qui utilise hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="32d3f-139">hello following creates a **ServiceBusService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="32d3f-140">Création d’abonnements</span><span class="sxs-lookup"><span data-stu-id="32d3f-140">Create subscriptions</span></span>
<span data-ttu-id="32d3f-141">Abonnements aux rubriques sont également créés par hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="32d3f-141">Topic subscriptions are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="32d3f-142">Les abonnements sont nommés et peuvent avoir un filtre facultatif qui limite l’ensemble hello de messages remis de file d’attente virtuelle de l’abonnement toohello.</span><span class="sxs-lookup"><span data-stu-id="32d3f-142">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="32d3f-143">Abonnements sont persistantes et continuent jusqu'à ce que soit leur tooexist ou hello rubrique associées, elles sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="32d3f-143">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="32d3f-144">Si votre application contient la logique toocreate un abonnement, il doit tout d’abord vérifier si hello abonnement existe déjà à l’aide de la `getSubscription` (méthode).</span><span class="sxs-lookup"><span data-stu-id="32d3f-144">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="32d3f-145">Créer un abonnement avec le filtre par défaut (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="32d3f-145">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="32d3f-146">Hello **MatchAll** filtre est hello par défaut qui est utilisé si aucun filtre n’est spécifiée lors de la création d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="32d3f-146">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="32d3f-147">Hello lorsque **MatchAll** filtre est utilisé, la rubrique de toohello publié tous les messages sont placés dans la file d’attente virtuelle de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="32d3f-147">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="32d3f-148">Hello exemple suivant crée un abonnement nommé « AllMessages » et utilise hello par défaut **MatchAll** filtre.</span><span class="sxs-lookup"><span data-stu-id="32d3f-148">hello following example creates a subscription named 'AllMessages' and uses hello default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="32d3f-149">Création d’abonnements avec des filtres</span><span class="sxs-lookup"><span data-stu-id="32d3f-149">Create subscriptions with filters</span></span>
<span data-ttu-id="32d3f-150">Vous pouvez également créer des filtres qui vous permettent de tooscope lesquelles messages envoyés tooa rubrique doit apparaître dans un abonnement à une rubrique spécifique.</span><span class="sxs-lookup"><span data-stu-id="32d3f-150">You can also create filters that allow you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="32d3f-151">Bonjour type de filtre pris en charge par les abonnements plus souple est la **SqlFilter**, qui implémente un sous-ensemble de SQL92.</span><span class="sxs-lookup"><span data-stu-id="32d3f-151">hello most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="32d3f-152">Filtres SQL fonctionnent sur les propriétés hello de messages hello qui sont publiées toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="32d3f-152">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="32d3f-153">Pour plus d’informations sur les expressions hello qui peuvent être utilisées avec un filtre SQL, consultez hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxe.</span><span class="sxs-lookup"><span data-stu-id="32d3f-153">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="32d3f-154">Filtres peuvent être ajoutés tooa abonnement à l’aide de hello `createRule` méthode Hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="32d3f-154">Filters can be added tooa subscription by using hello `createRule` method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="32d3f-155">Cette méthode vous permet de vous permet d’ajouter de nouveaux filtres tooan abonnement.</span><span class="sxs-lookup"><span data-stu-id="32d3f-155">This method allows you to add new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="32d3f-156">Étant donné que le filtre par défaut de hello est appliqué automatiquement tooall nouveaux abonnements, vous devez d’abord supprimer filtre par défaut de hello ou **MatchAll** remplace tous les autres filtres que vous pouvez spécifier.</span><span class="sxs-lookup"><span data-stu-id="32d3f-156">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="32d3f-157">Vous pouvez supprimer la règle par défaut de hello à l’aide de hello `deleteRule` méthode de la **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="32d3f-157">You can remove hello default rule by using hello `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="32d3f-158">Hello exemple suivant crée un abonnement nommé `HighMessages` avec un **SqlFilter** qui sélectionne uniquement les messages qui ont personnalisé `messagenumber` propriété supérieure à 3 :</span><span class="sxs-lookup"><span data-stu-id="32d3f-158">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="32d3f-159">De même, hello exemple suivant crée un abonnement nommé `LowMessages` avec un **SqlFilter** qui sélectionne uniquement les messages qui ont un `messagenumber` propriété inférieur ou égal too3 :</span><span class="sxs-lookup"><span data-stu-id="32d3f-159">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

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

<span data-ttu-id="32d3f-160">Lorsqu’un message est envoyé maintenant trop`MyTopic`, elle est envoyée à l’abonné de récepteurs toohello `AllMessages` abonnement à une rubrique et remis de manière sélective tooreceivers abonné toohello `HighMessages` et `LowMessages` abonnements à la rubrique (en fonction de contenu du message hello).</span><span class="sxs-lookup"><span data-stu-id="32d3f-160">When a message is now sent too`MyTopic`, it will always be delivered to receivers subscribed toohello `AllMessages` topic subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="how-toosend-messages-tooa-topic"></a><span data-ttu-id="32d3f-161">Comment les messages toosend tooa rubrique</span><span class="sxs-lookup"><span data-stu-id="32d3f-161">How toosend messages tooa topic</span></span>
<span data-ttu-id="32d3f-162">toosend une rubrique de Service Bus message tooa, votre application doit utiliser le `sendTopicMessage` méthode Hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="32d3f-162">toosend a message tooa Service Bus topic, your application must use the `sendTopicMessage` method of hello **ServiceBusService** object.</span></span>
<span data-ttu-id="32d3f-163">Les messages envoyés sont des rubriques du Bus tooService **BrokeredMessage** objets.</span><span class="sxs-lookup"><span data-stu-id="32d3f-163">Messages sent tooService Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="32d3f-164">**BrokeredMessage** objets comportent un ensemble de propriétés standard (tels que `Label` et `TimeToLive`), un dictionnaire qui est utilisé toohold des propriétés personnalisées spécifiques à l’application et un corps de données de chaîne.</span><span class="sxs-lookup"><span data-stu-id="32d3f-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="32d3f-165">Une application peut définir le corps de hello du message de type hello en passant une valeur de chaîne Hello `sendTopicMessage` et toute requise propriétés standard seront remplies par les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="32d3f-165">An application can set hello body of hello message by passing a string value to hello `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="32d3f-166">Hello exemple suivant montre comment toosend cinq messages de test à `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="32d3f-166">hello following example demonstrates how toosend five test messages to `MyTopic`.</span></span> <span data-ttu-id="32d3f-167">Notez que hello `messagenumber` varie en fonction de valeur de la propriété de chaque message sur l’itération hello de boucle de hello (Cela permet de déterminer les abonnements reçoivent) :</span><span class="sxs-lookup"><span data-stu-id="32d3f-167">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="32d3f-168">Rubriques Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="32d3f-168">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="32d3f-169">en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="32d3f-169">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="32d3f-170">Il n’existe aucune limite sur le nombre de hello de messages conservés dans une rubrique mais hello de taille totale des messages hello détenus par une rubrique est une extrémité de fin.</span><span class="sxs-lookup"><span data-stu-id="32d3f-170">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="32d3f-171">Cette taille de rubrique est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="32d3f-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="32d3f-172">Réception des messages d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="32d3f-172">Receive messages from a subscription</span></span>
<span data-ttu-id="32d3f-173">Les messages sont reçus à partir d’un abonnement à l’aide de la `receiveSubscriptionMessage` méthode sur hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="32d3f-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="32d3f-174">Par défaut, les messages sont supprimés de l’abonnement de hello lorsqu’elles sont lues ; Toutefois, vous pouvez lire (aperçu) et verrouiller le message de type hello sans la supprimer de l’abonnement de hello en définissant le paramètre facultatif hello `isPeekLock` trop**true**.</span><span class="sxs-lookup"><span data-stu-id="32d3f-174">By default, messages are deleted from hello subscription as they are read; however, you can read (peek) and lock hello message without deleting it from hello subscription by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="32d3f-175">Hello par défaut de lecture et de suppression de message de type hello comme partie de l’opération de réception est le modèle le plus simple hello et fonctionne mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec.</span><span class="sxs-lookup"><span data-stu-id="32d3f-175">hello default behavior of reading and deleting hello message as part of the receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="32d3f-176">toounderstand, envisagez un scénario dans lequel la hello problèmes consommateur reçoit la demande et puis se bloque avant de le traiter.</span><span class="sxs-lookup"><span data-stu-id="32d3f-176">toounderstand this, consider a scenario in which the consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="32d3f-177">Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.</span><span class="sxs-lookup"><span data-stu-id="32d3f-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="32d3f-178">Si hello `isPeekLock` paramètre est défini trop**true**, hello réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants.</span><span class="sxs-lookup"><span data-stu-id="32d3f-178">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="32d3f-179">Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="32d3f-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span>
<span data-ttu-id="32d3f-180">Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il exécute hello deuxième étape du processus de réception en appelant **deleteMessage** méthode et en fournissant le message toobe supprimé en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="32d3f-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of the receive process by calling **deleteMessage** method and providing the message toobe deleted as a parameter.</span></span> <span data-ttu-id="32d3f-181">Hello **deleteMessage** méthode marquer le message de type hello comme ayant été consommé et le supprimer de l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="32d3f-181">hello **deleteMessage** method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="32d3f-182">Hello exemple suivant montre comment les messages peuvent être reçus et traités à l’aide de `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="32d3f-182">hello following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="32d3f-183">Hello exemple reçoit d’abord et supprime un message de salutation 'LowMessages' abonnement, puis reçoit un message à l’aide de hello 'HighMessages' abonnement `isPeekLock` définir tootrue.</span><span class="sxs-lookup"><span data-stu-id="32d3f-183">hello example first receives and deletes a message from hello 'LowMessages' subscription, and then receives a message from hello 'HighMessages' subscription using `isPeekLock` set tootrue.</span></span> <span data-ttu-id="32d3f-184">Il supprime ensuite à l’aide du message hello `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="32d3f-184">It then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="32d3f-185">Comment toohandle application tombe en panne et messages illisibles</span><span class="sxs-lookup"><span data-stu-id="32d3f-185">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="32d3f-186">Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message.</span><span class="sxs-lookup"><span data-stu-id="32d3f-186">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="32d3f-187">Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlockMessage` méthode sur le **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="32d3f-187">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="32d3f-188">Cette opération provoquent Service Bus toounlock du message au sein de l’abonnement de hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.</span><span class="sxs-lookup"><span data-stu-id="32d3f-188">This will cause Service Bus toounlock the message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="32d3f-189">Il existe également un délai d’attente d’un message verrouillé dans l’abonnement, et en cas d’un message de type hello tooprocess avant application hello hello expiration délai de verrouillage (par exemple, si de l’application hello se bloque), puis le Service Bus déverrouille le message de type hello automatiquement et le rend disponible toobe de nouveau reçu.</span><span class="sxs-lookup"><span data-stu-id="32d3f-189">There is also a timeout associated with a message locked within the subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="32d3f-190">Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `deleteMessage` méthode est appelée, puis le message de type hello sera redistribué toohello application lors de son redémarrage.</span><span class="sxs-lookup"><span data-stu-id="32d3f-190">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="32d3f-191">Cela est souvent appelé *au moins une fois le traitement*, autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué.</span><span class="sxs-lookup"><span data-stu-id="32d3f-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="32d3f-192">Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message.</span><span class="sxs-lookup"><span data-stu-id="32d3f-192">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="32d3f-193">Cela est souvent obtenue grâce à la **MessageId** propriété de message de type hello, qui reste constante entre les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="32d3f-193">This is often achieved using the **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="32d3f-194">Suppression de rubriques et d'abonnements</span><span class="sxs-lookup"><span data-stu-id="32d3f-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="32d3f-195">Rubriques et les abonnements sont persistants et doivent être explicitement supprimés via hello [portail Azure] [ Azure portal] ou par programme.</span><span class="sxs-lookup"><span data-stu-id="32d3f-195">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="32d3f-196">Hello exemple suivant montre comment la rubrique de hello toodelete nommé `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="32d3f-196">hello following example demonstrates how toodelete hello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="32d3f-197">Suppression d’une rubrique supprime également tous les abonnements qui sont inscrits auprès de rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="32d3f-197">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="32d3f-198">Les abonnements peuvent aussi être supprimés de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="32d3f-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="32d3f-199">L’exemple suivant montre comment toodelete un abonnement nommé `HighMessages` de hello `MyTopic` rubrique :</span><span class="sxs-lookup"><span data-stu-id="32d3f-199">The following example shows how toodelete a subscription named `HighMessages` from hello `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="32d3f-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="32d3f-200">Next Steps</span></span>
<span data-ttu-id="32d3f-201">Maintenant que vous avez appris les notions de base de hello des rubriques Service Bus, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="32d3f-201">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="32d3f-202">Consultez [Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="32d3f-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="32d3f-203">Référence d’API pour [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="32d3f-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="32d3f-204">Visitez hello [Azure SDK pour le nœud] [ Azure SDK for Node] référentiel sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="32d3f-204">Visit hello [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[créer et déployer un tooan d’application Node.js Site Web Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
