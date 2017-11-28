---
title: "référence du développeur fonctions F # d’aaaAzure | Documents Microsoft"
description: "Comprendre comment toodevelop fonctions Azure à l’aide de F #."
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "azure functions, fonctions Azure, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur, F#"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1ac366ba6f73d191c582dcd9214b688ef719617a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="fe385-104">Informations de référence pour les développeurs F# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fe385-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe385-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="fe385-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="fe385-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="fe385-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="fe385-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fe385-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="fe385-108">F # pour les fonctions de Azure est une solution pour exécuter facilement des petits éléments de code, ou « fonctions » dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="fe385-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in hello cloud.</span></span> <span data-ttu-id="fe385-109">Les données circulent dans votre fonction F# par le biais d’arguments de fonction.</span><span class="sxs-lookup"><span data-stu-id="fe385-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="fe385-110">Les noms d’arguments sont spécifiés dans `function.json`, et qu’il existe des noms prédéfinis pour accéder à diverses tâches telles que hello des jetons d’enregistreur d’événements et l’annulation de fonction.</span><span class="sxs-lookup"><span data-stu-id="fe385-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="fe385-111">Cet article suppose que vous avez déjà lu hello [référence du développeur Azure fonctions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="fe385-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="fe385-112">Fonctionnement de .fsx</span><span class="sxs-lookup"><span data-stu-id="fe385-112">How .fsx works</span></span>
<span data-ttu-id="fe385-113">Un fichier `.fsx` est un script F#.</span><span class="sxs-lookup"><span data-stu-id="fe385-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="fe385-114">Il peut être considéré comme un projet F# contenu dans un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="fe385-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="fe385-115">fichier Hello contient à la fois code hello pour votre programme (dans ce cas, votre fonction Azure) et des directives pour la gestion des dépendances.</span><span class="sxs-lookup"><span data-stu-id="fe385-115">hello file contains both hello code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="fe385-116">Lorsque vous utilisez un `.fsx` pour une fonction d’Azure, généralement requis les assemblys sont automatiquement inclus pour vous, ce qui vous toofocus sur le code de fonction au lieu de « standard » hello.</span><span class="sxs-lookup"><span data-stu-id="fe385-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you toofocus on hello function rather than "boilerplate" code.</span></span>

