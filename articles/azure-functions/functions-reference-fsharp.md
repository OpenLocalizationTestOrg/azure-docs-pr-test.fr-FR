---
title: "Information de référence pour les développeurs F# sur Azure Functions | Microsoft Docs"
description: "Découvrez comment développer sur Azure Functions à l’aide de F#."
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "Azure fonctions, les fonctions, les événements de traitement, de webhooks, calcul dynamique, architecture sans F #"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1691d378263f6b4ce5072f5c621d8db02f774b5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="cd1f3-104">Informations de référence pour les développeurs F# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cd1f3-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd1f3-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="cd1f3-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="cd1f3-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="cd1f3-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="cd1f3-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="cd1f3-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="cd1f3-108">F# for Azure Functions est une solution conçue pour exécuter facilement de petits morceaux de code, ou « fonctions », dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud.</span></span> <span data-ttu-id="cd1f3-109">Les données circulent dans votre fonction F# par le biais d’arguments de fonction.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="cd1f3-110">Les noms d’argument sont spécifiés dans `function.json`, et il existe des noms prédéfinis pour accéder à des éléments tels que l’enregistreur de fonctions et les jetons d’annulation.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="cd1f3-111">Cet article repose sur l’hypothèse que vous avez déjà lu l’article [Informations de référence pour les développeurs sur Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="cd1f3-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="cd1f3-112">Fonctionnement de .fsx</span><span class="sxs-lookup"><span data-stu-id="cd1f3-112">How .fsx works</span></span>
<span data-ttu-id="cd1f3-113">Un fichier `.fsx` est un script F#.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="cd1f3-114">Il peut être considéré comme un projet F# contenu dans un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="cd1f3-115">Ce fichier contient à la fois le code de votre programme (dans ce cas précis, votre fonction Azure) et des directives concernant la gestion des dépendances.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-115">The file contains both the code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="cd1f3-116">Lorsque vous utilisez un fichier `.fsx` pour une fonction Azure, les assemblys généralement requis sont automatiquement inclus à votre intention, ce qui vous permet de vous concentrer sur la fonction plutôt que sur le code « réutilisable ».</span><span class="sxs-lookup"><span data-stu-id="cd1f3-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you to focus on the function rather than "boilerplate" code.</span></span>

