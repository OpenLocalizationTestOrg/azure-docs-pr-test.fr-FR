---
title: "Utiliser des déclencheurs et des liaisons dans Azure Functions | Microsoft Docs"
description: "Découvrez comment utiliser des déclencheurs et des liaisons dans Azure Functions pour connecter l’exécution de votre code aux événements en ligne et aux services cloud."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: cc41debb2523df77be4db05817a4c7ac55604439
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="ab7fa-104">Concepts des déclencheurs et liaisons Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ab7fa-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="ab7fa-105">Azure Functions vous permet d’écrire du code en réponse aux événements dans Azure et d’autres services, via des *déclencheurs* et *liaisons*.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-105">Azure Functions allows you to write code in response to events in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="ab7fa-106">Cet article est une vue d’ensemble conceptuelle des déclencheurs et pour tous les langages de programmation pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="ab7fa-107">Les fonctionnalités communes à toutes les liaisons sont décrites ici.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-107">Features that are common to all bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="ab7fa-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ab7fa-108">Overview</span></span>

<span data-ttu-id="ab7fa-109">Les déclencheurs et les liaisons permettent de définir de manière déclarative la façon dont une fonction est appelée et les données avec lesquelles elle fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-109">Triggers and bindings are a declarative way to define how a function is invoked and what data it works with.</span></span> <span data-ttu-id="ab7fa-110">Un *déclencheur* définit la façon dont une fonction est appelée.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="ab7fa-111">Une fonction ne doit avoir qu’un seul déclencheur.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="ab7fa-112">Les déclencheurs sont associés à des données, généralement la charge utile qui a déclenché la fonction.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-112">Triggers have associated data, which is usually the payload that triggered the function.</span></span> 

<span data-ttu-id="ab7fa-113">Les *liaisons* d’entrée et de sortie fournissent un moyen déclaratif de se connecter à des données à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-113">Input and output *bindings* provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="ab7fa-114">Comme pour les déclencheurs, vous spécifiez des chaînes de connexion et d’autres propriétés dans votre configuration des fonctions.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-114">Similar to triggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="ab7fa-115">Les liaisons sont facultatives et une fonction peut avoir plusieurs liaisons d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="ab7fa-116">À l’aide de déclencheurs et de liaisons, vous pouvez écrire du code qui est plus générique et qui ne code pas en dur les détails des services avec lesquels il interagit.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-116">Using triggers and bindings, you can write code that is more generic and does not hardcode the details of the services with which it interacts.</span></span> <span data-ttu-id="ab7fa-117">Les données provenant deq services deviennent simplement des valeurs d’entrée pour votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="ab7fa-118">Pour exporter des données vers un autre service (comme la création d’une nouvelle ligne dans le stockage de table Azure), utilisez la valeur de retour de la méthode.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-118">To output data to another service (such as creating a new row in Azure Table Storage), use the return value of the method.</span></span> <span data-ttu-id="ab7fa-119">Autrement, si vous avez besoin de plusieurs valeurs de sortie, utilisez un objet d’assistance.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-119">Or, if you need to output multiple values, use a helper object.</span></span> <span data-ttu-id="ab7fa-120">Les déclencheurs et les liaisons ont une propriété **Nom**, qui est un identificateur que vous utilisez dans votre code pour accéder à la liaison.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-120">Triggers and bindings have a **name** property, which is an identifier you use in your code to access the binding.</span></span>

<span data-ttu-id="ab7fa-121">Vous pouvez configurer des déclencheurs et liaisons dans l’onglet **Intégrer** du portail Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-121">You can configure triggers and bindings in the **Integrate** tab in the Azure Functions portal.</span></span> <span data-ttu-id="ab7fa-122">En coulisses, l’interface utilisateur modifie un fichier appelé *function.json* dans le répertoire de la fonction.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-122">Under the covers, the UI modifies a file called *function.json* file in the function directory.</span></span> <span data-ttu-id="ab7fa-123">Vous pouvez modifier ce fichier en choisissant l’**Éditeur avancé**.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-123">You can edit this file by changing to the **Advanced editor**.</span></span>

<span data-ttu-id="ab7fa-124">Le tableau suivant montre les déclencheurs et liaisons qui sont pris en charge avec Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-124">The following table shows the triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="ab7fa-125">Exemple : déclencheur de file d’attente et liaison de sortie de table</span><span class="sxs-lookup"><span data-stu-id="ab7fa-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="ab7fa-126">Imaginons que vous souhaitiez écrire une nouvelle ligne dans Stockage Table Azure à chaque fois qu’un nouveau message s’affiche dans Stockage File d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-126">Suppose you want to write a new row to Azure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="ab7fa-127">Ce scénario peut être implémenté à l’aide d’un déclencheur File d’attente Azure et d’une liaison de sortie Table.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="ab7fa-128">Un déclencheur de file d’attente nécessite les informations suivantes dans l’onglet **Intégrer** :</span><span class="sxs-lookup"><span data-stu-id="ab7fa-128">A queue trigger requires the following information in the **Integrate** tab:</span></span>

