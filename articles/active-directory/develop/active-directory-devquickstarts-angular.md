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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="da207-103">Sécuriser les applications à page unique AngularJS à l’aide d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="da207-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="da207-104">Azure Active Directory (Azure AD), il est simple et simple pour vous tooadd connexion, déconnexion, et seule page applications tooyour d’appels d’API d’OAuth sécurisé.</span><span class="sxs-lookup"><span data-stu-id="da207-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you tooadd sign-in, sign-out, and secure OAuth API calls tooyour single-page apps.</span></span>  <span data-ttu-id="da207-105">Il permet à vos utilisateurs de tooauthenticate d’applications avec leurs comptes Active Directory Windows Server et consommer des API Azure AD permet de protéger, telles que hello API Office 365 ou hello Azure API web.</span><span class="sxs-lookup"><span data-stu-id="da207-105">It enables your apps tooauthenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="da207-106">Pour les applications JavaScript s’exécutant dans un navigateur, Azure AD fournit hello Active Directory Authentication Library (ADAL), ou adal.js.</span><span class="sxs-lookup"><span data-stu-id="da207-106">For JavaScript applications running in a browser, Azure AD provides hello Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="da207-107">Hello seul but de adal.js est toomake plus facile pour les jetons d’accès tooget votre application.</span><span class="sxs-lookup"><span data-stu-id="da207-107">hello sole purpose of adal.js is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="da207-108">toodemonstrate facilité il s’agit, ici, nous créerons une application de liste de tooDo AngularJS qui :</span><span class="sxs-lookup"><span data-stu-id="da207-108">toodemonstrate just how easy it is, here we'll build an AngularJS tooDo List application that:</span></span>

* <span data-ttu-id="da207-109">Utilisateur se connecte hello dans application toohello à l’aide d’Azure AD en tant que fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="da207-109">Signs hello user in toohello app by using Azure AD as hello identity provider.</span></span>

* <span data-ttu-id="da207-110">Affiche des informations sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="da207-110">Displays some information about hello user.</span></span>
* <span data-ttu-id="da207-111">En toute sécurité les appels hello tooDo de l’application API liste à l’aide de jetons de support auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da207-111">Securely calls hello app's tooDo List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="da207-112">Signes hello utilisateur hors de l’application de hello.</span><span class="sxs-lookup"><span data-stu-id="da207-112">Signs hello user out of hello app.</span></span>

<span data-ttu-id="da207-113">toobuild hello, travail application complète, vous devez :</span><span class="sxs-lookup"><span data-stu-id="da207-113">toobuild hello complete, working application, you need to:</span></span>

1. <span data-ttu-id="da207-114">Inscrire votre application auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da207-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="da207-115">Installer la bibliothèque ADAL et configurer l’application hello une seule page.</span><span class="sxs-lookup"><span data-stu-id="da207-115">Install ADAL and configure hello single-page app.</span></span>
3. <span data-ttu-id="da207-116">Utiliser les pages sécurisées toohelp ADAL dans l’application une seule page hello.</span><span class="sxs-lookup"><span data-stu-id="da207-116">Use ADAL toohelp secure pages in hello single-page app.</span></span>

