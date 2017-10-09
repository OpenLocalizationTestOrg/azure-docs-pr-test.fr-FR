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
# <a name="add-sign-in-tooa-nodejs-web-app"></a>Ajouter une connexion tooa Node.js web app

> [!NOTE]
> Pas toutes les fonctionnalités et les scénarios de Azure Active Directory fonctionnent avec le point de terminaison hello v2.0. toodetermine si vous devez utiliser le point de terminaison hello v2.0 ou point de terminaison hello v1.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
> 

Dans ce didacticiel, nous utilisons hello toodo de Passport tâches suivantes :

* Dans une application web, connectez-vous à utilisateur de hello à l’aide d’Azure Active Directory (Azure AD) et hello v2.0 le point de terminaison.
* Afficher des informations sur l’utilisateur de hello.
* Signe hello utilisateur hors de l’application de hello.

**Passport** est un intergiciel d’authentification pour Node.js. Flexible et modulaire, Passport peut être intégré de façon transparente dans n’importe quelle application web Restify ou basée sur Express. Dans Passport, une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter ou d’autres options. Nous avons développé une stratégie pour Azure AD. Dans cet article, nous vous indiquons comment tooinstall hello module, puis ajoutez hello Azure AD `passport-azure-ad` plug-in.

## <a name="download"></a>Télécharger
code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs). didacticiel de hello toofollow, vous pouvez [télécharger la structure de l’application hello sous forme de fichier .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) ou un clone hello squelette :

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Vous pouvez également obtenir l’application hello terminée à fin hello de ce didacticiel.

