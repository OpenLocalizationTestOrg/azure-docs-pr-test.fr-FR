---
title: "aaaGetting démarrée avec l’authentification dans Azure AD et de déconnexion à l’aide de Node.js | Documents Microsoft"
description: "Découvrez comment toobuild un MVC Express de Node.js web application qui s’intègre avec Azure AD pour la connexion."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 81deecec-dbe2-4e75-8bc0-cf3788645f99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 26481899c74741743b947bd891b65ff24ffc43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a>Connexion et déconnexion d’Azure AD à l’aide d’une application web Node.js
Nous utilisons Passport pour :

* Signe hello utilisateur dans l’application toohello avec Azure Active Directory (Azure AD).
* Afficher des informations sur l’utilisateur de hello.
* Signe hello utilisateur hors de l’application de hello.

Passport est un intergiciel d’authentification pour Node.js. Flexible et modulaire, Passport peut être supprimé de manière transparente dans tooany rapides ou restify d’application web. Une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter et bien d’autres. Nous avons développé une stratégie pour Microsoft Azure Active Directory. Nous installer ce module et puis ajoutez hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.

toodo, hello prennent comme suit :

1. inscrire une application ;
2. Configurer votre hello de toouse application `passport-azure-ad` stratégie.
3. Utilisez Passport tooissue connectez-vous et demandes de déconnexion tooAzure AD.
4. Imprimer des données sur l’utilisateur de hello.

code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).  toofollow le long, vous pouvez [télécharger la structure de l’application hello sous forme de fichier .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) ou un clone hello squelette :

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

application Hello terminée est fournie à des fin de hello de ce didacticiel également.

## <a name="step-1-register-an-app"></a>Étape 1 : enregistrement d’une application
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Dans le menu de hello en hello haut hello, sélectionnez votre compte. Sous hello **répertoire** , choisissez client Active Directory de hello où vous souhaitez tooregister votre application.

3. Sélectionnez **plus Services** Bonjour hello menu gauche de l’écran hello et sélectionnez **Azure Active Directory**.

4. Sélectionnez **Inscriptions d’applications**, puis **Ajouter**.

5. Suivez hello invites toocreate un **Application Web** et/ou **WebAPI**.
  * Hello **nom** Hello application décrit toousers de votre application.

  * Hello **URL de connexion** est l’URL de base hello de votre application.  Hello valeur par défaut du squelette est ' http://localhost:3000/auth/openid/retour ».

6. Une fois l’application enregistrée, Azure AD lui affecte un ID d’application unique. Vous avez besoin de cette valeur suivante de hello sections, par conséquent, copiez-le à partir de la page de l’application hello.
7. À partir de hello **paramètres** -> **propriétés** page de votre application, la mise à jour de hello URI ID d’application. Hello **URI ID d’application** est un identificateur unique pour votre application. convention de Hello est le format de hello toouse `https://<tenant-domain>/<app-name>`, par exemple : `https://contoso.onmicrosoft.com/my-first-aad-app`.

## <a name="step-2-add-prerequisites-tooyour-directory"></a>Étape 2 : Ajouter le répertoire tooyour de conditions préalables
1. À partir de la ligne de commande hello, modifier le dossier racine de tooyour répertoires si vous n’êtes pas déjà, et en exécution hello commandes suivant :

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. De plus, vous avez besoin de `passport-azure-ad` :
    * `npm install passport-azure-ad`

Cette opération installe les bibliothèques hello qui `passport-azure-ad` dépend.

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>Étape 3 : Configurer votre stratégie de passport-nœud-js application toouse hello
Ici, nous configurons le protocole d’authentification OpenID Connect Express toouse hello.  Passport est utilisé toodo divers éléments, notamment les demandes de connexion et de déconnexion de problème, gérer la session de l’utilisateur hello et obtenir des informations sur l’utilisateur de hello.

1. toobegin, ouvrez hello `config.js` racine hello du projet de hello du fichier, puis entrez les valeurs de configuration de votre application Bonjour `exports.creds` section.

  * Hello `clientID` est hello **Id d’Application** qui est l’application tooyour attribué dans le portail de l’enregistrement hello.

  * Hello `returnURL` est hello **Uri de redirection** que vous avez entré dans le portail de hello.

  * Hello `clientSecret` est un secret hello que vous avez généré dans le portail de hello.

