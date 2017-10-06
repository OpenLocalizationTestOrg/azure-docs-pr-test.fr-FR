---
title: aaaGet main hello Azure CDN SDK pour Node.js | Documents Microsoft
description: "Découvrez comment toowrite Node.js applications toomanage CDN Azure."
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
ms.openlocfilehash: 6c805e5fb8e0b471e8b248cb2f4b29efd6c85940
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="0b090-103">Prise en main du développement Azure CDN</span><span class="sxs-lookup"><span data-stu-id="0b090-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b090-104">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0b090-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="0b090-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0b090-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="0b090-106">Vous pouvez utiliser hello [Azure CDN SDK pour Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate création et la gestion des profils CDN et des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="0b090-106">You can use hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="0b090-107">Ce didacticiel guide dans la création d’une application de console Node.js simple qui illustre plusieurs opérations disponibles de hello hello.</span><span class="sxs-lookup"><span data-stu-id="0b090-107">This tutorial walks through hello creation of a simple Node.js console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="0b090-108">Ce didacticiel n’est pas conçu toodescribe tous les aspects de hello Azure CDN SDK pour Node.js en détail.</span><span class="sxs-lookup"><span data-stu-id="0b090-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="0b090-109">toocomplete ce didacticiel, vous devez déjà avoir [Node.js](http://www.nodejs.org) **versions4.x.x** ou version ultérieure installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="0b090-109">toocomplete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="0b090-110">Vous pouvez utiliser n’importe quel éditeur de texte vous souhaitez toocreate votre application Node.js.</span><span class="sxs-lookup"><span data-stu-id="0b090-110">You can use any text editor you want toocreate your Node.js application.</span></span>  <span data-ttu-id="0b090-111">toowrite ce didacticiel, j’ai utilisé [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="0b090-111">toowrite this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="0b090-112">Hello [projet achevé de ce didacticiel](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) est disponible pour téléchargement sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="0b090-112">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="0b090-113">Créer votre projet et ajouter des dépendances NPM</span><span class="sxs-lookup"><span data-stu-id="0b090-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="0b090-114">Maintenant que nous avons créé un groupe de ressources pour les profils de notre CDN et donné notre profils CDN toomanage d’autorisation d’application Azure AD et les points de terminaison de ce groupe, nous pouvons commencer à créer notre application.</span><span class="sxs-lookup"><span data-stu-id="0b090-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="0b090-115">Créer un dossier toostore votre application.</span><span class="sxs-lookup"><span data-stu-id="0b090-115">Create a folder toostore your application.</span></span>  <span data-ttu-id="0b090-116">À partir d’une console avec hello Node.js tools dans votre chemin d’accès actuel, définir votre dossier de nouveau toothis emplacement actuel et initialiser votre projet en exécutant :</span><span class="sxs-lookup"><span data-stu-id="0b090-116">From a console with hello Node.js tools in your current path, set your current location toothis new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="0b090-117">Vous serez ensuite présenté à une série de questions tooinitialize votre projet.</span><span class="sxs-lookup"><span data-stu-id="0b090-117">You will then be presented a series of questions tooinitialize your project.</span></span>  <span data-ttu-id="0b090-118">Comme **point d’entrée**, ce didacticiel utilise *app.js*.</span><span class="sxs-lookup"><span data-stu-id="0b090-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="0b090-119">Vous pouvez afficher mes autres choix Bonjour l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="0b090-119">You can see my other choices in hello following example.</span></span>

![sortie init NPM](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="0b090-121">Notre projet est maintenant initialisé avec un fichier *packages.json* .</span><span class="sxs-lookup"><span data-stu-id="0b090-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="0b090-122">Notre projet va toouse certaines bibliothèques Azure contenues dans des packages NPM.</span><span class="sxs-lookup"><span data-stu-id="0b090-122">Our project is going toouse some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="0b090-123">Nous allons utiliser hello exécution du Client Azure pour Node.js (ms-rest-azure) et hello bibliothèque cliente de CDN Azure pour Node.js (azure cd arm).</span><span class="sxs-lookup"><span data-stu-id="0b090-123">We'll use hello Azure Client Runtime for Node.js (ms-rest-azure) and hello Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="0b090-124">Vous allez ajouter ces projets toohello en tant que dépendances.</span><span class="sxs-lookup"><span data-stu-id="0b090-124">Let's add those toohello project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="0b090-125">Hello packages sont effectuées après l’installation, hello *package.json* fichier doit se présenter exemple toothis similaire (version nombres peuvent varier) :</span><span class="sxs-lookup"><span data-stu-id="0b090-125">After hello packages are done installing, hello *package.json* file should look similar toothis example (version numbers may differ):</span></span>

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

<span data-ttu-id="0b090-126">Enfin, à l’aide de votre éditeur de texte, créez un fichier texte vide et l’enregistrer dans le dossier de projet en tant que racine hello *app.js*.</span><span class="sxs-lookup"><span data-stu-id="0b090-126">Finally, using your text editor, create a blank text file and save it in hello root of our project folder as *app.js*.</span></span>  <span data-ttu-id="0b090-127">Nous sommes maintenant prêt toobegin l’écriture de code.</span><span class="sxs-lookup"><span data-stu-id="0b090-127">We're now ready toobegin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="0b090-128">Paramètres « require », constantes, authentification et structure</span><span class="sxs-lookup"><span data-stu-id="0b090-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="0b090-129">Avec *app.js* ouvert dans notre éditeur, effectuons une structure de base hello de notre programme écrit.</span><span class="sxs-lookup"><span data-stu-id="0b090-129">With *app.js* open in our editor, let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="0b090-130">Ajoutez hello » nécessite » pour nos packages NPM haut hello, avec les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="0b090-130">Add hello "requires" for our NPM packages at hello top with hello following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="0b090-131">Nous devons toodefine certaines constantes que nos méthodes utilisera.</span><span class="sxs-lookup"><span data-stu-id="0b090-131">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="0b090-132">Ajoutez les éléments suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="0b090-132">Add hello following.</span></span>  <span data-ttu-id="0b090-133">Être tooreplace que des espaces réservés de hello, y compris hello  **&lt;crochets pointus&gt;**, avec vos propres valeurs en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="0b090-133">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="0b090-134">Ensuite, nous instancier le client de gestion du CDN hello et lui donner ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0b090-134">Next, we'll instantiate hello CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="0b090-135">Si vous utilisez une authentification d’utilisateurs individuels, ces deux lignes aura un aspect légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="0b090-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="0b090-136">Utilisez uniquement cet exemple de code si vous choisissez l’authentification utilisateur individuel toohave au lieu d’un service principal.</span><span class="sxs-lookup"><span data-stu-id="0b090-136">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="0b090-137">Être prudent tooguard vos informations d’identification de l’utilisateur individuel et les garder secret.</span><span class="sxs-lookup"><span data-stu-id="0b090-137">Be careful tooguard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="0b090-138">Être tooreplace que les éléments hello dans  **&lt;crochets pointus&gt;**  avec hello corriger les informations.</span><span class="sxs-lookup"><span data-stu-id="0b090-138">Be sure tooreplace hello items in **&lt;angle brackets&gt;** with hello correct information.</span></span>  <span data-ttu-id="0b090-139">Pour `<redirect URI>`, utilisez hello redirection URI que vous avez entré lorsque vous avez inscrit un application hello dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b090-139">For `<redirect URI>`, use hello redirect URI you entered when you registered hello application in Azure AD.</span></span>
4. <span data-ttu-id="0b090-140">Notre application de console Node.js va tootake certains paramètres de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="0b090-140">Our Node.js console application is going tootake some command-line parameters.</span></span>  <span data-ttu-id="0b090-141">Vérifions qu’au moins un des paramètres a été transmis.</span><span class="sxs-lookup"><span data-stu-id="0b090-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="0b090-142">Cela nous amène toohello la partie principale de notre programme, où nous BIFURQUE fonctions tooother basées sur les paramètres ont été transmis.</span><span class="sxs-lookup"><span data-stu-id="0b090-142">That brings us toohello main part of our program, where we branch off tooother functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="0b090-143">À plusieurs endroits dans notre programme, nous devrons toomake que hello bon nombre de paramètres ont été passé et affiche une aide si elles ne s’affichent pas corrects.</span><span class="sxs-lookup"><span data-stu-id="0b090-143">At several places in our program, we'll need toomake sure hello right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="0b090-144">Nous allons créer toodo de fonctions qui.</span><span class="sxs-lookup"><span data-stu-id="0b090-144">Let's create functions toodo that.</span></span>
   
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
7. <span data-ttu-id="0b090-145">Enfin, les fonctions hello que nous utiliserons sur le client de gestion du CDN hello étant asynchrones, dont ils ont besoin d’une méthode toocall retour quand ils ont terminé.</span><span class="sxs-lookup"><span data-stu-id="0b090-145">Finally, hello functions we'll be using on hello CDN management client are asynchronous, so they need a method toocall back when they're done.</span></span>  <span data-ttu-id="0b090-146">Nous allons en créer une qui peut afficher la sortie de hello à partir du client de gestion du CDN hello (le cas échéant) et quitter le programme de hello en douceur.</span><span class="sxs-lookup"><span data-stu-id="0b090-146">Let's make one that can display hello output from hello CDN management client (if any) and exit hello program gracefully.</span></span>
   
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

<span data-ttu-id="0b090-147">Maintenant que la structure de base hello de notre programme est écrit, nous devons créer les fonctions hello appelées en fonction de nos paramètres.</span><span class="sxs-lookup"><span data-stu-id="0b090-147">Now that hello basic structure of our program is written, we should create hello functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="0b090-148">Répertorier les profils CDN et points de terminaison</span><span class="sxs-lookup"><span data-stu-id="0b090-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="0b090-149">Commençons par toolist de code nos profils existants et les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="0b090-149">Let's start with code toolist our existing profiles and endpoints.</span></span>  <span data-ttu-id="0b090-150">Les commentaires de code fournissent la syntaxe de hello attendu donc nous savons à l’emplacement de chaque paramètre.</span><span class="sxs-lookup"><span data-stu-id="0b090-150">My code comments provide hello expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="0b090-151">Créer des profils CDN et des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="0b090-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="0b090-152">Ensuite, nous allons écrire des points de terminaison et les profils de toocreate fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="0b090-152">Next, we'll write hello functions toocreate profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="0b090-153">Vider un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="0b090-153">Purge an endpoint</span></span>
<span data-ttu-id="0b090-154">En supposant que le point de terminaison hello a été créé, une tâche courante que nous souhaitions tooperform dans notre programme purge contenu dans notre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="0b090-154">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="0b090-155">Supprimer des profils CDN et des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="0b090-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="0b090-156">Hello dernière fonction que nous inclurons supprime les points de terminaison et les profils.</span><span class="sxs-lookup"><span data-stu-id="0b090-156">hello last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="0b090-157">Programme hello</span><span class="sxs-lookup"><span data-stu-id="0b090-157">Running hello program</span></span>
<span data-ttu-id="0b090-158">Maintenant, nous pouvons exécuter notre programme Node.js à l’aide de notre débogueur favori ou sur la console hello.</span><span class="sxs-lookup"><span data-stu-id="0b090-158">We can now execute our Node.js program using our favorite debugger or at hello console.</span></span>

> [!TIP]
> <span data-ttu-id="0b090-159">Si vous utilisez le Code de Visual Studio en tant que le débogueur, vous devez tooset des toopass de votre environnement dans les paramètres de ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="0b090-159">If you're using Visual Studio Code as your debugger, you'll need tooset up your environment toopass in hello command-line parameters.</span></span>  <span data-ttu-id="0b090-160">Code Visual Studio utilise pour cela hello **lanuch.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="0b090-160">Visual Studio Code does this in hello **lanuch.json** file.</span></span>  <span data-ttu-id="0b090-161">Recherchez une propriété nommée **args** et ajouter un tableau de valeurs de chaîne pour vos paramètres, pour qu’il toothis similaire : `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="0b090-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar toothis:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="0b090-162">Commençons par répertorier nos profils.</span><span class="sxs-lookup"><span data-stu-id="0b090-162">Let's start by listing our profiles.</span></span>

![Liste des profils](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="0b090-164">Nous obtenons un tableau vide.</span><span class="sxs-lookup"><span data-stu-id="0b090-164">We got back an empty array.</span></span>  <span data-ttu-id="0b090-165">Cela est tout à fait normal puisque nous n’avons aucun profil dans notre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0b090-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="0b090-166">Créons donc maintenant un profil.</span><span class="sxs-lookup"><span data-stu-id="0b090-166">Let's create a profile now.</span></span>

![Création d’un profil](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="0b090-168">À présent, ajoutons un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="0b090-168">Now, let's add an endpoint.</span></span>

![Création d’un point de terminaison](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="0b090-170">Pour finir, nous allons supprimer notre profil.</span><span class="sxs-lookup"><span data-stu-id="0b090-170">Finally, let's delete our profile.</span></span>

![Suppression d’un profil](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="0b090-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b090-172">Next Steps</span></span>
<span data-ttu-id="0b090-173">projet de hello terminée toosee à partir de cette procédure pas à pas, [télécharger l’exemple hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="0b090-173">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="0b090-174">référence de hello toosee pour hello Azure CDN SDK pour Node.js, hello de vue [référence](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="0b090-174">toosee hello reference for hello Azure CDN SDK for Node.js, view hello [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="0b090-175">toofind une documentation supplémentaire sur hello Azure SDK pour Node.js, hello de vue [complète référence](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="0b090-175">toofind additional documentation on hello Azure SDK for Node.js, view hello [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="0b090-176">Gérez vos ressources CDN avec [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0b090-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

