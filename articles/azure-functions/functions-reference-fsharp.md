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
# <a name="azure-functions-f-developer-reference"></a>Informations de référence pour les développeurs F# sur Azure Functions
> [!div class="op_single_selector"]
> * [Script C#](functions-reference-csharp.md)
> * [Script F#](functions-reference-fsharp.md)
> * [Node.JS](functions-reference-node.md)
> 
> 

F # pour les fonctions de Azure est une solution pour exécuter facilement des petits éléments de code, ou « fonctions » dans le cloud de hello. Les données circulent dans votre fonction F# par le biais d’arguments de fonction. Les noms d’arguments sont spécifiés dans `function.json`, et qu’il existe des noms prédéfinis pour accéder à diverses tâches telles que hello des jetons d’enregistreur d’événements et l’annulation de fonction.

Cet article suppose que vous avez déjà lu hello [référence du développeur Azure fonctions](functions-reference.md).

## <a name="how-fsx-works"></a>Fonctionnement de .fsx
Un fichier `.fsx` est un script F#. Il peut être considéré comme un projet F# contenu dans un seul fichier. fichier Hello contient à la fois code hello pour votre programme (dans ce cas, votre fonction Azure) et des directives pour la gestion des dépendances.

Lorsque vous utilisez un `.fsx` pour une fonction d’Azure, généralement requis les assemblys sont automatiquement inclus pour vous, ce qui vous toofocus sur le code de fonction au lieu de « standard » hello.

## <a name="binding-tooarguments"></a>Liaison tooarguments
Chaque liaison prend en charge un ensemble d’arguments, comme détaillé dans hello [référence du développeur Azure fonctions déclencheurs et des liaisons](functions-triggers-bindings.md). Par exemple, une des liaisons d’arguments hello qu'un déclencheur blob prend en charge est POCO, ce qui peut être exprimé à l’aide d’un enregistrement F #. Par exemple :

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

Votre fonction Azure F# utilisera un ou plusieurs arguments. Lorsque nous parlons arguments des fonctions d’Azure, nous nous référons trop*d’entrée* arguments et *sortie* arguments. Un argument d’entrée est exactement il ressemble : entrée tooyour fonction d’Azure F #. Un *sortie* argument est données mutables ou un `byref<>` argument qui sert d’une manière toopass stockage des données *hors* de votre fonction.

Dans l’exemple hello ci-dessus, `blob` est un argument d’entrée, et `output` est un argument de sortie. Notez que nous avons utilisé `byref<>` pour `output` (il n’existe aucun hello de tooadd besoin `[<Out>]` annotation). À l’aide un `byref<>` type autorise votre toochange fonction quel argument hello enregistrement ou un objet fait référence à.

Lorsqu’un enregistrement F # est utilisé comme un type d’entrée, la définition d’enregistrement hello doit être marquée avec `[<CLIMutable>]` dans des champs hello correctement avant de passer hello enregistrement tooyour fonction tooallow hello Azure fonctions framework tooset ordre. Dans les coulisses hello, `[<CLIMutable>]` génère des méthodes setter de propriétés de l’enregistrement hello. Par exemple :

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

Une classe F# est également utilisable pour les arguments d’entrée et de sortie. Pour une classe, les propriétés nécessitent généralement des méthodes getter et setter. Par exemple :

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a>Journalisation
toolog sortie tooyour [journaux de diffusion en continu](../app-service-web/web-sites-streaming-logs-and-console.md) en F #, votre fonction doit prendre un argument de type `TraceWriter`. Par souci de cohérence, nous vous recommandons de nommer cet argument `log`. Par exemple :

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a>Async
Hello `async` workflow peut être utilisé, mais le résultat de hello doit tooreturn un `Task`. Pour ce faire, utilisez `Async.StartAsTask`. Par exemple :

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a>Jeton d’annulation
Si votre fonction doit toohandle arrêt en douceur, vous pouvez lui attribuer un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument. conjointement utilisable avec `async`. Par exemple :

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a>Importation des espaces de noms
Espaces de noms peuvent être ouverts dans hello normalement :

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Hello suivant des espaces de noms est automatiquement ouvertes :

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`.

## <a name="referencing-external-assemblies"></a>Référencement des assemblys externes
De même, l’assembly framework références ajoutées par hello `#r "AssemblyName"` directive.

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
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
* `System.Net.Http.Formatting`.

En outre, hello suivant des assemblys est spécial casse et peuvent être référencées par simplename (par exemple, `#r "AssemblyName"`) :

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNEt.WebHooks.Common`.

Si vous avez besoin de tooreference un assembly privé, vous pouvez télécharger le fichier d’assembly hello dans un `bin` fonction tooyour relatif de dossier et de la référence à l’aide de hello nom de fichier (par exemple)  `#r "MyAssembly.dll"`). Pour plus d’informations sur le fonctionnement des fichiers de dossier de fonction tooyour tooupload, consultez hello suivant la section sur la gestion des packages.

## <a name="editor-prelude"></a>Préambule destiné à l’éditeur
Un éditeur qui prend en charge les Services du compilateur F # ne seront pas prenant en charge des espaces de noms hello et des assemblys qui inclut automatiquement les fonctions de Azure. Par conséquent, il peut être utile tooinclude une étape préliminaire qui permet de rechercher les assemblys hello que vous utilisez l’éditeur de hello et tooexplicitly ouvrir les espaces de noms. Par exemple :

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

Lorsque les fonctions Azure s’exécute votre code, il traite source hello avec `COMPILED` défini prélude d’éditeur hello sera ignoré.

<a name="package"></a>

## <a name="package-management"></a>Gestion des packages
les packages NuGet toouse dans une fonction) (F #, ajoutez un `project.json` dossier de la fonction toohello hello du fichier dans le système de fichiers de l’application hello (fonction). Voici un exemple `project.json` fichier qui ajoute une référence de package NuGet trop`Microsoft.ProjectOxford.Face` version 1.1.0. :

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

Hello .NET Framework 4.6 est prise en charge uniquement, donc vous assurer que votre `project.json` fichier spécifie `net46` comme indiqué ici.

Lorsque vous téléchargez un `project.json` fichier, hello runtime Obtient les packages de hello et ajoute automatiquement les assemblys de package toohello de références. Vous n’avez pas besoin de tooadd `#r "AssemblyName"` directives. Ajoutez simplement hello requis `open` instructions tooyour `.fsx` fichier.

Vous souhaiterez peut-être tooput référence automatiquement les assemblys dans votre prélude éditeur, tooimprove interaction de votre éditeur avec les Services de compilation F #.

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a>Comment tooadd un `project.json` fichier tooyour Azure (fonction)
1. BEGIN en vous assurant que votre application de la fonction est en cours d’exécution, ce que vous pouvez faire en ouvrant votre fonction Bonjour portail Azure. Cela donne également accès des journaux de diffusion en continu toohello où la sortie d’installation de package s’affichera.
2. tooupload un `project.json` de fichiers, utilisez une des méthodes hello décrites dans [fonctionnement des fichiers de l’application tooupdate](functions-reference.md#fileupdate). Si vous utilisez [déploiement continu pour les fonctions Azure](functions-continuous-deployment.md), vous pouvez ajouter un `project.json` tooyour branche dans tooexperiment d’ordre avec celui-ci avant de l’ajouter branche de déploiement tooyour de mise en lots de fichiers.
3. Après avoir hello `project.json` fichier est ajouté, vous verrez toohello similaire de sortie dans votre fonction de l’exemple suivant de diffusion en continu de journal :

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
tooget une variable d’environnement ou une valeur de paramètre d’application, utilisez `System.Environment.GetEnvironmentVariable`, par exemple :

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a>Réutilisation du code .fsx
Vous pouvez utiliser le code d’autres fichiers `.fsx` au moyen d’une directive `#load`. Par exemple :

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

Fournit des chemins d’accès toohello `#load` directive sont emplacement relatif toohello de votre `.fsx` fichier.

* `#load "logger.fsx"`charge un fichier situé dans le dossier de fonction hello.
* `#load "package\logger.fsx"`charge un fichier situé dans hello `package` hello fonction dossier.
* `#load "..\shared\mylogger.fsx"`charge un fichier situé dans hello `shared` dossier hello même niveau en tant que dossier de fonction hello, autrement dit, directement sous `wwwroot`.

Hello `#load` directive ne fonctionne qu’avec `.fsx` les fichiers (script) (F #) et non avec `.fs` fichiers.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello suivant des ressources :

* [F# Guide](/dotnet/articles/fsharp/index) (Guide F#)
* [Meilleures pratiques pour Azure Functions](functions-best-practices.md)
* [Référence du développeur Azure Functions](functions-reference.md)
* [Informations de référence pour les développeurs C# sur Azure Functions](functions-reference-csharp.md)
* [Azure Functions NodeJS developer reference (Référence pour les développeurs NodeJS Azure Functions)](functions-reference-node.md)
* [Déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md)
* [Test des fonctions Azure](functions-test-a-function.md)
* [Mise à l’échelle d’Azure Functions](functions-scale.md)

