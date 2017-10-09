---
title: "liaisons de base de données de fonctions Cosmos aaaAzure | Documents Microsoft"
description: "Comprendre comment les liaisons de base de données Azure Cosmos toouse dans les fonctions d’Azure."
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
ms.openlocfilehash: 76b89e8296db1dd28dff9528903b1f6a28f55232
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a>Liaisons Cosmos DB Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment les liaisons de base de données Azure Cosmos tooconfigure et le code dans les fonctions d’Azure. Azure Functions prend en charge des liaisons d’entrée et de sortie pour Cosmos DB.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Pour plus d’informations sur la base de données Cosmos, consultez [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) et [générez une application de console Cosmos DB](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>Liaison d’entrée d’API DocumentDB
Hello liaison d’entrée d’API DocumentDB récupère un document de base de données Cosmos et lui transmet toohello nommé de paramètre d’entrée de la fonction hello. document Hello QU'ID peut être déterminé en fonction de déclencheur hello qui appelle la fonction hello. 

Hello liaison d’entrée d’API DocumentDB a hello propriétés dans suivantes *function.json*:

- `name`: Nom identificateur utilisé dans le code de la fonction de document de hello
- `type`: doit être défini trop « documentdb »
- `databaseName`: base de données hello contenant le document de hello
- `collectionName`: collection hello contenant le document de hello
- `id`: hello Id de hello document tooretrieve. Cette propriété prend en charge les paramètres de liaison ; consultez [lier les propriétés d’entrée de toocustom dans une expression de liaison](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) dans l’article de hello [déclencheurs de fonctions d’Azure et les concepts de liaisons](functions-triggers-bindings.md).
- `sqlQuery` : requête SQL Cosmos DB utilisée pour récupérer plusieurs documents. requête de Hello prend en charge les liaisons de l’exécution. Par exemple : `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: nom de hello du paramètre d’application hello contenant votre chaîne de connexion de base de données de Cosmos
- `direction`: doit être défini trop`"in"`.

Hello propriétés `id` et `sqlQuery` ne peuvent pas être spécifiés. Si ni `id` ni `sqlQuery` est définie, hello entière récupérer de la collection.

## <a name="using-a-documentdb-api-input-binding"></a>Utiliser une liaison d’entrée d’API DocumentDB

* En c# et les fonctions F #, lors de la fonction hello se termine avec succès, toutes les modifications apportées toohello le document d’entrée par le biais des paramètres d’entrée nommés sont automatiquement rendues persistantes. 
* Dans les fonctions JavaScript, les mises à jour ne sont pas effectuées une fois la fonction terminée. Au lieu de cela, utilisez `context.bindings.<documentName>In` et `context.bindings.<documentName>Out` toomake les mises à jour. Consultez hello [JavaScript exemple](#injavascript).

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>Exemple d’entrée pour un seul document
Supposons que vous avez hello suivantes API DocumentDB d’entrée de liaison Bonjour `bindings` tableau de function.json :

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

Voir exemple hello spécifiques à une langue qui utilise la valeur de cette liaison d’entrée tooupdate hello document texte.

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

Cet exemple requiert un `project.json` fichier indiquant hello `FSharp.Interop.Dynamic` et `Dynamitey` les dépendances de NuGet :

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

tooadd un `project.json` de fichiers, consultez [gestion des packages F #](functions-reference-fsharp.md#package).

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

Supposons que vous souhaitez tooretrieve plusieurs documents spécifiés par une requête SQL, à l’aide d’une file d’attente déclencheur toocustomize hello paramètres de la requête. 

Dans cet exemple, le déclencheur de file d’attente hello fournit un paramètre `departmentId`. Un message de la file d’attente de `{ "departmentId" : "Finance" }` renvoie tous les enregistrements pour le service finance de hello. Utilisez hello qui suit dans *function.json*:

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
Hello API DocumentDB liaison vous permet d’écrire une base de données de la base de données Azure Cosmos de tooan nouveau document de sortie. Il a hello propriétés dans suivantes *function.json*:

- `name`: Identificateur utilisé dans le code de fonction pour hello nouveau document
- `type`: doit être défini trop`"documentdb"`
- `databaseName`: base de données hello contenant la collection hello où hello nouveau document sera créé.
- `collectionName`: hello collection où le nouveau document de hello doit être créé.
- `createIfNotExists`: Une valeur booléenne tooindicate si la collection de hello sera créée s’il n’existe pas. valeur par défaut Hello est *false*. Hello raison pour cela est nouveau regroupements sont créés avec un débit réservé, ce qui a des implications de la tarification. Pour plus d’informations, visitez hello [page de tarification](https://azure.microsoft.com/pricing/details/documentdb/).
- `connection`: nom de hello du paramètre d’application hello contenant votre chaîne de connexion de base de données de Cosmos
- `direction`: doit être défini trop`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>Utilisation d’une liaison de sortie d’API DocumentDB
Cette section vous montre comment toouse votre API DocumentDB de sortie de liaison dans votre code de fonction.

Lorsque vous écrivez un paramètre de sortie toohello dans votre fonction, par défaut, qu'un nouveau document est généré dans votre base de données, avec un GUID généré automatiquement en tant que hello document ID. Vous pouvez spécifier les ID de document hello du document de sortie en spécifiant hello `id` propriété JSON dans hello paramètre de sortie. 

>[!Note]  
>Lorsque vous spécifiez des ID hello d’un document existant, elle est remplacée par le nouveau document de sortie hello. 

toooutput plusieurs documents, vous pouvez également lier trop`ICollector<T>` ou `IAsyncCollector<T>` où `T` est un des types de hello pris en charge.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>Exemple de liaison de sortie d’API DocumentDB
Supposons que vous avez hello suivantes API DocumentDB sortie liaison Bonjour `bindings` tableau de function.json :

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

Et vous disposez d’une liaison d’entrée de la file d’attente pour une file d’attente qui reçoit le JSON Bonjour suivant le format :

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Et que vous souhaitez les documents de Cosmos DB toocreate Bonjour suivant le format pour chaque enregistrement :

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Consultez l’exemple hello spécifiques à une langue qui utilise cette base de données de sortie liaison tooadd documents tooyour.

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

Cet exemple requiert un `project.json` fichier indiquant hello `FSharp.Interop.Dynamic` et `Dynamitey` les dépendances de NuGet :

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

tooadd un `project.json` de fichiers, consultez [gestion des packages F #](functions-reference-fsharp.md#package).

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
