---
title: "aaaDeploy un tooAzure d’application Sails.js web du Service d’applications | Documents Microsoft"
description: "Découvrez comment toodeploy une application Node.js Azure App Service. Ce didacticiel vous montre comment toodeploy un Sails.js web app."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a>Déployer un ordinateur Sails.js web application tooAzure du Service d’applications
Ce didacticiel vous montre comment toodeploy un tooAzure d’application Sails.js du Service d’applications. Dans le processus de hello, vous pouvez en déduire des connaissances générales sur la façon de tooconfigure votre toorun d’application Node.js dans le Service d’applications.

Vous y gagnerez des compétences utiles telles que :

* la configuration d’une application Sails.js s’exécutant dans App Service ;
* Déployer une application de tooApp Service à partir de la ligne de commande hello.
* Stdout et stderr lecture consigne tootroubleshoot tout problème de déploiement.
* le stockage de variables d’environnement en dehors du contrôle de code source ;
* l’accès aux variables d’environnement Azure à partir de votre application ;
* Connecter la base de données tooa (MongoDB).

Vous devriez avec une bonne connaissance de Sails.js. Ce didacticiel n’est pas prévue toohelp des problèmes liés toorunning Sail.js en général.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello
- [Azure CLI 2.0](app-service-web-nodejs-sails.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello

## <a name="prerequisites"></a>Composants requis
* [Node.JS](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [Azure CLI 2.0](/cli/azure/install-az-cli2)
* Un compte Microsoft Azure Si vous n’avez pas de compte, vous pouvez [vous inscrire pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> Vous pouvez [essayer App Service](https://azure.microsoft.com/try/app-service/) sans compte Azure. Créer une application de démarrage et de le manipuler pour les horaires de tooan--aucune carte de crédit requis, aucune des engagements.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>Étape 1 : Créer et configurer une application Sails.js localement
Commencez par créer rapidement une application Sails.js par défaut dans votre environnement de développement en procédant comme suit :

1. Terminal de ligne de commande de hello ouverte de votre choix et `CD` répertoire de travail tooa.
2. Créez une application Sails.js et exécutez-la :

        sails new <app_name>
        cd <app_name>
        sails lift

    Assurez-vous que vous pouvez parcourir la page d’accueil par défaut toohello à http://localhost:1377.

1. Ensuite, activez la journalisation pour Azure. Dans le répertoire racine, créez un fichier appelé `iisnode.yml` et ajoutez hello deux lignes suivantes :

        loggingEnabled: true
        logDirectory: iisnode

    La journalisation est maintenant activée pour hello [iisnode](https://github.com/tjanczuk/iisnode) serveur qu’Azure App Service utilisé par les applications Node.js toorun. 
    Pour plus d’informations sur le fonctionnement, consultez [comment toodebug un Node.js web application dans Azure App Service](web-sites-nodejs-debug.md).

2. Ensuite, configurez les variables d’environnement Azure hello Sails.js application toouse. Ouvrez config/env/production.js tooconfigure votre environnement de production, puis définissez `port` et `hookTimeout`:

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    La description de ces paramètres de configuration est disponible dans la [documentation Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).

4. Ensuite, coder en dur hello Node.js version de toouse. Dans package.json, ajoutez suivant de hello `engines` propriété tooset hello Node.js version tooone que nous voulons.

        "engines": {
            "node": "6.9.1"
        },

5. Enfin, initialisez un référentiel Git et validez vos fichiers. Dans l’hello racine de l’application (où est package.json), exécutez hello suivant de commandes Git :

        git init
        git add .
        git commit -m "<your commit message>"

Votre code est toobe prêt déployée. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>Étape 2 : Créer une application Azure et déployer Sails.js

Ensuite, créez des hello ressource du Service de l’application dans Azure et déployer votre tooit d’application Sails.js.

1. Ouvrez une session tooAzure comme suit :

        az login

    Suivez hello toocontinue invite hello compte de connexion dans un navigateur avec un compte Microsoft qui a votre abonnement Azure.

3. Définir l’utilisateur du déploiement hello pour le Service d’applications. Vous déploierez le code ultérieurement à l’aide de ces informations d’identification.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. Créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) avec un nom. Pour ce didacticiel Node.js, vous n’ayez pas besoin tooknow qu’il est.

        az group create --location "<location>" --name my-sailsjs-app-group

    toosee quel possible les valeurs que vous pouvez utiliser pour `<location>`, utilisez hello `az appservice list-locations` commande CLI.

3. Créez un [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) « FREE » avec un nom. Pour ce didacticiel node.js, sachez que vous ne serez pas facturé pour les Web Apps utilisées dans le cadre de cette offre.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. Créez une application web avec un nom unique dans `<app_name>`.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>Étape 3 : Configurer et déployer votre application Sails.js

1. Configurer un déploiement Git local pour votre application web avec hello de commande suivante :

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    Vous obtenez une sortie JSON comme celui-ci, ce qui signifie que hello le référentiel Git distant est configuré :

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. Ajouter des URL de hello Bonjour JSON comme un Git à distance pour votre référentiel local (appelé `azure` par souci de simplicité).

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. Déployer votre toohello du code exemple `azure` Git remote. Lorsque vous y êtes invité, utiliser des informations d’identification du déploiement hello configuré précédemment.

        git push azure master

7. Pour finir, lancez votre application Azure en temps réel dans le navigateur de hello :

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    Vous devez maintenant voir hello même Sails.js page d’accueil.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>Résoudre les problèmes de votre déploiement
Si votre application Sails.js échoue pour une raison quelconque dans le Service d’applications, \Journaux hello stderr toohelp de le résoudre.
Pour plus d’informations, consultez [comment toodebug un Node.js web application dans Azure App Service](web-sites-nodejs-debug.md).
Si l’application hello a démarré avec succès, journal de stdout hello doit afficher message de type hello familier :

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

Vous pouvez contrôler la granularité des journaux de stdout hello Bonjour [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) fichier.

## <a name="connect-tooa-database-in-azure"></a>Se connecter tooa de base de données dans Azure
base de données tooconnect tooa dans Azure, vous créez des hello de base de données de votre choix dans Azure, telles que la base de données SQL Azure, MySQL, MongoDB, le Cache Azure (Redis), etc. et utilisez hello correspondant [adaptateur de magasin de données](https://github.com/balderdashy/sails#compatibility) tooconnect tooit. Hello étapes décrites dans cette section vous montrent comment tooMongoDB tooconnect à l’aide un [base de données Azure Cosmos](../documentdb/documentdb-protocol-mongodb.md) base de données, ce qui peut prendre en charge les connexions de client MongoDB.

1. [Créez un compte Cosmos DB prenant en charge le protocole MongoDB](../documentdb/documentdb-create-mongodb-account.md).
2. [Créez une collection et une base de données Cosmos DB](../documentdb/documentdb-create-collection.md). nom Hello de collection de hello n’a pas d’importance, mais vous devez nom hello de base de données hello lorsque vous vous connectez à partir de Sails.js.
3. [Rechercher les informations de connexion de hello pour votre base de données de la base de données Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).
2. À partir de votre terminal de ligne de commande, installez l’adaptateur MongoDB hello :

        npm install sails-mongo --save

3. Ouvrez config/connections.js et ajoutez les hello suivant connexion objet toohello liste :

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > Hello `ssl: true` option est importante car [Cosmos DB exige](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 
    >
    >

4. Pour chaque variable d’environnement (`process.env.*`), vous devez tooset dans le Service d’applications. toodo, hello exécution suivant des commandes à partir de votre terminal. Utilisez les informations de connexion de hello pour votre base de données Cosmos.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    Activer vos paramètres dans les paramètres de l’application Azure conserve les données sensibles hors de votre contrôle de source (Git). Ensuite, vous allez configurer votre développement environnement toouse hello les mêmes informations de connexion.
5. Ouvrez config/local.js et ajoutez les hello connexions objet :

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    Cette configuration remplace les paramètres de hello dans votre fichier config/connections.js pour l’environnement local de hello. Ce fichier est exclu par .gitignore par défaut de hello dans votre projet, donc il n’est pas stocké dans Git. Maintenant, vous êtes en mesure de tooconnect tooyour Cosmos DB (MongoDB) base de données de votre application web Azure et de votre environnement de développement local.
6. Ouvrez config/env/production.js tooconfigure votre environnement de production et ajoutez hello suit `models` objet :

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Ouvrez config/env/development.js tooconfigure votre environnement de développement et ajoutez hello suit `models` objet :

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`vous permet d’utiliser toocreate de fonctionnalités de migration de base de données et mettre à jour facilement des collections de base de données ou des tables. Toutefois, `migrate: 'safe'` est utilisé pour votre environnement Azure (production), car Sails.js ne vous autorise pas toouse `migrate: 'alter'` dans un environnement de production (voir [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. À partir de hello terminal, [générer](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) un Sails.js [Géomètre API](http://sailsjs.org/documentation/concepts/blueprints) comme vous normalement, puis exécutez `sails lift` créer la base de données de hello Sails.js la migration de base de données. Par exemple :

         sails generate api mywidget
         sails lift

    Hello `mywidget` modèle généré par cette commande est vide, mais nous pouvons utiliser tooshow que nous disposons de connectivité de base de données.
    Lorsque vous exécutez `sails lift`, il crée des collections de manquant hello et tables pour hello modélise par votre application.
9. Accès aux API de plan hello vous venez de créer dans le navigateur de hello. Par exemple :

        http://localhost:1337/mywidget/create

    Hello API doit retourner tooyou arrière d’entrée hello créé dans la fenêtre de navigateur hello, ce qui signifie que votre collection est créée avec succès.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. Maintenant, push tooAzure de vos modifications et parcourir toomake d’application tooyour qu’il fonctionne toujours.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Accès aux API de plan hello de votre application web Azure. Par exemple :

         http://<appname>.azurewebsites.net/mywidget/create

     Si hello API retourne une autre nouvelle entrée, puis votre application web Azure communique avec une base de données tooyour Cosmos DB (MongoDB).

## <a name="more-resources"></a>Autres ressources
* [Prise en main des applications web Node.js dans Azure App Service](app-service-web-get-started-nodejs.md)
* [Utilisation de modules Node.js avec des applications Azure](../nodejs-use-node-modules-azure-apps.md)
