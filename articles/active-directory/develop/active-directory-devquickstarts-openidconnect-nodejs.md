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
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="242e2-103">Connexion et déconnexion d’Azure AD à l’aide d’une application web Node.js</span><span class="sxs-lookup"><span data-stu-id="242e2-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="242e2-104">Nous utilisons Passport pour :</span><span class="sxs-lookup"><span data-stu-id="242e2-104">Here we use Passport to:</span></span>

* <span data-ttu-id="242e2-105">Signe hello utilisateur dans l’application toohello avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="242e2-105">Sign hello user in toohello app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="242e2-106">Afficher des informations sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-106">Display information about hello user.</span></span>
* <span data-ttu-id="242e2-107">Signe hello utilisateur hors de l’application de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-107">Sign hello user out of hello app.</span></span>

<span data-ttu-id="242e2-108">Passport est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="242e2-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="242e2-109">Flexible et modulaire, Passport peut être supprimé de manière transparente dans tooany rapides ou restify d’application web.</span><span class="sxs-lookup"><span data-stu-id="242e2-109">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or restify web application.</span></span> <span data-ttu-id="242e2-110">Une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter et bien d’autres.</span><span class="sxs-lookup"><span data-stu-id="242e2-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="242e2-111">Nous avons développé une stratégie pour Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="242e2-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="242e2-112">Nous installer ce module et puis ajoutez hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="242e2-112">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="242e2-113">toodo, hello prennent comme suit :</span><span class="sxs-lookup"><span data-stu-id="242e2-113">toodo this, take hello following steps:</span></span>

1. <span data-ttu-id="242e2-114">inscrire une application ;</span><span class="sxs-lookup"><span data-stu-id="242e2-114">Register an app.</span></span>
2. <span data-ttu-id="242e2-115">Configurer votre hello de toouse application `passport-azure-ad` stratégie.</span><span class="sxs-lookup"><span data-stu-id="242e2-115">Set up your app toouse hello `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="242e2-116">Utilisez Passport tooissue connectez-vous et demandes de déconnexion tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="242e2-116">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="242e2-117">Imprimer des données sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-117">Print data about hello user.</span></span>

<span data-ttu-id="242e2-118">code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="242e2-118">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="242e2-119">toofollow le long, vous pouvez [télécharger la structure de l’application hello sous forme de fichier .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) ou un clone hello squelette :</span><span class="sxs-lookup"><span data-stu-id="242e2-119">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="242e2-120">application Hello terminée est fournie à des fin de hello de ce didacticiel également.</span><span class="sxs-lookup"><span data-stu-id="242e2-120">hello completed application is provided at hello end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="242e2-121">Étape 1 : enregistrement d’une application</span><span class="sxs-lookup"><span data-stu-id="242e2-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="242e2-122">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="242e2-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="242e2-123">Dans le menu de hello en hello haut hello, sélectionnez votre compte.</span><span class="sxs-lookup"><span data-stu-id="242e2-123">In hello menu at hello top of hello page, select your account.</span></span> <span data-ttu-id="242e2-124">Sous hello **répertoire** , choisissez client Active Directory de hello où vous souhaitez tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="242e2-124">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="242e2-125">Sélectionnez **plus Services** Bonjour hello menu gauche de l’écran hello et sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="242e2-125">Select **More Services** in hello menu on hello left side of hello screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="242e2-126">Sélectionnez **Inscriptions d’applications**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="242e2-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="242e2-127">Suivez hello invites toocreate un **Application Web** et/ou **WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="242e2-127">Follow hello prompts toocreate a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="242e2-128">Hello **nom** Hello application décrit toousers de votre application.</span><span class="sxs-lookup"><span data-stu-id="242e2-128">hello **name** of hello application describes your application toousers.</span></span>

  * <span data-ttu-id="242e2-129">Hello **URL de connexion** est l’URL de base hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="242e2-129">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="242e2-130">Hello valeur par défaut du squelette est ' http://localhost:3000/auth/openid/retour ».</span><span class="sxs-lookup"><span data-stu-id="242e2-130">hello skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="242e2-131">Une fois l’application enregistrée, Azure AD lui affecte un ID d’application unique.</span><span class="sxs-lookup"><span data-stu-id="242e2-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="242e2-132">Vous avez besoin de cette valeur suivante de hello sections, par conséquent, copiez-le à partir de la page de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-132">You need this value in hello following sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="242e2-133">À partir de hello **paramètres** -> **propriétés** page de votre application, la mise à jour de hello URI ID d’application.</span><span class="sxs-lookup"><span data-stu-id="242e2-133">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="242e2-134">Hello **URI ID d’application** est un identificateur unique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="242e2-134">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="242e2-135">convention de Hello est le format de hello toouse `https://<tenant-domain>/<app-name>`, par exemple : `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="242e2-135">hello convention is toouse hello format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-tooyour-directory"></a><span data-ttu-id="242e2-136">Étape 2 : Ajouter le répertoire tooyour de conditions préalables</span><span class="sxs-lookup"><span data-stu-id="242e2-136">Step 2: Add prerequisites tooyour directory</span></span>
