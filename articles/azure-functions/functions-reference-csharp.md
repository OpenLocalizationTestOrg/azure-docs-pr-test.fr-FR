---
title: "Information de référence pour les développeurs de scripts C# Azure Functions | Microsoft Docs"
description: "Découvrez comment développer sur Azure Functions à l’aide de C#."
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
ms.openlocfilehash: 83a351ce0279ada8ce7fe0513497349471334a86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="72384-104">Informations de référence pour les développeurs de scripts C# Azure Functions</span><span class="sxs-lookup"><span data-stu-id="72384-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72384-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="72384-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="72384-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="72384-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="72384-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="72384-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="72384-108">L’expérience de scripts C# pour Azure Functions repose sur le Kit de développement logiciel (SDK) Azure WebJobs.</span><span class="sxs-lookup"><span data-stu-id="72384-108">The C# script experience for Azure Functions is based on the Azure WebJobs SDK.</span></span> <span data-ttu-id="72384-109">Les données circulent dans votre fonction C# via des arguments de méthode.</span><span class="sxs-lookup"><span data-stu-id="72384-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="72384-110">Les noms d’argument sont spécifiés dans `function.json`, et il existe des noms prédéfinis pour accéder à des éléments tels que l’enregistreur de fonctions et les jetons d’annulation.</span><span class="sxs-lookup"><span data-stu-id="72384-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="72384-111">Cet article suppose que vous ayez déjà lu l’article [Informations de référence pour les développeurs sur Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="72384-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="72384-112">Pour plus d’informations sur l’utilisation des bibliothèques de classes C#, consultez la page [Utiliser des bibliothèques de classes .NET avec Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="72384-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="72384-113">Fonctionnement de .csx</span><span class="sxs-lookup"><span data-stu-id="72384-113">How .csx works</span></span>
<span data-ttu-id="72384-114">Le format `.csx` vous permet d’écrire de façon moins « réutilisable » et de vous concentrer uniquement sur l’écriture d’une fonction C#.</span><span class="sxs-lookup"><span data-stu-id="72384-114">The `.csx` format allows you to write less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="72384-115">Ajoutez les éventuels références d’assemblys et espaces de noms au début du fichier, comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="72384-115">Include any assembly references and namespaces at the beginning of the file as usual.</span></span> <span data-ttu-id="72384-116">Au lieu de tout encapsuler dans un espace de noms et une classe, définissez simplement une méthode `Run`.</span><span class="sxs-lookup"><span data-stu-id="72384-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="72384-117">Si vous devez inclure toutes les classes, par exemple pour définir des objets OCT (objets CLR traditionnels), vous pouvez inclure une classe dans le même fichier.</span><span class="sxs-lookup"><span data-stu-id="72384-117">If you need to include any classes, for instance to define Plain Old CLR Object (POCO) objects, you can include a class inside the same file.</span></span>   

## <a name="binding-to-arguments"></a><span data-ttu-id="72384-118">Liaison aux arguments</span><span class="sxs-lookup"><span data-stu-id="72384-118">Binding to arguments</span></span>
<span data-ttu-id="72384-119">Les diverses liaisons sont liées à une fonction C# par le biais de la propriété `name` de la configuration *function.json*.</span><span class="sxs-lookup"><span data-stu-id="72384-119">The various bindings are bound to a C# function via the `name` property in the *function.json* configuration.</span></span> <span data-ttu-id="72384-120">Chaque liaison prend en charge ses propres types ; par exemple, un déclencheur d’objets blob peut prendre en charge une chaîne, un OCT ou un CloudBlockBlob.</span><span class="sxs-lookup"><span data-stu-id="72384-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="72384-121">Les types pris en charge sont documentées dans la référence de chaque liaison.</span><span class="sxs-lookup"><span data-stu-id="72384-121">The supported types are documented in the reference for each binding.</span></span> <span data-ttu-id="72384-122">Des méthodes getter et setter doivent être définies pour chaque propriété d’un objet OCT.</span><span class="sxs-lookup"><span data-stu-id="72384-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="72384-123">Utiliser la valeur renvoyée par la méthode pour la liaison de sortie</span><span class="sxs-lookup"><span data-stu-id="72384-123">Using method return value for output binding</span></span>

