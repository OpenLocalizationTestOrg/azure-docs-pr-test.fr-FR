---
title: aaaAzure AD AngularJS prise en main | Documents Microsoft
description: "Comment toobuild une application de page unique AngularJS qui s’intègre avec Azure AD pour la connexion et appelle les API de protégé par AD Azure à l’aide d’OAuth."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: eca5e1c9662186dfae4f96ca3041f9350583cf79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>Sécuriser les applications à page unique AngularJS à l’aide d’Azure AD

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (Azure AD), il est simple et simple pour vous tooadd connexion, déconnexion, et seule page applications tooyour d’appels d’API d’OAuth sécurisé.  Il permet à vos utilisateurs de tooauthenticate d’applications avec leurs comptes Active Directory Windows Server et consommer des API Azure AD permet de protéger, telles que hello API Office 365 ou hello Azure API web.

Pour les applications JavaScript s’exécutant dans un navigateur, Azure AD fournit hello Active Directory Authentication Library (ADAL), ou adal.js. Hello seul but de adal.js est toomake plus facile pour les jetons d’accès tooget votre application. toodemonstrate facilité il s’agit, ici, nous créerons une application de liste de tooDo AngularJS qui :

* Utilisateur se connecte hello dans application toohello à l’aide d’Azure AD en tant que fournisseur d’identité hello.

* Affiche des informations sur l’utilisateur de hello.
* En toute sécurité les appels hello tooDo de l’application API liste à l’aide de jetons de support auprès d’Azure AD.
* Signes hello utilisateur hors de l’application de hello.

toobuild hello, travail application complète, vous devez :

1. Inscrire votre application auprès d’Azure AD.
2. Installer la bibliothèque ADAL et configurer l’application hello une seule page.
3. Utiliser les pages sécurisées toohelp ADAL dans l’application une seule page hello.

tooget démarré, [télécharger squelette d’application hello](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip). Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application. Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).

## <a name="step-1-register-hello-directorysearcher-application"></a>Étape 1 : Inscrire l’application de DirectorySearcher hello
tooenable vos utilisateurs de tooauthenticate d’application et des jetons de get, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Si vous êtes connecté dans les répertoires toomultiple, vous devrez peut-être tooensure vous visualisez le répertoire approprié de hello. toodo, sur la barre supérieure de hello, cliquez sur votre compte. Sous hello **répertoire** , choisissez locataire hello AD Azure où vous souhaitez tooregister votre application.
3. Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.
5. Suivez les invites hello et créer une nouvelle application web et/ou une API web :
  * **Nom** décrit toousers de votre application.
  * **Uri de redirection** est hello emplacement toowhich Azure AD renvoyer des jetons. emplacement par défaut de Hello pour cet exemple est `https://localhost:44326/`.
6. Une fois que vous avez terminé l’inscription, Azure AD assigne une application de tooyour ID unique d’application.  Vous aurez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de l’onglet de l’application hello.
7. Adal.js utilise toocommunicate de flux implicites hello OAuth avec Azure AD. Vous devez activer les flux implicites hello pour votre application :
  1. Cliquez sur l’application hello et sélectionnez **manifeste** éditeur de manifeste tooopen hello inline.
  2. Recherchez hello `oauth2AllowImplicitFlow` propriété. Définissez sa valeur trop`true`.
  3. Cliquez sur **enregistrer** manifeste de hello toosave.
8. Accordez les autorisations à votre locataire sur votre application. Accédez trop**paramètres** > **propriétés** > **autorisations requises**, puis cliquez sur hello **accorder des autorisations**bouton sur la barre supérieure de hello. Cliquez sur **Oui** tooconfirm.

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a>Étape 2 : Installer la bibliothèque ADAL et configurer l’application hello une seule page
Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer adal.js et écrire votre code lié à l’identité.

