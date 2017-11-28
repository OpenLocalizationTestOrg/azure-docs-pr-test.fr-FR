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
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="e2504-104">Liaisons Cosmos DB Azure Functions</span><span class="sxs-lookup"><span data-stu-id="e2504-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e2504-105">Cet article explique comment configurer et coder des liaisons Azure Cosmos DB dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="e2504-105">This article explains how to configure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="e2504-106">Azure Functions prend en charge des liaisons d’entrée et de sortie pour Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2504-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="e2504-107">Pour plus d’informations sur Cosmos DB, consultez les pages [Présentation de Cosmos DB](../documentdb/documentdb-introduction.md) et [Créer une application de console Cosmos DB](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e2504-107">For more information on Cosmos DB, see [Introduction to Cosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="e2504-108">Liaison d’entrée d’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e2504-108">DocumentDB API input binding</span></span>
<span data-ttu-id="e2504-109">La liaison d’entrée d’API DocumentDB récupère un document Cosmos DB et le transmet au paramètre d’entrée nommé de la fonction.</span><span class="sxs-lookup"><span data-stu-id="e2504-109">The DocumentDB API input binding retrieves a Cosmos DB document and passes it to the named input parameter of the function.</span></span> <span data-ttu-id="e2504-110">L’ID du document peut être déterminé en fonction du déclencheur qui appelle la fonction.</span><span class="sxs-lookup"><span data-stu-id="e2504-110">The document ID can be determined based on the trigger that invokes the function.</span></span> 

<span data-ttu-id="e2504-111">La liaison d’entrée d’API DocumentDB possède les propriétés suivantes dans *function.json* :</span><span class="sxs-lookup"><span data-stu-id="e2504-111">The DocumentDB API input binding has the following properties in *function.json*:</span></span>

- <span data-ttu-id="e2504-112">`name` : nom de l’identificateur utilisé dans le code de fonctions pour le document.</span><span class="sxs-lookup"><span data-stu-id="e2504-112">`name` : Identifier name used in function code for the document</span></span>
- <span data-ttu-id="e2504-113">`type` : doit être défini sur « documentdb ».</span><span class="sxs-lookup"><span data-stu-id="e2504-113">`type` : must be set to "documentdb"</span></span>
- <span data-ttu-id="e2504-114">`databaseName` : la base de données contenant le document.</span><span class="sxs-lookup"><span data-stu-id="e2504-114">`databaseName` : The database containing the document</span></span>
- <span data-ttu-id="e2504-115">`collectionName` : collection contenant le document.</span><span class="sxs-lookup"><span data-stu-id="e2504-115">`collectionName` : The collection containing the document</span></span>
- <span data-ttu-id="e2504-116">`id` : ID du document à récupérer.</span><span class="sxs-lookup"><span data-stu-id="e2504-116">`id` : The Id of the document to retrieve.</span></span> <span data-ttu-id="e2504-117">Cette propriété prend en charge les paramètres de liaison ; consultez la section [Lier aux propriétés d’entrée personnalisées dans une expression de liaison](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) de l’article [Concepts des déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="e2504-117">This property supports bindings parameters; see [Bind to custom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in the article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="e2504-118">`sqlQuery` : requête SQL Cosmos DB utilisée pour récupérer plusieurs documents.</span><span class="sxs-lookup"><span data-stu-id="e2504-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="e2504-119">La requête prend en charge les liaisons d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e2504-119">The query supports runtime bindings.</span></span> <span data-ttu-id="e2504-120">Par exemple : `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="e2504-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="e2504-121">`connection` : nom du paramètre d’application qui contient votre chaîne de connexion Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2504-121">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="e2504-122">`direction` : doit être défini sur `"in"`.</span><span class="sxs-lookup"><span data-stu-id="e2504-122">`direction`  : must be set to `"in"`.</span></span>

<span data-ttu-id="e2504-123">Les propriétés `id` et `sqlQuery` ne peuvent pas être spécifiées.</span><span class="sxs-lookup"><span data-stu-id="e2504-123">The properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="e2504-124">Si `id` et `sqlQuery` ne sont pas définis, l’ensemble de la collection est récupéré.</span><span class="sxs-lookup"><span data-stu-id="e2504-124">If neither `id` nor `sqlQuery` is set, the entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="e2504-125">Utiliser une liaison d’entrée d’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e2504-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="e2504-126">Dans les fonctions C# et F#, lorsque la fonction se termine correctement, toutes les modifications apportées au document d’entrée par le biais des paramètres d’entrée nommés sont automatiquement conservées.</span><span class="sxs-lookup"><span data-stu-id="e2504-126">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="e2504-127">Dans les fonctions JavaScript, les mises à jour ne sont pas effectuées une fois la fonction terminée.</span><span class="sxs-lookup"><span data-stu-id="e2504-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="e2504-128">Utilisez plutôt `context.bindings.<documentName>In` et `context.bindings.<documentName>Out` pour effectuer les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="e2504-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span></span> <span data-ttu-id="e2504-129">Consultez [l’exemple JavaScript](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="e2504-129">See the [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="e2504-130">Exemple d’entrée pour un seul document</span><span class="sxs-lookup"><span data-stu-id="e2504-130">Input sample for single document</span></span>
<span data-ttu-id="e2504-131">Supposez que le tableau `bindings` de function.json contient la liaison d’entrée d’API DocumentDB suivante :</span><span class="sxs-lookup"><span data-stu-id="e2504-131">Suppose you have the following DocumentDB API input binding in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="e2504-132">Consultez l’exemple dans le langage de votre choix pour voir comment utiliser cette liaison d’entrée pour mettre à jour la valeur de texte du document.</span><span class="sxs-lookup"><span data-stu-id="e2504-132">See the language-specific sample that uses this input binding to update the document's text value.</span></span>

* [<span data-ttu-id="e2504-133">C#</span><span class="sxs-lookup"><span data-stu-id="e2504-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="e2504-134">F#</span><span class="sxs-lookup"><span data-stu-id="e2504-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="e2504-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="e2504-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="e2504-136">Exemple d’entrée en C#</span><span class="sxs-lookup"><span data-stu-id="e2504-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="e2504-137">Exemple d’entrée en F#</span><span class="sxs-lookup"><span data-stu-id="e2504-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="e2504-138">Cet exemple requiert un fichier `project.json` qui spécifie les dépendances NuGet `FSharp.Interop.Dynamic` et `Dynamitey` :</span><span class="sxs-lookup"><span data-stu-id="e2504-138">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="e2504-139">Pour ajouter un fichier `project.json`, consultez [F# package management](functions-reference-fsharp.md#package) (Gestion des packages F#).</span><span class="sxs-lookup"><span data-stu-id="e2504-139">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="e2504-140">Exemple d’entrée en JavaScript</span><span class="sxs-lookup"><span data-stu-id="e2504-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="e2504-141">Exemple d’entrée avec plusieurs documents</span><span class="sxs-lookup"><span data-stu-id="e2504-141">Input sample with multiple documents</span></span>

<span data-ttu-id="e2504-142">Supposons que vous souhaitiez récupérer plusieurs documents spécifiés par une requête SQL, à l’aide d’un déclencheur de file d’attente pour personnaliser les paramètres de requête.</span><span class="sxs-lookup"><span data-stu-id="e2504-142">Suppose that you wish to retrieve multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span> 

<span data-ttu-id="e2504-143">Dans cet exemple, le déclencheur de file d’attente fournit un paramètre `departmentId`. Un message de file d’attente de `{ "departmentId" : "Finance" }` renvoie tous les enregistrements pour le département des finances.</span><span class="sxs-lookup"><span data-stu-id="e2504-143">In this example, the queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> <span data-ttu-id="e2504-144">Utilisez ce qui suit dans *function.json* :</span><span class="sxs-lookup"><span data-stu-id="e2504-144">Use the following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="e2504-145">Exemple d’entrée avec plusieurs documents en C#</span><span class="sxs-lookup"><span data-stu-id="e2504-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="e2504-146">Exemple d’entrée avec plusieurs documents en JavaScript</span><span class="sxs-lookup"><span data-stu-id="e2504-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="e2504-147"><a id="docdboutput"></a>Liaison de sortie d’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e2504-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="e2504-148">La liaison de sortie d’API DocumentDB vous permet d’écrire un nouveau document dans une base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2504-148">The DocumentDB API output binding lets you write a new document to an Azure Cosmos DB database.</span></span> <span data-ttu-id="e2504-149">Elle possède les propriétés suivantes dans *function.json* :</span><span class="sxs-lookup"><span data-stu-id="e2504-149">It has the following properties in *function.json*:</span></span>

- <span data-ttu-id="e2504-150">`name` : identificateur utilisé dans le code de fonctions pour le nouveau document.</span><span class="sxs-lookup"><span data-stu-id="e2504-150">`name` : Identifier used in function code for the new document</span></span>
- <span data-ttu-id="e2504-151">`type` : doit être défini sur `"documentdb"`.</span><span class="sxs-lookup"><span data-stu-id="e2504-151">`type` : must be set to `"documentdb"`</span></span>
- <span data-ttu-id="e2504-152">`databaseName` : base de données contenant la collection dans laquelle le nouveau document sera créé.</span><span class="sxs-lookup"><span data-stu-id="e2504-152">`databaseName` : The database containing the collection where the new document will be created.</span></span>
- <span data-ttu-id="e2504-153">`collectionName` : collection dans laquelle le nouveau document sera créé.</span><span class="sxs-lookup"><span data-stu-id="e2504-153">`collectionName` : The collection where the new document will be created.</span></span>
- <span data-ttu-id="e2504-154">`createIfNotExists` : valeur booléenne indiquant si la collection sera ou non créée si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="e2504-154">`createIfNotExists` : A boolean value to indicate whether the collection will be created if it does not exist.</span></span> <span data-ttu-id="e2504-155">La valeur par défaut est *false*.</span><span class="sxs-lookup"><span data-stu-id="e2504-155">The default is *false*.</span></span> <span data-ttu-id="e2504-156">Cette configuration est due au fait que les collections sont créées avec un débit réservé, ce qui a des conséquences sur le plan tarifaire.</span><span class="sxs-lookup"><span data-stu-id="e2504-156">The reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="e2504-157">Pour plus d’informations, consultez la [page de tarification](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="e2504-157">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="e2504-158">`connection` : nom du paramètre d’application qui contient votre chaîne de connexion Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2504-158">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="e2504-159">`direction` : doit être défini sur `"out"`.</span><span class="sxs-lookup"><span data-stu-id="e2504-159">`direction` : must be set to `"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="e2504-160">Utilisation d’une liaison de sortie d’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e2504-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="e2504-161">Cette section vous montre comment utiliser la liaison de sortie d’API DocumentDB dans le code de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="e2504-161">This section shows you how to use your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="e2504-162">Si vous écrivez dans le paramètre de sortie de votre fonction, par défaut, un nouveau document est généré dans votre base de données avec un GUID généré automatiquement en tant qu’ID de document.</span><span class="sxs-lookup"><span data-stu-id="e2504-162">When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="e2504-163">Vous pouvez spécifier l’ID du document de sortie en spécifiant la propriété JSON `id` dans le paramètre de sortie.</span><span class="sxs-lookup"><span data-stu-id="e2504-163">You can specify the document ID of output document by specifying the `id` JSON property in the output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="e2504-164">Lorsque vous spécifier l’ID d’un document existant, il est remplacé par le nouveau document de sortie.</span><span class="sxs-lookup"><span data-stu-id="e2504-164">When you specify the ID of an existing document, it gets overwritten by the new output document.</span></span> 

<span data-ttu-id="e2504-165">Pour générer plusieurs documents, vous pouvez également vous lier à `ICollector<T>` ou `IAsyncCollector<T>` où `T` est un des types pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e2504-165">To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="e2504-166">Exemple de liaison de sortie d’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e2504-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="e2504-167">Supposons que le tableau `bindings` de function.json contient la liaison de sortie d’API DocumentDB suivante :</span><span class="sxs-lookup"><span data-stu-id="e2504-167">Suppose you have the following DocumentDB API output binding in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="e2504-168">Et que vous disposez d’une liaison d’entrée de file d’attente pour une file d’attente qui reçoit le code JSON dans le format suivant :</span><span class="sxs-lookup"><span data-stu-id="e2504-168">And you have a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="e2504-169">Et que vous souhaitez créer des documents Cosmos DB au format suivant pour chaque enregistrement :</span><span class="sxs-lookup"><span data-stu-id="e2504-169">And you want to create Cosmos DB documents in the following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="e2504-170">Consultez l’exemple dans le langage de votre choix pour voir comment utiliser cette liaison de sortie pour ajouter des documents à votre base de données.</span><span class="sxs-lookup"><span data-stu-id="e2504-170">See the language-specific sample that uses this output binding to add documents to your database.</span></span>

* [<span data-ttu-id="e2504-171">C#</span><span class="sxs-lookup"><span data-stu-id="e2504-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="e2504-172">F#</span><span class="sxs-lookup"><span data-stu-id="e2504-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="e2504-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="e2504-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="e2504-174">Exemple de sortie en C#</span><span class="sxs-lookup"><span data-stu-id="e2504-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="e2504-175">Exemple de sortie en F#</span><span class="sxs-lookup"><span data-stu-id="e2504-175">Output sample in F#</span></span> #

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

<span data-ttu-id="e2504-176">Cet exemple requiert un fichier `project.json` qui spécifie les dépendances NuGet `FSharp.Interop.Dynamic` et `Dynamitey` :</span><span class="sxs-lookup"><span data-stu-id="e2504-176">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="e2504-177">Pour ajouter un fichier `project.json`, consultez [F# package management](functions-reference-fsharp.md#package) (Gestion des packages F#).</span><span class="sxs-lookup"><span data-stu-id="e2504-177">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="e2504-178">Exemple de sortie en JavaScript</span><span class="sxs-lookup"><span data-stu-id="e2504-178">Output sample in JavaScript</span></span>

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