2. Ensuite, ouvrez hello `app.js` dans fichier hello la racine du projet de hello. Ajoutez ensuite hello après appel tooinvoke hello `OIDCStrategy` stratégie qui est fourni avec `passport-azure-ad`.

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. Après cela, utilisez stratégie hello nous référencé toohandle nos demandes de connexion.

    ```JavaScript
    // Use hello OIDCStrategy within Passport. (Section 2)
    //
    //   Strategies in passport require a `validate` function that accepts
    //   credentials (in this case, an OpenID identifier), and invokes a callback
    //   with a user object.
    passport.use(new OIDCStrategy({
        callbackURL: config.creds.returnURL,
        realm: config.creds.realm,
        clientID: config.creds.clientID,
        clientSecret: config.creds.clientSecret,
        oidcIssuer: config.creds.issuer,
        identityMetadata: config.creds.identityMetadata,
        skipUserProfile: config.creds.skipUserProfile,
        responseType: config.creds.responseType,
        responseMode: config.creds.responseMode
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
        if (!profile.email) {
        return done(new Error("No email found"), null);
        }
        // asynchronous verification, for effect...
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
Passport utilise un modèle semblable pour toutes ses stratégies (Twitter, Facebook, etc.), que respectent tous les enregistreurs de stratégie. Stratégie de hello, vous constatez que nous passer une fonction qui a un jeton et un terminé en tant que paramètres de hello. stratégie de Hello est fourni dans toous une fois qu’il effectue son travail. Puis nous souhaitons utilisateur de hello toostore et jeton de hello dissimulation nous n’avez pas besoin tooask pour celle-ci à nouveau.

> [!IMPORTANT]
code de précédent Hello prend tout utilisateur qui se produit tooauthenticate tooour server. C’est ce qu’on appelle l’enregistrement automatique. Nous vous recommandons de ne laisser tout le monde authentifier le serveur de production tooa sans avoir d’abord les inscrire via un processus que vous décidez de. Il s’agit généralement de modèle hello que vous voyez dans les applications consommateur, ce qui vous permettent tooregister avec Facebook, mais vous demander des informations supplémentaires tooprovide. Si cela n’était pas un exemple d’application, nous avons extrait hello son adresse électronique à partir de l’objet du jeton hello qui est retourné et demandé toofill d’utilisateur hello des informations supplémentaires. Comme il s’agit d’un serveur de test, nous les ajoutons toohello base de données.


4. Ensuite, vous allez ajouter des méthodes hello qui nous tootrack hello utilisateurs connectés comme requis par Passport. Ces méthodes incluent la sérialisation et la désérialisation des informations de l’utilisateur hello.

    ```JavaScript

            // Passport session setup. (Section 2)

            //   toosupport persistent sign-in sessions, Passport needs toobe able to
            //   serialize users into hello session and deserialize them out of hello session. Typically,
            //   this is done simply by storing hello user ID when serializing and finding
            //   hello user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array toohold signed-in users
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

