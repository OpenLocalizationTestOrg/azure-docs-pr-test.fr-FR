---
title: "aaaAzure référence du développeur fonctions C# Script | Documents Microsoft"
description: "Comprendre comment toodevelop fonctions Azure à l’aide de c#."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="11231-104">Informations de référence pour les développeurs de scripts C# Azure Functions</span><span class="sxs-lookup"><span data-stu-id="11231-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11231-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="11231-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="11231-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="11231-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="11231-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="11231-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="11231-108">Hello expérience de script c# pour les fonctions de Azure est basé sur hello Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="11231-108">hello C# script experience for Azure Functions is based on hello Azure WebJobs SDK.</span></span> <span data-ttu-id="11231-109">Les données circulent dans votre fonction C# via des arguments de méthode.</span><span class="sxs-lookup"><span data-stu-id="11231-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="11231-110">Les noms d’arguments sont spécifiés dans `function.json`, et qu’il existe des noms prédéfinis pour accéder à diverses tâches telles que hello des jetons d’enregistreur d’événements et l’annulation de fonction.</span><span class="sxs-lookup"><span data-stu-id="11231-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="11231-111">Cet article suppose que vous avez déjà lu hello [référence du développeur Azure fonctions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="11231-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="11231-112">Pour plus d’informations sur l’utilisation des bibliothèques de classes C#, consultez la page [Utiliser des bibliothèques de classes .NET avec Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="11231-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="11231-113">Fonctionnement de .csx</span><span class="sxs-lookup"><span data-stu-id="11231-113">How .csx works</span></span>
<span data-ttu-id="11231-114">Hello `.csx` format vous permet de toowrite moins de « standard » et le focus sur l’écriture de simplement une fonction c#.</span><span class="sxs-lookup"><span data-stu-id="11231-114">hello `.csx` format allows you toowrite less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="11231-115">Inclure les références d’assembly et les espaces de noms au début de hello du fichier de hello comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="11231-115">Include any assembly references and namespaces at hello beginning of hello file as usual.</span></span> <span data-ttu-id="11231-116">Au lieu de tout encapsuler dans un espace de noms et une classe, définissez simplement une méthode `Run`.</span><span class="sxs-lookup"><span data-stu-id="11231-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="11231-117">Si vous avez besoin de tooinclude toutes les classes, de l’instance toodefine brut est ancien objet CLR (POCO) des objets, vous pouvez inclure une classe à l’intérieur de hello même fichier.</span><span class="sxs-lookup"><span data-stu-id="11231-117">If you need tooinclude any classes, for instance toodefine Plain Old CLR Object (POCO) objects, you can include a class inside hello same file.</span></span>   

## <a name="binding-tooarguments"></a><span data-ttu-id="11231-118">Liaison tooarguments</span><span class="sxs-lookup"><span data-stu-id="11231-118">Binding tooarguments</span></span>
<span data-ttu-id="11231-119">fonction liée tooa c# via hello sont Hello diverses liaisons `name` propriété Bonjour *function.json* configuration.</span><span class="sxs-lookup"><span data-stu-id="11231-119">hello various bindings are bound tooa C# function via hello `name` property in hello *function.json* configuration.</span></span> <span data-ttu-id="11231-120">Chaque liaison prend en charge ses propres types ; par exemple, un déclencheur d’objets blob peut prendre en charge une chaîne, un OCT ou un CloudBlockBlob.</span><span class="sxs-lookup"><span data-stu-id="11231-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="11231-121">les types Hello pris en charge sont documentées dans la référence hello pour chaque liaison.</span><span class="sxs-lookup"><span data-stu-id="11231-121">hello supported types are documented in hello reference for each binding.</span></span> <span data-ttu-id="11231-122">Des méthodes getter et setter doivent être définies pour chaque propriété d’un objet OCT.</span><span class="sxs-lookup"><span data-stu-id="11231-122">A POCO object must have a getter and setter defined for each property.</span></span>

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="11231-123">Utiliser la valeur renvoyée par la méthode pour la liaison de sortie</span><span class="sxs-lookup"><span data-stu-id="11231-123">Using method return value for output binding</span></span>