### <a name="configure-hello-javascript-client"></a>Configurer le client JavaScript de hello
Commencez par ajouter des adal.js toohello TodoSPA projet à l’aide de hello Console du Gestionnaire de Package :
  1. Télécharger [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) et ajoutez-le toohello `App/Scripts/` répertoire du projet.
  2. Télécharger [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) et ajoutez-le toohello `App/Scripts/` répertoire du projet.
  3. Charger chaque script avant la fin de hello de hello `</body>` dans `index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a>Configurer le serveur principal hello
Pour principal tooDo API liste tooaccept jetons l’application hello seule page à partir du navigateur de hello, back-end hello a besoin des informations de configuration sur l’inscription d’une application hello. Dans le projet de TodoSPA hello, ouvrez `web.config`. Remplacez les valeurs hello d’éléments hello Bonjour `<appSettings>` section tooreflect hello valeurs que vous avez utilisé dans hello portail Azure. Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.
  * `ida:Tenant`est le domaine hello de votre client Azure AD--par exemple, contoso.onmicrosoft.com.
  * `ida:Audience`est l’ID de client hello de votre application que vous avez copié à partir du portail de hello.

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a>Étape 3 : Utilisation toohelp ADAL les pages sécurisées dans l’application hello une seule page
Adal.js s’intègre avec l’itinéraire AngularJS t les fournisseurs HTTP afin de permettre de sécuriser les vues individuelles dans votre application à page unique.

1. Dans `App/Scripts/app.js`, placer dans le module de adal.js hello :

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. Initialiser `adalProvider` à l’aide des valeurs de configuration hello de l’enregistrement de l’application, également dans `App/Scripts/app.js`:

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. Aider à sécuriser hello `TodoList` vue dans une application hello à l’aide d’une seule ligne de code : `requireADLogin`.

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>Résumé
Vous disposez maintenant d’une application de page unique sécurisée qui peut se connecter aux utilisateurs et émettre des demandes de jeton de support protégé tooits principal API. Lorsqu’un utilisateur clique hello **TodoList** lien, adal.js redirige automatiquement tooAzure AD pour la connexion si nécessaire. En outre, adal.js attachera automatiquement un accès jeton tooany Qu'ajax demande envoyées back-end toohello de l’application.  

Hello étapes précédentes sont une application une seule page hello bare toobuild de nécessaires minimale à l’aide de adal.js. Mais certaines autres fonctionnalités sont utiles dans application à page unique :

* tooexplicitly émettent des demandes de connexion et déconnexion, vous pouvez définir des fonctions dans vos contrôleurs qui appellent adal.js.  Dans `App/Scripts/homeCtrl.js`:

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* Vous pourriez toopresent des informations utilisateur dans l’interface utilisateur de l’application hello. Hello ADAL service a déjà été ajouté à toohello `userDataCtrl` contrôleur, afin que vous pouvez accéder aux hello `userInfo` objet Bonjour associé vue, `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* Il existe plusieurs scénarios dans lesquels vous voulez tooknow si hello utilisateur n’est connecté ou non. Vous pouvez également utiliser hello `userInfo` objet toogather ces informations.  Par exemple, dans `index.html`, vous pouvez afficher soit hello **connexion** ou **déconnexion** bouton en fonction de l’état d’authentification :

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

Votre application une seule page intégrée à Active Directory Azure peut authentifier les utilisateurs, en toute sécurité appeler le back-end à l’aide d’OAuth 2.0 et obtenir des informations de base sur l’utilisateur de hello. Si vous n’avez pas encore, est à présent hello temps toopopulate votre locataire avec certains utilisateurs. Exécutez votre application une seule page liste tooDo et connectez-vous avec l’un de ces utilisateurs. Ajouter la liste des tâches de l’utilisateur de tâches toohello, déconnectez-vous et reconnectez-vous.

Adal.js rend fonctionnalités d’identité commune tooincorporate facile dans votre application. Il s’occupe de tout le travail dirty hello pour vous : gestion du cache, la prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une signe dans l’interface utilisateur, l’actualisation des jetons expirés et bien plus encore.

Pour référence, l’exemple hello terminée (sans les valeurs de configuration) est disponible dans [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez maintenant déplacer sur les scénarios de tooadditional. Vous souhaiterez peut-être tootry : [appeler une API de web CORS à partir d’une application une seule page](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
