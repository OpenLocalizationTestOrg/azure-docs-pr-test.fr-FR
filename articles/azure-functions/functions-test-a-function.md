---
title: aaaTesting les fonctions Azure | Documents Microsoft
description: "Testez vos fonctions Azure à l’aide de Postman, cURL et Node.js."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur, test"
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a>Stratégies permettant de tester votre code dans Azure Functions

Cette rubrique montre hello est proche de diverses fonctions tootest façons, notamment l’utilisation de hello suivant général :

+ Outils basés sur HTTP, comme cURL, Postman et même un navigateur web pour les déclencheurs basés sur le web
+ Explorateur de stockage Azure, les déclencheurs tootest basée sur le stockage Azure
+ Onglet de test dans le portail de fonctions d’Azure hello
+ Fonction déclenchée par un minuteur
+ Application ou infrastructure de test

Toutes ces méthodes de test utilisent une fonction de déclenchement HTTP qui accepte une entrée par le biais requête chaîne hello ou paramètre de corps de demande. Cette fonction est créé dans la première section de hello.

## <a name="create-a-function-for-testing"></a>Créer une fonction de test
Pour la plupart de ce didacticiel, nous utilisons une version légèrement modifiée du modèle de fonction HttpTrigger JavaScript est disponible lorsque vous créez une fonction de hello. Si vous avez besoin d’aide pour créer une fonction, passez en revue ce [didacticiel](functions-create-first-azure-function.md). Choisissez hello **HttpTrigger - JavaScript** modèle lors de la création de fonction de test hello Bonjour [portail Azure].

Hello modèle de fonction par défaut est essentiellement une fonction « hello world » qui renvoie le nom précédent hello de hello demande corps ou une requête paramètre de chaîne, `name=<your name>`.  Nous allons mettre à jour les code hello tooalso permettent tooprovide hello nom et une adresse en tant que contenu JSON dans le corps de la demande hello. Puis la fonction hello répercute ces client toohello arrière lorsqu’il est disponible.   

Mettre à jour la fonction hello avec hello suivant de code, nous allons utiliser pour le test :

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a>Test d’une fonction avec des outils
En dehors de hello portail Azure, il existe différents outils que vous pouvez utiliser tootrigger vos fonctions pour le test. Ceux-ci incluent les outils de test HTTP (basés sur l’interface utilisateur et sur la ligne de commande), les outils d’accès au stockage Azure et même un simple navigateur web.

### <a name="test-with-a-browser"></a>Test avec un navigateur
navigateur Hello est une fonction de tootrigger facilement via le protocole HTTP. Vous pouvez utiliser un navigateur pour les requêtes GET qui ne nécessitent pas une charge utile du corps et utilisent uniquement des paramètres de chaîne de requête.

fonction de hello tootest définie précédemment, hello de copie **Url de la fonction** à partir du portail de hello. Il a hello suivant du formulaire :

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Ajouter hello `name` la chaîne de requête toohello paramètres. Utiliser un nom réel pour hello `<Enter a name here>` espace réservé.

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

URL de hello coller dans votre navigateur, vous devez obtenir un suivante toohello de la similaire réponse.

![Capture d’écran de l’onglet du navigateur Chrome avec la réponse de test](./media/functions-test-a-function/browser-test.png)

Cet exemple est le navigateur Chrome hello, qui encapsule hello a retourné une chaîne au format XML. Autres navigateurs affichent simplement les valeur de chaîne hello.

