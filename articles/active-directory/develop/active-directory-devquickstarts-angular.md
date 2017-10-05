---
title: "Bien démarrer avec Azure AD AngularJS | Microsoft Docs"
description: "Création d’une application à page unique AngularJS qui s’intègre avec Azure AD pour la connexion et appelle des API protégées par Azure AD à l’aide d’OAuth."
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
ms.openlocfilehash: 4153910bc03f112f84c26cda6f9c78f11028b934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="3898c-103">Sécuriser les applications à page unique AngularJS à l’aide d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="3898c-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="3898c-104">Azure Active Directory (Azure AD) simplifie l’ajout d’appels API OAuth de connexion, de déconnexion et de sécurisation à vos applications à page unique.</span><span class="sxs-lookup"><span data-stu-id="3898c-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span></span>  <span data-ttu-id="3898c-105">Il permet à votre application d’authentifier les utilisateurs avec leurs comptes Windows Server Active Directory et de consommer une API web protégée par Azure AD, telle que l’API Office 365 ou Azure.</span><span class="sxs-lookup"><span data-stu-id="3898c-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="3898c-106">Pour les applications JavaScript s’exécutant dans un navigateur, Azure AD fournit la bibliothèque d’authentification Active Directory (ADAL) ou adal.js.</span><span class="sxs-lookup"><span data-stu-id="3898c-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="3898c-107">adal.js a pour seule fonction de simplifier l’obtention des jetons d’accès pour votre application.</span><span class="sxs-lookup"><span data-stu-id="3898c-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="3898c-108">Pour illustrer sa facilité d’utilisation, nous allons créer une application de liste des tâches AngularJS qui effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="3898c-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span></span>

* <span data-ttu-id="3898c-109">connecte l’utilisateur à l’application à l’aide d’Azure AD comme fournisseur d’identité ;</span><span class="sxs-lookup"><span data-stu-id="3898c-109">Signs the user in to the app by using Azure AD as the identity provider.</span></span>

* <span data-ttu-id="3898c-110">affiche des informations sur l’utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="3898c-110">Displays some information about the user.</span></span>
* <span data-ttu-id="3898c-111">appelle en toute sécurité l’API de liste des tâches de l’application en utilisant des jetons porteurs d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="3898c-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="3898c-112">déconnecte l’utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="3898c-112">Signs the user out of the app.</span></span>

<span data-ttu-id="3898c-113">Pour générer l’application fonctionnelle complète, vous devez :</span><span class="sxs-lookup"><span data-stu-id="3898c-113">To build the complete, working application, you need to:</span></span>

1. <span data-ttu-id="3898c-114">Inscrire votre application auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3898c-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="3898c-115">Installer la bibliothèque ADAL et configurer l’application à page unique.</span><span class="sxs-lookup"><span data-stu-id="3898c-115">Install ADAL and configure the single-page app.</span></span>
3. <span data-ttu-id="3898c-116">Utilisez la bibliothèque ADAL pour sécuriser les pages dans l’application à page unique.</span><span class="sxs-lookup"><span data-stu-id="3898c-116">Use ADAL to help secure pages in the single-page app.</span></span>

