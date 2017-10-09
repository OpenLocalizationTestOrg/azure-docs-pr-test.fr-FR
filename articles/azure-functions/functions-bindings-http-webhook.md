---
title: les liaisons HTTP de fonctions et webhook aaaAzure | Documents Microsoft
description: "Comprendre comment toouse HTTP et webhook déclenche et les liaisons dans les fonctions d’Azure."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur, HTTP, API, REST"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a>Liaisons HTTP et webhook Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment tooconfigure et utiliser HTTP déclenche et les liaisons dans les fonctions d’Azure.
Avec ces options, vous pouvez utiliser les toowebhooks de toobuild de fonctions d’Azure sans serveur de répondre et API.

Les fonctions Azure fournit hello suivant des liaisons :
- Un [déclencheur HTTP](#httptrigger) vous permet d’appeler une fonction avec une requête HTTP. Cela peut être trop personnalisé toorespond[webhooks](#hooktrigger).
- Un [liaison de sortie HTTP](#output) vous permet de toorespond toohello demande.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a>Déclencheur HTTP
déclencheur HTTP Hello exécutera votre fonction dans la demande de réponse tooan HTTP. Vous pouvez le personnaliser URL de toorespond tooa particulière ou un ensemble de méthodes HTTP. Un déclencheur HTTP peut également être configuré toorespond toowebhooks. 

Si vous utilisez le portail de fonctions hello, vous pouvez également commencer immédiatement à l’aide d’un modèle existant. Sélectionnez **nouvelle fonction** et choisissez « Webhooks & de l’API » hello **scénario** liste déroulante. Sélectionnez un des modèles de hello et cliquez sur **créer**.

Par défaut, un déclencheur HTTP répondra demande toohello avec un code d’état HTTP 200 OK et un corps vide. toomodify hello réponse, configurez un [liaison de sortie HTTP](#output)

### <a name="configuring-an-http-trigger"></a>Configuration d’un déclencheur HTTP
Un déclencheur HTTP est défini en incluant un toohello similaire d’objet JSON suivant Bonjour `bindings` tableau de function.json :

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
liaison de Hello prend en charge hello propriétés suivantes :

* **nom** : requise : nom de la variable hello utilisée dans le code de fonction de requête de hello ou de corps de la demande. Voir [Utilisation d’un déclencheur HTTP à partir d’un code](#httptriggerusage).
* **type** : requise : doit être défini trop « httpTrigger ».
* **direction** : requise : doit être défini trop « in ».
* _authLevel_ : ce paramètre détermine les clés, le cas échéant, doivent toobe présent sur demande de hello dans la fonction d’ordre tooinvoke hello. Voir [Utilisation de clés](#keys) ci-dessous. valeur de Hello peut être hello suivantes :
    * _anonymous_ : aucune clé API n’est requise.
    * _function_ : une clé API spécifique de la fonction est requise. Cela est hello par défaut si aucun n’est fourni.
    * _administrateur_ : hello la clé principale est requise.
* **méthodes** : il s’agit d’un tableau de méthodes hello HTTP (fonction) hello toowhich répondra. Si non spécifié, fonction hello répondra tooall HTTP méthodes. Consultez [personnalisation de point de terminaison hello HTTP](#url).
* **itinéraire** : modèle d’itinéraire hello, contrôle toowhich définit votre fonction répondra des URL de la requête. Bonjour valeur par défaut si aucun n’est fourni est `<functionname>`. Consultez [personnalisation de point de terminaison hello HTTP](#url).
* **webHookType** : Cela configure tooact de déclencheur hello HTTP comme un récepteur de webhook pour le fournisseur spécifié de hello. Hello _méthodes_ propriété ne doit pas être définie si cela est choisi. Consultez [réponse toowebhooks](#hooktrigger). valeur de Hello peut être hello suivantes :
    * _genericJson_ : point de terminaison webhook à usage général sans logique pour un fournisseur spécifique.
    * _github_ : fonction hello répondra tooGitHub webhooks. Hello _authLevel_ propriété ne doit pas être définie si cela est choisi.
    * _marge_ : fonction hello répondra tooSlack webhooks. Hello _authLevel_ propriété ne doit pas être définie si cela est choisi.

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a>Utilisation d’un déclencheur HTTP à partir d’un code
Pour les fonctions de c# et F #, vous pouvez déclarer type hello de votre toobe d’entrée de déclencheur soit `HttpRequestMessage` ou un type personnalisé. Si vous choisissez `HttpRequestMessage`, vous obtiendrez un objet de demande toohello un accès complet. Pour un type personnalisé (par exemple, un POCO), les fonctions va tenter de corps de la demande tooparse hello en tant que propriétés de l’objet JSON toopopulate hello.

Pour les fonctions de Node.js hello fonctions runtime fournit des corps de la demande au lieu de l’objet de demande hello hello.

Pour des exemples d’utilisation, voir [Exemples de déclencheur HTTP](#httptriggersample).


<a name="output"></a>
## <a name="http-response-output-binding"></a>Liaison de sortie de réponse HTTP
Utilisez l’expéditeur de demande HTTP liaison toorespond toohello hello HTTP sortie. Cette liaison requiert un déclencheur HTTP et vous permet de réponse de hello toocustomize associée demande du déclencheur hello. Si aucune liaison de sortie HTTP n’est spécifiée, un déclencheur HTTP renvoie HTTP 200 OK avec un corps vide. 

### <a name="configuring-an-http-output-binding"></a>Configuration d’une liaison de sortie HTTP
Hello HTTP de la liaison est définie en incluant un toohello similaire d’objet JSON suivant Bonjour sortie `bindings` tableau de function.json :

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
liaison de Hello contient hello propriétés suivantes :

* **nom** : requise : hello nom de la variable utilisée dans le code de fonction pour la réponse de hello. Voir [Utilisation d’une liaison de sortie HTTP à partir d’un code](#outputusage).
* **type** : requise : doit être défini trop « http ».
* **direction** : requise : doit être défini trop « sortie ».

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a>Utilisation d’une liaison de sortie HTTP à partir d’un code
Vous pouvez utiliser hello sortie paramètre (par exemple, « res ») toorespond toohello http ou webhook appelant. Vous pouvez également utiliser la norme `Request.CreateResponse()` (c#) ou `context.res` (Node.JS) modèle tooreturn votre réponse. Pour des exemples qui illustrent comment toouse hello cette dernière méthode, consultez [exemples de déclencheur HTTP](#httptriggersample) et [exemples de déclencheurs de Webhook](#hooktriggersample).


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a>Répondre toowebhooks
Un déclencheur HTTP avec hello _webHookType_ propriété sera configuré toorespond trop[webhooks](https://en.wikipedia.org/wiki/Webhook). configuration de base Hello utilise le paramètre de « genericJson » hello. Ce qui réduit les demandes tooonly celles de l’utilisation de HTTP POST et hello `application/json` le type de contenu.

Hello déclencheur peut en outre être adaptés tooa webhook spécifique fournisseur (par exemple, [GitHub](https://developer.github.com/webhooks/) et [Slack](https://api.slack.com/outgoing-webhooks)). Si un fournisseur est spécifié, hello fonctions runtime peut prendre en charge la logique de validation du fournisseur hello pour vous.  

### <a name="configuring-github-as-a-webhook-provider"></a>Configurer GitHub en tant que fournisseur de webhooks
toorespond tooGitHub webhooks, commencez par créer votre fonction avec un déclencheur de HTTP et définir hello _webHookType_ propriété trop « github ». Ensuite, copiez son [URL](#url) et sa [clé API](#keys) vers la page **Ajouter un Webhook** de votre référentiel GitHub. Pour plus d’informations, voir la documentation [Création de webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409).

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a>Configuration de Slack en tant que fournisseur de webhook
webhook de marge Hello génère un jeton au lieu de ce qui vous permet de spécifier, vous devez donc configurer une clé spécifiques à une fonction avec jeton hello à partir de la marge. Voir [Utilisation de clés](#keys).

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a>Personnalisation de point de terminaison HTTP hello
Par défaut, lorsque vous créez une fonction d’un déclencheur HTTP, ou WebHook, fonction hello est adressable avec un itinéraire de formulaire de hello :

    http://<yourapp>.azurewebsites.net/api/<funcname> 

Vous pouvez personnaliser cet itinéraire à l’aide de hello facultatif `route` propriété sur le déclencheur de hello HTTP d’entrée de liaison. Par exemple, hello suivant *function.json* fichier définit un `route` propriétés d’un déclencheur HTTP :

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

À l’aide de cette configuration, fonction hello est maintenant adressable par hello suivant l’itinéraire au lieu de l’itinéraire d’origine de hello.

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

Cela permet au code de fonction hello toosupport deux des paramètres dans l’adresse de hello, « catégorie » et « id ». Vous pouvez utiliser les [contraintes d’itinéraire des API Web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) de votre choix avec vos paramètres. Hello suivant le code de fonction c# utilise les deux paramètres.

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

Voici les paramètres d’itinéraire même hello de toouse code Node.js (fonction).

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

Par défaut, tous les itinéraires de fonction sont préfixés par *api*. Vous pouvez également personnaliser ou supprimer le préfixe hello à l’aide de hello `http.routePrefix` propriété dans votre *host.json* fichier. exemple Hello supprime hello *api* préfixe d’itinéraire à l’aide d’une chaîne vide pour le préfixe hello Bonjour *host.json* fichier.

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

Pour plus d’informations sur la façon de tooupdate hello *host.json* fichier de votre fonction, consultez [fonctionnement des fichiers de l’application tooupdate](functions-reference.md#fileupdate). 

Pour plus d’informations sur les autres propriétés que vous pouvez configurer dans votre fichier *host.json*, consultez la [référence host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).


<a name="keys"></a>
## <a name="working-with-keys"></a>Utilisation de clés
HttpTriggers peut tirer parti des clés pour renforcer la sécurité. Un standard HttpTrigger pouvez les utiliser comme une clé d’API, nécessitant toobe de clé hello présent sur la demande de hello. Webhooks peut utiliser des clés tooauthorize demandes de plusieurs façons, selon le fournisseur hello prend en charge.

Les clés sont stockées dans votre Function App dans Azure, et chiffrées au repos. tooview vos clés, créer de nouveaux ou toonew les valeurs de clés de restauration, accédez tooone de vos fonctions au sein du portail de hello et sélectionnez « Gérer ». 

Il existe deux types de clés :
- **Clés d’hôtes**: ces clés sont partagés par toutes les fonctions de l’application de fonction hello. Lorsqu’il est utilisé comme une clé d’API, permettent de fonction tooany d’accès au sein de l’application de fonction hello.
- **Touches de fonction**: ces clés s’appliquent uniquement toohello des fonctions spécifiques dans lesquelles ils sont définis. Lorsqu’il est utilisé comme une clé d’API, ils ne permettre access toothat (fonction).

Chaque clé est nommé pour référence et il existe une clé par défaut (nommée « default ») au niveau de fonction et l’hôte hello. Hello **clé principale de** est une clé d’hôte par défaut nommée « _master » qui est défini pour chaque application de la fonction et ne peuvent pas être révoqués. Il fournit des API d’exécution d’un accès administratif toohello. À l’aide de `"authLevel": "admin"` Bonjour JSON de liaison requiert cette clé toobe présenté à la demande de hello ; une autre clé entraîne un échec d’autorisation.

> [!NOTE]
> Échéance toohello élevés des autorisations accordées par la clé principale de hello, vous ne devez pas partager cette clé avec des tiers ou le distribuer dans les applications clientes natives. Faites preuve de prudence lorsque vous choisissez le niveau d’autorisation d’admin hello.
> 
> 

### <a name="api-key-authorization"></a>Autorisation de clé API
Par défaut, un HttpTrigger requiert une clé d’API dans la demande HTTP hello. Par conséquent, votre requête HTTP ressemble normalement à ceci :

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

clé de Hello peut être inclus dans une variable de chaîne de requête nommée `code`, comme indiqué ci-dessus, ou il peut être inclus dans un `x-functions-key` en-tête HTTP. valeur de Hello de clé de hello peut être n’importe quelle touche de fonction définis pour la fonction de hello ou n’importe quelle touche de l’hôte.

Vous pouvez choisir des demandes tooallow sans clés ou spécifier que la clé principale hello doit être utilisée en modifiant les hello `authLevel` propriété Bonjour liaison JSON (voir [déclencheur HTTP](#httptrigger)).

### <a name="keys-and-webhooks"></a>Clés et webhooks
Autorisation de Webhook est gérée par le composant récepteur hello webhook, partie hello HttpTrigger et le mécanisme de hello varie selon le type de webhook hello. Toutefois, chaque mécanisme dépend d’une clé. Par défaut, touche de fonction hello nommée « default » est utilisée. Si vous le souhaitez toouse une autre clé, vous devez tooconfigure hello webhook fournisseur toosend hello nom de clé avec requête hello de hello suivant façons :

- **Chaîne de requête**: fournisseur de hello transmet le nom de la clé hello Bonjour `clientid` le paramètre de chaîne de requête (par exemple, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).
- **En-tête de demande**: fournisseur de hello transmet le nom de la clé hello Bonjour `x-functions-clientid` en-tête.

> [!NOTE]
> Les clés de fonction prennent le pas sur les clés d’hôte. Si deux clés sont définies avec le même nom, hello de hello touche de fonction sera utilisé.
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a>Exemples de déclencheur HTTP
Supposez que vous avez hello suivant déclencheur HTTP Bonjour `bindings` tableau de function.json :

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

Consultez l’exemple hello spécifiques à une langue qui recherche un `name` paramètre dans la chaîne de requête hello ou corps hello de demande de hello HTTP.

* [C#](#httptriggercsharp)
* [F#](#httptriggerfsharp)
* [Node.JS](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a>Exemple de déclencheur HTTP en C# #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

Vous pouvez également lier tooa POCO au lieu de `HttpRequestMessage`. Cela sera être intégré à partir du corps hello de demande hello, analysée au format JSON. De même, un type peut être passé en sortie de réponse HTTP de toohello de liaison, et cela sera retourné en tant que corps de réponse hello, avec un code de 200 état.
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a>Exemple de déclencheur HTTP en F# #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

Vous avez besoin une `project.json` fichier qui utilise NuGet tooreference hello `FSharp.Interop.Dynamic` et `Dynamitey` assemblys, comme suit :

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

Cette option NuGet toofetch les dépendances et les référencer dans votre script.

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a>Exemple de déclencheur HTTP en Node.js
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a>Exemples de webhook
Supposez que vous avez hello suivant déclencheur webhook Bonjour `bindings` tableau de function.json :

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

Voir exemple hello spécifiques au langage qui enregistre les commentaires de problème GitHub.

* [C#](#hooktriggercsharp)
* [F#](#hooktriggerfsharp)
* [Node.JS](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a>Exemple de Webhook en C# #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a>Exemple de Webhook en F# #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a>Exemple de webhook en Node.js
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