Dans le portail de hello **journaux** sortie de fenêtre, similaire toohello suivant est consigné lors de l’exécution de fonction hello :

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a>Test avec Postman
Hello recommandé outil tootest la plupart de vos fonctions est Postman, qui s’intègre avec le navigateur Chrome de hello. tooinstall Postman, consultez [Postman d’obtenir](https://www.getpostman.com/). Postman permet de contrôler beaucoup plus d’attributs d’une requête HTTP.

> [!TIP]
> Utilisez hello HTTP outil de test qui vous conviennent le mieux. Voici certains tooPostman alternatives :  
>
> * [Fiddler](http://www.telerik.com/fiddler)  
> * [Paw](https://luckymarmot.com/paw)  
>
>

fonction de hello tootest avec un corps de demande dans Postman :

1. Démarrer Postman de hello **applications** bouton dans le coin supérieur gauche de hello d’une fenêtre de navigateur Chrome.
2. Copiez votre **URL de fonction** et collez-la dans Postman. Il inclut le paramètre de chaîne de requête de code d’accès hello.
3. Changer de méthode hello HTTP trop**POST**.
4. Cliquez sur **corps** > **brutes**et ajoutez suivant toohello similaire de corps de demande un JSON :

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. Cliquez sur **Envoyer**.

Hello image suivante montre test hello echo simple fonction exemple dans ce didacticiel.

![Capture d’écran de l’interface utilisateur de Postman](./media/functions-test-a-function/postman-test.png)

Dans le portail de hello **journaux** sortie de fenêtre, similaire toohello suivant est consigné lors de l’exécution de fonction hello :

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a>Tester avec cURL à partir de la ligne de commande hello
Souvent lorsque vous testez le logiciel, il n’est pas nécessaire toolook tout plus hello débogage toohelp de ligne de commande de votre application. Il en est de même pour les fonctions. Notez que les cURL hello est disponible par défaut sur les systèmes basés sur Linux. Sous Windows, vous devez d’abord télécharger et installer hello [cURL outil](https://curl.haxx.se/).

fonction de hello tootest que nous avons défini précédemment, hello de copie **URL de la fonction** à partir du portail de hello. Il a hello suivant du formulaire :

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Il s’agit hello URL de votre fonction de déclenchement. Tester une opération GET à l’aide de la commande de cURL hello sur toomake de ligne de commande hello (`-G` ou `--get`) demande par rapport à la fonction hello :

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Cet exemple requiert un paramètre de chaîne de requête, qui peut être passé en tant que données (`-d`) Bonjour cURL commande :

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

Commande hello exécution et que vous consultez hello suivant de sortie de la fonction hello de ligne de commande hello :

![Capture d’écran de la sortie de l’invite de commande](./media/functions-test-a-function/curl-test.png)

Dans le portail de hello **journaux** sortie de fenêtre, similaire toohello suivant est consigné lors de l’exécution de fonction hello :

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a>Test d’un déclencheur d’objet blob à l’aide de l’Explorateur de stockage
Vous pouvez tester une fonction de déclenchement d’objet blob à l’aide de l’[Explorateur de stockage Azure](http://storageexplorer.com/).

1. Bonjour [portail Azure] pour votre application de la fonction, créez une fonction de déclencheur de blob c#, F # ou JavaScript. Nom de toohello toomonitor hello chemin d’accès de votre conteneur d’objets blob du jeu. Par exemple :

        files
2. Cliquez sur hello  **+**  tooselect ou pour créer le compte de stockage hello souhaité toouse. Cliquez ensuite sur **Créer**.
3. Créez un fichier texte avec hello suivant de texte et enregistrez-le :

        A text file for blob trigger function testing.
4. Exécutez [Azure Storage Explorer](http://storageexplorer.com/)et vous connecter toohello conteneur d’objets blob dans le compte de stockage hello en cours d’analyse.
5. Cliquez sur **télécharger** fichier de texte hello tooupload.

    ![Capture d’écran de l’explorateur de stockage](./media/functions-test-a-function/azure-storage-explorer-test.png)

code de la fonction Hello par défaut blob déclencheur rapports traitement hello du blob hello dans les journaux hello :

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a>Test d’une fonction au sein de fonctions
Bonjour Azure fonctions portail est conçu toolet vous testez HTTP et le minuteur déclenché fonctions. Vous pouvez également créer des fonctions tootrigger autres fonctions que vous testez.

### <a name="test-with-hello-functions-portal-run-button"></a>Avec le bouton d’exécuter portail hello fonctions de test
Hello portail fournit un **exécuter** bouton que vous pouvez utiliser certaines toodo de tests limités. Vous pouvez fournir un corps de demande à l’aide du bouton de hello, mais vous ne peut pas fournir les paramètres de chaîne de requête ou mettre à jour des en-têtes de demande.

Test hello HTTP déclencheur que nous avons créée précédemment en ajoutant un toohello similaire de chaîne JSON suivant Bonjour **corps de la demande** champ. Puis cliquez sur hello **exécuter** bouton.

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

Dans le portail de hello **journaux** sortie de fenêtre, similaire toohello suivant est consigné lors de l’exécution de fonction hello :

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a>Test avec un déclencheur de minuteur
Certaines fonctions ne peuvent pas être testées correctement avec les outils hello mentionnés précédemment. C’est le cas, par exemple, d’une fonction de déclenchement de file d’attente qui s’exécute lorsqu’un message est déposé dans [Stockage File d’attente Azure](../storage/queues/storage-dotnet-how-to-use-queues.md). Vous pouvez toujours écrire code toodrop un message dans votre file d’attente, et un exemple dans un projet de console est fourni plus loin dans cet article. Toutefois, une autre approche vous permet de tester des fonctions directement.  

Vous pouvez utiliser un déclencheur de minuteur configuré avec une liaison de sortie de file d’attente. Ce code de déclencheur du minuteur peut écrire hello test messages toohello file d’attente. Cette section présente un exemple.

Pour plus d’informations sur l’utilisation des liaisons avec des fonctions d’Azure, consultez hello [référence du développeur Azure fonctions](functions-reference.md).

#### <a name="create-a-queue-trigger-for-testing"></a>Créer un déclencheur de file d’attente pour le test
toodemonstrate cette approche, nous créons d’abord une fonction de déclenchement de file d’attente que nous souhaitons tootest pour une file d’attente nommée `queue-newusers`. Cette fonction traite les informations de nom et d’adresse d’un nouvel utilisateur déposées dans Stockage File d'attente.

> [!NOTE]
> Si vous utilisez un nom de file d’attente différente, assurez-vous que nom hello que vous utilisez est conforme toohello [d’affectation de noms de files d’attente et les métadonnées](https://msdn.microsoft.com/library/dd179349.aspx) règles. Sinon, vous recevez un message d’erreur.
>
>

1. Bonjour [portail Azure] pour votre application de la fonction, cliquez sur **nouvelle fonction** > **QueueTrigger - C#**.
2. Entrez toobe de nom de file d’attente hello analysé par la fonction de file d’attente hello :

        queue-newusers
3. Cliquez sur hello  **+**  tooselect ou pour créer le compte de stockage hello souhaité toouse. Cliquez ensuite sur **Créer**.
4. Laissez cette fenêtre de navigateur portail ouvert, pour que vous puissiez contrôler les entrées de journal hello pour le code de modèle de fonction hello par défaut file d’attente.

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a>Créer un toodrop de déclencheur de minuterie d’un message dans la file d’attente hello
1. Ouvrez hello [portail Azure] dans une nouvelle fenêtre de navigateur et accédez tooyour fonction app.
2. Cliquez sur **Nouvelle fonction** > **TimerTrigger - C#**. Entrez un tooset d’expression cron la fréquence à laquelle hello du minuteur code teste votre fonction de la file d’attente. Cliquez ensuite sur **Créer**. Si vous souhaitez hello test toorun toutes les 30 secondes, vous pouvez utiliser suivant de hello [expression CRON](https://wikipedia.org/wiki/Cron#CRON_expression):

        */30 * * * * *
3. Cliquez sur hello **intégrer** onglet pour votre nouveau déclencheur du minuteur.
4. Sous **Sortie**, cliquez sur le bouton **+ Nouvelle sortie**. Puis cliquez sur **File d’attente** et sur **Sélectionner**.
5. Nom de hello de note que vous utilisez pour hello **objet de message de file d’attente**. Vous l’utiliser dans le code de la fonction hello du minuteur.

        myQueue
6. Entrez les nom de file d’attente hello où le message de type hello est envoyé :

        queue-newusers
7. Cliquez sur hello  **+**  bouton compte de stockage tooselect hello précédemment utilisé avec le déclencheur de file d’attente hello. Cliquez ensuite sur **Enregistrer**.
8. Cliquez sur hello **développer** onglet pour votre déclencheur du minuteur.
9. Vous pouvez utiliser hello suivant de code pour la fonction de minuteur hello c#, tant que vous avez utilisé hello même file d’attente de nom de l’objet message présenté plus haut. Cliquez ensuite sur **Enregistrer**.

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

À ce stade, hello c# (fonction) du minuteur s’exécute toutes les 30 secondes si vous avez utilisé l’exemple d’expression cron de hello. chaque exécution du rapport de journaux Hello pour la fonction de minuteur hello :

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

Dans la fenêtre de navigateur hello pour la fonction de file d’attente hello, vous pouvez voir chaque message en cours de traitement :

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a>Test d’une fonction avec un code
Vous devrez peut-être toocreate un tootest externe de l’application ou infrastructure de vos fonctions.

### <a name="test-an-http-trigger-function-with-code-nodejs"></a>Test d’une fonction de déclenchement HTTP avec un code Node.js
Vous pouvez utiliser un tooexecute d’application Node.js un tootest de demande HTTP de votre fonction.
Assurez-vous que tooset :

* Hello `host` dans l’hôte d’application hello demande options tooyour (fonction).
* Le nom de fonction Bonjour `path`.
* Votre code d’accès (`<your code>`) Bonjour `path`.

Exemple de code :

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


Output:

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

Dans le portail de hello **journaux** sortie de fenêtre, similaire toohello suivant est consigné lors de l’exécution de fonction hello :

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a>Test d’une fonction de déclenchement de file d’attente avec un code : C# #
Nous l’avons mentionné plus haut que vous pouvez tester un déclencheur de la file d’attente à l’aide de code toodrop un message dans votre file d’attente. Hello suivant l’exemple de code est basé sur le code hello c# présenté dans hello [mise en route avec le stockage de file d’attente Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) didacticiel. Le code des autres langages est également disponible via ce lien.

tootest ce code dans une application console, vous devez :

* [Configurer votre chaîne de connexion de stockage dans le fichier app.config hello](../storage/queues/storage-dotnet-how-to-use-queues.md).
* Passez un `name` et `address` en tant que paramètres toohello application. Par exemple, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`. (Ce code accepte hello nom et adresse d’un nouvel utilisateur en tant qu’arguments de ligne de commande pendant l’exécution.)

Exemple de code C# :

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

Dans la fenêtre de navigateur hello pour la fonction de file d’attente hello, vous pouvez voir chaque message en cours de traitement :

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portail Azure]: https://portal.azure.com
