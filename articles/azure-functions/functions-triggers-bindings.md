---
title: "aaaWork avec des déclencheurs et des liaisons dans les fonctions de Azure | Documents Microsoft"
description: "Découvrez comment toouse déclenche et les liaisons dans les fonctions Azure tooconnect vos événements de tooonline de l’exécution de code et les services basés sur le cloud."
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
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="21d2d-104">Concepts des déclencheurs et liaisons Azure Functions</span><span class="sxs-lookup"><span data-stu-id="21d2d-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="21d2d-105">Les fonctions Azure vous permet au code de toowrite de tooevents de réponse dans Azure et d’autres services via *déclencheurs* et *liaisons*.</span><span class="sxs-lookup"><span data-stu-id="21d2d-105">Azure Functions allows you toowrite code in response tooevents in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="21d2d-106">Cet article est une vue d’ensemble conceptuelle des déclencheurs et pour tous les langages de programmation pris en charge.</span><span class="sxs-lookup"><span data-stu-id="21d2d-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="21d2d-107">Fonctionnalités des liaisons tooall courantes sont décrites ici.</span><span class="sxs-lookup"><span data-stu-id="21d2d-107">Features that are common tooall bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="21d2d-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="21d2d-108">Overview</span></span>

<span data-ttu-id="21d2d-109">Les déclencheurs et les liaisons sont un toodefine de façon déclarative comment une fonction est appelée et les données qu’il fonctionne avec.</span><span class="sxs-lookup"><span data-stu-id="21d2d-109">Triggers and bindings are a declarative way toodefine how a function is invoked and what data it works with.</span></span> <span data-ttu-id="21d2d-110">Un *déclencheur* définit la façon dont une fonction est appelée.</span><span class="sxs-lookup"><span data-stu-id="21d2d-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="21d2d-111">Une fonction ne doit avoir qu’un seul déclencheur.</span><span class="sxs-lookup"><span data-stu-id="21d2d-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="21d2d-112">Les déclencheurs ont des données, qui est généralement hello charge utile qui a déclenché la fonction hello associées.</span><span class="sxs-lookup"><span data-stu-id="21d2d-112">Triggers have associated data, which is usually hello payload that triggered hello function.</span></span> 

<span data-ttu-id="21d2d-113">Entrée et sortie *liaisons* fournissent un toodata tooconnect de façon déclarative à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="21d2d-113">Input and output *bindings* provide a declarative way tooconnect toodata from within your code.</span></span> <span data-ttu-id="21d2d-114">Tootriggers similaires, vous spécifiez les chaînes de connexion et d’autres propriétés dans votre configuration de la fonction.</span><span class="sxs-lookup"><span data-stu-id="21d2d-114">Similar tootriggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="21d2d-115">Les liaisons sont facultatives et une fonction peut avoir plusieurs liaisons d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="21d2d-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="21d2d-116">À l’aide de déclencheurs et des liaisons, vous pouvez écrire du code qui est plus générique et ne pas coder en dur hello détails des services hello avec lequel elle interagit.</span><span class="sxs-lookup"><span data-stu-id="21d2d-116">Using triggers and bindings, you can write code that is more generic and does not hardcode hello details of hello services with which it interacts.</span></span> <span data-ttu-id="21d2d-117">Les données provenant deq services deviennent simplement des valeurs d’entrée pour votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="21d2d-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="21d2d-118">service de tooanother toooutput données (par exemple, créez une nouvelle ligne dans le stockage Table Azure), utilisez la valeur de retour de hello de méthode hello.</span><span class="sxs-lookup"><span data-stu-id="21d2d-118">toooutput data tooanother service (such as creating a new row in Azure Table Storage), use hello return value of hello method.</span></span> <span data-ttu-id="21d2d-119">Ou, si vous devez toooutput plusieurs valeurs, utilisez un objet d’assistance.</span><span class="sxs-lookup"><span data-stu-id="21d2d-119">Or, if you need toooutput multiple values, use a helper object.</span></span> <span data-ttu-id="21d2d-120">Les déclencheurs et les liaisons ont un **nom** propriété, qui est un identificateur que vous utilisez dans votre liaison de hello tooaccess code.</span><span class="sxs-lookup"><span data-stu-id="21d2d-120">Triggers and bindings have a **name** property, which is an identifier you use in your code tooaccess hello binding.</span></span>