## <a name="1-register-an-app"></a>1 : Inscrire une application
Créer une application à [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez [ces étapes détaillées](active-directory-v2-app-registration.md) tooregister une application. Assurez-vous d’effectuer les tâches suivantes :

* Hello de copie **Id d’Application** affecté tooyour application. Vous en aurez besoin pour ce didacticiel.
* Ajouter hello **Web** plate-forme pour votre application.
* Hello de copie **URI de redirection** à partir du portail de hello. Vous devez utiliser hello URI par défaut de `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-add-prerequisities-tooyour-directory"></a>2 : ajouter un répertoire de tooyour préalables
À l’invite de commandes, modifiez dossier racine de répertoires toogo tooyour, si vous n’êtes pas déjà. Exécutez hello suivant de commandes :

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

En outre, nous utilisons `passport-azure-ad` squelette hello de démarrage rapide de hello :

* `npm install passport-azure-ad`

Cette opération installe les bibliothèques hello qui `passport-azure-ad` utilise.

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3 : configurer votre stratégie de passport-nœud-js application toouse hello
Configurer l’intergiciel (middleware) d’Express Bonjour Bonjour toouse protocole d’authentification OpenID Connect. Vous utilisez les demandes de connexion et de déconnexion Passport tooissue, gérez la session de l’utilisateur hello et obtenez des informations sur l’utilisateur hello, entre autres choses.

1.  Dans la racine de hello du projet de hello, ouvrez le fichier de Config.js de hello. Bonjour `exports.creds` section, entrez des valeurs de configuration de votre application.
  
  * `clientID`: hello **Id d’Application** qui est attribué tooyour application hello portail Azure.
  * `returnURL`: hello **URI de redirection** que vous avez entré dans le portail de hello.
  * `clientSecret`: secret hello que vous avez généré dans le portail de hello.

2.  Dans la racine de hello du projet de hello, ouvrez le fichier de App.js de hello. tooinvoke hello OIDCStrategy stratey, qui est livré avec `passport-azure-ad`, ajouter hello après appel :

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  toohandle vos demandes de connexion, utilisez la stratégie hello vous référencé :

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

Passport utilise un modèle similaire pour toutes ses stratégies (Twitter, Facebook, etc.). Tous les enregistreurs de stratégie respectent toohello modèle. Stratégie de hello de passer un `function()` qui utilise un jeton et `done` en tant que paramètres. stratégie de Hello est retournée une fois qu’il fait tout son travail. Stocker les utilisateur hello et jeton de hello dissimulation vous n’avez pas besoin tooask pour celle-ci à nouveau.

  > [!IMPORTANT]
  > Hello code précédent prend tout utilisateur qui peut authentifier tooyour server. C’est ce qu’on appelle l’enregistrement automatique. Sur un serveur de production, vous ne voudriez toolet tout le monde sans avoir d’abord les passent par un processus d’inscription que vous choisissez. Il s’agit généralement de modèle hello que vous voyez dans les applications consommateur. application Hello peut vous permettre de tooregister avec Facebook, mais il vous demande alors tooenter des informations supplémentaires. Si vous n’utilisiez un programme de ligne de commande pour ce didacticiel, vous pouvez extraire par courrier électronique hello à partir de l’objet du jeton hello qui est retourné. Ensuite, vous vous demandez peut-être hello utilisateur tooenter plus d’informations. Car il s’agit d’un serveur de test, vous ajoutez l’utilisateur de hello directement toohello base de données.
  > 
  > 

4.  Ajouter des méthodes hello que vous utilisez suivi tookeep d’utilisateurs qui se sont connectés, comme requis par Passport. Cela inclut la sérialisation et la désérialisation des informations de l’utilisateur hello :

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

5.  Ajoutez du code hello charge hello Express moteur. Vous utilisez hello par défaut /views et modèle de /routes Express fournit :

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

6.  Ajouter hello POST achemine que rassemblerez toohello de demandes de connexion réel hello `passport-azure-ad` moteur :

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

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4 : utiliser Passport tooissue connexion et déconnexion demande tooAzure AD
Votre application est maintenant configurée toocommunicate avec point de terminaison hello v2.0 à l’aide du protocole d’authentification OpenID Connect hello. Hello `passport-azure-ad` stratégie prend en charge tous les détails de hello d’élaborer des messages d’authentification, la validation des jetons d’Azure AD et la gestion de session d’utilisateur hello. Tout ce qui reste toodo est toogive vos utilisateurs un toosign moyen dans et les signer hors et toogather plus d’informations sur l’utilisateur hello qui s’est connecté.

1.  Ajouter hello **par défaut**, **connexion**, **compte**, et **déconnexion** méthodes tooyour App.js fichier :

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

  Voici les détails de hello :
    
    * Hello `/` toohello index.ejs vue redirige l’itinéraire. Il transmet les utilisateur hello dans la demande hello (s’il existe).
    * Hello `/account` Router tout d’abord *permet de s’assurer que vous êtes authentifié* (vous implémentez qui Bonjour suivant code). Ensuite, il passe utilisateur de hello dans la demande hello. Il s’agit afin d’obtenir plus d’informations sur l’utilisateur de hello.
    * Hello `/login` router des appels de votre `azuread-openidconnect` authentificateur de `passport-azuread`. Si qui ne réussit pas, il redirige l’utilisateur hello trop`/login`.
    * Hello `/logout` itinéraire appelle logout.ejs vue hello (et itinéraire). Cela efface les cookies, puis retourne hello tooindex.ejs arrière d’utilisateur.

2.  Ajouter hello **EnsureAuthenticated** méthode que vous avez utilisé précédemment dans `/account`:

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

3.  Dans App.js, créez le serveur de hello :

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a>5 : créer des itinéraires et des vues de hello dans Express que vous affichez votre utilisateur sur le site Web de hello
Ajouter les itinéraires hello et des vues qui affichent des informations de l’utilisateur toohello. les itinéraires Hello et vues également gérer hello `/logout` et `/login` les itinéraires que vous avez créé.

1. Dans le répertoire racine de hello, créez hello `/routes/index.js` itinéraire.

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  Dans le répertoire racine de hello, créez hello `/routes/user.js` itinéraire.

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  `/routes/index.js`et `/routes/user.js` simple d’itinéraires transmettre les vues de demandes de hello tooyour, y compris les utilisateur hello, le cas échéant.

3.  Dans le répertoire racine de hello, créez hello `/views/index.ejs` vue. Cette page appelle vos méthodes **de connexion** et **de déconnexion**. Vous utilisez également hello `/views/index.ejs` afficher les informations de compte toocapture. Vous pouvez utiliser hello conditionnel `if (!user)` en tant qu’utilisateur hello transmise par l’intermédiaire de la demande de hello. Cela signifie que vous disposez d’un utilisateur connecté.

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

4.  Dans le répertoire racine de hello, créez hello `/views/account.ejs` vue. Hello `/views/account.ejs` affichage vous permet de tooview des informations supplémentaires qui `passport-azuread` place dans la demande de l’utilisateur hello.

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

5.  Ajoutez une mise en page. Dans le répertoire racine de hello, créez hello `/views/layout.ejs` vue.

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

6.  toobuild et exécuter votre application, exécutez `node app.js`. Ensuite, passez trop`http://localhost:3000`.

7.  Connectez-vous à un compte personnel Microsoft ou à un compte scolaire/professionnel. Notez que l’identité d’utilisateur hello est répercutée dans la liste d’Account hello. 

Vous disposez maintenant d’une application web qui est sécurisée à l’aide de protocoles standard. Vous pouvez authentifier les utilisateurs dans votre application à l’aide de leurs comptes personnels, professionnels ou scolaires.

## <a name="next-steps"></a>Étapes suivantes
Pour référence, exemple hello terminée (sans les valeurs de configuration) est fourni en tant que [un fichier .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip). Vous pouvez également le cloner à partir de GitHub :

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Ensuite, vous pouvez déplacer sur toomore rubriques avancées. Vous souhaiterez peut-être tootry :

[Sécuriser une API de web Node.js à l’aide de point de terminaison hello v2.0](active-directory-v2-devquickstarts-node-api.md)

Voici quelques ressources supplémentaires :

* [Guide du développeur Azure AD v2.0](active-directory-appmodel-v2-overview.md)
* [Balise « azure-active-directory » dans Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Obtenir les mises à jour de sécurité de nos produits
Nous vous invitons à vous toosign des toobe averti lorsque des incidents de sécurité se produisent. Sur hello [des Notifications de sécurité techniques Microsoft](https://technet.microsoft.com/security/dd252948) page, s’abonner tooSecurity conseils alertes.