<span data-ttu-id="72384-124">Vous pouvez utiliser une valeur renvoyée par la méthode pour une liaison de sortie, en utilisant le nom `$return` dans *function.json* :</span><span class="sxs-lookup"><span data-stu-id="72384-124">You can use a method return value for an output binding, by using the name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="72384-125">Écrire plusieurs valeurs de sortie</span><span class="sxs-lookup"><span data-stu-id="72384-125">Writing multiple output values</span></span>

<span data-ttu-id="72384-126">Pour écrire plusieurs valeurs dans une liaison de sortie, utilisez le type [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou le type [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs).</span><span class="sxs-lookup"><span data-stu-id="72384-126">To write multiple values to an output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="72384-127">Ces types sont des collections en écriture seule, écrites dans la liaison de sortie à la fin de la méthode.</span><span class="sxs-lookup"><span data-stu-id="72384-127">These types are write-only collections that are written to the output binding when the method completes.</span></span>

<span data-ttu-id="72384-128">Cet exemple écrit plusieurs messages de file d’attente à l’aide de `ICollector` :</span><span class="sxs-lookup"><span data-stu-id="72384-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="72384-129">Journalisation</span><span class="sxs-lookup"><span data-stu-id="72384-129">Logging</span></span>
<span data-ttu-id="72384-130">Pour consigner la sortie dans vos journaux de diffusion en continu en C#, ajoutez un argument de type `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="72384-130">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="72384-131">Nous vous recommandons de le nommer `log`.</span><span class="sxs-lookup"><span data-stu-id="72384-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="72384-132">Évitez d’utiliser `Console.Write` dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="72384-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="72384-133">`TraceWriter` est défini dans le [Kit de développement logiciel (SDK) Azure WebJobs](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="72384-133">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="72384-134">Le niveau de journalisation de `TraceWriter` est configurable dans [host\.json].</span><span class="sxs-lookup"><span data-stu-id="72384-134">The log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="72384-135">Async</span><span class="sxs-lookup"><span data-stu-id="72384-135">Async</span></span>
<span data-ttu-id="72384-136">Pour rendre une fonction asynchrone, utilisez le mot clé `async` et retournez un objet `Task`.</span><span class="sxs-lookup"><span data-stu-id="72384-136">To make a function asynchronous, use the `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="72384-137">Jeton d’annulation</span><span class="sxs-lookup"><span data-stu-id="72384-137">Cancellation Token</span></span>
<span data-ttu-id="72384-138">Certaines opérations requièrent un arrêt approprié.</span><span class="sxs-lookup"><span data-stu-id="72384-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="72384-139">Bien qu’il soit toujours préférable d’écrire du code permettant de faire face à aux incidents, définissez un argument typé [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) dans les cas où vous souhaitez traiter des demandes d’arrêt approprié.</span><span class="sxs-lookup"><span data-stu-id="72384-139">While it's always best to write code that can handle crashing,  in cases where you want to handle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="72384-140">Un `CancellationToken` est fourni pour signaler le déclenchement d’un arrêt de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="72384-140">A `CancellationToken` is provided to signal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="72384-141">Importation des espaces de noms</span><span class="sxs-lookup"><span data-stu-id="72384-141">Importing namespaces</span></span>
<span data-ttu-id="72384-142">Si vous avez besoin d’importer des espaces de noms, vous pouvez le faire comme vous en avez l’habitude à l’aide de la clause `using` .</span><span class="sxs-lookup"><span data-stu-id="72384-142">If you need to import namespaces, you can do so as usual, with the `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="72384-143">Les espaces de noms suivants sont automatiquement importés et sont donc facultatifs :</span><span class="sxs-lookup"><span data-stu-id="72384-143">The following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="72384-144">Référencement des assemblys externes</span><span class="sxs-lookup"><span data-stu-id="72384-144">Referencing External Assemblies</span></span>
<span data-ttu-id="72384-145">Pour les assemblys de framework, ajoutez des références à l’aide de la directive `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="72384-145">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="72384-146">Les assemblys suivants sont ajoutés automatiquement par l’environnement hébergeant Azure Functions :</span><span class="sxs-lookup"><span data-stu-id="72384-146">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="72384-147">Les assemblys suivants peuvent être référencés par nom simple (par exemple, `#r "AssemblyName"`) :</span><span class="sxs-lookup"><span data-stu-id="72384-147">The following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="72384-148">Référencer des assemblys personnalisés</span><span class="sxs-lookup"><span data-stu-id="72384-148">Referencing custom assemblies</span></span>

<span data-ttu-id="72384-149">Pour référencer un assembly personnalisé, vous pouvez utiliser soit un assembly *partagé*, soit un assembly *privé* :</span><span class="sxs-lookup"><span data-stu-id="72384-149">To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="72384-150">Les assemblys partagés sont communs à toutes les fonctions d’une application de fonction.</span><span class="sxs-lookup"><span data-stu-id="72384-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="72384-151">Pour référencer un assembly personnalisé, chargez-le dans votre application de fonction, par exemple dans un dossier `bin` à la racine.</span><span class="sxs-lookup"><span data-stu-id="72384-151">To reference a custom assembly, upload the assembly to your function app, such as in a `bin` folder in the function app root.</span></span> 
- <span data-ttu-id="72384-152">Les assemblys privés font partie du contexte d’une fonction donnée et sont compatibles avec le chargement indépendant de versions différentes.</span><span class="sxs-lookup"><span data-stu-id="72384-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="72384-153">Les assemblys privés doivent être chargés dans un dossier `bin` du répertoire de la fonction.</span><span class="sxs-lookup"><span data-stu-id="72384-153">Private assemblies should be uploaded in a `bin` folder in the function directory.</span></span> <span data-ttu-id="72384-154">Référencez-les avec le nom de fichier, par exemple `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="72384-154">Reference using the file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="72384-155">Pour plus d’informations sur le téléchargement de fichiers vers votre conteneur de fonctions, consultez la section suivante sur la gestion des packages.</span><span class="sxs-lookup"><span data-stu-id="72384-155">For information on how to upload files to your function folder, see the following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="72384-156">Répertoires surveillés</span><span class="sxs-lookup"><span data-stu-id="72384-156">Watched directories</span></span>

<span data-ttu-id="72384-157">Le répertoire qui contient le fichier de script de la fonction est automatiquement surveillé pour détecter les modifications apportées aux assemblys.</span><span class="sxs-lookup"><span data-stu-id="72384-157">The directory that contains the function script file is automatically watched for changes to assemblies.</span></span> <span data-ttu-id="72384-158">Pour surveiller les modifications des assemblys dans d’autres répertoires, ajoutez-les à la liste `watchDirectories` dans [host\.json].</span><span class="sxs-lookup"><span data-stu-id="72384-158">To watch for assembly changes in other directories, add them to the `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="72384-159">Utiliser des packages NuGet</span><span class="sxs-lookup"><span data-stu-id="72384-159">Using NuGet packages</span></span>
<span data-ttu-id="72384-160">Pour utiliser des packages NuGet dans une fonction C#, chargez un fichier *project.json* dans le dossier de la fonction du système de fichiers de l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="72384-160">To use NuGet packages in a C# function, upload a *project.json* file to the function's folder in the function app's file system.</span></span> <span data-ttu-id="72384-161">Voici un exemple de fichier *project.json* qui ajoute une référence à Microsoft.ProjectOxford.Face version 1.1.0 :</span><span class="sxs-lookup"><span data-stu-id="72384-161">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="72384-162">Seul .NET Framework 4.6 est pris en charge. Par conséquent, assurez-vous que votre fichier *project.json* spécifie `net46` comme indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="72384-162">Only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="72384-163">Lorsque vous chargez un fichier *project.json* , le runtime récupère les packages et ajoute automatiquement des références aux assemblys de packages.</span><span class="sxs-lookup"><span data-stu-id="72384-163">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="72384-164">Vous n’avez pas besoin d’ajouter de directives `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="72384-164">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="72384-165">Pour utiliser les types définis dans les packages NuGet, ajoutez les instructions `using` requises à votre fichier *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="72384-165">To use the types defined in the NuGet packages, add the required `using` statements to your *run.csx* file</span></span> 

<span data-ttu-id="72384-166">Dans le runtime Functions, la restauration NuGet fonctionne en comparant `project.json` et `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="72384-166">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="72384-167">Si la date et l’heure des fichiers **ne correspondent pas**, NuGet lance une restauration et télécharge des packages mis à jour.</span><span class="sxs-lookup"><span data-stu-id="72384-167">If the date and time stamps of the files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="72384-168">Si, à l’inverse, ils **correspondent**, NuGet n’effectue pas de restauration.</span><span class="sxs-lookup"><span data-stu-id="72384-168">However, if the date and time stamps of the files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="72384-169">Par conséquent, il ne faut pas déployer `project.lock.json`, car il force NuGet à ignorer la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="72384-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet to skip package restore.</span></span> <span data-ttu-id="72384-170">Pour éviter de déployer le fichier de verrouillage, ajoutez `project.lock.json` au fichier `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="72384-170">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span></span>

<span data-ttu-id="72384-171">Pour utiliser un flux NuGet personnalisé, spécifiez-le dans un fichier *Nuget.Config* à la racine de l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="72384-171">To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the Function App root.</span></span> <span data-ttu-id="72384-172">Pour plus d’informations, consultez la page [Configurer le comportement de NuGet](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="72384-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="72384-173">Utiliser un fichier project.json</span><span class="sxs-lookup"><span data-stu-id="72384-173">Using a project.json file</span></span>
1. <span data-ttu-id="72384-174">Ouvrez la fonction sur le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="72384-174">Open the function in the Azure portal.</span></span> <span data-ttu-id="72384-175">L’onglet journaux affiche la sortie d’installation du package.</span><span class="sxs-lookup"><span data-stu-id="72384-175">The logs tab displays the package installation output.</span></span>
2. <span data-ttu-id="72384-176">Pour charger un fichier project.json, utilisez l’une des méthodes décrites dans la section [Guide pratique pour mettre à jour les fichiers d’application de fonction](functions-reference.md#fileupdate) de la rubrique Informations de référence pour les développeurs sur Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="72384-176">To upload a project.json file, use one of the methods described in the [How to update function app files](functions-reference.md#fileupdate) in the Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="72384-177">Une fois le fichier *project.json* chargé, une sortie semblable à l’exemple ci-après s’affiche dans le journal de diffusion en continu de votre fonction :</span><span class="sxs-lookup"><span data-stu-id="72384-177">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="72384-178">Variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="72384-178">Environment variables</span></span>
<span data-ttu-id="72384-179">Pour obtenir une variable d’environnement ou une valeur de paramètre d’application, utilisez `System.Environment.GetEnvironmentVariable`, comme illustré dans l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="72384-179">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="72384-180">Réutilisation du code .csx</span><span class="sxs-lookup"><span data-stu-id="72384-180">Reusing .csx code</span></span>
<span data-ttu-id="72384-181">Vous pouvez utiliser des classes et des méthodes définies dans d’autres fichiers *.csx* au sein de votre fichier *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="72384-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="72384-182">Pour ce faire, utilisez les directives `#load` dans votre fichier *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="72384-182">To do that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="72384-183">Dans l’exemple suivant, une routine de journalisation nommée `MyLogger` est partagée dans *myLogger.csx* et chargés dans *run.csx* à l’aide de la directive`#load` :</span><span class="sxs-lookup"><span data-stu-id="72384-183">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span></span>

<span data-ttu-id="72384-184">Exemple *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="72384-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="72384-185">Exemple *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="72384-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="72384-186">L’utilisation d’un fichier *.csx* partagé est un cas de figure courant lorsque vous souhaitez typer fortement vos arguments entre les fonctions à l’aide d’un objet OCT.</span><span class="sxs-lookup"><span data-stu-id="72384-186">Using a shared *.csx* is a common pattern when you want to strongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="72384-187">Dans l’exemple simplifié suivant, un déclencheur HTTP et un déclencheur de file d’attente partagent un objet OCT nommé `Order` pour typer fortement les données de commande :</span><span class="sxs-lookup"><span data-stu-id="72384-187">In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span></span>

<span data-ttu-id="72384-188">Exemple avec *run.csx* pour un déclencheur HTTP :</span><span class="sxs-lookup"><span data-stu-id="72384-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting to processing queue.");

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

<span data-ttu-id="72384-189">Exemple avec *run.csx* pour un déclencheur de file d’attente :</span><span class="sxs-lookup"><span data-stu-id="72384-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="72384-190">Exemple avec *order.csx* :</span><span class="sxs-lookup"><span data-stu-id="72384-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="72384-191">Vous pouvez utiliser un chemin d’accès relatif avec la directive `#load` :</span><span class="sxs-lookup"><span data-stu-id="72384-191">You can use a relative path with the `#load` directive:</span></span>

* <span data-ttu-id="72384-192">`#load "mylogger.csx"` charge un fichier situé dans le dossier de la fonction.</span><span class="sxs-lookup"><span data-stu-id="72384-192">`#load "mylogger.csx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="72384-193">`#load "loadedfiles\mylogger.csx"` charge un fichier situé dans un dossier du dossier de la fonction.</span><span class="sxs-lookup"><span data-stu-id="72384-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span></span>
* <span data-ttu-id="72384-194">`#load "..\shared\mylogger.csx"` charge un fichier situé dans un dossier situé au même niveau que le dossier de la fonction, c’est-à-dire directement sous *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="72384-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="72384-195">La directive `#load` ne fonctionne qu’avec des fichiers *.csx* (script C#) et non avec des fichiers *.cs*.</span><span class="sxs-lookup"><span data-stu-id="72384-195">The `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="72384-196">Liaison à l’exécution au moyen des liaisons impératives</span><span class="sxs-lookup"><span data-stu-id="72384-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="72384-197">Avec C# et d’autres langages .NET, vous pouvez utiliser un schéma de liaison [impératif](https://en.wikipedia.org/wiki/Imperative_programming), par opposition aux liaisons [ *déclaratives* ](https://en.wikipedia.org/wiki/Declarative_programming) dans *function.json*.</span><span class="sxs-lookup"><span data-stu-id="72384-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="72384-198">La liaison impérative est utile lorsque les paramètres de liaison doivent être calculés au moment du runtime plutôt que lors de la conception.</span><span class="sxs-lookup"><span data-stu-id="72384-198">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="72384-199">Avec ce modèle, vous pouvez effectuer une liaison à la volée avec une liaison d’entrée et de sortie prise en charge dans le code de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="72384-199">With this pattern, you can bind to supported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="72384-200">Définissez une liaison impérative comme suit :</span><span class="sxs-lookup"><span data-stu-id="72384-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="72384-201">**N’incluez pas** d’entrée dans *function.json* pour les liaisons impératives souhaitées.</span><span class="sxs-lookup"><span data-stu-id="72384-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="72384-202">Transmettez un paramètre d’entrée [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) ou [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="72384-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="72384-203">Utilisez le modèle en C# suivant pour effectuer la liaison de données.</span><span class="sxs-lookup"><span data-stu-id="72384-203">Use the following C# pattern to perform the data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="72384-204">où `BindingTypeAttribute` est l’attribut .NET qui définit votre liaison et `T` est le type d’entrée ou de sortie pris en charge par ce type de liaison.</span><span class="sxs-lookup"><span data-stu-id="72384-204">where `BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is the input or output type that's supported by that binding type.</span></span> <span data-ttu-id="72384-205">`T` ne peut pas être un type de paramètre `out` (comme `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="72384-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="72384-206">Par exemple, la liaison de sortie de la table Mobile Apps prend en charge [six types de sortie](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), mais vous pouvez utiliser uniquement [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) pour `T`.</span><span class="sxs-lookup"><span data-stu-id="72384-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="72384-207">L’exemple de code suivant crée une [liaison de sortie d’objet blob de stockage](functions-bindings-storage-blob.md#using-a-blob-output-binding) avec un chemin d’objet blob défini au moment de l’exécution, puis écrit une chaîne vers l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="72384-207">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string to the blob.</span></span>

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

<span data-ttu-id="72384-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) définit la liaison d’entrée ou de sortie de [l’objet blob de stockage](functions-bindings-storage-blob.md), et [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) est un type de liaison de sortie pris en charge.</span><span class="sxs-lookup"><span data-stu-id="72384-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="72384-209">Le code tel quel obtient le paramètre d’application par défaut pour la chaîne de connexion de compte de stockage (c’est-à-dire `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="72384-209">As is, the code gets the default app setting for the Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="72384-210">Vous pouvez spécifier un paramètre d’application personnalisé à utiliser en ajoutant l’attribut [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) et en transmettant le tableau d’attributs dans `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="72384-210">You can specify a custom app setting to use by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="72384-211">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="72384-211">For example,</span></span>

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

<span data-ttu-id="72384-212">Le tableau suivant répertorie les attributs .NET pour chaque type de liaison et les packages dans lesquels ils sont définis.</span><span class="sxs-lookup"><span data-stu-id="72384-212">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="72384-213">Liaison</span><span class="sxs-lookup"><span data-stu-id="72384-213">Binding</span></span> | <span data-ttu-id="72384-214">Attribut</span><span class="sxs-lookup"><span data-stu-id="72384-214">Attribute</span></span> | <span data-ttu-id="72384-215">Ajouter la référence</span><span class="sxs-lookup"><span data-stu-id="72384-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="72384-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="72384-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="72384-217">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="72384-217">Event Hubs</span></span> | <span data-ttu-id="72384-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="72384-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="72384-219">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="72384-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="72384-220">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="72384-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="72384-221">Service Bus</span><span class="sxs-lookup"><span data-stu-id="72384-221">Service Bus</span></span> | <span data-ttu-id="72384-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="72384-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="72384-223">File d’attente de stockage</span><span class="sxs-lookup"><span data-stu-id="72384-223">Storage queue</span></span> | <span data-ttu-id="72384-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="72384-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="72384-225">Objet blob de stockage</span><span class="sxs-lookup"><span data-stu-id="72384-225">Storage blob</span></span> | <span data-ttu-id="72384-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="72384-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="72384-227">Table de stockage</span><span class="sxs-lookup"><span data-stu-id="72384-227">Storage table</span></span> | <span data-ttu-id="72384-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="72384-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="72384-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="72384-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="72384-230">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72384-230">Next steps</span></span>
<span data-ttu-id="72384-231">Pour plus d’informations, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="72384-231">For more information, see the following resources:</span></span>

* [<span data-ttu-id="72384-232">Meilleures pratiques pour Azure Functions</span><span class="sxs-lookup"><span data-stu-id="72384-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="72384-233">Référence du développeur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="72384-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="72384-234">Informations de référence pour les développeurs F# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="72384-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="72384-235">Azure Functions NodeJS developer reference (Référence pour les développeurs NodeJS Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="72384-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="72384-236">Azure Functions triggers and bindings (Déclencheurs et liaisons Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="72384-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