<span data-ttu-id="21d2d-121">Vous pouvez configurer des déclencheurs et des liaisons dans hello **intégrer** portail de fonctions d’Azure hello.</span><span class="sxs-lookup"><span data-stu-id="21d2d-121">You can configure triggers and bindings in hello **Integrate** tab in hello Azure Functions portal.</span></span> <span data-ttu-id="21d2d-122">Dans les coulisses hello, hello l’interface utilisateur modifie un fichier appelé *function.json* fichier dans le répertoire de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="21d2d-122">Under hello covers, hello UI modifies a file called *function.json* file in hello function directory.</span></span> <span data-ttu-id="21d2d-123">Vous pouvez modifier ce fichier en modifiant toohello **éditeur avancé**.</span><span class="sxs-lookup"><span data-stu-id="21d2d-123">You can edit this file by changing toohello **Advanced editor**.</span></span>

<span data-ttu-id="21d2d-124">Hello tableau suivant présente les déclencheurs hello et des liaisons qui sont pris en charge avec les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="21d2d-124">hello following table shows hello triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="21d2d-125">Exemple : déclencheur de file d’attente et liaison de sortie de table</span><span class="sxs-lookup"><span data-stu-id="21d2d-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="21d2d-126">Supposons que vous toowrite une nouvelle tooAzure de ligne le stockage de Table chaque fois qu’un nouveau message s’affiche dans le stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="21d2d-126">Suppose you want toowrite a new row tooAzure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="21d2d-127">Ce scénario peut être implémenté à l’aide d’un déclencheur File d’attente Azure et d’une liaison de sortie Table.</span><span class="sxs-lookup"><span data-stu-id="21d2d-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="21d2d-128">Un déclencheur de la file d’attente nécessite hello informations Bonjour suivantes **intégrer** onglet :</span><span class="sxs-lookup"><span data-stu-id="21d2d-128">A queue trigger requires hello following information in hello **Integrate** tab:</span></span>

* <span data-ttu-id="21d2d-129">nom de Hello du paramètre d’application hello qui contient la chaîne de connexion de compte de stockage hello pour la file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="21d2d-129">hello name of hello app setting that contains hello storage account connection string for hello queue</span></span>
* <span data-ttu-id="21d2d-130">nom de file d’attente Hello</span><span class="sxs-lookup"><span data-stu-id="21d2d-130">hello queue name</span></span>
* <span data-ttu-id="21d2d-131">Hello identificateur dans votre code tooread hello du contenu d’hello file d’attente message, tel que `order`.</span><span class="sxs-lookup"><span data-stu-id="21d2d-131">hello identifier in your code tooread hello contents of hello queue message, such as `order`.</span></span>

<span data-ttu-id="21d2d-132">toowrite tooAzure le stockage de Table, utilisez une liaison de sortie avec hello les détails suivants :</span><span class="sxs-lookup"><span data-stu-id="21d2d-132">toowrite tooAzure Table Storage, use an output binding with hello following details:</span></span>

* <span data-ttu-id="21d2d-133">nom de Hello du paramètre d’application hello qui contient la chaîne de connexion de compte de stockage hello pour la table de hello</span><span class="sxs-lookup"><span data-stu-id="21d2d-133">hello name of hello app setting that contains hello storage account connection string for hello table</span></span>
* <span data-ttu-id="21d2d-134">nom de la table Hello</span><span class="sxs-lookup"><span data-stu-id="21d2d-134">hello table name</span></span>
* <span data-ttu-id="21d2d-135">Identificateur Hello dans votre toocreate de code de sortie des éléments, ou valeur de retour de hello à partir de la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="21d2d-135">hello identifier in your code toocreate output items, or hello return value from hello function.</span></span>

<span data-ttu-id="21d2d-136">Liaisons utilisent les paramètres de l’application pour hello tooenforce à des chaînes de connexion meilleures pratiques qui *function.json* ne contient pas de clés secrètes de service.</span><span class="sxs-lookup"><span data-stu-id="21d2d-136">Bindings use app settings for connection strings tooenforce hello best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="21d2d-137">Ensuite, utilisez les identificateurs hello vous avez fourni toointegrate avec le stockage Azure dans votre code.</span><span class="sxs-lookup"><span data-stu-id="21d2d-137">Then, use hello identifiers you provided toointegrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
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
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
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

