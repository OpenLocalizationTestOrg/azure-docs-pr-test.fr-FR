---
title: "Prise en main de la connexion et de la déconnexion d’Azure AD à l’aide de Node.js | Microsoft Docs"
description: "Découvrez comment créer une application web Node.js Express MVC qui s’intègre avec Azure AD pour la connexion."
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
ms.openlocfilehash: 13317b016f9ff3955f376b858645c42668b0de42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="9ae4c-103">Connexion et déconnexion d’Azure AD à l’aide d’une application web Node.js</span><span class="sxs-lookup"><span data-stu-id="9ae4c-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="9ae4c-104">Nous utilisons Passport pour :</span><span class="sxs-lookup"><span data-stu-id="9ae4c-104">Here we use Passport to:</span></span>

* <span data-ttu-id="9ae4c-105">connecter l’utilisateur à l’application avec Azure Active Directory (Azure AD) ;</span><span class="sxs-lookup"><span data-stu-id="9ae4c-105">Sign the user in to the app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="9ae4c-106">afficher les informations sur l’utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="9ae4c-106">Display information about the user.</span></span>
* <span data-ttu-id="9ae4c-107">déconnecter l’utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-107">Sign the user out of the app.</span></span>

<span data-ttu-id="9ae4c-108">Passport est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="9ae4c-109">Flexible et modulaire, Passport peut discrètement intervenir dans n’importe quelle application web basée sur Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-109">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or restify web application.</span></span> <span data-ttu-id="9ae4c-110">Une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter et bien d’autres.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="9ae4c-111">Nous avons développé une stratégie pour Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="9ae4c-112">Nous installons ce module, puis nous y ajoutons le plug-in `passport-azure-ad` Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-112">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="9ae4c-113">Pour cela, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9ae4c-113">To do this, take the following steps:</span></span>

1. <span data-ttu-id="9ae4c-114">inscrire une application ;</span><span class="sxs-lookup"><span data-stu-id="9ae4c-114">Register an app.</span></span>
2. <span data-ttu-id="9ae4c-115">configurer votre application pour utiliser la stratégie `passport-azure-ad` ;</span><span class="sxs-lookup"><span data-stu-id="9ae4c-115">Set up your app to use the `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="9ae4c-116">utiliser Passport pour émettre des demandes de connexion et de déconnexion dans Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="9ae4c-116">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="9ae4c-117">imprimer les données relatives à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-117">Print data about the user.</span></span>

<span data-ttu-id="9ae4c-118">Le code associé à ce didacticiel est stocké [sur GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="9ae4c-118">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="9ae4c-119">Pour suivre la procédure, vous pouvez [télécharger la structure de l’application au format .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) ou la cloner :</span><span class="sxs-lookup"><span data-stu-id="9ae4c-119">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="9ae4c-120">L'application terminée est également fournie à la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-120">The completed application is provided at the end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="9ae4c-121">Étape 1 : enregistrement d’une application</span><span class="sxs-lookup"><span data-stu-id="9ae4c-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="9ae4c-122">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9ae4c-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="9ae4c-123">Dans le menu situé en haut de la page, sélectionnez votre compte.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-123">In the menu at the top of the page, select your account.</span></span> <span data-ttu-id="9ae4c-124">Dans la liste **Répertoire**, choisissez le locataire Active Directory auprès duquel vous voulez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-124">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="9ae4c-125">Sélectionnez **Plus de services** dans le menu sur la gauche de l’écran, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-125">Select **More Services** in the menu on the left side of the screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="9ae4c-126">Sélectionnez **Inscriptions d’applications**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="9ae4c-127">Suivez les invites et créez une **application web** et/ou une **API web**.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-127">Follow the prompts to create a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="9ae4c-128">Le **nom** de l’application doit décrire votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-128">The **name** of the application describes your application to users.</span></span>

  * <span data-ttu-id="9ae4c-129">L’ **URL de connexion** est l’URL de base de votre application.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-129">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="9ae4c-130">La valeur par défaut de la structure est `http://localhost:3000/auth/openid/return`\`.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-130">The skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="9ae4c-131">Une fois l’application enregistrée, Azure AD lui affecte un ID d’application unique.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="9ae4c-132">Copiez cette valeur à partir de la page de l’application, car vous en aurez besoin dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-132">You need this value in the following sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="9ae4c-133">À partir de la page **Paramètres** -> **Propriétés** de votre application, mettez à jour l’URI ID d’application.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-133">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="9ae4c-134">Un **URI ID d’application** est un identificateur unique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-134">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="9ae4c-135">La convention consiste à utiliser le format `https://<tenant-domain>/<app-name>`, par exemple : `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-135">The convention is to use the format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-to-your-directory"></a><span data-ttu-id="9ae4c-136">Étape 2 : ajout d’éléments requis au répertoire</span><span class="sxs-lookup"><span data-stu-id="9ae4c-136">Step 2: Add prerequisites to your directory</span></span>