1. <span data-ttu-id="242e2-137">À partir de la ligne de commande hello, modifier le dossier racine de tooyour répertoires si vous n’êtes pas déjà, et en exécution hello commandes suivant :</span><span class="sxs-lookup"><span data-stu-id="242e2-137">From hello command line, change directories tooyour root folder if you're not already there, and then run hello following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="242e2-138">De plus, vous avez besoin de `passport-azure-ad` :</span><span class="sxs-lookup"><span data-stu-id="242e2-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="242e2-139">Cette opération installe les bibliothèques hello qui `passport-azure-ad` dépend.</span><span class="sxs-lookup"><span data-stu-id="242e2-139">This installs hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="242e2-140">Étape 3 : Configurer votre stratégie de passport-nœud-js application toouse hello</span><span class="sxs-lookup"><span data-stu-id="242e2-140">Step 3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="242e2-141">Ici, nous configurons le protocole d’authentification OpenID Connect Express toouse hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-141">Here, we configure Express toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="242e2-142">Passport est utilisé toodo divers éléments, notamment les demandes de connexion et de déconnexion de problème, gérer la session de l’utilisateur hello et obtenir des informations sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-142">Passport is used toodo various things, including issue sign-in and sign-out requests, manage hello user's session, and get information about hello user.</span></span>

1. <span data-ttu-id="242e2-143">toobegin, ouvrez hello `config.js` racine hello du projet de hello du fichier, puis entrez les valeurs de configuration de votre application Bonjour `exports.creds` section.</span><span class="sxs-lookup"><span data-stu-id="242e2-143">toobegin, open hello `config.js` file at hello root of hello project, and then enter your app's configuration values in hello `exports.creds` section.</span></span>

  * <span data-ttu-id="242e2-144">Hello `clientID` est hello **Id d’Application** qui est l’application tooyour attribué dans le portail de l’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-144">hello `clientID` is hello **Application Id** that's assigned tooyour app in hello registration portal.</span></span>

  * <span data-ttu-id="242e2-145">Hello `returnURL` est hello **Uri de redirection** que vous avez entré dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-145">hello `returnURL` is hello **Redirect Uri** that you entered in hello portal.</span></span>

  * <span data-ttu-id="242e2-146">Hello `clientSecret` est un secret hello que vous avez généré dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-146">hello `clientSecret` is hello secret that you generated in hello portal.</span></span>

