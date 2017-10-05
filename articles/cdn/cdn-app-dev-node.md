---
title: "Prise en main du kit de développement logiciel Azure CDN pour Node.js | Microsoft Docs"
description: "Apprenez à écrire des applications Node.js pour gérer Azure CDN."
services: cdn
documentationcenter: nodejs
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c4bb6a61-de3d-4f0c-9dca-202554c43dfa
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 46ae8cd9775432d126cbde856c1fb06ea319297e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="184fa-103">Prise en main du développement Azure CDN</span><span class="sxs-lookup"><span data-stu-id="184fa-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="184fa-104">Node.JS</span><span class="sxs-lookup"><span data-stu-id="184fa-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="184fa-105">.NET</span><span class="sxs-lookup"><span data-stu-id="184fa-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="184fa-106">Vous pouvez utiliser le [kit de développement logiciel Azure CDN pour Node.js](https://www.npmjs.com/package/azure-arm-cdn) pour automatiser la création et la gestion des points de terminaison et profils CDN.</span><span class="sxs-lookup"><span data-stu-id="184fa-106">You can use the [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="184fa-107">Ce didacticiel présente la création d’une application console Node.js simple, qui exécute plusieurs des opérations disponibles.</span><span class="sxs-lookup"><span data-stu-id="184fa-107">This tutorial walks through the creation of a simple Node.js console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="184fa-108">Il n’a pas vocation à décrire en détail tous les aspects du kit de développement logiciel Azure CDN pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="184fa-108">This tutorial is not intended to describe all aspects of the Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="184fa-109">Pour suivre ce didacticiel, vous devez avoir au préalable installé et configuré [Node.js](http://www.nodejs.org) **4.x.x** ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="184fa-109">To complete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="184fa-110">Vous pouvez utiliser n’importe quel éditeur de texte pour créer votre application Node.js.</span><span class="sxs-lookup"><span data-stu-id="184fa-110">You can use any text editor you want to create your Node.js application.</span></span>  <span data-ttu-id="184fa-111">Pour écrire ce didacticiel, j’ai utilisé [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="184fa-111">To write this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="184fa-112">Le [projet achevé de ce didacticiel](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) est disponible en téléchargement sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="184fa-112">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="184fa-113">Créer votre projet et ajouter des dépendances NPM</span><span class="sxs-lookup"><span data-stu-id="184fa-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="184fa-114">Maintenant que nous avons créé un groupe de ressources pour nos profils CDN et autorisé l’application Azure AD à gérer les points de terminaison et profils CDN au sein de ce groupe, nous pouvons créer notre application.</span><span class="sxs-lookup"><span data-stu-id="184fa-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="184fa-115">Créez un dossier pour stocker votre application.</span><span class="sxs-lookup"><span data-stu-id="184fa-115">Create a folder to store your application.</span></span>  <span data-ttu-id="184fa-116">À partir d’une console contenant les outils Node.js dans votre chemin d’accès actuel, définissez votre emplacement actuel vers ce nouveau dossier et initialisez votre projet en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="184fa-116">From a console with the Node.js tools in your current path, set your current location to this new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="184fa-117">Vous obtenez alors une série de questions qui vous permettront d’initialiser votre projet.</span><span class="sxs-lookup"><span data-stu-id="184fa-117">You will then be presented a series of questions to initialize your project.</span></span>  <span data-ttu-id="184fa-118">Comme **point d’entrée**, ce didacticiel utilise *app.js*.</span><span class="sxs-lookup"><span data-stu-id="184fa-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="184fa-119">Vous pouvez voir mes autres choix dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="184fa-119">You can see my other choices in the following example.</span></span>