<span data-ttu-id="11231-124">Vous pouvez utiliser une valeur de retour de méthode pour une liaison de sortie, à l’aide du nom de hello `$return` dans *function.json*:</span><span class="sxs-lookup"><span data-stu-id="11231-124">You can use a method return value for an output binding, by using hello name `$return` in *function.json*:</span></span>

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a><span data-ttu-id="11231-125">Écrire plusieurs valeurs de sortie</span><span class="sxs-lookup"><span data-stu-id="11231-125">Writing multiple output values</span></span>

<span data-ttu-id="11231-126">liaison de sortie de plusieurs valeurs tooan toowrite, utilisez hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span><span class="sxs-lookup"><span data-stu-id="11231-126">toowrite multiple values tooan output binding, use hello [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="11231-127">Ces types sont en écriture seule des collections qui sont écrite toohello liaison de sortie issue de la méthode hello.</span><span class="sxs-lookup"><span data-stu-id="11231-127">These types are write-only collections that are written toohello output binding when hello method completes.</span></span>

<span data-ttu-id="11231-128">Cet exemple écrit plusieurs messages de file d’attente à l’aide de `ICollector` :</span><span class="sxs-lookup"><span data-stu-id="11231-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="11231-129">Journalisation</span><span class="sxs-lookup"><span data-stu-id="11231-129">Logging</span></span>
<span data-ttu-id="11231-130">toolog sortie des journaux de diffusion en continu tooyour en c#, incluent un argument de type `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="11231-130">toolog output tooyour streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="11231-131">Nous vous recommandons de le nommer `log`.</span><span class="sxs-lookup"><span data-stu-id="11231-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="11231-132">Évitez d’utiliser `Console.Write` dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="11231-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="11231-133">`TraceWriter`est défini dans hello [Kit de développement logiciel Azure WebJobs](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="11231-133">`TraceWriter` is defined in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="11231-134">Hello du niveau de journalisation de `TraceWriter` peuvent être configurés dans [hôte\.json].</span><span class="sxs-lookup"><span data-stu-id="11231-134">hello log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="11231-135">Async</span><span class="sxs-lookup"><span data-stu-id="11231-135">Async</span></span>
<span data-ttu-id="11231-136">toomake une fonction asynchrone, utilisez hello `async` (mot clé) et retournent un `Task` objet.</span><span class="sxs-lookup"><span data-stu-id="11231-136">toomake a function asynchronous, use hello `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="11231-137">Jeton d’annulation</span><span class="sxs-lookup"><span data-stu-id="11231-137">Cancellation Token</span></span>
<span data-ttu-id="11231-138">Certaines opérations requièrent un arrêt approprié.</span><span class="sxs-lookup"><span data-stu-id="11231-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="11231-139">Bien qu’il soit toujours meilleure code toowrite qui peut gérer en panne, dans les cas où vous souhaitez que les demandes de l’arrêt correct de toohandle, vous définissez un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument de type.</span><span class="sxs-lookup"><span data-stu-id="11231-139">While it's always best toowrite code that can handle crashing,  in cases where you want toohandle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="11231-140">A `CancellationToken` est fourni toosignal qu’un arrêt de l’hôte est déclenché.</span><span class="sxs-lookup"><span data-stu-id="11231-140">A `CancellationToken` is provided toosignal that a host shutdown is triggered.</span></span>

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a><span data-ttu-id="11231-141">Importation des espaces de noms</span><span class="sxs-lookup"><span data-stu-id="11231-141">Importing namespaces</span></span>
<span data-ttu-id="11231-142">Si vous avez besoin d’espaces de noms tooimport, vous pouvez le faire comme d’habitude, avec hello `using` clause.</span><span class="sxs-lookup"><span data-stu-id="11231-142">If you need tooimport namespaces, you can do so as usual, with hello `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="11231-143">Hello espaces de noms suivants sont automatiquement importés et sont par conséquent facultatifs :</span><span class="sxs-lookup"><span data-stu-id="11231-143">hello following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="11231-144">Référencement des assemblys externes</span><span class="sxs-lookup"><span data-stu-id="11231-144">Referencing External Assemblies</span></span>
<span data-ttu-id="11231-145">Pour les assemblys d’infrastructure, ajoutez des références à l’aide de hello `#r "AssemblyName"` directive.</span><span class="sxs-lookup"><span data-stu-id="11231-145">For framework assemblies, add references by using hello `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="11231-146">Hello assemblys suivants sont automatiquement ajoutés par les fonctions d’Azure hello environnement d’hébergement :</span><span class="sxs-lookup"><span data-stu-id="11231-146">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

<span data-ttu-id="11231-147">Hello assemblys suivants peuvent être référencées par le nom simple (par exemple, `#r "AssemblyName"`) :</span><span class="sxs-lookup"><span data-stu-id="11231-147">hello following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="11231-148">Référencer des assemblys personnalisés</span><span class="sxs-lookup"><span data-stu-id="11231-148">Referencing custom assemblies</span></span>

<span data-ttu-id="11231-149">tooreference un assembly personnalisé, vous pouvez utiliser un *partagé* assembly ou un *privé* assembly :</span><span class="sxs-lookup"><span data-stu-id="11231-149">tooreference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="11231-150">Les assemblys partagés sont communs à toutes les fonctions d’une application de fonction.</span><span class="sxs-lookup"><span data-stu-id="11231-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="11231-151">tooreference un assembly personnalisé, télécharger l’application de fonction hello assembly tooyour, comme dans un `bin` dossier racine d’application hello (fonction).</span><span class="sxs-lookup"><span data-stu-id="11231-151">tooreference a custom assembly, upload hello assembly tooyour function app, such as in a `bin` folder in hello function app root.</span></span> 
- <span data-ttu-id="11231-152">Les assemblys privés font partie du contexte d’une fonction donnée et sont compatibles avec le chargement indépendant de versions différentes.</span><span class="sxs-lookup"><span data-stu-id="11231-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="11231-153">Les assemblys privés doivent être téléchargées dans un `bin` dossier du répertoire de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="11231-153">Private assemblies should be uploaded in a `bin` folder in hello function directory.</span></span> <span data-ttu-id="11231-154">Référence à l’aide de nom de fichier hello, tel que `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="11231-154">Reference using hello file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="11231-155">Pour plus d’informations sur le fonctionnement des fichiers de dossier de fonction tooyour tooupload, consultez hello suivant la section sur la gestion des packages.</span><span class="sxs-lookup"><span data-stu-id="11231-155">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="11231-156">Répertoires surveillés</span><span class="sxs-lookup"><span data-stu-id="11231-156">Watched directories</span></span>

<span data-ttu-id="11231-157">Hello répertoire qui contient le fichier de script de fonction hello est automatiquement surveillé pour tooassemblies de modifications.</span><span class="sxs-lookup"><span data-stu-id="11231-157">hello directory that contains hello function script file is automatically watched for changes tooassemblies.</span></span> <span data-ttu-id="11231-158">toowatch modifier des assemblys dans d’autres répertoires, ajoutez-les toohello `watchDirectories` liste [hôte\.json].</span><span class="sxs-lookup"><span data-stu-id="11231-158">toowatch for assembly changes in other directories, add them toohello `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="11231-159">Utiliser des packages NuGet</span><span class="sxs-lookup"><span data-stu-id="11231-159">Using NuGet packages</span></span>
<span data-ttu-id="11231-160">les packages NuGet toouse dans une fonction c#, téléchargez un *project.json* dossier de la fonction toohello du fichier dans le système de fichiers de l’application hello (fonction).</span><span class="sxs-lookup"><span data-stu-id="11231-160">toouse NuGet packages in a C# function, upload a *project.json* file toohello function's folder in hello function app's file system.</span></span> <span data-ttu-id="11231-161">Voici un exemple *project.json* fichier qui ajoute une référence tooMicrosoft.ProjectOxford.Face version 1.1.0 :</span><span class="sxs-lookup"><span data-stu-id="11231-161">Here is an example *project.json* file that adds a reference tooMicrosoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="11231-162">Hello .NET Framework 4.6 est prise en charge uniquement, donc vous assurer que votre *project.json* fichier spécifie `net46` comme indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="11231-162">Only hello .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="11231-163">Lorsque vous téléchargez un *project.json* de fichiers, obtient les packages de hello hello runtime et ajoute automatiquement les assemblys de package toohello de références.</span><span class="sxs-lookup"><span data-stu-id="11231-163">When you upload a *project.json* file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="11231-164">Vous n’avez pas besoin de tooadd `#r "AssemblyName"` directives.</span><span class="sxs-lookup"><span data-stu-id="11231-164">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="11231-165">les types de hello toouse définis dans les packages NuGet hello, ajouter hello requis `using` instructions tooyour *run.csx* fichier</span><span class="sxs-lookup"><span data-stu-id="11231-165">toouse hello types defined in hello NuGet packages, add hello required `using` statements tooyour *run.csx* file</span></span> 

<span data-ttu-id="11231-166">Lors de l’exécution de fonctions hello NuGet restauration fonctionne en comparant `project.json` et `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="11231-166">In hello Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="11231-167">Si hello cachets de date et heure des fichiers de hello **pas** exécute de correspondance, une restauration de NuGet et des téléchargements de NuGet mis à jour les packages.</span><span class="sxs-lookup"><span data-stu-id="11231-167">If hello date and time stamps of hello files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="11231-168">Toutefois, si hello cachets de date et heure des fichiers de hello **faire** correspondance, NuGet n’effectue pas une restauration.</span><span class="sxs-lookup"><span data-stu-id="11231-168">However, if hello date and time stamps of hello files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="11231-169">Par conséquent, `project.lock.json` ne doit pas être déployé car il entraîne la restauration des packages NuGet tooskip.</span><span class="sxs-lookup"><span data-stu-id="11231-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet tooskip package restore.</span></span> <span data-ttu-id="11231-170">tooavoid déploiement verrou de hello, ajoutez hello `project.lock.json` toohello `.gitignore` fichier.</span><span class="sxs-lookup"><span data-stu-id="11231-170">tooavoid deploying hello lock file, add hello `project.lock.json` toohello `.gitignore` file.</span></span>

<span data-ttu-id="11231-171">toouse un flux NuGet personnalisé, spécifiez hello de flux dans un *Nuget.Config* fichier racine d’application de la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="11231-171">toouse a custom NuGet feed, specify hello feed in a *Nuget.Config* file in hello Function App root.</span></span> <span data-ttu-id="11231-172">Pour plus d’informations, consultez la page [Configurer le comportement de NuGet](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="11231-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="11231-173">Utiliser un fichier project.json</span><span class="sxs-lookup"><span data-stu-id="11231-173">Using a project.json file</span></span>
1. <span data-ttu-id="11231-174">Ouvrez la fonction hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="11231-174">Open hello function in hello Azure portal.</span></span> <span data-ttu-id="11231-175">Hello ouvre l’onglet affiche hello package installation la sortie.</span><span class="sxs-lookup"><span data-stu-id="11231-175">hello logs tab displays hello package installation output.</span></span>
2. <span data-ttu-id="11231-176">tooupload un fichier project.json, utilisez une des méthodes de hello décrites dans hello [fonctionnement des fichiers de l’application tooupdate](functions-reference.md#fileupdate) dans la rubrique de référence du développeur hello fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="11231-176">tooupload a project.json file, use one of hello methods described in hello [How tooupdate function app files](functions-reference.md#fileupdate) in hello Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="11231-177">Après avoir hello *project.json* fichier est téléchargé, vous voyez la sortie comme hello dans votre fonction de l’exemple suivant de diffusion en continu de journal :</span><span class="sxs-lookup"><span data-stu-id="11231-177">After hello *project.json* file is uploaded, you see output like hello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="11231-178">Variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="11231-178">Environment variables</span></span>
<span data-ttu-id="11231-179">tooget une variable d’environnement ou une valeur de paramètre d’application, utilisez `System.Environment.GetEnvironmentVariable`, comme indiqué dans l’exemple de code suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="11231-179">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in hello following code example:</span></span>

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
    log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}

public static string GetEnvironmentVariable(string name)
{
    return name + ": " +
        System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```

## <a name="reusing-csx-code"></a><span data-ttu-id="11231-180">Réutilisation du code .csx</span><span class="sxs-lookup"><span data-stu-id="11231-180">Reusing .csx code</span></span>
<span data-ttu-id="11231-181">Vous pouvez utiliser des classes et des méthodes définies dans d’autres fichiers *.csx* au sein de votre fichier *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="11231-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="11231-182">toodo, qui utilisent `#load` directives dans votre *run.csx* fichier.</span><span class="sxs-lookup"><span data-stu-id="11231-182">toodo that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="11231-183">Bonjour l’exemple suivant, une routine de journalisation nommé `MyLogger` est partagé dans *myLogger.csx* et chargés en *run.csx* à l’aide de hello `#load` directive :</span><span class="sxs-lookup"><span data-stu-id="11231-183">In hello following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using hello `#load` directive:</span></span>

<span data-ttu-id="11231-184">Exemple *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="11231-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="11231-185">Exemple *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="11231-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="11231-186">À l’aide d’un élément partagé *.csx* est courant lorsque vous souhaitez toostrongly tapez vos arguments entre les fonctions à l’aide d’un objet POCO.</span><span class="sxs-lookup"><span data-stu-id="11231-186">Using a shared *.csx* is a common pattern when you want toostrongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="11231-187">Bonjour simplifiée de l’exemple suivant, un déclencheur HTTP et le déclencheur de la file d’attente partagent un objet POCO nommé `Order` toostrongly les données de commande type hello :</span><span class="sxs-lookup"><span data-stu-id="11231-187">In hello following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` toostrongly type hello order data:</span></span>

<span data-ttu-id="11231-188">Exemple avec *run.csx* pour un déclencheur HTTP :</span><span class="sxs-lookup"><span data-stu-id="11231-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

<span data-ttu-id="11231-189">Exemple avec *run.csx* pour un déclencheur de file d’attente :</span><span class="sxs-lookup"><span data-stu-id="11231-189">Example *run.csx* for queue trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

<span data-ttu-id="11231-190">Exemple avec *order.csx* :</span><span class="sxs-lookup"><span data-stu-id="11231-190">Example *order.csx*:</span></span>

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

<span data-ttu-id="11231-191">Vous pouvez utiliser un chemin d’accès relatif par hello `#load` directive :</span><span class="sxs-lookup"><span data-stu-id="11231-191">You can use a relative path with hello `#load` directive:</span></span>

* <span data-ttu-id="11231-192">`#load "mylogger.csx"`charge un fichier situé dans le dossier de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="11231-192">`#load "mylogger.csx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="11231-193">`#load "loadedfiles\mylogger.csx"`charge un fichier situé dans un dossier de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="11231-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in hello function folder.</span></span>
* <span data-ttu-id="11231-194">`#load "..\shared\mylogger.csx"`charge un fichier situé dans un dossier à hello même niveau en tant que dossier de fonction hello, autrement dit, directement sous *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="11231-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at hello same level as hello function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="11231-195">Hello `#load` directive fonctionne uniquement avec *.csx* les fichiers (C# script), pas avec *.cs* fichiers.</span><span class="sxs-lookup"><span data-stu-id="11231-195">hello `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="11231-196">Liaison à l’exécution au moyen des liaisons impératives</span><span class="sxs-lookup"><span data-stu-id="11231-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="11231-197">En c# et d’autres langages .NET, vous pouvez utiliser un [impératif](https://en.wikipedia.org/wiki/Imperative_programming) modèle de liaison, en opposition toohello [ *déclarative* ](https://en.wikipedia.org/wiki/Declarative_programming) liaisons dans *function.json*.</span><span class="sxs-lookup"><span data-stu-id="11231-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed toohello [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="11231-198">Liaison impératif est utile lorsque les paramètres de liaison doivent toobe calculée au moment de l’exécution au lieu de conception.</span><span class="sxs-lookup"><span data-stu-id="11231-198">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="11231-199">Avec ce modèle, vous pouvez lier toosupported entrée et sortie de liaison à la volée dans votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="11231-199">With this pattern, you can bind toosupported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="11231-200">Définissez une liaison impérative comme suit :</span><span class="sxs-lookup"><span data-stu-id="11231-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="11231-201">**N’incluez pas** d’entrée dans *function.json* pour les liaisons impératives souhaitées.</span><span class="sxs-lookup"><span data-stu-id="11231-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="11231-202">Transmettez un paramètre d’entrée [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) ou [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="11231-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="11231-203">Utilisez hello suivant c# modèle tooperform hello liaison de données.</span><span class="sxs-lookup"><span data-stu-id="11231-203">Use hello following C# pattern tooperform hello data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="11231-204">où `BindingTypeAttribute` est l’attribut .NET hello qui définit votre liaison et `T` est hello type d’entrée ou de sortie qui est pris en charge par ce type de liaison.</span><span class="sxs-lookup"><span data-stu-id="11231-204">where `BindingTypeAttribute` is hello .NET attribute that defines your binding and `T` is hello input or output type that's supported by that binding type.</span></span> <span data-ttu-id="11231-205">`T` ne peut pas être un type de paramètre `out` (comme `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="11231-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="11231-206">Par exemple, la liaison de sortie de la table Mobile Apps prend en charge [six types de sortie](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), mais vous pouvez utiliser uniquement [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) pour `T`.</span><span class="sxs-lookup"><span data-stu-id="11231-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="11231-207">Hello suivant l’exemple de code crée un [liaison de sortie blob de stockage](functions-bindings-storage-blob.md#using-a-blob-output-binding) avec l’objet blob de chemin d’accès qui est définie au moment de l’exécution, puis écrit un chaîne toohello blob.</span><span class="sxs-lookup"><span data-stu-id="11231-207">hello following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string toohello blob.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

<span data-ttu-id="11231-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) définit hello [objet blob de stockage](functions-bindings-storage-blob.md) d’entrée ou sortie de la liaison, et [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) est un type de liaison de sortie pris en charge.</span><span class="sxs-lookup"><span data-stu-id="11231-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines hello [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="11231-209">En l’état, code de hello Obtient le paramètre d’application par défaut hello pour hello chaîne de connexion de compte de stockage (c'est-à-dire `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="11231-209">As is, hello code gets hello default app setting for hello Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="11231-210">Vous pouvez spécifier un toouse de paramètre d’application personnalisé en ajoutant le [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) et en passant le tableau d’attributs hello dans `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="11231-210">You can specify a custom app setting toouse by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing hello attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="11231-211">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="11231-211">For example,</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

<span data-ttu-id="11231-212">Hello tableau suivant répertorie les attributs .NET hello pour chaque liaison type et hello les packages dans lequel ils sont définis.</span><span class="sxs-lookup"><span data-stu-id="11231-212">hello following table lists hello .NET attributes for each binding type and hello packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="11231-213">Liaison</span><span class="sxs-lookup"><span data-stu-id="11231-213">Binding</span></span> | <span data-ttu-id="11231-214">Attribut</span><span class="sxs-lookup"><span data-stu-id="11231-214">Attribute</span></span> | <span data-ttu-id="11231-215">Ajouter la référence</span><span class="sxs-lookup"><span data-stu-id="11231-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="11231-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="11231-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="11231-217">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="11231-217">Event Hubs</span></span> | <span data-ttu-id="11231-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="11231-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="11231-219">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="11231-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="11231-220">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="11231-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="11231-221">Service Bus</span><span class="sxs-lookup"><span data-stu-id="11231-221">Service Bus</span></span> | <span data-ttu-id="11231-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="11231-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="11231-223">File d’attente de stockage</span><span class="sxs-lookup"><span data-stu-id="11231-223">Storage queue</span></span> | <span data-ttu-id="11231-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="11231-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="11231-225">Objet blob de stockage</span><span class="sxs-lookup"><span data-stu-id="11231-225">Storage blob</span></span> | <span data-ttu-id="11231-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="11231-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="11231-227">Table de stockage</span><span class="sxs-lookup"><span data-stu-id="11231-227">Storage table</span></span> | <span data-ttu-id="11231-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="11231-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="11231-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="11231-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="11231-230">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="11231-230">Next steps</span></span>
<span data-ttu-id="11231-231">Pour plus d’informations, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="11231-231">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="11231-232">Meilleures pratiques pour Azure Functions</span><span class="sxs-lookup"><span data-stu-id="11231-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="11231-233">Référence du développeur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="11231-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="11231-234">Informations de référence pour les développeurs F# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="11231-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="11231-235">Azure Functions NodeJS developer reference (Référence pour les développeurs NodeJS Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="11231-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="11231-236">Azure Functions triggers and bindings (Déclencheurs et liaisons Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="11231-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
