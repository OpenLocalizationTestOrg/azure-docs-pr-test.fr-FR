---
title: "Azure AD B2C : sécuriser une API web à l’aide de Node.js | Microsoft Docs"
description: "Comment toobuild un Node.js web API qui accepte les jetons provenant d’un locataire B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a>Azure AD B2C : sécuriser une API web à l’aide de Node.js
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

Avec Azure Active Directory (Azure AD) B2C, vous pouvez sécuriser une API web à l’aide de jetons d’accès OAuth 2.0, Ces jetons permettent à vos applications clientes qui utilisent Azure AD B2C tooauthenticate toohello API. Cet article vous explique comment toocreate une API de la « liste des tâches » qui permet aux utilisateurs tooadd et liste des tâches. Hello web API est sécurisé à l’aide d’Azure AD B2C et autorise uniquement les utilisateurs authentifiés toomanage leur liste de tâches.

> [!NOTE]
> Cet exemple a été écrit à l’aide de tooby toobe connecté notre [iOS B2C exemple d’application](active-directory-b2c-devquickstarts-ios.md). Hello en cours de la procédure tout d’abord, puis suivez avec cet exemple.
>
>

**Passport** est un intergiciel d’authentification pour Node.js. Flexible et modulaire, Passport peut être installé discrètement dans toute application web basée sur Express ou Restify. Une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter,etc. Nous avons développé une stratégie pour Azure Active Directory (Azure AD). Vous installez ce module et que vous ajoutez ensuite hello Azure AD `passport-azure-ad` plug-in.

toodo cet exemple, vous devez :

1. inscrivez une application auprès d’Azure AD ;
2. Configurer votre application toouse Passport `azure-ad-passport` plug-in.
3. Configurer une client application toocall hello « liste de tâches » API web.

## <a name="get-an-azure-ad-b2c-directory"></a>Obtention d'un répertoire Azure AD B2C
Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.  Un répertoire est un conteneur destiné à recevoir tous les utilisateurs, applications, groupes et autres.  Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant de continuer.

## <a name="create-an-application"></a>Création d'une application
Ensuite, vous devez toocreate une application dans votre répertoire B2C qui donne à Azure AD des informations qu’il doit toosecurely communiquer avec votre application. Dans ce cas, application de client hello et API web sont représentés par un seul **ID de l’Application**, car ils constituent une seule application logique. toocreate une application, procédez comme [ces instructions](active-directory-b2c-app-registration.md). Veillez à effectuer les opérations suivantes :

* Inclure un **web web/de l’application api** dans l’application hello
* Entrez `http://localhost/TodoListService` comme **URL de réponse**. Il s’agit d’URL par défaut de hello pour cet exemple de code.
* Créez une **clé secrète d’application** pour votre application et copiez-la. Vous aurez besoin de cette donnée ultérieurement. Notez que cette valeur doit toobe [XML échappé](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) avant de l’utiliser.
* Hello de copie **ID d’Application** qui est attribué tooyour application. Vous aurez besoin de cette donnée ultérieurement.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Création de vos stratégies
Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md). Cette application contient deux expériences d’identité : l’inscription et la connexion. Vous devez toocreate une stratégie de chaque type, comme décrit dans la [article de référence de stratégie](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).  Lors de la création de vos 3 stratégies, assurez-vous de :

* Choisissez hello **nom d’affichage** et d’autres attributs d’inscription de votre stratégie d’inscription.
* Choisissez hello **nom d’affichage** et **ID d’objet** revendications de l’application dans chaque stratégie.  Vous pouvez aussi choisir d'autres revendications.
* Copie vers le bas hello **nom** de chaque stratégie après l’avoir créée. Il doit avoir le préfixe de hello `b2c_1_`.  Vous aurez besoin des noms de ces stratégies ultérieurement.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Après avoir créé votre trois stratégies, vous êtes prêt toobuild votre application.