<span data-ttu-id="da207-117">tooget démarré, [télécharger squelette d’application hello](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="da207-117">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="da207-118">Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="da207-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="da207-119">Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="da207-119">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-hello-directorysearcher-application"></a><span data-ttu-id="da207-120">Étape 1 : Inscrire l’application de DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="da207-120">Step 1: Register hello DirectorySearcher application</span></span>
<span data-ttu-id="da207-121">tooenable vos utilisateurs de tooauthenticate d’application et des jetons de get, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client :</span><span class="sxs-lookup"><span data-stu-id="da207-121">tooenable your app tooauthenticate users and get tokens, you first need tooregister it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="da207-122">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="da207-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="da207-123">Si vous êtes connecté dans les répertoires toomultiple, vous devrez peut-être tooensure vous visualisez le répertoire approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="da207-123">If you are signed in toomultiple directories, you may need tooensure you are viewing hello correct directory.</span></span> <span data-ttu-id="da207-124">toodo, sur la barre supérieure de hello, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="da207-124">toodo so, on hello top bar, click your account.</span></span> <span data-ttu-id="da207-125">Sous hello **répertoire** , choisissez locataire hello AD Azure où vous souhaitez tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="da207-125">Under hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="da207-126">Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="da207-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="da207-127">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="da207-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="da207-128">Suivez les invites hello et créer une nouvelle application web et/ou une API web :</span><span class="sxs-lookup"><span data-stu-id="da207-128">Follow hello prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="da207-129">**Nom** décrit toousers de votre application.</span><span class="sxs-lookup"><span data-stu-id="da207-129">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="da207-130">**Uri de redirection** est hello emplacement toowhich Azure AD renvoyer des jetons.</span><span class="sxs-lookup"><span data-stu-id="da207-130">**Redirect Uri** is hello location toowhich Azure AD will return tokens.</span></span> <span data-ttu-id="da207-131">emplacement par défaut de Hello pour cet exemple est `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="da207-131">hello default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="da207-132">Une fois que vous avez terminé l’inscription, Azure AD assigne une application de tooyour ID unique d’application.</span><span class="sxs-lookup"><span data-stu-id="da207-132">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span>  <span data-ttu-id="da207-133">Vous aurez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de l’onglet de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="da207-133">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="da207-134">Adal.js utilise toocommunicate de flux implicites hello OAuth avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da207-134">Adal.js uses hello OAuth implicit flow toocommunicate with Azure AD.</span></span> <span data-ttu-id="da207-135">Vous devez activer les flux implicites hello pour votre application :</span><span class="sxs-lookup"><span data-stu-id="da207-135">You must enable hello implicit flow for your application:</span></span>
  1. <span data-ttu-id="da207-136">Cliquez sur l’application hello et sélectionnez **manifeste** éditeur de manifeste tooopen hello inline.</span><span class="sxs-lookup"><span data-stu-id="da207-136">Click hello application and select **Manifest** tooopen hello inline manifest editor.</span></span>
  2. <span data-ttu-id="da207-137">Recherchez hello `oauth2AllowImplicitFlow` propriété.</span><span class="sxs-lookup"><span data-stu-id="da207-137">Locate hello `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="da207-138">Définissez sa valeur trop`true`.</span><span class="sxs-lookup"><span data-stu-id="da207-138">Set its value too`true`.</span></span>
  3. <span data-ttu-id="da207-139">Cliquez sur **enregistrer** manifeste de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="da207-139">Click **Save** toosave hello manifest.</span></span>
8. <span data-ttu-id="da207-140">Accordez les autorisations à votre locataire sur votre application.</span><span class="sxs-lookup"><span data-stu-id="da207-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="da207-141">Accédez trop**paramètres** > **propriétés** > **autorisations requises**, puis cliquez sur hello **accorder des autorisations**bouton sur la barre supérieure de hello.</span><span class="sxs-lookup"><span data-stu-id="da207-141">Go too**Settings** > **Properties** > **Required Permissions**, and click hello **Grant Permissions** button on hello top bar.</span></span> <span data-ttu-id="da207-142">Cliquez sur **Oui** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="da207-142">Click **Yes** tooconfirm.</span></span>

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a><span data-ttu-id="da207-143">Étape 2 : Installer la bibliothèque ADAL et configurer l’application hello une seule page</span><span class="sxs-lookup"><span data-stu-id="da207-143">Step 2: Install ADAL and configure hello single-page app</span></span>
<span data-ttu-id="da207-144">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer adal.js et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="da207-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-hello-javascript-client"></a><span data-ttu-id="da207-145">Configurer le client JavaScript de hello</span><span class="sxs-lookup"><span data-stu-id="da207-145">Configure hello JavaScript client</span></span>
<span data-ttu-id="da207-146">Commencez par ajouter des adal.js toohello TodoSPA projet à l’aide de hello Console du Gestionnaire de Package :</span><span class="sxs-lookup"><span data-stu-id="da207-146">Begin by adding adal.js toohello TodoSPA project by using hello Package Manager Console:</span></span>
  1. <span data-ttu-id="da207-147">Télécharger [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) et ajoutez-le toohello `App/Scripts/` répertoire du projet.</span><span class="sxs-lookup"><span data-stu-id="da207-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it toohello `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="da207-148">Télécharger [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) et ajoutez-le toohello `App/Scripts/` répertoire du projet.</span><span class="sxs-lookup"><span data-stu-id="da207-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it toohello `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="da207-149">Charger chaque script avant la fin de hello de hello `</body>` dans `index.html`:</span><span class="sxs-lookup"><span data-stu-id="da207-149">Load each script before hello end of hello `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a><span data-ttu-id="da207-150">Configurer le serveur principal hello</span><span class="sxs-lookup"><span data-stu-id="da207-150">Configure hello back end server</span></span>
<span data-ttu-id="da207-151">Pour principal tooDo API liste tooaccept jetons l’application hello seule page à partir du navigateur de hello, back-end hello a besoin des informations de configuration sur l’inscription d’une application hello.</span><span class="sxs-lookup"><span data-stu-id="da207-151">For hello single-page app's back-end tooDo List API tooaccept tokens from hello browser, hello back end needs configuration information about hello app registration.</span></span> <span data-ttu-id="da207-152">Dans le projet de TodoSPA hello, ouvrez `web.config`.</span><span class="sxs-lookup"><span data-stu-id="da207-152">In hello TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="da207-153">Remplacez les valeurs hello d’éléments hello Bonjour `<appSettings>` section tooreflect hello valeurs que vous avez utilisé dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="da207-153">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="da207-154">Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="da207-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="da207-155">`ida:Tenant`est le domaine hello de votre client Azure AD--par exemple, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="da207-155">`ida:Tenant` is hello domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="da207-156">`ida:Audience`est l’ID de client hello de votre application que vous avez copié à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="da207-156">`ida:Audience` is hello client ID of your application that you copied from hello portal.</span></span>

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a><span data-ttu-id="da207-157">Étape 3 : Utilisation toohelp ADAL les pages sécurisées dans l’application hello une seule page</span><span class="sxs-lookup"><span data-stu-id="da207-157">Step 3: Use ADAL toohelp secure pages in hello single-page app</span></span>
<span data-ttu-id="da207-158">Adal.js s’intègre avec l’itinéraire AngularJS t les fournisseurs HTTP afin de permettre de sécuriser les vues individuelles dans votre application à page unique.</span><span class="sxs-lookup"><span data-stu-id="da207-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="da207-159">Dans `App/Scripts/app.js`, placer dans le module de adal.js hello :</span><span class="sxs-lookup"><span data-stu-id="da207-159">In `App/Scripts/app.js`, bring in hello adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="da207-160">Initialiser `adalProvider` à l’aide des valeurs de configuration hello de l’enregistrement de l’application, également dans `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="da207-160">Initialize `adalProvider` by using hello configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="da207-161">Aider à sécuriser hello `TodoList` vue dans une application hello à l’aide d’une seule ligne de code : `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="da207-161">Help secure hello `TodoList` view in hello app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="da207-162">Résumé</span><span class="sxs-lookup"><span data-stu-id="da207-162">Summary</span></span>
<span data-ttu-id="da207-163">Vous disposez maintenant d’une application de page unique sécurisée qui peut se connecter aux utilisateurs et émettre des demandes de jeton de support protégé tooits principal API.</span><span class="sxs-lookup"><span data-stu-id="da207-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests tooits back-end API.</span></span> <span data-ttu-id="da207-164">Lorsqu’un utilisateur clique hello **TodoList** lien, adal.js redirige automatiquement tooAzure AD pour la connexion si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="da207-164">When a user clicks hello **TodoList** link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span> <span data-ttu-id="da207-165">En outre, adal.js attachera automatiquement un accès jeton tooany Qu'ajax demande envoyées back-end toohello de l’application.</span><span class="sxs-lookup"><span data-stu-id="da207-165">In addition, adal.js will automatically attach an access token tooany Ajax requests that are sent toohello app's back end.</span></span>  

<span data-ttu-id="da207-166">Hello étapes précédentes sont une application une seule page hello bare toobuild de nécessaires minimale à l’aide de adal.js.</span><span class="sxs-lookup"><span data-stu-id="da207-166">hello preceding steps are hello bare minimum necessary toobuild a single-page app by using adal.js.</span></span> <span data-ttu-id="da207-167">Mais certaines autres fonctionnalités sont utiles dans application à page unique :</span><span class="sxs-lookup"><span data-stu-id="da207-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="da207-168">tooexplicitly émettent des demandes de connexion et déconnexion, vous pouvez définir des fonctions dans vos contrôleurs qui appellent adal.js.</span><span class="sxs-lookup"><span data-stu-id="da207-168">tooexplicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="da207-169">Dans `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="da207-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="da207-170">Vous pourriez toopresent des informations utilisateur dans l’interface utilisateur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="da207-170">You might want toopresent user information in hello app's UI.</span></span> <span data-ttu-id="da207-171">Hello ADAL service a déjà été ajouté à toohello `userDataCtrl` contrôleur, afin que vous pouvez accéder aux hello `userInfo` objet Bonjour associé vue, `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="da207-171">hello ADAL service has already been added toohello `userDataCtrl` controller, so you can access hello `userInfo` object in hello associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="da207-172">Il existe plusieurs scénarios dans lesquels vous voulez tooknow si hello utilisateur n’est connecté ou non.</span><span class="sxs-lookup"><span data-stu-id="da207-172">There are many scenarios in which you'll want tooknow if hello user is signed in or not.</span></span> <span data-ttu-id="da207-173">Vous pouvez également utiliser hello `userInfo` objet toogather ces informations.</span><span class="sxs-lookup"><span data-stu-id="da207-173">You can also use hello `userInfo` object toogather this information.</span></span>  <span data-ttu-id="da207-174">Par exemple, dans `index.html`, vous pouvez afficher soit hello **connexion** ou **déconnexion** bouton en fonction de l’état d’authentification :</span><span class="sxs-lookup"><span data-stu-id="da207-174">For instance, in `index.html`, you can show either hello **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="da207-175">Votre application une seule page intégrée à Active Directory Azure peut authentifier les utilisateurs, en toute sécurité appeler le back-end à l’aide d’OAuth 2.0 et obtenir des informations de base sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="da207-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about hello user.</span></span> <span data-ttu-id="da207-176">Si vous n’avez pas encore, est à présent hello temps toopopulate votre locataire avec certains utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="da207-176">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span> <span data-ttu-id="da207-177">Exécutez votre application une seule page liste tooDo et connectez-vous avec l’un de ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="da207-177">Run your tooDo List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="da207-178">Ajouter la liste des tâches de l’utilisateur de tâches toohello, déconnectez-vous et reconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="da207-178">Add tasks toohello user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="da207-179">Adal.js rend fonctionnalités d’identité commune tooincorporate facile dans votre application.</span><span class="sxs-lookup"><span data-stu-id="da207-179">Adal.js makes it easy tooincorporate common identity features into your application.</span></span> <span data-ttu-id="da207-180">Il s’occupe de tout le travail dirty hello pour vous : gestion du cache, la prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une signe dans l’interface utilisateur, l’actualisation des jetons expirés et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="da207-180">It takes care of all hello dirty work for you: cache management, OAuth protocol support, presenting hello user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="da207-181">Pour référence, l’exemple hello terminée (sans les valeurs de configuration) est disponible dans [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="da207-181">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="da207-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="da207-182">Next steps</span></span>
<span data-ttu-id="da207-183">Vous pouvez maintenant déplacer sur les scénarios de tooadditional.</span><span class="sxs-lookup"><span data-stu-id="da207-183">You can now move on tooadditional scenarios.</span></span> <span data-ttu-id="da207-184">Vous souhaiterez peut-être tootry : [appeler une API de web CORS à partir d’une application une seule page](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="da207-184">You might want tootry: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
