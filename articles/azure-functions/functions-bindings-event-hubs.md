---
title: "Liaisons d’Event Hubs Azure Functions | Microsoft Docs"
description: "Découvrez comment utiliser des liaisons Azure Event Hubs dans Azure Functions."
services: functions
documentationcenter: na
author: wesmc7777
manager: cfowler
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/20/2017
ms.author: wesmc
ms.openlocfilehash: 85eb6985ef3579b1b2313db3ce5f91c3471da72f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="azure-functions-event-hubs-bindings"></a>Liaisons d’Event Hubs Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment configurer et utiliser des liaisons [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) pour Azure Functions.
Azure Functions prend en charge des liaisons de déclencheur et de sortie pour des Event Hubs.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Si vous débutez avec Azure Event Hubs, consultez la [vue d’ensemble d’Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).

<a name="trigger"></a>

## <a name="event-hub-trigger"></a>Déclencheur Event Hubs
Utilisez le déclencheur Event Hubs pour répondre à un événement envoyé à un flux d’événements d’un hub d’événements. Vous devez disposer de l’accès en lecture au hub d’événements pour configurer le déclencheur.

Le déclencheur Event Hubs d’une fonction utilise l’objet JSON suivant dans le tableau `bindings` de function.json :

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of the event hub>",
    "consumerGroup": "Consumer group to use - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

`consumerGroup` est une propriété facultative utilisée pour définir le [groupe de consommateurs](../event-hubs/event-hubs-features.md#event-consumers) utilisé pour l’abonnement à des événements dans le hub. En cas d’omission, le groupe de consommateurs `$Default` est utilisé.  
`connection` doit être le nom d’un paramètre d’application qui contient la chaîne de connexion à l’espace de noms du hub d’événements.
Copiez cette chaîne de connexion en cliquant sur le bouton **Informations de connexion** pour *l’espace de noms*, et non pour le hub d’événements lui-même. Cette chaîne de connexion doit avoir au moins des droits de lecture pour activer le déclencheur.

Vous pouvez fournir des [paramètres supplémentaires](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) dans un fichier host.json pour affiner les déclencheurs Event Hubs.  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Utilisation du déclencheur
Quand une fonction de déclenchement Event Hubs est déclenchée, le message qui le déclenche est passé à la fonction en tant que chaîne.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Exemple de déclencheur
Supposez que le tableau `bindings` de function.json contient le déclencheur Event Hubs suivant :

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Consultez l’exemple dans le langage de votre choix pour voir comment enregistrer le corps du message du déclencheur de hub d’événements.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Exemple de déclencheur en C# #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Vous pouvez également recevoir l’événement en tant qu’objet [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata), qui vous permet d’accéder aux métadonnées de l’événement.

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

Pour recevoir les événements dans un lot, modifiez la signature de méthode sur `string[]` ou `EventData[]`.

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Exemple de déclencheur en F# #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Exemple de déclencheur en Node.js

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a>Liaison de sortie Event Hubs
Utilisez la liaison de sortie Event Hubs pour écrire des événements dans un flux d’événements du hub d’événements. Vous devez disposer de l’autorisation d’envoi à un hub d’événements pour y écrire les événements.

La liaison de sortie utilise l’objet JSON suivant dans le tableau `bindings` de function.json :

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

`connection` doit être le nom d’un paramètre d’application qui contient la chaîne de connexion à l’espace de noms du hub d’événements.
Copiez cette chaîne de connexion en cliquant sur le bouton **Informations de connexion** pour *l’espace de noms*, et non pour le hub d’événements lui-même. Cette chaîne de connexion doit disposer d’autorisations d’envoi pour envoyer le message au flux d’événements.

## <a name="output-usage"></a>Utilisation en sortie
Cette section vous montre comment utiliser la liaison de sortie Event Hubs dans le code de votre fonction.

Vous pouvez générer des messages au concentrateur d’événements configuré avec les types de paramètres suivants :

* `out string`
* `ICollector<string>`(pour envoyer plusieurs messages)
* `IAsyncCollector<string>` (version asynchrone de `ICollector<T>`)

<a name="outputsample"></a>

## <a name="output-sample"></a>Exemple de sortie
Supposez que le tableau `bindings` de function.json contient la liaison de sortie Event Hubs suivante :

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Consultez l’exemple dans le langage de votre choix pour voir comment écrire un événement dans le flux d’événements.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.JS](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Exemple de sortie en C# #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

Ou, pour créer plusieurs messages :

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Exemple de sortie en F# #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a>Exemple de sortie pour Node.js

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

Ou, pour envoyer plusieurs messages,

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
