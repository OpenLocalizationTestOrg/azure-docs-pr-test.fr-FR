---
title: aaaAzure AD Node.js prise en main | Documents Microsoft
description: "Comment toobuild une API web de Node.js REST qui s’intègre à Azure AD pour l’authentification."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a>Prise en main d’API web pour Node.js
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

*Passport* est un intergiciel d’authentification pour Node.js. Flexible et modulaire, Passport peut être supprimé de manière transparente dans tooany rapides ou Restify d’application web. Une gamme complète de stratégies prend en charge l’authentification avec un nom d’utilisateur et un mot de passe, Facebook, Twitter et bien d’autres. Nous avons développé une stratégie pour Microsoft Azure Active Directory (Azure AD). Nous installer ce module et puis ajoutez hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.

toodo, vous devez :

1. inscrivez une application auprès d’Azure AD ;
2. Configurer votre application toouse Passport `passport-azure-ad` plug-in.
3. Configurer une client application toocall hello tooDo API web de liste.

code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).

> [!NOTE]
> Cet article n’aborde pas comment tooimplement connectez-vous, d’abonnement, ou le profil de gestion avec Azure Active Directory B2C. Il se concentre sur des API web appelant après que hello utilisateur est déjà authentifié.  Nous vous recommandons de commencer avec [comment toointegrate avec le document d’Azure Active Directory](active-directory-how-to-integrate.md) toolearn relatives aux principes élémentaires de hello d’Azure Active Directory.
>
>

Nous avons publié à tout le code source hello pour cet exemple en cours d’exécution dans GitHub sous une licence du MIT, nous avons tooclone libre (ou mieux encore, branche) et fournir des commentaires et extraire des demandes.

## <a name="about-nodejs-modules"></a>À propos des modules Node.js
Nous utilisons des modules Node.js au cours de cette procédure détaillée. Les modules sont des packages JavaScript chargeables qui fournissent une fonctionnalité spécifique à votre application. Généralement, vous installez des modules d’à l’aide de hello Node.js un outil de ligne de commande NPM dans le répertoire d’installation NPM hello. Toutefois, certains modules, tels que du module HTTP du hello, sont inclus dans le package de Node.js hello core.

Modules installés sont enregistrés dans hello **node_modules** répertoire à votre répertoire d’installation de Node.js racine hello. Chaque module Bonjour **node_modules** répertoire maintient son propre **node_modules** répertoire qui contient tous les modules dont il dépend. Chaque module requis dispose également de son propre répertoire **node_modules**. Cette structure de répertoire récursive représente la chaîne de dépendance hello.

Cette structure de chaîne de dépendance augmente l’encombrement de l’application. Mais elle garantit également que toutes les dépendances sont respectées, cette version de modules de hello hello qui est utilisée dans le développement est également utilisée en production. Comportement d’application hello de production est ainsi plus prévisibles et évite les problèmes de contrôle de version qui peuvent affecter les utilisateurs.

## <a name="step-1-register-an-azure-ad-tenant"></a>Étape 1 : inscription d’un client Azure AD
toouse cet exemple, vous avez besoin d’un locataire Azure Active Directory. Si vous ne savez pas quel un locataire est ou tooget, voir [comment tooget une annonce Azure locataire](active-directory-howto-tenant.md).

## <a name="step-2-create-an-application"></a>Étape 2 : création d’une application
Ensuite, vous créez une application dans votre annuaire que Azure AD de fournit des informations qu’il doit toosecurely communiquent avec votre application.  Application cliente de hello et API web sont représentés par un seul **ID d’Application** dans ce cas, car ils constituent une seule application logique.  toocreate une application, procédez comme [ces instructions](active-directory-how-applications-are-added.md). Si vous générez une application métier, [ces instructions supplémentaires peuvent être utiles](../active-directory-applications-guiding-developers-for-lob-applications.md).

toocreate une application :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Dans le menu supérieur de hello, sélectionnez votre compte. Ensuite, sous hello **répertoire** , choisissez client Active Directory de hello où vous souhaitez tooregister votre application.

