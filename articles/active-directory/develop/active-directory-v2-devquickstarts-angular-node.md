---
title: "aaaAzure AD v2.0 application à page unique NodeJS AngularJS prise en main | Documents Microsoft"
description: Comment toobuild une application angulaire JS seule Page qui se connecte aux utilisateurs avec Microsoft personnel des comptes et utiliser comptes professionnels ou scolaires.
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
ms.openlocfilehash: 1ab450caf08ab05fba140b94b1b8de652e99cbc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a><span data-ttu-id="25fa9-103">Ajouter l’application à page unique connexion tooan AngularJS - NodeJS</span><span class="sxs-lookup"><span data-stu-id="25fa9-103">Add sign-in tooan AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="25fa9-104">Dans cet article, nous allons ajouter connectez-vous avec Microsoft sous tension comptes tooan AngularJS application à l’aide du point de terminaison v2.0 hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="25fa9-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="25fa9-105">point de terminaison Hello v2.0 vous tooperform une intégration unique dans votre application et authentifier les utilisateurs avec des comptes personnels et de travail/school.</span><span class="sxs-lookup"><span data-stu-id="25fa9-105">hello v2.0 endpoint enable you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="25fa9-106">Cet exemple est une application à page unique de liste de tâches qui stocke les tâches dans une API REST du serveur principal, écrite en NodeJS et sécurisée à l’aide de jetons du porteur OAuth d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25fa9-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="25fa9-107">Hello AngularJS application utilisera notre bibliothèque d’authentification de JavaScript open source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello du processus de connexion entière et acquérir des jetons pour hello appel API REST.</span><span class="sxs-lookup"><span data-stu-id="25fa9-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="25fa9-108">Hello même modèle peut être appliqué tooauthenticate tooother API REST, comme hello [Microsoft Graph](https://graph.microsoft.com) ou hello API du Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="25fa9-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com) or hello Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="25fa9-109">Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="25fa9-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="25fa9-110">toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="25fa9-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="25fa9-111">Télécharger</span><span class="sxs-lookup"><span data-stu-id="25fa9-111">Download</span></span>
<span data-ttu-id="25fa9-112">tooget démarré, vous devez toodownload & installer [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="25fa9-112">tooget started, you'll need toodownload & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="25fa9-113">Vous pouvez ensuite cloner ou [télécharger](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) une application squelette :</span><span class="sxs-lookup"><span data-stu-id="25fa9-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="25fa9-114">application squelette Hello inclut tout le code réutilisable hello pour une application AngularJS simple, mais il manque l’intégralité des hello liées à l’identité.</span><span class="sxs-lookup"><span data-stu-id="25fa9-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="25fa9-115">Si vous ne souhaitez pas toofollow le long, vous pouvez à la place cloner ou [télécharger](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) exemple hello s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="25fa9-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="25fa9-116">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="25fa9-116">Register an app</span></span>
<span data-ttu-id="25fa9-117">Tout d’abord, créez une application dans hello [portail de l’enregistrement d’application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou procédez [une procédure détaillée](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="25fa9-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="25fa9-118">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="25fa9-118">Make sure to:</span></span>

* <span data-ttu-id="25fa9-119">Ajouter hello **Web** plate-forme pour votre application.</span><span class="sxs-lookup"><span data-stu-id="25fa9-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="25fa9-120">Entrez hello correct **URI de redirection**.</span><span class="sxs-lookup"><span data-stu-id="25fa9-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="25fa9-121">valeur par défaut de Hello pour cet exemple est `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="25fa9-121">hello default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="25fa9-122">Laissez hello **autorise le flux implicite** case à cocher activée.</span><span class="sxs-lookup"><span data-stu-id="25fa9-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="25fa9-123">Copie vers le bas hello **ID d’Application** qui est attribué tooyour application, vous en aurez besoin dans quelques instants.</span><span class="sxs-lookup"><span data-stu-id="25fa9-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="25fa9-124">Installer adal.js</span><span class="sxs-lookup"><span data-stu-id="25fa9-124">Install adal.js</span></span>
<span data-ttu-id="25fa9-125">toostart, accédez tooproject que vous avez téléchargé et installez adal.js.</span><span class="sxs-lookup"><span data-stu-id="25fa9-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="25fa9-126">Si [bower](http://bower.io/) est installé, il vous suffit d’exécuter cette commande.</span><span class="sxs-lookup"><span data-stu-id="25fa9-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="25fa9-127">Pour toutes les incompatibilités au niveau de la version de dépendance, choisissez une version supérieure hello.</span><span class="sxs-lookup"><span data-stu-id="25fa9-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="25fa9-128">Sinon, vous pouvez télécharger manuellement [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) et [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="25fa9-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="25fa9-129">Ajoutez les deux fichiers toohello `app/lib/adal-angular-experimental/dist` active.</span><span class="sxs-lookup"><span data-stu-id="25fa9-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="25fa9-130">Ouvrez projet de hello dans votre éditeur de texte et charger adal.js à fin hello hello du corps de page :</span><span class="sxs-lookup"><span data-stu-id="25fa9-130">Now open hello project in your favorite text editor, and load adal.js at hello end of hello page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="25fa9-131">Configurer hello API REST</span><span class="sxs-lookup"><span data-stu-id="25fa9-131">Set up hello REST API</span></span>
<span data-ttu-id="25fa9-132">Pendant que nous configurons choses, permet l’utilisation d’API REST get hello back-end.</span><span class="sxs-lookup"><span data-stu-id="25fa9-132">While we're setting things up, lets get hello backend REST API working.</span></span>  <span data-ttu-id="25fa9-133">Dans une invite de commandes, installez tous les packages nécessaires hello en exécutant (Assurez-vous que vous êtes dans le répertoire de niveau supérieur de hello du projet de hello) :</span><span class="sxs-lookup"><span data-stu-id="25fa9-133">In a command prompt, install all hello necessary packages by running (make sure you're in hello top-level directory of hello project):</span></span>

```
npm install
```

<span data-ttu-id="25fa9-134">À présent ouvrir `config.js` et remplacer hello `audience` valeur :</span><span class="sxs-lookup"><span data-stu-id="25fa9-134">Now open `config.js` and replace hello `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="25fa9-135">Hello API REST utilisera cette jetons toovalidate de valeur qu’il reçoit à partir de l’application angulaire hello sur les requêtes AJAX.</span><span class="sxs-lookup"><span data-stu-id="25fa9-135">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>  <span data-ttu-id="25fa9-136">Notez que cette API REST simple stocke les données en mémoire - pour chaque serveur de hello toostop temps, vous perdrez toutes les tâches créées précédemment.</span><span class="sxs-lookup"><span data-stu-id="25fa9-136">Note that this simple REST API stores data in-memory - so each time toostop hello server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="25fa9-137">C’est tout temps hello, nous allons toospend décrivant le fonctionne de l’API REST de hello.</span><span class="sxs-lookup"><span data-stu-id="25fa9-137">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="25fa9-138">Pensez toopoke libre dans le code hello, mais si vous souhaitez toolearn plus d’informations sur la sécurisation d’API avec Azure AD, consultez [cet article](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="25fa9-138">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="25fa9-139">Connecter les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="25fa9-139">Sign users in</span></span>
<span data-ttu-id="25fa9-140">Temps toowrite du code d’identité.</span><span class="sxs-lookup"><span data-stu-id="25fa9-140">Time toowrite some identity code.</span></span>  <span data-ttu-id="25fa9-141">Vous avez peut-être remarqué que adal.js contient un fournisseur AngularJS, qui se combine parfaitement aux mécanismes de routage Angular.</span><span class="sxs-lookup"><span data-stu-id="25fa9-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="25fa9-142">Commencez par ajouter hello module adal toohello application :</span><span class="sxs-lookup"><span data-stu-id="25fa9-142">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="25fa9-143">Vous pouvez désormais initialiser hello `adalProvider` avec votre ID d’Application :</span><span class="sxs-lookup"><span data-stu-id="25fa9-143">You can now initialize hello `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for hello public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // hello 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from hello registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - hello default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="25fa9-144">Très bien adal.js a toutes les informations de hello, elle doit toosecure vos utilisateurs d’application et connectez-vous dans.</span><span class="sxs-lookup"><span data-stu-id="25fa9-144">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="25fa9-145">connexions tooforce pour un itinéraire particulier dans une application hello, il sont une ligne de code :</span><span class="sxs-lookup"><span data-stu-id="25fa9-145">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that hello user must be logged in tooaccess hello route
})

...
```

<span data-ttu-id="25fa9-146">Quand un utilisateur clique sur hello `TodoList` lien, adal.js redirige automatiquement tooAzure AD pour la connexion si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="25fa9-146">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="25fa9-147">Vous pouvez également envoyer explicitement des requêtes de connexion et de déconnexion en invoquant adal.js dans vos contrôleurs :</span><span class="sxs-lookup"><span data-stu-id="25fa9-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js hello same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect hello user toosign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect hello user toolog out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="25fa9-148">Afficher les informations utilisateur</span><span class="sxs-lookup"><span data-stu-id="25fa9-148">Display user info</span></span>
<span data-ttu-id="25fa9-149">Maintenant que hello utilisateur n’est connecté, vous devez probablement des données d’authentification tooaccess hello signé de l’utilisateur dans votre application.</span><span class="sxs-lookup"><span data-stu-id="25fa9-149">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="25fa9-150">Adal.js expose ces informations pour vous dans hello `userInfo` objet.</span><span class="sxs-lookup"><span data-stu-id="25fa9-150">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="25fa9-151">tooaccess cet objet dans une vue, ajoutez d’abord étendue de racine adal.js toohello de contrôleur correspondant de hello :</span><span class="sxs-lookup"><span data-stu-id="25fa9-151">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="25fa9-152">Ensuite, vous pouvez adresser directement hello `userInfo` objet dans votre affichage :</span><span class="sxs-lookup"><span data-stu-id="25fa9-152">Then you can directly address hello `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get hello user's profile information from hello ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="25fa9-153">Vous pouvez également utiliser hello `userInfo` toodetermine de l’objet si hello utilisateur n’est connecté ou non.</span><span class="sxs-lookup"><span data-stu-id="25fa9-153">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use hello ADAL userInfo object tooshow hello right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-hello-rest-api"></a><span data-ttu-id="25fa9-154">Appeler l’API REST de hello</span><span class="sxs-lookup"><span data-stu-id="25fa9-154">Call hello REST API</span></span>
<span data-ttu-id="25fa9-155">Enfin, il est temps tooget certains jetons et un appel hello toocreate de l’API REST, lire, mettre à jour et supprimer des tâches.</span><span class="sxs-lookup"><span data-stu-id="25fa9-155">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="25fa9-156">Devinez quoi ?</span><span class="sxs-lookup"><span data-stu-id="25fa9-156">Well guess what?</span></span>  <span data-ttu-id="25fa9-157">Vous n’avez pas toodo *une chose*.</span><span class="sxs-lookup"><span data-stu-id="25fa9-157">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="25fa9-158">Adal.js se charge automatiquement d’obtenir, de mettre en cache et d’actualiser les jetons.</span><span class="sxs-lookup"><span data-stu-id="25fa9-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="25fa9-159">Il se charge également de joindre ces jetons que toooutgoing AJAX demande que vous envoyez toohello API REST.</span><span class="sxs-lookup"><span data-stu-id="25fa9-159">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="25fa9-160">Comment ceci fonctionne-t-il ?</span><span class="sxs-lookup"><span data-stu-id="25fa9-160">How exactly does this work?</span></span> <span data-ttu-id="25fa9-161">Il s’agit de tous les magique de toohello Merci de [AngularJS intercepteurs](https://docs.angularjs.org/api/ng/service/$http), ce qui permet de adal.js tootransform des messages http entrants et sortants.</span><span class="sxs-lookup"><span data-stu-id="25fa9-161">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="25fa9-162">En outre, adal.js suppose que toutes les demandes d’envoi toohello même domaine comme fenêtre hello doit utiliser des jetons destinés à hello même ID d’Application comme hello application AngularJS.</span><span class="sxs-lookup"><span data-stu-id="25fa9-162">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="25fa9-163">C’est pourquoi nous avons utilisé hello même ID d’Application dans les deux applications angulaire hello et hello NodeJS REST API.</span><span class="sxs-lookup"><span data-stu-id="25fa9-163">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="25fa9-164">Bien entendu, vous pouvez substituer ce comportement et indiquer adal.js tooget jetons pour les autres API REST si nécessaire - mais ce pourquoi ce scénario simple effectuera les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="25fa9-164">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="25fa9-165">Voici un extrait de code qui montre comment il est facile de demandes toosend avec jetons de support auprès d’Azure AD :</span><span class="sxs-lookup"><span data-stu-id="25fa9-165">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="25fa9-166">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="25fa9-166">Congratulations!</span></span>  <span data-ttu-id="25fa9-167">Votre application intégrée Azure AD à page unique est désormais terminée.</span><span class="sxs-lookup"><span data-stu-id="25fa9-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="25fa9-168">Vous pouvez lui tirer votre chapeau.</span><span class="sxs-lookup"><span data-stu-id="25fa9-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="25fa9-169">Il peut authentifier les utilisateurs en toute sécurité appeler son principal API REST en utilisant OpenID Connect et obtenir des informations de base sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="25fa9-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="25fa9-170">La boîte de hello, il prend en charge tout utilisateur disposant d’un personnel Account de Microsoft ou un compte de travail/école d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25fa9-170">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="25fa9-171">Essayer application hello en exécutant :</span><span class="sxs-lookup"><span data-stu-id="25fa9-171">Give hello app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="25fa9-172">Dans un navigateur, accédez trop`http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="25fa9-172">In a browser navigate too`http://localhost:8080`.</span></span>  <span data-ttu-id="25fa9-173">Connectez-vous à un compte personnel Microsoft ou à un compte scolaire/professionnel.</span><span class="sxs-lookup"><span data-stu-id="25fa9-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="25fa9-174">Ajouter la liste des tâches de l’utilisateur de tâches toohello et se déconnecter.  Essayez de vous connecter à l’aide de hello autre type de compte.</span><span class="sxs-lookup"><span data-stu-id="25fa9-174">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="25fa9-175">Si vous avez besoin d’un utilisateurs de travail/scolaire toocreate de client Azure AD, [Découvrez comment ici d’un tooget](active-directory-howto-tenant.md) (il est disponible).</span><span class="sxs-lookup"><span data-stu-id="25fa9-175">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="25fa9-176">toocontinue en savoir plus sur hello hello du point de terminaison v2.0, head arrière tooour [guide du développeur v2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25fa9-176">toocontinue learning about hello hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="25fa9-177">Pour obtenir des ressources supplémentaires, consultez :</span><span class="sxs-lookup"><span data-stu-id="25fa9-177">For additional resources, check out:</span></span>

* [<span data-ttu-id="25fa9-178">Exemples Azure sur GitHub &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="25fa9-178">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="25fa9-179">Azure AD sur Stack Overflow &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="25fa9-179">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="25fa9-180">Documentation Azure AD sur [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="25fa9-180">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="25fa9-181">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="25fa9-181">Get security updates for our products</span></span>
<span data-ttu-id="25fa9-182">Nous vous conseillons de notifications tooget les incidents de sécurité se produire en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="25fa9-182">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
