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
# <a name="azure-functions-c-script-developer-reference"></a>Informations de référence pour les développeurs de scripts C# Azure Functions
> [!div class="op_single_selector"]
> * [Script C#](functions-reference-csharp.md)
> * [Script F#](functions-reference-fsharp.md)
> * [Node.JS](functions-reference-node.md)
>
>

Hello expérience de script c# pour les fonctions de Azure est basé sur hello Azure WebJobs SDK. Les données circulent dans votre fonction C# via des arguments de méthode. Les noms d’arguments sont spécifiés dans `function.json`, et qu’il existe des noms prédéfinis pour accéder à diverses tâches telles que hello des jetons d’enregistreur d’événements et l’annulation de fonction.

Cet article suppose que vous avez déjà lu hello [référence du développeur Azure fonctions](functions-reference.md).

Pour plus d’informations sur l’utilisation des bibliothèques de classes C#, consultez la page [Utiliser des bibliothèques de classes .NET avec Azure Functions](functions-dotnet-class-library.md).

## <a name="how-csx-works"></a>Fonctionnement de .csx
Hello `.csx` format vous permet de toowrite moins de « standard » et le focus sur l’écriture de simplement une fonction c#. Inclure les références d’assembly et les espaces de noms au début de hello du fichier de hello comme d’habitude. Au lieu de tout encapsuler dans un espace de noms et une classe, définissez simplement une méthode `Run`. Si vous avez besoin de tooinclude toutes les classes, de l’instance toodefine brut est ancien objet CLR (POCO) des objets, vous pouvez inclure une classe à l’intérieur de hello même fichier.   

## <a name="binding-tooarguments"></a>Liaison tooarguments
fonction liée tooa c# via hello sont Hello diverses liaisons `name` propriété Bonjour *function.json* configuration. Chaque liaison prend en charge ses propres types ; par exemple, un déclencheur d’objets blob peut prendre en charge une chaîne, un OCT ou un CloudBlockBlob. les types Hello pris en charge sont documentées dans la référence hello pour chaque liaison. Des méthodes getter et setter doivent être définies pour chaque propriété d’un objet OCT.

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

Vous pouvez utiliser une valeur de retour de méthode pour une liaison de sortie, à l’aide du nom de hello `$return` dans *function.json*:

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

liaison de sortie de plusieurs valeurs tooan toowrite, utilisez hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types. Ces types sont en écriture seule des collections qui sont écrite toohello liaison de sortie issue de la méthode hello.

Cet exemple écrit plusieurs messages de file d’attente à l’aide de `ICollector` :

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>Journalisation
toolog sortie des journaux de diffusion en continu tooyour en c#, incluent un argument de type `TraceWriter`. Nous vous recommandons de le nommer `log`. Évitez d’utiliser `Console.Write` dans Azure Functions. 

`TraceWriter`est défini dans hello [Kit de développement logiciel Azure WebJobs](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs). Hello du niveau de journalisation de `TraceWriter` peuvent être configurés dans [hôte\.json].

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>Async
toomake une fonction asynchrone, utilisez hello `async` (mot clé) et retournent un `Task` objet.

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
Certaines opérations requièrent un arrêt approprié. Bien qu’il soit toujours meilleure code toowrite qui peut gérer en panne, dans les cas où vous souhaitez que les demandes de l’arrêt correct de toohandle, vous définissez un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument de type.  A `CancellationToken` est fourni toosignal qu’un arrêt de l’hôte est déclenché.

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
Si vous avez besoin d’espaces de noms tooimport, vous pouvez le faire comme d’habitude, avec hello `using` clause.

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Hello espaces de noms suivants sont automatiquement importés et sont par conséquent facultatifs :

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>Référencement des assemblys externes
Pour les assemblys d’infrastructure, ajoutez des références à l’aide de hello `#r "AssemblyName"` directive.

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Hello assemblys suivants sont automatiquement ajoutés par les fonctions d’Azure hello environnement d’hébergement :

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

Hello assemblys suivants peuvent être référencées par le nom simple (par exemple, `#r "AssemblyName"`) :

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>Référencer des assemblys personnalisés

tooreference un assembly personnalisé, vous pouvez utiliser un *partagé* assembly ou un *privé* assembly :
- Les assemblys partagés sont communs à toutes les fonctions d’une application de fonction. tooreference un assembly personnalisé, télécharger l’application de fonction hello assembly tooyour, comme dans un `bin` dossier racine d’application hello (fonction). 
- Les assemblys privés font partie du contexte d’une fonction donnée et sont compatibles avec le chargement indépendant de versions différentes. Les assemblys privés doivent être téléchargées dans un `bin` dossier du répertoire de fonction hello. Référence à l’aide de nom de fichier hello, tel que `#r "MyAssembly.dll"`. 

Pour plus d’informations sur le fonctionnement des fichiers de dossier de fonction tooyour tooupload, consultez hello suivant la section sur la gestion des packages.

### <a name="watched-directories"></a>Répertoires surveillés

Hello répertoire qui contient le fichier de script de fonction hello est automatiquement surveillé pour tooassemblies de modifications. toowatch modifier des assemblys dans d’autres répertoires, ajoutez-les toohello `watchDirectories` liste [hôte\.json].

## <a name="using-nuget-packages"></a>Utiliser des packages NuGet
les packages NuGet toouse dans une fonction c#, téléchargez un *project.json* dossier de la fonction toohello du fichier dans le système de fichiers de l’application hello (fonction). Voici un exemple *project.json* fichier qui ajoute une référence tooMicrosoft.ProjectOxford.Face version 1.1.0 :

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

Hello .NET Framework 4.6 est prise en charge uniquement, donc vous assurer que votre *project.json* fichier spécifie `net46` comme indiqué ici.

Lorsque vous téléchargez un *project.json* de fichiers, obtient les packages de hello hello runtime et ajoute automatiquement les assemblys de package toohello de références. Vous n’avez pas besoin de tooadd `#r "AssemblyName"` directives. les types de hello toouse définis dans les packages NuGet hello, ajouter hello requis `using` instructions tooyour *run.csx* fichier 

Lors de l’exécution de fonctions hello NuGet restauration fonctionne en comparant `project.json` et `project.lock.json`. Si hello cachets de date et heure des fichiers de hello **pas** exécute de correspondance, une restauration de NuGet et des téléchargements de NuGet mis à jour les packages. Toutefois, si hello cachets de date et heure des fichiers de hello **faire** correspondance, NuGet n’effectue pas une restauration. Par conséquent, `project.lock.json` ne doit pas être déployé car il entraîne la restauration des packages NuGet tooskip. tooavoid déploiement verrou de hello, ajoutez hello `project.lock.json` toohello `.gitignore` fichier.

toouse un flux NuGet personnalisé, spécifiez hello de flux dans un *Nuget.Config* fichier racine d’application de la fonction hello. Pour plus d’informations, consultez la page [Configurer le comportement de NuGet](/nuget/consume-packages/configuring-nuget-behavior).

### <a name="using-a-projectjson-file"></a>Utiliser un fichier project.json
1. Ouvrez la fonction hello Bonjour portail Azure. Hello ouvre l’onglet affiche hello package installation la sortie.
2. tooupload un fichier project.json, utilisez une des méthodes de hello décrites dans hello [fonctionnement des fichiers de l’application tooupdate](functions-reference.md#fileupdate) dans la rubrique de référence du développeur hello fonctions d’Azure.
3. Après avoir hello *project.json* fichier est téléchargé, vous voyez la sortie comme hello dans votre fonction de l’exemple suivant de diffusion en continu de journal :

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
tooget une variable d’environnement ou une valeur de paramètre d’application, utilisez `System.Environment.GetEnvironmentVariable`, comme indiqué dans l’exemple de code suivant de hello :

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
Vous pouvez utiliser des classes et des méthodes définies dans d’autres fichiers *.csx* au sein de votre fichier *run.csx*. toodo, qui utilisent `#load` directives dans votre *run.csx* fichier. Bonjour l’exemple suivant, une routine de journalisation nommé `MyLogger` est partagé dans *myLogger.csx* et chargés en *run.csx* à l’aide de hello `#load` directive :

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

À l’aide d’un élément partagé *.csx* est courant lorsque vous souhaitez toostrongly tapez vos arguments entre les fonctions à l’aide d’un objet POCO. Bonjour simplifiée de l’exemple suivant, un déclencheur HTTP et le déclencheur de la file d’attente partagent un objet POCO nommé `Order` toostrongly les données de commande type hello :

Exemple avec *run.csx* pour un déclencheur HTTP :

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

Vous pouvez utiliser un chemin d’accès relatif par hello `#load` directive :

* `#load "mylogger.csx"`charge un fichier situé dans le dossier de fonction hello.
* `#load "loadedfiles\mylogger.csx"`charge un fichier situé dans un dossier de fonction hello.
* `#load "..\shared\mylogger.csx"`charge un fichier situé dans un dossier à hello même niveau en tant que dossier de fonction hello, autrement dit, directement sous *wwwroot*.

Hello `#load` directive fonctionne uniquement avec *.csx* les fichiers (C# script), pas avec *.cs* fichiers.

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>Liaison à l’exécution au moyen des liaisons impératives

En c# et d’autres langages .NET, vous pouvez utiliser un [impératif](https://en.wikipedia.org/wiki/Imperative_programming) modèle de liaison, en opposition toohello [ *déclarative* ](https://en.wikipedia.org/wiki/Declarative_programming) liaisons dans *function.json*. Liaison impératif est utile lorsque les paramètres de liaison doivent toobe calculée au moment de l’exécution au lieu de conception. Avec ce modèle, vous pouvez lier toosupported entrée et sortie de liaison à la volée dans votre code de fonction.

Définissez une liaison impérative comme suit :

- **N’incluez pas** d’entrée dans *function.json* pour les liaisons impératives souhaitées.
- Transmettez un paramètre d’entrée [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) ou [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).
- Utilisez hello suivant c# modèle tooperform hello liaison de données.

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

où `BindingTypeAttribute` est l’attribut .NET hello qui définit votre liaison et `T` est hello type d’entrée ou de sortie qui est pris en charge par ce type de liaison. `T` ne peut pas être un type de paramètre `out` (comme `out JObject`). Par exemple, la liaison de sortie de la table Mobile Apps prend en charge [six types de sortie](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), mais vous pouvez utiliser uniquement [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) pour `T`.

Hello suivant l’exemple de code crée un [liaison de sortie blob de stockage](functions-bindings-storage-blob.md#using-a-blob-output-binding) avec l’objet blob de chemin d’accès qui est définie au moment de l’exécution, puis écrit un chaîne toohello blob.

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

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) définit hello [objet blob de stockage](functions-bindings-storage-blob.md) d’entrée ou sortie de la liaison, et [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) est un type de liaison de sortie pris en charge.
En l’état, code de hello Obtient le paramètre d’application par défaut hello pour hello chaîne de connexion de compte de stockage (c'est-à-dire `AzureWebJobsStorage`). Vous pouvez spécifier un toouse de paramètre d’application personnalisé en ajoutant le [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) et en passant le tableau d’attributs hello dans `BindAsync<T>()`. Par exemple,

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

Hello tableau suivant répertorie les attributs .NET hello pour chaque liaison type et hello les packages dans lequel ils sont définis.

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
Pour plus d’informations, consultez hello suivant des ressources :

* [Meilleures pratiques pour Azure Functions](functions-best-practices.md)
* [Référence du développeur Azure Functions](functions-reference.md)
* [Informations de référence pour les développeurs F# sur Azure Functions](functions-reference-fsharp.md)
* [Azure Functions NodeJS developer reference (Référence pour les développeurs NodeJS Azure Functions)](functions-reference-node.md)
* [Azure Functions triggers and bindings (Déclencheurs et liaisons Azure Functions)](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