<span data-ttu-id="3898c-117">Pour commencer, téléchargez [la structure de l’application](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) ou [l’exemple terminé](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="3898c-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="3898c-118">Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="3898c-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="3898c-119">Si vous ne disposez pas encore d’un client, [découvrez comment en obtenir un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="3898c-119">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-the-directorysearcher-application"></a><span data-ttu-id="3898c-120">Étape 1 : Inscrire l’application DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="3898c-120">Step 1: Register the DirectorySearcher application</span></span>
<span data-ttu-id="3898c-121">Pour autoriser votre application à authentifier les utilisateurs et à obtenir des jetons, vous devez tout d’abord l’inscrire dans votre client Azure AD :</span><span class="sxs-lookup"><span data-stu-id="3898c-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="3898c-122">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3898c-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3898c-123">Si vous êtes connecté à plusieurs répertoires, vous devez peut-être vous assurer que vous consultez le répertoire approprié.</span><span class="sxs-lookup"><span data-stu-id="3898c-123">If you are signed in to multiple directories, you may need to ensure you are viewing the correct directory.</span></span> <span data-ttu-id="3898c-124">Pour ce faire, dans la barre supérieure, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="3898c-124">To do so, on the top bar, click your account.</span></span> <span data-ttu-id="3898c-125">Dans la liste **Répertoire**, choisissez le locataire Azure AD auprès duquel vous voulez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="3898c-125">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="3898c-126">Dans le volet gauche, cliquez sur **Plus de services**, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3898c-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="3898c-127">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3898c-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="3898c-128">Suivez les invites et créez une application web et/ou API web :</span><span class="sxs-lookup"><span data-stu-id="3898c-128">Follow the prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="3898c-129">**Nom** décrit votre application pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3898c-129">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="3898c-130">**URI de redirection** est l’emplacement auquel Azure AD renvoie les jetons.</span><span class="sxs-lookup"><span data-stu-id="3898c-130">**Redirect Uri** is the location to which Azure AD will return tokens.</span></span> <span data-ttu-id="3898c-131">L’emplacement par défaut de cet exemple est `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="3898c-131">The default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="3898c-132">Une fois l’inscription terminée, Azure AD affecte un ID d’application unique à votre application.</span><span class="sxs-lookup"><span data-stu-id="3898c-132">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span>  <span data-ttu-id="3898c-133">Copiez cette valeur dans l’onglet de l’application, car vous en aurez besoin dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="3898c-133">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="3898c-134">Adal.js utilise le flux implicite OAuth pour communiquer avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3898c-134">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span></span> <span data-ttu-id="3898c-135">Vous devez activer ce flux pour votre application :</span><span class="sxs-lookup"><span data-stu-id="3898c-135">You must enable the implicit flow for your application:</span></span>
  1. <span data-ttu-id="3898c-136">Cliquez sur l’application et sélectionnez **Manifeste** pour ouvrir l’éditeur de manifeste en ligne.</span><span class="sxs-lookup"><span data-stu-id="3898c-136">Click the application and select **Manifest** to open the inline manifest editor.</span></span>
  2. <span data-ttu-id="3898c-137">Recherchez la propriété `oauth2AllowImplicitFlow`.</span><span class="sxs-lookup"><span data-stu-id="3898c-137">Locate the `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="3898c-138">Affectez-lui la valeur `true`.</span><span class="sxs-lookup"><span data-stu-id="3898c-138">Set its value to `true`.</span></span>
  3. <span data-ttu-id="3898c-139">Cliquez sur **Enregistrer** pour enregistrer le manifeste.</span><span class="sxs-lookup"><span data-stu-id="3898c-139">Click **Save** to save the manifest.</span></span>
8. <span data-ttu-id="3898c-140">Accordez les autorisations à votre locataire sur votre application.</span><span class="sxs-lookup"><span data-stu-id="3898c-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="3898c-141">Sélectionnez **Paramètres** > **Propriétés** > **Autorisations requises**, puis cliquez sur le bouton **Accorder des autorisations** dans la barre supérieure.</span><span class="sxs-lookup"><span data-stu-id="3898c-141">Go to **Settings** > **Properties** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span></span> <span data-ttu-id="3898c-142">Cliquez sur **Yes** (Oui) pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="3898c-142">Click **Yes** to confirm.</span></span>

## <a name="step-2-install-adal-and-configure-the-single-page-app"></a><span data-ttu-id="3898c-143">Étape 2 : Installer la bibliothèque ADAL et configurer l’application à page unique</span><span class="sxs-lookup"><span data-stu-id="3898c-143">Step 2: Install ADAL and configure the single-page app</span></span>
<span data-ttu-id="3898c-144">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer adal.js et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="3898c-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-the-javascript-client"></a><span data-ttu-id="3898c-145">Configurer le client JavaScript</span><span class="sxs-lookup"><span data-stu-id="3898c-145">Configure the JavaScript client</span></span>
<span data-ttu-id="3898c-146">Commencez par ajouter adal.js au projet TodoSPA à l’aide de la console du gestionnaire de package :</span><span class="sxs-lookup"><span data-stu-id="3898c-146">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span></span>
  1. <span data-ttu-id="3898c-147">Téléchargez [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) et ajoutez-le au répertoire du projet `App/Scripts/`.</span><span class="sxs-lookup"><span data-stu-id="3898c-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="3898c-148">Téléchargez [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) et ajoutez-le au répertoire du projet `App/Scripts/`.</span><span class="sxs-lookup"><span data-stu-id="3898c-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="3898c-149">Chargez chaque script avant la fin de la section `</body>` in `index.html`:</span><span class="sxs-lookup"><span data-stu-id="3898c-149">Load each script before the end of the `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-the-back-end-server"></a><span data-ttu-id="3898c-150">Configurer le serveur principal</span><span class="sxs-lookup"><span data-stu-id="3898c-150">Configure the back end server</span></span>
<span data-ttu-id="3898c-151">Pour que l’API de liste des tâches de serveur principal de l’application à page unique accepte les jetons à partir du navigateur, le serveur principal a besoin d’informations de configuration sur l’inscription de l’application.</span><span class="sxs-lookup"><span data-stu-id="3898c-151">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span></span> <span data-ttu-id="3898c-152">Dans le projet TodoSPA, ouvrez `web.config`.</span><span class="sxs-lookup"><span data-stu-id="3898c-152">In the TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="3898c-153">Remplacez les valeurs des éléments de la section `<appSettings>` afin qu’elles reflètent les valeurs que vous avez utilisées dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3898c-153">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="3898c-154">Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="3898c-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="3898c-155">`ida:Tenant` est le domaine de votre client Azure AD, par exemple, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="3898c-155">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="3898c-156">`ida:Audience` est l’ID client de votre application, copié à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="3898c-156">`ida:Audience` is the client ID of your application that you copied from the portal.</span></span>

## <a name="step-3-use-adal-to-help-secure-pages-in-the-single-page-app"></a><span data-ttu-id="3898c-157">Étape 3 : Utiliser la bibliothèque ADAL pour sécuriser les pages dans l’application à page unique</span><span class="sxs-lookup"><span data-stu-id="3898c-157">Step 3: Use ADAL to help secure pages in the single-page app</span></span>
<span data-ttu-id="3898c-158">Adal.js s’intègre avec l’itinéraire AngularJS t les fournisseurs HTTP afin de permettre de sécuriser les vues individuelles dans votre application à page unique.</span><span class="sxs-lookup"><span data-stu-id="3898c-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="3898c-159">Dans `App/Scripts/app.js`, ouvrez le module adal.js :</span><span class="sxs-lookup"><span data-stu-id="3898c-159">In `App/Scripts/app.js`, bring in the adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="3898c-160">Initialisez `adalProvider` à l’aide des valeurs de configuration de l’inscription de votre application, également dans `App/Scripts/app.js` :</span><span class="sxs-lookup"><span data-stu-id="3898c-160">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="3898c-161">Sécurisez la vue `TodoList` dans l’application à l’aide d’une seule ligne de code : `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="3898c-161">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="3898c-162">Résumé</span><span class="sxs-lookup"><span data-stu-id="3898c-162">Summary</span></span>
<span data-ttu-id="3898c-163">Vous disposez maintenant d’une application à page unique sécurisée qui peut connecter les utilisateurs et émettre un jeton porteur vers son API de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="3898c-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span></span> <span data-ttu-id="3898c-164">Lorsqu’un utilisateur clique sur le lien **TodoList**, adal.js redirige automatiquement vers Azure AD pour la connexion, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3898c-164">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span> <span data-ttu-id="3898c-165">En outre, adal.js joint automatiquement un jeton d’accès à toutes les demandes Ajax envoyées au serveur principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="3898c-165">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span></span>  

<span data-ttu-id="3898c-166">Les étapes ci-dessus sont le minimum requis pour générer une application à page unique à l’aide d’adal.js.</span><span class="sxs-lookup"><span data-stu-id="3898c-166">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span></span> <span data-ttu-id="3898c-167">Mais certaines autres fonctionnalités sont utiles dans application à page unique :</span><span class="sxs-lookup"><span data-stu-id="3898c-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="3898c-168">Pour émettre explicitement des demandes de connexion et de déconnexion, vous pouvez définir des fonctions dans vos contrôleurs qui appellent adal.js.</span><span class="sxs-lookup"><span data-stu-id="3898c-168">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="3898c-169">Dans `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="3898c-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="3898c-170">Vous pouvez présenter des informations utilisateur dans l’interface utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="3898c-170">You might want to present user information in the app's UI.</span></span> <span data-ttu-id="3898c-171">Le service ADAL a déjà été ajouté au contrôleur `userDataCtrl`. Vous pouvez donc accéder à l’objet `userInfo` dans la vue associée, `App/Views/UserData.html` :</span><span class="sxs-lookup"><span data-stu-id="3898c-171">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="3898c-172">Il existe de nombreux scénarios dans lesquels vous souhaitez savoir si l’utilisateur est connecté ou non.</span><span class="sxs-lookup"><span data-stu-id="3898c-172">There are many scenarios in which you'll want to know if the user is signed in or not.</span></span> <span data-ttu-id="3898c-173">Vous pouvez aussi utiliser l’objet `userInfo` pour rassembler ces informations.</span><span class="sxs-lookup"><span data-stu-id="3898c-173">You can also use the `userInfo` object to gather this information.</span></span>  <span data-ttu-id="3898c-174">Par exemple, dans `index.html`, vous pouvez afficher le bouton **Connexion** ou **Déconnexion** en fonction de l’état d’authentification :</span><span class="sxs-lookup"><span data-stu-id="3898c-174">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="3898c-175">Votre application à page unique intégrée à Azure AD peut authentifier les utilisateurs, appeler en toute sécurité son serveur principal à l’aide d’OAuth 2.0 et obtenir des informations de base sur l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3898c-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="3898c-176">Si vous ne l’avez pas encore fait, il est maintenant temps de remplir votre client avec quelques utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3898c-176">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="3898c-177">Exécutez votre application à page unique de listes des tâches et connectez-vous avec un de ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3898c-177">Run your To Do List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="3898c-178">Ajoutez des tâches à la liste des tâches des utilisateurs, déconnectez-vous et reconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="3898c-178">Add tasks to the user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="3898c-179">Adal.js facilite l’intégration des fonctionnalités d’identité communes dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3898c-179">Adal.js makes it easy to incorporate common identity features into your application.</span></span> <span data-ttu-id="3898c-180">Elle effectue les tâches ingrates pour vous : gestion du cache, prise en charge du protocole OAuth, présentation d’une interface utilisateur de connexion à l’utilisateur, actualisation des jetons expirés et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="3898c-180">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="3898c-181">Pour référence, l’exemple terminé (sans vos valeurs de configuration) est disponible dans [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="3898c-181">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3898c-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3898c-182">Next steps</span></span>
<span data-ttu-id="3898c-183">Vous pouvez à présent aborder d’autres scénarios.</span><span class="sxs-lookup"><span data-stu-id="3898c-183">You can now move on to additional scenarios.</span></span> <span data-ttu-id="3898c-184">Vous souhaiterez peut-être essayer : [Appeler une API web CORS à partir d’une application à page unique](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="3898c-184">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
