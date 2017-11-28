---
title: "Liaisons de fichier externe Azure Functions (version préliminaire) | Microsoft Docs"
description: Utilisation de liaisons du fichiers externes dans Azure Functions
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 2082e4e9b23271be93f3e3ab43997c3243238da8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="14cad-103">Liaisons de fichiers externes Azure Functions (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="14cad-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="14cad-104">Cet article montre comment manipuler les fichiers à partir de différents fournisseurs SaaS (par exemple, OneDrive, Dropbox) au sein de votre fonction en utilisant des liaisons intégrées.</span><span class="sxs-lookup"><span data-stu-id="14cad-104">This article shows how to manipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="14cad-105">Azure Functions prend en charge les liaisons de déclencheur, d’entrée et de sortie pour les fichiers externes.</span><span class="sxs-lookup"><span data-stu-id="14cad-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="14cad-106">Cette liaison crée des connexions d’API aux fournisseurs SaaS, ou utilise des connexions d’API existantes à partir du groupe de ressources de votre application Function App.</span><span class="sxs-lookup"><span data-stu-id="14cad-106">This binding creates API connections to SaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="14cad-107">Connexions de fichiers prises en charge</span><span class="sxs-lookup"><span data-stu-id="14cad-107">Supported File connections</span></span>

|<span data-ttu-id="14cad-108">Connecteur</span><span class="sxs-lookup"><span data-stu-id="14cad-108">Connector</span></span>|<span data-ttu-id="14cad-109">Déclencheur</span><span class="sxs-lookup"><span data-stu-id="14cad-109">Trigger</span></span>|<span data-ttu-id="14cad-110">Entrée</span><span class="sxs-lookup"><span data-stu-id="14cad-110">Input</span></span>|<span data-ttu-id="14cad-111">Sortie</span><span class="sxs-lookup"><span data-stu-id="14cad-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="14cad-112">Box</span><span class="sxs-lookup"><span data-stu-id="14cad-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="14cad-113">x</span><span class="sxs-lookup"><span data-stu-id="14cad-113">x</span></span>|<span data-ttu-id="14cad-114">x</span><span class="sxs-lookup"><span data-stu-id="14cad-114">x</span></span>|<span data-ttu-id="14cad-115">x</span><span class="sxs-lookup"><span data-stu-id="14cad-115">x</span></span>
|[<span data-ttu-id="14cad-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="14cad-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="14cad-117">x</span><span class="sxs-lookup"><span data-stu-id="14cad-117">x</span></span>|<span data-ttu-id="14cad-118">x</span><span class="sxs-lookup"><span data-stu-id="14cad-118">x</span></span>|<span data-ttu-id="14cad-119">x</span><span class="sxs-lookup"><span data-stu-id="14cad-119">x</span></span>
|[<span data-ttu-id="14cad-120">FTP</span><span class="sxs-lookup"><span data-stu-id="14cad-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="14cad-121">x</span><span class="sxs-lookup"><span data-stu-id="14cad-121">x</span></span>|<span data-ttu-id="14cad-122">x</span><span class="sxs-lookup"><span data-stu-id="14cad-122">x</span></span>|<span data-ttu-id="14cad-123">x</span><span class="sxs-lookup"><span data-stu-id="14cad-123">x</span></span>
|[<span data-ttu-id="14cad-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="14cad-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="14cad-125">x</span><span class="sxs-lookup"><span data-stu-id="14cad-125">x</span></span>|<span data-ttu-id="14cad-126">x</span><span class="sxs-lookup"><span data-stu-id="14cad-126">x</span></span>|<span data-ttu-id="14cad-127">x</span><span class="sxs-lookup"><span data-stu-id="14cad-127">x</span></span>
|[<span data-ttu-id="14cad-128">OneDrive Entreprise</span><span class="sxs-lookup"><span data-stu-id="14cad-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="14cad-129">x</span><span class="sxs-lookup"><span data-stu-id="14cad-129">x</span></span>|<span data-ttu-id="14cad-130">x</span><span class="sxs-lookup"><span data-stu-id="14cad-130">x</span></span>|<span data-ttu-id="14cad-131">x</span><span class="sxs-lookup"><span data-stu-id="14cad-131">x</span></span>
|[<span data-ttu-id="14cad-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="14cad-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="14cad-133">x</span><span class="sxs-lookup"><span data-stu-id="14cad-133">x</span></span>|<span data-ttu-id="14cad-134">x</span><span class="sxs-lookup"><span data-stu-id="14cad-134">x</span></span>|<span data-ttu-id="14cad-135">x</span><span class="sxs-lookup"><span data-stu-id="14cad-135">x</span></span>
|[<span data-ttu-id="14cad-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="14cad-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="14cad-137">x</span><span class="sxs-lookup"><span data-stu-id="14cad-137">x</span></span>|<span data-ttu-id="14cad-138">x</span><span class="sxs-lookup"><span data-stu-id="14cad-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="14cad-139">Les connexions aux fichiers externes peuvent également servir dans les applications [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="14cad-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="14cad-140">Liaison de déclencheur de fichier externe</span><span class="sxs-lookup"><span data-stu-id="14cad-140">External File trigger binding</span></span>

<span data-ttu-id="14cad-141">Le déclencheur de fichier externe Azure vous permet de surveiller un dossier à distance et d’exécuter votre code de fonction en cas de détection de modifications.</span><span class="sxs-lookup"><span data-stu-id="14cad-141">The Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="14cad-142">Le déclencheur de fichier externe utilise les objets JSON suivants dans le tableau `bindings` de function.json</span><span class="sxs-lookup"><span data-stu-id="14cad-142">The external file trigger uses the following JSON objects in the `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder to monitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of the following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="14cad-143">Modèles de nom</span><span class="sxs-lookup"><span data-stu-id="14cad-143">Name patterns</span></span>
<span data-ttu-id="14cad-144">Vous pouvez spécifier un modèle de nom de fichier dans la propriété `path` .</span><span class="sxs-lookup"><span data-stu-id="14cad-144">You can specify a file name pattern in the `path` property.</span></span> <span data-ttu-id="14cad-145">Le dossier référencé doit exister dans le fournisseur SaaS.</span><span class="sxs-lookup"><span data-stu-id="14cad-145">The folder referenced must exist in the SaaS provider.</span></span>
<span data-ttu-id="14cad-146">Exemples :</span><span class="sxs-lookup"><span data-stu-id="14cad-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="14cad-147">Ce chemin d’accès trouverait un fichier appelé *original-File1.txt* dans le dossier *input*, et la variable `name` du code de fonction présenterait la valeur `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="14cad-147">This path would find a file named *original-File1.txt* in the *input* folder, and the value of the `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="14cad-148">Autre exemple :</span><span class="sxs-lookup"><span data-stu-id="14cad-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="14cad-149">Ce chemin d’accès trouverait également un fichier nommé *original-File1.txt*, et les variables `filename` et `fileextension` du code de fonction présenteraient respectivement les valeurs *original-File1* et *txt*.</span><span class="sxs-lookup"><span data-stu-id="14cad-149">This path would also find a file named *original-File1.txt*, and the value of the `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="14cad-150">Vous pouvez restreindre le type des fichiers à l’aide d’une valeur fixe pour l’extension de fichier.</span><span class="sxs-lookup"><span data-stu-id="14cad-150">You can restrict the file type of files by using a fixed value for the file extension.</span></span> <span data-ttu-id="14cad-151">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="14cad-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="14cad-152">Dans ce cas, seuls les fichiers *.png* dans le dossier *samples* déclenchent la fonction.</span><span class="sxs-lookup"><span data-stu-id="14cad-152">In this case, only *.png* files in the *samples* folder trigger the function.</span></span>

<span data-ttu-id="14cad-153">Les accolades sont des caractères spéciaux dans les modèles de nom.</span><span class="sxs-lookup"><span data-stu-id="14cad-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="14cad-154">Pour spécifier des noms de fichier qui présentent des accolades, doublez ces dernières.</span><span class="sxs-lookup"><span data-stu-id="14cad-154">To specify file names that have curly braces in the name, double the curly braces.</span></span>
<span data-ttu-id="14cad-155">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="14cad-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="14cad-156">Ce chemin trouverait un fichier nommé *{20140101}-soundfile.mp3* dans le dossier *images*, et la valeur de la variable `name` dans le code de fonction serait *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="14cad-156">This path would find a file named *{20140101}-soundfile.mp3* in the *images* folder, and the `name` variable value in the function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
The Azure Functions runtime makes sure that no external file trigger function gets called more than once for the same new or updated file.
It does so by maintaining *file receipts* to determine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in the Azure storage account for your function app
(specified by the `AzureWebJobsStorage` app setting). A file receipt has the following information:

* The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* The folder name
* The file type ("BlockFile" or "PageFile")
* The file name
* The ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

To force reprocessing of a file, delete the file receipt for that file from the *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="14cad-157">Gestion des fichiers incohérents</span><span class="sxs-lookup"><span data-stu-id="14cad-157">Handling poison files</span></span>
<span data-ttu-id="14cad-158">En cas d’échec d’une fonction de déclenchement de fichier externe, Azure Functions réessaie cette fonction jusqu’à 5 fois par défaut (première tentative comprise) pour un fichier donné.</span><span class="sxs-lookup"><span data-stu-id="14cad-158">When an external file trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given file.</span></span>
<span data-ttu-id="14cad-159">Si toutes les 5 tentatives échouent, Functions ajoute un message à une file d’attente Stockage nommée *webjobs-apihubtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="14cad-159">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="14cad-160">Le message en file d’attente associé aux fichiers incohérents correspond à un objet JSON, qui contient les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="14cad-160">The queue message for poison files is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="14cad-161">FunctionId (au format *&lt;nom de l’application de fonctions>*.Functions.*&lt;nom de la fonction>*)</span><span class="sxs-lookup"><span data-stu-id="14cad-161">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="14cad-162">FileType</span><span class="sxs-lookup"><span data-stu-id="14cad-162">FileType</span></span>
* <span data-ttu-id="14cad-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="14cad-163">FolderName</span></span>
* <span data-ttu-id="14cad-164">FileName</span><span class="sxs-lookup"><span data-stu-id="14cad-164">FileName</span></span>
* <span data-ttu-id="14cad-165">ETag (identificateur de version du fichier, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="14cad-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="14cad-166">Utilisation du déclencheur</span><span class="sxs-lookup"><span data-stu-id="14cad-166">Trigger usage</span></span>
<span data-ttu-id="14cad-167">Dans les fonctions C#, vous liez les données de fichier d’entrée à l’aide d’un paramètre nommé dans la signature de la fonction, comme `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="14cad-167">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="14cad-168">Où `T` est le type de données dans lequel vous souhaitez désérialiser les données, et `paramName` le nom que vous avez spécifié dans le [code JSON du déclencheur](#trigger).</span><span class="sxs-lookup"><span data-stu-id="14cad-168">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="14cad-169">Dans les fonctions Node.js, vous accédez aux données de fichier d’entrée en utilisant `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="14cad-169">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="14cad-170">Le fichier peut être désérialisé dans l’un des types suivants :</span><span class="sxs-lookup"><span data-stu-id="14cad-170">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="14cad-171">N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour les données de fichier sérialisées en JSON.</span><span class="sxs-lookup"><span data-stu-id="14cad-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="14cad-172">Si vous déclarez un type d’entrée personnalisé (par exemple, `FooType`), Azure Functions tente de désérialiser les données JSON dans le type spécifié.</span><span class="sxs-lookup"><span data-stu-id="14cad-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="14cad-173">Chaîne : utile pour les données de fichier texte.</span><span class="sxs-lookup"><span data-stu-id="14cad-173">String - useful for text file data.</span></span>

<span data-ttu-id="14cad-174">Dans les fonctions C#, vous pouvez également effectuer une liaison vers un des types suivants (le runtime Functions tente de désérialiser les données du fichier à l’aide de ce type) :</span><span class="sxs-lookup"><span data-stu-id="14cad-174">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="14cad-175">Exemple de déclencheur</span><span class="sxs-lookup"><span data-stu-id="14cad-175">Trigger sample</span></span>
<span data-ttu-id="14cad-176">Supposons le code function.json suivant, qui définit un déclencheur de fichier externe :</span><span class="sxs-lookup"><span data-stu-id="14cad-176">Suppose you have the following function.json, that defines an external file trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

<span data-ttu-id="14cad-177">Consultez l’exemple dans le langage de votre choix pour voir comment enregistrer le contenu de chaque fichier ajouté au dossier surveillé.</span><span class="sxs-lookup"><span data-stu-id="14cad-177">See the language-specific sample that logs the contents of each file that is added to the monitored folder.</span></span>

* [<span data-ttu-id="14cad-178">C#</span><span class="sxs-lookup"><span data-stu-id="14cad-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="14cad-179">Node.JS</span><span class="sxs-lookup"><span data-stu-id="14cad-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="14cad-180">Utilisation du déclencheur en C#</span><span class="sxs-lookup"><span data-stu-id="14cad-180">Trigger usage in C#</span></span> #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="14cad-181">Utilisation du déclencheur en Node.js</span><span class="sxs-lookup"><span data-stu-id="14cad-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="14cad-182">Liaison d’entrée de fichier externe</span><span class="sxs-lookup"><span data-stu-id="14cad-182">External File input binding</span></span>
<span data-ttu-id="14cad-183">La liaison d’entrée de fichier externe Azure vous permet d’utiliser un fichier à partir d’un dossier externe dans votre fonction.</span><span class="sxs-lookup"><span data-stu-id="14cad-183">The Azure external file input binding enables you to use a file from an external folder in your function.</span></span>

<span data-ttu-id="14cad-184">L’entrée de fichier externe d’une fonction utilise les objets JSON suivants dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="14cad-184">The external file input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="14cad-185">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="14cad-185">Note the following:</span></span>

* <span data-ttu-id="14cad-186">`path` doit contenir le nom du dossier et le nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="14cad-186">`path` must contain the folder name and the file name.</span></span> <span data-ttu-id="14cad-187">Par exemple, si votre fonction contient un [déclencheur de file d’attente](functions-bindings-storage-queue.md), vous pouvez utiliser `"path": "samples-workitems/{queueTrigger}"` pour pointer vers un fichier dans le dossier `samples-workitems` avec un nom qui correspond au nom de fichier spécifié dans le message du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="14cad-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="14cad-188">Utilisation en entrée</span><span class="sxs-lookup"><span data-stu-id="14cad-188">Input usage</span></span>
<span data-ttu-id="14cad-189">Dans les fonctions C#, vous liez les données de fichier d’entrée à l’aide d’un paramètre nommé dans la signature de la fonction, comme `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="14cad-189">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="14cad-190">Où `T` est le type de données dans lequel vous souhaitez désérialiser les données, et `paramName` le nom que vous avez spécifié dans la [liaison d’entrée](#input).</span><span class="sxs-lookup"><span data-stu-id="14cad-190">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="14cad-191">Dans les fonctions Node.js, vous accédez aux données de fichier d’entrée en utilisant `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="14cad-191">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="14cad-192">Le fichier peut être désérialisé dans l’un des types suivants :</span><span class="sxs-lookup"><span data-stu-id="14cad-192">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="14cad-193">N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour les données de fichier sérialisées en JSON.</span><span class="sxs-lookup"><span data-stu-id="14cad-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="14cad-194">Si vous déclarez un type d’entrée personnalisé (par exemple, `InputType`), Azure Functions tente de désérialiser les données JSON dans le type spécifié.</span><span class="sxs-lookup"><span data-stu-id="14cad-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="14cad-195">Chaîne : utile pour les données de fichier texte.</span><span class="sxs-lookup"><span data-stu-id="14cad-195">String - useful for text file data.</span></span>

<span data-ttu-id="14cad-196">Dans les fonctions C#, vous pouvez également effectuer une liaison vers un des types suivants (le runtime Functions tente de désérialiser les données du fichier à l’aide de ce type) :</span><span class="sxs-lookup"><span data-stu-id="14cad-196">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="14cad-197">Liaison de sortie de fichier externe</span><span class="sxs-lookup"><span data-stu-id="14cad-197">External File output binding</span></span>
<span data-ttu-id="14cad-198">La liaison de sortie de fichier externe Azure vous permet d’écrire des fichiers sur un dossier externe dans votre fonction.</span><span class="sxs-lookup"><span data-stu-id="14cad-198">The Azure external file output binding enables you to write files to an external folder in your function.</span></span>

<span data-ttu-id="14cad-199">La sortie de fichier externe pour une fonction utilise les objets JSON suivants dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="14cad-199">The external file output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="14cad-200">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="14cad-200">Note the following:</span></span>

* <span data-ttu-id="14cad-201">`path` doit contenir le nom du dossier et le nom du fichier sur lequel écrire.</span><span class="sxs-lookup"><span data-stu-id="14cad-201">`path` must contain the folder name and the file name to write to.</span></span> <span data-ttu-id="14cad-202">Par exemple, si votre fonction contient un [déclencheur de file d’attente](functions-bindings-storage-queue.md), vous pouvez utiliser `"path": "samples-workitems/{queueTrigger}"` pour pointer vers un fichier dans le dossier `samples-workitems` avec un nom qui correspond au nom de fichier spécifié dans le message du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="14cad-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="14cad-203">Utilisation en sortie</span><span class="sxs-lookup"><span data-stu-id="14cad-203">Output usage</span></span>
<span data-ttu-id="14cad-204">Dans les fonctions C#, vous liez le fichier de sortie à l’aide du paramètre `out` nommé dans la signature de la fonction, par exemple, `out <T> <name>`, où `T` est le type de données dans lequel vous souhaitez sérialiser les données, et `paramName` le nom que vous avez spécifié dans la [liaison de sortie](#output).</span><span class="sxs-lookup"><span data-stu-id="14cad-204">In C# functions, you bind to the output file by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="14cad-205">Dans les fonctions Node.js, vous accédez au fichier de sortie en utilisant `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="14cad-205">In Node.js functions, you access the output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="14cad-206">Vous pouvez écrire dans le fichier de sortie à l’aide d’un des types suivants :</span><span class="sxs-lookup"><span data-stu-id="14cad-206">You can write to the output file using any of the following types:</span></span>

* <span data-ttu-id="14cad-207">N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour la sérialisation JSON.</span><span class="sxs-lookup"><span data-stu-id="14cad-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="14cad-208">Si vous déclarez un type de sortie personnalisée (par exemple, `out OutputType paramName`), Azure Functions tente de sérialiser un objet en JSON.</span><span class="sxs-lookup"><span data-stu-id="14cad-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="14cad-209">Si le paramètre de sortie est Null quand la fonction s’arrête, le runtime Functions crée un fichier comme objet Null.</span><span class="sxs-lookup"><span data-stu-id="14cad-209">If the output parameter is null when the function exits, the Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="14cad-210">Chaîne : (`out string paramName`) utile pour les données de fichier texte.</span><span class="sxs-lookup"><span data-stu-id="14cad-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="14cad-211">Le runtime Functions crée un fichier uniquement si le paramètre de chaîne n’est pas Null quand la fonction s’arrête.</span><span class="sxs-lookup"><span data-stu-id="14cad-211">the Functions runtime creates a file only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="14cad-212">Dans les fonctions C#, vous pouvez également définir une sortie vers les types suivants :</span><span class="sxs-lookup"><span data-stu-id="14cad-212">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="14cad-213">Entrée + Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="14cad-213">Input + Output sample</span></span>
<span data-ttu-id="14cad-214">Supposons le code function.json suivant, qui définit un [déclencheur de file d’attente Stockage](functions-bindings-storage-queue.md), une entrée de fichier externe et une sortie de fichier externe :</span><span class="sxs-lookup"><span data-stu-id="14cad-214">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="14cad-215">Consultez l’exemple dans le langage de votre choix pour voir comment copier le fichier d’entrée dans le fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="14cad-215">See the language-specific sample that copies the input file to the output file.</span></span>

* [<span data-ttu-id="14cad-216">C#</span><span class="sxs-lookup"><span data-stu-id="14cad-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="14cad-217">Node.JS</span><span class="sxs-lookup"><span data-stu-id="14cad-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="14cad-218">Utilisation en C#</span><span class="sxs-lookup"><span data-stu-id="14cad-218">Usage in C#</span></span> #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a><span data-ttu-id="14cad-219">Utilisation en Node.js</span><span class="sxs-lookup"><span data-stu-id="14cad-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="14cad-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14cad-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
