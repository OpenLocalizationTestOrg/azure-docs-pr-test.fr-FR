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
# <a name="azure-functions-c-script-developer-reference"></a>Informations de référence pour les développeurs de scripts C# Azure Functions
> [!div class="op_single_selector"]
> * [Script C#](functions-reference-csharp.md)
> * [Script F#](functions-reference-fsharp.md)
> * [Node.JS](functions-reference-node.md)
>
>

L’expérience de scripts C# pour Azure Functions repose sur le Kit de développement logiciel (SDK) Azure WebJobs. Les données circulent dans votre fonction C# via des arguments de méthode. Les noms d’argument sont spécifiés dans `function.json`, et il existe des noms prédéfinis pour accéder à des éléments tels que l’enregistreur de fonctions et les jetons d’annulation.

Cet article suppose que vous ayez déjà lu l’article [Informations de référence pour les développeurs sur Azure Functions](functions-reference.md).

Pour plus d’informations sur l’utilisation des bibliothèques de classes C#, consultez la page [Utiliser des bibliothèques de classes .NET avec Azure Functions](functions-dotnet-class-library.md).

## <a name="how-csx-works"></a>Fonctionnement de .csx
Le format `.csx` vous permet d’écrire de façon moins « réutilisable » et de vous concentrer uniquement sur l’écriture d’une fonction C#. Ajoutez les éventuels références d’assemblys et espaces de noms au début du fichier, comme d’habitude. Au lieu de tout encapsuler dans un espace de noms et une classe, définissez simplement une méthode `Run`. Si vous devez inclure toutes les classes, par exemple pour définir des objets OCT (objets CLR traditionnels), vous pouvez inclure une classe dans le même fichier.   

## <a name="binding-to-arguments"></a>Liaison aux arguments
Les diverses liaisons sont liées à une fonction C# par le biais de la propriété `name` de la configuration *function.json*. Chaque liaison prend en charge ses propres types ; par exemple, un déclencheur d’objets blob peut prendre en charge une chaîne, un OCT ou un CloudBlockBlob. Les types pris en charge sont documentées dans la référence de chaque liaison. Des méthodes getter et setter doivent être définies pour chaque propriété d’un objet OCT.

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

## <a name="using-method-return-value-for-output-binding"></a>Utiliser la valeur renvoyée par la méthode pour la liaison de sortie

Vous pouvez utiliser une valeur renvoyée par la méthode pour une liaison de sortie, en utilisant le nom `$return` dans *function.json* :

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

## <a name="writing-multiple-output-values"></a>Écrire plusieurs valeurs de sortie

Pour écrire plusieurs valeurs dans une liaison de sortie, utilisez le type [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou le type [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs). Ces types sont des collections en écriture seule, écrites dans la liaison de sortie à la fin de la méthode.

Cet exemple écrit plusieurs messages de file d’attente à l’aide de `ICollector` :

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>Journalisation
Pour consigner la sortie dans vos journaux de diffusion en continu en C#, ajoutez un argument de type `TraceWriter`. Nous vous recommandons de le nommer `log`. Évitez d’utiliser `Console.Write` dans Azure Functions. 

`TraceWriter` est défini dans le [Kit de développement logiciel (SDK) Azure WebJobs](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs). Le niveau de journalisation de `TraceWriter` est configurable dans [host\.json].

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>Async
Pour rendre une fonction asynchrone, utilisez le mot clé `async` et retournez un objet `Task`.

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a>Jeton d’annulation
Certaines opérations requièrent un arrêt approprié. Bien qu’il soit toujours préférable d’écrire du code permettant de faire face à aux incidents, définissez un argument typé [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) dans les cas où vous souhaitez traiter des demandes d’arrêt approprié.  Un `CancellationToken` est fourni pour signaler le déclenchement d’un arrêt de l’hôte.

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

## <a name="importing-namespaces"></a>Importation des espaces de noms
Si vous avez besoin d’importer des espaces de noms, vous pouvez le faire comme vous en avez l’habitude à l’aide de la clause `using` .

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Les espaces de noms suivants sont automatiquement importés et sont donc facultatifs :

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>Référencement des assemblys externes
Pour les assemblys de framework, ajoutez des références à l’aide de la directive `#r "AssemblyName"` .

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Les assemblys suivants sont ajoutés automatiquement par l’environnement hébergeant Azure Functions :

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

Les assemblys suivants peuvent être référencés par nom simple (par exemple, `#r "AssemblyName"`) :

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>Référencer des assemblys personnalisés

Pour référencer un assembly personnalisé, vous pouvez utiliser soit un assembly *partagé*, soit un assembly *privé* :
- Les assemblys partagés sont communs à toutes les fonctions d’une application de fonction. Pour référencer un assembly personnalisé, chargez-le dans votre application de fonction, par exemple dans un dossier `bin` à la racine. 
- Les assemblys privés font partie du contexte d’une fonction donnée et sont compatibles avec le chargement indépendant de versions différentes. Les assemblys privés doivent être chargés dans un dossier `bin` du répertoire de la fonction. Référencez-les avec le nom de fichier, par exemple `#r "MyAssembly.dll"`. 

Pour plus d’informations sur le téléchargement de fichiers vers votre conteneur de fonctions, consultez la section suivante sur la gestion des packages.

### <a name="watched-directories"></a>Répertoires surveillés

Le répertoire qui contient le fichier de script de la fonction est automatiquement surveillé pour détecter les modifications apportées aux assemblys. Pour surveiller les modifications des assemblys dans d’autres répertoires, ajoutez-les à la liste `watchDirectories` dans [host\.json].

## <a name="using-nuget-packages"></a>Utiliser des packages NuGet
Pour utiliser des packages NuGet dans une fonction C#, chargez un fichier *project.json* dans le dossier de la fonction du système de fichiers de l’application de fonction. Voici un exemple de fichier *project.json* qui ajoute une référence à Microsoft.ProjectOxford.Face version 1.1.0 :

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

Seul .NET Framework 4.6 est pris en charge. Par conséquent, assurez-vous que votre fichier *project.json* spécifie `net46` comme indiqué ici.

Lorsque vous chargez un fichier *project.json* , le runtime récupère les packages et ajoute automatiquement des références aux assemblys de packages. Vous n’avez pas besoin d’ajouter de directives `#r "AssemblyName"` . Pour utiliser les types définis dans les packages NuGet, ajoutez les instructions `using` requises à votre fichier *run.csx*. 

Dans le runtime Functions, la restauration NuGet fonctionne en comparant `project.json` et `project.lock.json`. Si la date et l’heure des fichiers **ne correspondent pas**, NuGet lance une restauration et télécharge des packages mis à jour. Si, à l’inverse, ils **correspondent**, NuGet n’effectue pas de restauration. Par conséquent, il ne faut pas déployer `project.lock.json`, car il force NuGet à ignorer la restauration des packages. Pour éviter de déployer le fichier de verrouillage, ajoutez `project.lock.json` au fichier `.gitignore`.

Pour utiliser un flux NuGet personnalisé, spécifiez-le dans un fichier *Nuget.Config* à la racine de l’application de fonction. Pour plus d’informations, consultez la page [Configurer le comportement de NuGet](/nuget/consume-packages/configuring-nuget-behavior).

### <a name="using-a-projectjson-file"></a>Utiliser un fichier project.json
1. Ouvrez la fonction sur le Portail Azure. L’onglet journaux affiche la sortie d’installation du package.
2. Pour charger un fichier project.json, utilisez l’une des méthodes décrites dans la section [Guide pratique pour mettre à jour les fichiers d’application de fonction](functions-reference.md#fileupdate) de la rubrique Informations de référence pour les développeurs sur Azure Functions.
3. Une fois le fichier *project.json* chargé, une sortie semblable à l’exemple ci-après s’affiche dans le journal de diffusion en continu de votre fonction :

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

## <a name="environment-variables"></a>Variables d’environnement
Pour obtenir une variable d’environnement ou une valeur de paramètre d’application, utilisez `System.Environment.GetEnvironmentVariable`, comme illustré dans l’exemple de code suivant :

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

## <a name="reusing-csx-code"></a>Réutilisation du code .csx
Vous pouvez utiliser des classes et des méthodes définies dans d’autres fichiers *.csx* au sein de votre fichier *run.csx*. Pour ce faire, utilisez les directives `#load` dans votre fichier *run.csx*. Dans l’exemple suivant, une routine de journalisation nommée `MyLogger` est partagée dans *myLogger.csx* et chargés dans *run.csx* à l’aide de la directive`#load` :

Exemple *run.csx*:

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

Exemple *mylogger.csx*:

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

L’utilisation d’un fichier *.csx* partagé est un cas de figure courant lorsque vous souhaitez typer fortement vos arguments entre les fonctions à l’aide d’un objet OCT. Dans l’exemple simplifié suivant, un déclencheur HTTP et un déclencheur de file d’attente partagent un objet OCT nommé `Order` pour typer fortement les données de commande :

Exemple avec *run.csx* pour un déclencheur HTTP :

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

Exemple avec *run.csx* pour un déclencheur de file d’attente :

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

Exemple avec *order.csx* :

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

Vous pouvez utiliser un chemin d’accès relatif avec la directive `#load` :

* `#load "mylogger.csx"` charge un fichier situé dans le dossier de la fonction.
* `#load "loadedfiles\mylogger.csx"` charge un fichier situé dans un dossier du dossier de la fonction.
* `#load "..\shared\mylogger.csx"` charge un fichier situé dans un dossier situé au même niveau que le dossier de la fonction, c’est-à-dire directement sous *wwwroot*.

La directive `#load` ne fonctionne qu’avec des fichiers *.csx* (script C#) et non avec des fichiers *.cs*.

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>Liaison à l’exécution au moyen des liaisons impératives

Avec C# et d’autres langages .NET, vous pouvez utiliser un schéma de liaison [impératif](https://en.wikipedia.org/wiki/Imperative_programming), par opposition aux liaisons [ *déclaratives* ](https://en.wikipedia.org/wiki/Declarative_programming) dans *function.json*. La liaison impérative est utile lorsque les paramètres de liaison doivent être calculés au moment du runtime plutôt que lors de la conception. Avec ce modèle, vous pouvez effectuer une liaison à la volée avec une liaison d’entrée et de sortie prise en charge dans le code de votre fonction.

Définissez une liaison impérative comme suit :

- **N’incluez pas** d’entrée dans *function.json* pour les liaisons impératives souhaitées.
- Transmettez un paramètre d’entrée [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) ou [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).
- Utilisez le modèle en C# suivant pour effectuer la liaison de données.

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

où `BindingTypeAttribute` est l’attribut .NET qui définit votre liaison et `T` est le type d’entrée ou de sortie pris en charge par ce type de liaison. `T` ne peut pas être un type de paramètre `out` (comme `out JObject`). Par exemple, la liaison de sortie de la table Mobile Apps prend en charge [six types de sortie](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), mais vous pouvez utiliser uniquement [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) pour `T`.

L’exemple de code suivant crée une [liaison de sortie d’objet blob de stockage](functions-bindings-storage-blob.md#using-a-blob-output-binding) avec un chemin d’objet blob défini au moment de l’exécution, puis écrit une chaîne vers l’objet blob.

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

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) définit la liaison d’entrée ou de sortie de [l’objet blob de stockage](functions-bindings-storage-blob.md), et [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) est un type de liaison de sortie pris en charge.
Le code tel quel obtient le paramètre d’application par défaut pour la chaîne de connexion de compte de stockage (c’est-à-dire `AzureWebJobsStorage`). Vous pouvez spécifier un paramètre d’application personnalisé à utiliser en ajoutant l’attribut [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) et en transmettant le tableau d’attributs dans `BindAsync<T>()`. Par exemple,

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

Le tableau suivant répertorie les attributs .NET pour chaque type de liaison et les packages dans lesquels ils sont définis.

> [!div class="mx-codeBreakAll"]
| Liaison | Attribut | Ajouter la référence |
|------|------|------|
| Cosmos DB | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| Event Hubs | [`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| Mobile Apps | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| Notification Hubs | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| Service Bus | [`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| File d’attente de stockage | [`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Objet blob de stockage | [`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Table de stockage | [`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Twilio | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez les ressources suivantes :

* [Meilleures pratiques pour Azure Functions](functions-best-practices.md)
* [Référence du développeur Azure Functions](functions-reference.md)
* [Informations de référence pour les développeurs F# sur Azure Functions](functions-reference-fsharp.md)
* [Azure Functions NodeJS developer reference (Référence pour les développeurs NodeJS Azure Functions)](functions-reference-node.md)
* [Azure Functions triggers and bindings (Déclencheurs et liaisons Azure Functions)](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
