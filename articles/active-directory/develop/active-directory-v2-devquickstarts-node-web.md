---
title: "Connexion à une application web Node.js à l’aide d’Azure Active Directory v2.0 | Microsoft Docs"
description: "Découvrez comment générer une application web Node.js qui connecte les utilisateurs à l’aide de leur compte Microsoft personnel et de leurs comptes professionnel ou scolaire."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 6d49c742f72440e22830915c90de009d9188db2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="4da2b-103">Ajouter une connexion à une application web Node.js</span><span class="sxs-lookup"><span data-stu-id="4da2b-103">Add sign-in to a Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="4da2b-104">Certains scénarios et fonctionnalités d’Azure Active Directory ne fonctionnent pas avec le point de terminaison 2.0.</span><span class="sxs-lookup"><span data-stu-id="4da2b-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="4da2b-105">Pour déterminer si vous devez utiliser le point de terminaison 2.0 ou 1.0, consultez les [limites de 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="4da2b-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="4da2b-106">Dans ce didacticiel, nous utilisons Passport pour effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="4da2b-106">In this tutorial, we use Passport to do the following tasks:</span></span>

* <span data-ttu-id="4da2b-107">Dans une application web, connectez l’utilisateur à l’aide d’Azure Active Directory (Azure AD) et du point de terminaison v2.0.</span><span class="sxs-lookup"><span data-stu-id="4da2b-107">In a web app, sign in the user by using Azure Active Directory (Azure AD) and the v2.0 endpoint.</span></span>
* <span data-ttu-id="4da2b-108">afficher les informations sur l’utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="4da2b-108">Display information about the user.</span></span>
* <span data-ttu-id="4da2b-109">déconnecter l’utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="4da2b-109">Sign the user out of the app.</span></span>