toolearn sur le fonctionnement des stratégies dans Azure AD B2C, commencer par hello [.NET web application mise en route didacticiel](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="download-hello-code"></a>Télécharger le code de hello
Hello du code pour ce didacticiel [est conservée sur GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS). exemple de hello toobuild en tant que vous accédez, vous pouvez [télécharger un projet sous forme de fichier .zip de squelette](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip). Vous pouvez également dupliquer le squelette de hello :

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

application Hello terminée est également [disponible sous forme de fichier .zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) ou sur hello `complete` branche Hello même référentiel.

## <a name="download-nodejs-for-your-platform"></a>Télécharger Node.js pour votre plateforme
toosuccessfully utiliser cet exemple, vous avez besoin d’une installation active de Node.js.

Installez Node.js à partir de [nodejs.org](http://nodejs.org).

## <a name="install-mongodb-for-your-platform"></a>Installer MongoDB pour votre plateforme
toosuccessfully utiliser cet exemple, vous avez besoin d’une installation active de MongoDB. Nous utilisons MongoDB toomake de votre API REST persistant entre les instances de serveur.

Installez MongoDB à partir de [mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Cette procédure pas à pas suppose que vous utilisez des points de terminaison hello par défaut installation et le serveur pour MongoDB, c'est-à-dire lors de cette écriture hello `mongodb://localhost`.
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a>Installer des modules de Restify hello dans votre API web
Nous utilisons Restify toobuild votre API REST. Restify est une infrastructure d’application Node.js minimale et flexible dérivée d’Express. Elle inclut un ensemble complet de fonctionnalités de création API REST sur Connect.

### <a name="install-restify"></a>Installation de Restify
À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`. Si hello `azuread` répertoire n’existe pas, créez-le.

`cd azuread` ou `mkdir azuread;`

Entrez hello de commande suivante :

`npm install restify`

Cette commande permet d’installer Restify.

#### <a name="did-you-get-an-error"></a>Une erreur est-elle survenue ?
Dans certains systèmes d’exploitation, lorsque vous utilisez `npm`, vous pouvez recevoir hello erreur `Error: EPERM, chmod '/usr/local/bin/..'` et une demande que vous exécutez un compte de hello en tant qu’administrateur. Si ce problème se produit, utilisez hello `sudo` commande toorun `npm` à un niveau de privilège supérieur.

#### <a name="did-you-get-a-dtrace-error"></a>Avez-vous reçu une erreur DTrace ?
Lors de l’installation de Restify, un texte semblable au suivant peut s’afficher :

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

Restify fournit un mécanisme puissant pour suivre les appels REST à l’aide de DTrace. Toutefois, de nombreux systèmes d’exploitation ne disposent pas de DTrace. Vous pouvez ignorer ces erreurs.

Hello une sortie de la commande hello doit apparaître le texte toothis similaire :

    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a>Installer Passport.dans votre API web
À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà.

Installez Passport à l’aide de hello de commande suivante :

`npm install passport`

sortie de Hello de commande hello doit être texte toothis similaire :

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a>Ajouter l’organisation de passport tooyour web API
Ajoutez ensuite la stratégie d’OAuth hello à l’aide de `passport-azuread`, un ensemble de stratégies qui se connectent Azure AD à Passport. Utilisez cette stratégie pour les jetons de support dans l’exemple d’API REST hello.

> [!NOTE]
> Bien qu’OAuth2 fournisse une infrastructure dans laquelle tout type de jeton connu peut être émis, seuls certains types de jeton sont utilisés de manière généralisée. les jetons de Hello pour protéger les points de terminaison sont des jetons de support. Ces types de jetons sont hello plus largement émis dans OAuth2. De nombreuses implémentations supposent que les jetons de porteur hello seul type de jeton émis.
>
>

À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà.

Installer hello Passport `passport-azure-ad` module à l’aide de hello de commande suivante :

`npm install passport-azure-ad`

sortie de Hello de commande hello doit être texte toothis similaire :

``
passport-azure-ad@1.0.0 node_modules/passport-azure-ad
├── xtend@4.0.0
├── xmldom@0.1.19
├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
├── underscore@1.8.3
├── async@1.3.0
├── jsonwebtoken@5.0.2
├── xml-crypto@0.5.27 (xpath.js@1.0.6)
├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
└── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
``

## <a name="add-mongodb-modules-tooyour-web-api"></a>Ajout de MongoDB modules tooyour web API
Cet exemple utilise MongoDB comme magasin de données. Pour ce dernier, installez Mongoose, un plug-in largement utilisé pour la gestion des modèles et des schémas.

* `npm install mongoose`

## <a name="install-additional-modules"></a>Installation de modules supplémentaires
Ensuite, installez hello restant modules requis.

À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :

`cd azuread`

Installer les modules hello dans votre `node_modules` active :

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a>Créer un fichier server.js avec vos dépendances
Hello `server.js` fichier fournit la majorité de hello des fonctionnalités de hello pour votre serveur d’API Web.

À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :

`cd azuread`

Créez un fichier `server.js` dans un éditeur. Ajoutez hello informations suivantes :

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

Enregistrez le fichier de hello. Vous revenez plus tard tooit.

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a>Créer un toostore de fichier config.js vos paramètres Azure AD
Ce fichier de code transmet les paramètres de configuration hello à partir de votre portail Azure AD de toohello `Passport.js` fichier. Vous avez créé ces valeurs de configuration lorsque vous avez ajouté le portail de hello web API toohello dans hello première partie de procédure pas à pas hello. Nous vous expliquons quels tooput dans les valeurs hello de ces paramètres après avoir copié les code hello.

À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :

`cd azuread`

Créez un fichier `config.js` dans un éditeur. Ajoutez hello informations suivantes :

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a>Valeurs requises
`clientID`: hello ID client de votre application d’API Web.

`IdentityMetadata`: Cette propriété est si `passport-azure-ad` recherche de vos données de configuration pour le fournisseur d’identité hello. Il recherche également des jetons web hello clés toovalidate hello JSON.

`audience`: hello URI (URI) à partir du portail hello qui identifie votre application appelante.

`tenantName`: nom de votre locataire (par exemple, **contoso.onmicrosoft.com**).

`policyName`: hello stratégie que vous souhaitez les jetons de hello toovalidate dans tooyour server à venir. Cette stratégie doit être hello même stratégie que vous utilisez dans l’application hello client pour la connexion.

> [!NOTE]
> Pour l’instant, utilisez hello même stratégies sur le programme d’installation de client et le serveur. Si vous avez déjà effectué une procédure pas à pas et créé ces stratégies, vous n’avez pas besoin toodo encore une fois. Étant donné que vous effectué la procédure pas à pas hello, vous ne doivent pas devez tooset des nouvelles stratégies pour les procédures détaillées de client sur le site de hello.
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a>Ajouter le fichier de configuration tooyour server.js
valeurs hello tooread hello `config.js` que vous avez créé, ajoutez hello `.config` comme une ressource requise dans votre application, puis, définissez hello variables globales toothose Bonjour `config.js` document.

À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :

`cd azuread`

Ouvrez hello `server.js` fichier dans un éditeur. Ajoutez hello informations suivantes :

```Javascript
var config = require('./config');
```
Ajouter une nouvelle section trop`server.js` incluant hello suivant de code :

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

Ensuite, vous allez ajouter des espaces réservés pour les utilisateurs de hello nous recevons de nos applications appelante.

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

Nous allons également créer notre enregistreur d’événements.

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Ajouter des informations de modèle et schéma de MongoDB hello à l’aide de Mongoose
Hello préparation antérieure bénéfiques Bring de ces trois fichiers dans un service de l’API REST.

Pour cette procédure pas à pas, utiliser des MongoDB toostore vos tâches, comme indiqué précédemment.

Bonjour `config.js` fichier, vous avez appelé votre base de données **tasklist**. Ce nom a été également ce que vous mettez à fin hello Hello `mongoose_auth_local` URL de connexion. Vous n’avez pas besoin toocreate cette base de données au préalable dans MongoDB. Il crée de la base de données hello de hello première exécution de votre application serveur.

Une fois que vous indiquez à quel toouse de base de données MongoDB server de hello, vous devez toowrite certains modèles de code supplémentaire toocreate hello et un schéma pour vos tâches de serveur.

### <a name="expand-hello-model"></a>Développez le modèle de hello
Ce modèle de schéma est simple. Vous pouvez le développer en fonction de vos besoins.

`owner`: Qui est assigné toohello tâche. Cet objet est une **chaîne**.  

`Text`: tâche hello lui-même. Cet objet est une **chaîne**.

`date`: date de hello que la tâche hello est plein. Cet objet est une **dateHeure**.

`completed`: Si la tâche hello est terminée. Cet objet est un **booléen**.

### <a name="create-hello-schema-in-hello-code"></a>Créer un schéma de hello dans le code hello
À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :

`cd azuread`

Ouvrez hello `server.js` fichier dans un éditeur. Ajoutez hello informations sous l’entrée de configuration hello suivantes :

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
Vous créez tout d’abord le schéma de hello, puis vous créez un objet de modèle que vous utilisez toostore vos données dans l’ensemble de hello code lorsque vous définissez votre **itinéraires**.

## <a name="add-routes-for-your-rest-api-task-server"></a>Ajouter des itinéraires pour votre serveur de la tâche API REST
Maintenant que vous avez un toowork de modèle de base de données avec, ajoutez des itinéraires hello que vous utilisez pour votre serveur d’API REST.

### <a name="about-routes-in-restify"></a>À propos des itinéraires dans Restify
Fonctionnement des gammes Restify Bonjour même façon qu’ils utilisent lorsqu’ils utilisent la pile de Express hello. Vous définissez des itinéraires à l’aide de hello URI que vous attendez hello client applications toocall.

Voici un exemple de modèle d’un itinéraire Restify :

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

Restify et Express fournissent des fonctionnalités bien plus approfondies, comme la définition de types d’application et la création d’un routage complexe entre différents points de terminaison. Pour des raisons de hello de ce didacticiel, nous conserver ces itinéraires simple.

#### <a name="add-default-routes-tooyour-server"></a>Ajouter le serveur de tooyour d’itinéraires par défaut
Vous ajoutez maintenant les itinéraires CRUD base hello de **créer** et **liste** pour notre API REST. Vous trouverez les autres itinéraires Bonjour `complete` branche de l’exemple hello.

À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :

`cd azuread`

Ouvrez hello `server.js` fichier dans un éditeur. Sous les entrées de base de données hello apportées ci-dessus ajouter hello informations suivantes :

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
    _task.date = new Date();

    _task.save(function(err) {
        if (err) {
            req.log.warn(err, 'createTask: unable toosave');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err)
            return next(err);

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Add one!");
        }

        if (!owner) {
            log.warn(err, "You did not pass an owner when listing tasks.");
        } else {

            res.json(data);

        }
    });

    return next();
}
```


#### <a name="add-error-handling-for-hello-routes"></a>Ajouter la gestion des erreurs pour les itinéraires hello
Ajoutez une gestion des erreurs afin que vous pouvez communiquer les problèmes de client toohello précédent de manière à ce qu’il puisse comprendre.

Ajoutez hello suivant de code :

```Javascript
///--- Errors for communicating something interesting back toohello client
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="create-your-server"></a>Créer votre serveur
Vous avez maintenant défini votre base de données et mis vos itinéraires en place. dernière chose de Hello pour vous toodo est tooadd hello server instance qui gère vos appels.

Restify et Express fournissent une forte personnalisation pour un serveur d’API REST, mais nous utilisons le programme d’installation plus simple de hello ici.

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a>Ajouter hello itinéraires toohello serveur (sans authentification)
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a>Ajouter le serveur d’authentification tooyour API REST
Maintenant que vous disposez d’un serveur API REST en cours d’exécution, vous pouvez l’utiliser dans Azure AD.

À partir de la ligne de commande hello, remplacez votre répertoire trop`azuread`, s’il n’est pas déjà :

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Utilisez hello OIDCBearerStrategy qui est inclus avec passport-azure-ad
> [!TIP]
> Lorsque vous écrivez API, vous devez lier toujours hello toosomething de données unique à partir du jeton hello qui hello utilisateur ne peut pas usurper l’identité. Lorsque le serveur de hello stocke des éléments de tâche, il est par conséquent, en fonction de hello **oid** d’utilisateur hello dans le jeton hello (appelé via token.oid), qui s’intègre dans le champ hello « propriétaire ». Cette valeur permet de s’assurer que seul cet utilisateur peut accéder à ses propres tâches. Il n’aucune exposition Bonjour API de « propriétaire », un utilisateur externe peut demander que d’autres éléments de tâche même s’ils sont authentifiés.
>
>

Ensuite, utilisez la stratégie de support hello fourni avec `passport-azure-ad`.

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

Passport utilise hello même modèle pour toutes les stratégies de son. Vous lui transmettez une `function()` qui dispose des paramètres `token` et `done`. stratégie de Hello revient tooyou après que qu’il a terminé tout son travail. Vous devez ensuite stocker utilisateur de hello et enregistrer le jeton de hello afin que vous n’avez pas besoin tooask pour celle-ci à nouveau.

> [!IMPORTANT]
> code Hello ci-dessus prend tout utilisateur qui se produit tooauthenticate tooyour server. Ce processus est appelé enregistrement automatique. Dans les serveurs de production, ne laissez pas dans les API hello d’accès aux utilisateurs sans avoir d’abord les passent par un processus d’inscription. Ce processus est généralement hello modèle que s’affiche dans les applications consommateur qui vous permettent tooregister à l’aide de Facebook, mais vous demander de toofill des informations supplémentaires. Si ce programme n’est pas un programme de ligne de commande, nous avons extrait par courrier électronique hello à partir de l’objet du jeton hello qui est retourné et demandé toofill aux utilisateurs des informations supplémentaires. Comme il s’agit d’un exemple, nous les ajoutons tooan base de données.
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a>Exécutez votre tooverify d’application serveur qu’il rejette vous
Vous pouvez utiliser `curl` toosee si vous avez maintenant OAuth2 protection par rapport à vos points de terminaison. Hello en-têtes retournés doivent être suffisamment tootell que vous êtes sur le chemin d’accès correct de hello.

Vérifiez que votre instance MongoDB est en cours d’exécution :

    $sudo mongodb

Modifier toohello active et le serveur d’exécution hello :

    $ cd azuread
    $ node server.js

Dans une nouvelle fenêtre de terminal, exécutez `curl`

Essayez une commande basique, comme POST :

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

Une erreur 401 est réponse hello souhaitée. Il indique que cette couche de Passport hello essaie tooredirect toohello de point de terminaison authorize.

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a>Vous disposez maintenant d’un service API REST qui utilise OAuth2.
Vous avez implémenté une API REST à l’aide de Restify et d’OAuth. Vous avez maintenant suffisamment code afin que vous pouvez continuer toodevelop votre service et générer cet exemple. Vous êtes allé aussi loin que possible avec ce serveur sans utiliser un client compatible OAuth2. Pour cette étape suivante, utilisez une procédure pas à pas supplémentaires comme notre [connecter tooa web API à l’aide d’iOS avec B2C](active-directory-b2c-devquickstarts-ios.md) procédure pas à pas.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez maintenant déplacer des rubriques toomore avancée, telles que :

[Se connecter tooa web API à l’aide d’iOS avec B2C](active-directory-b2c-devquickstarts-ios.md)
