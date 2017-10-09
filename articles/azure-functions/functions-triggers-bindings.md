---
title: "aaaWork avec des déclencheurs et des liaisons dans les fonctions de Azure | Documents Microsoft"
description: "Découvrez comment toouse déclenche et les liaisons dans les fonctions Azure tooconnect vos événements de tooonline de l’exécution de code et les services basés sur le cloud."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a>Concepts des déclencheurs et liaisons Azure Functions
Les fonctions Azure vous permet au code de toowrite de tooevents de réponse dans Azure et d’autres services via *déclencheurs* et *liaisons*. Cet article est une vue d’ensemble conceptuelle des déclencheurs et pour tous les langages de programmation pris en charge. Fonctionnalités des liaisons tooall courantes sont décrites ici.

## <a name="overview"></a>Vue d'ensemble

Les déclencheurs et les liaisons sont un toodefine de façon déclarative comment une fonction est appelée et les données qu’il fonctionne avec. Un *déclencheur* définit la façon dont une fonction est appelée. Une fonction ne doit avoir qu’un seul déclencheur. Les déclencheurs ont des données, qui est généralement hello charge utile qui a déclenché la fonction hello associées. 

Entrée et sortie *liaisons* fournissent un toodata tooconnect de façon déclarative à partir de votre code. Tootriggers similaires, vous spécifiez les chaînes de connexion et d’autres propriétés dans votre configuration de la fonction. Les liaisons sont facultatives et une fonction peut avoir plusieurs liaisons d’entrée et de sortie. 

À l’aide de déclencheurs et des liaisons, vous pouvez écrire du code qui est plus générique et ne pas coder en dur hello détails des services hello avec lequel elle interagit. Les données provenant deq services deviennent simplement des valeurs d’entrée pour votre code de fonction. service de tooanother toooutput données (par exemple, créez une nouvelle ligne dans le stockage Table Azure), utilisez la valeur de retour de hello de méthode hello. Ou, si vous devez toooutput plusieurs valeurs, utilisez un objet d’assistance. Les déclencheurs et les liaisons ont un **nom** propriété, qui est un identificateur que vous utilisez dans votre liaison de hello tooaccess code.

Vous pouvez configurer des déclencheurs et des liaisons dans hello **intégrer** portail de fonctions d’Azure hello. Dans les coulisses hello, hello l’interface utilisateur modifie un fichier appelé *function.json* fichier dans le répertoire de fonction hello. Vous pouvez modifier ce fichier en modifiant toohello **éditeur avancé**.

Hello tableau suivant présente les déclencheurs hello et des liaisons qui sont pris en charge avec les fonctions d’Azure. 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a>Exemple : déclencheur de file d’attente et liaison de sortie de table

Supposons que vous toowrite une nouvelle tooAzure de ligne le stockage de Table chaque fois qu’un nouveau message s’affiche dans le stockage de file d’attente Azure. Ce scénario peut être implémenté à l’aide d’un déclencheur File d’attente Azure et d’une liaison de sortie Table. 

Un déclencheur de la file d’attente nécessite hello informations Bonjour suivantes **intégrer** onglet :

* nom de Hello du paramètre d’application hello qui contient la chaîne de connexion de compte de stockage hello pour la file d’attente hello
* nom de file d’attente Hello
* Hello identificateur dans votre code tooread hello du contenu d’hello file d’attente message, tel que `order`.

toowrite tooAzure le stockage de Table, utilisez une liaison de sortie avec hello les détails suivants :

* nom de Hello du paramètre d’application hello qui contient la chaîne de connexion de compte de stockage hello pour la table de hello
* nom de la table Hello
* Identificateur Hello dans votre toocreate de code de sortie des éléments, ou valeur de retour de hello à partir de la fonction hello.

Liaisons utilisent les paramètres de l’application pour hello tooenforce à des chaînes de connexion meilleures pratiques qui *function.json* ne contient pas de clés secrètes de service.

Ensuite, utilisez les identificateurs hello vous avez fourni toointegrate avec le stockage Azure dans votre code.

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