5.  Ensuite, nous allons ajouter le moteur Express hello hello code tooload. Nous utilisons ici hello par défaut /views et modèle de /routes Express fournit.

    ```JavaScript

        // configure Express (section 2)

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

6. Enfin, vous allez ajouter hello achemine que rassemblerez toohello de demandes de connexion réel hello `passport-azure-ad` moteur :


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware tooauthenticate the
        //   request. hello first step in OpenID authentication involves redirecting
        //   hello user tootheir OpenID provider. After authenticating, hello OpenID
        //   provider redirects hello user back toothis application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in hello Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Étape 4 : Connexion à utiliser Passport tooissue et demandes de déconnexion tooAzure AD
Votre application est maintenant toocommunicate correctement configurée avec un point de terminaison hello à l’aide du protocole d’authentification OpenID Connect hello.  `passport-azure-ad`a prise en charge tous les détails de hello d’élaborer des messages d’authentification, la validation des jetons d’Azure AD et la gestion des sessions utilisateur. Tout ce qui reste est distribution à vos utilisateurs de se déconnecter toosign moyen dans, ainsi que la collecte des informations supplémentaires sur les utilisateurs connectés hello.

1. Tout d’abord, nous allons ajouter par défaut de hello, connectez-vous, compte et méthodes déconnexion tooour `app.js` fichier :

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
            log.info('Login was called in hello Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  Examinons-les en détail :

  * Hello `/`itinéraire redirige toohello index.ejs affichage, en passant les utilisateur hello demande de hello (s’il existe).
  * Hello `/account` Router tout d’abord *garantit que nous sommes authentifiés* (nous implémenter qui Bonjour exemple suivant), et puis passe hello utilisateur dans la demande de hello afin que nous pouvons obtenir plus d’informations sur l’utilisateur de hello.
  * Hello `/login` itinéraire appelle l’authentificateur de notre organisation-openidconnect de `passport-azuread`. Si qui ne réussit pas, il redirige hello arrière trop d’utilisateur.
  * Hello `/logout` itinéraire appelle simplement hello logout.ejs (et itinéraire), les cookies d’efface et renvoie ensuite hello tooindex.ejs arrière d’utilisateur.

3. Pour la dernière partie de hello de `app.js`, nous allons ajouter hello **EnsureAuthenticated** méthode qui est utilisée dans `/account`, comme indiqué précédemment.

    ```JavaScript

        // Simple route middleware tooensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs toobe protected. If
        //   hello request is authenticated (typically via a persistent sign-in session),
        //   hello request proceeds. Otherwise, hello user is redirected toothe
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. Enfin, nous allons créer de serveur hello lui-même dans `app.js`:

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a>Étape 5 : toodisplay notre utilisateur dans le site Web de hello, créer des vues hello et les itinéraires dans Express
`app.js` est désormais terminé. Nous avons besoin des itinéraires de hello tooadd simplement et que vous affiche des informations hello nous obtenir toohello utilisateur, ainsi que gérer hello `/logout` et `/login` les itinéraires que nous avons créés.

1. Créer hello `/routes/index.js` itinéraire sous le répertoire racine de hello.

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. Créer hello `/routes/user.js` itinéraire sous le répertoire racine de hello.

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 Ces transmettre les vues de demandes de hello tooour, y compris les utilisateur hello s’il est présent.

3. Créer hello `/views/index.ejs` sous le répertoire racine de hello. Il s’agit d’une page simple qui appelle nos méthodes de connexion et de déconnexion et nous permet de toograb les informations de compte. Notez que nous pouvons utiliser hello conditionnel `if (!user)` comme utilisateur hello transmise par l’intermédiaire de la demande de hello est la preuve que nous avons un utilisateur connecté.

    ```JavaScript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
        <h2>Hello, <%= user.displayName %>.</h2>
        <a href="/account">Account Info</a></br>
        <a href="/logout">Log Out</a>
    <% } %>
    ```

4. Créer hello `/views/account.ejs` afficher sous le répertoire racine de hello afin que nous pouvons afficher des informations supplémentaires qui `passport-azuread` a placé dans la demande de l’utilisateur hello.

    ```Javascript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
    <p>displayName: <%= user.displayName %></p>
    <p>givenName: <%= user.name.givenName %></p>
    <p>familyName: <%= user.name.familyName %></p>
    <p>UPN: <%= user._json.upn %></p>
    <p>Profile ID: <%= user.id %></p>
  ##Next steps  <p>Full Claimes</p>
    <%- JSON.stringify(user) %>
    <p></p>
    <a href="/logout">Log Out</a>
    <% } %>
    ```

5. Améliorons-en l’apparence à l’aide d’une mise en page. Créer hello ' / répertoire racine de vue des views/layout.ejs sous hello.

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
                <a href="/login">Log In</a>
                </p>
            <% } else { %>
                <p>
                <a href="/">Home</a> |
                <a href="/account">Account</a> |
                <a href="/logout">Log Out</a>
                </p>
            <% } %>
            <%- body %>
        </body>
    </html>
    ```

##<a name="next-steps"></a>Étapes suivantes
Enfin, générez et exécutez votre application. Exécutez `node app.js`, puis passez trop`http://localhost:3000`.

Connectez-vous avec un compte Microsoft personnel ou d’un compte professionnel ou scolaire et notez comment hello l’identité d’utilisateur est répercutée dans la liste d’Account hello. Vous disposez désormais d’une application web sécurisée à l’aide de protocoles standard et pouvant authentifier les utilisateurs avec leurs comptes personnels et professionnels/scolaires.

Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie comme un fichier .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Vous pouvez également le cloner à partir de GitHub :

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

Vous pouvez maintenant aborder des rubriques plus sophistiquées. Vous souhaiterez peut-être tootry :

[Sécurisation d’une API web avec Azure AD](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