1. <span data-ttu-id="9ae4c-137">Dans la ligne de commande, placez les répertoires dans votre dossier racine s’ils n’y sont pas encore, puis exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9ae4c-137">From the command line, change directories to your root folder if you're not already there, and then run the following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="9ae4c-138">De plus, vous avez besoin de `passport-azure-ad` :</span><span class="sxs-lookup"><span data-stu-id="9ae4c-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="9ae4c-139">Cela installe les bibliothèques dont dépend `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-139">This installs the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="9ae4c-140">Étape 3 : configuration de votre application pour utiliser la stratégie passport-nod-js</span><span class="sxs-lookup"><span data-stu-id="9ae4c-140">Step 3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="9ae4c-141">Ici, nous configurons Express pour utiliser le protocole d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-141">Here, we configure Express to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="9ae4c-142">Passport est utilisé pour plusieurs choses, notamment pour émettre des demandes de connexion et de déconnexion, gérer la session utilisateur et obtenir des informations concernant l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-142">Passport is used to do various things, including issue sign-in and sign-out requests, manage the user's session, and get information about the user.</span></span>

1. <span data-ttu-id="9ae4c-143">Pour commencer, ouvrez le fichier `config.js` dans la racine du projet, puis entrez les valeurs de configuration de votre application dans la section `exports.creds`.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-143">To begin, open the `config.js` file at the root of the project, and then enter your app's configuration values in the `exports.creds` section.</span></span>

  * <span data-ttu-id="9ae4c-144">L’élément `clientID` est l’**ID d’application** affecté à votre application dans le portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-144">The `clientID` is the **Application Id** that's assigned to your app in the registration portal.</span></span>

  * <span data-ttu-id="9ae4c-145">L’élément `returnURL` est l’**URI de redirection** que vous avez saisie dans le portail.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-145">The `returnURL` is the **Redirect Uri** that you entered in the portal.</span></span>

  * <span data-ttu-id="9ae4c-146">L’élément `clientSecret` est la clé secrète que vous avez générée dans le portail.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-146">The `clientSecret` is the secret that you generated in the portal.</span></span>

2. <span data-ttu-id="9ae4c-147">Ouvrez ensuite le fichier `app.js` à la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-147">Next, open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="9ae4c-148">Ajoutez l’appel suivant pour appeler la stratégie `OIDCStrategy` qui accompagne `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-148">Then add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="9ae4c-149">Après cela, utilisez la stratégie référencée pour gérer les demandes de connexion.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-149">After that, use the strategy we just referenced to handle our sign-in requests.</span></span>

    ```JavaScript
    // Use the OIDCStrategy within Passport. (Section 2)
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
<span data-ttu-id="9ae4c-150">Passport utilise un modèle semblable pour toutes ses stratégies (Twitter, Facebook, etc.), que respectent tous les enregistreurs de stratégie.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="9ae4c-151">Comme vous pouvez le voir dans la stratégie, nous transmettons une fonction dont les paramètres sont un jeton et un done.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-151">Looking at the strategy, you see that we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="9ae4c-152">La stratégie nous revient une fois le travail effectué.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-152">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="9ae4c-153">Il est alors intéressant de stocker l’utilisateur et le jeton afin de ne pas avoir à les redemander.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-153">Then we want to store the user and stash the token so we don't need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="9ae4c-154">Le code précédent note tout utilisateur s’authentifiant sur notre serveur.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-154">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="9ae4c-155">C’est ce qu’on appelle l’enregistrement automatique.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-155">This is known as auto-registration.</span></span> <span data-ttu-id="9ae4c-156">Nous vous recommandons de ne laisser personne s’authentifier auprès d’un serveur de production sans l’obliger au préalable à s’inscrire via un processus dont vous décidez.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-156">We    recommend that you don't let anyone authenticate to a production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="9ae4c-157">C’est généralement le modèle des applications consommateur, qui vous permettent de vous inscrire via Facebook mais vous demandent ensuite des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-157">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to provide additional information.</span></span> <span data-ttu-id="9ae4c-158">S’il ne s’agissait pas d’un exemple d’application, nous aurions pu extraire l’adresse e-mail à partir de l’objet de jeton retourné, avant d’inviter l’utilisateur à entrer des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-158">If this weren't a sample application, we could have extracted the user's email address from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="9ae4c-159">Comme il s’agit d’un serveur de test, nous les ajoutons à la base de données en mémoire.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-159">Because this is a test server, we add them to the in-memory database.</span></span>


4. <span data-ttu-id="9ae4c-160">Ensuite, nous allons ajouter les méthodes qui assurent le suivi des utilisateurs connectés, comme requis par Passport.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-160">Next, let's add the methods that enable us to track the signed-in users as required by Passport.</span></span> <span data-ttu-id="9ae4c-161">Ces méthodes incluent la sérialisation et la désérialisation des informations d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-161">These methods include serializing and deserializing the user's information.</span></span>

    ```JavaScript

            // Passport session setup. (Section 2)

            //   To support persistent sign-in sessions, Passport needs to be able to
            //   serialize users into the session and deserialize them out of the session. Typically,
            //   this is done simply by storing the user ID when serializing and finding
            //   the user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array to hold signed-in users
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

