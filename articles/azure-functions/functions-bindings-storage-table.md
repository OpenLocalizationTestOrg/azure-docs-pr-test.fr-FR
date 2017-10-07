---
title: liaisons de Table de stockage des fonctions aaaAzure | Documents Microsoft
description: "Comprendre comment les liaisons de stockage Azure toouse dans les fonctions d’Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: 90c2a73329139d4ab3504bc0e2c90370133158bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-storage-table-bindings"></a>Liaisons de table Azure Functions Storage
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment tooconfigure et code le stockage Azure table liaisons dans les fonctions d’Azure. Azure Functions prend en charge les liaisons d’entrée et de sortie pour les tables Azure Storage.

liaison de table de stockage Hello prend en charge hello les scénarios suivants :

* **Lecture d’une seule ligne dans une fonction C# ou Node.js** - Définition de `partitionKey` et `rowKey`. Hello `filter` et `take` propriétés ne sont pas utilisées dans ce scénario.
* **Lecture de plusieurs lignes dans une fonction c#** -hello fonctions runtime fournit un `IQueryable<T>` objet lié toohello table. Le type `T` doit dériver de `TableEntity` ou implémenter `ITableEntity`. Hello `partitionKey`, `rowKey`, `filter`, et `take` propriétés ne sont pas utilisées dans ce scénario, vous pouvez utiliser hello `IQueryable` toodo l’objet de filtrage requis. 
* **Lecture de plusieurs lignes dans une fonction de nœud** - hello définissez `filter` et `take` propriétés. Ne définissez pas `partitionKey` ni `rowKey`.
* **Écrivez une ou plusieurs lignes dans une fonction c#** -hello fonctions runtime fournit un `ICollector<T>` ou `IAsyncCollector<T>` toohello liée, table, où `T` Spécifie le schéma de hello d’entités de hello souhaité tooadd. En général, le type `T` dérive de `TableEntity` ou implémente `ITableEntity`, mais ce n’est pas obligatoire. Hello `partitionKey`, `rowKey`, `filter`, et `take` propriétés ne sont pas utilisées dans ce scénario.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a>Liaison d’entrée d'une table Storage
Hello liaison d’entrée de table de stockage Azure vous permet de toouse une table de stockage dans votre fonction. 

Hello, fonction de tooa d’entrée de table de stockage utilise hello objets JSON Bonjour suivants `bindings` tableau de function.json :

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity tooread - see below>",
    "rowKey": "<RowKey of table entity tooread - see below>",
    "take": "<Maximum number of entities tooread in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

Notez hello suivantes : 