Voici hello *function.json* toohello précédant le code correspondant. Notez que hello même configuration peut être utilisée, quel que soit le langage hello d’implémentation de la fonction hello.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
contenu de hello tooview et modification de *function.json* Bonjour portail Azure, cliquez sur hello **éditeur avancé** option hello **intégrer** onglet de votre fonction.

Pour plus d’exemples de code et de détails sur l’intégration avec Stockage Azure, consultez [Déclencheurs et liaisons Azure Functions pour Stockage Azure](functions-bindings-storage.md).

### <a name="binding-direction"></a>Sens de la liaison

Tous les déclencheurs et liaisons ont une propriété `direction` :

- Pour les déclencheurs, direction de hello est toujours`in`
- Les liaisons d’entrée et de sortie utilisent `in` et `out`
- Certaines liaisons prennent en charge un sens spécial `inout`. Si vous utilisez `inout`, hello uniquement **éditeur avancé** est disponible dans hello **intégrer** onglet.

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a>À l’aide de tooreturn de type de retour de fonction hello une sortie unique

Hello exemple précédent indique comment tooprovide de valeur de retour de fonction de hello toouse sortie tooa liaison, qui est obtenue à l’aide du paramètre de nom spécial hello `$return`. (Cela n’est pris en charge que dans les langages qui ont une valeur de retour, tels que C#, JavaScript et F#.) Si une fonction comporte plusieurs liaisons de sortie, utilisez `$return` pour un seul hello de liaisons de sortie. 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

exemples de Hello ci-dessous montrent comment retournent les types sont utilisés avec les liaisons de sortie en c#, JavaScript et F #.

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a>Liaison de propriété Datatype

Dans .NET, utilisez le type de données hello types toodefine hello pour les données d’entrée. Par exemple, utilisez `string` toobind toohello texte un déclencheur de la file d’attente et un tooread de tableau d’octets binaire.

Pour les langues qui sont typées dynamiquement tels que JavaScript, utilisez hello `dataType` propriété dans la définition de la liaison hello. Par exemple, tooread hello contenu d’une requête HTTP au format binaire, utilisez le type de hello `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Les autres options pour `dataType` sont `stream` et `string`.

## <a name="resolving-app-settings"></a>Résolution des paramètres de l’application
En tant que meilleure pratique, les chaînes de connexion et les secrets doivent être gérés avec des paramètres de l’application, plutôt qu’avec des fichiers de configuration. Cela limite l’accès toothese secrets et le rend safe toostore *function.json* dans un référentiel de contrôle source publique.

Paramètres de l’application sont également utiles quand vous le souhaitez configuration toochange basée sur l’environnement de hello. Par exemple, dans un environnement de test, vous souhaiterez toomonitor un conteneur de stockage différent de file d’attente ou un objet blob.

Les paramètres de l’application sont résolus à chaque fois qu’une valeur est placée entre des signes de pourcentage, comme `%MyAppSetting%`. Notez que hello `connection` est un cas spécial de propriété des déclencheurs et des liaisons et résout automatiquement les valeurs en tant que paramètres de l’application. 

exemple Hello est un déclencheur de file d’attente qui utilise un paramètre d’application `%input-queue-name%` tootrigger de file d’attente toodefine hello sur.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a>Propriétés de métadonnées de déclencheur

Dans Ajout toohello charge utile de données fourni par un déclencheur (par exemple, la file d’attente message de salutation qui a déclenché une fonction), les déclencheurs de fournir des valeurs de métadonnées supplémentaires. Ces valeurs peuvent être utilisées comme paramètres d’entrée dans c# et F # ou propriétés hello `context.bindings` objet dans JavaScript. 

Par exemple, un déclencheur de la file d’attente prend en charge hello propriétés suivantes :

* QueueTrigger - déclenchant le contenu du message si une chaîne valide
* DequeueCount
* ExpirationTime
* ID
* InsertionTime
* NextVisibleTime
* PopReceipt

Détails des propriétés de métadonnées pour chaque déclencheur sont décrits dans la rubrique de référence correspondante hello. Documentation est également disponible dans hello **intégrer** onglet du portail hello, Bonjour **Documentation** section sous la zone de configuration de liaison hello.  

Par exemple, étant donné que les déclencheurs de l’objet blob ont des retards, vous pouvez utiliser un toorun de déclencheur de file d’attente votre fonction (consultez [déclencheur du stockage Blob](functions-bindings-storage-blob.md#storage-blob-trigger). message de file d’attente Hello contiendrait tootrigger de nom de fichier blob hello sur. À l’aide de hello `queueTrigger` propriété de métadonnées, vous pouvez définir ce comportement dans votre configuration, plutôt que dans votre code.

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

Les propriétés de métadonnées à partir d’un déclencheur peuvent également être utilisées dans un *expression de liaison* pour une autre liaison, comme décrit dans hello suivant la section.

## <a name="binding-expressions-and-patterns"></a>Modèles et expressions de liaison

Une des fonctionnalités plus puissantes de hello des déclencheurs et des liaisons *liaison d’expressions*. Au sein de votre liaison, vous pouvez définir des modèles d’expression qui peuvent ensuite être utilisés dans d’autres liaisons ou votre code. Métadonnées de déclencheur peuvent également servir de liaison d’expressions, comme indiqué dans l’exemple hello Bonjour précédant la section.

Par exemple, supposons que vous souhaitiez tooresize des images dans le conteneur de stockage blob particulier, similaire toohello **taille de l’Image** modèle Bonjour **nouvelle fonction** page. Accédez trop**nouvelle fonction** -> langue **c#** -> scénario **exemples** -> **ImageResizer-CSharp**. 

Voici hello *function.json* définition :

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

Notez que hello `filename` paramètre est utilisé dans la définition du déclencheur hello blob ainsi que des objets blob de hello liaison de sortie. Ce paramètre peut également être utilisé dans le code de fonction.

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a>GUID aléatoires
Fonctions Azure fournit une syntaxe plus de commodité pour générer des GUID dans vos liaisons, par le biais hello `{rand-guid}` expression de liaison. Hello exemple suivant utilise cette toogenerate un nom d’objet blob unique : 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a>Heure actuelle

Vous pouvez utiliser d’expression de liaison hello `DateTime`, ce qui donne trop`DateTime.UtcNow`.

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a>Lier les propriétés d’entrée de toocustom dans une expression de liaison

Expressions de liaison peuvent également référencer des propriétés qui sont définies dans la charge utile de déclencheur hello lui-même. Par exemple, vous voudrez fichier de stockage des objets blob toodynamically bind tooa à partir d’un nom de fichier fourni dans un webhook.

Par exemple, hello suivant *function.json* utilise une propriété appelée `BlobName` à partir de la charge utile de déclencheur hello :

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

tooaccomplish cette dans c# et F #, vous devez définir un POCO qui définit les champs hello qui seront désérialisés dans la charge utile de déclencheur hello.

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

Dans JavaScript, la désérialisation JSON est effectuée automatiquement et vous pouvez utiliser directement les propriétés hello.

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a>Configuration de la liaison des données lors de l’exécution

En c# et d’autres langages .NET, vous pouvez utiliser un modèle de liaison impérative, que les liaisons de déclarative toohello exécutée dans *function.json*. Liaison impératif est utile lorsque les paramètres de liaison doivent toobe calculée au moment de l’exécution au lieu de conception. toolearn, voir [liaison lors de l’exécution via les liaisons impératifs](functions-reference-csharp.md#imperative-bindings) dans la référence du développeur hello c#.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur une liaison spécifique, consultez hello suivant des articles :

- [HTTP et webhooks](functions-bindings-http-webhook.md)
- [Minuteur](functions-bindings-timer.md)
- [Stockage de files d’attente](functions-bindings-storage-queue.md)
- [Stockage d’objets blob](functions-bindings-storage-blob.md)
- [Stockage Table](functions-bindings-storage-table.md)
- [Concentrateur d’événements](functions-bindings-event-hubs.md)
- [Service Bus](functions-bindings-service-bus.md)
- [Cosmos DB](functions-bindings-documentdb.md)
- [SendGrid](functions-bindings-sendgrid.md)
- [Twilio](functions-bindings-twilio.md)
- [Notification Hubs](functions-bindings-notification-hubs.md)
- [Mobile Apps](functions-bindings-mobile-apps.md)
- [Fichier externe](functions-bindings-external-file.md)