2. <span data-ttu-id="242e2-147">Ensuite, ouvrez hello `app.js` dans fichier hello la racine du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-147">Next, open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="242e2-148">Ajoutez ensuite hello après appel tooinvoke hello `OIDCStrategy` stratégie qui est fourni avec `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="242e2-148">Then add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="242e2-149">Après cela, utilisez stratégie hello nous référencé toohandle nos demandes de connexion.</span><span class="sxs-lookup"><span data-stu-id="242e2-149">After that, use hello strategy we just referenced toohandle our sign-in requests.</span></span>

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
<span data-ttu-id="242e2-150">Passport utilise un modèle semblable pour toutes ses stratégies (Twitter, Facebook, etc.), que respectent tous les enregistreurs de stratégie.</span><span class="sxs-lookup"><span data-stu-id="242e2-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="242e2-151">Stratégie de hello, vous constatez que nous passer une fonction qui a un jeton et un terminé en tant que paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-151">Looking at hello strategy, you see that we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="242e2-152">stratégie de Hello est fourni dans toous une fois qu’il effectue son travail.</span><span class="sxs-lookup"><span data-stu-id="242e2-152">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="242e2-153">Puis nous souhaitons utilisateur de hello toostore et jeton de hello dissimulation nous n’avez pas besoin tooask pour celle-ci à nouveau.</span><span class="sxs-lookup"><span data-stu-id="242e2-153">Then we want toostore hello user and stash hello token so we don't need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="242e2-154">code de précédent Hello prend tout utilisateur qui se produit tooauthenticate tooour server.</span><span class="sxs-lookup"><span data-stu-id="242e2-154">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="242e2-155">C’est ce qu’on appelle l’enregistrement automatique.</span><span class="sxs-lookup"><span data-stu-id="242e2-155">This is known as auto-registration.</span></span> <span data-ttu-id="242e2-156">Nous vous recommandons de ne laisser tout le monde authentifier le serveur de production tooa sans avoir d’abord les inscrire via un processus que vous décidez de.</span><span class="sxs-lookup"><span data-stu-id="242e2-156">We    recommend that you don't let anyone authenticate tooa production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="242e2-157">Il s’agit généralement de modèle hello que vous voyez dans les applications consommateur, ce qui vous permettent tooregister avec Facebook, mais vous demander des informations supplémentaires tooprovide.</span><span class="sxs-lookup"><span data-stu-id="242e2-157">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you tooprovide additional information.</span></span> <span data-ttu-id="242e2-158">Si cela n’était pas un exemple d’application, nous avons extrait hello son adresse électronique à partir de l’objet du jeton hello qui est retourné et demandé toofill d’utilisateur hello des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="242e2-158">If this weren't a sample application, we could have extracted hello user's email address from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="242e2-159">Comme il s’agit d’un serveur de test, nous les ajoutons toohello base de données.</span><span class="sxs-lookup"><span data-stu-id="242e2-159">Because this is a test server, we add them toohello in-memory database.</span></span>


4. <span data-ttu-id="242e2-160">Ensuite, vous allez ajouter des méthodes hello qui nous tootrack hello utilisateurs connectés comme requis par Passport.</span><span class="sxs-lookup"><span data-stu-id="242e2-160">Next, let's add hello methods that enable us tootrack hello signed-in users as required by Passport.</span></span> <span data-ttu-id="242e2-161">Ces méthodes incluent la sérialisation et la désérialisation des informations de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-161">These methods include serializing and deserializing hello user's information.</span></span>

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

5.  <span data-ttu-id="242e2-162">Ensuite, nous allons ajouter le moteur Express hello hello code tooload.</span><span class="sxs-lookup"><span data-stu-id="242e2-162">Next, let's add hello code tooload hello Express engine.</span></span> <span data-ttu-id="242e2-163">Nous utilisons ici hello par défaut /views et modèle de /routes Express fournit.</span><span class="sxs-lookup"><span data-stu-id="242e2-163">Here we use hello default /views and /routes pattern that Express provides.</span></span>

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

