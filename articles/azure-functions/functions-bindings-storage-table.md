---
title: Liaisons de table Azure Functions Storage | Microsoft Docs
description: "Découvrez comment utiliser des liaisons de Stockage Azure dans Azure Functions."
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
ms.openlocfilehash: bb01be3ee044f60376e0c9c2de7b3dd34f3b7aca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="8f38d-104">Liaisons de table Azure Functions Storage</span><span class="sxs-lookup"><span data-stu-id="8f38d-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="8f38d-105">Cet article explique comment configurer et coder des liaisons de table de Stockage Azure dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="8f38d-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="8f38d-106">Azure Functions prend en charge les liaisons d’entrée et de sortie pour les tables Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8f38d-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="8f38d-107">La liaison de table Storage prend en charge les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="8f38d-107">The Storage table binding supports the following scenarios:</span></span>

* <span data-ttu-id="8f38d-108">**Lecture d’une seule ligne dans une fonction C# ou Node.js** - Définition de `partitionKey` et `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="8f38d-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="8f38d-109">Les propriétés `filter` et `take` ne sont pas utilisées dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="8f38d-109">The `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="8f38d-110">**Lecture de plusieurs lignes dans une fonction C#** - Le runtime Functions fournit un objet `IQueryable<T>` lié à la table.</span><span class="sxs-lookup"><span data-stu-id="8f38d-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span></span> <span data-ttu-id="8f38d-111">Le type `T` doit dériver de `TableEntity` ou implémenter `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="8f38d-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="8f38d-112">Les propriétés `partitionKey`, `rowKey`, `filter` et `take` ne sont pas utilisées dans ce scénario ; s’il y a lieu, vous pouvez utiliser l’objet `IQueryable` pour effectuer le filtrage éventuellement requis.</span><span class="sxs-lookup"><span data-stu-id="8f38d-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span></span> 
* <span data-ttu-id="8f38d-113">**Lecture de plusieurs lignes dans une fonction Node** - Définition des propriétés `filter` et `take`.</span><span class="sxs-lookup"><span data-stu-id="8f38d-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span></span> <span data-ttu-id="8f38d-114">Ne définissez pas `partitionKey` ni `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="8f38d-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="8f38d-115">**Écriture d'une ou plusieurs lignes dans une fonction C#** Le runtime Functions fournit un objet `ICollector<T>` ou `IAsyncCollector<T>` lié à la table, où `T` spécifie le schéma des entités à ajouter.</span><span class="sxs-lookup"><span data-stu-id="8f38d-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="8f38d-116">En général, le type `T` dérive de `TableEntity` ou implémente `ITableEntity`, mais ce n’est pas obligatoire.</span><span class="sxs-lookup"><span data-stu-id="8f38d-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="8f38d-117">Les propriétés `partitionKey`, `rowKey`, `filter` et `take` ne sont pas utilisées dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="8f38d-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="8f38d-118">Liaison d’entrée d'une table Storage</span><span class="sxs-lookup"><span data-stu-id="8f38d-118">Storage table input binding</span></span>
<span data-ttu-id="8f38d-119">La liaison d’entrée d'une table Azure Storage vous permet d’utiliser une table Storage dans votre fonction.</span><span class="sxs-lookup"><span data-stu-id="8f38d-119">The Azure Storage table input binding enables you to use a storage table in your function.</span></span> 

<span data-ttu-id="8f38d-120">L’entrée de table Storage d’une fonction utilise les objets JSON suivants dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="8f38d-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to read - see below>",
    "rowKey": "<RowKey of table entity to read - see below>",
    "take": "<Maximum number of entities to read in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="8f38d-121">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="8f38d-121">Note the following:</span></span> 

