---
title: "aaaAdd tooa de connexion dans l’application web Node.js pour Azure B2C | Documents Microsoft"
description: "Comment toobuild une application web de Node.js qui se connecte les utilisateurs à l’aide d’un locataire B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a>Azure AD B2C : Ajouter l’application web connectez-vous tooa Node.js

**Passport** est un intergiciel d’authentification pour Node.js. Extrêmement flexible et modulaire, Passport peut être installé discrètement dans n’importe quelle application web basée sur Express ou Restify. Une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter,etc.

Nous avons développé une stratégie pour Azure Active Directory (Azure AD). Vous allez installer ce module et puis ajoutez hello Azure AD `passport-azure-ad` plug-in.

toodo, vous devez :

1. Inscrivez une application en utilisant Azure AD.
2. Configurer votre hello de toouse application `passport-azure-ad` plug-in.
3. Utilisez Passport tooissue connectez-vous et demandes de déconnexion tooAzure AD.
4. Imprimez les données utilisateur.

Hello du code pour ce didacticiel [est conservée sur GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS). toofollow le long, vous pouvez [télécharger la structure de l’application hello sous forme de fichier .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip). Vous pouvez également dupliquer le squelette de hello :

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

application Hello terminée est fournie à la fin de hello de ce didacticiel.

## <a name="get-an-azure-ad-b2c-directory"></a>Obtention d'un répertoire Azure AD B2C

Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.  Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes, etc. Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant d’aller plus loin dans ce guide.

## <a name="create-an-application"></a>Création d'une application

Ensuite, vous devez toocreate une application dans votre répertoire B2C. Cela fournit des informations de Azure AD lui toocommunicate en toute sécurité avec votre application. Les deux hello application cliente et l’API web est représenté par un seul **ID de l’Application**, car ils constituent une seule application logique. toocreate une application, procédez comme [ces instructions](active-directory-b2c-app-registration.md). Veillez à effectuer les opérations suivantes :

