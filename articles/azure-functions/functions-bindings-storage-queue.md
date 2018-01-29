---
title: "Liaisons de stockage File d’attente Azure pour Azure Functions"
description: "Comprendre comment utiliser la liaison de sortie et le déclencheur Stockage File d’attente Azure dans Azure Functions."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/23/2017
ms.author: glenga
ms.openlocfilehash: 2ca511bf0c145878cc80bdbae694f581fd487820
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2018
---
# <a name="azure-queue-storage-bindings-for-azure-functions"></a>Liaisons de stockage File d’attente Azure pour Azure Functions

Cet article explique comment utiliser les liaisons Stockage File d’attente Azure dans Azure Functions. Azure Functions prend en charge les liaisons de déclencheur et de sortie pour les files d’attente.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="trigger"></a>Déclencheur

Utilisez le déclencheur de file d’attente pour démarrer une fonction lorsqu’un nouvel élément est reçu sur une file d’attente. Le message de file d’attente est fourni comme entrée pour la fonction.

## <a name="trigger---example"></a>Déclencheur - exemple

Consultez l’exemple propre à un langage particulier :

* [C#](#trigger---c-example)
* [Script C# (.csx)](#trigger---c-script-example)
* [JavaScript](#trigger---javascript-example)

### <a name="trigger---c-example"></a>Déclencheur - exemple C#

L’exemple suivant montre un code de [fonction C#](functions-dotnet-class-library.md) qui interroge la file d’attente `myqueue-items` et écrit un journal chaque fois qu’un élément de la file d’attente est traité.

```csharp
public static class QueueFunctions
{
    [FunctionName("QueueTrigger")]
    public static void QueueTrigger(
        [QueueTrigger("myqueue-items")] string myQueueItem, 
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}
```

### <a name="trigger---c-script-example"></a>Déclencheur - exemple Script C#

L’exemple suivant montre une liaison de déclencheur d’objet blob dans un fichier *function.json* et un code de [script C# (.csx)](functions-reference-csharp.md) qui utilise cette liaison. La fonction interroge la file d’attente `myqueue-items` et écrit un journal chaque fois qu’un élément de la file d’attente est traité.

Voici le fichier *function.json* :

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionAppSetting"
        }
    ]
}
```

La section [configuration](#trigger---configuration) décrit ces propriétés.

Voici le code Script C# :

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

La section [utilisation](#trigger---usage) explique `myQueueItem`, qui est nommé par la propriété `name` dans function.json.  La [section sur les métadonnées de message](#trigger---message-metadata) détaille toutes les autres variables indiquées.

### <a name="trigger---javascript-example"></a>Déclencheur - exemple JavaScript

L’exemple suivant montre une liaison de déclencheur d’objet blob dans un fichier *function.json* et une [fonction JavaScript](functions-reference-node.md) qui utilise la liaison. La fonction interroge la file d’attente `myqueue-items` et écrit un journal chaque fois qu’un élément de la file d’attente est traité.

Voici le fichier *function.json* :

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionAppSetting"
        }
    ]
}
```

La section [configuration](#trigger---configuration) décrit ces propriétés.

Voici le code JavaScript :

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id =', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

La section [utilisation](#trigger---usage) explique `myQueueItem`, qui est nommé par la propriété `name` dans function.json.  La [section sur les métadonnées de message](#trigger---message-metadata) détaille toutes les autres variables indiquées.

## <a name="trigger---attributes"></a>Déclencheur - attributs
 
Dans les [bibliothèques de classes C#](functions-dotnet-class-library.md), utilisez les attributs suivants pour configurer un déclencheur de file d’attente :

* [QueueTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueTriggerAttribute.cs), défini dans le package NuGet [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs)

  Le constructeur de l’attribut prend le nom de la file d’attente à surveiller, comme illustré dans l’exemple suivant :

  ```csharp
  [FunctionName("QueueTrigger")]
  public static void Run(
      [QueueTrigger("myqueue-items")] string myQueueItem, 
      TraceWriter log)
  {
      ...
  }
  ```

  Vous pouvez définir la propriété `Connection` pour spécifier le compte de stockage à utiliser, comme indiqué dans l’exemple suivant :

  ```csharp
  [FunctionName("QueueTrigger")]
  public static void Run(
      [QueueTrigger("myqueue-items", Connection = "StorageConnectionAppSetting")] string myQueueItem, 
      TraceWriter log)
  {
      ....
  }
  ```
 
  Pour obtenir un exemple complet, consultez [Déclencheur - exemple C#](#trigger---c-example).

* [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs), défini dans le package NuGet [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs)

  Fournit une autre manière de spécifier le compte de stockage à utiliser. Le constructeur prend le nom d’un paramètre d’application comportant une chaîne de connexion de stockage. L’attribut peut être appliqué au niveau du paramètre, de la méthode ou de la classe. L’exemple suivant montre le niveau de la classe et celui de la méthode :

  ```csharp
  [StorageAccount("ClassLevelStorageAppSetting")]
  public static class AzureFunctions
  {
      [FunctionName("QueueTrigger")]
      [StorageAccount("FunctionLevelStorageAppSetting")]
      public static void Run( //...
  {
      ...
  }
  ```

Le compte de stockage à utiliser est déterminé dans l’ordre suivant :

* La propriété `Connection` de l’attribut `QueueTrigger`.
* L’attribut `StorageAccount` appliqué au même paramètre que l’attribut `QueueTrigger`.
* L’attribut `StorageAccount` appliqué à la fonction.
* L’attribut `StorageAccount` appliqué à la classe.
* Le paramètre d’application « AzureWebJobsStorage ».

## <a name="trigger---configuration"></a>Déclencheur - configuration

Le tableau suivant décrit les propriétés de configuration de liaison que vous définissez dans le fichier *function.json* et l’attribut `QueueTrigger`.

|Propriété function.json | Propriété d’attribut |DESCRIPTION|
|---------|---------|----------------------|
|**type** | n/a| Cette propriété doit être définie sur `queueTrigger`. Cette propriété est définie automatiquement lorsque vous créez le déclencheur dans le portail Azure.|
|**direction**| n/a | Dans le fichier *function.json* uniquement. Cette propriété doit être définie sur `in`. Cette propriété est définie automatiquement lorsque vous créez le déclencheur dans le portail Azure. |
|**name** | n/a |Nom de la variable qui représente la file d’attente dans le code de la fonction.  | 
|**queueName** | **QueueName**| Nom de la file d’attente à interroger. | 
|**Connexion** | **Connection** |Nom d’un paramètre d’application comportant la chaîne de connexion de stockage à utiliser pour cette liaison. Si le nom du paramètre d’application commence par « AzureWebJobs », vous ne pouvez spécifier que le reste du nom ici. Par exemple, si vous définissez `connection` sur « MyStorage », le runtime Functions recherche un paramètre d’application qui est nommé « AzureWebJobsMyStorage ». Si vous laissez `connection` vide, le runtime Functions utilise la chaîne de connexion de stockage par défaut dans le paramètre d’application nommé `AzureWebJobsStorage`.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="trigger---usage"></a>Déclencheur - utilisation
 
Dans C# et Script C#, accédez aux données d’objets blob en utilisant un paramètre de méthode comme `Stream paramName`. Dans Script C#, `paramName` est la valeur spécifiée dans la propriété `name` de *function.json*. Vous pouvez lier aux types suivants :

* Objet POCO - Le runtime Functions désérialise une charge utile JSON en objet POCO. 
* `string`
* `byte[]`
* [CloudQueueMessage]

Dans JavaScript, utilisez `context.bindings.<name>` pour accéder à la charge utile de l’élément de file d’attente. Si la charge utile est JSON, elle est désérialisée en objet.

## <a name="trigger---message-metadata"></a>Déclencheur - métadonnées de message

Le déclencheur de file d’attente fournit plusieurs propriétés de métadonnées. Ces propriétés peuvent être utilisées dans les expressions de liaison dans d’autres liaisons ou en tant que paramètres dans votre code. Les valeurs ont la même sémantique que [CloudQueueMessage](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage).

|Propriété|type|DESCRIPTION|
|--------|----|-----------|
|`QueueTrigger`|`string`|Charge utile de file d’attente (s’il s’agit d’une chaîne valide). Si la charge utile du message de file d’attente est une chaîne, `QueueTrigger` a la même valeur que la variable nommée par la propriété `name` dans *function.json*.|
|`DequeueCount`|`int`|Nombre de fois que ce message a été enlevé de la file d’attente.|
|`ExpirationTime`|`DateTimeOffset?`|Heure à laquelle le message expire.|
|`Id`|`string`|ID de message de la file d’attente.|
|`InsertionTime`|`DateTimeOffset?`|Heure à laquelle le message a été ajouté à la file d’attente.|
|`NextVisibleTime`|`DateTimeOffset?`|Heure à laquelle le message sera de nouveau visible.|
|`PopReceipt`|`string`|Réception pop du message.|

## <a name="trigger---poison-messages"></a>Déclencheur - messages incohérents

En cas d’échec d’une fonction de déclenchement de file d’attente, Azure Functions réessaie la fonction jusqu’à cinq fois (première tentative comprise) pour un message de file d’attente donné. Si les cinq tentatives échouent, le runtime Functions ajoute un message à une file d’attente nommée *&lt;nom_file_d’attente_d’origine>-poison*. Vous pouvez écrire une fonction pour traiter les messages de la file d’attente de messages incohérents en les consignant dans un journal ou en envoyant une notification signalant qu’une attention manuelle est nécessaire.

Pour gérer manuellement les messages incohérents, vérifiez la propriété [dequeueCount](#trigger---message-metadata) dans le message de file d’attente.

## <a name="trigger---hostjson-properties"></a>Déclencheur - propriétés de host.json

Le fichier [host.json](functions-host-json.md#queues) contient les paramètres qui contrôlent le comportement du déclencheur de file d’attente.

[!INCLUDE [functions-host-json-queues](../../includes/functions-host-json-queues.md)]

## <a name="output"></a>Sortie

Utilisez la liaison de sortie Stockage File d’attente Azure pour écrire des messages dans une file d’attente.

## <a name="output---example"></a>Sortie - exemple

Consultez l’exemple propre à un langage particulier :

* [C#](#output---c-example)
* [Script C# (.csx)](#output---c-script-example)
* [JavaScript](#output---javascript-example)

### <a name="output---c-example"></a>Sortie - exemple C#

L’exemple suivant montre un code [de fonction C#](functions-dotnet-class-library.md) qui crée un message de file d’attente pour chaque requête HTTP reçue.

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }
}
```

### <a name="output---c-script-example"></a>Sortie - exemple Script C#

L’exemple suivant montre une liaison de déclencheur d’objet blob dans un fichier *function.json* et un code de [script C# (.csx)](functions-reference-csharp.md) qui utilise cette liaison. La fonction crée un élément de file d’attente avec une charge utile POCO pour chaque requête HTTP reçue.

Voici le fichier *function.json* :

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
      "connection": "MyStorageConnectionAppSetting",
    }
  ]
}
``` 

La section [configuration](#output---configuration) décrit ces propriétés.

Voici le code Script C# qui crée un message de file d’attente unique :

```cs
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

Vous pouvez envoyer plusieurs messages à la fois en utilisant un paramètre `ICollector` ou `IAsyncCollector`. Voici le code Script C# qui envoie plusieurs messages, l’un avec les données de requête HTTP, et l’autre avec des valeurs codées en dur :

```cs
public static void Run(
    CustomQueueMessage input, 
    ICollector<CustomQueueMessage> myQueueItem, 
    TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

### <a name="output---javascript-example"></a>Sortie - exemple JavaScript

L’exemple suivant montre une liaison de déclencheur d’objet blob dans un fichier *function.json* et une [fonction JavaScript](functions-reference-node.md) qui utilise la liaison. La fonction crée un élément de file d’attente pour chaque requête HTTP reçue.

Voici le fichier *function.json* :

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
      "connection": "MyStorageConnectionAppSetting",
    }
  ]
}
``` 

La section [configuration](#output---configuration) décrit ces propriétés.

Voici le code JavaScript :

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

Vous pouvez envoyer plusieurs messages à la fois en définissant un tableau de messages pour la liaison de sortie `myQueueItem`. Le code JavaScript suivant envoie deux messages de file d’attente avec des valeurs codées en dur pour chaque requête HTTP reçue.

```javascript
module.exports = function(context) {
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="output---attributes"></a>Sortie - attributs
 
Dans les [bibliothèques de classes C#](functions-dotnet-class-library.md), utilisez l’attribut [QueueAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs) qui est défini dans le package NuGet [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs).

L’attribut s’applique à un paramètre `out` ou à la valeur de retour de la fonction. Le constructeur de l’attribut prend le nom de la file d’attente, comme illustré dans l’exemple suivant :

```csharp
[FunctionName("QueueOutput")]
[return: Queue("myqueue-items")]
public static string Run([HttpTrigger] dynamic input,  TraceWriter log)
{
    ...
}
```

Vous pouvez définir la propriété `Connection` pour spécifier le compte de stockage à utiliser, comme indiqué dans l’exemple suivant :

```csharp
[FunctionName("QueueOutput")]
[return: Queue("myqueue-items", Connection = "StorageConnectionAppSetting")]
public static string Run([HttpTrigger] dynamic input,  TraceWriter log)
{
    ...
}
```

Pour obtenir un exemple complet, consultez [Sortie - exemple C#](#output---c-example).

Vous pouvez utiliser l’attribut `StorageAccount` pour spécifier le compte de stockage au niveau de la classe, de la méthode ou du paramètre. Pour plus d’informations, consultez [Déclencheur - attributs](#trigger---attribute).

## <a name="output---configuration"></a>Sortie - configuration

Le tableau suivant décrit les propriétés de configuration de liaison que vous définissez dans le fichier *function.json* et l’attribut `Queue`.

|Propriété function.json | Propriété d’attribut |DESCRIPTION|
|---------|---------|----------------------|
|**type** | n/a | Cette propriété doit être définie sur `queue`. Cette propriété est définie automatiquement lorsque vous créez le déclencheur dans le portail Azure.|
|**direction** | n/a | Cette propriété doit être définie sur `out`. Cette propriété est définie automatiquement lorsque vous créez le déclencheur dans le portail Azure. |
|**name** | n/a | Nom de la variable qui représente la file d’attente dans le code de la fonction. La valeur doit être `$return` pour faire référence à la valeur de retour de la fonction.| 
|**queueName** |**QueueName** | Nom de la file d’attente. | 
|**Connexion** | **Connection** |Nom d’un paramètre d’application comportant la chaîne de connexion de stockage à utiliser pour cette liaison. Si le nom du paramètre d’application commence par « AzureWebJobs », vous ne pouvez spécifier que le reste du nom ici. Par exemple, si vous définissez `connection` sur « MyStorage », le runtime Functions recherche un paramètre d’application qui est nommé « AzureWebJobsMyStorage ». Si vous laissez `connection` vide, le runtime Functions utilise la chaîne de connexion de stockage par défaut dans le paramètre d’application nommé `AzureWebJobsStorage`.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="output---usage"></a>Sortie - utilisation
 
En C# et Script C#, écrivez un message de file d’attente unique en utilisant un paramètre de méthode tel que `out T paramName`. Dans Script C#, `paramName` est la valeur spécifiée dans la propriété `name` de *function.json*. Vous pouvez utiliser le type de retour de la méthode au lieu d’un paramètre `out`, et `T` peut être un des types suivants :

* Un objet POCO sérialisable au format JSON
* `string`
* `byte[]`
* [CloudQueueMessage] 

En C# et Script C#, écrivez plusieurs messages de file d’attente à l’aide d’un des types suivants : 

* `ICollector<T>` ou `IAsyncCollector<T>`
* [CloudQueue](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

Dans les fonctions JavaScript, utilisez `context.bindings.<name>` pour accéder au message de file d’attente de sortie. Vous pouvez utiliser une chaîne ou un objet sérialisable JSON pour la charge utile de l’élément de file d’attente.

## <a name="next-steps"></a>étapes suivantes

> [!div class="nextstepaction"]
> [Accéder à un guide de démarrage rapide qui utilise un déclencheur de stockage de file d’attente](functions-create-storage-queue-triggered-function.md)

> [!div class="nextstepaction"]
> [Accéder à un didacticiel qui utilise une liaison de sortie de stockage de file d’attente](functions-integrate-storage-queue-output-binding.md)

> [!div class="nextstepaction"]
> [En savoir plus sur les déclencheurs et les liaisons Azure Functions](functions-triggers-bindings.md)

<!-- LINKS -->

[CloudQueueMessage]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