<span data-ttu-id="4da2b-110">**Passport** est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="4da2b-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="4da2b-111">Flexible et modulaire, Passport peut être intégré de façon transparente dans n’importe quelle application web Restify ou basée sur Express.</span><span class="sxs-lookup"><span data-stu-id="4da2b-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="4da2b-112">Dans Passport, une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter ou d’autres options.</span><span class="sxs-lookup"><span data-stu-id="4da2b-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="4da2b-113">Nous avons développé une stratégie pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4da2b-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="4da2b-114">Dans cet article, nous vous montrons comment installer le module, puis comment ajouter le plug-in `passport-azure-ad` d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4da2b-114">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="4da2b-115">Télécharger</span><span class="sxs-lookup"><span data-stu-id="4da2b-115">Download</span></span>
<span data-ttu-id="4da2b-116">Le code associé à ce didacticiel est stocké [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="4da2b-116">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="4da2b-117">Pour suivre le didacticiel, vous pouvez [télécharger la structure de l’application au format .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) ou bien la cloner :</span><span class="sxs-lookup"><span data-stu-id="4da2b-117">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="4da2b-118">Vous pouvez également obtenir l’application terminée à la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4da2b-118">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="4da2b-119">1 : Inscrire une application</span><span class="sxs-lookup"><span data-stu-id="4da2b-119">1: Register an app</span></span>
<span data-ttu-id="4da2b-120">Créez une application sur [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md) pour inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="4da2b-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="4da2b-121">Assurez-vous d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="4da2b-121">Make sure you:</span></span>

* <span data-ttu-id="4da2b-122">Copier **l’ID d’application** affecté à votre application.</span><span class="sxs-lookup"><span data-stu-id="4da2b-122">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="4da2b-123">Vous en aurez besoin pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4da2b-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="4da2b-124">Ajoutez la plate-forme **Web** pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4da2b-124">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="4da2b-125">Copiez **l’URI de redirection** provenant du portail.</span><span class="sxs-lookup"><span data-stu-id="4da2b-125">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="4da2b-126">Vous devez utiliser la valeur d’URI par défaut `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="4da2b-126">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-to-your-directory"></a><span data-ttu-id="4da2b-127">2 : Ajouter les éléments requis à votre répertoire</span><span class="sxs-lookup"><span data-stu-id="4da2b-127">2: Add prerequisities to your directory</span></span>
<span data-ttu-id="4da2b-128">À l’invite de commande, accédez aux répertoires de votre dossier racine si ce n’est pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="4da2b-128">At a command prompt, change directories to go to your root folder, if you are not already there.</span></span> <span data-ttu-id="4da2b-129">Exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4da2b-129">Run the following commands:</span></span>

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

<span data-ttu-id="4da2b-130">En outre, nous utilisons `passport-azure-ad` dans la structure du démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="4da2b-130">In addition, we use `passport-azure-ad` in the skeleton of the quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="4da2b-131">Cela installe les bibliothèques qu’utilise `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="4da2b-131">This installs the libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="4da2b-132">3. Configurer l’application pour utiliser la stratégie passport-node-js</span><span class="sxs-lookup"><span data-stu-id="4da2b-132">3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="4da2b-133">Configurez l’intergiciel Express pour utiliser le protocole d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="4da2b-133">Set up the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="4da2b-134">Passport sera utilisé notamment pour émettre des demandes de connexion et de déconnexion, gérer la session utilisateur et obtenir des informations concernant l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4da2b-134">You use Passport to issue sign-in and sign-out requests, manage the user's session, and get information about the user, among other things.</span></span>

1.  <span data-ttu-id="4da2b-135">Ouvrez le fichier Config.js à la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="4da2b-135">In the root of the project, open the Config.js file.</span></span> <span data-ttu-id="4da2b-136">Dans la section `exports.creds`, entrez les valeurs de configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="4da2b-136">In the `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="4da2b-137">`clientID` : **l’ID d’application** que le portail Azure a affecté à votre application.</span><span class="sxs-lookup"><span data-stu-id="4da2b-137">`clientID`: The **Application Id** that's assigned to your app in the Azure portal.</span></span>
  * <span data-ttu-id="4da2b-138">`returnURL` : **l’URI de redirection** que vous avez saisie dans le portail.</span><span class="sxs-lookup"><span data-stu-id="4da2b-138">`returnURL`: The **Redirect URI** that you entered in the portal.</span></span>
  * <span data-ttu-id="4da2b-139">`clientSecret` : la clé secrète que vous avez générée dans le portail.</span><span class="sxs-lookup"><span data-stu-id="4da2b-139">`clientSecret`: The secret that you generated in the portal.</span></span>

2.  <span data-ttu-id="4da2b-140">Ouvrez le fichier App.js à la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="4da2b-140">In the root of the project, open the App.js file.</span></span> <span data-ttu-id="4da2b-141">Pour appeler le stratey OIDCStrategy, qui est fournie avec `passport-azure-ad`, ajoutez l’appel suivant :</span><span class="sxs-lookup"><span data-stu-id="4da2b-141">To invoke the OIDCStrategy stratey, which comes with `passport-azure-ad`, add the following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="4da2b-142">Utilisez la stratégie référencée pour gérer les demandes de connexion :</span><span class="sxs-lookup"><span data-stu-id="4da2b-142">To handle your sign-in requests, use the strategy you just referenced:</span></span>

  ```JavaScript
  // Use the OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. The function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
      process.nextTick(function () {
        findByEmail(profile.email, function(err, user) {
          if (err) {
            return done(err);
          }
          if (!user) {
            // "Auto-registration"
            users.push(profile);
            return done(null, profile);
          }
          return done(null, user);
        });
      });
    }
  ));
  ```

<span data-ttu-id="4da2b-143">Passport utilise un modèle similaire pour toutes ses stratégies (Twitter, Facebook, etc.).</span><span class="sxs-lookup"><span data-stu-id="4da2b-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="4da2b-144">Tous les enregistreurs de stratégie adhèrent au modèle.</span><span class="sxs-lookup"><span data-stu-id="4da2b-144">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="4da2b-145">Transmettez à la stratégie une `function()` qui utilise un jeton et `done` comme paramètres.</span><span class="sxs-lookup"><span data-stu-id="4da2b-145">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="4da2b-146">La stratégie est retournée une fois qu’elle a effectué tout son travail.</span><span class="sxs-lookup"><span data-stu-id="4da2b-146">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="4da2b-147">Stockez l’utilisateur et mettez le jeton de côté pour ne pas avoir à le redemander.</span><span class="sxs-lookup"><span data-stu-id="4da2b-147">Store the user and stash the token so you don’t need to ask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="4da2b-148">Le code précédent accepte n’importe quel utilisateur qui peut s’authentifier auprès de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="4da2b-148">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="4da2b-149">C’est ce qu’on appelle l’enregistrement automatique.</span><span class="sxs-lookup"><span data-stu-id="4da2b-149">This is known as auto-registration.</span></span> <span data-ttu-id="4da2b-150">Sur un serveur de production, vous n’allez laisser entrer personne sans d’abord lui imposer un processus d’inscription de votre choix.</span><span class="sxs-lookup"><span data-stu-id="4da2b-150">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="4da2b-151">Il s’agit généralement du modèle que vous voyez dans les applications consommateur.</span><span class="sxs-lookup"><span data-stu-id="4da2b-151">This is usually the pattern that you see in consumer apps.</span></span> <span data-ttu-id="4da2b-152">L’application peut permettre de vous inscrire sur Facebook, mais elle vous demande ensuite d’entrer des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4da2b-152">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="4da2b-153">Si vous n’utilisiez pas un programme de ligne de commande pour ce didacticiel, vous pouvez extraire l’e-mail de l’objet jeton qui est retourné.</span><span class="sxs-lookup"><span data-stu-id="4da2b-153">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="4da2b-154">Ensuite, vous pouvez demander à l’utilisateur d’entrer des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4da2b-154">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="4da2b-155">Comme il s’agit d’un serveur de test, vous ajoutez l’utilisateur directement à la base de données en mémoire.</span><span class="sxs-lookup"><span data-stu-id="4da2b-155">Because this is a test server, you add the user directly to the in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="4da2b-156">Ajoutez les méthodes que vous utilisez pour effectuer le suivi des utilisateurs qui se sont connectés, comme requis par Passport.</span><span class="sxs-lookup"><span data-stu-id="4da2b-156">Add the methods that you use to keep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="4da2b-157">Cela inclut la sérialisation et la désérialisation des informations d’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="4da2b-157">This includes serializing and deserializing the user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   To support persistent login sessions, Passport needs to be able to
  //   serialize users into, and deserialize users out of, the session. Typically,
  //   this is as simple as storing the user ID when serializing, and finding
  //   the user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array to hold signed-in users
  var users = [];

  var findByEmail = function(email, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
      var user = users[i];
      log.info('we are using user: ', user);
      if (user.email === email) {
        return fn(null, user);
      }
    }
    return fn(null, null);
  };
  ```

5.  <span data-ttu-id="4da2b-158">Ajoutez le code pour charger le moteur Express.</span><span class="sxs-lookup"><span data-stu-id="4da2b-158">Add the code that loads the Express engine.</span></span> <span data-ttu-id="4da2b-159">Vous utiliserez le modèle /views et /routes par défaut fourni par Express :</span><span class="sxs-lookup"><span data-stu-id="4da2b-159">You use the default /views and /routes pattern that Express provides:</span></span>

  ```JavaScript

  // Set up Express (section 2)

  var app = express();

  app.configure(function() {
    app.set('views', __dirname + '/views');
    app.set('view engine', 'ejs');
    app.use(express.logger());
    app.use(express.methodOverride());
    app.use(cookieParser());
    app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
    app.use(bodyParser.urlencoded({ extended : true }));
    // Initialize Passport!  Also use passport.session() middleware, to support
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="4da2b-160">Ajoutez maintenant les itinéraires POST qui transmettent les demandes de connexion au moteur `passport-azure-ad` :</span><span class="sxs-lookup"><span data-stu-id="4da2b-160">Add the POST routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. The first step in OpenID authentication involves redirecting
  //   the user to the user's OpenID provider. After authenticating, the OpenID
  //   provider redirects the user back to this application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in the sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called.
  //   In this example, it redirects the user to the home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called. 
  //   In this example, it redirects the user to the home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="4da2b-161">4. Utiliser Passport pour émettre des demandes de connexion et de déconnexion dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="4da2b-161">4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="4da2b-162">Votre application est maintenant configurée pour communiquer avec le point de terminaison v2.0 en utilisant le protocole d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="4da2b-162">Your app is now set up to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="4da2b-163">La stratégie `passport-azure-ad` a pris en charge tous les détails de la création de messages d’authentification, de la validation des jetons d’Azure AD et de la gestion des sessions utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4da2b-163">The `passport-azure-ad` strategy takes care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining the user session.</span></span> <span data-ttu-id="4da2b-164">Il ne reste plus qu’à fournir aux utilisateurs un moyen de se connecter, de se déconnecter et de collecter des informations supplémentaires une fois connectés.</span><span class="sxs-lookup"><span data-stu-id="4da2b-164">All that is left to do is to give your users a way to sign in and sign out, and to gather more information about the user who is signed in.</span></span>

1.  <span data-ttu-id="4da2b-165">Ajoutez les méthodes **par défaut**, **de connexion**, **de compte** et **de déconnexion** à votre fichier App.js :</span><span class="sxs-lookup"><span data-stu-id="4da2b-165">Add the **default**, **login**, **account**, and **logout** methods to your App.js file:</span></span>

  ```JavaScript

  //Routes (section 4)

  app.get('/', function(req, res){
    res.render('index', { user: req.user });
  });

  app.get('/account', ensureAuthenticated, function(req, res){
    res.render('account', { user: req.user });
  });

  app.get('/login',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Login was called in the sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="4da2b-166">Voici les détails :</span><span class="sxs-lookup"><span data-stu-id="4da2b-166">Here are the details:</span></span>
    
    * <span data-ttu-id="4da2b-167">L’itinéraire `/` vous redirige vers la vue index.ejs.</span><span class="sxs-lookup"><span data-stu-id="4da2b-167">The `/` route redirects to the index.ejs view.</span></span> <span data-ttu-id="4da2b-168">Il transfère l’utilisateur dans la demande (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="4da2b-168">It passes the user in the request (if it exists).</span></span>
    * <span data-ttu-id="4da2b-169">L’itinéraire `/account` s’assure d’abord *que vous vous êtes authentifié* (à implémenter dans le code suivant).</span><span class="sxs-lookup"><span data-stu-id="4da2b-169">The `/account` route first *ensures that you are authenticated* (you implement that in the following code).</span></span> <span data-ttu-id="4da2b-170">Il transfère ensuite l’utilisateur dans la demande.</span><span class="sxs-lookup"><span data-stu-id="4da2b-170">Then, it passes the user in the request.</span></span> <span data-ttu-id="4da2b-171">Vous pourrez ainsi obtenir des informations supplémentaires sur l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4da2b-171">This is so you can get more information about the user.</span></span>
    * <span data-ttu-id="4da2b-172">L’itinéraire `/login` appelle votre application d’authentification `azuread-openidconnect` depuis `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="4da2b-172">The `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="4da2b-173">En cas d’échec, il redirige l’utilisateur vers `/login`.</span><span class="sxs-lookup"><span data-stu-id="4da2b-173">If that doesn't succeed, it redirects the user back to `/login`.</span></span>
    * <span data-ttu-id="4da2b-174">L’itinéraire `/logout` appelle la vue (et l’itinéraire) logout.ejs.</span><span class="sxs-lookup"><span data-stu-id="4da2b-174">The `/logout` route calls the logout.ejs view (and route).</span></span> <span data-ttu-id="4da2b-175">Cela efface les cookies, puis renvoie l’utilisateur vers index.ejs.</span><span class="sxs-lookup"><span data-stu-id="4da2b-175">This clears cookies, and then returns the user back to index.ejs.</span></span>

2.  <span data-ttu-id="4da2b-176">Ajoutez la méthode **EnsureAuthenticated** que vous avez utilisée précédemment dans `/account` :</span><span class="sxs-lookup"><span data-stu-id="4da2b-176">Add the **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware to ensure the user is authenticated (section 4)

  //   Use this route middleware on any resource that needs to be protected. If
  //   the request is authenticated (typically via a persistent login session),
  //   the request proceeds. Otherwise, the user is redirected to the
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="4da2b-177">Dans App.js, créez le serveur :</span><span class="sxs-lookup"><span data-stu-id="4da2b-177">In App.js, create the server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-the-views-and-routes-in-express-that-you-show-your-user-on-the-website"></a><span data-ttu-id="4da2b-178">5. Créer des vues et des itinéraires dans Express pour afficher l’utilisateur dans le site web</span><span class="sxs-lookup"><span data-stu-id="4da2b-178">5: Create the views and routes in Express that you show your user on the website</span></span>
<span data-ttu-id="4da2b-179">Ajoutez les itinéraires et les vues qui fournissent des informations à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4da2b-179">Add the routes and views that show information to the user.</span></span> <span data-ttu-id="4da2b-180">Les itinéraires et les vues gèrent également les itinéraires `/logout` et `/login` que vous avez créés.</span><span class="sxs-lookup"><span data-stu-id="4da2b-180">The routes and views also handle the `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="4da2b-181">Créez l’itinéraire `/routes/index.js` dans le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="4da2b-181">In the root directory, create the `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="4da2b-182">Créez l’itinéraire `/routes/user.js` dans le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="4da2b-182">In the root directory, create the `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="4da2b-183">`/routes/index.js` et `/routes/user.js` sont des itinéraires simples qui transmettent la demande à vos vues, en incluant l’utilisateur le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="4da2b-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along the request to your views, including the user, if present.</span></span>

3.  <span data-ttu-id="4da2b-184">Créez la vue `/views/index.ejs` dans le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="4da2b-184">In the root directory, create the `/views/index.ejs` view.</span></span> <span data-ttu-id="4da2b-185">Cette page appelle vos méthodes **de connexion** et **de déconnexion**.</span><span class="sxs-lookup"><span data-stu-id="4da2b-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="4da2b-186">Vous utiliserez également la vue `/views/index.ejs` pour capturer les informations de compte.</span><span class="sxs-lookup"><span data-stu-id="4da2b-186">You also use the `/views/index.ejs` view to capture account information.</span></span> <span data-ttu-id="4da2b-187">Vous pouvez utiliser la condition `if (!user)` lorsque l’utilisateur est transféré dans la demande.</span><span class="sxs-lookup"><span data-stu-id="4da2b-187">You can use the conditional `if (!user)` as the user being passed through in the request.</span></span> <span data-ttu-id="4da2b-188">Cela signifie que vous disposez d’un utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="4da2b-188">It is evidence that you have a user signed in.</span></span>

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  <span data-ttu-id="4da2b-189">Créez la vue `/views/account.ejs` dans le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="4da2b-189">In the root directory, create the `/views/account.ejs` view.</span></span> <span data-ttu-id="4da2b-190">La vue `/views/account.ejs` vous permet d’afficher des informations supplémentaires que `passport-azuread` ajoute à la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4da2b-190">The `/views/account.ejs` view allows you to view additional information that `passport-azuread` puts in the user request.</span></span>

  ```Javascript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
  <p>displayName: <%= user.displayName %></p>
  <p>givenName: <%= user.name.givenName %></p>
  <p>familyName: <%= user.name.familyName %></p>
  <p>UPN: <%= user._json.upn %></p>
  <p>Profile ID: <%= user.id %></p>
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  <span data-ttu-id="4da2b-191">Ajoutez une mise en page.</span><span class="sxs-lookup"><span data-stu-id="4da2b-191">Add a layout.</span></span> <span data-ttu-id="4da2b-192">Créez la vue `/views/layout.ejs` dans le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="4da2b-192">In the root directory, create the `/views/layout.ejs` view.</span></span>

  ```HTML

  <!DOCTYPE html>
  <html>
      <head>
          <title>Passport-OpenID Example</title>
      </head>
      <body>
          <% if (!user) { %>
              <p>
              <a href="/">Home</a> |
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  <span data-ttu-id="4da2b-193">Exécutez `node app.js` pour générer et exécuter votre application.</span><span class="sxs-lookup"><span data-stu-id="4da2b-193">To build and run your app, run `node app.js`.</span></span> <span data-ttu-id="4da2b-194">Ensuite, accédez à `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="4da2b-194">Then, go to `http://localhost:3000`.</span></span>

7.  <span data-ttu-id="4da2b-195">Connectez-vous à un compte personnel Microsoft ou à un compte scolaire/professionnel.</span><span class="sxs-lookup"><span data-stu-id="4da2b-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="4da2b-196">Notez que l’identité de l’utilisateur s’affiche dans la liste /account.</span><span class="sxs-lookup"><span data-stu-id="4da2b-196">Note that the user's identity is reflected in the /account list.</span></span> 

<span data-ttu-id="4da2b-197">Vous disposez maintenant d’une application web qui est sécurisée à l’aide de protocoles standard.</span><span class="sxs-lookup"><span data-stu-id="4da2b-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="4da2b-198">Vous pouvez authentifier les utilisateurs dans votre application à l’aide de leurs comptes personnels, professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="4da2b-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4da2b-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4da2b-199">Next steps</span></span>
<span data-ttu-id="4da2b-200">Pour référence, l’exemple terminé (sans vos valeurs de configuration) est fourni en tant que [fichier .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="4da2b-200">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="4da2b-201">Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="4da2b-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="4da2b-202">Vous pouvez maintenant aborder des rubriques plus avancées.</span><span class="sxs-lookup"><span data-stu-id="4da2b-202">Next, you can move on to more advanced topics.</span></span> <span data-ttu-id="4da2b-203">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4da2b-203">You might want to try:</span></span>

[<span data-ttu-id="4da2b-204">Sécuriser une API web Node.js à l’aide du point de terminaison v2.0</span><span class="sxs-lookup"><span data-stu-id="4da2b-204">Secure a Node.js web API by using the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="4da2b-205">Voici quelques ressources supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="4da2b-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="4da2b-206">Guide du développeur Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="4da2b-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="4da2b-207">Balise « azure-active-directory » dans Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="4da2b-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="4da2b-208">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="4da2b-208">Get security updates for our products</span></span>
<span data-ttu-id="4da2b-209">Nous vous encourageons à vous inscrire pour être averti quand des incidents de sécurité se produisent.</span><span class="sxs-lookup"><span data-stu-id="4da2b-209">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="4da2b-210">Sur la page [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948), abonnez-vous aux alertes d’avis de sécurité.</span><span class="sxs-lookup"><span data-stu-id="4da2b-210">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