![sortie init NPM](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="184fa-121">Notre projet est maintenant initialisé avec un fichier *packages.json* .</span><span class="sxs-lookup"><span data-stu-id="184fa-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="184fa-122">Notre projet va utiliser certaines bibliothèques Azure contenues dans des packages NPM.</span><span class="sxs-lookup"><span data-stu-id="184fa-122">Our project is going to use some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="184fa-123">Nous allons utiliser le Runtime client Azure pour Node.js (ms-rest-azure) et la bibliothèque cliente Azure CDN pour Node.js (azure-arm-cd).</span><span class="sxs-lookup"><span data-stu-id="184fa-123">We'll use the Azure Client Runtime for Node.js (ms-rest-azure) and the Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="184fa-124">Ajoutons-les au projet sous forme de dépendances.</span><span class="sxs-lookup"><span data-stu-id="184fa-124">Let's add those to the project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="184fa-125">Une fois les packages installés, le fichier *package.json* doit se présenter comme dans cet exemple (les numéros de version peuvent varier) :</span><span class="sxs-lookup"><span data-stu-id="184fa-125">After the packages are done installing, the *package.json* file should look similar to this example (version numbers may differ):</span></span>

``` json
{
  "name": "cdn_node",
  "version": "1.0.0",
  "description": "Azure CDN Node.js tutorial project",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Cam Soper",
  "license": "MIT",
  "dependencies": {
    "azure-arm-cdn": "^0.2.1",
    "ms-rest-azure": "^1.14.4"
  }
}
```

<span data-ttu-id="184fa-126">Enfin, à l’aide de votre éditeur de texte, créez un fichier texte vide et enregistrez-le à la racine de votre dossier de projet en tant que *app.js*.</span><span class="sxs-lookup"><span data-stu-id="184fa-126">Finally, using your text editor, create a blank text file and save it in the root of our project folder as *app.js*.</span></span>  <span data-ttu-id="184fa-127">Nous pouvons maintenant commencer à écrire du code.</span><span class="sxs-lookup"><span data-stu-id="184fa-127">We're now ready to begin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="184fa-128">Paramètres « require », constantes, authentification et structure</span><span class="sxs-lookup"><span data-stu-id="184fa-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="184fa-129">Ouvrez *app.js* dans votre éditeur pour commencer à écrire la structure de base de notre programme.</span><span class="sxs-lookup"><span data-stu-id="184fa-129">With *app.js* open in our editor, let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="184fa-130">Ajoutez les paramètres « require » pour nos packages NPM au début du code, comme suit :</span><span class="sxs-lookup"><span data-stu-id="184fa-130">Add the "requires" for our NPM packages at the top with the following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="184fa-131">Nous devons définir certaines constantes que nos méthodes utiliseront.</span><span class="sxs-lookup"><span data-stu-id="184fa-131">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="184fa-132">Ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="184fa-132">Add the following.</span></span>  <span data-ttu-id="184fa-133">Veillez à remplacer les espaces réservés, notamment les **&lt;éléments entre chevrons&gt;**, par vos propres valeurs, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="184fa-133">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
    ``` javascript
    //Tenant app constants
    const clientId = "<YOUR CLIENT ID>";
    const clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    const tenantId = "<YOUR TENANT ID>";
   
    //Application constants
    const subscriptionId = "<YOUR SUBSCRIPTION ID>";
    const resourceGroupName = "CdnConsoleTutorial";
    const resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. <span data-ttu-id="184fa-134">Nous allons maintenant instancier le client de gestion CDN et lui donner nos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="184fa-134">Next, we'll instantiate the CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="184fa-135">Si vous utilisez une authentification d’utilisateurs individuels, ces deux lignes aura un aspect légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="184fa-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="184fa-136">N’utilisez ce code que si vous privilégiez l’authentification d’utilisateurs individuels au principal du service.</span><span class="sxs-lookup"><span data-stu-id="184fa-136">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="184fa-137">Veillez à protéger vos informations d’identification d’utilisateurs individuels et à ne pas les divulguer.</span><span class="sxs-lookup"><span data-stu-id="184fa-137">Be careful to guard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="184fa-138">Veillez à remplacer les éléments entre **&lt;chevrons&gt;** par les informations appropriées.</span><span class="sxs-lookup"><span data-stu-id="184fa-138">Be sure to replace the items in **&lt;angle brackets&gt;** with the correct information.</span></span>  <span data-ttu-id="184fa-139">Pour `<redirect URI>`, utilisez l’URI de redirection que vous avez entré lorsque vous avez inscrit l’application dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="184fa-139">For `<redirect URI>`, use the redirect URI you entered when you registered the application in Azure AD.</span></span>
4. <span data-ttu-id="184fa-140">Notre application console Node.js va prendre quelques paramètres de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="184fa-140">Our Node.js console application is going to take some command-line parameters.</span></span>  <span data-ttu-id="184fa-141">Vérifions qu’au moins un des paramètres a été transmis.</span><span class="sxs-lookup"><span data-stu-id="184fa-141">Let's validate that at least one parameter was passed.</span></span>
   
   ```javascript
   //Collect command-line parameters
   var parms = process.argv.slice(2);
   
   //Do we have parameters?
   if(parms == null || parms.length == 0)
   {
       console.log("Not enough parameters!");
       console.log("Valid commands are list, delete, create, and purge.");
       process.exit(1);
   }
   ```
5. <span data-ttu-id="184fa-142">Cela nous amène à la partie principale de notre programme, où nous créons des branches vers d’autres fonctions dépendant des paramètres qui ont été transmis.</span><span class="sxs-lookup"><span data-stu-id="184fa-142">That brings us to the main part of our program, where we branch off to other functions based on what parameters were passed.</span></span>
   
    ```javascript
    switch(parms[0].toLowerCase())
    {
        case "list":
            cdnList();
            break;
   
        case "create":
            cdnCreate();
            break;
   
        case "delete":
            cdnDelete();
            break;
   
        case "purge":
            cdnPurge();
            break;
   
        default:
            console.log("Valid commands are list, delete, create, and purge.");
            process.exit(1);
    }
    ```
6. <span data-ttu-id="184fa-143">À plusieurs endroits de notre programme, nous devons nous assurer que le nombre de paramètres approprié a été transmis et afficher une aide si ces paramètres nous semblent incorrects.</span><span class="sxs-lookup"><span data-stu-id="184fa-143">At several places in our program, we'll need to make sure the right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="184fa-144">Nous allons créer des fonctions pour effectuer cette vérification.</span><span class="sxs-lookup"><span data-stu-id="184fa-144">Let's create functions to do that.</span></span>
   
   ```javascript
   function requireParms(parmCount) {
       if(parms.length < parmCount) {
           usageHelp(parms[0].toLowerCase());
           process.exit(1);
       }
   }
   
   function usageHelp(cmd) {
       console.log("Usage for " + cmd + ":");
       switch(cmd)
       {
           case "list":
               console.log("list profiles");
               console.log("list endpoints <profile name>");
               break;
   
           case "create":
               console.log("create profile <profile name>");
               console.log("create endpoint <profile name> <endpoint name> <origin hostname>");
               break;
   
           case "delete":
               console.log("delete profile <profile name>");
               console.log("delete endpoint <profile name> <endpoint name>");
               break;
   
           case "purge":
               console.log("purge <profile name> <endpoint name> <path>");
               break;
   
           default:
               console.log("Invalid command.");
       }
   }
   ```
7. <span data-ttu-id="184fa-145">Les fonctions que nous allons utiliser sur le client de gestion CDN sont asynchrones, ce qui signifie qu’elles ont besoin d’une méthode pour relancer un appel à la fin de leur exécution.</span><span class="sxs-lookup"><span data-stu-id="184fa-145">Finally, the functions we'll be using on the CDN management client are asynchronous, so they need a method to call back when they're done.</span></span>  <span data-ttu-id="184fa-146">Nous allons en créer une qui permet d’afficher la sortie à partir du client de gestion CDN (le cas échéant) et de fermer le programme correctement.</span><span class="sxs-lookup"><span data-stu-id="184fa-146">Let's make one that can display the output from the CDN management client (if any) and exit the program gracefully.</span></span>
   
    ```javascript
    function callback(err, result, request, response) {
        if (err) {
            console.log(err);
            process.exit(1);
        } else {
            console.log((result == null) ? "Done!" : result);
            process.exit(0);
        }
    }
    ```

<span data-ttu-id="184fa-147">Maintenant que nous avons écrit la structure de base de notre programme, nous devons créer les fonctions appelées en fonction de nos paramètres.</span><span class="sxs-lookup"><span data-stu-id="184fa-147">Now that the basic structure of our program is written, we should create the functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="184fa-148">Répertorier les profils CDN et points de terminaison</span><span class="sxs-lookup"><span data-stu-id="184fa-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="184fa-149">Commençons par répertorier les profils et les points de terminaison existants.</span><span class="sxs-lookup"><span data-stu-id="184fa-149">Let's start with code to list our existing profiles and endpoints.</span></span>  <span data-ttu-id="184fa-150">Les commentaires de mon code indiquent la syntaxe appropriée pour nous permettre de savoir quel paramètre va à quel emplacement.</span><span class="sxs-lookup"><span data-stu-id="184fa-150">My code comments provide the expected syntax so we know where each parameter goes.</span></span>

```javascript
// list profiles
// list endpoints <profile name>
function cdnList(){
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profiles":
            console.log("Listing profiles...");
            cdnClient.profiles.listByResourceGroup(resourceGroupName, callback);
            break;

        case "endpoints":
            requireParms(3);
            console.log("Listing endpoints...");
            cdnClient.endpoints.listByProfile(parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="184fa-151">Créer des profils CDN et des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="184fa-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="184fa-152">Nous allons ensuite écrire des fonctions permettant de créer des profils et des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="184fa-152">Next, we'll write the functions to create profiles and endpoints.</span></span>

```javascript
function cdnCreate() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profile":
            cdnCreateProfile();
            break;

        case "endpoint":
            cdnCreateEndpoint();
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}

// create profile <profile name>
function cdnCreateProfile() {
    requireParms(3);
    console.log("Creating profile...");
    var standardCreateParameters = {
        location: resourceLocation,
        sku: {
            name: 'Standard_Verizon'
        }
    };

    cdnClient.profiles.create(parms[2], standardCreateParameters, resourceGroupName, callback);
}

// create endpoint <profile name> <endpoint name> <origin hostname>        
function cdnCreateEndpoint() {
    requireParms(5);
    console.log("Creating endpoint...");
    var endpointProperties = {
        location: resourceLocation,
        origins: [{
            name: parms[4],
            hostName: parms[4]
        }]
    };

    cdnClient.endpoints.create(parms[3], endpointProperties, parms[2], resourceGroupName, callback);
}
```

## <a name="purge-an-endpoint"></a><span data-ttu-id="184fa-153">Vider un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="184fa-153">Purge an endpoint</span></span>
<span data-ttu-id="184fa-154">En supposant que le point de terminaison a été créé, nous allons certainement chercher à vider le contenu du programme dans notre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="184fa-154">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="184fa-155">Supprimer des profils CDN et des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="184fa-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="184fa-156">La dernière fonction que nous allons ajouter permet de supprimer les points de terminaison et les profils.</span><span class="sxs-lookup"><span data-stu-id="184fa-156">The last function we will include deletes endpoints and profiles.</span></span>

```javascript
function cdnDelete() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        // delete profile <profile name>
        case "profile":
            requireParms(3);
            console.log("Deleting profile...");
            cdnClient.profiles.deleteIfExists(parms[2], resourceGroupName, callback);
            break;

        // delete endpoint <profile name> <endpoint name>
        case "endpoint":
            requireParms(4);
            console.log("Deleting endpoint...");
            cdnClient.endpoints.deleteIfExists(parms[3], parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="running-the-program"></a><span data-ttu-id="184fa-157">Exécution du programme</span><span class="sxs-lookup"><span data-stu-id="184fa-157">Running the program</span></span>
<span data-ttu-id="184fa-158">Nous pouvons à présent exécuter notre programme Node.js à l’aide de notre débogueur favori ou sur la console.</span><span class="sxs-lookup"><span data-stu-id="184fa-158">We can now execute our Node.js program using our favorite debugger or at the console.</span></span>

> [!TIP]
> <span data-ttu-id="184fa-159">Si vous utilisez Visual Studio Code comme débogueur, vous devez configurer votre environnement pour transmettre les paramètres de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="184fa-159">If you're using Visual Studio Code as your debugger, you'll need to set up your environment to pass in the command-line parameters.</span></span>  <span data-ttu-id="184fa-160">Visual Studio Code utilise le fichier **lanuch.json** à cette fin.</span><span class="sxs-lookup"><span data-stu-id="184fa-160">Visual Studio Code does this in the **lanuch.json** file.</span></span>  <span data-ttu-id="184fa-161">Recherchez une propriété nommée **args** et ajoutez un tableau de valeurs de chaîne pour vos paramètres, pour obtenir un résultat semblable à ce qui suit : `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="184fa-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar to this:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="184fa-162">Commençons par répertorier nos profils.</span><span class="sxs-lookup"><span data-stu-id="184fa-162">Let's start by listing our profiles.</span></span>

![Liste des profils](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="184fa-164">Nous obtenons un tableau vide.</span><span class="sxs-lookup"><span data-stu-id="184fa-164">We got back an empty array.</span></span>  <span data-ttu-id="184fa-165">Cela est tout à fait normal puisque nous n’avons aucun profil dans notre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="184fa-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="184fa-166">Créons donc maintenant un profil.</span><span class="sxs-lookup"><span data-stu-id="184fa-166">Let's create a profile now.</span></span>

![Création d’un profil](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="184fa-168">À présent, ajoutons un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="184fa-168">Now, let's add an endpoint.</span></span>

![Création d’un point de terminaison](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="184fa-170">Pour finir, nous allons supprimer notre profil.</span><span class="sxs-lookup"><span data-stu-id="184fa-170">Finally, let's delete our profile.</span></span>

![Suppression d’un profil](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="184fa-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="184fa-172">Next Steps</span></span>
<span data-ttu-id="184fa-173">Pour voir le projet achevé obtenu à partir de cette procédure pas à pas, [téléchargez l’exemple](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="184fa-173">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="184fa-174">Pour voir la référence du kit de développement logiciel Azure CDN pour Node.js, consultez cette [référence](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="184fa-174">To see the reference for the Azure CDN SDK for Node.js, view the [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="184fa-175">Pour rechercher une documentation supplémentaire sur le kit de développement logiciel Azure pour Node.js, consultez la [référence complète](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="184fa-175">To find additional documentation on the Azure SDK for Node.js, view the [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="184fa-176">Gérez vos ressources CDN avec [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="184fa-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