3. Dans le menu hello hello gauche, sélectionnez **plus Services**, puis sélectionnez **Azure Active Directory**.

4. Sélectionnez **Inscriptions d’applications**, puis **Ajouter**.

5. Suivez hello invites toocreate un **Application Web et/ou WebAPI**.

      * Hello **nom** Hello application décrit utilisateurs tooend de votre application.

      * Hello **URL de connexion** est l’URL de base hello de votre application.  Hello par défaut de l’URL de l’exemple de code hello est `https://localhost:8080`.

6. Une fois l’application enregistrée, Azure AD lui affecte un ID d’application unique. Vous avez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de la page de l’application hello.

7. À partir de hello **paramètres** -> **propriétés** page de votre application, la mise à jour de hello URI ID d’application. Hello **URI ID d’application** est un identificateur unique pour votre application. convention de Hello est toouse `https://<tenant-domain>/<app-name>`, par exemple : `https://contoso.onmicrosoft.com/my-first-aad-app`.

8. Créer un **clé** pour votre application à partir de hello **paramètres** page, puis le copier quelque part. Vous en aurez besoin rapidement.

## <a name="step-3-download-nodejs-for-your-platform"></a>Étape 3 : téléchargement de Node.js pour votre plateforme
toosuccessfully utiliser cet exemple, vous devez disposer d’une installation active de Node.js.

