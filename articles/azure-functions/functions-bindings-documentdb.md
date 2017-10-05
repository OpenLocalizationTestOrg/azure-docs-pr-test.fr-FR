---
title: Liaisons Cosmos DB Azure Functions | Microsoft Docs
description: "Découvrez comment utiliser des liaisons Azure Cosmos DB dans Azure Functions."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/18/2016
ms.author: glenga
ms.openlocfilehash: de95b0591eb95e76dbb7ba2382e9e14e1f66cda1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a>Liaisons Cosmos DB Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment configurer et coder des liaisons Azure Cosmos DB dans Azure Functions. Azure Functions prend en charge des liaisons d’entrée et de sortie pour Cosmos DB.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Pour plus d’informations sur Cosmos DB, consultez les pages [Présentation de Cosmos DB](../documentdb/documentdb-introduction.md) et [Créer une application de console Cosmos DB](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>Liaison d’entrée d’API DocumentDB
La liaison d’entrée d’API DocumentDB récupère un document Cosmos DB et le transmet au paramètre d’entrée nommé de la fonction. L’ID du document peut être déterminé en fonction du déclencheur qui appelle la fonction. 

La liaison d’entrée d’API DocumentDB possède les propriétés suivantes dans *function.json* :

- `name` : nom de l’identificateur utilisé dans le code de fonctions pour le document.
- `type` : doit être défini sur « documentdb ».
- `databaseName` : la base de données contenant le document.
- `collectionName` : collection contenant le document.
- `id` : ID du document à récupérer. Cette propriété prend en charge les paramètres de liaison ; consultez la section [Lier aux propriétés d’entrée personnalisées dans une expression de liaison](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) de l’article [Concepts des déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md).
- `sqlQuery` : requête SQL Cosmos DB utilisée pour récupérer plusieurs documents. La requête prend en charge les liaisons d’exécution. Par exemple : `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection` : nom du paramètre d’application qui contient votre chaîne de connexion Cosmos DB.
- `direction` : doit être défini sur `"in"`.

Les propriétés `id` et `sqlQuery` ne peuvent pas être spécifiées. Si `id` et `sqlQuery` ne sont pas définis, l’ensemble de la collection est récupéré.

## <a name="using-a-documentdb-api-input-binding"></a>Utiliser une liaison d’entrée d’API DocumentDB

* Dans les fonctions C# et F#, lorsque la fonction se termine correctement, toutes les modifications apportées au document d’entrée par le biais des paramètres d’entrée nommés sont automatiquement conservées. 
* Dans les fonctions JavaScript, les mises à jour ne sont pas effectuées une fois la fonction terminée. Utilisez plutôt `context.bindings.<documentName>In` et `context.bindings.<documentName>Out` pour effectuer les mises à jour. Consultez [l’exemple JavaScript](#injavascript).

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>Exemple d’entrée pour un seul document
Supposez que le tableau `bindings` de function.json contient la liaison d’entrée d’API DocumentDB suivante :

```json
{
  "name": "inputDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "id" : "{queueTrigger}",
  "connection": "MyAccount_COSMOSDB",     
  "direction": "in"
}
```

Consultez l’exemple dans le langage de votre choix pour voir comment utiliser cette liaison d’entrée pour mettre à jour la valeur de texte du document.

* [C#](#incsharp)
* [F#](#infsharp)
* [JavaScript](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a>Exemple d’entrée en C# #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a>Exemple d’entrée en F# #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

Cet exemple requiert un fichier `project.json` qui spécifie les dépendances NuGet `FSharp.Interop.Dynamic` et `Dynamitey` :

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

Pour ajouter un fichier `project.json`, consultez [F# package management](functions-reference-fsharp.md#package) (Gestion des packages F#).

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a>Exemple d’entrée en JavaScript

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a>Exemple d’entrée avec plusieurs documents

Supposons que vous souhaitiez récupérer plusieurs documents spécifiés par une requête SQL, à l’aide d’un déclencheur de file d’attente pour personnaliser les paramètres de requête. 

Dans cet exemple, le déclencheur de file d’attente fournit un paramètre `departmentId`. Un message de file d’attente de `{ "departmentId" : "Finance" }` renvoie tous les enregistrements pour le département des finances. Utilisez ce qui suit dans *function.json* :

```
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}"
    "connection": "CosmosDBConnection"
}
```

### <a name="input-sample-with-multiple-documents-in-c"></a>Exemple d’entrée avec plusieurs documents en C#

```csharp
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{   
    foreach (var doc in documents)
    {
        // operate on each document
    }    
}

public class QueuePayload
{
    public string departmentId { get; set; }
}
```

### <a name="input-sample-with-multiple-documents-in-javascript"></a>Exemple d’entrée avec plusieurs documents en JavaScript

```javascript
module.exports = function (context, input) {    
    var documents = context.bindings.documents;
    for (var i = 0; i < documents.length; i++) {
        var document = documents[i];
        // operate on each document
    }       
    context.done();
};
```

## <a id="docdboutput"></a>Liaison de sortie d’API DocumentDB
La liaison de sortie d’API DocumentDB vous permet d’écrire un nouveau document dans une base de données Azure Cosmos DB. Elle possède les propriétés suivantes dans *function.json* :

- `name` : identificateur utilisé dans le code de fonctions pour le nouveau document.
- `type` : doit être défini sur `"documentdb"`.
- `databaseName` : base de données contenant la collection dans laquelle le nouveau document sera créé.
- `collectionName` : collection dans laquelle le nouveau document sera créé.
- `createIfNotExists` : valeur booléenne indiquant si la collection sera ou non créée si elle n’existe pas. La valeur par défaut est *false*. Cette configuration est due au fait que les collections sont créées avec un débit réservé, ce qui a des conséquences sur le plan tarifaire. Pour plus d’informations, consultez la [page de tarification](https://azure.microsoft.com/pricing/details/documentdb/).
- `connection` : nom du paramètre d’application qui contient votre chaîne de connexion Cosmos DB.
- `direction` : doit être défini sur `"out"`.

## <a name="using-a-documentdb-api-output-binding"></a>Utilisation d’une liaison de sortie d’API DocumentDB
Cette section vous montre comment utiliser la liaison de sortie d’API DocumentDB dans le code de votre fonction.

Si vous écrivez dans le paramètre de sortie de votre fonction, par défaut, un nouveau document est généré dans votre base de données avec un GUID généré automatiquement en tant qu’ID de document. Vous pouvez spécifier l’ID du document de sortie en spécifiant la propriété JSON `id` dans le paramètre de sortie. 

>[!Note]  
>Lorsque vous spécifier l’ID d’un document existant, il est remplacé par le nouveau document de sortie. 

Pour générer plusieurs documents, vous pouvez également vous lier à `ICollector<T>` ou `IAsyncCollector<T>` où `T` est un des types pris en charge.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>Exemple de liaison de sortie d’API DocumentDB
Supposons que le tableau `bindings` de function.json contient la liaison de sortie d’API DocumentDB suivante :

```json
{
  "name": "employeeDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "createIfNotExists": true,
  "connection": "MyAccount_COSMOSDB",     
  "direction": "out"
}
```

Et que vous disposez d’une liaison d’entrée de file d’attente pour une file d’attente qui reçoit le code JSON dans le format suivant :

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Et que vous souhaitez créer des documents Cosmos DB au format suivant pour chaque enregistrement :

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Consultez l’exemple dans le langage de votre choix pour voir comment utiliser cette liaison de sortie pour ajouter des documents à votre base de données.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [JavaScript](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Exemple de sortie en C# #

```cs
#r "Newtonsoft.Json"

using System;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
  log.Info($"C# Queue trigger function processed: {myQueueItem}");

  dynamic employee = JObject.Parse(myQueueItem);

  employeeDocument = new {
    id = employee.name + "-" + employee.employeeId,
    name = employee.name,
    employeeId = employee.employeeId,
    address = employee.address
  };
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Exemple de sortie en F# #

```fsharp
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Employee = {
  id: string
  name: string
  employeeId: string
  address: string
}

let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
  log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
  let employee = JObject.Parse(myQueueItem)
  employeeDocument <-
    { id = sprintf "%s-%s" employee?name employee?employeeId
      name = employee?name
      employeeId = employee?employeeId
      address = employee?address }
```

Cet exemple requiert un fichier `project.json` qui spécifie les dépendances NuGet `FSharp.Interop.Dynamic` et `Dynamitey` :

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

Pour ajouter un fichier `project.json`, consultez [F# package management](functions-reference-fsharp.md#package) (Gestion des packages F#).

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a>Exemple de sortie en JavaScript

```javascript
module.exports = function (context) {

  context.bindings.employeeDocument = JSON.stringify({ 
    id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
    name: context.bindings.myQueueItem.name,
    employeeId: context.bindings.myQueueItem.employeeId,
    address: context.bindings.myQueueItem.address
  });

  context.done();
};
```