5.  <span data-ttu-id="9ae4c-162">Ensuite, nous allons ajouter le code pour charger le moteur Express.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-162">Next, let's add the code to load the Express engine.</span></span> <span data-ttu-id="9ae4c-163">Ici, nous utiliserons le modèle par défaut /views et /routes fourni par Express.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-163">Here we use the default /views and /routes pattern that Express provides.</span></span>

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
          // Initialize Passport!  Also use passport.session() middleware, to support
          // persistent login sessions (recommended).
          app.use(passport.initialize());
          app.use(passport.session());
          app.use(app.router);
          app.use(express.static(__dirname + '/../../public'));
        });

    ```

6. <span data-ttu-id="9ae4c-164">Enfin, nous allons ajouter les itinéraires qui transmettent les demandes d’ouverture de session au moteur `passport-azure-ad` :</span><span class="sxs-lookup"><span data-stu-id="9ae4c-164">Finally, let's add the routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware to authenticate the
        //   request. The first step in OpenID authentication involves redirecting
        //   the user to their OpenID provider. After authenticating, the OpenID
        //   provider redirects the user back to this application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in the Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="9ae4c-165">Étape 4 : utilisation de Passport pour émettre des demandes de connexion et de déconnexion dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ae4c-165">Step 4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="9ae4c-166">Votre application est maintenant correctement configurée pour communiquer avec le point de terminaison en utilisant le protocole d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-166">Your app is now properly configured to communicate with the endpoint by using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="9ae4c-167">`passport-azure-ad` a pris en charge tous les détails de la création de messages d’authentification, de la validation des jetons d’Azure AD et de la gestion des sessions utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-167">`passport-azure-ad` has taken care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="9ae4c-168">Il ne reste plus qu’à fournir aux utilisateurs un moyen de se connecter, de se déconnecter et de collecter des informations supplémentaires sur les utilisateurs connectés.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-168">All that remains is giving your users a way to sign in and sign out, and gathering additional information about the signed-in users.</span></span>

1. <span data-ttu-id="9ae4c-169">Tout d’abord, nous allons ajouter au fichier `app.js` les méthodes par défaut de connexion, de compte et de déconnexion :</span><span class="sxs-lookup"><span data-stu-id="9ae4c-169">First, let's add the default, sign-in, account, and sign-out methods to our `app.js` file:</span></span>

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
            log.info('Login was called in the Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  <span data-ttu-id="9ae4c-170">Examinons-les en détail :</span><span class="sxs-lookup"><span data-stu-id="9ae4c-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="9ae4c-171">L’itinéraire `/` redirige vers la vue index.ejs en transmettant l’utilisateur dans la demande (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="9ae4c-171">The `/`route redirects to the index.ejs view, passing the user in the request (if it exists).</span></span>
  * <span data-ttu-id="9ae4c-172">L’itinéraire `/account` *s’assure d’abord que nous sommes authentifiés* (nous implémentons cela dans l’exemple suivant), puis transmet l’utilisateur dans la demande afin que nous puissions obtenir des informations supplémentaires sur l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-172">The `/account` route first *ensures we are authenticated* (we implement that in the following example), and then passes the user in the request so that we can get additional information about the user.</span></span>
  * <span data-ttu-id="9ae4c-173">L’itinéraire `/login` appelle notre authentificateur azuread-openidconnect à partir de `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-173">The `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="9ae4c-174">En cas d’échec, il redirige l’utilisateur vers la page de connexion.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-174">If that doesn't succeed, it redirects the user back to /login.</span></span>
  * <span data-ttu-id="9ae4c-175">L’itinéraire `/logout` appelle simplement logout.ejs (et l’itinéraire) qui efface les cookies, puis renvoie l’utilisateur à index.ejs.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-175">The `/logout` route simply calls the logout.ejs (and route), which clears cookies and then returns the user back to index.ejs.</span></span>

