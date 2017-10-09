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
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="67a55-104">Stratégies permettant de tester votre code dans Azure Functions</span><span class="sxs-lookup"><span data-stu-id="67a55-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="67a55-105">Cette rubrique montre hello est proche de diverses fonctions tootest façons, notamment l’utilisation de hello suivant général :</span><span class="sxs-lookup"><span data-stu-id="67a55-105">This topic demonstrates hello various ways tootest functions, including using hello following general approaches:</span></span>

+ <span data-ttu-id="67a55-106">Outils basés sur HTTP, comme cURL, Postman et même un navigateur web pour les déclencheurs basés sur le web</span><span class="sxs-lookup"><span data-stu-id="67a55-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="67a55-107">Explorateur de stockage Azure, les déclencheurs tootest basée sur le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="67a55-107">Azure Storage Explorer, tootest Azure Storage-based triggers</span></span>
+ <span data-ttu-id="67a55-108">Onglet de test dans le portail de fonctions d’Azure hello</span><span class="sxs-lookup"><span data-stu-id="67a55-108">Test tab in hello Azure Functions portal</span></span>
+ <span data-ttu-id="67a55-109">Fonction déclenchée par un minuteur</span><span class="sxs-lookup"><span data-stu-id="67a55-109">Timer-triggered function</span></span>
+ <span data-ttu-id="67a55-110">Application ou infrastructure de test</span><span class="sxs-lookup"><span data-stu-id="67a55-110">Testing application or framework</span></span>

