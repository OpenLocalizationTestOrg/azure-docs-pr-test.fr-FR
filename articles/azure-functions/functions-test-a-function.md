---
title: Test des fonctions Azure Functions | Microsoft Docs
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
ms.openlocfilehash: aca03ba4137893157fcbe6650336782ab88cd234
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="38727-104">Stratégies permettant de tester votre code dans Azure Functions</span><span class="sxs-lookup"><span data-stu-id="38727-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="38727-105">Cette rubrique montre les différentes manières de tester les fonctions, parmi lesquelles les approches générales suivantes :</span><span class="sxs-lookup"><span data-stu-id="38727-105">This topic demonstrates the various ways to test functions, including using the following general approaches:</span></span>

+ <span data-ttu-id="38727-106">Outils basés sur HTTP, comme cURL, Postman et même un navigateur web pour les déclencheurs basés sur le web</span><span class="sxs-lookup"><span data-stu-id="38727-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="38727-107">Explorateur de stockage Azure pour tester les déclencheurs basés sur le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="38727-107">Azure Storage Explorer, to test Azure Storage-based triggers</span></span>
+ <span data-ttu-id="38727-108">Onglet de test dans le portail Azure Functions</span><span class="sxs-lookup"><span data-stu-id="38727-108">Test tab in the Azure Functions portal</span></span>
+ <span data-ttu-id="38727-109">Fonction déclenchée par un minuteur</span><span class="sxs-lookup"><span data-stu-id="38727-109">Timer-triggered function</span></span>
+ <span data-ttu-id="38727-110">Application ou infrastructure de test</span><span class="sxs-lookup"><span data-stu-id="38727-110">Testing application or framework</span></span>