3. <span data-ttu-id="9ae4c-176">Pour la dernière partie de `app.js`, ajoutons la méthode **EnsureAuthenticated** utilisée dans `/account`, comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-176">For the last part of `app.js`, let's add the **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript

        // Simple route middleware to ensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs to be protected. If
        //   the request is authenticated (typically via a persistent sign-in session),
        //   the request proceeds. Otherwise, the user is redirected to the
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. <span data-ttu-id="9ae4c-177">Enfin, créons le serveur proprement dit dans `app.js` :</span><span class="sxs-lookup"><span data-stu-id="9ae4c-177">Finally, let's create the server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-to-display-our-user-in-the-website-create-the-views-and-routes-in-express"></a><span data-ttu-id="9ae4c-178">Étape 5 : création de vues et d’itinéraires dans Express pour afficher notre utilisateur dans le site web</span><span class="sxs-lookup"><span data-stu-id="9ae4c-178">Step 5: To display our user in the website, create the views and routes in Express</span></span>
<span data-ttu-id="9ae4c-179">`app.js` est désormais terminé.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-179">Now `app.js` is complete.</span></span> <span data-ttu-id="9ae4c-180">Il suffit d'ajouter les itinéraires et les vues qui affichent les informations que nous obtenons de l'utilisateur et traitent les itinéraires `/logout` et `/login` que nous avons créés.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-180">We simply need to add the routes and views that show the information we get to the user, as well as handle the `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="9ae4c-181">Créez l’itinéraire `/routes/index.js` sous le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-181">Create the `/routes/index.js` route under the root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="9ae4c-182">Créez l’itinéraire `/routes/user.js` sous le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-182">Create the `/routes/user.js` route under the root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="9ae4c-183">Ils transmettent la demande à nos vues, en incluant l’utilisateur le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-183">These pass along the request to our views, including the user if present.</span></span>

3. <span data-ttu-id="9ae4c-184">Créez la vue `/views/index.ejs` sous le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-184">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="9ae4c-185">Il s’agit d’une page simple qui appelle nos méthodes de connexion et de déconnexion et nous permet de récupérer des informations de compte.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-185">This is a simple page that calls our login and logout methods and enables us to grab account information.</span></span> <span data-ttu-id="9ae4c-186">Notez que nous pouvons utiliser l’instruction conditionnelle `if (!user)` , étant donné que l’utilisateur transmis dans la demande prouve qu’un utilisateur est connecté.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-186">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="9ae4c-187">Créez la vue `/views/account.ejs` sous le répertoire racine, afin d’afficher les informations supplémentaires que `passport-azuread` a placées dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-187">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azuread` has put in the user request.</span></span>

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

5. <span data-ttu-id="9ae4c-188">Améliorons-en l’apparence à l’aide d’une mise en page.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="9ae4c-189">Créez l’affichage « /views/layout.ejs » sous le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-189">Create the '/views/layout.ejs' view under the root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="9ae4c-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ae4c-190">Next steps</span></span>
<span data-ttu-id="9ae4c-191">Enfin, générez et exécutez votre application.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-191">Finally, build and run your app.</span></span> <span data-ttu-id="9ae4c-192">Exécutez `node app.js`, puis accédez à `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-192">Run `node app.js`, and then go to `http://localhost:3000`.</span></span>

<span data-ttu-id="9ae4c-193">Connectez-vous avec un compte Microsoft personnel ou un compte professionnel ou scolaire, et notez comment l’identité de l’utilisateur est indiquée dans la liste de comptes.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-193">Sign in with either a personal Microsoft account or a work or school account, and notice how the user's identity is reflected in the /account list.</span></span> <span data-ttu-id="9ae4c-194">Vous disposez désormais d’une application web sécurisée à l’aide de protocoles standard et pouvant authentifier les utilisateurs avec leurs comptes personnels et professionnels/scolaires.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="9ae4c-195">Pour référence, l’exemple terminé (sans vos valeurs de configuration) [est fourni en tant que fichier .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="9ae4c-195">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="9ae4c-196">Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="9ae4c-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="9ae4c-197">Vous pouvez maintenant aborder des rubriques plus sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="9ae4c-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="9ae4c-198">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9ae4c-198">You might want to try:</span></span>

[<span data-ttu-id="9ae4c-199">Sécurisation d’une API web avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ae4c-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