<span data-ttu-id="21d2d-138">Voici hello *function.json* toohello précédant le code correspondant.</span><span class="sxs-lookup"><span data-stu-id="21d2d-138">Here is hello *function.json* that corresponds toohello preceding code.</span></span> <span data-ttu-id="21d2d-139">Notez que hello même configuration peut être utilisée, quel que soit le langage hello d’implémentation de la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="21d2d-139">Note that hello same configuration can be used, regardless of hello language of hello function implementation.</span></span>

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
<span data-ttu-id="21d2d-140">contenu de hello tooview et modification de *function.json* Bonjour portail Azure, cliquez sur hello **éditeur avancé** option hello **intégrer** onglet de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="21d2d-140">tooview and edit hello contents of *function.json* in hello Azure portal, click hello **Advanced editor** option on hello **Integrate** tab of your function.</span></span>

<span data-ttu-id="21d2d-141">Pour plus d’exemples de code et de détails sur l’intégration avec Stockage Azure, consultez [Déclencheurs et liaisons Azure Functions pour Stockage Azure](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="21d2d-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="21d2d-142">Sens de la liaison</span><span class="sxs-lookup"><span data-stu-id="21d2d-142">Binding direction</span></span>

<span data-ttu-id="21d2d-143">Tous les déclencheurs et liaisons ont une propriété `direction` :</span><span class="sxs-lookup"><span data-stu-id="21d2d-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="21d2d-144">Pour les déclencheurs, direction de hello est toujours`in`</span><span class="sxs-lookup"><span data-stu-id="21d2d-144">For triggers, hello direction is always `in`</span></span>
- <span data-ttu-id="21d2d-145">Les liaisons d’entrée et de sortie utilisent `in` et `out`</span><span class="sxs-lookup"><span data-stu-id="21d2d-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="21d2d-146">Certaines liaisons prennent en charge un sens spécial `inout`.</span><span class="sxs-lookup"><span data-stu-id="21d2d-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="21d2d-147">Si vous utilisez `inout`, hello uniquement **éditeur avancé** est disponible dans hello **intégrer** onglet.</span><span class="sxs-lookup"><span data-stu-id="21d2d-147">If you use `inout`, only hello **Advanced editor** is available in hello **Integrate** tab.</span></span>

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a><span data-ttu-id="21d2d-148">À l’aide de tooreturn de type de retour de fonction hello une sortie unique</span><span class="sxs-lookup"><span data-stu-id="21d2d-148">Using hello function return type tooreturn a single output</span></span>

<span data-ttu-id="21d2d-149">Hello exemple précédent indique comment tooprovide de valeur de retour de fonction de hello toouse sortie tooa liaison, qui est obtenue à l’aide du paramètre de nom spécial hello `$return`.</span><span class="sxs-lookup"><span data-stu-id="21d2d-149">hello preceding example shows how toouse hello function return value tooprovide output tooa binding, which is achieved by using hello special name parameter `$return`.</span></span> <span data-ttu-id="21d2d-150">(Cela n’est pris en charge que dans les langages qui ont une valeur de retour, tels que C#, JavaScript et F#.) Si une fonction comporte plusieurs liaisons de sortie, utilisez `$return` pour un seul hello de liaisons de sortie.</span><span class="sxs-lookup"><span data-stu-id="21d2d-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of hello output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="21d2d-151">exemples de Hello ci-dessous montrent comment retournent les types sont utilisés avec les liaisons de sortie en c#, JavaScript et F #.</span><span class="sxs-lookup"><span data-stu-id="21d2d-151">hello examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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
// JavaScript: return a value in hello second parameter toocontext.done
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

## <a name="binding-datatype-property"></a><span data-ttu-id="21d2d-152">Liaison de propriété Datatype</span><span class="sxs-lookup"><span data-stu-id="21d2d-152">Binding dataType property</span></span>

<span data-ttu-id="21d2d-153">Dans .NET, utilisez le type de données hello types toodefine hello pour les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="21d2d-153">In .NET, use hello types toodefine hello data type for input data.</span></span> <span data-ttu-id="21d2d-154">Par exemple, utilisez `string` toobind toohello texte un déclencheur de la file d’attente et un tooread de tableau d’octets binaire.</span><span class="sxs-lookup"><span data-stu-id="21d2d-154">For instance, use `string` toobind toohello text of a queue trigger and a byte array tooread as binary.</span></span>

<span data-ttu-id="21d2d-155">Pour les langues qui sont typées dynamiquement tels que JavaScript, utilisez hello `dataType` propriété dans la définition de la liaison hello.</span><span class="sxs-lookup"><span data-stu-id="21d2d-155">For languages that are dynamically typed such as JavaScript, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="21d2d-156">Par exemple, tooread hello contenu d’une requête HTTP au format binaire, utilisez le type de hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="21d2d-156">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="21d2d-157">Les autres options pour `dataType` sont `stream` et `string`.</span><span class="sxs-lookup"><span data-stu-id="21d2d-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="21d2d-158">Résolution des paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="21d2d-158">Resolving app settings</span></span>
<span data-ttu-id="21d2d-159">En tant que meilleure pratique, les chaînes de connexion et les secrets doivent être gérés avec des paramètres de l’application, plutôt qu’avec des fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="21d2d-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="21d2d-160">Cela limite l’accès toothese secrets et le rend safe toostore *function.json* dans un référentiel de contrôle source publique.</span><span class="sxs-lookup"><span data-stu-id="21d2d-160">This limits access toothese secrets and makes it safe toostore *function.json* in a public source control repository.</span></span>

<span data-ttu-id="21d2d-161">Paramètres de l’application sont également utiles quand vous le souhaitez configuration toochange basée sur l’environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="21d2d-161">App settings are also useful whenever you want toochange configuration based on hello environment.</span></span> <span data-ttu-id="21d2d-162">Par exemple, dans un environnement de test, vous souhaiterez toomonitor un conteneur de stockage différent de file d’attente ou un objet blob.</span><span class="sxs-lookup"><span data-stu-id="21d2d-162">For example, in a test environment, you may want toomonitor a different queue or blob storage container.</span></span>

<span data-ttu-id="21d2d-163">Les paramètres de l’application sont résolus à chaque fois qu’une valeur est placée entre des signes de pourcentage, comme `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="21d2d-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="21d2d-164">Notez que hello `connection` est un cas spécial de propriété des déclencheurs et des liaisons et résout automatiquement les valeurs en tant que paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="21d2d-164">Note that hello `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="21d2d-165">exemple Hello est un déclencheur de file d’attente qui utilise un paramètre d’application `%input-queue-name%` tootrigger de file d’attente toodefine hello sur.</span><span class="sxs-lookup"><span data-stu-id="21d2d-165">hello following example is a queue trigger that uses an app setting `%input-queue-name%` toodefine hello queue tootrigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="21d2d-166">Propriétés de métadonnées de déclencheur</span><span class="sxs-lookup"><span data-stu-id="21d2d-166">Trigger metadata properties</span></span>

<span data-ttu-id="21d2d-167">Dans Ajout toohello charge utile de données fourni par un déclencheur (par exemple, la file d’attente message de salutation qui a déclenché une fonction), les déclencheurs de fournir des valeurs de métadonnées supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="21d2d-167">In addition toohello data payload provided by a trigger (such as hello queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="21d2d-168">Ces valeurs peuvent être utilisées comme paramètres d’entrée dans c# et F # ou propriétés hello `context.bindings` objet dans JavaScript.</span><span class="sxs-lookup"><span data-stu-id="21d2d-168">These values can be used as input parameters in C# and F# or properties on hello `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="21d2d-169">Par exemple, un déclencheur de la file d’attente prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="21d2d-169">For example, a queue trigger supports hello following properties:</span></span>

* <span data-ttu-id="21d2d-170">QueueTrigger - déclenchant le contenu du message si une chaîne valide</span><span class="sxs-lookup"><span data-stu-id="21d2d-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="21d2d-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="21d2d-171">DequeueCount</span></span>
* <span data-ttu-id="21d2d-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="21d2d-172">ExpirationTime</span></span>
* <span data-ttu-id="21d2d-173">ID</span><span class="sxs-lookup"><span data-stu-id="21d2d-173">Id</span></span>
* <span data-ttu-id="21d2d-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="21d2d-174">InsertionTime</span></span>
* <span data-ttu-id="21d2d-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="21d2d-175">NextVisibleTime</span></span>
* <span data-ttu-id="21d2d-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="21d2d-176">PopReceipt</span></span>

<span data-ttu-id="21d2d-177">Détails des propriétés de métadonnées pour chaque déclencheur sont décrits dans la rubrique de référence correspondante hello.</span><span class="sxs-lookup"><span data-stu-id="21d2d-177">Details of metadata properties for each trigger are described in hello corresponding reference topic.</span></span> <span data-ttu-id="21d2d-178">Documentation est également disponible dans hello **intégrer** onglet du portail hello, Bonjour **Documentation** section sous la zone de configuration de liaison hello.</span><span class="sxs-lookup"><span data-stu-id="21d2d-178">Documentation is also available in hello **Integrate** tab of hello portal, in hello **Documentation** section below hello binding configuration area.</span></span>  

<span data-ttu-id="21d2d-179">Par exemple, étant donné que les déclencheurs de l’objet blob ont des retards, vous pouvez utiliser un toorun de déclencheur de file d’attente votre fonction (consultez [déclencheur du stockage Blob](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="21d2d-179">For example, since blob triggers have some delays, you can use a queue trigger toorun your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="21d2d-180">message de file d’attente Hello contiendrait tootrigger de nom de fichier blob hello sur.</span><span class="sxs-lookup"><span data-stu-id="21d2d-180">hello queue message would contain hello blob filename tootrigger on.</span></span> <span data-ttu-id="21d2d-181">À l’aide de hello `queueTrigger` propriété de métadonnées, vous pouvez définir ce comportement dans votre configuration, plutôt que dans votre code.</span><span class="sxs-lookup"><span data-stu-id="21d2d-181">Using hello `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="21d2d-182">Les propriétés de métadonnées à partir d’un déclencheur peuvent également être utilisées dans un *expression de liaison* pour une autre liaison, comme décrit dans hello suivant la section.</span><span class="sxs-lookup"><span data-stu-id="21d2d-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in hello following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="21d2d-183">Modèles et expressions de liaison</span><span class="sxs-lookup"><span data-stu-id="21d2d-183">Binding expressions and patterns</span></span>

<span data-ttu-id="21d2d-184">Une des fonctionnalités plus puissantes de hello des déclencheurs et des liaisons *liaison d’expressions*.</span><span class="sxs-lookup"><span data-stu-id="21d2d-184">One of hello most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="21d2d-185">Au sein de votre liaison, vous pouvez définir des modèles d’expression qui peuvent ensuite être utilisés dans d’autres liaisons ou votre code.</span><span class="sxs-lookup"><span data-stu-id="21d2d-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="21d2d-186">Métadonnées de déclencheur peuvent également servir de liaison d’expressions, comme indiqué dans l’exemple hello Bonjour précédant la section.</span><span class="sxs-lookup"><span data-stu-id="21d2d-186">Trigger metadata can also be used in binding expressions, as show in hello sample in hello preceding section.</span></span>

<span data-ttu-id="21d2d-187">Par exemple, supposons que vous souhaitiez tooresize des images dans le conteneur de stockage blob particulier, similaire toohello **taille de l’Image** modèle Bonjour **nouvelle fonction** page.</span><span class="sxs-lookup"><span data-stu-id="21d2d-187">For example, suppose you want tooresize images in particular blob storage container, similar toohello **Image Resizer** template in hello **New Function** page.</span></span> <span data-ttu-id="21d2d-188">Accédez trop**nouvelle fonction** -> langue **c#** -> scénario **exemples** -> **ImageResizer-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="21d2d-188">Go too**New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="21d2d-189">Voici hello *function.json* définition :</span><span class="sxs-lookup"><span data-stu-id="21d2d-189">Here is hello *function.json* definition:</span></span>

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

<span data-ttu-id="21d2d-190">Notez que hello `filename` paramètre est utilisé dans la définition du déclencheur hello blob ainsi que des objets blob de hello liaison de sortie.</span><span class="sxs-lookup"><span data-stu-id="21d2d-190">Notice that hello `filename` parameter is used in both hello blob trigger definition as well as hello blob output binding.</span></span> <span data-ttu-id="21d2d-191">Ce paramètre peut également être utilisé dans le code de fonction.</span><span class="sxs-lookup"><span data-stu-id="21d2d-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="21d2d-192">GUID aléatoires</span><span class="sxs-lookup"><span data-stu-id="21d2d-192">Random GUIDs</span></span>
<span data-ttu-id="21d2d-193">Fonctions Azure fournit une syntaxe plus de commodité pour générer des GUID dans vos liaisons, par le biais hello `{rand-guid}` expression de liaison.</span><span class="sxs-lookup"><span data-stu-id="21d2d-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through hello `{rand-guid}` binding expression.</span></span> <span data-ttu-id="21d2d-194">Hello exemple suivant utilise cette toogenerate un nom d’objet blob unique :</span><span class="sxs-lookup"><span data-stu-id="21d2d-194">hello following example uses this toogenerate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="21d2d-195">Heure actuelle</span><span class="sxs-lookup"><span data-stu-id="21d2d-195">Current time</span></span>

<span data-ttu-id="21d2d-196">Vous pouvez utiliser d’expression de liaison hello `DateTime`, ce qui donne trop`DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="21d2d-196">You can use hello binding expression `DateTime`, which resolves too`DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a><span data-ttu-id="21d2d-197">Lier les propriétés d’entrée de toocustom dans une expression de liaison</span><span class="sxs-lookup"><span data-stu-id="21d2d-197">Bind toocustom input properties in a binding expression</span></span>

<span data-ttu-id="21d2d-198">Expressions de liaison peuvent également référencer des propriétés qui sont définies dans la charge utile de déclencheur hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="21d2d-198">Binding expressions can also reference properties that are defined in hello trigger payload itself.</span></span> <span data-ttu-id="21d2d-199">Par exemple, vous voudrez fichier de stockage des objets blob toodynamically bind tooa à partir d’un nom de fichier fourni dans un webhook.</span><span class="sxs-lookup"><span data-stu-id="21d2d-199">For example, you may want toodynamically bind tooa blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="21d2d-200">Par exemple, hello suivant *function.json* utilise une propriété appelée `BlobName` à partir de la charge utile de déclencheur hello :</span><span class="sxs-lookup"><span data-stu-id="21d2d-200">For example, hello following *function.json* uses a property called `BlobName` from hello trigger payload:</span></span>

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

<span data-ttu-id="21d2d-201">tooaccomplish cette dans c# et F #, vous devez définir un POCO qui définit les champs hello qui seront désérialisés dans la charge utile de déclencheur hello.</span><span class="sxs-lookup"><span data-stu-id="21d2d-201">tooaccomplish this in C# and F#, you must define a POCO that defines hello fields that will be deserialized in hello trigger payload.</span></span>

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

<span data-ttu-id="21d2d-202">Dans JavaScript, la désérialisation JSON est effectuée automatiquement et vous pouvez utiliser directement les propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="21d2d-202">In JavaScript, JSON deserialization is automatically performed and you can use hello properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="21d2d-203">Configuration de la liaison des données lors de l’exécution</span><span class="sxs-lookup"><span data-stu-id="21d2d-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="21d2d-204">En c# et d’autres langages .NET, vous pouvez utiliser un modèle de liaison impérative, que les liaisons de déclarative toohello exécutée dans *function.json*.</span><span class="sxs-lookup"><span data-stu-id="21d2d-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed toohello declarative bindings in *function.json*.</span></span> <span data-ttu-id="21d2d-205">Liaison impératif est utile lorsque les paramètres de liaison doivent toobe calculée au moment de l’exécution au lieu de conception.</span><span class="sxs-lookup"><span data-stu-id="21d2d-205">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="21d2d-206">toolearn, voir [liaison lors de l’exécution via les liaisons impératifs](functions-reference-csharp.md#imperative-bindings) dans la référence du développeur hello c#.</span><span class="sxs-lookup"><span data-stu-id="21d2d-206">toolearn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in hello C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21d2d-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="21d2d-207">Next steps</span></span>
<span data-ttu-id="21d2d-208">Pour plus d’informations sur une liaison spécifique, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="21d2d-208">For more information on a specific binding, see hello following articles:</span></span>

- [<span data-ttu-id="21d2d-209">HTTP et webhooks</span><span class="sxs-lookup"><span data-stu-id="21d2d-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="21d2d-210">Minuteur</span><span class="sxs-lookup"><span data-stu-id="21d2d-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="21d2d-211">Stockage de files d’attente</span><span class="sxs-lookup"><span data-stu-id="21d2d-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="21d2d-212">Stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="21d2d-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="21d2d-213">Stockage Table</span><span class="sxs-lookup"><span data-stu-id="21d2d-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="21d2d-214">Concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="21d2d-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="21d2d-215">Service Bus</span><span class="sxs-lookup"><span data-stu-id="21d2d-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="21d2d-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="21d2d-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="21d2d-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="21d2d-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="21d2d-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="21d2d-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="21d2d-219">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="21d2d-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="21d2d-220">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="21d2d-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="21d2d-221">Fichier externe</span><span class="sxs-lookup"><span data-stu-id="21d2d-221">External file</span></span>](functions-bindings-external-file.md)
