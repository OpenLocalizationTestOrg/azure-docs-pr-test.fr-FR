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
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a>Ajouter l’application à page unique connexion tooan AngularJS - NodeJS
Dans cet article, nous allons ajouter connectez-vous avec Microsoft sous tension comptes tooan AngularJS application à l’aide du point de terminaison v2.0 hello Azure Active Directory. point de terminaison Hello v2.0 vous tooperform une intégration unique dans votre application et authentifier les utilisateurs avec des comptes personnels et de travail/school.

Cet exemple est une application à page unique de liste de tâches qui stocke les tâches dans une API REST du serveur principal, écrite en NodeJS et sécurisée à l’aide de jetons du porteur OAuth d’Azure AD.  Hello AngularJS application utilisera notre bibliothèque d’authentification de JavaScript open source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello du processus de connexion entière et acquérir des jetons pour hello appel API REST.  Hello même modèle peut être appliqué tooauthenticate tooother API REST, comme hello [Microsoft Graph](https://graph.microsoft.com) ou hello API du Gestionnaire de ressources Azure.

> [!NOTE]
> Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.  toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

## <a name="download"></a>Télécharger
tooget démarré, vous devez toodownload & installer [node.js](https://nodejs.org).  Vous pouvez ensuite cloner ou [télécharger](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) une application squelette :

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

application squelette Hello inclut tout le code réutilisable hello pour une application AngularJS simple, mais il manque l’intégralité des hello liées à l’identité.  Si vous ne souhaitez pas toofollow le long, vous pouvez à la place cloner ou [télécharger](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) exemple hello s’est terminée.

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a>Inscription d’une application
Tout d’abord, créez une application dans hello [portail de l’enregistrement d’application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou procédez [une procédure détaillée](active-directory-v2-app-registration.md).  Veillez à respecter les points suivants :

* Ajouter hello **Web** plate-forme pour votre application.
* Entrez hello correct **URI de redirection**. valeur par défaut de Hello pour cet exemple est `http://localhost:8080`.
* Laissez hello **autorise le flux implicite** case à cocher activée. 

Copie vers le bas hello **ID d’Application** qui est attribué tooyour application, vous en aurez besoin dans quelques instants. 

## <a name="install-adaljs"></a>Installer adal.js
toostart, accédez tooproject que vous avez téléchargé et installez adal.js.  Si [bower](http://bower.io/) est installé, il vous suffit d’exécuter cette commande.  Pour toutes les incompatibilités au niveau de la version de dépendance, choisissez une version supérieure hello.

```
bower install adal-angular#experimental
```

Sinon, vous pouvez télécharger manuellement [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) et [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).  Ajoutez les deux fichiers toohello `app/lib/adal-angular-experimental/dist` active.

Ouvrez projet de hello dans votre éditeur de texte et charger adal.js à fin hello hello du corps de page :

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a>Configurer hello API REST
Pendant que nous configurons choses, permet l’utilisation d’API REST get hello back-end.  Dans une invite de commandes, installez tous les packages nécessaires hello en exécutant (Assurez-vous que vous êtes dans le répertoire de niveau supérieur de hello du projet de hello) :

```
npm install
```

À présent ouvrir `config.js` et remplacer hello `audience` valeur :

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

Hello API REST utilisera cette jetons toovalidate de valeur qu’il reçoit à partir de l’application angulaire hello sur les requêtes AJAX.  Notez que cette API REST simple stocke les données en mémoire - pour chaque serveur de hello toostop temps, vous perdrez toutes les tâches créées précédemment.

C’est tout temps hello, nous allons toospend décrivant le fonctionne de l’API REST de hello.  Pensez toopoke libre dans le code hello, mais si vous souhaitez toolearn plus d’informations sur la sécurisation d’API avec Azure AD, consultez [cet article](active-directory-v2-devquickstarts-node-api.md). 

## <a name="sign-users-in"></a>Connecter les utilisateurs
Temps toowrite du code d’identité.  Vous avez peut-être remarqué que adal.js contient un fournisseur AngularJS, qui se combine parfaitement aux mécanismes de routage Angular.  Commencez par ajouter hello module adal toohello application :

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

Vous pouvez désormais initialiser hello `adalProvider` avec votre ID d’Application :

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

Très bien adal.js a toutes les informations de hello, elle doit toosecure vos utilisateurs d’application et connectez-vous dans.  connexions tooforce pour un itinéraire particulier dans une application hello, il sont une ligne de code :

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

Quand un utilisateur clique sur hello `TodoList` lien, adal.js redirige automatiquement tooAzure AD pour la connexion si nécessaire.  Vous pouvez également envoyer explicitement des requêtes de connexion et de déconnexion en invoquant adal.js dans vos contrôleurs :

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

## <a name="display-user-info"></a>Afficher les informations utilisateur
Maintenant que hello utilisateur n’est connecté, vous devez probablement des données d’authentification tooaccess hello signé de l’utilisateur dans votre application.  Adal.js expose ces informations pour vous dans hello `userInfo` objet.  tooaccess cet objet dans une vue, ajoutez d’abord étendue de racine adal.js toohello de contrôleur correspondant de hello :

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

Ensuite, vous pouvez adresser directement hello `userInfo` objet dans votre affichage : 

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

Vous pouvez également utiliser hello `userInfo` toodetermine de l’objet si hello utilisateur n’est connecté ou non.

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

## <a name="call-hello-rest-api"></a>Appeler l’API REST de hello
Enfin, il est temps tooget certains jetons et un appel hello toocreate de l’API REST, lire, mettre à jour et supprimer des tâches.  Devinez quoi ?  Vous n’avez pas toodo *une chose*.  Adal.js se charge automatiquement d’obtenir, de mettre en cache et d’actualiser les jetons.  Il se charge également de joindre ces jetons que toooutgoing AJAX demande que vous envoyez toohello API REST.  

Comment ceci fonctionne-t-il ? Il s’agit de tous les magique de toohello Merci de [AngularJS intercepteurs](https://docs.angularjs.org/api/ng/service/$http), ce qui permet de adal.js tootransform des messages http entrants et sortants.  En outre, adal.js suppose que toutes les demandes d’envoi toohello même domaine comme fenêtre hello doit utiliser des jetons destinés à hello même ID d’Application comme hello application AngularJS.  C’est pourquoi nous avons utilisé hello même ID d’Application dans les deux applications angulaire hello et hello NodeJS REST API.  Bien entendu, vous pouvez substituer ce comportement et indiquer adal.js tooget jetons pour les autres API REST si nécessaire - mais ce pourquoi ce scénario simple effectuera les valeurs par défaut.

Voici un extrait de code qui montre comment il est facile de demandes toosend avec jetons de support auprès d’Azure AD :

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

Félicitations !  Votre application intégrée Azure AD à page unique est désormais terminée.  Vous pouvez lui tirer votre chapeau.  Il peut authentifier les utilisateurs en toute sécurité appeler son principal API REST en utilisant OpenID Connect et obtenir des informations de base sur l’utilisateur de hello.  La boîte de hello, il prend en charge tout utilisateur disposant d’un personnel Account de Microsoft ou un compte de travail/école d’Azure AD.  Essayer application hello en exécutant :

```
node server.js
```

Dans un navigateur, accédez trop`http://localhost:8080`.  Connectez-vous à un compte personnel Microsoft ou à un compte scolaire/professionnel.  Ajouter la liste des tâches de l’utilisateur de tâches toohello et se déconnecter.  Essayez de vous connecter à l’aide de hello autre type de compte. Si vous avez besoin d’un utilisateurs de travail/scolaire toocreate de client Azure AD, [Découvrez comment ici d’un tooget](active-directory-howto-tenant.md) (il est disponible).

toocontinue en savoir plus sur hello hello du point de terminaison v2.0, head arrière tooour [guide du développeur v2.0](active-directory-appmodel-v2-overview.md).  Pour obtenir des ressources supplémentaires, consultez :

* [Exemples Azure sur GitHub &gt;&gt;](https://github.com/Azure-Samples)
* [Azure AD sur Stack Overflow &gt;&gt;](http://stackoverflow.com/questions/tagged/azure-active-directory)
* Documentation Azure AD sur [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)

## <a name="get-security-updates-for-our-products"></a>Obtenir les mises à jour de sécurité de nos produits
Nous vous conseillons de notifications tooget les incidents de sécurité se produire en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.