6. <span data-ttu-id="242e2-164">Enfin, vous allez ajouter hello achemine que rassemblerez toohello de demandes de connexion réel hello `passport-azure-ad` moteur :</span><span class="sxs-lookup"><span data-stu-id="242e2-164">Finally, let's add hello routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>


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


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="242e2-165">Étape 4 : Connexion à utiliser Passport tooissue et demandes de déconnexion tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="242e2-165">Step 4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="242e2-166">Votre application est maintenant toocommunicate correctement configurée avec un point de terminaison hello à l’aide du protocole d’authentification OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-166">Your app is now properly configured toocommunicate with hello endpoint by using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="242e2-167">`passport-azure-ad`a prise en charge tous les détails de hello d’élaborer des messages d’authentification, la validation des jetons d’Azure AD et la gestion des sessions utilisateur.</span><span class="sxs-lookup"><span data-stu-id="242e2-167">`passport-azure-ad` has taken care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="242e2-168">Tout ce qui reste est distribution à vos utilisateurs de se déconnecter toosign moyen dans, ainsi que la collecte des informations supplémentaires sur les utilisateurs connectés hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-168">All that remains is giving your users a way toosign in and sign out, and gathering additional information about hello signed-in users.</span></span>

1. <span data-ttu-id="242e2-169">Tout d’abord, nous allons ajouter par défaut de hello, connectez-vous, compte et méthodes déconnexion tooour `app.js` fichier :</span><span class="sxs-lookup"><span data-stu-id="242e2-169">First, let's add hello default, sign-in, account, and sign-out methods tooour `app.js` file:</span></span>

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

2.  <span data-ttu-id="242e2-170">Examinons-les en détail :</span><span class="sxs-lookup"><span data-stu-id="242e2-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="242e2-171">Hello `/`itinéraire redirige toohello index.ejs affichage, en passant les utilisateur hello demande de hello (s’il existe).</span><span class="sxs-lookup"><span data-stu-id="242e2-171">hello `/`route redirects toohello index.ejs view, passing hello user in hello request (if it exists).</span></span>
  * <span data-ttu-id="242e2-172">Hello `/account` Router tout d’abord *garantit que nous sommes authentifiés* (nous implémenter qui Bonjour exemple suivant), et puis passe hello utilisateur dans la demande de hello afin que nous pouvons obtenir plus d’informations sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-172">hello `/account` route first *ensures we are authenticated* (we implement that in hello following example), and then passes hello user in hello request so that we can get additional information about hello user.</span></span>
  * <span data-ttu-id="242e2-173">Hello `/login` itinéraire appelle l’authentificateur de notre organisation-openidconnect de `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="242e2-173">hello `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="242e2-174">Si qui ne réussit pas, il redirige hello arrière trop d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="242e2-174">If that doesn't succeed, it redirects hello user back too/login.</span></span>
  * <span data-ttu-id="242e2-175">Hello `/logout` itinéraire appelle simplement hello logout.ejs (et itinéraire), les cookies d’efface et renvoie ensuite hello tooindex.ejs arrière d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="242e2-175">hello `/logout` route simply calls hello logout.ejs (and route), which clears cookies and then returns hello user back tooindex.ejs.</span></span>

3. <span data-ttu-id="242e2-176">Pour la dernière partie de hello de `app.js`, nous allons ajouter hello **EnsureAuthenticated** méthode qui est utilisée dans `/account`, comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="242e2-176">For hello last part of `app.js`, let's add hello **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

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

