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
# <a name="azure-functions-external-file-bindings-preview"></a>Liaisons de fichiers externes Azure Functions (version préliminaire)
Cet article explique comment toomanipulate fichiers à partir de SaaS différents fournisseurs (par exemple, OneDrive, Dropbox) dans votre fonction utilisant des liaisons intégrées. Azure Functions prend en charge les liaisons de déclencheur, d’entrée et de sortie pour les fichiers externes.

Cette liaison crée des connexions de l’API tooSaaS fournisseurs, ou utilise des connexions API existantes du groupe de ressources de votre application de fonction.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a>Connexions de fichiers prises en charge

|Connecteur|Déclencheur|Entrée|Sortie|
|:-----|:---:|:---:|:---:|
|[Box](https://www.box.com)|x|x|x
|[Dropbox](https://www.dropbox.com)|x|x|x
|[FTP](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|x|x|x
|[OneDrive](https://onedrive.live.com)|x|x|x
|[OneDrive Entreprise](https://onedrive.live.com/about/business/)|x|x|x
|[SFTP](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|x|x|x
|[Google Drive](https://www.google.com/drive/)||x|x|

> [!NOTE]
> Les connexions aux fichiers externes peuvent également servir dans les applications [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)

## <a name="external-file-trigger-binding"></a>Liaison de déclencheur de fichier externe

déclencheur de fichier externe Azure Hello vous permet de surveiller un dossier distant et exécuter votre code de fonction lorsque des modifications sont détectées.

déclencheur de fichier externe Hello utilise hello objets JSON Bonjour suivants `bindings` tableau de function.json

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

### <a name="name-patterns"></a>Modèles de nom
Vous pouvez spécifier un modèle de nom de fichier Bonjour `path` propriété. dossier Hello référencé doit exister dans le fournisseur de SaaS hello.
Exemples :

```json
"path": "input/original-{name}",
```

Ce chemin d’accès est de trouver un fichier nommé *d’origine-File1.txt* Bonjour *d’entrée* dossier et la valeur de hello de hello `name` variable dans le code de la fonction serait `File1.txt`.

Autre exemple :

```json
"path": "input/{filename}.{fileextension}",
```

Ce chemin d’accès est également trouver un fichier nommé *d’origine-File1.txt*et la valeur hello Hello `filename` et `fileextension` variables dans le code de la fonction serait *d’origine-File1* et  *txt*.

Vous pouvez limiter le type de fichier hello de fichiers à l’aide d’une valeur fixe pour l’extension de fichier hello. Par exemple :

```json
"path": "samples/{name}.png",
```

Dans ce cas, seul *.png* fichiers Bonjour *exemples* dossier déclencheur hello (fonction).

Les accolades sont des caractères spéciaux dans les modèles de nom. toospecify les noms de fichiers qui ont des accolades dans nom hello, accolades doubles hello.
Par exemple :

```json
"path": "images/{{20140101}}-{name}",
```

Ce chemin d’accès est de trouver un fichier nommé *{20140101}-soundfile.mp3* Bonjour *images* dossier et hello `name` valeur de la variable dans le code de la fonction hello serait *soundfile.mp3*.

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

### <a name="handling-poison-files"></a>Gestion des fichiers incohérents
En cas d’échec d’une fonction de déclencheur de fichier externe, les fonctions de Azure essaie de nouveau cette fonction des heures de too5 par défaut (y compris la première tentative de hello) pour un fichier donné.
Si toutes les 5 tentatives échouent, les fonctions ajoute un message tooa stockage file d’attente nommée *webjobs-apihubtrigger-incohérents*. message de file d’attente Hello pour les fichiers de messages incohérents est un objet JSON qui contient les propriétés suivantes de hello :

* ID de fonction (au format de hello  *&lt;nom de l’application fonction >*. Fonctions.  *&lt;nom de la fonction >*)
* FileType
* FolderName
* FileName
* ETag (identificateur de version du fichier, par exemple : « 0x8D1DC6E70A277EF »)


<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Utilisation du déclencheur
Dans les fonctions C#, vous lier des données de fichier d’entrée toohello à l’aide d’un paramètre nommé dans votre signature de fonction, comme `<T> <name>`.
Où `T` est que les données de hello toodeserialize, de type de données de hello et `paramName` est le nom hello spécifié dans le [déclencher JSON](#trigger). Dans les fonctions de Node.js, vous accédez à l’aide des données de fichier d’entrée hello `context.bindings.<name>`.

fichier de Hello pouvant être désérialisé dans n’importe quel Hello les types suivants :

* N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour les données de fichier sérialisées en JSON.
  Si vous déclarez un type d’entrée personnalisé (par exemple, `FooType`), des données JSON toodeserialize hello tente de fonctions d’Azure vers le type spécifié.
* Chaîne : utile pour les données de fichier texte.

Dans les fonctions C#, vous pouvez également lier tooany des types suivants de hello et hello fonctions runtime essaie de désérialiser des données de fichier hello à l’aide de ce type :

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a>Exemple de déclencheur
Supposez que vous avez hello suivant function.json, qui définit un déclencheur de fichier externe :

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

Voir exemple hello spécifiques au langage qui enregistre le contenu de hello de chaque fichier qui est ajouté à toohello les dossier surveillé.

* [C#](#triggercsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a>Utilisation du déclencheur en C# #

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

### <a name="trigger-usage-in-nodejs"></a>Utilisation du déclencheur en Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a>Liaison d’entrée de fichier externe
liaison d’entrée de fichier externe Azure Hello vous permet de toouse un fichier à partir d’un dossier externe dans votre fonction.

fonction tooa d’entrée de fichier externe Hello utilise hello objets JSON Bonjour suivants `bindings` tableau de function.json :

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

Notez hello suivantes :

* `path`doit contenir le nom du dossier hello et nom de fichier hello. Par exemple, si vous avez un [déclencheur de la file d’attente](functions-bindings-storage-queue.md) dans votre fonction, vous pouvez utiliser `"path": "samples-workitems/{queueTrigger}"` toopoint tooa fichier hello `samples-workitems` dossier avec un nom qui correspond au nom de fichier hello spécifié dans le message d’appel du déclencheur.   

<a name="inputusage"></a>

## <a name="input-usage"></a>Utilisation en entrée
Dans les fonctions C#, vous lier des données de fichier d’entrée toohello à l’aide d’un paramètre nommé dans votre signature de fonction, comme `<T> <name>`.
Où `T` est que les données de hello toodeserialize, de type de données de hello et `paramName` est le nom hello spécifié dans le [liaison d’entrée](#input). Dans les fonctions de Node.js, vous accédez à l’aide des données de fichier d’entrée hello `context.bindings.<name>`.

fichier de Hello pouvant être désérialisé dans n’importe quel Hello les types suivants :

* N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour les données de fichier sérialisées en JSON.
  Si vous déclarez un type d’entrée personnalisé (par exemple, `InputType`), des données JSON toodeserialize hello tente de fonctions d’Azure vers le type spécifié.
* Chaîne : utile pour les données de fichier texte.

Dans les fonctions C#, vous pouvez également lier tooany des types suivants de hello et hello fonctions runtime essaie de désérialiser des données de fichier hello à l’aide de ce type :

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a>Liaison de sortie de fichier externe
liaison vous permet de toowrite fichiers tooan un dossier externe dans votre fonction de sortie Hello Azure fichier externe.

les fichiers externes Hello de sortie pour une fonction utilise hello objets JSON Bonjour suivants `bindings` tableau de function.json :

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

Notez hello suivantes :

* `path`doit contenir le nom du dossier hello et toowrite de nom de fichier hello pour. Par exemple, si vous avez un [déclencheur de la file d’attente](functions-bindings-storage-queue.md) dans votre fonction, vous pouvez utiliser `"path": "samples-workitems/{queueTrigger}"` toopoint tooa fichier hello `samples-workitems` dossier avec un nom qui correspond au nom de fichier hello spécifié dans le message d’appel du déclencheur.   

<a name="outputusage"></a>

## <a name="output-usage"></a>Utilisation en sortie
Dans les fonctions C#, vous liez fichier de sortie toohello à l’aide de hello nommé `out` paramètre dans votre signature de fonction, comme `out <T> <name>`, où `T` est que les données de hello tooserialize, de type de données de hello et `paramName` est hello nom que vous avez spécifié dans le [liaison de sortie](#output). Dans les fonctions de Node.js, vous accédez à l’aide de fichiers de sortie hello `context.bindings.<name>`.

Vous pouvez écrire le fichier de sortie toohello à l’aide de hello les types suivants :

* N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour la sérialisation JSON.
  Si vous déclarez un type de sortie personnalisée (par exemple, `out OutputType paramName`), les fonctions Azure tente tooserialize objet dans JSON. Si le paramètre de sortie hello est null lorsque hello fonction s’arrête, hello fonctions runtime crée un fichier en tant qu’objet null.
* Chaîne : (`out string paramName`) utile pour les données de fichier texte. Hello fonctions runtime crée un fichier uniquement si le paramètre de chaîne est non null lorsque hello fonction s’arrête.

Dans les fonctions de c#, vous pouvez également copier tooany Hello les types suivants :

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a>Entrée + Exemple de sortie
Supposons que vous avez hello suivant function.json, qui définit un [déclencheur de file d’attente de stockage](functions-bindings-storage-queue.md), l’entrée d’un fichier externe et un fichier externe de sortie :

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

Voir exemple hello spécifiques au langage qui copie le fichier de sortie toohello hello fichier d’entrée.

* [C#](#incsharp)
* [Node.JS](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a>Utilisation en C# #

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

### <a name="usage-in-nodejs"></a>Utilisation en Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