* <span data-ttu-id="ab7fa-129">Le nom du paramètre d’application qui contient la chaîne de connexion de compte de stockage pour la file d’attente</span><span class="sxs-lookup"><span data-stu-id="ab7fa-129">The name of the app setting that contains the storage account connection string for the queue</span></span>
* <span data-ttu-id="ab7fa-130">Le nom de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="ab7fa-130">The queue name</span></span>
* <span data-ttu-id="ab7fa-131">L’identificateur dans votre code pour lire le contenu du message de la file d’attente, tel que `order`.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-131">The identifier in your code to read the contents of the queue message, such as `order`.</span></span>

<span data-ttu-id="ab7fa-132">Pour écrire dans Stockage Table Azure, utilisez une liaison de sortie avec les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ab7fa-132">To write to Azure Table Storage, use an output binding with the following details:</span></span>

* <span data-ttu-id="ab7fa-133">Le nom du paramètre d’application qui contient la chaîne de connexion de compte de stockage pour la table</span><span class="sxs-lookup"><span data-stu-id="ab7fa-133">The name of the app setting that contains the storage account connection string for the table</span></span>
* <span data-ttu-id="ab7fa-134">Le nom de la table</span><span class="sxs-lookup"><span data-stu-id="ab7fa-134">The table name</span></span>
* <span data-ttu-id="ab7fa-135">L’identificateur dans votre code pour créer des éléments de sortie ou la valeur de retour de la fonction.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-135">The identifier in your code to create output items, or the return value from the function.</span></span>

<span data-ttu-id="ab7fa-136">Les liaisons utilisent des paramètres d’application pour les chaînes de connexion afin d’appliquer la meilleure pratique qui consiste à ce que *function.json* ne contient aucun secret de service.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-136">Bindings use app settings for connection strings to enforce the best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="ab7fa-137">Utilisez ensuite les identificateurs que vous avez fournis pour intégrer Stockage Azure dans votre code.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-137">Then, use the identifiers you provided to integrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The second parameter to context.done is used as the value for the new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

<span data-ttu-id="ab7fa-138">Voici le *function.json* qui correspond au code précédent.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-138">Here is the *function.json* that corresponds to the preceding code.</span></span> <span data-ttu-id="ab7fa-139">Veuillez noter que la même configuration peut être utilisée, quelle que soit la langue de l’implémentation de la fonction.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-139">Note that the same configuration can be used, regardless of the language of the function implementation.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
<span data-ttu-id="ab7fa-140">Pour afficher et modifier le contenu de *function.json* dans le portail Azure, cliquez sur l’option **Éditeur avancé** dans l’onglet **Intégrer** de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-140">To view and edit the contents of *function.json* in the Azure portal, click the **Advanced editor** option on the **Integrate** tab of your function.</span></span>