4. <span data-ttu-id="242e2-177">Enfin, nous allons créer de serveur hello lui-même dans `app.js`:</span><span class="sxs-lookup"><span data-stu-id="242e2-177">Finally, let's create hello server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a><span data-ttu-id="242e2-178">Étape 5 : toodisplay notre utilisateur dans le site Web de hello, créer des vues hello et les itinéraires dans Express</span><span class="sxs-lookup"><span data-stu-id="242e2-178">Step 5: toodisplay our user in hello website, create hello views and routes in Express</span></span>
<span data-ttu-id="242e2-179">`app.js` est désormais terminé.</span><span class="sxs-lookup"><span data-stu-id="242e2-179">Now `app.js` is complete.</span></span> <span data-ttu-id="242e2-180">Nous avons besoin des itinéraires de hello tooadd simplement et que vous affiche des informations hello nous obtenir toohello utilisateur, ainsi que gérer hello `/logout` et `/login` les itinéraires que nous avons créés.</span><span class="sxs-lookup"><span data-stu-id="242e2-180">We simply need tooadd hello routes and views that show hello information we get toohello user, as well as handle hello `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="242e2-181">Créer hello `/routes/index.js` itinéraire sous le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-181">Create hello `/routes/index.js` route under hello root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="242e2-182">Créer hello `/routes/user.js` itinéraire sous le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-182">Create hello `/routes/user.js` route under hello root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="242e2-183">Ces transmettre les vues de demandes de hello tooour, y compris les utilisateur hello s’il est présent.</span><span class="sxs-lookup"><span data-stu-id="242e2-183">These pass along hello request tooour views, including hello user if present.</span></span>

3. <span data-ttu-id="242e2-184">Créer hello `/views/index.ejs` sous le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-184">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="242e2-185">Il s’agit d’une page simple qui appelle nos méthodes de connexion et de déconnexion et nous permet de toograb les informations de compte.</span><span class="sxs-lookup"><span data-stu-id="242e2-185">This is a simple page that calls our login and logout methods and enables us toograb account information.</span></span> <span data-ttu-id="242e2-186">Notez que nous pouvons utiliser hello conditionnel `if (!user)` comme utilisateur hello transmise par l’intermédiaire de la demande de hello est la preuve que nous avons un utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="242e2-186">Notice that we can use hello conditional `if (!user)` as hello user being passed through in hello request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="242e2-187">Créer hello `/views/account.ejs` afficher sous le répertoire racine de hello afin que nous pouvons afficher des informations supplémentaires qui `passport-azuread` a placé dans la demande de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-187">Create hello `/views/account.ejs` view under hello root directory so that we can view additional information that `passport-azuread` has put in hello user request.</span></span>

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

5. <span data-ttu-id="242e2-188">Améliorons-en l’apparence à l’aide d’une mise en page.</span><span class="sxs-lookup"><span data-stu-id="242e2-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="242e2-189">Créer hello ' / répertoire racine de vue des views/layout.ejs sous hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-189">Create hello '/views/layout.ejs' view under hello root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="242e2-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="242e2-190">Next steps</span></span>
<span data-ttu-id="242e2-191">Enfin, générez et exécutez votre application.</span><span class="sxs-lookup"><span data-stu-id="242e2-191">Finally, build and run your app.</span></span> <span data-ttu-id="242e2-192">Exécutez `node app.js`, puis passez trop`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="242e2-192">Run `node app.js`, and then go too`http://localhost:3000`.</span></span>

<span data-ttu-id="242e2-193">Connectez-vous avec un compte Microsoft personnel ou d’un compte professionnel ou scolaire et notez comment hello l’identité d’utilisateur est répercutée dans la liste d’Account hello.</span><span class="sxs-lookup"><span data-stu-id="242e2-193">Sign in with either a personal Microsoft account or a work or school account, and notice how hello user's identity is reflected in hello /account list.</span></span> <span data-ttu-id="242e2-194">Vous disposez désormais d’une application web sécurisée à l’aide de protocoles standard et pouvant authentifier les utilisateurs avec leurs comptes personnels et professionnels/scolaires.</span><span class="sxs-lookup"><span data-stu-id="242e2-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="242e2-195">Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie comme un fichier .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="242e2-195">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="242e2-196">Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="242e2-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="242e2-197">Vous pouvez maintenant aborder des rubriques plus sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="242e2-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="242e2-198">Vous souhaiterez peut-être tootry :</span><span class="sxs-lookup"><span data-stu-id="242e2-198">You might want tootry:</span></span>

[<span data-ttu-id="242e2-199">Sécurisation d’une API web avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="242e2-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
