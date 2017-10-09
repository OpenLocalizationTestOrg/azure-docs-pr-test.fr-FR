---
title: "liaisons de stockage d’objets Blob fonctions aaaAzure | Documents Microsoft"
description: "Comprendre comment toouse le stockage Azure déclenche et les liaisons dans les fonctions d’Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a>Liaisons de stockage Blob Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment tooconfigure et fonctionnent avec les liaisons de stockage d’objets Blob Azure dans les fonctions d’Azure. Azure Functions prend en charge les liaisons de déclencheur, d’entrée et de sortie pour Stockage Blob Azure. Pour les fonctionnalités qui sont disponibles dans toutes les liaisons, consultez [Concepts des déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> Un [compte de stockage pour objet blob uniquement](../storage/common/storage-create-storage-account.md#blob-storage-accounts) n’est pas pris en charge. Les déclencheurs et les liaisons de stockage blob nécessitent un compte de stockage à usage général. 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a>Déclencheurs et liaisons de stockage blob

À l’aide de déclencheur de stockage d’objets Blob Azure hello, votre code de fonction est appelée lorsqu’un objet blob nouveau ou mis à jour est détecté. contenu d’objet blob Hello est fournies en tant que fonction de toohello d’entrée.

Définir un déclencheur de stockage d’objets blob à l’aide de hello **intégrer** portail de fonctions hello. portail Hello crée hello définition Bonjour **liaisons** section de *function.json*:

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