## <a name="binding-to-arguments"></a><span data-ttu-id="cd1f3-117">Liaison aux arguments</span><span class="sxs-lookup"><span data-stu-id="cd1f3-117">Binding to arguments</span></span>
<span data-ttu-id="cd1f3-118">Chaque liaison prend en charge un ensemble spécifique d’arguments, comme décrit en détail dans [Informations de référence pour les développeurs sur les déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="cd1f3-118">Each binding supports some set of arguments, as detailed in the [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="cd1f3-119">Par exemple, l’une des liaisons d’argument prises en charge par un déclencheur d’objet blob est un objet CLR traditionnel (POCO), qui peut être exprimé à l’aide d’un enregistrement F#.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-119">For example, one of the argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="cd1f3-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="cd1f3-121">Votre fonction Azure F# utilisera un ou plusieurs arguments.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="cd1f3-122">Quand nous parlons d’arguments Azure Functions, nous faisons référence à des arguments *d’entrée* et à des arguments de *sortie*.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-122">When we talk about Azure Functions arguments, we refer to *input* arguments and *output* arguments.</span></span> <span data-ttu-id="cd1f3-123">Un argument d’entrée est exactement ce que son nom laisse entendre : une entrée pour votre fonction Azure F#.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-123">An input argument is exactly what it sounds like: input to your F# Azure Function.</span></span> <span data-ttu-id="cd1f3-124">Un argument de *sortie* correspond à des données mutables ou à un argument `byref<>` permettant de retransmettre des données *hors* de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way to pass data back *out* of your function.</span></span>

<span data-ttu-id="cd1f3-125">Dans l’exemple ci-dessus, `blob` est un argument d’entrée, tandis que `output` est un argument de sortie.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-125">In the example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="cd1f3-126">Notez que nous avons utilisé le type `byref<>` pour l’argument `output` (il n’est pas nécessaire d’ajouter l’annotation `[<Out>]`).</span><span class="sxs-lookup"><span data-stu-id="cd1f3-126">Notice that we used `byref<>` for `output` (there's no need to add the `[<Out>]` annotation).</span></span> <span data-ttu-id="cd1f3-127">L’utilisation d’un type `byref<>` permet à votre fonction de modifier l’enregistrement ou l’objet auxquels l’argument fait référence.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-127">Using a `byref<>` type allows your function to change which record or object the argument refers to.</span></span>

<span data-ttu-id="cd1f3-128">Lorsqu’un enregistrement F# est utilisé comme type d’entrée, la définition d’enregistrement doit être indiquée par `[<CLIMutable>]` pour permettre à l’infrastructure Azure Functions de définir les champs de manière appropriée avant de transmettre l’enregistrement à votre fonction.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-128">When an F# record is used as an input type, the record definition must be marked with `[<CLIMutable>]` in order to allow the Azure Functions framework to set the fields appropriately before passing the record to your function.</span></span> <span data-ttu-id="cd1f3-129">En arrière-plan, `[<CLIMutable>]` génère des méthodes setter pour les propriétés d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-129">Under the hood, `[<CLIMutable>]` generates setters for the record properties.</span></span> <span data-ttu-id="cd1f3-130">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="cd1f3-131">Une classe F# est également utilisable pour les arguments d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="cd1f3-132">Pour une classe, les propriétés nécessitent généralement des méthodes getter et setter.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="cd1f3-133">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="cd1f3-134">Journalisation</span><span class="sxs-lookup"><span data-stu-id="cd1f3-134">Logging</span></span>
<span data-ttu-id="cd1f3-135">Pour consigner la sortie dans vos [journaux de diffusion en continu](../app-service-web/web-sites-streaming-logs-and-console.md) dans F#, votre fonction doit utiliser un argument de type `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-135">To log output to your [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="cd1f3-136">Par souci de cohérence, nous vous recommandons de nommer cet argument `log`.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="cd1f3-137">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="cd1f3-138">Async</span><span class="sxs-lookup"><span data-stu-id="cd1f3-138">Async</span></span>
<span data-ttu-id="cd1f3-139">Il est possible d’utiliser le workflow `async`, mais le résultat doit renvoyer un élément `Task`.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-139">The `async` workflow can be used, but the result needs to return a `Task`.</span></span> <span data-ttu-id="cd1f3-140">Pour ce faire, utilisez `Async.StartAsTask`. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="cd1f3-141">Jeton d’annulation</span><span class="sxs-lookup"><span data-stu-id="cd1f3-141">Cancellation Token</span></span>
<span data-ttu-id="cd1f3-142">Si votre fonction doit gérer les arrêts de manière appropriée, vous pouvez lui fournir un argument [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) .</span><span class="sxs-lookup"><span data-stu-id="cd1f3-142">If your function needs to handle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="cd1f3-143">conjointement utilisable avec `async`. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="cd1f3-144">Importation des espaces de noms</span><span class="sxs-lookup"><span data-stu-id="cd1f3-144">Importing namespaces</span></span>
<span data-ttu-id="cd1f3-145">Les espaces de noms peuvent être ouverts de la manière habituelle :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-145">Namespaces can be opened in the usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="cd1f3-146">Les espaces de noms ci-après sont ouverts automatiquement :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-146">The following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="cd1f3-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="cd1f3-148">Référencement des assemblys externes</span><span class="sxs-lookup"><span data-stu-id="cd1f3-148">Referencing External Assemblies</span></span>
<span data-ttu-id="cd1f3-149">De même, les références d’assembly d’infrastructure sont ajoutées avec la directive `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="cd1f3-149">Similarly, framework assembly references be added with the `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="cd1f3-150">Les assemblys suivants sont ajoutés automatiquement par l’environnement hébergeant Azure Functions :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-150">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

* <span data-ttu-id="cd1f3-151">`mscorlib`</span><span class="sxs-lookup"><span data-stu-id="cd1f3-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="cd1f3-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="cd1f3-153">En outre, les assemblys ci-après ont une casse spécifique et peuvent être référencés par leur nom simple (par exemple, `#r "AssemblyName"`) :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-153">In addition, the following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="cd1f3-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="cd1f3-155">Si vous avez besoin de référencer un assembly privé, vous pouvez charger le fichier d’assembly dans un dossier `bin` relatif à votre fonction et le référencer à l’aide du nom de fichier (par exemple, `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="cd1f3-155">If you need to reference a private assembly, you can upload the assembly file into a `bin` folder relative to your function and reference it by using the file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="cd1f3-156">Pour plus d’informations sur le téléchargement de fichiers vers votre conteneur de fonctions, consultez la section suivante sur la gestion des packages.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-156">For information on how to upload files to your function folder, see the following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="cd1f3-157">Préambule destiné à l’éditeur</span><span class="sxs-lookup"><span data-stu-id="cd1f3-157">Editor Prelude</span></span>
<span data-ttu-id="cd1f3-158">Un éditeur prenant en charge F# Compiler Services ne reconnaît pas les espaces de noms et les assemblys automatiquement inclus par Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-158">An editor that supports F# Compiler Services will not be aware of the namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="cd1f3-159">Il peut donc être utile d’insérer un préambule conçu pour permettre à l’éditeur de localiser les assemblys que vous utilisez et d’ouvrir explicitement les espaces de noms.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-159">As such, it can be useful to include a prelude that helps the editor find the assemblies you are using, and to explicitly open namespaces.</span></span> <span data-ttu-id="cd1f3-160">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-160">For example:</span></span>

```fsharp
#if !COMPILED
#I "../../bin/Binaries/WebJobs.Script.Host"
#r "Microsoft.Azure.WebJobs.Host.dll"
#endif

open Sytem
open Microsoft.Azure.WebJobs.Host

let Run(blob: string, output: byref<string>, log: TraceWriter) =
    ...
```

<span data-ttu-id="cd1f3-161">Lorsque la solution Azure Functions exécute votre code, elle traite la source avec l’élément `COMPILED` défini, de sorte que le préambule destiné à l’éditeur sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-161">When Azure Functions executes your code, it processes the source with `COMPILED` defined, so the editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="cd1f3-162">Gestion des packages</span><span class="sxs-lookup"><span data-stu-id="cd1f3-162">Package management</span></span>
<span data-ttu-id="cd1f3-163">Pour utiliser des packages NuGet dans une fonction F#, ajoutez un fichier `project.json` au dossier de la fonction dans le système de fichiers de l’application de fonctions.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-163">To use NuGet packages in an F# function, add a `project.json` file to the the function's folder in the function app's file system.</span></span> <span data-ttu-id="cd1f3-164">Voici un exemple de fichier `project.json` ajoutant une référence de package NuGet à `Microsoft.ProjectOxford.Face` version 1.1.0 :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-164">Here is an example `project.json` file that adds a NuGet package reference to `Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

<span data-ttu-id="cd1f3-165">Seul .NET Framework 4.6 est pris en charge. Par conséquent, assurez-vous que votre fichier `project.json` spécifie `net46` comme indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-165">Only the .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="cd1f3-166">Lorsque vous chargez un fichier `project.json` , le runtime obtient les packages et ajoute automatiquement des références aux assemblys de packages.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-166">When you upload a `project.json` file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="cd1f3-167">Vous n’avez pas besoin d’ajouter de directives `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="cd1f3-167">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="cd1f3-168">Il vous suffit d’ajouter les instructions `open` requises à votre fichier `.fsx`.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-168">Just add the required `open` statements to your `.fsx` file.</span></span>

<span data-ttu-id="cd1f3-169">Si vous le souhaitez, vous pouvez placer automatiquement les assemblys de référence dans votre préambule destiné à l’éditeur, afin d’améliorer l’interaction de votre éditeur avec F# Compile Services.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-169">You may wish to put automatically references assemblies in your editor prelude, to improve your editor's interaction with F# Compile Services.</span></span>

### <a name="how-to-add-a-projectjson-file-to-your-azure-function"></a><span data-ttu-id="cd1f3-170">Ajout d’un fichier `project.json` à votre fonction Azure</span><span class="sxs-lookup"><span data-stu-id="cd1f3-170">How to add a `project.json` file to your Azure Function</span></span>
1. <span data-ttu-id="cd1f3-171">Commencez par vous assurer que votre conteneur de fonctions est en cours d’exécution. Ce que vous pouvez faire en ouvrant votre fonction dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-171">Begin by making sure your function app is running, which you can do by opening your function in the Azure portal.</span></span> <span data-ttu-id="cd1f3-172">Il donne également accès aux journaux de diffusion en continu où le résultat de l’installation du package s’affiche.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-172">This also gives access to the streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="cd1f3-173">Pour charger un fichier `project.json` , utilisez l’une des méthodes décrites dans l’article [Comment mettre à jour les fichiers du conteneur de fonctions](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="cd1f3-173">To upload a `project.json` file, use one of the methods described in [how to update function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="cd1f3-174">Si vous utilisez l’article [Déploiement continu pour Azure Functions](functions-continuous-deployment.md), vous pouvez ajouter un fichier `project.json` à votre branche intermédiaire afin de le tester avant de l’ajouter à votre branche de déploiement.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file to your staging branch in order to experiment with it before adding it to your deployment branch.</span></span>
3. <span data-ttu-id="cd1f3-175">Une fois le fichier `project.json` ajouté, une sortie semblable à l’exemple ci-après apparaîtra dans le journal de diffusion en continu de votre fonction :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-175">After the `project.json` file is added, you will see output similar to the following example in your function's streaming log:</span></span>

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a><span data-ttu-id="cd1f3-176">Variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="cd1f3-176">Environment variables</span></span>
<span data-ttu-id="cd1f3-177">Pour obtenir une variable d’environnement ou une valeur de paramètre d’application, utilisez `System.Environment.GetEnvironmentVariable`. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-177">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="cd1f3-178">Réutilisation du code .fsx</span><span class="sxs-lookup"><span data-stu-id="cd1f3-178">Reusing .fsx code</span></span>
<span data-ttu-id="cd1f3-179">Vous pouvez utiliser le code d’autres fichiers `.fsx` au moyen d’une directive `#load`.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="cd1f3-180">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-180">For example:</span></span>

`run.fsx`

```fsharp
#load "logger.fsx"

let Run(timer: TimerInfo, log: TraceWriter) =
    mylog log (sprintf "Timer: %s" DateTime.Now.ToString())
```

`logger.fsx`

```fsharp
let mylog(log: TraceWriter, text: string) =
    log.Verbose(text);
```

<span data-ttu-id="cd1f3-181">Les chemins d’accès fournis à la directive `#load` sont relatifs à l’emplacement de votre fichier `.fsx`.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-181">Paths provides to the `#load` directive are relative to the location of your `.fsx` file.</span></span>

* <span data-ttu-id="cd1f3-182">`#load "logger.fsx"` charge un fichier situé dans le dossier de la fonction.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-182">`#load "logger.fsx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="cd1f3-183">`#load "package\logger.fsx"` charge un fichier situé dans le dossier `package` du dossier de la fonction.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-183">`#load "package\logger.fsx"` loads a file located in the `package` folder in the function folder.</span></span>
* <span data-ttu-id="cd1f3-184">`#load "..\shared\mylogger.fsx"` charge un fichier situé dans le dossier `shared` au même niveau que le dossier de la fonction, c’est-à-dire, directement sous `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-184">`#load "..\shared\mylogger.fsx"` loads a file located in the `shared` folder at the same level as the function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="cd1f3-185">La directive `#load` ne fonctionne qu’avec des fichiers `.fsx` (script F#), et non avec des fichiers `.fs`.</span><span class="sxs-lookup"><span data-stu-id="cd1f3-185">The `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd1f3-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd1f3-186">Next steps</span></span>
<span data-ttu-id="cd1f3-187">Pour plus d’informations, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="cd1f3-187">For more information, see the following resources:</span></span>

* <span data-ttu-id="cd1f3-188">[F# Guide](/dotnet/articles/fsharp/index) (Guide F#)</span><span class="sxs-lookup"><span data-stu-id="cd1f3-188">[F# Guide](/dotnet/articles/fsharp/index)</span></span>
* [<span data-ttu-id="cd1f3-189">Meilleures pratiques pour Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cd1f3-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="cd1f3-190">Référence du développeur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cd1f3-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="cd1f3-191">Informations de référence pour les développeurs C# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cd1f3-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="cd1f3-192">Azure Functions NodeJS developer reference (Référence pour les développeurs NodeJS Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="cd1f3-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="cd1f3-193">Déclencheurs et liaisons Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cd1f3-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="cd1f3-194">Test des fonctions Azure</span><span class="sxs-lookup"><span data-stu-id="cd1f3-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="cd1f3-195">Mise à l’échelle d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cd1f3-195">Azure Functions scaling</span></span>](functions-scale.md)

