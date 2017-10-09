---
title: "liaisons de stockage de file d’attente de fonctions aaaAzure | Documents Microsoft"
description: "Comprendre comment toouse le stockage Azure déclenche et les liaisons dans les fonctions d’Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a>Liaisons de stockage de file d’attente d’Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article décrit comment tooconfigure et code liaisons de stockage de file d’attente Azure dans les fonctions d’Azure. Azure Functions prend en charge les liaisons de déclencheur et de sortie pour les files d’attente Azure. Pour les fonctionnalités qui sont disponibles dans toutes les liaisons, consultez [Concepts des déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a>Déclencheur de stockage de file d’attente
déclencheur de stockage de file d’attente Azure Hello permet toomonitor un stockage de file d’attente pour les nouveaux messages et réagit toothem. 

Définir un déclencheur de la file d’attente à l’aide de hello **intégrer** portail de fonctions hello. portail Hello crée hello définition Bonjour **liaisons** section de *function.json*:

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* Hello `connection` propriété doit contenir le nom hello d’un paramètre d’application qui contient une chaîne de connexion de stockage. Bonjour portail Azure, hello éditeur standard Bonjour **intégrer** onglet configure ce paramètre d’application pour vous lorsque vous sélectionnez un compte de stockage.

Paramètres supplémentaires peuvent être fournies dans un [host.json fichier](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther affiner les déclencheurs de stockage de file d’attente. Par exemple, vous pouvez modifier la fréquence d’interrogation de file d’attente de hello en host.json.

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a>Utilisation d’un déclencheur de file d’attente
Dans les fonctions de Node.js, accéder à l’aide des données de file d’attente hello `context.bindings.<name>`.


Dans les fonctions de .NET, accéder à l’aide d’un paramètre de méthode comme charge utile de file d’attente hello `CloudQueueMessage paramName`. Ici, `paramName` est la valeur hello spécifiée Bonjour [configuration du déclencheur](#trigger). message de file d’attente d’appel peut être désérialisé tooany Hello les types suivants :

* Objet POCO. Utilisez si la charge utile de file d’attente hello est un objet JSON. Hello fonctions runtime désérialise la charge utile de hello en objet POCO hello. 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a>Métadonnées de déclencheur de file d’attente
déclencheur de file d’attente Hello fournit plusieurs propriétés de métadonnées. Ces propriétés peuvent être utilisées dans les expressions de liaison dans d’autres liaisons ou en tant que paramètres dans votre code. les valeurs Hello ont hello même sémantique que [ `CloudQueueMessage` ].

* **QueueTrigger** : charge utile de la file d’attente (s’il s’agit d’une chaîne valide)
* **DequeueCount** : type `int`. Bonjour le nombre de fois où que ce message a été dépilé.
* **ExpirationTime** : type `DateTimeOffset?`. temps de Hello ce message hello expire.
* **Id**:type `string`. ID de message de la file d’attente.
* **InsertionTime** : type `DateTimeOffset?`. temps de Hello ce message de type hello a été ajouté à la file d’attente de toohello.
* **NextVisibleTime** : tapez `DateTimeOffset?`. temps de Hello ce message de type hello sera de nouveau visible.
* **PopReceipt** : type `string`. accusé de réception pop du message de type Hello.

Consultez Comment toouse hello dans les métadonnées de file d’attente [exemple de déclencheur](#triggersample).

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Exemple de déclencheur
Supposons que vous avez hello suivant function.json qui définit un déclencheur de la file d’attente :

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

Consultez l’exemple de langage spécifiques hello qui Récupère et enregistre les métadonnées de file d’attente.

* [C#](#triggercsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Exemple de déclencheur en C# #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Exemple de déclencheur en Node.js

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a>Gestion des messages de file d’attente incohérents
En cas d’échec d’une fonction de déclenchement de file d’attente, les fonctions de Azure essaie de nouveau cette fonction des toofive heures pour un message de la file d’attente donnée, y compris hello tout d’abord essayer. Si toutes les cinq tentatives échouent, hello fonctions runtime ajoute un stockage de file d’attente message tooa nommé  *&lt;originalqueuename >-incohérents*. Vous pouvez écrire une fonction tooprocess messages de file d’attente de messages incohérents hello par les enregistrer ou de l’envoi d’une notification qu’attention manuelle est nécessaire. 

les messages incohérents toohandle vérifier manuellement, hello `dequeueCount` de message de file d’attente hello (consultez [métadonnées de file d’attente déclencheur](#meta)).

<a name="output"></a>

## <a name="queue-storage-output-binding"></a>Liaison de sortie de stockage de file d’attente
liaison vous permet de file d’attente de tooa toowrite messages de sortie Hello stockage de file d’attente Azure. 

Définir une file d’attente de liaison de sortie à l’aide de hello **intégrer** portail de fonctions hello. portail Hello crée hello définition Bonjour **liaisons** section de *function.json*:

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* Hello `connection` propriété doit contenir le nom hello d’un paramètre d’application qui contient une chaîne de connexion de stockage. Bonjour portail Azure, hello éditeur standard Bonjour **intégrer** onglet configure ce paramètre d’application pour vous lorsque vous sélectionnez un compte de stockage.

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a>Utilisation d’une liaison de sortie de file d’attente
Dans les fonctions de Node.js, vous accédez à l’aide de file d’attente de sortie hello `context.bindings.<name>`.

Dans les fonctions de .NET, vous pouvez produire tooany Hello les types suivants. Lorsqu’il existe un paramètre de type `T`, `T` doit être un des types de sortie hello pris en charge, tel que `string` ou un POCO.

* `out T` (sérialisé au format JSON)
* `out string`
* `out byte[]`
* `out`[`CloudQueueMessage`] 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

Vous pouvez également utiliser le type de retour de méthode hello comme hello liaison de sortie.

<a name="outputsample"></a>

## <a name="queue-output-sample"></a>Exemple de sortie de file d’attente
suivant de Hello *function.json* définit un déclencheur HTTP avec une file d’attente de liaison de sortie :

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

Consultez l’exemple hello spécifiques au langage qui génère un message de la file d’attente avec une charge utile HTTP entrant hello.

* [C#](#outcsharp)
* [Node.JS](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a>Exemple de sortie de file d’attente en C# #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

utilisation de plusieurs messages, toosend un `ICollector`:

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a>Exemple de sortie de file d’attente en Node.js

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

Ou, toosend plusieurs messages,

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir un exemple d’une fonction qui utilise des déclencheurs de stockage de file d’attente et les liaisons, consultez [créer un service Azure de tooan fonction Azure connecté](functions-create-an-azure-connected-function.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