* <span data-ttu-id="8f38d-122">Utilisez `partitionKey` et `rowKey` pour lire une seule entité.</span><span class="sxs-lookup"><span data-stu-id="8f38d-122">Use `partitionKey` and `rowKey` together to read a single entity.</span></span> <span data-ttu-id="8f38d-123">Ces propriétés sont facultatives.</span><span class="sxs-lookup"><span data-stu-id="8f38d-123">These properties are optional.</span></span> 
* <span data-ttu-id="8f38d-124">`connection` doit contenir le nom d’un paramètre d’application comportant une chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="8f38d-124">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="8f38d-125">Dans le portail Azure, l’éditeur standard sous l’onglet **Intégrer** configure ce paramètre d’application pour vous quand vous créez un compte Stockage ou en sélectionne un.</span><span class="sxs-lookup"><span data-stu-id="8f38d-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="8f38d-126">Vous pouvez également [configurer ce paramètre d’application manuellement](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="8f38d-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="8f38d-127">Utilisation en entrée</span><span class="sxs-lookup"><span data-stu-id="8f38d-127">Input usage</span></span>
<span data-ttu-id="8f38d-128">Dans les fonctions C#, vous liez l'entité (ou les entités) de table d’entrée à l’aide d’un paramètre nommé dans la signature de la fonction, comme `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="8f38d-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="8f38d-129">Où `T` est le type de données dans lequel vous souhaitez désérialiser les données, et `paramName` le nom que vous avez spécifié dans la [liaison d’entrée](#input).</span><span class="sxs-lookup"><span data-stu-id="8f38d-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="8f38d-130">Dans les fonctions Node.js, vous accédez à l'entité (ou les entités) de table d’entrée à l’aide de `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="8f38d-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="8f38d-131">Les données d’entrée peuvent être désérialisées dans les fonctions Node.js ou C#.</span><span class="sxs-lookup"><span data-stu-id="8f38d-131">The input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="8f38d-132">Les objets désérialisés ont des propriétés `RowKey` et `PartitionKey`.</span><span class="sxs-lookup"><span data-stu-id="8f38d-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="8f38d-133">Dans les fonctions C#, vous pouvez également effectuer une liaison vers un des types suivants (le runtime Functions tente de désérialiser les données de la table à l’aide de ce type) :</span><span class="sxs-lookup"><span data-stu-id="8f38d-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span></span>

* <span data-ttu-id="8f38d-134">Tout type qui implémente `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="8f38d-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="8f38d-135">Exemple d’entrée</span><span class="sxs-lookup"><span data-stu-id="8f38d-135">Input sample</span></span>
<span data-ttu-id="8f38d-136">Supposons que vous avez le fichier function.json suivant, qui utilise un déclencheur de file d’attente pour lire une seule ligne du tableau.</span><span class="sxs-lookup"><span data-stu-id="8f38d-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span></span> <span data-ttu-id="8f38d-137">Le JSON spécifie `PartitionKey` 
`RowKey`.</span><span class="sxs-lookup"><span data-stu-id="8f38d-137">The JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="8f38d-138">`"rowKey": "{queueTrigger}"` indique que la clé de ligne provient de la chaîne de message de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="8f38d-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span></span>

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

<span data-ttu-id="8f38d-139">Consultez l’exemple spécifique au langage, qui lit une entité de table unique.</span><span class="sxs-lookup"><span data-stu-id="8f38d-139">See the language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="8f38d-140">C#</span><span class="sxs-lookup"><span data-stu-id="8f38d-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="8f38d-141">F#</span><span class="sxs-lookup"><span data-stu-id="8f38d-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="8f38d-142">Node.JS</span><span class="sxs-lookup"><span data-stu-id="8f38d-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="8f38d-143">Exemple d’entrée en C#</span><span class="sxs-lookup"><span data-stu-id="8f38d-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="8f38d-144">Exemple d’entrée en F#</span><span class="sxs-lookup"><span data-stu-id="8f38d-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="8f38d-145">Exemple d’entrée en Node.js</span><span class="sxs-lookup"><span data-stu-id="8f38d-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="8f38d-146">Liaison de sortie d'une table Storage</span><span class="sxs-lookup"><span data-stu-id="8f38d-146">Storage table output binding</span></span>
<span data-ttu-id="8f38d-147">La liaison de sortie de table Azure Storage vous permet d’écrire des entités dans une table Storage de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="8f38d-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span></span> 

<span data-ttu-id="8f38d-148">La sortie de table Storage pour une fonction utilise les objets JSON suivants dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="8f38d-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to write - see below>",
    "rowKey": "<RowKey of table entity to write - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="8f38d-149">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="8f38d-149">Note the following:</span></span> 

* <span data-ttu-id="8f38d-150">Utilisez `partitionKey` et `rowKey` pour écire une seule entité.</span><span class="sxs-lookup"><span data-stu-id="8f38d-150">Use `partitionKey` and `rowKey` together to write a single entity.</span></span> <span data-ttu-id="8f38d-151">Ces propriétés sont facultatives.</span><span class="sxs-lookup"><span data-stu-id="8f38d-151">These properties are optional.</span></span> <span data-ttu-id="8f38d-152">Vous pouvez également spécifier `PartitionKey` et `RowKey` lorsque vous créez les objets d’entité dans votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="8f38d-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span></span>
* <span data-ttu-id="8f38d-153">`connection` doit contenir le nom d’un paramètre d’application comportant une chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="8f38d-153">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="8f38d-154">Dans le portail Azure, l’éditeur standard sous l’onglet **Intégrer** configure ce paramètre d’application pour vous quand vous créez un compte Stockage ou en sélectionne un.</span><span class="sxs-lookup"><span data-stu-id="8f38d-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="8f38d-155">Vous pouvez également [configurer ce paramètre d’application manuellement](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="8f38d-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="8f38d-156">Utilisation en sortie</span><span class="sxs-lookup"><span data-stu-id="8f38d-156">Output usage</span></span>
<span data-ttu-id="8f38d-157">Dans les fonctions C#, vous liez la sortie de table à l’aide du paramètre `out` nommé dans la signature de la fonction, par exemple, `out <T> <name>`, où `T` est le type de données dans lequel vous souhaitez sérialiser les données, et `paramName` le nom que vous avez spécifié dans la [liaison de sortie](#output).</span><span class="sxs-lookup"><span data-stu-id="8f38d-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="8f38d-158">Dans les fonctions Node.js, vous accédez à la sortie de table en utilisant `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="8f38d-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="8f38d-159">Vous pouvez sérialiser les objets dans les fonctions Node.js ou C#.</span><span class="sxs-lookup"><span data-stu-id="8f38d-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="8f38d-160">Dans les fonctions C#, vous pouvez également lier les types suivants :</span><span class="sxs-lookup"><span data-stu-id="8f38d-160">In C# functions, you can also bind to the following types:</span></span>