Installez Node.js à partir de l’adresse suivante : [http://nodejs.org](http://nodejs.org).

## <a name="step-4-install-mongodb-on-your-platform"></a>Étape 4 : installation de MongoDB sur votre plateforme
toosuccessfully utiliser cet exemple, vous devez disposer d’une installation active de MongoDB. Vous utilisez MongoDB toomake hello API REST persistant entre les instances de serveur.

Installez MongoDB à partir de l’adresse suivante : [http://mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Cette procédure pas à pas suppose que vous utilisez points de terminaison hello par défaut installation et le serveur pour MongoDB, qui au moment de la rédaction de hello est mongodb://localhost.
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a>Étape 5 : Installer les modules de Restify hello dans votre API web
Nous utilisons Restify toobuild notre API REST. Restify est une infrastructure d’application Node.js minimale et flexible qui est dérivée d’Express. Elle inclut un ensemble complet de fonctionnalités de création API REST sur Connect.

### <a name="install-restify"></a>Installation de Restify
1. À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** active. Si hello **organisation** répertoire n’existe pas, créez-le.

        `cd azuread - or- mkdir azuread; cd azuread`

2. Tapez hello de commande suivante :

    `npm install restify`

    Cette commande permet d’installer Restify.

#### <a name="did-you-get-an-error"></a>Une erreur est-elle survenue ?
Lorsque vous utilisez NPM sur certains systèmes d’exploitation, vous pouvez obtenir le message d’erreur suivant : **Error: EPERM, chmod '/usr/local/bin/..'** et une suggestion que vous essayez de compte de hello en cours d’exécution en tant qu’administrateur. Si cela se produit, utilisez toorun de commande hello sudo NPM à un niveau de privilège supérieur.

#### <a name="did-you-get-an-error-regarding-dtrace"></a>Une erreur relative à DTRACE est-elle survenue ?
Lors de l’installation de Restify, vous risquez de voir une erreur comme celle-ci :

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

sortie Hello de cette commande doit ressembler similaire toohello suivant de sortie :

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


## <a name="step-6-install-passportjs-in-your-web-api"></a>Étape 6 : installation de Passport.js dans votre API web
[Passport](http://passportjs.org/) est un intergiciel d’authentification pour Node.js. Flexible et modulaire, Passport peut être supprimé de manière transparente dans tooany rapides ou Restify d’application web. Une gamme complète de stratégies prend en charge l’authentification avec un nom d’utilisateur et un mot de passe, Facebook, Twitter et bien d’autres.

Nous avons développé une stratégie pour Azure Active Directory. Nous installer ce module et que vous ajoutez ensuite la stratégie d’Azure Active Directory hello plug-in.

1. À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** active.

2. tooinstall passport.js, entrez hello de commande suivante :

    `npm install passport`

    sortie de Hello de commande hello doit ressembler similaire toohello suivantes :

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a>Étape 7 : Ajouter Passport-Azure-AD tooyour web API
Ensuite, nous ajoutons stratégie de hello OAuth à l’aide de `passport-azure-ad`, un ensemble de stratégies qui se connectent tooPassport d’Azure Active Directory. Nous utilisons cette stratégie pour les jetons du porteur dans cet exemple d’API REST.

> [!NOTE]
> Bien qu’OAuth2 fournisse une infrastructure dans laquelle tout type de jeton connu peut être émis, seuls certains types de jeton sont couramment utilisés. Jetons de support sont des jetons de hello couramment utilisé pour protéger les points de terminaison. Ils sont type hello plus largement émis de jeton dans OAuth2. De nombreuses implémentations supposent que les jetons de porteur hello seul type de jetons émis.
>
>

À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** active.

Tapez ce qui suit hello commande tooinstall hello Passport.js `passport-azure-ad module`:

`npm install passport-azure-ad`

sortie de Hello de commande hello doit ressembler similaire toohello suivant de sortie :


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a>Étape 8 : Ajouter MongoDB modules tooyour web API
Nous utilisons MongoDB comme magasin de données. Pour cette raison, nous devons tooinstall hello est largement utilisé plug-in appelée Mongoose toomanage les modèles et les schémas. Nous devons également le pilote de base de données tooinstall hello pour MongoDB (qui est également appelée MongoDB).

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a>Étape 9 : installation de modules supplémentaires
Ensuite, nous installons hello restant modules requis.

1. À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.

    `cd azuread`

2. Entrez hello suivant de commandes tooinstall ces modules dans votre **node_modules** active :

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a>Étape 10 : création d’un server.js avec vos dépendances
fichier de server.js Hello fournit la plupart des fonctionnalités de hello pour notre serveur d’API web. Nous ajoutons la plupart de nos toothis du fichier de code. À des fins de production, nous vous recommandons de refactoriser fonctionnalité hello en fichiers plus petits, tels que les contrôleurs et itinéraires distincts. Dans cette démonstration, nous utilisons server.js pour cette fonctionnalité.

1. À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.

    `cd azuread`

2. Créer un `server.js` dans votre éditeur favori et puis ajoutez hello informations suivantes :

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. Enregistrez le fichier de hello. Nous allons retourner tooit peu de temps.

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a>Étape 11 : Créer un toostore de fichier de configuration de vos paramètres d’Azure AD
Ce fichier de code passe les paramètres de configuration hello depuis votre tooPassport.js portail Azure Active Directory. Vous avez créé ces valeurs de configuration lorsque vous avez ajouté le portail de hello web API toohello dans hello première partie de procédure pas à pas hello. Nous vous expliquons quels tooput dans les valeurs hello de ces paramètres après avoir copié les code hello.

1. À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.

    `cd azuread`

2. Créer un `config.js` dans votre éditeur favori et puis ajoutez hello informations suivantes :

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. Enregistrez le fichier de hello.

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a>Étape 12 : Ajouter le fichier de configuration valeurs tooyour server.js
Nous devons tooread de ces valeurs à partir du fichier .config hello que vous avez créé dans notre application. toodo, nous ajouter le fichier .config de hello en tant qu’une ressource requise dans notre application. Ensuite, nous avons défini hello global toomatch hello des variables dans le document de config.js hello.

1. À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.

    `cd azuread`

2. Ouvrez votre `server.js` dans votre éditeur favori et puis ajoutez hello informations suivantes :

    ```Javascript
    var config = require('./config');
    ```
3. Puis ajoutez une nouvelle section trop`server.js` avec hello suivant de code :

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. Enregistrez le fichier de hello.

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Étape 13 : Ajouter hello informations MongoDB modèle et de schéma à l’aide de Mongoose
Toute cette préparation va maintenant toostart rembourser que nous combiner ces trois fichiers dans un service de l’API REST.

Pour cette procédure pas à pas, nous utilisons MongoDB toostore notre tâches comme indiqué à l’étape 4.

Bonjour `config.js` que nous avons créé à l’étape 11, nous vous avons appelé notre base de données de fichiers `tasklist`, car il s’agit de ce que nous mettre à fin hello de notre **mogoose_auth_local** URL de connexion. Vous n’avez pas besoin toocreate cette base de données au préalable dans MongoDB. Au lieu de cela, MongoDB crée cela pour nous sur hello première exécution de notre application de serveur (en supposant que cette base de données hello n’existe pas déjà).

Maintenant que nous avons dit server de hello quelle base de données MongoDB nous aimerions toouse, nous devons toowrite certains modèles de code supplémentaire toocreate hello et un schéma pour les tâches de notre serveur.

### <a name="discussion-of-hello-model"></a>Présentation du modèle de hello
Notre modèle de schéma est simple. Vous le développez en fonction de vos besoins.

: Hello nom de personne hello toohello tâche est affectée. **Chaîne**.

TÂCHE : la tâche hello lui-même. **Chaîne**.

DATE : date de hello cette tâche hello est plein. **DATEHEURE**.

TERMINÉE : Si la tâche hello a été effectuée ou non. **BOOLÉEN**.

### <a name="creating-hello-schema-in-hello-code"></a>Création de schéma de hello dans du code hello
1. À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.

    `cd azuread`

2. Ouvrez votre `server.js` dans votre éditeur favori et puis ajoutez hello informations sous l’entrée de configuration hello suivantes :

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
    var TaskSchema = new Schema({
        owner: String,
        task: String,
        completed: Boolean,
        date: Date
    });

    // Use hello schema tooregister a model.
    mongoose.model('Task', TaskSchema);
    var Task = mongoose.model('Task');
    ```
Comme vous pouvez le voir à partir du code hello, nous créons notre schéma tout d’abord. Nous créons un objet de modèle que nous utilisons toostore nos données tout au long de hello le code quand nous définissons notre **itinéraires**.

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a>Étape 14 : ajout de nos itinéraires pour notre serveur de tâche de l’API REST
Maintenant que nous avons un toowork de modèle de base de données avec, vous allez ajouter des itinéraires hello nous sommes allons utiliser pour le serveur d’API REST.

### <a name="about-routes-in-restify"></a>À propos des itinéraires dans Restify
Fonctionnement des gammes Restify hello même façon qu’ils Bonjour Express empilent. Vous définissez des itinéraires à l’aide de hello URI que vous attendez hello client applications toocall. En général, vous définissez vos itinéraires dans un fichier distinct. Nous concerne, nous plaçons notre itinéraires dans le fichier de server.js hello. Nous vous recommandons de factoriser ces itinéraires dans leur propre fichier s’ils sont destinés à la production.

Un exemple de modèle d’un itinéraire Restify se présente comme suit :

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


Il s’agit de modèle hello à son niveau le plus simple. Restify (et Express) fournit des fonctionnalités bien plus approfondies, comme la définition de types d’application et la fourniture d’un routage complexe entre différents points de terminaison. Pour nos objectifs, nous conservons ces itinéraires simples.

### <a name="add-default-routes-tooour-server"></a>Ajouter le serveur de tooour d’itinéraires par défaut
Nous avons maintenant ajouter hello base CRUD itinéraires de créer, récupérer, mettre à jour et supprimer.

1. À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà :

    `cd azuread`

2. Ouvrez hello `server.js` dans votre éditeur favori et puis ajoutez hello suivant ci-dessous hello de base de données les entrées précédentes que vous avez apportées :

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.task = req.params.task;
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


// Delete a task by name.

function removeTask(req, res, next) {

    Task.remove({
        task: req.params.task,
        owner: owner
    }, function(err) {
        if (err) {
            req.log.warn(err,
                'removeTask: unable toodelete %s',
                req.params.task);
            next(err);
        } else {
            log.info('Deleted task:', req.params.task);
            res.send(204);
            next();
        }
    });
}

// Delete all tasks.

function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
}


// Get a specific task based on name.

function getTask(req, res, next) {

    log.info('getTask was called for: ', owner);
    Task.find({
        owner: owner
    }, function(err, data) {
        if (err) {
            req.log.warn(err, 'get: unable tooread %s', owner);
            next(err);
            return;
        }

        res.json(data);
    });

    return next();
}

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a>Ajouter la gestion des erreurs dans nos API
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a>Étape 15 : création de votre serveur
Nous avons défini notre base de données et nos itinéraires sont en place. Hello dernière chose toodo est ajouter l’instance de serveur hello qui gère les appels.

Restify (et Express), vous pouvez effectuer un grand nombre de personnalisation pour un serveur d’API REST, mais à nouveau, nous allons le programme d’installation toouse hello plus simple pour nos besoins.

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a>Étape 16 : Ajouter le serveur de toohello hello itinéraires (sans authentification pour l’instant)
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler.
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a>Étape 17 : Exécuter un serveur hello (avant d’ajouter la prise en charge OAuth)
Testez votre serveur avant d’ajouter l’authentification.

tootest de façon plus simple de Hello votre serveur est à l’aide de curl dans une ligne de commande. Avant cela, nous avons besoin d’un utilitaire qui permet de sortie tooparse au format JSON.

1. Installez hello suivant outil JSON (tous les hello exemple suivant permet d’utiliser cet outil) :

    `$npm install -g jsontool`

    Cette commande installe outil JSON hello globalement. Maintenant que nous avons accompli qui, nous allons lire avec un serveur de hello :

2. Vérifiez tout d’abord que votre instance mongoDB est en cours d’exécution :

    `$sudo mongod`

3. Ensuite, basculez de toohello et démarrer curling :

    `$ cd azuread``$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4. Nous pouvons à présent ajouter une tâche de la manière suivante :

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    réponse de Hello doit être :

        ```Shell
        HTTP/1.1 201 Created
        Connection: close
        Access-Control-Allow-Origin: *
        Access-Control-Allow-Headers: X-Requested-With
        Content-Type: application/x-www-form-urlencoded
        Content-Length: 5
        Date: Tue, 04 Feb 2014 01:02:26 GMT
        Hello
        ```
    Et nous pouvons répertorier des tâches pour Brandon de cette manière :

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Si tout cela fonctionne, nous sommes le serveur d’API REST toohello tooadd prêt OAuth.

Vous avez un serveur d’API REST avec MongoDB !

## <a name="step-18-add-authentication-tooour-rest-api-server"></a>Étape 18 : Ajouter le serveur d’authentification tooour API REST
Maintenant que nous disposons d’une API REST en cours d’exécution, commençons à l’utiliser avec Azure AD.

À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Utilisez hello OIDCBearerStrategy qui est inclus avec passport-azure-ad
Jusqu’à présent, nous avons créé un serveur REST TODO standard ne disposant d’aucune autorisation. Nous allons commencer à tout rassembler.

1. Tout d’abord, nous devons tooindicate que nous souhaitons toouse Passport. Placez cela juste après la configuration de l’autre serveur :

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > Lorsque vous écrivez API, nous vous recommandons de toujours lier hello toosomething de données unique à partir du jeton hello qui hello utilisateur ne peut pas usurper l’identité. Lorsque ce serveur stocke des éléments de tâche, il les stocke en fonction de l’ID d’objet hello d’utilisateur hello dans le jeton hello (appelé via token.oid), que nous avons dans le champ « propriétaire » de hello. Cela permet de s’assurer que seul cet utilisateur peut accéder à ses éléments TODO. Il n’aucune exposition Bonjour API de « propriétaire », un utilisateur externe peut demander hello TODOs autres même s’ils sont authentifiés.                    

2. Suivant nous allons utiliser la stratégie de support hello fourni avec `passport-azure-ad`. Recherchez le code hello pour le moment et nous expliquerons rest de hello peu de temps. Placez ceci après ce que vous avez collé ci-dessus :

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
    **/

    var findById = function(id, fn) {
        for (var i = 0, len = users.length; i < len; i++) {
            var user = users[i];
            if (user.sub === id) {
                log.info('Found user: ', user);
                return fn(null, user);
            }
        }
        return fn(null, null);
    };


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

Passport utilise un modèle semblable pour toutes ses stratégies (Twitter, Facebook, etc.), que respectent tous les enregistreurs de stratégie. Stratégie de hello, vous constatez que nous transmettons une fonction qui a un jeton et un terminé en tant que paramètres de hello. stratégie de Hello est fourni dans toous une fois qu’il effectue son travail. Une fois que c’est le cas nous stockons les utilisateur hello et jeton de hello dissimulation donc nous ne devons tooask pour celle-ci à nouveau.

> [!IMPORTANT]
> code de précédent Hello prend tout utilisateur qui se produit tooauthenticate tooour server. C’est ce qu’on appelle l’enregistrement automatique. Dans les serveurs de production, nous vous recommandons de faire passer toute personne qui essaie de se connecter par un processus d’inscription de votre choix. Il s’agit généralement de modèle hello que vous voyez dans les applications consommateur, ce qui vous permettent tooregister avec Facebook, mais vous demander de toofill des informations supplémentaires. Si ce n’était pas un programme de ligne de commande, nous avons extrait par courrier électronique hello à partir de l’objet du jeton hello qui est retourné et demandé toofill d’utilisateur hello des informations supplémentaires. Comme il s’agit d’un serveur de test, nous avons simplement ajouter toohello base de données.
>
>

### <a name="protect-some-endpoints"></a>Protéger certains points de terminaison
Protéger les points de terminaison en spécifiant hello `passport.authenticate()` appel avec le protocole de hello que vous souhaitez toouse.

toomake notre code de serveur faire quelque chose plus intéressant, nous allons modifier un itinéraire hello.

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a>Étape 19 : ré-exécution de votre application serveur et contrôle du rejet
Nous allons utiliser `curl` toosee à nouveau si vous disposez à présent OAuth2 protection par rapport à ses points de terminaison. Nous faisons ce contrôle avant d’exécuter l’un de nos Kits de développement logiciel (SDK) clients sur ce point de terminaison. Hello en-têtes retournés doivent être suffisamment tootell nous si nous allons vers le bas du chemin d’accès correct de hello.

1. Vérifiez tout d’abord que votre instance mongoDB est en cours d’exécution :

    `$sudo mongod`

2. Ensuite, basculez de toohello et former une boucle.

      `$ cd azuread``$ node server.js`

3. Essayez une commande basique, comme POST.

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

Une erreur 401 est réponse hello que vous cherchez ici. Cette réponse indique que cette couche de Passport hello tente de point de terminaison tooredirect toohello autorisé, qui est exactement ce que vous souhaitez.

## <a name="next-steps"></a>Étapes suivantes
Vous êtes allé aussi loin que possible avec ce serveur sans utiliser un client compatible OAuth2. Vous devez toogo via une procédure pas à pas supplémentaires.

Vous savez maintenant comment tooimplement une API REST à l’aide de Restify et OAuth2. Vous avez également plus que suffisante tookeep code développement de votre service et à l’apprentissage comment toobuild dans cet exemple.

Si vous êtes intéressé par les étapes suivantes hello dans votre parcours de la bibliothèque ADAL, Voici certains clients pris en charge ADAL, nous recommandons que vous conservez à travailler avec.

Cloner la machine de développement tooyour et le configurer comme décrit dans la procédure pas à pas hello.

[Bibliothèque ADAL pour iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[Bibliothèque ADAL pour Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