<span data-ttu-id="67a55-111">Toutes ces méthodes de test utilisent une fonction de déclenchement HTTP qui accepte une entrée par le biais requête chaîne hello ou paramètre de corps de demande.</span><span class="sxs-lookup"><span data-stu-id="67a55-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or hello request body.</span></span> <span data-ttu-id="67a55-112">Cette fonction est créé dans la première section de hello.</span><span class="sxs-lookup"><span data-stu-id="67a55-112">You create this function in hello first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="67a55-113">Créer une fonction de test</span><span class="sxs-lookup"><span data-stu-id="67a55-113">Create a function for testing</span></span>
<span data-ttu-id="67a55-114">Pour la plupart de ce didacticiel, nous utilisons une version légèrement modifiée du modèle de fonction HttpTrigger JavaScript est disponible lorsque vous créez une fonction de hello.</span><span class="sxs-lookup"><span data-stu-id="67a55-114">For most of this tutorial, we use a slightly modified version of hello HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="67a55-115">Si vous avez besoin d’aide pour créer une fonction, passez en revue ce [didacticiel](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="67a55-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="67a55-116">Choisissez hello **HttpTrigger - JavaScript** modèle lors de la création de fonction de test hello Bonjour [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="67a55-116">Choose hello **HttpTrigger- JavaScript** template when creating hello test function in hello [Azure portal].</span></span>

<span data-ttu-id="67a55-117">Hello modèle de fonction par défaut est essentiellement une fonction « hello world » qui renvoie le nom précédent hello de hello demande corps ou une requête paramètre de chaîne, `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="67a55-117">hello default function template is basically a "hello world" function that echoes back hello name from hello request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="67a55-118">Nous allons mettre à jour les code hello tooalso permettent tooprovide hello nom et une adresse en tant que contenu JSON dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="67a55-118">We'll update hello code tooalso allow you tooprovide hello name and an address as JSON content in hello request body.</span></span> <span data-ttu-id="67a55-119">Puis la fonction hello répercute ces client toohello arrière lorsqu’il est disponible.</span><span class="sxs-lookup"><span data-stu-id="67a55-119">Then hello function echoes these back toohello client when available.</span></span>   

<span data-ttu-id="67a55-120">Mettre à jour la fonction hello avec hello suivant de code, nous allons utiliser pour le test :</span><span class="sxs-lookup"><span data-stu-id="67a55-120">Update hello function with hello following code, which we will use for testing:</span></span>

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

## <a name="test-a-function-with-tools"></a><span data-ttu-id="67a55-121">Test d’une fonction avec des outils</span><span class="sxs-lookup"><span data-stu-id="67a55-121">Test a function with tools</span></span>
<span data-ttu-id="67a55-122">En dehors de hello portail Azure, il existe différents outils que vous pouvez utiliser tootrigger vos fonctions pour le test.</span><span class="sxs-lookup"><span data-stu-id="67a55-122">Outside hello Azure portal, there are various tools that you can use tootrigger your functions for testing.</span></span> <span data-ttu-id="67a55-123">Ceux-ci incluent les outils de test HTTP (basés sur l’interface utilisateur et sur la ligne de commande), les outils d’accès au stockage Azure et même un simple navigateur web.</span><span class="sxs-lookup"><span data-stu-id="67a55-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="67a55-124">Test avec un navigateur</span><span class="sxs-lookup"><span data-stu-id="67a55-124">Test with a browser</span></span>
<span data-ttu-id="67a55-125">navigateur Hello est une fonction de tootrigger facilement via le protocole HTTP.</span><span class="sxs-lookup"><span data-stu-id="67a55-125">hello web browser is a simple way tootrigger functions via HTTP.</span></span> <span data-ttu-id="67a55-126">Vous pouvez utiliser un navigateur pour les requêtes GET qui ne nécessitent pas une charge utile du corps et utilisent uniquement des paramètres de chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="67a55-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="67a55-127">fonction de hello tootest définie précédemment, hello de copie **Url de la fonction** à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="67a55-127">tootest hello function we defined earlier, copy hello **Function Url** from hello portal.</span></span> <span data-ttu-id="67a55-128">Il a hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="67a55-128">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="67a55-129">Ajouter hello `name` la chaîne de requête toohello paramètres.</span><span class="sxs-lookup"><span data-stu-id="67a55-129">Append hello `name` parameter toohello query string.</span></span> <span data-ttu-id="67a55-130">Utiliser un nom réel pour hello `<Enter a name here>` espace réservé.</span><span class="sxs-lookup"><span data-stu-id="67a55-130">Use an actual name for hello `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="67a55-131">URL de hello coller dans votre navigateur, vous devez obtenir un suivante toohello de la similaire réponse.</span><span class="sxs-lookup"><span data-stu-id="67a55-131">Paste hello URL into your browser, and you should get a response similar toohello following.</span></span>

![Capture d’écran de l’onglet du navigateur Chrome avec la réponse de test](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="67a55-133">Cet exemple est le navigateur Chrome hello, qui encapsule hello a retourné une chaîne au format XML.</span><span class="sxs-lookup"><span data-stu-id="67a55-133">This example is hello Chrome browser, which wraps hello returned string in XML.</span></span> <span data-ttu-id="67a55-134">Autres navigateurs affichent simplement les valeur de chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="67a55-134">Other browsers display just hello string value.</span></span>

<span data-ttu-id="67a55-135">Dans le portail de hello **journaux** sortie de fenêtre, similaire toohello suivant est consigné lors de l’exécution de fonction hello :</span><span class="sxs-lookup"><span data-stu-id="67a55-135">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="67a55-136">Test avec Postman</span><span class="sxs-lookup"><span data-stu-id="67a55-136">Test with Postman</span></span>
<span data-ttu-id="67a55-137">Hello recommandé outil tootest la plupart de vos fonctions est Postman, qui s’intègre avec le navigateur Chrome de hello.</span><span class="sxs-lookup"><span data-stu-id="67a55-137">hello recommended tool tootest most of your functions is Postman, which integrates with hello Chrome browser.</span></span> <span data-ttu-id="67a55-138">tooinstall Postman, consultez [Postman d’obtenir](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="67a55-138">tooinstall Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="67a55-139">Postman permet de contrôler beaucoup plus d’attributs d’une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="67a55-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="67a55-140">Utilisez hello HTTP outil de test qui vous conviennent le mieux.</span><span class="sxs-lookup"><span data-stu-id="67a55-140">Use hello HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="67a55-141">Voici certains tooPostman alternatives :</span><span class="sxs-lookup"><span data-stu-id="67a55-141">Here are some alternatives tooPostman:</span></span>  
>
> * [<span data-ttu-id="67a55-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="67a55-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="67a55-143">Paw</span><span class="sxs-lookup"><span data-stu-id="67a55-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="67a55-144">fonction de hello tootest avec un corps de demande dans Postman :</span><span class="sxs-lookup"><span data-stu-id="67a55-144">tootest hello function with a request body in Postman:</span></span>

1. <span data-ttu-id="67a55-145">Démarrer Postman de hello **applications** bouton dans le coin supérieur gauche de hello d’une fenêtre de navigateur Chrome.</span><span class="sxs-lookup"><span data-stu-id="67a55-145">Start Postman from hello **Apps** button in hello upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="67a55-146">Copiez votre **URL de fonction** et collez-la dans Postman.</span><span class="sxs-lookup"><span data-stu-id="67a55-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="67a55-147">Il inclut le paramètre de chaîne de requête de code d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="67a55-147">It includes hello access code query string parameter.</span></span>
3. <span data-ttu-id="67a55-148">Changer de méthode hello HTTP trop**POST**.</span><span class="sxs-lookup"><span data-stu-id="67a55-148">Change hello HTTP method too**POST**.</span></span>
4. <span data-ttu-id="67a55-149">Cliquez sur **corps** > **brutes**et ajoutez suivant toohello similaire de corps de demande un JSON :</span><span class="sxs-lookup"><span data-stu-id="67a55-149">Click **Body** > **raw**, and add a JSON request body similar toohello following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="67a55-150">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="67a55-150">Click **Send**.</span></span>

<span data-ttu-id="67a55-151">Hello image suivante montre test hello echo simple fonction exemple dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="67a55-151">hello following image shows testing hello simple echo function example in this tutorial.</span></span>

![Capture d’écran de l’interface utilisateur de Postman](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="67a55-153">Dans le portail de hello **journaux** sortie de fenêtre, similaire toohello suivant est consigné lors de l’exécution de fonction hello :</span><span class="sxs-lookup"><span data-stu-id="67a55-153">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a><span data-ttu-id="67a55-154">Tester avec cURL à partir de la ligne de commande hello</span><span class="sxs-lookup"><span data-stu-id="67a55-154">Test with cURL from hello command line</span></span>
<span data-ttu-id="67a55-155">Souvent lorsque vous testez le logiciel, il n’est pas nécessaire toolook tout plus hello débogage toohelp de ligne de commande de votre application.</span><span class="sxs-lookup"><span data-stu-id="67a55-155">Often when you're testing software, it's not necessary toolook any further than hello command line toohelp debug your application.</span></span> <span data-ttu-id="67a55-156">Il en est de même pour les fonctions.</span><span class="sxs-lookup"><span data-stu-id="67a55-156">This is no different with testing functions.</span></span> <span data-ttu-id="67a55-157">Notez que les cURL hello est disponible par défaut sur les systèmes basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="67a55-157">Note that hello cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="67a55-158">Sous Windows, vous devez d’abord télécharger et installer hello [cURL outil](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="67a55-158">On Windows, you must first download and install hello [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="67a55-159">fonction de hello tootest que nous avons défini précédemment, hello de copie **URL de la fonction** à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="67a55-159">tootest hello function that we defined earlier, copy hello **Function URL** from hello portal.</span></span> <span data-ttu-id="67a55-160">Il a hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="67a55-160">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="67a55-161">Il s’agit hello URL de votre fonction de déclenchement.</span><span class="sxs-lookup"><span data-stu-id="67a55-161">This is hello URL for triggering your function.</span></span> <span data-ttu-id="67a55-162">Tester une opération GET à l’aide de la commande de cURL hello sur toomake de ligne de commande hello (`-G` ou `--get`) demande par rapport à la fonction hello :</span><span class="sxs-lookup"><span data-stu-id="67a55-162">Test this by using hello cURL command on hello command line toomake a GET (`-G` or `--get`) request against hello function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="67a55-163">Cet exemple requiert un paramètre de chaîne de requête, qui peut être passé en tant que données (`-d`) Bonjour cURL commande :</span><span class="sxs-lookup"><span data-stu-id="67a55-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in hello cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="67a55-164">Commande hello exécution et que vous consultez hello suivant de sortie de la fonction hello de ligne de commande hello :</span><span class="sxs-lookup"><span data-stu-id="67a55-164">Run hello command, and you see hello following output of hello function on hello command line:</span></span>

![Capture d’écran de la sortie de l’invite de commande](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="67a55-166">Dans le portail de hello **journaux** sortie de fenêtre, similaire toohello suivant est consigné lors de l’exécution de fonction hello :</span><span class="sxs-lookup"><span data-stu-id="67a55-166">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="67a55-167">Test d’un déclencheur d’objet blob à l’aide de l’Explorateur de stockage</span><span class="sxs-lookup"><span data-stu-id="67a55-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="67a55-168">Vous pouvez tester une fonction de déclenchement d’objet blob à l’aide de l’[Explorateur de stockage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="67a55-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="67a55-169">Bonjour [portail Azure] pour votre application de la fonction, créez une fonction de déclencheur de blob c#, F # ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="67a55-169">In hello [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="67a55-170">Nom de toohello toomonitor hello chemin d’accès de votre conteneur d’objets blob du jeu.</span><span class="sxs-lookup"><span data-stu-id="67a55-170">Set hello path toomonitor toohello name of your blob container.</span></span> <span data-ttu-id="67a55-171">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="67a55-171">For example:</span></span>

        files
2. <span data-ttu-id="67a55-172">Cliquez sur hello  **+**  tooselect ou pour créer le compte de stockage hello souhaité toouse.</span><span class="sxs-lookup"><span data-stu-id="67a55-172">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="67a55-173">Cliquez ensuite sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="67a55-173">Then click **Create**.</span></span>
3. <span data-ttu-id="67a55-174">Créez un fichier texte avec hello suivant de texte et enregistrez-le :</span><span class="sxs-lookup"><span data-stu-id="67a55-174">Create a text file with hello following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="67a55-175">Exécutez [Azure Storage Explorer](http://storageexplorer.com/)et vous connecter toohello conteneur d’objets blob dans le compte de stockage hello en cours d’analyse.</span><span class="sxs-lookup"><span data-stu-id="67a55-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect toohello blob container in hello storage account being monitored.</span></span>
5. <span data-ttu-id="67a55-176">Cliquez sur **télécharger** fichier de texte hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="67a55-176">Click **Upload** tooupload hello text file.</span></span>

    ![Capture d’écran de l’explorateur de stockage](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="67a55-178">code de la fonction Hello par défaut blob déclencheur rapports traitement hello du blob hello dans les journaux hello :</span><span class="sxs-lookup"><span data-stu-id="67a55-178">hello default blob trigger function code reports hello processing of hello blob in hello logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="67a55-179">Test d’une fonction au sein de fonctions</span><span class="sxs-lookup"><span data-stu-id="67a55-179">Test a function within functions</span></span>
<span data-ttu-id="67a55-180">Bonjour Azure fonctions portail est conçu toolet vous testez HTTP et le minuteur déclenché fonctions.</span><span class="sxs-lookup"><span data-stu-id="67a55-180">hello Azure Functions portal is designed toolet you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="67a55-181">Vous pouvez également créer des fonctions tootrigger autres fonctions que vous testez.</span><span class="sxs-lookup"><span data-stu-id="67a55-181">You can also create functions tootrigger other functions that you are testing.</span></span>

### <a name="test-with-hello-functions-portal-run-button"></a><span data-ttu-id="67a55-182">Avec le bouton d’exécuter portail hello fonctions de test</span><span class="sxs-lookup"><span data-stu-id="67a55-182">Test with hello Functions portal Run button</span></span>
<span data-ttu-id="67a55-183">Hello portail fournit un **exécuter** bouton que vous pouvez utiliser certaines toodo de tests limités.</span><span class="sxs-lookup"><span data-stu-id="67a55-183">hello portal provides a **Run** button that you can use toodo some limited testing.</span></span> <span data-ttu-id="67a55-184">Vous pouvez fournir un corps de demande à l’aide du bouton de hello, mais vous ne peut pas fournir les paramètres de chaîne de requête ou mettre à jour des en-têtes de demande.</span><span class="sxs-lookup"><span data-stu-id="67a55-184">You can provide a request body by using hello button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="67a55-185">Test hello HTTP déclencheur que nous avons créée précédemment en ajoutant un toohello similaire de chaîne JSON suivant Bonjour **corps de la demande** champ.</span><span class="sxs-lookup"><span data-stu-id="67a55-185">Test hello HTTP trigger function we created earlier by adding a JSON string similar toohello following in hello **Request body** field.</span></span> <span data-ttu-id="67a55-186">Puis cliquez sur hello **exécuter** bouton.</span><span class="sxs-lookup"><span data-stu-id="67a55-186">Then click hello **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="67a55-187">Dans le portail de hello **journaux** sortie de fenêtre, similaire toohello suivant est consigné lors de l’exécution de fonction hello :</span><span class="sxs-lookup"><span data-stu-id="67a55-187">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="67a55-188">Test avec un déclencheur de minuteur</span><span class="sxs-lookup"><span data-stu-id="67a55-188">Test with a timer trigger</span></span>
<span data-ttu-id="67a55-189">Certaines fonctions ne peuvent pas être testées correctement avec les outils hello mentionnés précédemment.</span><span class="sxs-lookup"><span data-stu-id="67a55-189">Some functions can't be adequately tested with hello tools mentioned previously.</span></span> <span data-ttu-id="67a55-190">C’est le cas, par exemple, d’une fonction de déclenchement de file d’attente qui s’exécute lorsqu’un message est déposé dans [Stockage File d’attente Azure](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="67a55-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="67a55-191">Vous pouvez toujours écrire code toodrop un message dans votre file d’attente, et un exemple dans un projet de console est fourni plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="67a55-191">You can always write code toodrop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="67a55-192">Toutefois, une autre approche vous permet de tester des fonctions directement.</span><span class="sxs-lookup"><span data-stu-id="67a55-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="67a55-193">Vous pouvez utiliser un déclencheur de minuteur configuré avec une liaison de sortie de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="67a55-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="67a55-194">Ce code de déclencheur du minuteur peut écrire hello test messages toohello file d’attente.</span><span class="sxs-lookup"><span data-stu-id="67a55-194">That timer trigger code can then write hello test messages toohello queue.</span></span> <span data-ttu-id="67a55-195">Cette section présente un exemple.</span><span class="sxs-lookup"><span data-stu-id="67a55-195">This section walks through an example.</span></span>

<span data-ttu-id="67a55-196">Pour plus d’informations sur l’utilisation des liaisons avec des fonctions d’Azure, consultez hello [référence du développeur Azure fonctions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="67a55-196">For more in-depth information on using bindings with Azure Functions, see hello [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="67a55-197">Créer un déclencheur de file d’attente pour le test</span><span class="sxs-lookup"><span data-stu-id="67a55-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="67a55-198">toodemonstrate cette approche, nous créons d’abord une fonction de déclenchement de file d’attente que nous souhaitons tootest pour une file d’attente nommée `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="67a55-198">toodemonstrate this approach, we first create a queue trigger function that we want tootest for a queue named `queue-newusers`.</span></span> <span data-ttu-id="67a55-199">Cette fonction traite les informations de nom et d’adresse d’un nouvel utilisateur déposées dans Stockage File d'attente.</span><span class="sxs-lookup"><span data-stu-id="67a55-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="67a55-200">Si vous utilisez un nom de file d’attente différente, assurez-vous que nom hello que vous utilisez est conforme toohello [d’affectation de noms de files d’attente et les métadonnées](https://msdn.microsoft.com/library/dd179349.aspx) règles.</span><span class="sxs-lookup"><span data-stu-id="67a55-200">If you use a different queue name, make sure hello name you use conforms toohello [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="67a55-201">Sinon, vous recevez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="67a55-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="67a55-202">Bonjour [portail Azure] pour votre application de la fonction, cliquez sur **nouvelle fonction** > **QueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="67a55-202">In hello [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="67a55-203">Entrez toobe de nom de file d’attente hello analysé par la fonction de file d’attente hello :</span><span class="sxs-lookup"><span data-stu-id="67a55-203">Enter hello queue name toobe monitored by hello queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="67a55-204">Cliquez sur hello  **+**  tooselect ou pour créer le compte de stockage hello souhaité toouse.</span><span class="sxs-lookup"><span data-stu-id="67a55-204">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="67a55-205">Cliquez ensuite sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="67a55-205">Then click **Create**.</span></span>
4. <span data-ttu-id="67a55-206">Laissez cette fenêtre de navigateur portail ouvert, pour que vous puissiez contrôler les entrées de journal hello pour le code de modèle de fonction hello par défaut file d’attente.</span><span class="sxs-lookup"><span data-stu-id="67a55-206">Leave this portal browser window open, so you can monitor hello log entries for hello default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a><span data-ttu-id="67a55-207">Créer un toodrop de déclencheur de minuterie d’un message dans la file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="67a55-207">Create a timer trigger toodrop a message in hello queue</span></span>
1. <span data-ttu-id="67a55-208">Ouvrez hello [portail Azure] dans une nouvelle fenêtre de navigateur et accédez tooyour fonction app.</span><span class="sxs-lookup"><span data-stu-id="67a55-208">Open hello [Azure portal] in a new browser window, and navigate tooyour function app.</span></span>
2. <span data-ttu-id="67a55-209">Cliquez sur **Nouvelle fonction** > **TimerTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="67a55-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="67a55-210">Entrez un tooset d’expression cron la fréquence à laquelle hello du minuteur code teste votre fonction de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="67a55-210">Enter a cron expression tooset how often hello timer code tests your queue function.</span></span> <span data-ttu-id="67a55-211">Cliquez ensuite sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="67a55-211">Then click **Create**.</span></span> <span data-ttu-id="67a55-212">Si vous souhaitez hello test toorun toutes les 30 secondes, vous pouvez utiliser suivant de hello [expression CRON](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="67a55-212">If you want hello test toorun every 30 seconds, you can use hello following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="67a55-213">Cliquez sur hello **intégrer** onglet pour votre nouveau déclencheur du minuteur.</span><span class="sxs-lookup"><span data-stu-id="67a55-213">Click hello **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="67a55-214">Sous **Sortie**, cliquez sur le bouton **+ Nouvelle sortie**.</span><span class="sxs-lookup"><span data-stu-id="67a55-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="67a55-215">Puis cliquez sur **File d’attente** et sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="67a55-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="67a55-216">Nom de hello de note que vous utilisez pour hello **objet de message de file d’attente**.</span><span class="sxs-lookup"><span data-stu-id="67a55-216">Note hello name you use for hello **queue message object**.</span></span> <span data-ttu-id="67a55-217">Vous l’utiliser dans le code de la fonction hello du minuteur.</span><span class="sxs-lookup"><span data-stu-id="67a55-217">You use this in hello timer function code.</span></span>

        myQueue
6. <span data-ttu-id="67a55-218">Entrez les nom de file d’attente hello où le message de type hello est envoyé :</span><span class="sxs-lookup"><span data-stu-id="67a55-218">Enter hello queue name where hello message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="67a55-219">Cliquez sur hello  **+**  bouton compte de stockage tooselect hello précédemment utilisé avec le déclencheur de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="67a55-219">Click hello **+** button tooselect hello storage account you used previously with hello queue trigger.</span></span> <span data-ttu-id="67a55-220">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="67a55-220">Then click **Save**.</span></span>
8. <span data-ttu-id="67a55-221">Cliquez sur hello **développer** onglet pour votre déclencheur du minuteur.</span><span class="sxs-lookup"><span data-stu-id="67a55-221">Click hello **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="67a55-222">Vous pouvez utiliser hello suivant de code pour la fonction de minuteur hello c#, tant que vous avez utilisé hello même file d’attente de nom de l’objet message présenté plus haut.</span><span class="sxs-lookup"><span data-stu-id="67a55-222">You can use hello following code for hello C# timer function, as long as you used hello same queue message object name shown earlier.</span></span> <span data-ttu-id="67a55-223">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="67a55-223">Then click **Save**.</span></span>

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

<span data-ttu-id="67a55-224">À ce stade, hello c# (fonction) du minuteur s’exécute toutes les 30 secondes si vous avez utilisé l’exemple d’expression cron de hello.</span><span class="sxs-lookup"><span data-stu-id="67a55-224">At this point, hello C# timer function executes every 30 seconds if you used hello example cron expression.</span></span> <span data-ttu-id="67a55-225">chaque exécution du rapport de journaux Hello pour la fonction de minuteur hello :</span><span class="sxs-lookup"><span data-stu-id="67a55-225">hello logs for hello timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="67a55-226">Dans la fenêtre de navigateur hello pour la fonction de file d’attente hello, vous pouvez voir chaque message en cours de traitement :</span><span class="sxs-lookup"><span data-stu-id="67a55-226">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="67a55-227">Test d’une fonction avec un code</span><span class="sxs-lookup"><span data-stu-id="67a55-227">Test a function with code</span></span>
<span data-ttu-id="67a55-228">Vous devrez peut-être toocreate un tootest externe de l’application ou infrastructure de vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="67a55-228">You may need toocreate an external application or framework tootest your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="67a55-229">Test d’une fonction de déclenchement HTTP avec un code Node.js</span><span class="sxs-lookup"><span data-stu-id="67a55-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="67a55-230">Vous pouvez utiliser un tooexecute d’application Node.js un tootest de demande HTTP de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="67a55-230">You can use a Node.js app tooexecute an HTTP request tootest your function.</span></span>
<span data-ttu-id="67a55-231">Assurez-vous que tooset :</span><span class="sxs-lookup"><span data-stu-id="67a55-231">Make sure tooset:</span></span>

* <span data-ttu-id="67a55-232">Hello `host` dans l’hôte d’application hello demande options tooyour (fonction).</span><span class="sxs-lookup"><span data-stu-id="67a55-232">hello `host` in hello request options tooyour function app host.</span></span>
* <span data-ttu-id="67a55-233">Le nom de fonction Bonjour `path`.</span><span class="sxs-lookup"><span data-stu-id="67a55-233">Your function name in hello `path`.</span></span>
* <span data-ttu-id="67a55-234">Votre code d’accès (`<your code>`) Bonjour `path`.</span><span class="sxs-lookup"><span data-stu-id="67a55-234">Your access code (`<your code>`) in hello `path`.</span></span>

<span data-ttu-id="67a55-235">Exemple de code :</span><span class="sxs-lookup"><span data-stu-id="67a55-235">Code example:</span></span>

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


<span data-ttu-id="67a55-236">Output:</span><span class="sxs-lookup"><span data-stu-id="67a55-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

<span data-ttu-id="67a55-237">Dans le portail de hello **journaux** sortie de fenêtre, similaire toohello suivant est consigné lors de l’exécution de fonction hello :</span><span class="sxs-lookup"><span data-stu-id="67a55-237">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="67a55-238">Test d’une fonction de déclenchement de file d’attente avec un code : C#</span><span class="sxs-lookup"><span data-stu-id="67a55-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="67a55-239">Nous l’avons mentionné plus haut que vous pouvez tester un déclencheur de la file d’attente à l’aide de code toodrop un message dans votre file d’attente.</span><span class="sxs-lookup"><span data-stu-id="67a55-239">We mentioned earlier that you can test a queue trigger by using code toodrop a message in your queue.</span></span> <span data-ttu-id="67a55-240">Hello suivant l’exemple de code est basé sur le code hello c# présenté dans hello [mise en route avec le stockage de file d’attente Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="67a55-240">hello following example code is based on hello C# code presented in hello [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="67a55-241">Le code des autres langages est également disponible via ce lien.</span><span class="sxs-lookup"><span data-stu-id="67a55-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="67a55-242">tootest ce code dans une application console, vous devez :</span><span class="sxs-lookup"><span data-stu-id="67a55-242">tootest this code in a console app, you must:</span></span>

* <span data-ttu-id="67a55-243">[Configurer votre chaîne de connexion de stockage dans le fichier app.config hello](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="67a55-243">[Configure your storage connection string in hello app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="67a55-244">Passez un `name` et `address` en tant que paramètres toohello application.</span><span class="sxs-lookup"><span data-stu-id="67a55-244">Pass a `name` and `address` as parameters toohello app.</span></span> <span data-ttu-id="67a55-245">Par exemple, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="67a55-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="67a55-246">(Ce code accepte hello nom et adresse d’un nouvel utilisateur en tant qu’arguments de ligne de commande pendant l’exécution.)</span><span class="sxs-lookup"><span data-stu-id="67a55-246">(This code accepts hello name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="67a55-247">Exemple de code C# :</span><span class="sxs-lookup"><span data-stu-id="67a55-247">Example C# code:</span></span>

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

<span data-ttu-id="67a55-248">Dans la fenêtre de navigateur hello pour la fonction de file d’attente hello, vous pouvez voir chaque message en cours de traitement :</span><span class="sxs-lookup"><span data-stu-id="67a55-248">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portail Azure]: https://portal.azure.com
