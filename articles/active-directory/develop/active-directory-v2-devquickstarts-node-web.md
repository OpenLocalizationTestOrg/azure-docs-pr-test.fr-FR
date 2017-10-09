---
title: "v2.0 d’Active Directory aaaAzure Node.js web application connectez-vous | Documents Microsoft"
description: "Découvrez comment toobuild un Node.js web application qui se connecte un utilisateur à l’aide d’un compte Microsoft personnel et un compte professionnel ou scolaire."
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
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="aa90f-103">Ajouter une connexion tooa Node.js web app</span><span class="sxs-lookup"><span data-stu-id="aa90f-103">Add sign-in tooa Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="aa90f-104">Pas toutes les fonctionnalités et les scénarios de Azure Active Directory fonctionnent avec le point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="aa90f-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="aa90f-105">toodetermine si vous devez utiliser le point de terminaison hello v2.0 ou point de terminaison hello v1.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="aa90f-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="aa90f-106">Dans ce didacticiel, nous utilisons hello toodo de Passport tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="aa90f-106">In this tutorial, we use Passport toodo hello following tasks:</span></span>

* <span data-ttu-id="aa90f-107">Dans une application web, connectez-vous à utilisateur de hello à l’aide d’Azure Active Directory (Azure AD) et hello v2.0 le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="aa90f-107">In a web app, sign in hello user by using Azure Active Directory (Azure AD) and hello v2.0 endpoint.</span></span>
* <span data-ttu-id="aa90f-108">Afficher des informations sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-108">Display information about hello user.</span></span>
* <span data-ttu-id="aa90f-109">Signe hello utilisateur hors de l’application de hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="aa90f-110">**Passport** est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="aa90f-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="aa90f-111">Flexible et modulaire, Passport peut être intégré de façon transparente dans n’importe quelle application web Restify ou basée sur Express.</span><span class="sxs-lookup"><span data-stu-id="aa90f-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="aa90f-112">Dans Passport, une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter ou d’autres options.</span><span class="sxs-lookup"><span data-stu-id="aa90f-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="aa90f-113">Nous avons développé une stratégie pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa90f-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="aa90f-114">Dans cet article, nous vous indiquons comment tooinstall hello module, puis ajoutez hello Azure AD `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="aa90f-114">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="aa90f-115">Télécharger</span><span class="sxs-lookup"><span data-stu-id="aa90f-115">Download</span></span>
<span data-ttu-id="aa90f-116">code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="aa90f-116">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="aa90f-117">didacticiel de hello toofollow, vous pouvez [télécharger la structure de l’application hello sous forme de fichier .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) ou un clone hello squelette :</span><span class="sxs-lookup"><span data-stu-id="aa90f-117">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="aa90f-118">Vous pouvez également obtenir l’application hello terminée à fin hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="aa90f-118">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="aa90f-119">1 : Inscrire une application</span><span class="sxs-lookup"><span data-stu-id="aa90f-119">1: Register an app</span></span>
<span data-ttu-id="aa90f-120">Créer une application à [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez [ces étapes détaillées](active-directory-v2-app-registration.md) tooregister une application.</span><span class="sxs-lookup"><span data-stu-id="aa90f-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="aa90f-121">Assurez-vous d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="aa90f-121">Make sure you:</span></span>

* <span data-ttu-id="aa90f-122">Hello de copie **Id d’Application** affecté tooyour application.</span><span class="sxs-lookup"><span data-stu-id="aa90f-122">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="aa90f-123">Vous en aurez besoin pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="aa90f-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="aa90f-124">Ajouter hello **Web** plate-forme pour votre application.</span><span class="sxs-lookup"><span data-stu-id="aa90f-124">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="aa90f-125">Hello de copie **URI de redirection** à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-125">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="aa90f-126">Vous devez utiliser hello URI par défaut de `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="aa90f-126">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-tooyour-directory"></a><span data-ttu-id="aa90f-127">2 : ajouter un répertoire de tooyour préalables</span><span class="sxs-lookup"><span data-stu-id="aa90f-127">2: Add prerequisities tooyour directory</span></span>
<span data-ttu-id="aa90f-128">À l’invite de commandes, modifiez dossier racine de répertoires toogo tooyour, si vous n’êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="aa90f-128">At a command prompt, change directories toogo tooyour root folder, if you are not already there.</span></span> <span data-ttu-id="aa90f-129">Exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="aa90f-129">Run hello following commands:</span></span>

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

<span data-ttu-id="aa90f-130">En outre, nous utilisons `passport-azure-ad` squelette hello de démarrage rapide de hello :</span><span class="sxs-lookup"><span data-stu-id="aa90f-130">In addition, we use `passport-azure-ad` in hello skeleton of hello quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="aa90f-131">Cette opération installe les bibliothèques hello qui `passport-azure-ad` utilise.</span><span class="sxs-lookup"><span data-stu-id="aa90f-131">This installs hello libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="aa90f-132">3 : configurer votre stratégie de passport-nœud-js application toouse hello</span><span class="sxs-lookup"><span data-stu-id="aa90f-132">3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="aa90f-133">Configurer l’intergiciel (middleware) d’Express Bonjour Bonjour toouse protocole d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="aa90f-133">Set up hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="aa90f-134">Vous utilisez les demandes de connexion et de déconnexion Passport tooissue, gérez la session de l’utilisateur hello et obtenez des informations sur l’utilisateur hello, entre autres choses.</span><span class="sxs-lookup"><span data-stu-id="aa90f-134">You use Passport tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, among other things.</span></span>

1.  <span data-ttu-id="aa90f-135">Dans la racine de hello du projet de hello, ouvrez le fichier de Config.js de hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-135">In hello root of hello project, open hello Config.js file.</span></span> <span data-ttu-id="aa90f-136">Bonjour `exports.creds` section, entrez des valeurs de configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="aa90f-136">In hello `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="aa90f-137">`clientID`: hello **Id d’Application** qui est attribué tooyour application hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="aa90f-137">`clientID`: hello **Application Id** that's assigned tooyour app in hello Azure portal.</span></span>
  * <span data-ttu-id="aa90f-138">`returnURL`: hello **URI de redirection** que vous avez entré dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-138">`returnURL`: hello **Redirect URI** that you entered in hello portal.</span></span>
  * <span data-ttu-id="aa90f-139">`clientSecret`: secret hello que vous avez généré dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-139">`clientSecret`: hello secret that you generated in hello portal.</span></span>

2.  <span data-ttu-id="aa90f-140">Dans la racine de hello du projet de hello, ouvrez le fichier de App.js de hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-140">In hello root of hello project, open hello App.js file.</span></span> <span data-ttu-id="aa90f-141">tooinvoke hello OIDCStrategy stratey, qui est livré avec `passport-azure-ad`, ajouter hello après appel :</span><span class="sxs-lookup"><span data-stu-id="aa90f-141">tooinvoke hello OIDCStrategy stratey, which comes with `passport-azure-ad`, add hello following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="aa90f-142">toohandle vos demandes de connexion, utilisez la stratégie hello vous référencé :</span><span class="sxs-lookup"><span data-stu-id="aa90f-142">toohandle your sign-in requests, use hello strategy you just referenced:</span></span>

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
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

<span data-ttu-id="aa90f-143">Passport utilise un modèle similaire pour toutes ses stratégies (Twitter, Facebook, etc.).</span><span class="sxs-lookup"><span data-stu-id="aa90f-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="aa90f-144">Tous les enregistreurs de stratégie respectent toohello modèle.</span><span class="sxs-lookup"><span data-stu-id="aa90f-144">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="aa90f-145">Stratégie de hello de passer un `function()` qui utilise un jeton et `done` en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="aa90f-145">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="aa90f-146">stratégie de Hello est retournée une fois qu’il fait tout son travail.</span><span class="sxs-lookup"><span data-stu-id="aa90f-146">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="aa90f-147">Stocker les utilisateur hello et jeton de hello dissimulation vous n’avez pas besoin tooask pour celle-ci à nouveau.</span><span class="sxs-lookup"><span data-stu-id="aa90f-147">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="aa90f-148">Hello code précédent prend tout utilisateur qui peut authentifier tooyour server.</span><span class="sxs-lookup"><span data-stu-id="aa90f-148">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="aa90f-149">C’est ce qu’on appelle l’enregistrement automatique.</span><span class="sxs-lookup"><span data-stu-id="aa90f-149">This is known as auto-registration.</span></span> <span data-ttu-id="aa90f-150">Sur un serveur de production, vous ne voudriez toolet tout le monde sans avoir d’abord les passent par un processus d’inscription que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="aa90f-150">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="aa90f-151">Il s’agit généralement de modèle hello que vous voyez dans les applications consommateur.</span><span class="sxs-lookup"><span data-stu-id="aa90f-151">This is usually hello pattern that you see in consumer apps.</span></span> <span data-ttu-id="aa90f-152">application Hello peut vous permettre de tooregister avec Facebook, mais il vous demande alors tooenter des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="aa90f-152">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="aa90f-153">Si vous n’utilisiez un programme de ligne de commande pour ce didacticiel, vous pouvez extraire par courrier électronique hello à partir de l’objet du jeton hello qui est retourné.</span><span class="sxs-lookup"><span data-stu-id="aa90f-153">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="aa90f-154">Ensuite, vous vous demandez peut-être hello utilisateur tooenter plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="aa90f-154">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="aa90f-155">Car il s’agit d’un serveur de test, vous ajoutez l’utilisateur de hello directement toohello base de données.</span><span class="sxs-lookup"><span data-stu-id="aa90f-155">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="aa90f-156">Ajouter des méthodes hello que vous utilisez suivi tookeep d’utilisateurs qui se sont connectés, comme requis par Passport.</span><span class="sxs-lookup"><span data-stu-id="aa90f-156">Add hello methods that you use tookeep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="aa90f-157">Cela inclut la sérialisation et la désérialisation des informations de l’utilisateur hello :</span><span class="sxs-lookup"><span data-stu-id="aa90f-157">This includes serializing and deserializing hello user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
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

5.  <span data-ttu-id="aa90f-158">Ajoutez du code hello charge hello Express moteur.</span><span class="sxs-lookup"><span data-stu-id="aa90f-158">Add hello code that loads hello Express engine.</span></span> <span data-ttu-id="aa90f-159">Vous utilisez hello par défaut /views et modèle de /routes Express fournit :</span><span class="sxs-lookup"><span data-stu-id="aa90f-159">You use hello default /views and /routes pattern that Express provides:</span></span>

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
    // Initialize Passport!  Also use passport.session() middleware, toosupport
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="aa90f-160">Ajouter hello POST achemine que rassemblerez toohello de demandes de connexion réel hello `passport-azure-ad` moteur :</span><span class="sxs-lookup"><span data-stu-id="aa90f-160">Add hello POST routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="aa90f-161">4 : utiliser Passport tooissue connexion et déconnexion demande tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="aa90f-161">4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="aa90f-162">Votre application est maintenant configurée toocommunicate avec point de terminaison hello v2.0 à l’aide du protocole d’authentification OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-162">Your app is now set up toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="aa90f-163">Hello `passport-azure-ad` stratégie prend en charge tous les détails de hello d’élaborer des messages d’authentification, la validation des jetons d’Azure AD et la gestion de session d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-163">hello `passport-azure-ad` strategy takes care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining hello user session.</span></span> <span data-ttu-id="aa90f-164">Tout ce qui reste toodo est toogive vos utilisateurs un toosign moyen dans et les signer hors et toogather plus d’informations sur l’utilisateur hello qui s’est connecté.</span><span class="sxs-lookup"><span data-stu-id="aa90f-164">All that is left toodo is toogive your users a way toosign in and sign out, and toogather more information about hello user who is signed in.</span></span>

1.  <span data-ttu-id="aa90f-165">Ajouter hello **par défaut**, **connexion**, **compte**, et **déconnexion** méthodes tooyour App.js fichier :</span><span class="sxs-lookup"><span data-stu-id="aa90f-165">Add hello **default**, **login**, **account**, and **logout** methods tooyour App.js file:</span></span>

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
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="aa90f-166">Voici les détails de hello :</span><span class="sxs-lookup"><span data-stu-id="aa90f-166">Here are hello details:</span></span>
    
    * <span data-ttu-id="aa90f-167">Hello `/` toohello index.ejs vue redirige l’itinéraire.</span><span class="sxs-lookup"><span data-stu-id="aa90f-167">hello `/` route redirects toohello index.ejs view.</span></span> <span data-ttu-id="aa90f-168">Il transmet les utilisateur hello dans la demande hello (s’il existe).</span><span class="sxs-lookup"><span data-stu-id="aa90f-168">It passes hello user in hello request (if it exists).</span></span>
    * <span data-ttu-id="aa90f-169">Hello `/account` Router tout d’abord *permet de s’assurer que vous êtes authentifié* (vous implémentez qui Bonjour suivant code).</span><span class="sxs-lookup"><span data-stu-id="aa90f-169">hello `/account` route first *ensures that you are authenticated* (you implement that in hello following code).</span></span> <span data-ttu-id="aa90f-170">Ensuite, il passe utilisateur de hello dans la demande hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-170">Then, it passes hello user in hello request.</span></span> <span data-ttu-id="aa90f-171">Il s’agit afin d’obtenir plus d’informations sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-171">This is so you can get more information about hello user.</span></span>
    * <span data-ttu-id="aa90f-172">Hello `/login` router des appels de votre `azuread-openidconnect` authentificateur de `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="aa90f-172">hello `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="aa90f-173">Si qui ne réussit pas, il redirige l’utilisateur hello trop`/login`.</span><span class="sxs-lookup"><span data-stu-id="aa90f-173">If that doesn't succeed, it redirects hello user back too`/login`.</span></span>
    * <span data-ttu-id="aa90f-174">Hello `/logout` itinéraire appelle logout.ejs vue hello (et itinéraire).</span><span class="sxs-lookup"><span data-stu-id="aa90f-174">hello `/logout` route calls hello logout.ejs view (and route).</span></span> <span data-ttu-id="aa90f-175">Cela efface les cookies, puis retourne hello tooindex.ejs arrière d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="aa90f-175">This clears cookies, and then returns hello user back tooindex.ejs.</span></span>

2.  <span data-ttu-id="aa90f-176">Ajouter hello **EnsureAuthenticated** méthode que vous avez utilisé précédemment dans `/account`:</span><span class="sxs-lookup"><span data-stu-id="aa90f-176">Add hello **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="aa90f-177">Dans App.js, créez le serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="aa90f-177">In App.js, create hello server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a><span data-ttu-id="aa90f-178">5 : créer des itinéraires et des vues de hello dans Express que vous affichez votre utilisateur sur le site Web de hello</span><span class="sxs-lookup"><span data-stu-id="aa90f-178">5: Create hello views and routes in Express that you show your user on hello website</span></span>
<span data-ttu-id="aa90f-179">Ajouter les itinéraires hello et des vues qui affichent des informations de l’utilisateur toohello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-179">Add hello routes and views that show information toohello user.</span></span> <span data-ttu-id="aa90f-180">les itinéraires Hello et vues également gérer hello `/logout` et `/login` les itinéraires que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="aa90f-180">hello routes and views also handle hello `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="aa90f-181">Dans le répertoire racine de hello, créez hello `/routes/index.js` itinéraire.</span><span class="sxs-lookup"><span data-stu-id="aa90f-181">In hello root directory, create hello `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="aa90f-182">Dans le répertoire racine de hello, créez hello `/routes/user.js` itinéraire.</span><span class="sxs-lookup"><span data-stu-id="aa90f-182">In hello root directory, create hello `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="aa90f-183">`/routes/index.js`et `/routes/user.js` simple d’itinéraires transmettre les vues de demandes de hello tooyour, y compris les utilisateur hello, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="aa90f-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along hello request tooyour views, including hello user, if present.</span></span>

3.  <span data-ttu-id="aa90f-184">Dans le répertoire racine de hello, créez hello `/views/index.ejs` vue.</span><span class="sxs-lookup"><span data-stu-id="aa90f-184">In hello root directory, create hello `/views/index.ejs` view.</span></span> <span data-ttu-id="aa90f-185">Cette page appelle vos méthodes **de connexion** et **de déconnexion**.</span><span class="sxs-lookup"><span data-stu-id="aa90f-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="aa90f-186">Vous utilisez également hello `/views/index.ejs` afficher les informations de compte toocapture.</span><span class="sxs-lookup"><span data-stu-id="aa90f-186">You also use hello `/views/index.ejs` view toocapture account information.</span></span> <span data-ttu-id="aa90f-187">Vous pouvez utiliser hello conditionnel `if (!user)` en tant qu’utilisateur hello transmise par l’intermédiaire de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-187">You can use hello conditional `if (!user)` as hello user being passed through in hello request.</span></span> <span data-ttu-id="aa90f-188">Cela signifie que vous disposez d’un utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="aa90f-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="aa90f-189">Dans le répertoire racine de hello, créez hello `/views/account.ejs` vue.</span><span class="sxs-lookup"><span data-stu-id="aa90f-189">In hello root directory, create hello `/views/account.ejs` view.</span></span> <span data-ttu-id="aa90f-190">Hello `/views/account.ejs` affichage vous permet de tooview des informations supplémentaires qui `passport-azuread` place dans la demande de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-190">hello `/views/account.ejs` view allows you tooview additional information that `passport-azuread` puts in hello user request.</span></span>

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

5.  <span data-ttu-id="aa90f-191">Ajoutez une mise en page.</span><span class="sxs-lookup"><span data-stu-id="aa90f-191">Add a layout.</span></span> <span data-ttu-id="aa90f-192">Dans le répertoire racine de hello, créez hello `/views/layout.ejs` vue.</span><span class="sxs-lookup"><span data-stu-id="aa90f-192">In hello root directory, create hello `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="aa90f-193">toobuild et exécuter votre application, exécutez `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="aa90f-193">toobuild and run your app, run `node app.js`.</span></span> <span data-ttu-id="aa90f-194">Ensuite, passez trop`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="aa90f-194">Then, go too`http://localhost:3000`.</span></span>

7.  <span data-ttu-id="aa90f-195">Connectez-vous à un compte personnel Microsoft ou à un compte scolaire/professionnel.</span><span class="sxs-lookup"><span data-stu-id="aa90f-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="aa90f-196">Notez que l’identité d’utilisateur hello est répercutée dans la liste d’Account hello.</span><span class="sxs-lookup"><span data-stu-id="aa90f-196">Note that hello user's identity is reflected in hello /account list.</span></span> 

<span data-ttu-id="aa90f-197">Vous disposez maintenant d’une application web qui est sécurisée à l’aide de protocoles standard.</span><span class="sxs-lookup"><span data-stu-id="aa90f-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="aa90f-198">Vous pouvez authentifier les utilisateurs dans votre application à l’aide de leurs comptes personnels, professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="aa90f-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa90f-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aa90f-199">Next steps</span></span>
<span data-ttu-id="aa90f-200">Pour référence, exemple hello terminée (sans les valeurs de configuration) est fourni en tant que [un fichier .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="aa90f-200">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="aa90f-201">Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="aa90f-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="aa90f-202">Ensuite, vous pouvez déplacer sur toomore rubriques avancées.</span><span class="sxs-lookup"><span data-stu-id="aa90f-202">Next, you can move on toomore advanced topics.</span></span> <span data-ttu-id="aa90f-203">Vous souhaiterez peut-être tootry :</span><span class="sxs-lookup"><span data-stu-id="aa90f-203">You might want tootry:</span></span>

[<span data-ttu-id="aa90f-204">Sécuriser une API de web Node.js à l’aide de point de terminaison hello v2.0</span><span class="sxs-lookup"><span data-stu-id="aa90f-204">Secure a Node.js web API by using hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="aa90f-205">Voici quelques ressources supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="aa90f-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="aa90f-206">Guide du développeur Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="aa90f-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="aa90f-207">Balise « azure-active-directory » dans Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="aa90f-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="aa90f-208">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="aa90f-208">Get security updates for our products</span></span>
<span data-ttu-id="aa90f-209">Nous vous invitons à vous toosign des toobe averti lorsque des incidents de sécurité se produisent.</span><span class="sxs-lookup"><span data-stu-id="aa90f-209">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="aa90f-210">Sur hello [des Notifications de sécurité techniques Microsoft](https://technet.microsoft.com/security/dd252948) page, s’abonner tooSecurity conseils alertes.</span><span class="sxs-lookup"><span data-stu-id="aa90f-210">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

