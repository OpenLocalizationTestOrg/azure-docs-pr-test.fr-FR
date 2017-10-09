---
title: "liaisons du fichier externe de fonctions aaaAzure (version préliminaire) | Documents Microsoft"
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
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="9ec94-103">Liaisons de fichiers externes Azure Functions (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="9ec94-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="9ec94-104">Cet article explique comment toomanipulate fichiers à partir de SaaS différents fournisseurs (par exemple, OneDrive, Dropbox) dans votre fonction utilisant des liaisons intégrées.</span><span class="sxs-lookup"><span data-stu-id="9ec94-104">This article shows how toomanipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="9ec94-105">Azure Functions prend en charge les liaisons de déclencheur, d’entrée et de sortie pour les fichiers externes.</span><span class="sxs-lookup"><span data-stu-id="9ec94-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="9ec94-106">Cette liaison crée des connexions de l’API tooSaaS fournisseurs, ou utilise des connexions API existantes du groupe de ressources de votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="9ec94-106">This binding creates API connections tooSaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="9ec94-107">Connexions de fichiers prises en charge</span><span class="sxs-lookup"><span data-stu-id="9ec94-107">Supported File connections</span></span>

|<span data-ttu-id="9ec94-108">Connecteur</span><span class="sxs-lookup"><span data-stu-id="9ec94-108">Connector</span></span>|<span data-ttu-id="9ec94-109">Déclencheur</span><span class="sxs-lookup"><span data-stu-id="9ec94-109">Trigger</span></span>|<span data-ttu-id="9ec94-110">Entrée</span><span class="sxs-lookup"><span data-stu-id="9ec94-110">Input</span></span>|<span data-ttu-id="9ec94-111">Sortie</span><span class="sxs-lookup"><span data-stu-id="9ec94-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="9ec94-112">Box</span><span class="sxs-lookup"><span data-stu-id="9ec94-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="9ec94-113">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-113">x</span></span>|<span data-ttu-id="9ec94-114">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-114">x</span></span>|<span data-ttu-id="9ec94-115">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-115">x</span></span>
|[<span data-ttu-id="9ec94-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="9ec94-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="9ec94-117">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-117">x</span></span>|<span data-ttu-id="9ec94-118">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-118">x</span></span>|<span data-ttu-id="9ec94-119">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-119">x</span></span>
|[<span data-ttu-id="9ec94-120">FTP</span><span class="sxs-lookup"><span data-stu-id="9ec94-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="9ec94-121">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-121">x</span></span>|<span data-ttu-id="9ec94-122">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-122">x</span></span>|<span data-ttu-id="9ec94-123">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-123">x</span></span>
|[<span data-ttu-id="9ec94-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="9ec94-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="9ec94-125">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-125">x</span></span>|<span data-ttu-id="9ec94-126">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-126">x</span></span>|<span data-ttu-id="9ec94-127">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-127">x</span></span>
|[<span data-ttu-id="9ec94-128">OneDrive Entreprise</span><span class="sxs-lookup"><span data-stu-id="9ec94-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="9ec94-129">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-129">x</span></span>|<span data-ttu-id="9ec94-130">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-130">x</span></span>|<span data-ttu-id="9ec94-131">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-131">x</span></span>
|[<span data-ttu-id="9ec94-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="9ec94-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="9ec94-133">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-133">x</span></span>|<span data-ttu-id="9ec94-134">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-134">x</span></span>|<span data-ttu-id="9ec94-135">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-135">x</span></span>
|[<span data-ttu-id="9ec94-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="9ec94-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="9ec94-137">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-137">x</span></span>|<span data-ttu-id="9ec94-138">x</span><span class="sxs-lookup"><span data-stu-id="9ec94-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="9ec94-139">Les connexions aux fichiers externes peuvent également servir dans les applications [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="9ec94-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="9ec94-140">Liaison de déclencheur de fichier externe</span><span class="sxs-lookup"><span data-stu-id="9ec94-140">External File trigger binding</span></span>

<span data-ttu-id="9ec94-141">déclencheur de fichier externe Azure Hello vous permet de surveiller un dossier distant et exécuter votre code de fonction lorsque des modifications sont détectées.</span><span class="sxs-lookup"><span data-stu-id="9ec94-141">hello Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="9ec94-142">déclencheur de fichier externe Hello utilise hello objets JSON Bonjour suivants `bindings` tableau de function.json</span><span class="sxs-lookup"><span data-stu-id="9ec94-142">hello external file trigger uses hello following JSON objects in hello `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="9ec94-143">Modèles de nom</span><span class="sxs-lookup"><span data-stu-id="9ec94-143">Name patterns</span></span>
<span data-ttu-id="9ec94-144">Vous pouvez spécifier un modèle de nom de fichier Bonjour `path` propriété.</span><span class="sxs-lookup"><span data-stu-id="9ec94-144">You can specify a file name pattern in hello `path` property.</span></span> <span data-ttu-id="9ec94-145">dossier Hello référencé doit exister dans le fournisseur de SaaS hello.</span><span class="sxs-lookup"><span data-stu-id="9ec94-145">hello folder referenced must exist in hello SaaS provider.</span></span>
<span data-ttu-id="9ec94-146">Exemples :</span><span class="sxs-lookup"><span data-stu-id="9ec94-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="9ec94-147">Ce chemin d’accès est de trouver un fichier nommé *d’origine-File1.txt* Bonjour *d’entrée* dossier et la valeur de hello de hello `name` variable dans le code de la fonction serait `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="9ec94-147">This path would find a file named *original-File1.txt* in hello *input* folder, and hello value of hello `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="9ec94-148">Autre exemple :</span><span class="sxs-lookup"><span data-stu-id="9ec94-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="9ec94-149">Ce chemin d’accès est également trouver un fichier nommé *d’origine-File1.txt*et la valeur hello Hello `filename` et `fileextension` variables dans le code de la fonction serait *d’origine-File1* et  *txt*.</span><span class="sxs-lookup"><span data-stu-id="9ec94-149">This path would also find a file named *original-File1.txt*, and hello value of hello `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="9ec94-150">Vous pouvez limiter le type de fichier hello de fichiers à l’aide d’une valeur fixe pour l’extension de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="9ec94-150">You can restrict hello file type of files by using a fixed value for hello file extension.</span></span> <span data-ttu-id="9ec94-151">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9ec94-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="9ec94-152">Dans ce cas, seul *.png* fichiers Bonjour *exemples* dossier déclencheur hello (fonction).</span><span class="sxs-lookup"><span data-stu-id="9ec94-152">In this case, only *.png* files in hello *samples* folder trigger hello function.</span></span>

<span data-ttu-id="9ec94-153">Les accolades sont des caractères spéciaux dans les modèles de nom.</span><span class="sxs-lookup"><span data-stu-id="9ec94-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="9ec94-154">toospecify les noms de fichiers qui ont des accolades dans nom hello, accolades doubles hello.</span><span class="sxs-lookup"><span data-stu-id="9ec94-154">toospecify file names that have curly braces in hello name, double hello curly braces.</span></span>
<span data-ttu-id="9ec94-155">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9ec94-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="9ec94-156">Ce chemin d’accès est de trouver un fichier nommé *{20140101}-soundfile.mp3* Bonjour *images* dossier et hello `name` valeur de la variable dans le code de la fonction hello serait *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="9ec94-156">This path would find a file named *{20140101}-soundfile.mp3* in hello *images* folder, and hello `name` variable value in hello function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="9ec94-157">Gestion des fichiers incohérents</span><span class="sxs-lookup"><span data-stu-id="9ec94-157">Handling poison files</span></span>
<span data-ttu-id="9ec94-158">En cas d’échec d’une fonction de déclencheur de fichier externe, les fonctions de Azure essaie de nouveau cette fonction des heures de too5 par défaut (y compris la première tentative de hello) pour un fichier donné.</span><span class="sxs-lookup"><span data-stu-id="9ec94-158">When an external file trigger function fails, Azure Functions retries that function up too5 times by default (including hello first try) for a given file.</span></span>
<span data-ttu-id="9ec94-159">Si toutes les 5 tentatives échouent, les fonctions ajoute un message tooa stockage file d’attente nommée *webjobs-apihubtrigger-incohérents*.</span><span class="sxs-lookup"><span data-stu-id="9ec94-159">If all 5 tries fail, Functions adds a message tooa Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="9ec94-160">message de file d’attente Hello pour les fichiers de messages incohérents est un objet JSON qui contient les propriétés suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="9ec94-160">hello queue message for poison files is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="9ec94-161">ID de fonction (au format de hello  *&lt;nom de l’application fonction >*. Fonctions.  *&lt;nom de la fonction >*)</span><span class="sxs-lookup"><span data-stu-id="9ec94-161">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="9ec94-162">FileType</span><span class="sxs-lookup"><span data-stu-id="9ec94-162">FileType</span></span>
* <span data-ttu-id="9ec94-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="9ec94-163">FolderName</span></span>
* <span data-ttu-id="9ec94-164">FileName</span><span class="sxs-lookup"><span data-stu-id="9ec94-164">FileName</span></span>
* <span data-ttu-id="9ec94-165">ETag (identificateur de version du fichier, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="9ec94-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="9ec94-166">Utilisation du déclencheur</span><span class="sxs-lookup"><span data-stu-id="9ec94-166">Trigger usage</span></span>
<span data-ttu-id="9ec94-167">Dans les fonctions C#, vous lier des données de fichier d’entrée toohello à l’aide d’un paramètre nommé dans votre signature de fonction, comme `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="9ec94-167">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="9ec94-168">Où `T` est que les données de hello toodeserialize, de type de données de hello et `paramName` est le nom hello spécifié dans le [déclencher JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="9ec94-168">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="9ec94-169">Dans les fonctions de Node.js, vous accédez à l’aide des données de fichier d’entrée hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="9ec94-169">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="9ec94-170">fichier de Hello pouvant être désérialisé dans n’importe quel Hello les types suivants :</span><span class="sxs-lookup"><span data-stu-id="9ec94-170">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="9ec94-171">N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour les données de fichier sérialisées en JSON.</span><span class="sxs-lookup"><span data-stu-id="9ec94-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="9ec94-172">Si vous déclarez un type d’entrée personnalisé (par exemple, `FooType`), des données JSON toodeserialize hello tente de fonctions d’Azure vers le type spécifié.</span><span class="sxs-lookup"><span data-stu-id="9ec94-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="9ec94-173">Chaîne : utile pour les données de fichier texte.</span><span class="sxs-lookup"><span data-stu-id="9ec94-173">String - useful for text file data.</span></span>

<span data-ttu-id="9ec94-174">Dans les fonctions C#, vous pouvez également lier tooany des types suivants de hello et hello fonctions runtime essaie de désérialiser des données de fichier hello à l’aide de ce type :</span><span class="sxs-lookup"><span data-stu-id="9ec94-174">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="9ec94-175">Exemple de déclencheur</span><span class="sxs-lookup"><span data-stu-id="9ec94-175">Trigger sample</span></span>
<span data-ttu-id="9ec94-176">Supposez que vous avez hello suivant function.json, qui définit un déclencheur de fichier externe :</span><span class="sxs-lookup"><span data-stu-id="9ec94-176">Suppose you have hello following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="9ec94-177">Voir exemple hello spécifiques au langage qui enregistre le contenu de hello de chaque fichier qui est ajouté à toohello les dossier surveillé.</span><span class="sxs-lookup"><span data-stu-id="9ec94-177">See hello language-specific sample that logs hello contents of each file that is added toohello monitored folder.</span></span>

* [<span data-ttu-id="9ec94-178">C#</span><span class="sxs-lookup"><span data-stu-id="9ec94-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="9ec94-179">Node.JS</span><span class="sxs-lookup"><span data-stu-id="9ec94-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="9ec94-180">Utilisation du déclencheur en C#</span><span class="sxs-lookup"><span data-stu-id="9ec94-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="9ec94-181">Utilisation du déclencheur en Node.js</span><span class="sxs-lookup"><span data-stu-id="9ec94-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="9ec94-182">Liaison d’entrée de fichier externe</span><span class="sxs-lookup"><span data-stu-id="9ec94-182">External File input binding</span></span>
<span data-ttu-id="9ec94-183">liaison d’entrée de fichier externe Azure Hello vous permet de toouse un fichier à partir d’un dossier externe dans votre fonction.</span><span class="sxs-lookup"><span data-stu-id="9ec94-183">hello Azure external file input binding enables you toouse a file from an external folder in your function.</span></span>

<span data-ttu-id="9ec94-184">fonction tooa d’entrée de fichier externe Hello utilise hello objets JSON Bonjour suivants `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="9ec94-184">hello external file input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="9ec94-185">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="9ec94-185">Note hello following:</span></span>

* <span data-ttu-id="9ec94-186">`path`doit contenir le nom du dossier hello et nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="9ec94-186">`path` must contain hello folder name and hello file name.</span></span> <span data-ttu-id="9ec94-187">Par exemple, si vous avez un [déclencheur de la file d’attente](functions-bindings-storage-queue.md) dans votre fonction, vous pouvez utiliser `"path": "samples-workitems/{queueTrigger}"` toopoint tooa fichier hello `samples-workitems` dossier avec un nom qui correspond au nom de fichier hello spécifié dans le message d’appel du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="9ec94-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="9ec94-188">Utilisation en entrée</span><span class="sxs-lookup"><span data-stu-id="9ec94-188">Input usage</span></span>
<span data-ttu-id="9ec94-189">Dans les fonctions C#, vous lier des données de fichier d’entrée toohello à l’aide d’un paramètre nommé dans votre signature de fonction, comme `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="9ec94-189">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="9ec94-190">Où `T` est que les données de hello toodeserialize, de type de données de hello et `paramName` est le nom hello spécifié dans le [liaison d’entrée](#input).</span><span class="sxs-lookup"><span data-stu-id="9ec94-190">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [input binding](#input).</span></span> <span data-ttu-id="9ec94-191">Dans les fonctions de Node.js, vous accédez à l’aide des données de fichier d’entrée hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="9ec94-191">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="9ec94-192">fichier de Hello pouvant être désérialisé dans n’importe quel Hello les types suivants :</span><span class="sxs-lookup"><span data-stu-id="9ec94-192">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="9ec94-193">N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour les données de fichier sérialisées en JSON.</span><span class="sxs-lookup"><span data-stu-id="9ec94-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="9ec94-194">Si vous déclarez un type d’entrée personnalisé (par exemple, `InputType`), des données JSON toodeserialize hello tente de fonctions d’Azure vers le type spécifié.</span><span class="sxs-lookup"><span data-stu-id="9ec94-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="9ec94-195">Chaîne : utile pour les données de fichier texte.</span><span class="sxs-lookup"><span data-stu-id="9ec94-195">String - useful for text file data.</span></span>

<span data-ttu-id="9ec94-196">Dans les fonctions C#, vous pouvez également lier tooany des types suivants de hello et hello fonctions runtime essaie de désérialiser des données de fichier hello à l’aide de ce type :</span><span class="sxs-lookup"><span data-stu-id="9ec94-196">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="9ec94-197">Liaison de sortie de fichier externe</span><span class="sxs-lookup"><span data-stu-id="9ec94-197">External File output binding</span></span>
<span data-ttu-id="9ec94-198">liaison vous permet de toowrite fichiers tooan un dossier externe dans votre fonction de sortie Hello Azure fichier externe.</span><span class="sxs-lookup"><span data-stu-id="9ec94-198">hello Azure external file output binding enables you toowrite files tooan external folder in your function.</span></span>

<span data-ttu-id="9ec94-199">les fichiers externes Hello de sortie pour une fonction utilise hello objets JSON Bonjour suivants `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="9ec94-199">hello external file output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="9ec94-200">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="9ec94-200">Note hello following:</span></span>

* <span data-ttu-id="9ec94-201">`path`doit contenir le nom du dossier hello et toowrite de nom de fichier hello pour.</span><span class="sxs-lookup"><span data-stu-id="9ec94-201">`path` must contain hello folder name and hello file name toowrite to.</span></span> <span data-ttu-id="9ec94-202">Par exemple, si vous avez un [déclencheur de la file d’attente](functions-bindings-storage-queue.md) dans votre fonction, vous pouvez utiliser `"path": "samples-workitems/{queueTrigger}"` toopoint tooa fichier hello `samples-workitems` dossier avec un nom qui correspond au nom de fichier hello spécifié dans le message d’appel du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="9ec94-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="9ec94-203">Utilisation en sortie</span><span class="sxs-lookup"><span data-stu-id="9ec94-203">Output usage</span></span>
<span data-ttu-id="9ec94-204">Dans les fonctions C#, vous liez fichier de sortie toohello à l’aide de hello nommé `out` paramètre dans votre signature de fonction, comme `out <T> <name>`, où `T` est que les données de hello tooserialize, de type de données de hello et `paramName` est hello nom que vous avez spécifié dans le [liaison de sortie](#output).</span><span class="sxs-lookup"><span data-stu-id="9ec94-204">In C# functions, you bind toohello output file by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in the [output binding](#output).</span></span> <span data-ttu-id="9ec94-205">Dans les fonctions de Node.js, vous accédez à l’aide de fichiers de sortie hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="9ec94-205">In Node.js functions, you access hello output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="9ec94-206">Vous pouvez écrire le fichier de sortie toohello à l’aide de hello les types suivants :</span><span class="sxs-lookup"><span data-stu-id="9ec94-206">You can write toohello output file using any of hello following types:</span></span>

* <span data-ttu-id="9ec94-207">N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour la sérialisation JSON.</span><span class="sxs-lookup"><span data-stu-id="9ec94-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="9ec94-208">Si vous déclarez un type de sortie personnalisée (par exemple, `out OutputType paramName`), les fonctions Azure tente tooserialize objet dans JSON.</span><span class="sxs-lookup"><span data-stu-id="9ec94-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts tooserialize object into JSON.</span></span> <span data-ttu-id="9ec94-209">Si le paramètre de sortie hello est null lorsque hello fonction s’arrête, hello fonctions runtime crée un fichier en tant qu’objet null.</span><span class="sxs-lookup"><span data-stu-id="9ec94-209">If hello output parameter is null when hello function exits, hello Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="9ec94-210">Chaîne : (`out string paramName`) utile pour les données de fichier texte.</span><span class="sxs-lookup"><span data-stu-id="9ec94-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="9ec94-211">Hello fonctions runtime crée un fichier uniquement si le paramètre de chaîne est non null lorsque hello fonction s’arrête.</span><span class="sxs-lookup"><span data-stu-id="9ec94-211">hello Functions runtime creates a file only if the string parameter is non-null when hello function exits.</span></span>

<span data-ttu-id="9ec94-212">Dans les fonctions de c#, vous pouvez également copier tooany Hello les types suivants :</span><span class="sxs-lookup"><span data-stu-id="9ec94-212">In C# functions you can also output tooany of hello following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="9ec94-213">Entrée + Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="9ec94-213">Input + Output sample</span></span>
<span data-ttu-id="9ec94-214">Supposons que vous avez hello suivant function.json, qui définit un [déclencheur de file d’attente de stockage](functions-bindings-storage-queue.md), l’entrée d’un fichier externe et un fichier externe de sortie :</span><span class="sxs-lookup"><span data-stu-id="9ec94-214">Suppose you have hello following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="9ec94-215">Voir exemple hello spécifiques au langage qui copie le fichier de sortie toohello hello fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="9ec94-215">See hello language-specific sample that copies hello input file toohello output file.</span></span>

* [<span data-ttu-id="9ec94-216">C#</span><span class="sxs-lookup"><span data-stu-id="9ec94-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="9ec94-217">Node.JS</span><span class="sxs-lookup"><span data-stu-id="9ec94-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="9ec94-218">Utilisation en C#</span><span class="sxs-lookup"><span data-stu-id="9ec94-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="9ec94-219">Utilisation en Node.js</span><span class="sxs-lookup"><span data-stu-id="9ec94-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="9ec94-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ec94-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
