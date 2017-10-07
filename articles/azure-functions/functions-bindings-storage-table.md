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
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="0ee57-104">Liaisons de table Azure Functions Storage</span><span class="sxs-lookup"><span data-stu-id="0ee57-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0ee57-105">Cet article explique comment tooconfigure et code le stockage Azure table liaisons dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee57-105">This article explains how tooconfigure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="0ee57-106">Azure Functions prend en charge les liaisons d’entrée et de sortie pour les tables Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0ee57-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="0ee57-107">liaison de table de stockage Hello prend en charge hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="0ee57-107">hello Storage table binding supports hello following scenarios:</span></span>

* <span data-ttu-id="0ee57-108">**Lecture d’une seule ligne dans une fonction C# ou Node.js** - Définition de `partitionKey` et `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="0ee57-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="0ee57-109">Hello `filter` et `take` propriétés ne sont pas utilisées dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="0ee57-109">hello `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="0ee57-110">**Lecture de plusieurs lignes dans une fonction c#** -hello fonctions runtime fournit un `IQueryable<T>` objet lié toohello table.</span><span class="sxs-lookup"><span data-stu-id="0ee57-110">**Read multiple rows in a C# function** - hello Functions runtime provides an `IQueryable<T>` object bound toohello table.</span></span> <span data-ttu-id="0ee57-111">Le type `T` doit dériver de `TableEntity` ou implémenter `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="0ee57-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="0ee57-112">Hello `partitionKey`, `rowKey`, `filter`, et `take` propriétés ne sont pas utilisées dans ce scénario, vous pouvez utiliser hello `IQueryable` toodo l’objet de filtrage requis.</span><span class="sxs-lookup"><span data-stu-id="0ee57-112">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use hello `IQueryable` object toodo any filtering required.</span></span> 
* <span data-ttu-id="0ee57-113">**Lecture de plusieurs lignes dans une fonction de nœud** - hello définissez `filter` et `take` propriétés.</span><span class="sxs-lookup"><span data-stu-id="0ee57-113">**Read multiple rows in a Node function** - Set hello `filter` and `take` properties.</span></span> <span data-ttu-id="0ee57-114">Ne définissez pas `partitionKey` ni `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="0ee57-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="0ee57-115">**Écrivez une ou plusieurs lignes dans une fonction c#** -hello fonctions runtime fournit un `ICollector<T>` ou `IAsyncCollector<T>` toohello liée, table, où `T` Spécifie le schéma de hello d’entités de hello souhaité tooadd.</span><span class="sxs-lookup"><span data-stu-id="0ee57-115">**Write one or more rows in a C# function** - hello Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound toohello table, where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="0ee57-116">En général, le type `T` dérive de `TableEntity` ou implémente `ITableEntity`, mais ce n’est pas obligatoire.</span><span class="sxs-lookup"><span data-stu-id="0ee57-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="0ee57-117">Hello `partitionKey`, `rowKey`, `filter`, et `take` propriétés ne sont pas utilisées dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="0ee57-117">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="0ee57-118">Liaison d’entrée d'une table Storage</span><span class="sxs-lookup"><span data-stu-id="0ee57-118">Storage table input binding</span></span>
<span data-ttu-id="0ee57-119">Hello liaison d’entrée de table de stockage Azure vous permet de toouse une table de stockage dans votre fonction.</span><span class="sxs-lookup"><span data-stu-id="0ee57-119">hello Azure Storage table input binding enables you toouse a storage table in your function.</span></span> 

<span data-ttu-id="0ee57-120">Hello, fonction de tooa d’entrée de table de stockage utilise hello objets JSON Bonjour suivants `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="0ee57-120">hello Storage table input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="0ee57-121">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ee57-121">Note hello following:</span></span> 