<span data-ttu-id="38727-111">Toutes ces méthodes de test utilisent une fonction de déclencheur HTTP qui accepte les entrées via un paramètre de chaîne de requête ou le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="38727-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or the request body.</span></span> <span data-ttu-id="38727-112">Vous allez créer cette fonction dans la première section.</span><span class="sxs-lookup"><span data-stu-id="38727-112">You create this function in the first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="38727-113">Créer une fonction de test</span><span class="sxs-lookup"><span data-stu-id="38727-113">Create a function for testing</span></span>
<span data-ttu-id="38727-114">Dans ce didacticiel, nous allons utiliser principalement une version légèrement modifiée du modèle de fonction JavaScript HttpTrigger disponible lors de la création d’une fonction.</span><span class="sxs-lookup"><span data-stu-id="38727-114">For most of this tutorial, we use a slightly modified version of the HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="38727-115">Si vous avez besoin d’aide pour créer une fonction, passez en revue ce [didacticiel](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="38727-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="38727-116">Sélectionnez le modèle **HttpTrigger- JavaScript** lors de la création de la fonction de test dans le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="38727-116">Choose the **HttpTrigger- JavaScript** template when creating the test function in the [Azure portal].</span></span>

<span data-ttu-id="38727-117">Le modèle de fonction par défaut est essentiellement une fonction « hello world » qui renvoie le nom à partir du corps de la requête ou du paramètre de chaîne de requête, `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="38727-117">The default function template is basically a "hello world" function that echoes back the name from the request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="38727-118">Nous allons mettre à jour le code pour vous permettre également de fournir le nom et l’adresse en tant que contenu JSON dans le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="38727-118">We'll update the code to also allow you to provide the name and an address as JSON content in the request body.</span></span> <span data-ttu-id="38727-119">La fonction les renvoie ensuite vers le client une fois disponibles.</span><span class="sxs-lookup"><span data-stu-id="38727-119">Then the function echoes these back to the client when available.</span></span>   

<span data-ttu-id="38727-120">Mettez à jour la fonction avec le code suivant que nous allons utiliser pour le test :</span><span class="sxs-lookup"><span data-stu-id="38727-120">Update the function with the following code, which we will use for testing:</span></span>

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
            body: "Please pass a name on the query string or in the request body"
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
        echoString += "\n" + "The address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults to 200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a><span data-ttu-id="38727-121">Test d’une fonction avec des outils</span><span class="sxs-lookup"><span data-stu-id="38727-121">Test a function with tools</span></span>
<span data-ttu-id="38727-122">En dehors du portail Azure, il existe différents outils que vous pouvez utiliser pour déclencher vos fonctions de test.</span><span class="sxs-lookup"><span data-stu-id="38727-122">Outside the Azure portal, there are various tools that you can use to trigger your functions for testing.</span></span> <span data-ttu-id="38727-123">Ceux-ci incluent les outils de test HTTP (basés sur l’interface utilisateur et sur la ligne de commande), les outils d’accès au stockage Azure et même un simple navigateur web.</span><span class="sxs-lookup"><span data-stu-id="38727-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="38727-124">Test avec un navigateur</span><span class="sxs-lookup"><span data-stu-id="38727-124">Test with a browser</span></span>
<span data-ttu-id="38727-125">Le navigateur web fournit un moyen simple de déclencher des fonctions via HTTP.</span><span class="sxs-lookup"><span data-stu-id="38727-125">The web browser is a simple way to trigger functions via HTTP.</span></span> <span data-ttu-id="38727-126">Vous pouvez utiliser un navigateur pour les requêtes GET qui ne nécessitent pas une charge utile du corps et utilisent uniquement des paramètres de chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="38727-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="38727-127">Pour tester la fonction que nous avons définie ci-dessus, copiez l’**URL de la fonction** à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="38727-127">To test the function we defined earlier, copy the **Function Url** from the portal.</span></span> <span data-ttu-id="38727-128">Elle se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="38727-128">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="38727-129">Ajoutez le paramètre `name` à la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="38727-129">Append the `name` parameter to the query string.</span></span> <span data-ttu-id="38727-130">Utilisez un nom réel pour l’espace réservé `<Enter a name here>`.</span><span class="sxs-lookup"><span data-stu-id="38727-130">Use an actual name for the `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="38727-131">Collez l’URL dans votre navigateur. Vous devriez obtenir une réponse similaire à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="38727-131">Paste the URL into your browser, and you should get a response similar to the following.</span></span>

![Capture d’écran de l’onglet du navigateur Chrome avec la réponse de test](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="38727-133">Cet exemple présente le navigateur Chrome, qui encapsule la chaîne renvoyée en XML.</span><span class="sxs-lookup"><span data-stu-id="38727-133">This example is the Chrome browser, which wraps the returned string in XML.</span></span> <span data-ttu-id="38727-134">D’autres navigateurs affichent seulement la valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="38727-134">Other browsers display just the string value.</span></span>

<span data-ttu-id="38727-135">Dans la fenêtre **Journaux** du portail, une sortie similaire à la suivante est journalisée lors de l’exécution de la fonction :</span><span class="sxs-lookup"><span data-stu-id="38727-135">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected to log-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="38727-136">Test avec Postman</span><span class="sxs-lookup"><span data-stu-id="38727-136">Test with Postman</span></span>
<span data-ttu-id="38727-137">L’outil recommandé pour tester la plupart de vos fonctions est Postman, qui s’intègre avec le navigateur Chrome.</span><span class="sxs-lookup"><span data-stu-id="38727-137">The recommended tool to test most of your functions is Postman, which integrates with the Chrome browser.</span></span> <span data-ttu-id="38727-138">Pour installer Postman, consultez [Get Postman](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="38727-138">To install Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="38727-139">Postman permet de contrôler beaucoup plus d’attributs d’une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="38727-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="38727-140">Utilisez l’outil de test HTTP qui vous convient le mieux.</span><span class="sxs-lookup"><span data-stu-id="38727-140">Use the HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="38727-141">Les solutions alternatives à Postman sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="38727-141">Here are some alternatives to Postman:</span></span>  
>
> * [<span data-ttu-id="38727-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="38727-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="38727-143">Paw</span><span class="sxs-lookup"><span data-stu-id="38727-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="38727-144">Pour tester la fonction avec un corps de requête dans Postman :</span><span class="sxs-lookup"><span data-stu-id="38727-144">To test the function with a request body in Postman:</span></span>

1. <span data-ttu-id="38727-145">Démarrez Postman à partir du bouton **Applications** dans le coin supérieur gauche d’une fenêtre de navigateur Chrome.</span><span class="sxs-lookup"><span data-stu-id="38727-145">Start Postman from the **Apps** button in the upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="38727-146">Copiez votre **URL de fonction** et collez-la dans Postman.</span><span class="sxs-lookup"><span data-stu-id="38727-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="38727-147">Elle inclut le paramètre de chaîne de requête de code d’accès.</span><span class="sxs-lookup"><span data-stu-id="38727-147">It includes the access code query string parameter.</span></span>
3. <span data-ttu-id="38727-148">Changez la méthode HTTP en **POST**.</span><span class="sxs-lookup"><span data-stu-id="38727-148">Change the HTTP method to **POST**.</span></span>
4. <span data-ttu-id="38727-149">Cliquez sur **Body** > **raw** et ajoutez un corps de requête JSON similaire au suivant :</span><span class="sxs-lookup"><span data-stu-id="38727-149">Click **Body** > **raw**, and add a JSON request body similar to the following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="38727-150">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="38727-150">Click **Send**.</span></span>

<span data-ttu-id="38727-151">L’illustration suivante montre un exemple de test de fonction d’écho simple dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="38727-151">The following image shows testing the simple echo function example in this tutorial.</span></span>

![Capture d’écran de l’interface utilisateur de Postman](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="38727-153">Dans la fenêtre **Journaux** du portail, une sortie similaire à la suivante est journalisée lors de l’exécution de la fonction :</span><span class="sxs-lookup"><span data-stu-id="38727-153">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-the-command-line"></a><span data-ttu-id="38727-154">Test avec cURL à partir de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="38727-154">Test with cURL from the command line</span></span>
<span data-ttu-id="38727-155">Souvent, lorsque vous testez des logiciels, la ligne de commande suffit pour déboguer votre application.</span><span class="sxs-lookup"><span data-stu-id="38727-155">Often when you're testing software, it's not necessary to look any further than the command line to help debug your application.</span></span> <span data-ttu-id="38727-156">Il en est de même pour les fonctions.</span><span class="sxs-lookup"><span data-stu-id="38727-156">This is no different with testing functions.</span></span> <span data-ttu-id="38727-157">Notez que cURL est disponible par défaut sur les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="38727-157">Note that the cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="38727-158">Sous Windows, vous devez d’abord télécharger et installer [l’outil cURL](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="38727-158">On Windows, you must first download and install the [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="38727-159">Pour tester la fonction que nous avons définie ci-dessus, copiez l’**URL de la fonction** à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="38727-159">To test the function that we defined earlier, copy the **Function URL** from the portal.</span></span> <span data-ttu-id="38727-160">Elle se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="38727-160">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="38727-161">Il s’agit de l’URL qui déclenche votre fonction.</span><span class="sxs-lookup"><span data-stu-id="38727-161">This is the URL for triggering your function.</span></span> <span data-ttu-id="38727-162">Nous pouvons tester cela à l’aide de la commande cURL sur la ligne de commande pour exécuter une requête Get (`-G` ou `--get`) sur la fonction :</span><span class="sxs-lookup"><span data-stu-id="38727-162">Test this by using the cURL command on the command line to make a GET (`-G` or `--get`) request against the function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="38727-163">Cet exemple particulier exige un paramètre de chaîne de requête qui peut être transmis en tant que données (`-d`) dans la commande cURL :</span><span class="sxs-lookup"><span data-stu-id="38727-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in the cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="38727-164">Exécutez la commande. La sortie suivante de la fonction s’affiche sur la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="38727-164">Run the command, and you see the following output of the function on the command line:</span></span>

![Capture d’écran de la sortie de l’invite de commande](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="38727-166">Dans la fenêtre **Journaux** du portail, une sortie similaire à la suivante est journalisée lors de l’exécution de la fonction :</span><span class="sxs-lookup"><span data-stu-id="38727-166">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected to log-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="38727-167">Test d’un déclencheur d’objet blob à l’aide de l’Explorateur de stockage</span><span class="sxs-lookup"><span data-stu-id="38727-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="38727-168">Vous pouvez tester une fonction de déclenchement d’objet blob à l’aide de l’[Explorateur de stockage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="38727-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="38727-169">Dans le [portail Azure] de votre application de fonction, créez une fonction de déclencheur d’objet blob C#, F# ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="38727-169">In the [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="38727-170">Définissez le chemin d’accès à surveiller sur le nom de votre conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="38727-170">Set the path to monitor to the name of your blob container.</span></span> <span data-ttu-id="38727-171">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="38727-171">For example:</span></span>

        files
2. <span data-ttu-id="38727-172">Cliquez sur le bouton **+** pour sélectionner ou créer le compte de stockage que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="38727-172">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="38727-173">Cliquez ensuite sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="38727-173">Then click **Create**.</span></span>
3. <span data-ttu-id="38727-174">Créez un fichier texte contenant le texte suivant et enregistrez-le :</span><span class="sxs-lookup"><span data-stu-id="38727-174">Create a text file with the following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="38727-175">Exécutez l’[Explorateur de stockage Azure](http://storageexplorer.com/) et connectez-vous au conteneur d’objets blob dans le compte de stockage surveillé.</span><span class="sxs-lookup"><span data-stu-id="38727-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect to the blob container in the storage account being monitored.</span></span>
5. <span data-ttu-id="38727-176">Cliquez sur **Charger** pour charger le fichier texte.</span><span class="sxs-lookup"><span data-stu-id="38727-176">Click **Upload** to upload the text file.</span></span>

    ![Capture d’écran de l’explorateur de stockage](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="38727-178">Le code de la fonction de déclenchement d’objets blob par défaut consigne le traitement de l’objet blob dans les journaux :</span><span class="sxs-lookup"><span data-stu-id="38727-178">The default blob trigger function code reports the processing of the blob in the logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected to log-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="38727-179">Test d’une fonction au sein de fonctions</span><span class="sxs-lookup"><span data-stu-id="38727-179">Test a function within functions</span></span>
<span data-ttu-id="38727-180">Le portail Azure Functions est conçu pour vous permettre de tester HTTP et les fonctions déclenchées par minuteur.</span><span class="sxs-lookup"><span data-stu-id="38727-180">The Azure Functions portal is designed to let you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="38727-181">Vous pouvez également créer des fonctions pour déclencher d’autres fonctions que vous testez.</span><span class="sxs-lookup"><span data-stu-id="38727-181">You can also create functions to trigger other functions that you are testing.</span></span>

### <a name="test-with-the-functions-portal-run-button"></a><span data-ttu-id="38727-182">Test avec le bouton d’exécution du portail Functions</span><span class="sxs-lookup"><span data-stu-id="38727-182">Test with the Functions portal Run button</span></span>
<span data-ttu-id="38727-183">Le portail fournit un bouton **Exécuter** qui vous permet d’effectuer des tests limités.</span><span class="sxs-lookup"><span data-stu-id="38727-183">The portal provides a **Run** button that you can use to do some limited testing.</span></span> <span data-ttu-id="38727-184">Vous pouvez fournir un corps de requête à l’aide du bouton mais vous ne pouvez pas fournir de paramètres de chaîne de requête ou mettre à jour des en-têtes de demande.</span><span class="sxs-lookup"><span data-stu-id="38727-184">You can provide a request body by using the button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="38727-185">Testez la fonction de déclenchement HTTP que nous avons créée précédemment en ajoutant une chaîne JSON similaire à la suivante dans le champ **Corps de requête**,</span><span class="sxs-lookup"><span data-stu-id="38727-185">Test the HTTP trigger function we created earlier by adding a JSON string similar to the following in the **Request body** field.</span></span> <span data-ttu-id="38727-186">puis cliquez sur le bouton **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="38727-186">Then click the **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="38727-187">Dans la fenêtre **Journaux** du portail, une sortie similaire à la suivante est journalisée lors de l’exécution de la fonction :</span><span class="sxs-lookup"><span data-stu-id="38727-187">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="38727-188">Test avec un déclencheur de minuteur</span><span class="sxs-lookup"><span data-stu-id="38727-188">Test with a timer trigger</span></span>
<span data-ttu-id="38727-189">Certaines fonctions ne peuvent pas être correctement testées avec les outils mentionnés précédemment.</span><span class="sxs-lookup"><span data-stu-id="38727-189">Some functions can't be adequately tested with the tools mentioned previously.</span></span> <span data-ttu-id="38727-190">C’est le cas, par exemple, d’une fonction de déclenchement de file d’attente qui s’exécute lorsqu’un message est déposé dans [Stockage File d’attente Azure](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="38727-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="38727-191">Vous pouvez toujours écrire du code pour déposer un message dans votre file d’attente. Vous trouverez ci-après un exemple appliqué à un projet de console.</span><span class="sxs-lookup"><span data-stu-id="38727-191">You can always write code to drop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="38727-192">Toutefois, une autre approche vous permet de tester des fonctions directement.</span><span class="sxs-lookup"><span data-stu-id="38727-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="38727-193">Vous pouvez utiliser un déclencheur de minuteur configuré avec une liaison de sortie de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="38727-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="38727-194">Ce code de déclenchement du minuteur peut ensuite écrire des messages test dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="38727-194">That timer trigger code can then write the test messages to the queue.</span></span> <span data-ttu-id="38727-195">Cette section présente un exemple.</span><span class="sxs-lookup"><span data-stu-id="38727-195">This section walks through an example.</span></span>

<span data-ttu-id="38727-196">Pour des informations plus détaillées sur l’utilisation des liaisons avec les fonctions Azure, consultez la rubrique [Azure Functions developer reference](functions-reference.md)(Référence pour les développeurs Azure Functions).</span><span class="sxs-lookup"><span data-stu-id="38727-196">For more in-depth information on using bindings with Azure Functions, see the [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="38727-197">Créer un déclencheur de file d’attente pour le test</span><span class="sxs-lookup"><span data-stu-id="38727-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="38727-198">Pour illustrer cette approche, nous allons d’abord créer une fonction de déclenchement de file d’attente que nous voulons tester pour une file d’attente nommée `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="38727-198">To demonstrate this approach, we first create a queue trigger function that we want to test for a queue named `queue-newusers`.</span></span> <span data-ttu-id="38727-199">Cette fonction traite les informations de nom et d’adresse d’un nouvel utilisateur déposées dans Stockage File d'attente.</span><span class="sxs-lookup"><span data-stu-id="38727-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="38727-200">Si vous utilisez un nom de file d’attente différent, assurez-vous que le nom que vous utilisez est conforme aux règles d’ [affectation de noms pour les files d’attente et les métadonnées](https://msdn.microsoft.com/library/dd179349.aspx) .</span><span class="sxs-lookup"><span data-stu-id="38727-200">If you use a different queue name, make sure the name you use conforms to the [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="38727-201">Sinon, vous recevez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="38727-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="38727-202">Dans le [portail Azure] de votre application de fonction, cliquez sur **Nouvelle fonction** > **QueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="38727-202">In the [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="38727-203">Entrez le nom de file d’attente que la fonction de file d’attente doit surveiller :</span><span class="sxs-lookup"><span data-stu-id="38727-203">Enter the queue name to be monitored by the queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="38727-204">Cliquez sur le bouton **+** pour sélectionner ou créer le compte de stockage que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="38727-204">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="38727-205">Cliquez ensuite sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="38727-205">Then click **Create**.</span></span>
4. <span data-ttu-id="38727-206">Laissez cette fenêtre de navigateur du portail ouverte afin de surveiller les entrées de journal du code de modèle de fonction de file d’attente par défaut.</span><span class="sxs-lookup"><span data-stu-id="38727-206">Leave this portal browser window open, so you can monitor the log entries for the default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-to-drop-a-message-in-the-queue"></a><span data-ttu-id="38727-207">Créer un déclencheur de minuteur pour déposer un message dans la file d’attente</span><span class="sxs-lookup"><span data-stu-id="38727-207">Create a timer trigger to drop a message in the queue</span></span>
1. <span data-ttu-id="38727-208">Ouvrez le [portail Azure] dans une nouvelle fenêtre de navigateur et accédez à votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="38727-208">Open the [Azure portal] in a new browser window, and navigate to your function app.</span></span>
2. <span data-ttu-id="38727-209">Cliquez sur **Nouvelle fonction** > **TimerTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="38727-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="38727-210">Entrez une expression cron pour définir la fréquence à laquelle le code du minuteur exécutera le test de votre fonction de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="38727-210">Enter a cron expression to set how often the timer code tests your queue function.</span></span> <span data-ttu-id="38727-211">Cliquez ensuite sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="38727-211">Then click **Create**.</span></span> <span data-ttu-id="38727-212">Si vous souhaitez que le test s’exécute toutes les 30 secondes, vous pouvez utiliser l’[expression CRON](https://wikipedia.org/wiki/Cron#CRON_expression)suivante :</span><span class="sxs-lookup"><span data-stu-id="38727-212">If you want the test to run every 30 seconds, you can use the following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="38727-213">Cliquez sur l’onglet **Intégrer** pour votre nouveau déclencheur de minuteur.</span><span class="sxs-lookup"><span data-stu-id="38727-213">Click the **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="38727-214">Sous **Sortie**, cliquez sur le bouton **+ Nouvelle sortie**.</span><span class="sxs-lookup"><span data-stu-id="38727-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="38727-215">Puis cliquez sur **File d’attente** et sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="38727-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="38727-216">Notez le nom que vous utilisez pour l’**objet de message de file d’attente**.</span><span class="sxs-lookup"><span data-stu-id="38727-216">Note the name you use for the **queue message object**.</span></span> <span data-ttu-id="38727-217">Il est utilisé dans le code de fonction du minuteur.</span><span class="sxs-lookup"><span data-stu-id="38727-217">You use this in the timer function code.</span></span>

        myQueue
6. <span data-ttu-id="38727-218">Entrez le nom de la file d’attente vers laquelle le message est envoyé :</span><span class="sxs-lookup"><span data-stu-id="38727-218">Enter the queue name where the message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="38727-219">Cliquez sur le bouton **+** pour sélectionner le compte de stockage que vous avez utilisé précédemment avec le déclencheur de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="38727-219">Click the **+** button to select the storage account you used previously with the queue trigger.</span></span> <span data-ttu-id="38727-220">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="38727-220">Then click **Save**.</span></span>
8. <span data-ttu-id="38727-221">Cliquez sur l’onglet **Développer** de votre déclencheur de minuteur.</span><span class="sxs-lookup"><span data-stu-id="38727-221">Click the **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="38727-222">Vous pouvez utiliser le code suivant pour la fonction de minuteur C# dans la mesure où vous avez utilisé le même nom d’objet de message de file d’attente que celui illustré précédemment.</span><span class="sxs-lookup"><span data-stu-id="38727-222">You can use the following code for the C# timer function, as long as you used the same queue message object name shown earlier.</span></span> <span data-ttu-id="38727-223">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="38727-223">Then click **Save**.</span></span>

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

<span data-ttu-id="38727-224">À ce stade, la fonction de minuteur C# s’exécute toutes les 30 secondes si vous avez utilisé l’exemple d’expression cron.</span><span class="sxs-lookup"><span data-stu-id="38727-224">At this point, the C# timer function executes every 30 seconds if you used the example cron expression.</span></span> <span data-ttu-id="38727-225">Les journaux de la fonction de minuteur consignent chaque exécution :</span><span class="sxs-lookup"><span data-stu-id="38727-225">The logs for the timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="38727-226">Dans la fenêtre du navigateur de la fonction de file d’attente, vous pouvez voir chaque message traité :</span><span class="sxs-lookup"><span data-stu-id="38727-226">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="38727-227">Test d’une fonction avec un code</span><span class="sxs-lookup"><span data-stu-id="38727-227">Test a function with code</span></span>
<span data-ttu-id="38727-228">Vous pouvez avoir besoin de créer une application ou une infrastructure externe pour tester vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="38727-228">You may need to create an external application or framework to test your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="38727-229">Test d’une fonction de déclenchement HTTP avec un code Node.js</span><span class="sxs-lookup"><span data-stu-id="38727-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="38727-230">Vous pouvez utiliser une application Node.js pour exécuter une requête HTTP afin de tester votre fonction.</span><span class="sxs-lookup"><span data-stu-id="38727-230">You can use a Node.js app to execute an HTTP request to test your function.</span></span>
<span data-ttu-id="38727-231">Vous devez définir :</span><span class="sxs-lookup"><span data-stu-id="38727-231">Make sure to set:</span></span>

* <span data-ttu-id="38727-232">Le paramètre `host` dans les options de requête sur l’hôte de votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="38727-232">The `host` in the request options to your function app host.</span></span>
* <span data-ttu-id="38727-233">Votre nom de fonction dans le paramètre `path`.</span><span class="sxs-lookup"><span data-stu-id="38727-233">Your function name in the `path`.</span></span>
* <span data-ttu-id="38727-234">Votre code d’accès (`<your code>`) dans le paramètre `path`.</span><span class="sxs-lookup"><span data-stu-id="38727-234">Your access code (`<your code>`) in the `path`.</span></span>

<span data-ttu-id="38727-235">Exemple de code :</span><span class="sxs-lookup"><span data-stu-id="38727-235">Code example:</span></span>

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


<span data-ttu-id="38727-236">Output:</span><span class="sxs-lookup"><span data-stu-id="38727-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    The address you provided is Dallas, T.X. 75201

<span data-ttu-id="38727-237">Dans la fenêtre **Journaux** du portail, une sortie similaire à la suivante est journalisée lors de l’exécution de la fonction :</span><span class="sxs-lookup"><span data-stu-id="38727-237">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="38727-238">Test d’une fonction de déclenchement de file d’attente avec un code : C#</span><span class="sxs-lookup"><span data-stu-id="38727-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="38727-239">Nous avons mentionné plus tôt que vous pouvez tester un déclencheur de file d’attente à l’aide d’un code pour déposer un message dans votre file d’attente.</span><span class="sxs-lookup"><span data-stu-id="38727-239">We mentioned earlier that you can test a queue trigger by using code to drop a message in your queue.</span></span> <span data-ttu-id="38727-240">L’exemple de code suivant est basé sur le code C# présenté dans le didacticiel [Prise en main du Stockage File d'attente Azure](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="38727-240">The following example code is based on the C# code presented in the [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="38727-241">Le code des autres langages est également disponible via ce lien.</span><span class="sxs-lookup"><span data-stu-id="38727-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="38727-242">Pour tester ce code dans une application de console, vous devez :</span><span class="sxs-lookup"><span data-stu-id="38727-242">To test this code in a console app, you must:</span></span>

* <span data-ttu-id="38727-243">[Configurer votre chaîne de connexion du stockage dans le fichier app.config](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="38727-243">[Configure your storage connection string in the app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="38727-244">Transmettez les paramètres `name` et `address` à l’application.</span><span class="sxs-lookup"><span data-stu-id="38727-244">Pass a `name` and `address` as parameters to the app.</span></span> <span data-ttu-id="38727-245">Par exemple, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="38727-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="38727-246">(Ce code accepte le nom et l’adresse d’un nouvel utilisateur en tant qu’arguments de ligne de commande pendant l’exécution.)</span><span class="sxs-lookup"><span data-stu-id="38727-246">(This code accepts the name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="38727-247">Exemple de code C# :</span><span class="sxs-lookup"><span data-stu-id="38727-247">Example C# code:</span></span>

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

    // Create the queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference to a queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create the queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it to the queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message to " + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

<span data-ttu-id="38727-248">Dans la fenêtre du navigateur de la fonction de file d’attente, vous pouvez voir chaque message traité :</span><span class="sxs-lookup"><span data-stu-id="38727-248">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portail Azure]: https://portal.azure.com
