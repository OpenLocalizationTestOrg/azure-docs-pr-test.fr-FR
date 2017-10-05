---
title: "Prise en main des applications à page unique NodeJS AngularJS Azure AD 2.0 | Microsoft Docs"
description: "Génération d’une application à page unique AngularJS qui connecte les utilisateurs avec les comptes Microsoft personnels et les comptes professionnels ou scolaires."
services: active-directory
documentationcenter: 
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: d286aa33-8a94-452f-beb7-ddc6c6daa5c8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 0e90171afd9c4c782fbb18375ab2d147497ef442
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---nodejs"></a><span data-ttu-id="9e15d-103">Ajouter une connexion à une application AngularJS à une seule page - NodeJS</span><span class="sxs-lookup"><span data-stu-id="9e15d-103">Add sign-in to an AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="9e15d-104">Dans cet article, nous allons ajouter la connexion avec des comptes Microsoft à une application AngularJS à l’aide du point de terminaison Azure Active Directory v2.0.</span><span class="sxs-lookup"><span data-stu-id="9e15d-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="9e15d-105">Le point de terminaison v2.0 permet d’effectuer une intégration simple dans votre application et d’authentifier les utilisateurs avec des comptes personnels ou professionnels/scolaires.</span><span class="sxs-lookup"><span data-stu-id="9e15d-105">the v2.0 endpoint enable you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="9e15d-106">Cet exemple est une application à page unique de liste de tâches qui stocke les tâches dans une API REST du serveur principal, écrite en NodeJS et sécurisée à l’aide de jetons du porteur OAuth d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e15d-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="9e15d-107">L’application AngularJS utilisera notre bibliothèque d’authentification open source JavaScript [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) afin de gérer l’intégralité du processus de connexion et d’acquérir les jetons utilisés pour appeler l’API REST.</span><span class="sxs-lookup"><span data-stu-id="9e15d-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="9e15d-108">Le même modèle peut être appliqué pour l’authentification d’autres API REST, comme les API [Microsoft Graph](https://graph.microsoft.com) ou Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e15d-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com) or the Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15d-109">Les scénarios et les fonctionnalités Azure Active Directory ne sont pas tous pris en charge par le point de terminaison v2.0.</span><span class="sxs-lookup"><span data-stu-id="9e15d-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="9e15d-110">Pour déterminer si vous devez utiliser le point de terminaison v2.0, consultez les [limitations de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="9e15d-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="9e15d-111">Télécharger</span><span class="sxs-lookup"><span data-stu-id="9e15d-111">Download</span></span>
<span data-ttu-id="9e15d-112">Pour commencer, vous devez télécharger et installer [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="9e15d-112">To get started, you'll need to download & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="9e15d-113">Vous pouvez ensuite cloner ou [télécharger](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) une application squelette :</span><span class="sxs-lookup"><span data-stu-id="9e15d-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="9e15d-114">L’application squelette comprend l’ensemble du code réutilisable associé à une application AngularJS simple, mais n’intègre pas l’ensemble des éléments liés à l’identité.</span><span class="sxs-lookup"><span data-stu-id="9e15d-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="9e15d-115">Si vous ne souhaitez pas suivre la procédure, vous pouvez cloner ou [télécharger](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) l’exemple terminé.</span><span class="sxs-lookup"><span data-stu-id="9e15d-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="9e15d-116">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="9e15d-116">Register an app</span></span>
<span data-ttu-id="9e15d-117">Dans un premier temps, créez une application dans le [portail d’inscription des applications](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="9e15d-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="9e15d-118">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="9e15d-118">Make sure to:</span></span>

* <span data-ttu-id="9e15d-119">ajouter la plateforme **web** pour votre application ;</span><span class="sxs-lookup"><span data-stu-id="9e15d-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="9e15d-120">entrer l’ **URI de redirection**approprié.</span><span class="sxs-lookup"><span data-stu-id="9e15d-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="9e15d-121">La valeur par défaut pour cet exemple est `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="9e15d-121">The default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="9e15d-122">Laissez la case **Autoriser un flux implicite** sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="9e15d-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="9e15d-123">Copiez l’ **ID d’application** affecté à votre application ; vous en aurez besoin rapidement.</span><span class="sxs-lookup"><span data-stu-id="9e15d-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="9e15d-124">Installer adal.js</span><span class="sxs-lookup"><span data-stu-id="9e15d-124">Install adal.js</span></span>
<span data-ttu-id="9e15d-125">Pour commencer, accédez au projet téléchargé, puis installez adal.js.</span><span class="sxs-lookup"><span data-stu-id="9e15d-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="9e15d-126">Si [bower](http://bower.io/) est installé, il vous suffit d’exécuter cette commande.</span><span class="sxs-lookup"><span data-stu-id="9e15d-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="9e15d-127">En cas d’incompatibilité de versions de dépendance, sélectionnez la version la plus élevée.</span><span class="sxs-lookup"><span data-stu-id="9e15d-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="9e15d-128">Sinon, vous pouvez télécharger manuellement [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) et [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="9e15d-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="9e15d-129">Ajoutez les deux fichiers au répertoire `app/lib/adal-angular-experimental/dist` .</span><span class="sxs-lookup"><span data-stu-id="9e15d-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="9e15d-130">Ouvrez maintenant le projet dans votre éditeur de texte favori, puis chargez adal.js à la fin du corps de la page :</span><span class="sxs-lookup"><span data-stu-id="9e15d-130">Now open the project in your favorite text editor, and load adal.js at the end of the page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="9e15d-131">Configurer l’API REST</span><span class="sxs-lookup"><span data-stu-id="9e15d-131">Set up the REST API</span></span>
<span data-ttu-id="9e15d-132">Pendant la configuration, tentons de lancer l’API REST du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="9e15d-132">While we're setting things up, lets get the backend REST API working.</span></span>  <span data-ttu-id="9e15d-133">Dans une invite de commande, installez l’ensemble des packages en exécutant (assurez-vous d’être dans le répertoire de niveau supérieur du projet) :</span><span class="sxs-lookup"><span data-stu-id="9e15d-133">In a command prompt, install all the necessary packages by running (make sure you're in the top-level directory of the project):</span></span>

```
npm install
```

<span data-ttu-id="9e15d-134">Ouvrez maintenant `config.js`, puis remplacez la valeur `audience` :</span><span class="sxs-lookup"><span data-stu-id="9e15d-134">Now open `config.js` and replace the `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with the Application ID from the registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="9e15d-135">L’API REST utilise cette valeur pour valider les jetons reçus de l’application Angular, dans les requêtes AJAX.</span><span class="sxs-lookup"><span data-stu-id="9e15d-135">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>  <span data-ttu-id="9e15d-136">Notez que cette API REST simple stocke les données en mémoire. Lorsque vous arrêtez le serveur, vous perdez l’ensemble des tâches précédemment créées.</span><span class="sxs-lookup"><span data-stu-id="9e15d-136">Note that this simple REST API stores data in-memory - so each time to stop the server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="9e15d-137">Nous n’évoquerons pas plus en avant le fonctionnement de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="9e15d-137">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="9e15d-138">N’hésitez pas à examiner le code, mais si vous souhaitez en savoir plus sur la sécurisation des API web à l’aide d’Azure AD, consultez [cet article](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="9e15d-138">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="9e15d-139">Connecter les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="9e15d-139">Sign users in</span></span>
<span data-ttu-id="9e15d-140">Il est temps d’écrire du code d’identité.</span><span class="sxs-lookup"><span data-stu-id="9e15d-140">Time to write some identity code.</span></span>  <span data-ttu-id="9e15d-141">Vous avez peut-être remarqué que adal.js contient un fournisseur AngularJS, qui se combine parfaitement aux mécanismes de routage Angular.</span><span class="sxs-lookup"><span data-stu-id="9e15d-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="9e15d-142">Commencez par ajouter le module adal à l’application :</span><span class="sxs-lookup"><span data-stu-id="9e15d-142">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="9e15d-143">Vous pouvez désormais initialiser l’élément `adalProvider` avec votre ID d’application :</span><span class="sxs-lookup"><span data-stu-id="9e15d-143">You can now initialize the `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for the public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // The 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from the registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - the default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="9e15d-144">Très bien, désormais adal.js possède toutes les informations nécessaires pour sécuriser votre application et connecter les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9e15d-144">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="9e15d-145">Pour forcer la connexion via un itinéraire particulier dans l’application, il vous suffit d’une ligne de code :</span><span class="sxs-lookup"><span data-stu-id="9e15d-145">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that the user must be logged in to access the route
})

...
```

<span data-ttu-id="9e15d-146">Désormais, lorsqu’un utilisateur clique sur le lien `TodoList` , adal.js redirige automatiquement vers Azure AD pour la connexion, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9e15d-146">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="9e15d-147">Vous pouvez également envoyer explicitement des requêtes de connexion et de déconnexion en invoquant adal.js dans vos contrôleurs :</span><span class="sxs-lookup"><span data-stu-id="9e15d-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js the same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect the user to sign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect the user to log out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="9e15d-148">Afficher les informations utilisateur</span><span class="sxs-lookup"><span data-stu-id="9e15d-148">Display user info</span></span>
<span data-ttu-id="9e15d-149">Maintenant que l’utilisateur est connecté, il vous faudra probablement accéder à ses données d’authentification dans votre application.</span><span class="sxs-lookup"><span data-stu-id="9e15d-149">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="9e15d-150">Adal.js expose ces informations pour vous dans l’objet `userInfo` .</span><span class="sxs-lookup"><span data-stu-id="9e15d-150">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="9e15d-151">Pour accéder à cet objet dans une vue, ajoutez adal.js sur l’étendue racine du contrôleur correspondant :</span><span class="sxs-lookup"><span data-stu-id="9e15d-151">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="9e15d-152">Vous pouvez ensuite directement traiter l’objet `userInfo` dans votre vue :</span><span class="sxs-lookup"><span data-stu-id="9e15d-152">Then you can directly address the `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get the user's profile information from the ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="9e15d-153">Vous pouvez également utiliser l’objet `userInfo` afin de déterminer si l’utilisateur est connecté ou non.</span><span class="sxs-lookup"><span data-stu-id="9e15d-153">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use the ADAL userInfo object to show the right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-the-rest-api"></a><span data-ttu-id="9e15d-154">Appeler l’API REST</span><span class="sxs-lookup"><span data-stu-id="9e15d-154">Call the REST API</span></span>
<span data-ttu-id="9e15d-155">Enfin, il est temps d’obtenir certains jetons et d’appeler l’API REST afin de créer, de lire, de mettre à jour et de supprimer les tâches.</span><span class="sxs-lookup"><span data-stu-id="9e15d-155">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="9e15d-156">Devinez quoi ?</span><span class="sxs-lookup"><span data-stu-id="9e15d-156">Well guess what?</span></span>  <span data-ttu-id="9e15d-157">Vous n’avez *rien*à faire.</span><span class="sxs-lookup"><span data-stu-id="9e15d-157">You don't have to do *a thing*.</span></span>  <span data-ttu-id="9e15d-158">Adal.js se charge automatiquement d’obtenir, de mettre en cache et d’actualiser les jetons.</span><span class="sxs-lookup"><span data-stu-id="9e15d-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="9e15d-159">Il joint également ces jetons aux requêtes AJAX sortantes que vous envoyez à l’API REST.</span><span class="sxs-lookup"><span data-stu-id="9e15d-159">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="9e15d-160">Comment ceci fonctionne-t-il ?</span><span class="sxs-lookup"><span data-stu-id="9e15d-160">How exactly does this work?</span></span> <span data-ttu-id="9e15d-161">Ces résultats sont obtenus à l’aide des [intercepteurs AngularJS](https://docs.angularjs.org/api/ng/service/$http) magiques, grâce auxquels adal.js peut transformer les messages http entrants et sortants.</span><span class="sxs-lookup"><span data-stu-id="9e15d-161">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="9e15d-162">En outre, adal.js suppose que l’ensemble des requêtes envoyées sur le domaine de la fenêtre doivent utiliser les jetons destinés à l’ID d’application de l’application AngularJS.</span><span class="sxs-lookup"><span data-stu-id="9e15d-162">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="9e15d-163">Dès lors, nous avons utilisé un ID d’application identique dans l’application Angular et dans l’API REST NodeJS.</span><span class="sxs-lookup"><span data-stu-id="9e15d-163">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="9e15d-164">Cela va de soi, vous pouvez ignorer ce comportement et demander à adal.js d’obtenir des jetons pour d’autres API REST, si nécessaire. Toutefois, pour ce scénario simple, les valeurs par défaut sont suffisantes.</span><span class="sxs-lookup"><span data-stu-id="9e15d-164">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="9e15d-165">Voici un extrait qui montre combien il est facile d’envoyer des requêtes à l’aide de jetons du porteur, à partir d’Azure AD :</span><span class="sxs-lookup"><span data-stu-id="9e15d-165">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="9e15d-166">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9e15d-166">Congratulations!</span></span>  <span data-ttu-id="9e15d-167">Votre application intégrée Azure AD à page unique est désormais terminée.</span><span class="sxs-lookup"><span data-stu-id="9e15d-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="9e15d-168">Vous pouvez lui tirer votre chapeau.</span><span class="sxs-lookup"><span data-stu-id="9e15d-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="9e15d-169">Elle peut authentifier les utilisateurs, appeler de manière sécurisée son API REST du serveur principal à l’aide d’OpenID Connect, et obtenir des informations de base sur l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9e15d-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="9e15d-170">Dès le départ, elle prend en charge l’ensemble des utilisateurs disposant d’un compte Microsoft personnel ou un compte professionnel/scolaire d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e15d-170">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="9e15d-171">Testez l’application en exécutant :</span><span class="sxs-lookup"><span data-stu-id="9e15d-171">Give the app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="9e15d-172">Dans un navigateur, accédez à `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="9e15d-172">In a browser navigate to `http://localhost:8080`.</span></span>  <span data-ttu-id="9e15d-173">Connectez-vous à un compte personnel Microsoft ou à un compte scolaire/professionnel.</span><span class="sxs-lookup"><span data-stu-id="9e15d-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="9e15d-174">Ajoutez des tâches à la liste des tâches de l’utilisateur, puis déconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="9e15d-174">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="9e15d-175">Essayez de vous connecter avec l’autre type de compte.</span><span class="sxs-lookup"><span data-stu-id="9e15d-175">Try signing in with the other type of account.</span></span> <span data-ttu-id="9e15d-176">Si vous avez besoin qu’un locataire Azure AD crée des utilisateurs scolaires/professionnels, [découvrez comment en obtenir un ici](active-directory-howto-tenant.md) (c’est gratuit).</span><span class="sxs-lookup"><span data-stu-id="9e15d-176">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="9e15d-177">Pour poursuivre l’apprentissage sur le point de terminaison v2.0, consultez de nouveau notre [guide du développeur v2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e15d-177">To continue learning about the the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="9e15d-178">Pour obtenir des ressources supplémentaires, consultez :</span><span class="sxs-lookup"><span data-stu-id="9e15d-178">For additional resources, check out:</span></span>

* [<span data-ttu-id="9e15d-179">Exemples Azure sur GitHub >></span><span class="sxs-lookup"><span data-stu-id="9e15d-179">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="9e15d-180">Azure AD sur Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="9e15d-180">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="9e15d-181">Documentation Azure AD sur [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="9e15d-181">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="9e15d-182">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="9e15d-182">Get security updates for our products</span></span>
<span data-ttu-id="9e15d-183">Nous vous encourageons à activer les notifications d’incidents de sécurité en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et en vous abonnant aux alertes d’avis de sécurité.</span><span class="sxs-lookup"><span data-stu-id="9e15d-183">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