Objet BLOB d’entrée et les liaisons de sortie sont définies à l’aide de `blob` en tant que type de liaison hello :

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* Hello `path` propriété prend en charge la liaison d’expressions et des paramètres de filtre. Consultez [Modèles de nom](#pattern).
* Hello `connection` propriété doit contenir le nom hello d’un paramètre d’application qui contient une chaîne de connexion de stockage. Bonjour portail Azure, hello éditeur standard Bonjour **intégrer** onglet configure ce paramètre d’application pour vous lorsque vous sélectionnez un compte de stockage.

> [!NOTE]
> Lorsque vous utilisez un déclencheur d’objets blob sur un plan de la consommation, il peut être délai de 10 minutes tooa dans le traitement de nouveaux objets BLOB après qu’une application de la fonction est devenu inactive. Après que application de fonction hello est en cours d’exécution, les objets BLOB est traitées immédiatement. tooavoid initiale de ce délai, envisagez l’une des options suivantes de hello :
> - Utilisez un plan App Service avec le paramètre Toujours actif activé.
> - Utiliser un autre mécanisme tootrigger hello objet blob de traitement, par exemple un message de la file d’attente qui contient le nom d’objet blob hello. Pour un exemple, consultez [Déclencheur de file d’attente avec liaison d’entrée d’objet blob](#input-sample).

<a name="pattern"></a>

### <a name="name-patterns"></a>Modèles de nom
Vous pouvez spécifier un modèle de nom d’objet blob dans hello `path` propriété, qui peut être une expression de filtre ou de la liaison. Consultez [Expressions et modèles de liaison](functions-triggers-bindings.md#binding-expressions-and-patterns).

Par exemple, tooblobs toofilter qui commencent par la chaîne hello d’origine », » utiliser hello définition. Ce chemin de recherche d’un objet blob nommé *d’origine-Blob1.txt* Bonjour *d’entrée* conteneur et la valeur de hello de hello `name` la variable dans le code de fonction est `Blob1`.

```json
"path": "input/original-{name}",
```

extension et nom de fichier blob toobind toohello séparément, utilisent deux modèles. Ce chemin de recherche également un objet blob nommé *d’origine-Blob1.txt*et la valeur hello Hello `blobname` et `blobextension` sont des variables dans le code de fonction *d’origine-Blob1* et *txt*.

```json
"path": "input/{blobname}.{blobextension}",
```

Vous pouvez limiter le type de fichier hello d’objets BLOB à l’aide d’une valeur fixe pour l’extension de fichier hello. Par exemple, tootrigger uniquement sur les fichiers .png, hello utilisez modèle :

```json
"path": "samples/{name}.png",
```

Les accolades sont des caractères spéciaux dans les modèles de nom. toospecify les noms d’objet blob qui ont des accolades dans le nom de hello, d’échappement des accolades hello à l’aide de deux accolades. exemple Hello recherche un objet blob nommé *{20140101}-soundfile.mp3* Bonjour *images* conteneur et hello `name` est de valeur de la variable dans le code de la fonction hello  *soundfile.MP3*. 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a>Métadonnées d’un déclencheur

déclencheur de blob Hello fournit plusieurs propriétés de métadonnées. Ces propriétés peuvent être utilisées dans des expressions de liaison dans d’autres liaisons ou en tant que paramètres dans votre code. Ces valeurs ont hello même sémantique que [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).

- **BlobTrigger**. Saisissez `string`. chemin d’accès de blob déclenchement Hello
- **Uri**. Saisissez `System.Uri`. URI de l’objet blob de Hello pour l’emplacement principal de hello.
- **Properties**. Saisissez `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`. Bonjour les propriétés de système de l’objet blob.
- **Metadata**. Saisissez `IDictionary<string,string>`. métadonnées définies par l’utilisateur Hello pour l’objet blob de hello.

<a name="receipts"></a>

### <a name="blob-receipts"></a>Reçus d’objets blob
Fonctions d’Azure Hello runtime garantit qu’aucune fonction de déclenchement d’objet blob n’est appelée plusieurs fois pour hello même objet blob de nouveau ou mis à jour. toodetermine si une version de l’objet blob donné a été traitée, il gère *accusés de réception d’objets blob*.

Magasins de fonctions Azure blob accusés de réception dans un conteneur nommé *hôtes de tâches Web azure* Bonjour compte de stockage Azure pour votre application (fonction) (défini par le paramètre d’application hello `AzureWebJobsStorage`). Un accusé de réception d’objet blob a hello informations suivantes :

* Hello déclenchée (fonction) («*&lt;nom de l’application fonction >*. Fonctions.  *&lt;nom de la fonction >*», par exemple : « MyFunctionApp.Functions.CopyBlob »)
* nom du conteneur Hello
* type d’objet blob Hello (« BlockBlob » ou « Un PageBlob »)
* nom d’objet blob Hello
* Hello ETag (un identificateur de version des objets blob, par exemple : « 0x8D1DC6E70A277EF »)

tooforce retraitement d’un objet blob, supprimez réception de blob hello pour cet objet blob hello *hôtes de tâches Web azure* conteneur manuellement.

<a name="poison"></a>

### <a name="handling-poison-blobs"></a>Gestion des objets blob incohérents
En cas d’échec d’une fonction de déclencheur d’objet blob, Azure Functions réessaie cette fonction jusqu’à 5 fois par défaut. 

Si toutes les 5 tentatives échouent, les fonctions Azure ajoute un message tooa stockage file d’attente nommée *webjobs-blobtrigger-incohérents*. message de file d’attente Hello pour les objets BLOB incohérent est un objet JSON qui contient les propriétés suivantes de hello :

* ID de fonction (au format de hello  *&lt;nom de l’application fonction >*. Fonctions.  *&lt;nom de la fonction >*)
* BlobType (« BlockBlob » ou « PageBlob »)
* ContainerName
* BlobName
* ETag (identificateur de version de l’objet blob, par exemple : « 0x8D1DC6E70A277EF »)

### <a name="blob-polling-for-large-containers"></a>Interrogation de blob pour les grands conteneurs
Si le conteneur d’objets blob hello en cours d’analyse contient plus de 10 000 objets BLOB, les fonctions hello runtime analyse journal toowatch de fichiers pour les objets BLOB nouveau ou modifié. Ce processus ne se déroule pas en temps réel. Une fonction ne peut-être pas déclenchée jusqu'à ce que quelques minutes ou plus après que l’objet blob de hello est créé. En outre, les [journaux de stockage sont créés selon le principe du meilleur effort](/rest/api/storageservices/About-Storage-Analytics-Logging). Il n’existe aucune garantie que tous les événements sont capturés. Dans certaines conditions, des journaux peuvent être omis. Si vous avez besoin de traitement de l’objet blob plus rapide ou plus fiable, envisagez de créer un [message de la file d’attente](../storage/queues/storage-dotnet-how-to-use-queues.md) lorsque vous créez l’objet blob de hello. Ensuite, utilisez un [déclencheur de la file d’attente](functions-bindings-storage-queue.md) au lieu d’un objet blob déclencheur tooprocess hello objet blob.

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a>Utilisation d’un déclencheur d’objets blob et d’une liaison d’entrée
Dans des fonctions .NET, accéder aux données d’objet blob de hello à l’aide d’un paramètre de méthode comme `Stream paramName`. Ici, `paramName` est la valeur hello spécifiée Bonjour [configuration du déclencheur](#trigger). Dans les fonctions de Node.js, hello d’accès d’entrée à l’aide des données blob `context.bindings.<name>`.

Dans .NET, vous pouvez lier tooany des types de hello dans la liste hello ci-dessous. S’ils sont utilisés comme liaison d’entrée, certains de ces types nécessitent une direction de liaison `inout` dans *function.json*. Cette direction n’est pas pris en charge par l’éditeur standard hello, vous devez donc utiliser hello éditeur avancé.

* `TextReader`
* `Stream`
* `ICloudBlob` (nécessite la direction de liaison « inout »)
* `CloudBlockBlob` (nécessite la direction de liaison « inout »)
* `CloudPageBlob` (nécessite la direction de liaison « inout »)
* `CloudAppendBlob` (nécessite la direction de liaison « inout »)

Si vous prévoyez des objets BLOB de texte, vous pouvez également lier tooa .NET `string` type. Ceci est recommandé uniquement si la taille des objets blob hello est petite, comme le contenu d’objet blob entier hello est chargés en mémoire. En règle générale, il est préférable de toouse un `Stream` ou `CloudBlockBlob` type.

## <a name="trigger-sample"></a>Exemple de déclencheur
Supposons que vous avez hello suivant function.json qui définit un déclencheur de stockage d’objets blob :

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

Voir exemple hello spécifiques au langage qui enregistre le contenu de hello de chaque objet blob qui est ajouté conteneur analysé de toohello.

* [C#](#triggercsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a>Exemples de déclencheur d’objet blob en C# #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a>Exemple de déclencheur en Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a>Utilisation d’une liaison de sortie d’objet blob

Dans les fonctions de .NET, vous devez utiliser un `out string` paramètre dans votre signature de fonction ou l’un des types hello Bonjour suivant liste. Dans les fonctions de Node.js, vous accédez à l’aide des objets blob de sortie hello `context.bindings.<name>`.

Dans les fonctions de .NET, vous pouvez produire tooany Hello les types suivants :

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a>Exemple de déclencheur de file d’attente avec une entrée et une sortie d’objet blob
Supposons que vous avez hello suivant function.json, qui définit un [déclencheur de stockage de la file d’attente](functions-bindings-storage-queue.md), un stockage d’objets blob d’entrée et un stockage d’objets blob de sortie. Utilisation de hello avis de hello `queueTrigger` propriété de métadonnées. dans l’objet blob de hello d’entrée et sortie `path` propriétés :

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
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

Voir exemple hello spécifiques au langage qui copie hello blob d’entrée toohello sortie blob.

* [C#](#incsharp)
* [Node.JS](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a>Exemple de liaison d’objet blob en C# #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a>Exemple de liaison d’objet blob en Node.js

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

