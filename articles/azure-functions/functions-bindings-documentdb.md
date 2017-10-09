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
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="0c529-104">Liaisons Cosmos DB Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0c529-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0c529-105">Cet article explique comment les liaisons de base de données Azure Cosmos tooconfigure et le code dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="0c529-105">This article explains how tooconfigure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="0c529-106">Azure Functions prend en charge des liaisons d’entrée et de sortie pour Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0c529-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="0c529-107">Pour plus d’informations sur la base de données Cosmos, consultez [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) et [générez une application de console Cosmos DB](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0c529-107">For more information on Cosmos DB, see [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="0c529-108">Liaison d’entrée d’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0c529-108">DocumentDB API input binding</span></span>
<span data-ttu-id="0c529-109">Hello liaison d’entrée d’API DocumentDB récupère un document de base de données Cosmos et lui transmet toohello nommé de paramètre d’entrée de la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="0c529-109">hello DocumentDB API input binding retrieves a Cosmos DB document and passes it toohello named input parameter of hello function.</span></span> <span data-ttu-id="0c529-110">document Hello QU'ID peut être déterminé en fonction de déclencheur hello qui appelle la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="0c529-110">hello document ID can be determined based on hello trigger that invokes hello function.</span></span> 

<span data-ttu-id="0c529-111">Hello liaison d’entrée d’API DocumentDB a hello propriétés dans suivantes *function.json*:</span><span class="sxs-lookup"><span data-stu-id="0c529-111">hello DocumentDB API input binding has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="0c529-112">`name`: Nom identificateur utilisé dans le code de la fonction de document de hello</span><span class="sxs-lookup"><span data-stu-id="0c529-112">`name` : Identifier name used in function code for hello document</span></span>
- <span data-ttu-id="0c529-113">`type`: doit être défini trop « documentdb »</span><span class="sxs-lookup"><span data-stu-id="0c529-113">`type` : must be set too"documentdb"</span></span>
- <span data-ttu-id="0c529-114">`databaseName`: base de données hello contenant le document de hello</span><span class="sxs-lookup"><span data-stu-id="0c529-114">`databaseName` : hello database containing hello document</span></span>
- <span data-ttu-id="0c529-115">`collectionName`: collection hello contenant le document de hello</span><span class="sxs-lookup"><span data-stu-id="0c529-115">`collectionName` : hello collection containing hello document</span></span>
- <span data-ttu-id="0c529-116">`id`: hello Id de hello document tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="0c529-116">`id` : hello Id of hello document tooretrieve.</span></span> <span data-ttu-id="0c529-117">Cette propriété prend en charge les paramètres de liaison ; consultez [lier les propriétés d’entrée de toocustom dans une expression de liaison](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) dans l’article de hello [déclencheurs de fonctions d’Azure et les concepts de liaisons](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="0c529-117">This property supports bindings parameters; see [Bind toocustom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in hello article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="0c529-118">`sqlQuery` : requête SQL Cosmos DB utilisée pour récupérer plusieurs documents.</span><span class="sxs-lookup"><span data-stu-id="0c529-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="0c529-119">requête de Hello prend en charge les liaisons de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="0c529-119">hello query supports runtime bindings.</span></span> <span data-ttu-id="0c529-120">Par exemple : `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="0c529-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="0c529-121">`connection`: nom de hello du paramètre d’application hello contenant votre chaîne de connexion de base de données de Cosmos</span><span class="sxs-lookup"><span data-stu-id="0c529-121">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="0c529-122">`direction`: doit être défini trop`"in"`.</span><span class="sxs-lookup"><span data-stu-id="0c529-122">`direction`  : must be set too`"in"`.</span></span>

<span data-ttu-id="0c529-123">Hello propriétés `id` et `sqlQuery` ne peuvent pas être spécifiés.</span><span class="sxs-lookup"><span data-stu-id="0c529-123">hello properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="0c529-124">Si ni `id` ni `sqlQuery` est définie, hello entière récupérer de la collection.</span><span class="sxs-lookup"><span data-stu-id="0c529-124">If neither `id` nor `sqlQuery` is set, hello entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="0c529-125">Utiliser une liaison d’entrée d’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0c529-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="0c529-126">En c# et les fonctions F #, lors de la fonction hello se termine avec succès, toutes les modifications apportées toohello le document d’entrée par le biais des paramètres d’entrée nommés sont automatiquement rendues persistantes.</span><span class="sxs-lookup"><span data-stu-id="0c529-126">In C# and F# functions, when hello function exits successfully, any changes made toohello input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="0c529-127">Dans les fonctions JavaScript, les mises à jour ne sont pas effectuées une fois la fonction terminée.</span><span class="sxs-lookup"><span data-stu-id="0c529-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="0c529-128">Au lieu de cela, utilisez `context.bindings.<documentName>In` et `context.bindings.<documentName>Out` toomake les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="0c529-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` toomake updates.</span></span> <span data-ttu-id="0c529-129">Consultez hello [JavaScript exemple](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="0c529-129">See hello [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="0c529-130">Exemple d’entrée pour un seul document</span><span class="sxs-lookup"><span data-stu-id="0c529-130">Input sample for single document</span></span>
<span data-ttu-id="0c529-131">Supposons que vous avez hello suivantes API DocumentDB d’entrée de liaison Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="0c529-131">Suppose you have hello following DocumentDB API input binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="0c529-132">Voir exemple hello spécifiques à une langue qui utilise la valeur de cette liaison d’entrée tooupdate hello document texte.</span><span class="sxs-lookup"><span data-stu-id="0c529-132">See hello language-specific sample that uses this input binding tooupdate hello document's text value.</span></span>

* [<span data-ttu-id="0c529-133">C#</span><span class="sxs-lookup"><span data-stu-id="0c529-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="0c529-134">F#</span><span class="sxs-lookup"><span data-stu-id="0c529-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="0c529-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c529-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="0c529-136">Exemple d’entrée en C#</span><span class="sxs-lookup"><span data-stu-id="0c529-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="0c529-137">Exemple d’entrée en F#</span><span class="sxs-lookup"><span data-stu-id="0c529-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="0c529-138">Cet exemple requiert un `project.json` fichier indiquant hello `FSharp.Interop.Dynamic` et `Dynamitey` les dépendances de NuGet :</span><span class="sxs-lookup"><span data-stu-id="0c529-138">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="0c529-139">tooadd un `project.json` de fichiers, consultez [gestion des packages F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="0c529-139">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="0c529-140">Exemple d’entrée en JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c529-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="0c529-141">Exemple d’entrée avec plusieurs documents</span><span class="sxs-lookup"><span data-stu-id="0c529-141">Input sample with multiple documents</span></span>

<span data-ttu-id="0c529-142">Supposons que vous souhaitez tooretrieve plusieurs documents spécifiés par une requête SQL, à l’aide d’une file d’attente déclencheur toocustomize hello paramètres de la requête.</span><span class="sxs-lookup"><span data-stu-id="0c529-142">Suppose that you wish tooretrieve multiple documents specified by a SQL query, using a queue trigger toocustomize hello query parameters.</span></span> 

<span data-ttu-id="0c529-143">Dans cet exemple, le déclencheur de file d’attente hello fournit un paramètre `departmentId`. Un message de la file d’attente de `{ "departmentId" : "Finance" }` renvoie tous les enregistrements pour le service finance de hello.</span><span class="sxs-lookup"><span data-stu-id="0c529-143">In this example, hello queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for hello finance department.</span></span> <span data-ttu-id="0c529-144">Utilisez hello qui suit dans *function.json*:</span><span class="sxs-lookup"><span data-stu-id="0c529-144">Use hello following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="0c529-145">Exemple d’entrée avec plusieurs documents en C#</span><span class="sxs-lookup"><span data-stu-id="0c529-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="0c529-146">Exemple d’entrée avec plusieurs documents en JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c529-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="0c529-147"><a id="docdboutput"></a>Liaison de sortie d’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0c529-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="0c529-148">Hello API DocumentDB liaison vous permet d’écrire une base de données de la base de données Azure Cosmos de tooan nouveau document de sortie.</span><span class="sxs-lookup"><span data-stu-id="0c529-148">hello DocumentDB API output binding lets you write a new document tooan Azure Cosmos DB database.</span></span> <span data-ttu-id="0c529-149">Il a hello propriétés dans suivantes *function.json*:</span><span class="sxs-lookup"><span data-stu-id="0c529-149">It has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="0c529-150">`name`: Identificateur utilisé dans le code de fonction pour hello nouveau document</span><span class="sxs-lookup"><span data-stu-id="0c529-150">`name` : Identifier used in function code for hello new document</span></span>
- <span data-ttu-id="0c529-151">`type`: doit être défini trop`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="0c529-151">`type` : must be set too`"documentdb"`</span></span>
- <span data-ttu-id="0c529-152">`databaseName`: base de données hello contenant la collection hello où hello nouveau document sera créé.</span><span class="sxs-lookup"><span data-stu-id="0c529-152">`databaseName` : hello database containing hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="0c529-153">`collectionName`: hello collection où le nouveau document de hello doit être créé.</span><span class="sxs-lookup"><span data-stu-id="0c529-153">`collectionName` : hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="0c529-154">`createIfNotExists`: Une valeur booléenne tooindicate si la collection de hello sera créée s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="0c529-154">`createIfNotExists` : A boolean value tooindicate whether hello collection will be created if it does not exist.</span></span> <span data-ttu-id="0c529-155">valeur par défaut Hello est *false*.</span><span class="sxs-lookup"><span data-stu-id="0c529-155">hello default is *false*.</span></span> <span data-ttu-id="0c529-156">Hello raison pour cela est nouveau regroupements sont créés avec un débit réservé, ce qui a des implications de la tarification.</span><span class="sxs-lookup"><span data-stu-id="0c529-156">hello reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="0c529-157">Pour plus d’informations, visitez hello [page de tarification](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="0c529-157">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="0c529-158">`connection`: nom de hello du paramètre d’application hello contenant votre chaîne de connexion de base de données de Cosmos</span><span class="sxs-lookup"><span data-stu-id="0c529-158">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="0c529-159">`direction`: doit être défini trop`"out"`</span><span class="sxs-lookup"><span data-stu-id="0c529-159">`direction` : must be set too`"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="0c529-160">Utilisation d’une liaison de sortie d’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0c529-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="0c529-161">Cette section vous montre comment toouse votre API DocumentDB de sortie de liaison dans votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="0c529-161">This section shows you how toouse your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="0c529-162">Lorsque vous écrivez un paramètre de sortie toohello dans votre fonction, par défaut, qu'un nouveau document est généré dans votre base de données, avec un GUID généré automatiquement en tant que hello document ID.</span><span class="sxs-lookup"><span data-stu-id="0c529-162">When you write toohello output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as hello document ID.</span></span> <span data-ttu-id="0c529-163">Vous pouvez spécifier les ID de document hello du document de sortie en spécifiant hello `id` propriété JSON dans hello paramètre de sortie.</span><span class="sxs-lookup"><span data-stu-id="0c529-163">You can specify hello document ID of output document by specifying hello `id` JSON property in hello output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="0c529-164">Lorsque vous spécifiez des ID hello d’un document existant, elle est remplacée par le nouveau document de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="0c529-164">When you specify hello ID of an existing document, it gets overwritten by hello new output document.</span></span> 

<span data-ttu-id="0c529-165">toooutput plusieurs documents, vous pouvez également lier trop`ICollector<T>` ou `IAsyncCollector<T>` où `T` est un des types de hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0c529-165">toooutput multiple documents, you can also bind too`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of hello supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="0c529-166">Exemple de liaison de sortie d’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0c529-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="0c529-167">Supposons que vous avez hello suivantes API DocumentDB sortie liaison Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="0c529-167">Suppose you have hello following DocumentDB API output binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="0c529-168">Et vous disposez d’une liaison d’entrée de la file d’attente pour une file d’attente qui reçoit le JSON Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="0c529-168">And you have a queue input binding for a queue that receives JSON in hello following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="0c529-169">Et que vous souhaitez les documents de Cosmos DB toocreate Bonjour suivant le format pour chaque enregistrement :</span><span class="sxs-lookup"><span data-stu-id="0c529-169">And you want toocreate Cosmos DB documents in hello following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="0c529-170">Consultez l’exemple hello spécifiques à une langue qui utilise cette base de données de sortie liaison tooadd documents tooyour.</span><span class="sxs-lookup"><span data-stu-id="0c529-170">See hello language-specific sample that uses this output binding tooadd documents tooyour database.</span></span>

* [<span data-ttu-id="0c529-171">C#</span><span class="sxs-lookup"><span data-stu-id="0c529-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="0c529-172">F#</span><span class="sxs-lookup"><span data-stu-id="0c529-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="0c529-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c529-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="0c529-174">Exemple de sortie en C#</span><span class="sxs-lookup"><span data-stu-id="0c529-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="0c529-175">Exemple de sortie en F#</span><span class="sxs-lookup"><span data-stu-id="0c529-175">Output sample in F#</span></span> #

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

<span data-ttu-id="0c529-176">Cet exemple requiert un `project.json` fichier indiquant hello `FSharp.Interop.Dynamic` et `Dynamitey` les dépendances de NuGet :</span><span class="sxs-lookup"><span data-stu-id="0c529-176">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="0c529-177">tooadd un `project.json` de fichiers, consultez [gestion des packages F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="0c529-177">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="0c529-178">Exemple de sortie en JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c529-178">Output sample in JavaScript</span></span>

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