## <a name="binding-tooarguments"></a><span data-ttu-id="fe385-117">Liaison tooarguments</span><span class="sxs-lookup"><span data-stu-id="fe385-117">Binding tooarguments</span></span>
<span data-ttu-id="fe385-118">Chaque liaison prend en charge un ensemble d’arguments, comme détaillé dans hello [référence du développeur Azure fonctions déclencheurs et des liaisons](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="fe385-118">Each binding supports some set of arguments, as detailed in hello [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="fe385-119">Par exemple, une des liaisons d’arguments hello qu'un déclencheur blob prend en charge est POCO, ce qui peut être exprimé à l’aide d’un enregistrement F #.</span><span class="sxs-lookup"><span data-stu-id="fe385-119">For example, one of hello argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="fe385-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="fe385-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="fe385-121">Votre fonction Azure F# utilisera un ou plusieurs arguments.</span><span class="sxs-lookup"><span data-stu-id="fe385-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="fe385-122">Lorsque nous parlons arguments des fonctions d’Azure, nous nous référons trop*d’entrée* arguments et *sortie* arguments.</span><span class="sxs-lookup"><span data-stu-id="fe385-122">When we talk about Azure Functions arguments, we refer too*input* arguments and *output* arguments.</span></span> <span data-ttu-id="fe385-123">Un argument d’entrée est exactement il ressemble : entrée tooyour fonction d’Azure F #.</span><span class="sxs-lookup"><span data-stu-id="fe385-123">An input argument is exactly what it sounds like: input tooyour F# Azure Function.</span></span> <span data-ttu-id="fe385-124">Un *sortie* argument est données mutables ou un `byref<>` argument qui sert d’une manière toopass stockage des données *hors* de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="fe385-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way toopass data back *out* of your function.</span></span>

<span data-ttu-id="fe385-125">Dans l’exemple hello ci-dessus, `blob` est un argument d’entrée, et `output` est un argument de sortie.</span><span class="sxs-lookup"><span data-stu-id="fe385-125">In hello example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="fe385-126">Notez que nous avons utilisé `byref<>` pour `output` (il n’existe aucun hello de tooadd besoin `[<Out>]` annotation).</span><span class="sxs-lookup"><span data-stu-id="fe385-126">Notice that we used `byref<>` for `output` (there's no need tooadd hello `[<Out>]` annotation).</span></span> <span data-ttu-id="fe385-127">À l’aide un `byref<>` type autorise votre toochange fonction quel argument hello enregistrement ou un objet fait référence à.</span><span class="sxs-lookup"><span data-stu-id="fe385-127">Using a `byref<>` type allows your function toochange which record or object hello argument refers to.</span></span>

<span data-ttu-id="fe385-128">Lorsqu’un enregistrement F # est utilisé comme un type d’entrée, la définition d’enregistrement hello doit être marquée avec `[<CLIMutable>]` dans des champs hello correctement avant de passer hello enregistrement tooyour fonction tooallow hello Azure fonctions framework tooset ordre.</span><span class="sxs-lookup"><span data-stu-id="fe385-128">When an F# record is used as an input type, hello record definition must be marked with `[<CLIMutable>]` in order tooallow hello Azure Functions framework tooset hello fields appropriately before passing hello record tooyour function.</span></span> <span data-ttu-id="fe385-129">Dans les coulisses hello, `[<CLIMutable>]` génère des méthodes setter de propriétés de l’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="fe385-129">Under hello hood, `[<CLIMutable>]` generates setters for hello record properties.</span></span> <span data-ttu-id="fe385-130">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="fe385-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="fe385-131">Une classe F# est également utilisable pour les arguments d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="fe385-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="fe385-132">Pour une classe, les propriétés nécessitent généralement des méthodes getter et setter.</span><span class="sxs-lookup"><span data-stu-id="fe385-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="fe385-133">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="fe385-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="fe385-134">Journalisation</span><span class="sxs-lookup"><span data-stu-id="fe385-134">Logging</span></span>
<span data-ttu-id="fe385-135">toolog sortie tooyour [journaux de diffusion en continu](../app-service-web/web-sites-streaming-logs-and-console.md) en F #, votre fonction doit prendre un argument de type `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="fe385-135">toolog output tooyour [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="fe385-136">Par souci de cohérence, nous vous recommandons de nommer cet argument `log`.</span><span class="sxs-lookup"><span data-stu-id="fe385-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="fe385-137">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="fe385-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="fe385-138">Async</span><span class="sxs-lookup"><span data-stu-id="fe385-138">Async</span></span>
<span data-ttu-id="fe385-139">Hello `async` workflow peut être utilisé, mais le résultat de hello doit tooreturn un `Task`.</span><span class="sxs-lookup"><span data-stu-id="fe385-139">hello `async` workflow can be used, but hello result needs tooreturn a `Task`.</span></span> <span data-ttu-id="fe385-140">Pour ce faire, utilisez `Async.StartAsTask`. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="fe385-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="fe385-141">Jeton d’annulation</span><span class="sxs-lookup"><span data-stu-id="fe385-141">Cancellation Token</span></span>
<span data-ttu-id="fe385-142">Si votre fonction doit toohandle arrêt en douceur, vous pouvez lui attribuer un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span><span class="sxs-lookup"><span data-stu-id="fe385-142">If your function needs toohandle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="fe385-143">conjointement utilisable avec `async`. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="fe385-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="fe385-144">Importation des espaces de noms</span><span class="sxs-lookup"><span data-stu-id="fe385-144">Importing namespaces</span></span>
<span data-ttu-id="fe385-145">Espaces de noms peuvent être ouverts dans hello normalement :</span><span class="sxs-lookup"><span data-stu-id="fe385-145">Namespaces can be opened in hello usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="fe385-146">Hello suivant des espaces de noms est automatiquement ouvertes :</span><span class="sxs-lookup"><span data-stu-id="fe385-146">hello following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="fe385-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="fe385-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="fe385-148">Référencement des assemblys externes</span><span class="sxs-lookup"><span data-stu-id="fe385-148">Referencing External Assemblies</span></span>
<span data-ttu-id="fe385-149">De même, l’assembly framework références ajoutées par hello `#r "AssemblyName"` directive.</span><span class="sxs-lookup"><span data-stu-id="fe385-149">Similarly, framework assembly references be added with hello `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="fe385-150">Hello assemblys suivants sont automatiquement ajoutés par les fonctions d’Azure hello environnement d’hébergement :</span><span class="sxs-lookup"><span data-stu-id="fe385-150">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* <span data-ttu-id="fe385-151">`mscorlib`</span><span class="sxs-lookup"><span data-stu-id="fe385-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="fe385-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="fe385-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="fe385-153">En outre, hello suivant des assemblys est spécial casse et peuvent être référencées par simplename (par exemple, `#r "AssemblyName"`) :</span><span class="sxs-lookup"><span data-stu-id="fe385-153">In addition, hello following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="fe385-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="fe385-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="fe385-155">Si vous avez besoin de tooreference un assembly privé, vous pouvez télécharger le fichier d’assembly hello dans un `bin` fonction tooyour relatif de dossier et de la référence à l’aide de hello nom de fichier (par exemple)  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="fe385-155">If you need tooreference a private assembly, you can upload hello assembly file into a `bin` folder relative tooyour function and reference it by using hello file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="fe385-156">Pour plus d’informations sur le fonctionnement des fichiers de dossier de fonction tooyour tooupload, consultez hello suivant la section sur la gestion des packages.</span><span class="sxs-lookup"><span data-stu-id="fe385-156">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="fe385-157">Préambule destiné à l’éditeur</span><span class="sxs-lookup"><span data-stu-id="fe385-157">Editor Prelude</span></span>
<span data-ttu-id="fe385-158">Un éditeur qui prend en charge les Services du compilateur F # ne seront pas prenant en charge des espaces de noms hello et des assemblys qui inclut automatiquement les fonctions de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe385-158">An editor that supports F# Compiler Services will not be aware of hello namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="fe385-159">Par conséquent, il peut être utile tooinclude une étape préliminaire qui permet de rechercher les assemblys hello que vous utilisez l’éditeur de hello et tooexplicitly ouvrir les espaces de noms.</span><span class="sxs-lookup"><span data-stu-id="fe385-159">As such, it can be useful tooinclude a prelude that helps hello editor find hello assemblies you are using, and tooexplicitly open namespaces.</span></span> <span data-ttu-id="fe385-160">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="fe385-160">For example:</span></span>

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

<span data-ttu-id="fe385-161">Lorsque les fonctions Azure s’exécute votre code, il traite source hello avec `COMPILED` défini prélude d’éditeur hello sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="fe385-161">When Azure Functions executes your code, it processes hello source with `COMPILED` defined, so hello editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="fe385-162">Gestion des packages</span><span class="sxs-lookup"><span data-stu-id="fe385-162">Package management</span></span>
<span data-ttu-id="fe385-163">les packages NuGet toouse dans une fonction) (F #, ajoutez un `project.json` dossier de la fonction toohello hello du fichier dans le système de fichiers de l’application hello (fonction).</span><span class="sxs-lookup"><span data-stu-id="fe385-163">toouse NuGet packages in an F# function, add a `project.json` file toohello hello function's folder in hello function app's file system.</span></span> <span data-ttu-id="fe385-164">Voici un exemple `project.json` fichier qui ajoute une référence de package NuGet trop`Microsoft.ProjectOxford.Face` version 1.1.0. :</span><span class="sxs-lookup"><span data-stu-id="fe385-164">Here is an example `project.json` file that adds a NuGet package reference too`Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="fe385-165">Hello .NET Framework 4.6 est prise en charge uniquement, donc vous assurer que votre `project.json` fichier spécifie `net46` comme indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="fe385-165">Only hello .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="fe385-166">Lorsque vous téléchargez un `project.json` fichier, hello runtime Obtient les packages de hello et ajoute automatiquement les assemblys de package toohello de références.</span><span class="sxs-lookup"><span data-stu-id="fe385-166">When you upload a `project.json` file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="fe385-167">Vous n’avez pas besoin de tooadd `#r "AssemblyName"` directives.</span><span class="sxs-lookup"><span data-stu-id="fe385-167">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="fe385-168">Ajoutez simplement hello requis `open` instructions tooyour `.fsx` fichier.</span><span class="sxs-lookup"><span data-stu-id="fe385-168">Just add hello required `open` statements tooyour `.fsx` file.</span></span>

<span data-ttu-id="fe385-169">Vous souhaiterez peut-être tooput référence automatiquement les assemblys dans votre prélude éditeur, tooimprove interaction de votre éditeur avec les Services de compilation F #.</span><span class="sxs-lookup"><span data-stu-id="fe385-169">You may wish tooput automatically references assemblies in your editor prelude, tooimprove your editor's interaction with F# Compile Services.</span></span>

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a><span data-ttu-id="fe385-170">Comment tooadd un `project.json` fichier tooyour Azure (fonction)</span><span class="sxs-lookup"><span data-stu-id="fe385-170">How tooadd a `project.json` file tooyour Azure Function</span></span>
1. <span data-ttu-id="fe385-171">BEGIN en vous assurant que votre application de la fonction est en cours d’exécution, ce que vous pouvez faire en ouvrant votre fonction Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fe385-171">Begin by making sure your function app is running, which you can do by opening your function in hello Azure portal.</span></span> <span data-ttu-id="fe385-172">Cela donne également accès des journaux de diffusion en continu toohello où la sortie d’installation de package s’affichera.</span><span class="sxs-lookup"><span data-stu-id="fe385-172">This also gives access toohello streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="fe385-173">tooupload un `project.json` de fichiers, utilisez une des méthodes hello décrites dans [fonctionnement des fichiers de l’application tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="fe385-173">tooupload a `project.json` file, use one of hello methods described in [how tooupdate function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="fe385-174">Si vous utilisez [déploiement continu pour les fonctions Azure](functions-continuous-deployment.md), vous pouvez ajouter un `project.json` tooyour branche dans tooexperiment d’ordre avec celui-ci avant de l’ajouter branche de déploiement tooyour de mise en lots de fichiers.</span><span class="sxs-lookup"><span data-stu-id="fe385-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file tooyour staging branch in order tooexperiment with it before adding it tooyour deployment branch.</span></span>
3. <span data-ttu-id="fe385-175">Après avoir hello `project.json` fichier est ajouté, vous verrez toohello similaire de sortie dans votre fonction de l’exemple suivant de diffusion en continu de journal :</span><span class="sxs-lookup"><span data-stu-id="fe385-175">After hello `project.json` file is added, you will see output similar toohello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="fe385-176">Variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="fe385-176">Environment variables</span></span>
<span data-ttu-id="fe385-177">tooget une variable d’environnement ou une valeur de paramètre d’application, utilisez `System.Environment.GetEnvironmentVariable`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="fe385-177">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="fe385-178">Réutilisation du code .fsx</span><span class="sxs-lookup"><span data-stu-id="fe385-178">Reusing .fsx code</span></span>
<span data-ttu-id="fe385-179">Vous pouvez utiliser le code d’autres fichiers `.fsx` au moyen d’une directive `#load`.</span><span class="sxs-lookup"><span data-stu-id="fe385-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="fe385-180">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="fe385-180">For example:</span></span>

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

<span data-ttu-id="fe385-181">Fournit des chemins d’accès toohello `#load` directive sont emplacement relatif toohello de votre `.fsx` fichier.</span><span class="sxs-lookup"><span data-stu-id="fe385-181">Paths provides toohello `#load` directive are relative toohello location of your `.fsx` file.</span></span>

* <span data-ttu-id="fe385-182">`#load "logger.fsx"`charge un fichier situé dans le dossier de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="fe385-182">`#load "logger.fsx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="fe385-183">`#load "package\logger.fsx"`charge un fichier situé dans hello `package` hello fonction dossier.</span><span class="sxs-lookup"><span data-stu-id="fe385-183">`#load "package\logger.fsx"` loads a file located in hello `package` folder in hello function folder.</span></span>
* <span data-ttu-id="fe385-184">`#load "..\shared\mylogger.fsx"`charge un fichier situé dans hello `shared` dossier hello même niveau en tant que dossier de fonction hello, autrement dit, directement sous `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="fe385-184">`#load "..\shared\mylogger.fsx"` loads a file located in hello `shared` folder at hello same level as hello function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="fe385-185">Hello `#load` directive ne fonctionne qu’avec `.fsx` les fichiers (script) (F #) et non avec `.fs` fichiers.</span><span class="sxs-lookup"><span data-stu-id="fe385-185">hello `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe385-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fe385-186">Next steps</span></span>
<span data-ttu-id="fe385-187">Pour plus d’informations, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="fe385-187">For more information, see hello following resources:</span></span>

* <span data-ttu-id="fe385-188">[F# Guide](/dotnet/articles/fsharp/index) (Guide F#)</span><span class="sxs-lookup"><span data-stu-id="fe385-188">[F# Guide](/dotnet/articles/fsharp/index)</span></span>
* [<span data-ttu-id="fe385-189">Meilleures pratiques pour Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fe385-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="fe385-190">Référence du développeur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fe385-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="fe385-191">Informations de référence pour les développeurs C# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fe385-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="fe385-192">Azure Functions NodeJS developer reference (Référence pour les développeurs NodeJS Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="fe385-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="fe385-193">Déclencheurs et liaisons Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fe385-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="fe385-194">Test des fonctions Azure</span><span class="sxs-lookup"><span data-stu-id="fe385-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="fe385-195">Mise à l’échelle d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fe385-195">Azure Functions scaling</span></span>](functions-scale.md)

