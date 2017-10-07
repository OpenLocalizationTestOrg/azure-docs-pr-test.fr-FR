---
title: "aaaAzure fonctions Service Bus déclencheurs et les liaisons | Documents Microsoft"
description: "Comprendre comment toouse Azure Service Bus déclenche et les liaisons dans les fonctions d’Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a>Liaisons Service Bus Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment tooconfigure et de travailler avec des liaisons de Service Bus de Azure dans les fonctions d’Azure. 

Azure Functions prend en charge les liaisons de déclencheur et de sortie pour les files d’attente et les rubriques Service Bus.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a>Déclencheur Service Bus
Utilisez hello Service Bus déclencheur toorespond toomessages à partir d’une file d’attente du Bus de Service ou une rubrique. 

déclencheurs de file d’attente et rubrique Service Bus Hello sont définis par hello objets JSON Bonjour suivants `bindings` tableau de function.json :

* Déclencheur de *file d’attente* :

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* Déclencheur de *rubrique* :

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

Notez hello suivantes :

* Pour `connection`, [créer un paramètre d’application dans votre application de la fonction](functions-how-to-use-azure-function-app-settings.md) qui contient l’espace de noms de Service Bus hello connexion chaîne tooyour, puis spécifiez le nom de hello du paramètre d’application hello Bonjour `connection` propriété dans votre déclencheur. Obtenir de chaîne de connexion hello en suivant les étapes de hello présentés au [obtenir des informations d’identification de gestion hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  chaîne de connexion Hello doit être d’un espace de noms Service Bus, tooa non limité, la file d’attente spécifique ou une rubrique.
  Si vous laissez `connection` vide, le déclencheur de hello part du principe qu’une chaîne de connexion de Service Bus par défaut est spécifiée dans une application de paramètre nommé `AzureWebJobsServiceBus`.
* Pour `accessRights`, les valeurs disponibles sont `manage` et `listen`. valeur par défaut Hello est `manage`, ce qui signifie que hello `connection` a hello **gérer** autorisation. Si vous utilisez une chaîne de connexion qui n’a pas de hello **gérer** de jeu d’autorisations, `accessRights` trop`listen`. Dans le cas contraire, les fonctions hello runtime risque d’échouer lors de la tentative toodo les opérations qui nécessitent les droits de gestion.

## <a name="trigger-behavior"></a>Comportement du déclencheur
* **Modèle de thread unique** - par défaut, le processus d’exécution de fonctions hello plusieurs messages simultanément. toodirect hello runtime tooprocess uniquement une file d’attente ou rubrique message unique à la fois, définissez `serviceBus.maxConcurrentCalls` too1 dans *host.json*. 
  Pour plus d’informations sur *host.json*, consultez [Structure de dossiers](functions-reference.md#folder-structure) et [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).
* **Gestion des messages incohérents** - Service Bus assure sa propre gestion des messages incohérents. Il est impossible de la contrôler ou de la configurer dans la configuration ou le code d’Azure Functions. 
* **Comportement de PeekLock** -hello fonctions runtime reçoit un message dans [ `PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) et appelle `Complete` sur le message de type hello si hello est terminée avec succès, ou des appels `Abandon` si hello Échec de la fonction. 
  Si la fonction hello s’exécute plus longtemps que hello `PeekLock` délai d’attente, les verrous hello est automatiquement renouvelée.

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Utilisation du déclencheur
Cette section vous montre comment toouse votre Service Bus déclencher dans votre code de fonction. 

En c# et F #, message d’appel du déclencheur Service Bus peut être désérialisé tooany Hello les types d’entrée suivants :

* `string` - utile pour les messages de type chaîne
* `byte[]` - utile pour les données binaires
* N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour les données JSON sérialisées.
  Si vous déclarez un type d’entrée personnalisé, tel que `CustomType`, les fonctions Azure essaie de données JSON de hello toodeserialize vers le type spécifié.
* `BrokeredMessage`-permet de vous hello désérialisé message avec hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) (méthode).

Dans Node.js, message d’appel du déclencheur Service Bus est passé dans la fonction hello comme une chaîne ou un objet JSON.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Exemple de déclencheur
Supposons que vous avez hello suivant function.json :

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

Voir exemple hello spécifiques au langage qui traite un message de la file d’attente Service Bus.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Exemple de déclencheur en C# #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Exemple de déclencheur en F# #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Exemple de déclencheur en Node.js

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a>Liaison de sortie Service Bus
Hello sortie de file d’attente et rubrique Service Bus pour une fonction utiliser hello objets JSON Bonjour suivants `bindings` tableau de function.json :

* Sortie de *file d’attente* :

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* Sortie de *rubrique* :

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

Notez hello suivantes :

* Pour `connection`, [créer un paramètre d’application dans votre application de la fonction](functions-how-to-use-azure-function-app-settings.md) qui contient l’espace de noms de Service Bus hello connexion chaîne tooyour, puis spécifiez le nom de hello du paramètre d’application hello Bonjour `connection` propriété dans votre sortie. liaison. Obtenir de chaîne de connexion hello en suivant les étapes de hello présentés au [obtenir des informations d’identification de gestion hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  chaîne de connexion Hello doit être d’un espace de noms Service Bus, tooa non limité, la file d’attente spécifique ou une rubrique.
  Si vous laissez `connection` vide, hello liaison de sortie suppose qu’une chaîne de connexion de Service Bus par défaut est spécifiée dans une application de paramètre nommé `AzureWebJobsServiceBus`.
* Pour `accessRights`, les valeurs disponibles sont `manage` et `listen`. valeur par défaut Hello est `manage`, ce qui signifie que hello `connection` a hello **gérer** autorisation. Si vous utilisez une chaîne de connexion qui n’a pas de hello **gérer** de jeu d’autorisations, `accessRights` trop`listen`. Dans le cas contraire, les fonctions hello runtime risque d’échouer lors de la tentative toodo les opérations qui nécessitent les droits de gestion.

<a name="outputusage"></a>

## <a name="output-usage"></a>Utilisation en sortie
En c# et F #, les fonctions Azure peut créer un message de la file d’attente Service Bus à partir d’un des types suivants de hello :

* N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) - la définition du paramètre ressemble à `out T paramName` (C#).
  Fonctions désérialise un objet de hello dans un message JSON. Si la valeur de sortie hello est null lorsque hello fonction s’arrête, fonctions crée le message de salutation avec un objet null.
* `string` - La définition du paramètre ressemble à `out string paraName` (C#). Si la valeur du paramètre hello est non null lorsque hello fonction s’arrête, fonctions crée un message.
* `byte[]` - La définition du paramètre ressemble à `out byte[] paraName` (C#). Si la valeur du paramètre hello est non null lorsque hello fonction s’arrête, fonctions crée un message.
* `BrokeredMessage` - La définition du paramètre ressemble à `out BrokeredMessage paraName` (C#). Si la valeur du paramètre hello est non null lorsque hello fonction s’arrête, fonctions crée un message.

Pour créer plusieurs messages dans une fonction C#, vous pouvez utiliser `ICollector<T>` ou `IAsyncCollector<T>`. Un message est créé lorsque vous appelez hello `Add` (méthode).

Dans Node.js, vous pouvez affecter une chaîne, un tableau d’octets ou un objet de Javascript (désérialisé dans JSON) trop`context.binding.<paramName>`.

<a name="outputsample"></a>

## <a name="output-sample"></a>Exemple de sortie
Supposons que vous avez hello suivant function.json, qui définit une sortie de la file d’attente Service Bus :

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

Voir exemple hello spécifiques au langage qui envoie une file d’attente service bus de messages toohello.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.JS](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Exemple de sortie en C# #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

Ou, toocreate plusieurs messages :

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Exemple de sortie en F# #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Exemple de sortie en Node.js

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

Ou, toocreate plusieurs messages :

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