* <span data-ttu-id="0ee57-122">Utilisez `partitionKey` et `rowKey` tooread ensemble une entité unique.</span><span class="sxs-lookup"><span data-stu-id="0ee57-122">Use `partitionKey` and `rowKey` together tooread a single entity.</span></span> <span data-ttu-id="0ee57-123">Ces propriétés sont facultatives.</span><span class="sxs-lookup"><span data-stu-id="0ee57-123">These properties are optional.</span></span> 
* <span data-ttu-id="0ee57-124">`connection`doit contenir nom hello d’un paramètre d’application qui contient une chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="0ee57-124">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="0ee57-125">Bonjour portail Azure, hello éditeur standard Bonjour **intégrer** onglet configure ce paramètre d’application pour vous lorsque vous créez un stockage de compte ou sélectionne un existant.</span><span class="sxs-lookup"><span data-stu-id="0ee57-125">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="0ee57-126">Vous pouvez également [configurer ce paramètre d’application manuellement](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="0ee57-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="0ee57-127">Utilisation en entrée</span><span class="sxs-lookup"><span data-stu-id="0ee57-127">Input usage</span></span>
<span data-ttu-id="0ee57-128">Dans les fonctions C#, vous liez toohello d’entrée table entité (ou les entités) à l’aide d’un paramètre nommé dans votre signature de fonction, comme `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="0ee57-128">In C# functions, you bind toohello input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="0ee57-129">Où `T` est que les données de hello toodeserialize, de type de données de hello et `paramName` est le nom hello spécifié Bonjour [liaison d’entrée](#input).</span><span class="sxs-lookup"><span data-stu-id="0ee57-129">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in hello [input binding](#input).</span></span> <span data-ttu-id="0ee57-130">Dans les fonctions de Node.js, vous accéder hello d’entrée table entité (ou les entités) à l’aide de `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="0ee57-130">In Node.js functions, you access hello input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="0ee57-131">les données d’entrée Hello pouvant être désérialisées dans les fonctions Node.js ou c#.</span><span class="sxs-lookup"><span data-stu-id="0ee57-131">hello input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="0ee57-132">les objets Hello désérialisé ont `RowKey` et `PartitionKey` propriétés.</span><span class="sxs-lookup"><span data-stu-id="0ee57-132">hello deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="0ee57-133">Dans les fonctions de c#, vous pouvez également lier tooany Hello les types suivants, et les fonctions hello runtime va tenter de désérialiser trop à l’aide de ce type de données de la table hello :</span><span class="sxs-lookup"><span data-stu-id="0ee57-133">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime will attempt too deserialize hello table data using that type:</span></span>

* <span data-ttu-id="0ee57-134">Tout type qui implémente `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="0ee57-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="0ee57-135">Exemple d’entrée</span><span class="sxs-lookup"><span data-stu-id="0ee57-135">Input sample</span></span>
<span data-ttu-id="0ee57-136">Supposé qu'avoir hello suivant function.json, qui utilise un tooread de déclencheur de file d’attente une seule ligne du tableau.</span><span class="sxs-lookup"><span data-stu-id="0ee57-136">Supposed you have hello following function.json, which uses a queue trigger tooread a single table row.</span></span> <span data-ttu-id="0ee57-137">Spécifie Hello JSON `PartitionKey`  
 `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="0ee57-137">hello JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="0ee57-138">`"rowKey": "{queueTrigger}"`Indique que cette clé de ligne hello provient de la chaîne de message de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="0ee57-138">`"rowKey": "{queueTrigger}"` indicates that hello row key comes from hello queue message string.</span></span>

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

<span data-ttu-id="0ee57-139">Voir exemple hello spécifiques au langage qui lit une entité de table unique.</span><span class="sxs-lookup"><span data-stu-id="0ee57-139">See hello language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="0ee57-140">C#</span><span class="sxs-lookup"><span data-stu-id="0ee57-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="0ee57-141">F#</span><span class="sxs-lookup"><span data-stu-id="0ee57-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="0ee57-142">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0ee57-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="0ee57-143">Exemple d’entrée en C#</span><span class="sxs-lookup"><span data-stu-id="0ee57-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="0ee57-144">Exemple d’entrée en F#</span><span class="sxs-lookup"><span data-stu-id="0ee57-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="0ee57-145">Exemple d’entrée en Node.js</span><span class="sxs-lookup"><span data-stu-id="0ee57-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="0ee57-146">Liaison de sortie d'une table Storage</span><span class="sxs-lookup"><span data-stu-id="0ee57-146">Storage table output binding</span></span>
<span data-ttu-id="0ee57-147">liaison vous permet de table de stockage toowrite entités tooa dans votre fonction de sortie Hello table de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee57-147">hello Azure Storage table output binding enables you toowrite entities tooa Storage table in your function.</span></span> 

<span data-ttu-id="0ee57-148">Hello sortie de table de stockage pour une fonction utilise hello objets JSON Bonjour suivants `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="0ee57-148">hello Storage table output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="0ee57-149">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ee57-149">Note hello following:</span></span> 

* <span data-ttu-id="0ee57-150">Utilisez `partitionKey` et `rowKey` toowrite ensemble une entité unique.</span><span class="sxs-lookup"><span data-stu-id="0ee57-150">Use `partitionKey` and `rowKey` together toowrite a single entity.</span></span> <span data-ttu-id="0ee57-151">Ces propriétés sont facultatives.</span><span class="sxs-lookup"><span data-stu-id="0ee57-151">These properties are optional.</span></span> <span data-ttu-id="0ee57-152">Vous pouvez également spécifier `PartitionKey` et `RowKey` lorsque vous créez hello objets d’entité dans votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="0ee57-152">You can also specify `PartitionKey` and `RowKey` when you create hello entity objects in your function code.</span></span>
* <span data-ttu-id="0ee57-153">`connection`doit contenir nom hello d’un paramètre d’application qui contient une chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="0ee57-153">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="0ee57-154">Bonjour portail Azure, hello éditeur standard Bonjour **intégrer** onglet configure ce paramètre d’application pour vous lorsque vous créez un stockage de compte ou sélectionne un existant.</span><span class="sxs-lookup"><span data-stu-id="0ee57-154">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="0ee57-155">Vous pouvez également [configurer ce paramètre d’application manuellement](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="0ee57-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="0ee57-156">Utilisation en sortie</span><span class="sxs-lookup"><span data-stu-id="0ee57-156">Output usage</span></span>
<span data-ttu-id="0ee57-157">Dans les fonctions C#, vous liez sortie de table toohello à l’aide de hello nommé `out` paramètre dans votre signature de fonction, comme `out <T> <name>`, où `T` est que les données de hello tooserialize, de type de données de hello et `paramName` est hello nom que vous avez spécifié dans hello [liaison de sortie](#output).</span><span class="sxs-lookup"><span data-stu-id="0ee57-157">In C# functions, you bind toohello table output by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in hello [output binding](#output).</span></span> <span data-ttu-id="0ee57-158">Dans les fonctions Node.js, vous accédez à table hello de sortie à l’aide de `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="0ee57-158">In Node.js functions, you access hello table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="0ee57-159">Vous pouvez sérialiser les objets dans les fonctions Node.js ou C#.</span><span class="sxs-lookup"><span data-stu-id="0ee57-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="0ee57-160">Dans les fonctions de c#, vous pouvez également lier toohello les types suivants :</span><span class="sxs-lookup"><span data-stu-id="0ee57-160">In C# functions, you can also bind toohello following types:</span></span>

* <span data-ttu-id="0ee57-161">Tout type qui implémente `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="0ee57-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="0ee57-162">`ICollector<T>`(toooutput plusieurs entités.</span><span class="sxs-lookup"><span data-stu-id="0ee57-162">`ICollector<T>` (toooutput multiple entities.</span></span> <span data-ttu-id="0ee57-163">Voir l'[exemple](#outcsharp).)</span><span class="sxs-lookup"><span data-stu-id="0ee57-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="0ee57-164">`IAsyncCollector<T>` (version asynchrone de `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="0ee57-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="0ee57-165">`CloudTable`(à l’aide de hello SDK Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0ee57-165">`CloudTable` (using hello Azure Storage SDK.</span></span> <span data-ttu-id="0ee57-166">Voir l'[exemple](#readmulti).)</span><span class="sxs-lookup"><span data-stu-id="0ee57-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="0ee57-167">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="0ee57-167">Output sample</span></span>
<span data-ttu-id="0ee57-168">suivant de Hello *function.json* et *run.csx* exemple illustre comment toowrite plusieurs entités de table.</span><span class="sxs-lookup"><span data-stu-id="0ee57-168">hello following *function.json* and *run.csx* example shows how toowrite multiple table entities.</span></span>

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

<span data-ttu-id="0ee57-169">Voir exemple hello spécifiques au langage qui crée plusieurs entités de table.</span><span class="sxs-lookup"><span data-stu-id="0ee57-169">See hello language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="0ee57-170">C#</span><span class="sxs-lookup"><span data-stu-id="0ee57-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="0ee57-171">F#</span><span class="sxs-lookup"><span data-stu-id="0ee57-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="0ee57-172">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0ee57-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="0ee57-173">Exemple de sortie en C#</span><span class="sxs-lookup"><span data-stu-id="0ee57-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="0ee57-174">Exemple de sortie en F#</span><span class="sxs-lookup"><span data-stu-id="0ee57-174">Output sample in F#</span></span> #
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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="0ee57-175">Exemple de sortie en Node.js</span><span class="sxs-lookup"><span data-stu-id="0ee57-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="0ee57-176">Exemple : lire plusieurs entités de table en C#</span><span class="sxs-lookup"><span data-stu-id="0ee57-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="0ee57-177">suivant de Hello *function.json* et exemple de code c# lit les entités d’une clé de partition qui est spécifié dans le message de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="0ee57-177">hello following *function.json* and C# code example reads entities for a partition key that is specified in hello queue message.</span></span>

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

<span data-ttu-id="0ee57-178">Hello code c# ajoute un toohello référence SDK de stockage Azure afin que le type d’entité hello peut dériver de `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="0ee57-178">hello C# code adds a reference toohello Azure Storage SDK so that hello entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0ee57-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0ee57-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

