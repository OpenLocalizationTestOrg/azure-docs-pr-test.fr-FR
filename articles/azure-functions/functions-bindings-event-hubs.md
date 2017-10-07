---
title: "liaisons de concentrateurs d’événements de fonctions aaaAzure | Documents Microsoft"
description: "Comprendre comment les liaisons d’Azure Event Hubs toouse dans les fonctions d’Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
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
ms.openlocfilehash: e864f032ad5ac58d318c9843c3844b5642733a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-event-hubs-bindings"></a>Liaisons d’Event Hubs Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment tooconfigure et utiliser [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) liaisons pour les fonctions d’Azure.
Azure Functions prend en charge des liaisons de déclencheur et de sortie pour des Event Hubs.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Si vous êtes nouveau tooAzure Event Hubs, consultez hello [vue d’ensemble des concentrateurs d’événements](../event-hubs/event-hubs-what-is-event-hubs.md).

<a name="trigger"></a>

## <a name="event-hub-trigger"></a>Déclencheur Event Hubs
Utilisez les concentrateurs d’événements hello déclencher l’événement de tooan de toorespond envoyé le flux d’événements tooan événement hub. Vous devez avoir accès en lecture toohello événement hub tooset déclencheur de hello.

déclencheur de fonction Hello Event Hubs utilise hello objet JSON Bonjour `bindings` tableau de function.json :

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of hello event hub>",
    "consumerGroup": "Consumer group toouse - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

`consumerGroup`est un hello tooset de propriété facultative utilisée [groupe de consommateurs](../event-hubs/event-hubs-features.md#event-consumers) utilisé toosubscribe tooevents dans le hub de hello. Si omis, hello `$Default` groupe de consommateurs est utilisé.  
`connection`doit être nom hello d’un paramètre d’application qui contient l’espace de noms hello connexion chaîne toohello du concentrateur d’événements.
Copier cette chaîne de connexion en cliquant sur hello **les informations de connexion** bouton pour hello *espace de noms*, pas les concentrateur d’événements hello lui-même. Cette chaîne de connexion doit avoir au moins lecture déclencheur de hello tooactivate autorisations.

[Paramètres supplémentaires](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) peut être fournie dans un host.json toofurther fichier fine paramétrer les concentrateurs d’événements déclencheurs.  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Utilisation du déclencheur
Lorsqu’une fonction de déclenchement de concentrateurs d’événements est déclenchée, message de type hello qui le déclenche est passé dans la fonction hello sous forme de chaîne.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Exemple de déclencheur
Supposez que vous avez hello concentrateurs d’événements suivante se déclencher dans hello `bindings` tableau de function.json :

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Voir exemple hello spécifiques au langage qui enregistre le corps du message hello du déclencheur de concentrateur d’événements hello.

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

Vous pouvez également recevoir des événements hello comme un [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) objet, qui vous donne l’accès à toohello métadonnées d’événement.

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

événements tooreceive dans un lot, modifier la signature de méthode hello trop`string[]` ou `EventData[]`.

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
Hello d’utiliser concentrateurs d’événements de sortie de flux d’événements liaison toowrite événements tooan événement hub. Vous devez disposer d’envoi autorisation tooan événement hub toowrite événements tooit.

liaison de sortie Hello utilise hello objet JSON Bonjour `bindings` tableau de function.json :

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

`connection`doit être nom hello d’un paramètre d’application qui contient l’espace de noms hello connexion chaîne toohello du concentrateur d’événements.
Copier cette chaîne de connexion en cliquant sur hello **les informations de connexion** bouton pour hello *espace de noms*, pas les concentrateur d’événements hello lui-même. Cette chaîne de connexion doit avoir le flux d’événements envoi autorisations toosend hello message toohello.

## <a name="output-usage"></a>Utilisation en sortie
Cette section vous montre comment toouse vos Hubs d’événements de sortie de liaison dans votre code de fonction.

Vous pouvez produire concentrateur d’événements de messages toohello configuré avec hello les types de paramètres suivants :

* `out string`
* `ICollector<string>`(toooutput plusieurs messages)
* `IAsyncCollector<string>` (version asynchrone de `ICollector<T>`)

<a name="outputsample"></a>

## <a name="output-sample"></a>Exemple de sortie
Supposons que vous avez hello suivantes concentrateurs d’événements de sortie liaison Bonjour `bindings` tableau de function.json :

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Consultez l’exemple de langage spécifiques hello qui écrit un flux même toohello d’événements.

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

Ou, toocreate plusieurs messages :

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

Ou, toosend plusieurs messages,

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