<span data-ttu-id="ab7fa-141">Pour plus d’exemples de code et de détails sur l’intégration avec Stockage Azure, consultez [Déclencheurs et liaisons Azure Functions pour Stockage Azure](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ab7fa-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="ab7fa-142">Sens de la liaison</span><span class="sxs-lookup"><span data-stu-id="ab7fa-142">Binding direction</span></span>

<span data-ttu-id="ab7fa-143">Tous les déclencheurs et liaisons ont une propriété `direction` :</span><span class="sxs-lookup"><span data-stu-id="ab7fa-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="ab7fa-144">Pour les déclencheurs, le sens est toujours `in`</span><span class="sxs-lookup"><span data-stu-id="ab7fa-144">For triggers, the direction is always `in`</span></span>
- <span data-ttu-id="ab7fa-145">Les liaisons d’entrée et de sortie utilisent `in` et `out`</span><span class="sxs-lookup"><span data-stu-id="ab7fa-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="ab7fa-146">Certaines liaisons prennent en charge un sens spécial `inout`.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="ab7fa-147">Si vous utilisez `inout`, seule l’option **Éditeur avancé** est disponible dans l’onglet **Intégrer**.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-147">If you use `inout`, only the **Advanced editor** is available in the **Integrate** tab.</span></span>

## <a name="using-the-function-return-type-to-return-a-single-output"></a><span data-ttu-id="ab7fa-148">Utilisation du type de retour de fonction pour retourner une seule sortie</span><span class="sxs-lookup"><span data-stu-id="ab7fa-148">Using the function return type to return a single output</span></span>

<span data-ttu-id="ab7fa-149">L’exemple précédent montre comment utiliser la valeur de retour de fonction pour fournir la sortie à une liaison, ce qui nécessite d’utiliser le paramètre de nom spécial `$return`.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-149">The preceding example shows how to use the function return value to provide output to a binding, which is achieved by using the special name parameter `$return`.</span></span> <span data-ttu-id="ab7fa-150">(Cela n’est pris en charge que dans les langages qui ont une valeur de retour, tels que C#, JavaScript et F#.) Si une fonction comporte plusieurs liaisons de sortie, utilisez `$return` pour une seule des liaisons de sortie.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of the output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="ab7fa-151">Les exemples ci-dessous montrent comment les types de retour sont utilisés avec des liaisons de sortie dans C#, JavaScript et F#.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-151">The examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in the second parameter to context.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a><span data-ttu-id="ab7fa-152">Liaison de propriété Datatype</span><span class="sxs-lookup"><span data-stu-id="ab7fa-152">Binding dataType property</span></span>

<span data-ttu-id="ab7fa-153">Dans .NET, utilisez les types pour définir le type des données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-153">In .NET, use the types to define the data type for input data.</span></span> <span data-ttu-id="ab7fa-154">Par exemple, utilisez `string` pour lier au texte d’un déclencheur de file d’attente et un tableau d’octets pour lire sous forme binaire.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-154">For instance, use `string` to bind to the text of a queue trigger and a byte array to read as binary.</span></span>

<span data-ttu-id="ab7fa-155">Pour les langages dont le type est dynamique, tels que JavaScript, vous devez utiliser la propriété `dataType` dans la définition de la liaison.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-155">For languages that are dynamically typed such as JavaScript, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="ab7fa-156">Par exemple, pour lire le contenu d’une requête HTTP dans un format binaire, utilisez le type `binary` :</span><span class="sxs-lookup"><span data-stu-id="ab7fa-156">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="ab7fa-157">Les autres options pour `dataType` sont `stream` et `string`.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="ab7fa-158">Résolution des paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="ab7fa-158">Resolving app settings</span></span>
<span data-ttu-id="ab7fa-159">En tant que meilleure pratique, les chaînes de connexion et les secrets doivent être gérés avec des paramètres de l’application, plutôt qu’avec des fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="ab7fa-160">Cela limite l’accès à ces secrets et permet de stocker *function.json* en toute sécurité dans un référentiel de contrôle de code source public.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-160">This limits access to these secrets and makes it safe to store *function.json* in a public source control repository.</span></span>

<span data-ttu-id="ab7fa-161">Les paramètres de l’application sont également utiles lorsque vous souhaitez modifier la configuration en fonction de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-161">App settings are also useful whenever you want to change configuration based on the environment.</span></span> <span data-ttu-id="ab7fa-162">Par exemple, dans un environnement de test, vous pourriez vouloir surveiller une autre file d’attente ou un autre conteneur Stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-162">For example, in a test environment, you may want to monitor a different queue or blob storage container.</span></span>

<span data-ttu-id="ab7fa-163">Les paramètres de l’application sont résolus à chaque fois qu’une valeur est placée entre des signes de pourcentage, comme `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="ab7fa-164">Veuillez noter que la propriété `connection` des déclencheurs et liaisons est un cas spécial et résout automatiquement les valeurs en tant que paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-164">Note that the `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="ab7fa-165">L’exemple suivant est un déclencheur de file d’attente qui utilise un paramètre d’application `%input-queue-name%` pour définir la file d’attente sur laquelle effectuer le déclenchement.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-165">The following example is a queue trigger that uses an app setting `%input-queue-name%` to define the queue to trigger on.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a><span data-ttu-id="ab7fa-166">Propriétés de métadonnées de déclencheur</span><span class="sxs-lookup"><span data-stu-id="ab7fa-166">Trigger metadata properties</span></span>

<span data-ttu-id="ab7fa-167">En plus de la charge utile de données fournie par un déclencheur (par exemple, le message de file d’attente qui a déclenché une fonction), plusieurs déclencheurs fournissent des valeurs de métadonnées supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-167">In addition to the data payload provided by a trigger (such as the queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="ab7fa-168">Ces valeurs peuvent être utilisées comme paramètres d’entrée dans C# et F# ou comme propriétés sur l’objet `context.bindings` dans JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-168">These values can be used as input parameters in C# and F# or properties on the `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="ab7fa-169">Par exemple, un déclencheur de file d’attente prend en charge les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="ab7fa-169">For example, a queue trigger supports the following properties:</span></span>

* <span data-ttu-id="ab7fa-170">QueueTrigger - déclenchant le contenu du message si une chaîne valide</span><span class="sxs-lookup"><span data-stu-id="ab7fa-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="ab7fa-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="ab7fa-171">DequeueCount</span></span>
* <span data-ttu-id="ab7fa-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="ab7fa-172">ExpirationTime</span></span>
* <span data-ttu-id="ab7fa-173">ID</span><span class="sxs-lookup"><span data-stu-id="ab7fa-173">Id</span></span>
* <span data-ttu-id="ab7fa-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="ab7fa-174">InsertionTime</span></span>
* <span data-ttu-id="ab7fa-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="ab7fa-175">NextVisibleTime</span></span>
* <span data-ttu-id="ab7fa-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="ab7fa-176">PopReceipt</span></span>

<span data-ttu-id="ab7fa-177">Les détails des propriétés de métadonnées pour chaque déclencheur sont décrits dans la rubrique de référence correspondante.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-177">Details of metadata properties for each trigger are described in the corresponding reference topic.</span></span> <span data-ttu-id="ab7fa-178">La documentation est également disponible dans l’onglet **Intégrer** du portail, dans la section **Documentation** située sous la zone de configuration de liaison.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-178">Documentation is also available in the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.</span></span>  

<span data-ttu-id="ab7fa-179">Par exemple, étant donné que les déclencheurs d’objet blob connaissent des retards, vous pouvez utiliser un déclencheur de file d’attente pour exécuter votre fonction (voir [Déclencheur Stockage Blob](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="ab7fa-179">For example, since blob triggers have some delays, you can use a queue trigger to run your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="ab7fa-180">Le message de file d’attente contiendra le nom de fichier du blob à déclencher.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-180">The queue message would contain the blob filename to trigger on.</span></span> <span data-ttu-id="ab7fa-181">À l’aide de la propriété de métadonnées `queueTrigger`, vous pouvez spécifier ce comportement partout dans votre configuration, plutôt que dans votre code.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-181">Using the `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

<span data-ttu-id="ab7fa-182">Les propriétés de métadonnées provenant d’un déclencheur peuvent également être utilisées dans une *expression de liaison* pour une autre liaison, comme décrit dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in the following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="ab7fa-183">Modèles et expressions de liaison</span><span class="sxs-lookup"><span data-stu-id="ab7fa-183">Binding expressions and patterns</span></span>

<span data-ttu-id="ab7fa-184">Les *expressions de liaison* sont l’une des fonctionnalités les plus puissantes des déclencheurs et liaisons.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-184">One of the most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="ab7fa-185">Au sein de votre liaison, vous pouvez définir des modèles d’expression qui peuvent ensuite être utilisés dans d’autres liaisons ou votre code.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="ab7fa-186">Des métadonnées de déclencheur peuvent également être utilisées dans les expressions de liaison, comme indiqué dans l’exemple présenté dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-186">Trigger metadata can also be used in binding expressions, as show in the sample in the preceding section.</span></span>

<span data-ttu-id="ab7fa-187">Par exemple, imaginons que vous vouliez redimensionner des images d’un conteneur Stockage Blob donné, et ce de manière similaire au modèle **Redimensionnement d’image** de la page **Nouvelle fonction**.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-187">For example, suppose you want to resize images in particular blob storage container, similar to the **Image Resizer** template in the **New Function** page.</span></span> <span data-ttu-id="ab7fa-188">Accédez à **Nouvelle fonction** -> Langage **C#** -> Scénario **Exemples** -> **ImageResizer-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-188">Go to **New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="ab7fa-189">Voici la définition *function.json* :</span><span class="sxs-lookup"><span data-stu-id="ab7fa-189">Here is the *function.json* definition:</span></span>

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

<span data-ttu-id="ab7fa-190">Veuillez noter que le paramètre `filename` est utilisé aussi bien dans la définition du déclencheur d’objet blob que dans la liaison de sortie d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-190">Notice that the `filename` parameter is used in both the blob trigger definition as well as the blob output binding.</span></span> <span data-ttu-id="ab7fa-191">Ce paramètre peut également être utilisé dans le code de fonction.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="ab7fa-192">GUID aléatoires</span><span class="sxs-lookup"><span data-stu-id="ab7fa-192">Random GUIDs</span></span>
<span data-ttu-id="ab7fa-193">Azure Functions fournit une syntaxe pratique pour générer des GUID dans vos liaisons, via l’expression de liaison `{rand-guid}`.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through the `{rand-guid}` binding expression.</span></span> <span data-ttu-id="ab7fa-194">L’exemple suivant l’utilise pour générer un nom d’objet blob unique :</span><span class="sxs-lookup"><span data-stu-id="ab7fa-194">The following example uses this to generate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="ab7fa-195">Heure actuelle</span><span class="sxs-lookup"><span data-stu-id="ab7fa-195">Current time</span></span>

<span data-ttu-id="ab7fa-196">Vous pouvez utiliser l’expression de liaison `DateTime`, est résolue en `DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-196">You can use the binding expression `DateTime`, which resolves to `DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-to-custom-input-properties-in-a-binding-expression"></a><span data-ttu-id="ab7fa-197">Lier aux propriétés d’entrée personnalisées dans une expression de liaison</span><span class="sxs-lookup"><span data-stu-id="ab7fa-197">Bind to custom input properties in a binding expression</span></span>

<span data-ttu-id="ab7fa-198">Les expressions de liaison peuvent également référencer des propriétés définies dans la charge utile du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-198">Binding expressions can also reference properties that are defined in the trigger payload itself.</span></span> <span data-ttu-id="ab7fa-199">Par exemple, vous souhaiterez peut-être effectuer une liaison dynamique vers un fichier Stockage Blob à partir d’un nom de fichier fourni dans un webhook.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-199">For example, you may want to dynamically bind to a blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="ab7fa-200">Par exemple, le *function.json* suivant utilise une propriété appelée `BlobName` provenant de la charge utile du déclencheur :</span><span class="sxs-lookup"><span data-stu-id="ab7fa-200">For example, the following *function.json* uses a property called `BlobName` from the trigger payload:</span></span>

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

<span data-ttu-id="ab7fa-201">Pour y parvenir dans C# et F #, vous devez définir un objet POCO qui définit les champs qui seront désérialisés dans la charge utile du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-201">To accomplish this in C# and F#, you must define a POCO that defines the fields that will be deserialized in the trigger payload.</span></span>

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

<span data-ttu-id="ab7fa-202">Dans JavaScript, la désérialisation JSON est effectuée automatiquement et vous pouvez directement utiliser les propriétés.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-202">In JavaScript, JSON deserialization is automatically performed and you can use the properties directly.</span></span>

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="ab7fa-203">Configuration de la liaison des données lors de l’exécution</span><span class="sxs-lookup"><span data-stu-id="ab7fa-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="ab7fa-204">En C# et dans d’autres langages .NET, vous pouvez utiliser un schéma de liaison impératif, par opposition aux liaisons déclaratives *dans function.json*.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in *function.json*.</span></span> <span data-ttu-id="ab7fa-205">La liaison impérative est utile lorsque les paramètres de liaison doivent être calculés au moment du runtime plutôt que lors de la conception.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-205">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="ab7fa-206">Pour plus d’informations, voir [Liaison lors de l’exécution via des liaisons impératives](functions-reference-csharp.md#imperative-bindings) dans la référence du développeur C#.</span><span class="sxs-lookup"><span data-stu-id="ab7fa-206">To learn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in the C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab7fa-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ab7fa-207">Next steps</span></span>
<span data-ttu-id="ab7fa-208">Pour plus d’informations sur une liaison spécifique, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="ab7fa-208">For more information on a specific binding, see the following articles:</span></span>

- [<span data-ttu-id="ab7fa-209">HTTP et webhooks</span><span class="sxs-lookup"><span data-stu-id="ab7fa-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="ab7fa-210">Minuteur</span><span class="sxs-lookup"><span data-stu-id="ab7fa-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="ab7fa-211">Stockage de files d’attente</span><span class="sxs-lookup"><span data-stu-id="ab7fa-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="ab7fa-212">Stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="ab7fa-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="ab7fa-213">Stockage Table</span><span class="sxs-lookup"><span data-stu-id="ab7fa-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="ab7fa-214">Concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="ab7fa-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="ab7fa-215">Service Bus</span><span class="sxs-lookup"><span data-stu-id="ab7fa-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="ab7fa-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ab7fa-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="ab7fa-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="ab7fa-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="ab7fa-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="ab7fa-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="ab7fa-219">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="ab7fa-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="ab7fa-220">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="ab7fa-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="ab7fa-221">Fichier externe</span><span class="sxs-lookup"><span data-stu-id="ab7fa-221">External file</span></span>](functions-bindings-external-file.md)
