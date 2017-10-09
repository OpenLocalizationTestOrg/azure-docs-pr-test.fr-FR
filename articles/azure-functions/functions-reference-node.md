---
title: "référence du développeur pour les fonctions Azure aaaJavaScript | Documents Microsoft"
description: "Comprendre le fonctionnement de toodevelop à l’aide de JavaScript."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a>Guide des développeurs JavaScript sur Azure Functions
> [!div class="op_single_selector"]
> * [Script C#](functions-reference-csharp.md)
> * [Script F#](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

Hello JavaScript expérience pour les fonctions Azure rend facile tooexport une fonction qui est passée comme un `context` objet permettant de communiquer avec le runtime de hello et pour recevoir et envoyer des données via les liaisons.

Cet article suppose que vous avez déjà lu hello [référence du développeur Azure fonctions](functions-reference.md).

## <a name="exporting-a-function"></a>Exporter une fonction
Toutes les fonctions JavaScript doivent exporter un seul `function` via `module.exports` pour hello runtime toofind hello fonction et l’exécuter. Cette fonction doit toujours inclure un objet `context` .

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

Liaisons de `direction === "in"` sont passés comme arguments de fonction, ce qui signifie que vous pouvez utiliser [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically gérer de nouvelles entrées (par exemple, à l’aide de `arguments.length` tooiterate sur toutes vos entrées). Cette fonctionnalité est pratique si vous ne disposez que d’un déclencheur sans entrée supplémentaire, dans la mesure où vous pouvez accéder de manière prévisible aux données de votre déclencheur sans faire référence à votre objet `context`.

arguments de Hello sont toujours passées le long de la fonction toohello dans l’ordre de hello dans lequel ils apparaissent dans *function.json*, même si vous ne les spécifiez dans votre instruction d’exportations. Par exemple, si vous avez `function(context, a, b)` et modifiez-le trop`function(context, a)`, vous pouvez toujours obtenir les valeur hello `b` dans le code de fonction en vous reportant trop`arguments[3]`.

Toutes les liaisons, quelle que soit la direction, sont également transmis sur hello `context` (voir hello script suivant) de l’objet. 

## <a name="context-object"></a>Objet de contexte
Hello runtime utilise un `context` objet toopass données tooand à partir de votre fonction et le toolet vous communiquez avec le runtime de hello.

Hello objet de contexte est toujours première fonction de tooa paramètre hello et doit être inclus, car il possède des méthodes telles que `context.done` et `context.log`, qui sont requis toouse hello runtime correctement. Vous pouvez nommer les objets hello ce que vous voulez (par exemple, `ctx` ou `c`).

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a>Propriété context.bindings

```
context.bindings
```
Retourne un objet nommé qui contient toutes vos données d’entrée et de sortie. Par exemple, hello après la définition de la liaison dans votre *function.json* permet d’accéder à hello le contenu de la file d’attente de hello de hello `context.bindings.myInput` objet. 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a>Méthode context.done
```
context.done([err],[propertyBag])
```

Informe le runtime hello que votre code est terminée. Vous devez appeler `context.done`, ou autre hello runtime jamais sait que votre fonction est terminée et l’exécution de hello va expirer. 

Hello `context.done` méthode permet de vous toopass sauvegarder un runtime de toohello d’erreur définis par l’utilisateur et un sac de propriétés qui remplacent les propriétés de hello sur hello `context.bindings` objet.

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a>Méthode context.log  

```
context.log(message)
```
Vous permet de toowrite toohello diffusion en continu journaux de la console au niveau de trace par défaut hello. Sur `context.log`, d’autres méthodes de journalisation qui vous permettre d’écrire le journal de la console toohello à d’autres niveaux de trace :


| Méthode                 | Description                                |
| ---------------------- | ------------------------------------------ |
| **error(_message_)**   | Écrit tooerror au niveau de journalisation, ou inférieure.   |
| **warn(_message_)**    | Écrit toowarning au niveau de journalisation, ou inférieure. |
| **info(_message_)**    | Écrit tooinfo au niveau de journalisation, ou inférieure.    |
| **verbose(_message_)** | Écrit la journalisation au niveau du tooverbose.           |

Hello exemple suivant écrit console toohello au niveau de trace d’avertissement hello :

```javascript
context.log.warn("Something has happened."); 
```
Vous pouvez définir le seuil de niveau de trace hello pour l’enregistrement dans le fichier de host.json hello ou mettez-le hors tension.  Pour plus d’informations sur le fonctionnement des journaux toowrite toohello, consultez la section de suivante de hello.

## <a name="binding-data-type"></a>Type de données d’une liaison

toodefine type de données de hello pour une liaison d’entrée, utilisez hello `dataType` propriété dans la définition de la liaison hello. Par exemple, tooread hello contenu d’une requête HTTP au format binaire, utilisez le type de hello `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Les autres options pour `dataType` sont `stream` et `string`.

## <a name="writing-trace-output-toohello-console"></a>Console de toohello de sortie de trace en écriture 

Dans les fonctions, vous utilisez hello `context.log` console toohello de méthodes toowrite trace sortie. À ce stade, vous ne pouvez pas utiliser `console.log` toowrite toohello console.

Lorsque vous appelez `context.log()`, votre message est écrit console toohello au niveau de trace par défaut de hello, qui est hello _info_ niveau de suivi. Hello de code suivant écrit console toohello au niveau de trace hello info :

```javascript
context.log({hello: 'world'});  
```

Bonjour code précédent est équivalent toohello suivant de code :

```javascript
context.log.info({hello: 'world'});  
```

Hello de code suivant écrit console toohello au niveau d’erreur hello :

```javascript
context.log.error("An error has occurred.");  
```

Étant donné que _erreur_ est hello de trace la plus élevée au niveau, cette trace est écrite sortie toohello à tous les niveaux de trace tant que la journalisation est activée.  


Tous les `context.log` méthodes prennent en charge hello même format de paramètre est pris en charge par hello Node.js [util.format méthode](https://nodejs.org/api/util.html#util_util_format_format). Tenez compte des hello suivant de code, qui écrit toohello console à l’aide du niveau de trace par défaut hello :

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

Vous pouvez également hello écriture même code Bonjour suivant le format :

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a>Configurer le niveau de trace hello pour la journalisation de console

Fonctions vous permet de définir le niveau de trace hello seuil pour l’écriture de console toohello, ce qui rend la façon de hello toocontrol facilement les traces sont écrites toohello console à partir de vos fonctions. seuil de hello tooset pour toutes les traces écrites toohello console, utilisez hello `tracing.consoleLevel` propriété dans le fichier de host.json hello. Ce paramètre s’applique à des fonctions de tooall dans votre application de la fonction. Hello exemple suivant définit la journalisation documentée hello trace seuil tooenable :

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

Les valeurs de **consoleLevel** correspondent toohello les noms de hello `context.log` méthodes. le jeu de la trace de toutes les journalisation toohello console, toodisable **consoleLevel** too_off_. Pour plus d’informations sur le fichier de host.json hello, consultez hello [rubrique de référence host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

## <a name="http-triggers-and-bindings"></a>Déclencheurs et liaisons HTTP

De sortie HTTP et les déclencheurs de webhook et HTTP liaisons utilisent la demande et messages de réponse objets toorepresent hello HTTP.  

### <a name="request-object"></a>Objet Requête

Hello `request` objet a hello propriétés suivantes :

| Propriété      | Description                                                    |
| ------------- | -------------------------------------------------------------- |
| _body_        | Objet qui contient le corps hello de demande de hello.               |
| _headers_     | Objet qui contient les en-têtes de demande hello.                   |
| _method_      | Bonjour la méthode HTTP de la demande de hello.                                |
| _originalUrl_ | Hello l’URL de demande de hello.                                        |
| _params_      | Objet qui contient les paramètres de routage hello de demande de hello. |
| _query_       | Objet qui contient des paramètres de requête hello.                  |
| _rawBody_     | corps de Hello du message de type hello en tant que chaîne.                           |


### <a name="response-object"></a>Objet Réponse

Hello `response` objet a hello propriétés suivantes :

| Propriété  | Description                                               |
| --------- | --------------------------------------------------------- |
| _body_    | Objet qui contient le corps de réponse de hello de hello.         |
| _headers_ | Objet qui contient les en-têtes de réponse hello.             |
| _isRaw_   | Indique que la mise en forme est ignorée pour la réponse de hello.    |
| _statut_  | code d’état HTTP de la réponse de hello de Hello.                     |

### <a name="accessing-hello-request-and-response"></a>L’accès à la demande de hello et de réponse 

Lorsque vous travaillez avec des déclencheurs HTTP, vous pouvez accéder aux objets de demande et de réponse HTTP dans une des trois manières hello :

+ Hello nommé d’entrée et de sortie des liaisons. De cette façon, le déclencheur HTTP hello et liaisons fonctionnent hello même comme toute autre liaison. Hello exemple suivant définit l’objet de réponse hello aide portant un nom `response` liaison : 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ À partir de `req` et `res` propriétés hello `context` objet. De cette façon, vous pouvez utiliser les données de tooaccess HTTP de modèle classique de hello à partir de l’objet de contexte hello, au lieu d’avoir hello toouse complète `context.bindings.name` modèle. Hello suivant montre l’exemple de comment tooaccess hello `req` et `res` objets hello `context`:

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ En appelant `context.done()`. Un type spécial de liaison HTTP renvoie la réponse hello passé toohello `context.done()` (méthode). Hello suivant HTTP sortie liaison définit un `$return` paramètre de sortie :

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    Cette liaison de sortie attend réponse de hello toosupply lorsque vous appelez `done()`, comme suit :

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a>Version du nœud et gestion des packages
version du nœud Hello est actuellement verrouillée à `6.5.0`. Nous examinons la prise en charge d’autres versions ainsi que le fait de la rendre configurable.

Hello suit vous permettre d’inclure des packages dans votre application de fonction : 

1. Accédez trop`https://<function_app_name>.scm.azurewebsites.net`.

2. Cliquez sur **Console de débogage** > **CMD**.

3. Accédez trop`D:\home\site\wwwroot`, puis faites glisser votre toohello de fichier package.json **wwwroot** dossier au niveau de la partie supérieure de la page de hello hello.  
    Vous pouvez télécharger les fichiers tooyour fonction application autrement également. Pour plus d’informations, consultez [fonctionnement des fichiers de l’application tooupdate](functions-reference.md#fileupdate). 

4. Une fois hello package.json fichier est chargé, exécutez hello `npm install` commande hello **console de l’exécution à distance Kudu**.  
    Cette action télécharge les packages hello indiqués dans le fichier de package.json hello et redémarre l’application de fonction hello.

Une fois hello packages dont vous avez besoin sont installés, vous importez les tooyour fonction en appelant `require('packagename')`, comme dans hello l’exemple suivant :

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

Vous devez définir un `package.json` fichier à votre application de la fonction hello racine. Fichier de définition hello permet à toutes les fonctions de partage d’application hello hello mêmes packages mis en cache, ce qui donne de meilleurs hello. Si un conflit de version, vous pouvez le résoudre en ajoutant un `package.json` fichier dans le dossier hello d’une fonction spécifique.  

## <a name="environment-variables"></a>Variables d’environnement
tooget une variable d’environnement ou une valeur de paramètre d’application, utilisez `process.env`, comme indiqué dans l’exemple de code suivant de hello :

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a>Considérations relatives aux fonctions JavaScript

Lorsque vous travaillez avec les fonctions JavaScript, tenez compte des considérations hello Bonjour les deux sections suivantes.

### <a name="choose-single-core-app-service-plans"></a>Choisir des plans App Service à cœur unique

Lorsque vous créez une application de fonction qui utilise hello plan App Service, nous vous recommandons de sélectionner un plan à cœur unique au lieu d’un plan à plusieurs cœurs. Aujourd'hui, les fonctions exécute les fonctions JavaScript plus efficacement sur des machines virtuelles à cœur unique, et à l’aide de machines virtuelles plus grandes ne produit pas les améliorations des performances hello attendu. Le cas échéant, vous pouvez faire une mise à l’échelle horizontale manuellement en ajoutant des instances de machine virtuelle à cœur unique, ou vous pouvez activer la mise à l’échelle automatique. Pour plus d’informations, consultez [Mettre à l’échelle le nombre d’instances manuellement ou automatiquement](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).    

### <a name="typescript-and-coffeescript-support"></a>Prise en charge de typeScript et CoffeeScript
Étant donné que la prise en charge directe n’existe pas encore de TypeScript ou CoffeeScript de compilation automatique via l’exécution de hello, cette prise en charge doit toobe gérée en dehors de l’exécution de hello, au moment du déploiement. 

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello suivant des ressources :

* [Meilleures pratiques pour Azure Functions](functions-best-practices.md)
* [Référence du développeur Azure Functions](functions-reference.md)
* [Informations de référence pour les développeurs C# sur Azure Functions](functions-reference-csharp.md)
* [Informations de référence pour les développeurs F# sur Azure Functions](functions-reference-fsharp.md)
* [Déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md)