* <span data-ttu-id="8f38d-161">Tout type qui implémente `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="8f38d-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="8f38d-162">`ICollector<T>` (pour la sortie de plusieurs entités.</span><span class="sxs-lookup"><span data-stu-id="8f38d-162">`ICollector<T>` (to output multiple entities.</span></span> <span data-ttu-id="8f38d-163">Voir l'[exemple](#outcsharp).)</span><span class="sxs-lookup"><span data-stu-id="8f38d-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="8f38d-164">`IAsyncCollector<T>` (version asynchrone de `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="8f38d-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="8f38d-165">`CloudTable` (utilisation du Kit de développement logiciel (SDK) de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8f38d-165">`CloudTable` (using the Azure Storage SDK.</span></span> <span data-ttu-id="8f38d-166">Voir l'[exemple](#readmulti).)</span><span class="sxs-lookup"><span data-stu-id="8f38d-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="8f38d-167">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="8f38d-167">Output sample</span></span>
<span data-ttu-id="8f38d-168">Les exemples de fichiers *function.json* et *run.csx* ci-après indiquent comment écrire plusieurs entités de table.</span><span class="sxs-lookup"><span data-stu-id="8f38d-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span></span>

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

<span data-ttu-id="8f38d-169">Consultez l’exemple spécifique au langage, qui crée plusieurs entités de table.</span><span class="sxs-lookup"><span data-stu-id="8f38d-169">See the language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="8f38d-170">C#</span><span class="sxs-lookup"><span data-stu-id="8f38d-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="8f38d-171">F#</span><span class="sxs-lookup"><span data-stu-id="8f38d-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="8f38d-172">Node.JS</span><span class="sxs-lookup"><span data-stu-id="8f38d-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="8f38d-173">Exemple de sortie en C#</span><span class="sxs-lookup"><span data-stu-id="8f38d-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="8f38d-174">Exemple de sortie en F#</span><span class="sxs-lookup"><span data-stu-id="8f38d-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 to 10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="8f38d-175">Exemple de sortie en Node.js</span><span class="sxs-lookup"><span data-stu-id="8f38d-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="8f38d-176">Exemple : lire plusieurs entités de table en C#</span><span class="sxs-lookup"><span data-stu-id="8f38d-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="8f38d-177">L’exemple de fichier *function.json* et de code C# ci-après lit les entités relatives à une clé de partition spécifiée dans le message de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="8f38d-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span></span>

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

<span data-ttu-id="8f38d-178">Le code C# ajoute une référence au SDK Azure Storage afin que le type d’entité puisse dériver de `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="8f38d-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8f38d-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8f38d-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