- Inclure un **application web**/**web API** dans l’application hello.
- Entrez `http://localhost:3000/auth/openid/return` comme **URL de réponse**. Il s’agit d’URL par défaut de hello pour cet exemple de code.
- Créez une **clé secrète d’application** pour votre application et copiez-la. Vous en aurez besoin ultérieurement. Notez que cette valeur doit toobe [XML échappé](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) avant de l’utiliser.
- Hello de copie **ID d’Application** qui est attribué tooyour application. Vous allez également en avoir besoin par la suite.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Création de vos stratégies

Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md). Cette application contient trois expériences liées à l’identité : l’inscription, la connexion et la connexion avec Facebook. Vous devez toocreate cette stratégie de chaque type, comme décrit dans la [article de référence de stratégie](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Lors de la création de vos 3 stratégies, assurez-vous de :

- Choisissez hello **nom d’affichage** et d’autres attributs d’inscription de votre stratégie d’inscription.
- Choisissez hello **nom d’affichage** et **ID d’objet** revendications de l’application dans chaque stratégie. Vous pouvez aussi choisir d'autres revendications.
- Hello de copie **nom** de chaque stratégie après l’avoir créée. Il doit avoir le préfixe de hello `b2c_1_`.  Vous aurez besoin des noms de ces stratégies ultérieurement.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Après avoir créé votre trois stratégies, vous êtes prêt toobuild votre application.

Notez que cet article ne couvre pas la façon dont les stratégies hello toouse vous venez de créer. toolearn sur le fonctionnement des stratégies dans Azure AD B2C, commencer par hello [.NET web application mise en route didacticiel](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="add-prerequisites-tooyour-directory"></a>Ajouter un répertoire tooyour de conditions préalables

À partir de la ligne de commande hello, modifiez le dossier racine du tooyour de répertoires, si vous n’êtes pas déjà. Exécutez hello suivant de commandes :

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

En outre, nous avons utilisé `passport-azure-ad` pour notre version préliminaire dans squelette hello Hello démarrage rapide.

- `npm install passport-azure-ad`

Il installe les bibliothèques hello qui `passport-azure-ad` dépend.

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a>Configurer votre hello de toouse application Node.js de Passport stratégie
Configurer un intergiciel (middleware) d’Express Bonjour Bonjour toouse protocole d’authentification OpenID Connect. Passport est utilisé tooissue les demandes de connexion et déconnexion, gérer les sessions utilisateur et obtenir des informations sur les utilisateurs, entre autres.

Ouvrez hello `config.js` fichier racine hello du projet de hello et entrez les valeurs de configuration de votre application Bonjour `exports.creds` section.
- `clientID`: hello **ID d’Application** affecté application tooyour dans le portail de l’enregistrement hello.
- `returnURL`: hello **URI de redirection** vous avez entré dans le portail de hello.
- `tenantName`: nom du client de votre application, par exemple, hello **contoso.onmicrosoft.com**.

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Ouvrez hello `app.js` dans fichier hello la racine du projet de hello. Ajouter hello après appel tooinvoke hello `OIDCStrategy` stratégie qui est fourni avec `passport-azure-ad`.


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

Utilisez stratégie hello vous référencé uniquement les demandes de connexion toohandle.

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
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
Passport utilise un modèle similaire pour l’ensemble de ses stratégies (y compris Twitter et Facebook). Tous les enregistreurs de stratégie respectent toothis modèle. Lorsque vous examinez la stratégie de hello, vous pouvez voir que vous lui passez un `function()` qui a un jeton et un `done` en tant que paramètres de hello. stratégie de Hello revient tooyou après que qu’il a terminé tout son travail. Stocker les utilisateur hello et dissimuler les jeton hello afin que vous n’avez pas besoin tooask pour celle-ci à nouveau.

> [!IMPORTANT]
Hello code précédent prend tous les utilisateurs auxquels hello serveur authentifie. C’est ce que l’on appelle l’enregistrement automatique. Lorsque vous utilisez des serveurs de production, vous ne souhaitez pas toolet dans les utilisateurs, sauf si elles sont passées par un processus d’inscription que vous avez définis. C’est le modèle souvent utilisé dans les applications grand public. Qui vous permettent de tooregister à l’aide de Facebook, mais, ils invite toofill des informations supplémentaires. Si notre application n’était pas un exemple, nous avons extraire une adresse de messagerie à partir de l’objet du jeton hello qui est retournée et puis demandez à toofill d’utilisateur hello des informations supplémentaires. Comme il s’agit d’un serveur de test, nous suffit d’ajouter les utilisateurs toohello base de données.

Ajouter des méthodes hello qui permettent de suivre tookeep d’utilisateurs qui se sont connectés, comme requis par Passport. Cela inclut la sérialisation et la désérialisation des informations des utilisateurs :

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
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

Ajoutez le moteur Express hello hello code tooload. Dans les éléments suivants de hello, vous pouvez voir que nous utilisons par défaut de hello `/views` et `/routes` modèle Express fournit.

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

Ajouter hello `POST` itinéraires remettre hello toohello de demandes de connexion réel `passport-azure-ad` moteur :

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Utilisez Passport tooissue connectez-vous et demandes de déconnexion tooAzure AD

Votre application est maintenant toocommunicate correctement configurée avec un point de terminaison hello v2.0 à l’aide du protocole d’authentification OpenID Connect hello. `passport-azure-ad`a prise en charge des détails de hello d’élaborer des messages d’authentification, la validation des jetons d’Azure AD et la gestion de session utilisateur. Tout ce qui reste est toogive vos utilisateurs un toosign moyen dans et les signer hors et toogather plus d’informations sur les utilisateurs qui sont connectés.

Ajoutez d’abord par défaut de hello, connectez-vous, compte et méthodes déconnexion tooyour `app.js` fichier :

```JavaScript

//Routes (Section 4)

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

tooreview ces méthodes en détail :
- Hello `/` itinéraire redirige toohello `index.ejs` vue en passant l’utilisateur de hello dans la demande hello (s’il existe).
- Hello `/account` itinéraire vérifie d’abord que vous êtes authentifié (hello mise en œuvre pour cette figure ci-dessous). Il passe ensuite les utilisateur hello dans la demande hello qui vous pouvez d’obtenir des informations supplémentaires sur l’utilisateur de hello.
- Hello `/login` itinéraire appels hello `azuread-openidconnect` authentificateur de `passport-azure-ad`. S’il ne réussit pas, les itinéraires hello redirige l’utilisateur hello trop`/login`.
- `/logout` appelle simplement `logout.ejs` (et son itinéraire). Cela efface les cookies et puis retourne hello utilisateur trop`index.ejs`.


Pour la dernière partie de hello de `app.js`, ajouter hello `EnsureAuthenticated` méthode qui est utilisée dans hello `/account` itinéraire.

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

Enfin, créez le serveur hello lui-même dans `app.js`.

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a>Créer des vues hello et achemine dans Express toocall vos stratégies

La création du fichier `app.js` est maintenant terminée. Vous devez simplement les itinéraires de hello tooadd et vues que vous autorisent des stratégies d’ouverture de session et d’inscription toocall hello. Ils gèrent également hello `/logout` et `/login` itinéraires que vous avez créé.

Créer hello `/routes/index.js` itinéraire sous le répertoire racine de hello.

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

Créer hello `/routes/user.js` itinéraire sous le répertoire racine de hello.

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

Vues de demandes tooyour transmettez ces itinéraires simples. Ils comprennent les utilisateur hello, s’il en existe.

Créer hello `/views/index.ejs` sous le répertoire racine de hello. Il s’agit d’une page simple qui appelle des stratégies de connexion et de déconnexion. Vous pouvez également l’utiliser toograb les informations de compte. Notez que vous pouvez utiliser hello conditionnel `if (!user)` comme utilisateur de hello est passé par le biais de demande hello tooprovide preuve que l’utilisateur hello est connecté.

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

Créer hello `/views/account.ejs` afficher sous le répertoire racine de hello afin que vous pouvez afficher des informations supplémentaires qui `passport-azure-ad` placé dans la demande de l’utilisateur hello.

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
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

Vous pouvez maintenant créer et exécuter votre application

Exécutez `node app.js` et accédez trop`http://localhost:3000`


S’inscrire ou se connecter à l’aide de messages électroniques ou Facebook toohello application. Déconnectez-vous, puis reconnectez-vous comme si vous étiez un autre utilisateur.

##<a name="next-steps"></a>Étapes suivantes

Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie comme un fichier .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Vous pouvez également le cloner à partir de GitHub :

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

Vous pouvez maintenant passer toomore rubriques avancées. Vous pouvez essayer :

[Sécuriser une API web à l’aide du modèle de hello B2C dans Node.js](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
