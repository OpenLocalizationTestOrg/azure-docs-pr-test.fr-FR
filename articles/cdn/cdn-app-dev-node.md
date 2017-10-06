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
# <a name="get-started-with-azure-cdn-development"></a>Prise en main du développement Azure CDN
> [!div class="op_single_selector"]
> * [Node.JS](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Vous pouvez utiliser hello [Azure CDN SDK pour Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate création et la gestion des profils CDN et des points de terminaison.  Ce didacticiel guide dans la création d’une application de console Node.js simple qui illustre plusieurs opérations disponibles de hello hello.  Ce didacticiel n’est pas conçu toodescribe tous les aspects de hello Azure CDN SDK pour Node.js en détail.

toocomplete ce didacticiel, vous devez déjà avoir [Node.js](http://www.nodejs.org) **versions4.x.x** ou version ultérieure installé et configuré.  Vous pouvez utiliser n’importe quel éditeur de texte vous souhaitez toocreate votre application Node.js.  toowrite ce didacticiel, j’ai utilisé [Visual Studio Code](https://code.visualstudio.com).  

> [!TIP]
> Hello [projet achevé de ce didacticiel](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) est disponible pour téléchargement sur MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a>Créer votre projet et ajouter des dépendances NPM
Maintenant que nous avons créé un groupe de ressources pour les profils de notre CDN et donné notre profils CDN toomanage d’autorisation d’application Azure AD et les points de terminaison de ce groupe, nous pouvons commencer à créer notre application.

Créer un dossier toostore votre application.  À partir d’une console avec hello Node.js tools dans votre chemin d’accès actuel, définir votre dossier de nouveau toothis emplacement actuel et initialiser votre projet en exécutant :

    npm init

Vous serez ensuite présenté à une série de questions tooinitialize votre projet.  Comme **point d’entrée**, ce didacticiel utilise *app.js*.  Vous pouvez afficher mes autres choix Bonjour l’exemple suivant.

![sortie init NPM](./media/cdn-app-dev-node/cdn-npm-init.png)

Notre projet est maintenant initialisé avec un fichier *packages.json* .  Notre projet va toouse certaines bibliothèques Azure contenues dans des packages NPM.  Nous allons utiliser hello exécution du Client Azure pour Node.js (ms-rest-azure) et hello bibliothèque cliente de CDN Azure pour Node.js (azure cd arm).  Vous allez ajouter ces projets toohello en tant que dépendances.

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

Hello packages sont effectuées après l’installation, hello *package.json* fichier doit se présenter exemple toothis similaire (version nombres peuvent varier) :

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

Enfin, à l’aide de votre éditeur de texte, créez un fichier texte vide et l’enregistrer dans le dossier de projet en tant que racine hello *app.js*.  Nous sommes maintenant prêt toobegin l’écriture de code.

## <a name="requires-constants-authentication-and-structure"></a>Paramètres « require », constantes, authentification et structure
Avec *app.js* ouvert dans notre éditeur, effectuons une structure de base hello de notre programme écrit.

1. Ajoutez hello » nécessite » pour nos packages NPM haut hello, avec les éléments suivants de hello :
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. Nous devons toodefine certaines constantes que nos méthodes utilisera.  Ajoutez les éléments suivants de hello.  Être tooreplace que des espaces réservés de hello, y compris hello  **&lt;crochets pointus&gt;**, avec vos propres valeurs en fonction des besoins.
   
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
3. Ensuite, nous instancier le client de gestion du CDN hello et lui donner ses informations d’identification.
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Si vous utilisez une authentification d’utilisateurs individuels, ces deux lignes aura un aspect légèrement différent.
   
   > [!IMPORTANT]
   > Utilisez uniquement cet exemple de code si vous choisissez l’authentification utilisateur individuel toohave au lieu d’un service principal.  Être prudent tooguard vos informations d’identification de l’utilisateur individuel et les garder secret.
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Être tooreplace que les éléments hello dans  **&lt;crochets pointus&gt;**  avec hello corriger les informations.  Pour `<redirect URI>`, utilisez hello redirection URI que vous avez entré lorsque vous avez inscrit un application hello dans Azure AD.
4. Notre application de console Node.js va tootake certains paramètres de ligne de commande.  Vérifions qu’au moins un des paramètres a été transmis.
   
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
5. Cela nous amène toohello la partie principale de notre programme, où nous BIFURQUE fonctions tooother basées sur les paramètres ont été transmis.
   
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
6. À plusieurs endroits dans notre programme, nous devrons toomake que hello bon nombre de paramètres ont été passé et affiche une aide si elles ne s’affichent pas corrects.  Nous allons créer toodo de fonctions qui.
   
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
7. Enfin, les fonctions hello que nous utiliserons sur le client de gestion du CDN hello étant asynchrones, dont ils ont besoin d’une méthode toocall retour quand ils ont terminé.  Nous allons en créer une qui peut afficher la sortie de hello à partir du client de gestion du CDN hello (le cas échéant) et quitter le programme de hello en douceur.
   
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

Maintenant que la structure de base hello de notre programme est écrit, nous devons créer les fonctions hello appelées en fonction de nos paramètres.

## <a name="list-cdn-profiles-and-endpoints"></a>Répertorier les profils CDN et points de terminaison
Commençons par toolist de code nos profils existants et les points de terminaison.  Les commentaires de code fournissent la syntaxe de hello attendu donc nous savons à l’emplacement de chaque paramètre.

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

## <a name="create-cdn-profiles-and-endpoints"></a>Créer des profils CDN et des points de terminaison
Ensuite, nous allons écrire des points de terminaison et les profils de toocreate fonctions hello.

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

## <a name="purge-an-endpoint"></a>Vider un point de terminaison
En supposant que le point de terminaison hello a été créé, une tâche courante que nous souhaitions tooperform dans notre programme purge contenu dans notre point de terminaison.

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a>Supprimer des profils CDN et des points de terminaison
Hello dernière fonction que nous inclurons supprime les points de terminaison et les profils.

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

## <a name="running-hello-program"></a>Programme hello
Maintenant, nous pouvons exécuter notre programme Node.js à l’aide de notre débogueur favori ou sur la console hello.

> [!TIP]
> Si vous utilisez le Code de Visual Studio en tant que le débogueur, vous devez tooset des toopass de votre environnement dans les paramètres de ligne de commande hello.  Code Visual Studio utilise pour cela hello **lanuch.json** fichier.  Recherchez une propriété nommée **args** et ajouter un tableau de valeurs de chaîne pour vos paramètres, pour qu’il toothis similaire : `"args": ["list", "profiles"]`.
> 
> 

Commençons par répertorier nos profils.

![Liste des profils](./media/cdn-app-dev-node/cdn-list-profiles.png)

Nous obtenons un tableau vide.  Cela est tout à fait normal puisque nous n’avons aucun profil dans notre groupe de ressources.  Créons donc maintenant un profil.

![Création d’un profil](./media/cdn-app-dev-node/cdn-create-profile.png)

À présent, ajoutons un point de terminaison.

![Création d’un point de terminaison](./media/cdn-app-dev-node/cdn-create-endpoint.png)

Pour finir, nous allons supprimer notre profil.

![Suppression d’un profil](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a>Étapes suivantes
projet de hello terminée toosee à partir de cette procédure pas à pas, [télécharger l’exemple hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).

référence de hello toosee pour hello Azure CDN SDK pour Node.js, hello de vue [référence](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).

toofind une documentation supplémentaire sur hello Azure SDK pour Node.js, hello de vue [complète référence](http://azure.github.io/azure-sdk-for-node/).

Gérez vos ressources CDN avec [PowerShell](cdn-manage-powershell.md).

