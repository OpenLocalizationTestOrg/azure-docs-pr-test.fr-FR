---
title: "Prise en main des applications à page unique .NET AngularJS Azure AD 2.0 | Microsoft Docs"
description: "Génération d’une application à page unique AngularJS qui connecte les utilisateurs avec les comptes Microsoft personnels et les comptes professionnels ou scolaires."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 6a341781-278f-461b-92ca-7572a06e6852
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c68180c0ecabf5c0732f0db77ef1f3cc93be965b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---net"></a><span data-ttu-id="6c79b-103">Ajouter une connexion à une application AngularJS à une seule page - .NET</span><span class="sxs-lookup"><span data-stu-id="6c79b-103">Add sign-in to an AngularJS single page app - .NET</span></span>
<span data-ttu-id="6c79b-104">Dans cet article, nous ajouterons la connexion avec des comptes Microsoft à une application AngularJS, à l’aide du point de terminaison v2.0 d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6c79b-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="6c79b-105">Le point de terminaison v2.0 vous permet d’effectuer une intégration unique dans votre application et d’authentifier les utilisateurs avec des comptes personnels et des comptes professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="6c79b-105">The v2.0 endpoint enables you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="6c79b-106">Cet exemple est une application à page unique de liste de tâches qui stocke les tâches dans une API REST du serveur principal, écrite à l’aide de .NET 4.5 MVC et sécurisée à l’aide des jetons du porteur OAuth d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c79b-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using the .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="6c79b-107">L’application AngularJS utilisera notre bibliothèque d’authentification open source JavaScript [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) afin de gérer l’intégralité du processus de connexion et d’acquérir les jetons utilisés pour appeler l’API REST.</span><span class="sxs-lookup"><span data-stu-id="6c79b-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="6c79b-108">Le même modèle peut être appliqué pour l’authentification d’autres API REST, comme les API [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6c79b-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="6c79b-109">Les scénarios et les fonctionnalités Azure Active Directory ne sont pas tous pris en charge par le point de terminaison v2.0.</span><span class="sxs-lookup"><span data-stu-id="6c79b-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="6c79b-110">Pour déterminer si vous devez utiliser le point de terminaison v2.0, consultez les [limitations de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="6c79b-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="6c79b-111">Télécharger</span><span class="sxs-lookup"><span data-stu-id="6c79b-111">Download</span></span>
<span data-ttu-id="6c79b-112">Pour commencer, vous devez télécharger et installer Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c79b-112">To get started, you'll need to download & install Visual Studio.</span></span>  <span data-ttu-id="6c79b-113">Vous pouvez ensuite cloner ou [télécharger](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) une application squelette :</span><span class="sxs-lookup"><span data-stu-id="6c79b-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="6c79b-114">L’application squelette comprend l’ensemble du code réutilisable associé à une application AngularJS simple, mais n’intègre pas l’ensemble des éléments liés à l’identité.</span><span class="sxs-lookup"><span data-stu-id="6c79b-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="6c79b-115">Si vous ne souhaitez pas suivre la procédure, vous pouvez cloner ou [télécharger](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) l’exemple terminé.</span><span class="sxs-lookup"><span data-stu-id="6c79b-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="6c79b-116">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="6c79b-116">Register an app</span></span>
<span data-ttu-id="6c79b-117">Dans un premier temps, créez une application dans le [portail d’inscription des applications](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="6c79b-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="6c79b-118">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="6c79b-118">Make sure to:</span></span>

* <span data-ttu-id="6c79b-119">ajouter la plateforme **web** pour votre application ;</span><span class="sxs-lookup"><span data-stu-id="6c79b-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="6c79b-120">entrer l’ **URI de redirection**approprié.</span><span class="sxs-lookup"><span data-stu-id="6c79b-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="6c79b-121">La valeur par défaut pour cet exemple est `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="6c79b-121">The default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="6c79b-122">Laissez la case **Autoriser un flux implicite** sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="6c79b-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="6c79b-123">Copiez l’ **ID d’application** affecté à votre application ; vous en aurez besoin rapidement.</span><span class="sxs-lookup"><span data-stu-id="6c79b-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="6c79b-124">Installer adal.js</span><span class="sxs-lookup"><span data-stu-id="6c79b-124">Install adal.js</span></span>
<span data-ttu-id="6c79b-125">Pour commencer, accédez au projet téléchargé, puis installez adal.js.</span><span class="sxs-lookup"><span data-stu-id="6c79b-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="6c79b-126">Si [bower](http://bower.io/) est installé, il vous suffit d’exécuter cette commande.</span><span class="sxs-lookup"><span data-stu-id="6c79b-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="6c79b-127">En cas d’incompatibilité de versions de dépendance, sélectionnez la version la plus élevée.</span><span class="sxs-lookup"><span data-stu-id="6c79b-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="6c79b-128">Sinon, vous pouvez télécharger manuellement [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) et [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="6c79b-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="6c79b-129">Ajoutez les deux fichiers au répertoire `app/lib/adal-angular-experimental/dist` du projet `TodoSPA`.</span><span class="sxs-lookup"><span data-stu-id="6c79b-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory of the `TodoSPA` project.</span></span>

<span data-ttu-id="6c79b-130">Ouvrez maintenant le projet dans Visual Studio, puis chargez adal.js à la fin du corps de la page principale :</span><span class="sxs-lookup"><span data-stu-id="6c79b-130">Now open the project in Visual Studio, and load adal.js at the end of the main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="6c79b-131">Configurer l’API REST</span><span class="sxs-lookup"><span data-stu-id="6c79b-131">Set up the REST API</span></span>
<span data-ttu-id="6c79b-132">Pendant la configuration, tentons de lancer l’API REST du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="6c79b-132">While we're setting things up, let's get the backend REST API working.</span></span>  <span data-ttu-id="6c79b-133">À la racine du projet, ouvrez `web.config` et remplacez la valeur `audience`.</span><span class="sxs-lookup"><span data-stu-id="6c79b-133">In the root of the project, open `web.config` and replace the `audience` value.</span></span>  <span data-ttu-id="6c79b-134">L’API REST utilise cette valeur pour valider les jetons reçus de l’application Angular, dans les requêtes AJAX.</span><span class="sxs-lookup"><span data-stu-id="6c79b-134">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="6c79b-135">Nous n’évoquerons pas plus en avant le fonctionnement de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="6c79b-135">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="6c79b-136">N’hésitez pas à examiner le code, mais si vous souhaitez en savoir plus sur la sécurisation des API web à l’aide d’Azure AD, consultez [cet article](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="6c79b-136">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="6c79b-137">Connecter les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6c79b-137">Sign users in</span></span>
<span data-ttu-id="6c79b-138">Il est temps d’écrire du code d’identité.</span><span class="sxs-lookup"><span data-stu-id="6c79b-138">Time to write some identity code.</span></span>  <span data-ttu-id="6c79b-139">Vous avez peut-être remarqué que adal.js contient un fournisseur AngularJS, qui se combine parfaitement aux mécanismes de routage Angular.</span><span class="sxs-lookup"><span data-stu-id="6c79b-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="6c79b-140">Commencez par ajouter le module adal à l’application :</span><span class="sxs-lookup"><span data-stu-id="6c79b-140">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="6c79b-141">Vous pouvez désormais initialiser l’élément `adalProvider` avec votre ID d’application :</span><span class="sxs-lookup"><span data-stu-id="6c79b-141">You can now initialize the `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="6c79b-142">Très bien, désormais adal.js possède toutes les informations nécessaires pour sécuriser votre application et connecter les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6c79b-142">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="6c79b-143">Pour forcer la connexion via un itinéraire particulier dans l’application, il vous suffit d’une ligne de code :</span><span class="sxs-lookup"><span data-stu-id="6c79b-143">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="6c79b-144">Désormais, lorsqu’un utilisateur clique sur le lien `TodoList` , adal.js redirige automatiquement vers Azure AD pour la connexion, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6c79b-144">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="6c79b-145">Vous pouvez également envoyer explicitement des requêtes de connexion et de déconnexion en invoquant adal.js dans vos contrôleurs :</span><span class="sxs-lookup"><span data-stu-id="6c79b-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="6c79b-146">Afficher les informations utilisateur</span><span class="sxs-lookup"><span data-stu-id="6c79b-146">Display user info</span></span>
<span data-ttu-id="6c79b-147">Maintenant que l’utilisateur est connecté, il vous faudra probablement accéder à ses données d’authentification dans votre application.</span><span class="sxs-lookup"><span data-stu-id="6c79b-147">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="6c79b-148">Adal.js expose ces informations pour vous dans l’objet `userInfo` .</span><span class="sxs-lookup"><span data-stu-id="6c79b-148">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="6c79b-149">Pour accéder à cet objet dans une vue, ajoutez adal.js sur l’étendue racine du contrôleur correspondant :</span><span class="sxs-lookup"><span data-stu-id="6c79b-149">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="6c79b-150">Vous pouvez ensuite directement traiter l’objet `userInfo` dans votre vue :</span><span class="sxs-lookup"><span data-stu-id="6c79b-150">Then you can directly address the `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="6c79b-151">Vous pouvez également utiliser l’objet `userInfo` afin de déterminer si l’utilisateur est connecté ou non.</span><span class="sxs-lookup"><span data-stu-id="6c79b-151">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

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

## <a name="call-the-rest-api"></a><span data-ttu-id="6c79b-152">Appeler l’API REST</span><span class="sxs-lookup"><span data-stu-id="6c79b-152">Call the REST API</span></span>
<span data-ttu-id="6c79b-153">Enfin, il est temps d’obtenir certains jetons et d’appeler l’API REST afin de créer, de lire, de mettre à jour et de supprimer les tâches.</span><span class="sxs-lookup"><span data-stu-id="6c79b-153">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="6c79b-154">Devinez quoi ?</span><span class="sxs-lookup"><span data-stu-id="6c79b-154">Well guess what?</span></span>  <span data-ttu-id="6c79b-155">Vous n’avez *rien*à faire.</span><span class="sxs-lookup"><span data-stu-id="6c79b-155">You don't have to do *a thing*.</span></span>  <span data-ttu-id="6c79b-156">Adal.js se charge automatiquement d’obtenir, de mettre en cache et d’actualiser les jetons.</span><span class="sxs-lookup"><span data-stu-id="6c79b-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="6c79b-157">Il joint également ces jetons aux requêtes AJAX sortantes que vous envoyez à l’API REST.</span><span class="sxs-lookup"><span data-stu-id="6c79b-157">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="6c79b-158">Comment ceci fonctionne-t-il ?</span><span class="sxs-lookup"><span data-stu-id="6c79b-158">How exactly does this work?</span></span> <span data-ttu-id="6c79b-159">Ces résultats sont obtenus à l’aide des [intercepteurs AngularJS](https://docs.angularjs.org/api/ng/service/$http) magiques, grâce auxquels adal.js peut transformer les messages http entrants et sortants.</span><span class="sxs-lookup"><span data-stu-id="6c79b-159">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="6c79b-160">En outre, adal.js suppose que l’ensemble des requêtes envoyées sur le domaine de la fenêtre doivent utiliser les jetons destinés à l’ID d’application de l’application AngularJS.</span><span class="sxs-lookup"><span data-stu-id="6c79b-160">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="6c79b-161">Dès lors, nous avons utilisé un ID d’application identique dans l’application Angular et dans l’API REST NodeJS.</span><span class="sxs-lookup"><span data-stu-id="6c79b-161">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="6c79b-162">Cela va de soi, vous pouvez ignorer ce comportement et demander à adal.js d’obtenir des jetons pour d’autres API REST, si nécessaire. Toutefois, pour ce scénario simple, les valeurs par défaut sont suffisantes.</span><span class="sxs-lookup"><span data-stu-id="6c79b-162">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="6c79b-163">Voici un extrait qui montre combien il est facile d’envoyer des requêtes à l’aide de jetons du porteur, à partir d’Azure AD :</span><span class="sxs-lookup"><span data-stu-id="6c79b-163">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="6c79b-164">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="6c79b-164">Congratulations!</span></span>  <span data-ttu-id="6c79b-165">Votre application intégrée Azure AD à page unique est désormais terminée.</span><span class="sxs-lookup"><span data-stu-id="6c79b-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="6c79b-166">Vous pouvez lui tirer votre chapeau.</span><span class="sxs-lookup"><span data-stu-id="6c79b-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="6c79b-167">Elle peut authentifier les utilisateurs, appeler de manière sécurisée son API REST du serveur principal à l’aide d’OpenID Connect, et obtenir des informations de base sur l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6c79b-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="6c79b-168">Dès le départ, elle prend en charge l’ensemble des utilisateurs disposant d’un compte Microsoft personnel ou un compte professionnel/scolaire d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c79b-168">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="6c79b-169">Exécutez l’application, puis, dans un navigateur, accédez à `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="6c79b-169">Run the app, and in a browser navigate to `https://localhost:44326/`.</span></span>  <span data-ttu-id="6c79b-170">Connectez-vous à un compte personnel Microsoft ou à un compte scolaire/professionnel.</span><span class="sxs-lookup"><span data-stu-id="6c79b-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="6c79b-171">Ajoutez des tâches à la liste des tâches de l’utilisateur, puis déconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="6c79b-171">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="6c79b-172">Essayez de vous connecter avec l’autre type de compte.</span><span class="sxs-lookup"><span data-stu-id="6c79b-172">Try signing in with the other type of account.</span></span> <span data-ttu-id="6c79b-173">Si vous avez besoin qu’un locataire Azure AD crée des utilisateurs scolaires/professionnels, [découvrez comment en obtenir un ici](active-directory-howto-tenant.md) (c’est gratuit).</span><span class="sxs-lookup"><span data-stu-id="6c79b-173">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="6c79b-174">Pour en savoir plus sur le point de terminaison v2.0, consultez de nouveau notre [guide du développeur v2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c79b-174">To continue learning about the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="6c79b-175">Pour obtenir des ressources supplémentaires, consultez :</span><span class="sxs-lookup"><span data-stu-id="6c79b-175">For additional resources, check out:</span></span>

* [<span data-ttu-id="6c79b-176">Exemples Azure sur GitHub >></span><span class="sxs-lookup"><span data-stu-id="6c79b-176">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="6c79b-177">Azure AD sur Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="6c79b-177">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="6c79b-178">Documentation Azure AD sur [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="6c79b-178">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="6c79b-179">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="6c79b-179">Get security updates for our products</span></span>
<span data-ttu-id="6c79b-180">Nous vous encourageons à activer les notifications d’incidents de sécurité en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et en vous abonnant aux alertes d’avis de sécurité.</span><span class="sxs-lookup"><span data-stu-id="6c79b-180">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