* Utilisez `partitionKey` et `rowKey` tooread ensemble une entité unique. Ces propriétés sont facultatives. 
* `connection`doit contenir nom hello d’un paramètre d’application qui contient une chaîne de connexion de stockage. Bonjour portail Azure, hello éditeur standard Bonjour **intégrer** onglet configure ce paramètre d’application pour vous lorsque vous créez un stockage de compte ou sélectionne un existant. Vous pouvez également [configurer ce paramètre d’application manuellement](functions-how-to-use-azure-function-app-settings.md#settings).  

<a name="inputusage"></a>

## <a name="input-usage"></a>Utilisation en entrée
Dans les fonctions C#, vous liez toohello d’entrée table entité (ou les entités) à l’aide d’un paramètre nommé dans votre signature de fonction, comme `<T> <name>`.
Où `T` est que les données de hello toodeserialize, de type de données de hello et `paramName` est le nom hello spécifié Bonjour [liaison d’entrée](#input). Dans les fonctions de Node.js, vous accéder hello d’entrée table entité (ou les entités) à l’aide de `context.bindings.<name>`.

les données d’entrée Hello pouvant être désérialisées dans les fonctions Node.js ou c#. les objets Hello désérialisé ont `RowKey` et `PartitionKey` propriétés.

Dans les fonctions de c#, vous pouvez également lier tooany Hello les types suivants, et les fonctions hello runtime va tenter de désérialiser trop à l’aide de ce type de données de la table hello :

* Tout type qui implémente `ITableEntity`
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a>Exemple d’entrée
Supposé qu'avoir hello suivant function.json, qui utilise un tooread de déclencheur de file d’attente une seule ligne du tableau. Spécifie Hello JSON `PartitionKey`  
 `RowKey`. `"rowKey": "{queueTrigger}"`Indique que cette clé de ligne hello provient de la chaîne de message de file d’attente hello.

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

Voir exemple hello spécifiques au langage qui lit une entité de table unique.

* [C#](#inputcsharp)
* [F#](#inputfsharp)
* [Node.JS](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Exemple d’entrée en C# #
```csharp
public static void Run(string myQueueItem, Person personEntity, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    log.Info($"Name in Person entity: {personEntity.Name}");
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}
```

<a name="inputfsharp"></a>

### <a name="input-sample-in-f"></a>Exemple d’entrée en F# #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(myQueueItem: string, personEntity: Person) =
    log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
    log.Info(sprintf "Name in Person entity: %s" personEntity.Name)
```

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Exemple d’entrée en Node.js
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a>Liaison de sortie d'une table Storage
liaison vous permet de table de stockage toowrite entités tooa dans votre fonction de sortie Hello table de stockage Azure. 

Hello sortie de table de stockage pour une fonction utilise hello objets JSON Bonjour suivants `bindings` tableau de function.json :

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity toowrite - see below>",
    "rowKey": "<RowKey of table entity toowrite - see below>",
    "connection": "<Name of app setting - see below>",
}
```

Notez hello suivantes : 

* Utilisez `partitionKey` et `rowKey` toowrite ensemble une entité unique. Ces propriétés sont facultatives. Vous pouvez également spécifier `PartitionKey` et `RowKey` lorsque vous créez hello objets d’entité dans votre code de fonction.
* `connection`doit contenir nom hello d’un paramètre d’application qui contient une chaîne de connexion de stockage. Bonjour portail Azure, hello éditeur standard Bonjour **intégrer** onglet configure ce paramètre d’application pour vous lorsque vous créez un stockage de compte ou sélectionne un existant. Vous pouvez également [configurer ce paramètre d’application manuellement](functions-how-to-use-azure-function-app-settings.md#settings). 

<a name="outputusage"></a>

## <a name="output-usage"></a>Utilisation en sortie
Dans les fonctions C#, vous liez sortie de table toohello à l’aide de hello nommé `out` paramètre dans votre signature de fonction, comme `out <T> <name>`, où `T` est que les données de hello tooserialize, de type de données de hello et `paramName` est hello nom que vous avez spécifié dans hello [liaison de sortie](#output). Dans les fonctions Node.js, vous accédez à table hello de sortie à l’aide de `context.bindings.<name>`.

Vous pouvez sérialiser les objets dans les fonctions Node.js ou C#. Dans les fonctions de c#, vous pouvez également lier toohello les types suivants :

* Tout type qui implémente `ITableEntity`
* `ICollector<T>`(toooutput plusieurs entités. Voir l'[exemple](#outcsharp).)
* `IAsyncCollector<T>` (version asynchrone de `ICollector<T>`)
* `CloudTable`(à l’aide de hello SDK Azure Storage. Voir l'[exemple](#readmulti).)

<a name="outputsample"></a>

## <a name="output-sample"></a>Exemple de sortie
suivant de Hello *function.json* et *run.csx* exemple illustre comment toowrite plusieurs entités de table.

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnection",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

Voir exemple hello spécifiques au langage qui crée plusieurs entités de table.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.JS](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Exemple de sortie en C# #
```csharp
public static void Run(string input, ICollector<Person> tableBinding, TraceWriter log)
{
    for (int i = 1; i < 10; i++)
        {
            log.Info($"Adding Person entity {i}");
            tableBinding.Add(
                new Person() { 
                    PartitionKey = "Test", 
                    RowKey = i.ToString(), 
                    Name = "Name" + i.ToString() }
                );
        }

}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}

```
<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Exemple de sortie en F# #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 too10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Exemple de sortie en Node.js
```javascript
module.exports = function (context) {

    context.bindings.tableBinding = [];

    for (var i = 1; i < 10; i++) {
        context.bindings.tableBinding.push({
            PartitionKey: "Test",
            RowKey: i.toString(),
            Name: "Name " + i
        });
    }
    
    context.done();
};
```

<a name="readmulti"></a>

## <a name="sample-read-multiple-table-entities-in-c"></a>Exemple : lire plusieurs entités de table en C#  #
suivant de Hello *function.json* et exemple de code c# lit les entités d’une clé de partition qui est spécifié dans le message de file d’attente hello.

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnection",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

Hello code c# ajoute un toohello référence SDK de stockage Azure afin que le type d’entité hello peut dériver de `TableEntity`.

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;

public static void Run(string myQueueItem, IQueryable<Person> tableBinding, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    foreach (Person person in tableBinding.Where(p => p.PartitionKey == myQueueItem).ToList())
    {
        log.Info($"Name: {person.Name}");
    }
}

public class Person : TableEntity
{
    public string Name { get; set; }
}
```

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

