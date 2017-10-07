---
title: aaaBuild une application web Node.js et MongoDB dans Azure | Documents Microsoft
description: "Découvrez comment tooget une application Node.js dans Azure, avec une connexion tooa Cosmos base de données de base de données avec une chaîne de connexion MongoDB."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a>Créer une application web Node.js et MongoDB dans Azure

Azure Web Apps fournit un service d’hébergement hautement évolutif et appliquant des mises à jour correctives automatiquement. Ce didacticiel montre comment toocreate un Node.js web application dans Azure et le connecter tooa MongoDB base de données. Lorsque vous aurez terminé, vous disposerez d’une application MEAN (MongoDB, Express, AngularJS et Node.js) exécutée sous [Azure App Service](app-service-web-overview.md). Par souci de simplicité, exemple d’application hello utilise hello [framework de web MEAN.js](http://meanjs.org/).

![Application MEAN.js exécutée dans Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Ce que vous allez apprendre :

> [!div class="checklist"]
> * Créer une base de données MongoDB dans Azure
> * Se connecter à un tooMongoDB d’application Node.js
> * Déployer hello application tooAzure
> * Mettre à jour le modèle de données hello et redéployer l’application hello
> * Diffusion des journaux de diagnostic à partir d’Azure
> * Gérer l’application hello Bonjour portail Azure

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel :

1. [Installez Git](https://git-scm.com/)
1. [Installez Node.js et NPM](https://nodejs.org/)
1. [Installer Gulp.js](http://gulpjs.com/) (requis par [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))
1. [Installez et exécutez MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-mongodb"></a>Tester la base de données MongoDB locale

Fenêtre de terminal ouverte hello et `cd` toohello `bin` répertoire de votre installation MongoDB. Vous pouvez utiliser cette fenêtre de terminal de toorun toutes les commandes hello dans ce didacticiel.

Exécutez `mongo` sur le serveur de MongoDB local hello terminal tooconnect tooyour.

```bash
mongo
```

Si la connexion est établie, cela signifie que votre base de données MongoDB est déjà en cours d’exécution. Dans le cas contraire, assurez-vous que votre base de données MongoDB locale est démarré en suivant les étapes de hello à [installer MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/). Souvent, MongoDB est installé, mais vous devez toujours toostart en réexécutant `mongod`. 

Lorsque vous avez terminé votre base de données MongoDB de test, tapez `Ctrl+C` Bonjour Terminal Server. 

## <a name="create-local-nodejs-app"></a>Créer une application Node.js locale

Dans cette étape, vous définir un projet local Node.js hello.

### <a name="clone-hello-sample-application"></a>Exemple d’application hello de cloner

Dans la fenêtre de terminal hello, `cd` répertoire de travail tooa.  

Exécutez hello suivant le dépôt d’exemples de commande tooclone hello. 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

Ce dépôt d’exemples contient une copie de hello [MEAN.js référentiel](https://github.com/meanjs/mean). Il est modifié toorun sur le Service d’application (pour plus d’informations, consultez le référentiel de MEAN.js hello [fichier Lisez-moi](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).

### <a name="run-hello-application"></a>Exécutez l’application hello

Exécutez hello suivant des packages de commandes tooinstall hello requis et démarrer l’application hello.

```bash
cd meanjs
npm install
npm start
```

Lors de l’application hello est entièrement chargée, vous voyez quelque chose de similaire toohello message suivant :

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

Accédez toohttp://localhost:3000 dans un navigateur. Cliquez sur **s’inscrire** hello menu supérieur et créer un utilisateur de test. 

Hello MEAN.js exemple d’application stocke les données utilisateur dans la base de données hello. Si vous parvenez à la création d’un utilisateur et l’ouverture de session, votre application écrit les données toohello MongoDB base de données locale.

![MEAN.js se connecte correctement tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

Sélectionnez **administration > Gérer les Articles** tooadd certains articles.

Appuyez sur la touche Node.js à tout moment, toostop `Ctrl+C` Bonjour Terminal Server. 

## <a name="create-production-mongodb"></a>Créer une base de données MongoDB de production

Dans cette étape, vous allez créer une base de données MongoDB dans Azure. Lorsque votre application est déployée tooAzure, il utilise cette base de données du cloud.

Pour MongoDB, ce didacticiel utilise [Azure Cosmos DB](/azure/documentdb/). Cosmos DB prend en charge les connexions client MongoDB.

### <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Vous allez utiliser hello Azure CLI 2.0 toocreate hello ressources nécessaires toohost votre application dans Azure. Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Hello exemple suivant crée un groupe de ressources dans la région Europe de l’ouest hello.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

Hello d’utilisation [Liste emplacements az appservice](/cli/azure/appservice#list-locations) les emplacements disponibles toolist de commande CLI d’Azure. 

### <a name="create-a-cosmos-db-account"></a>Création d’un compte Cosmos DB

Créer un compte de base de données Cosmos avec hello [az cosmosdb créer](/cli/azure/cosmosdb#create) commande.

Bonjour suivant de commande, remplacez par un nom unique de la base de données Cosmos pour hello  *\<cosmosdb_name >* espace réservé. Ce nom est utilisé en tant que partie hello du point de terminaison de base de données Cosmos hello `https://<cosmosdb_name>.documents.azure.com/`, de sorte que le nom hello doit toobe unique dans tous les comptes de base de données Cosmos dans Azure. Hello nom doit contenir uniquement des lettres minuscules, des chiffres et des caractères de trait d’union (-) hello et doit être comprise entre 3 et 50 caractères.

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

Hello *--MongoDB kind* paramètre permet les connexions clientes MongoDB.

Lorsque hello Cosmos DB compte est créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-tooproduction-mongodb"></a>Connecter l’application tooproduction MongoDB

Dans cette étape, vous vous connectez votre MEAN.js application toohello Cosmos DB base de données exemple que vous venez de créer, à l’aide d’une chaîne de connexion MongoDB. 

### <a name="retrieve-hello-database-key"></a>Récupérer la clé de base de données hello

base de données de la base de données Cosmos tooconnect toohello, vous devez clé de base de données hello. Hello d’utilisation [liste clés az cosmosdb](/cli/azure/cosmosdb#list-keys) clé primaire de commande tooretrieve hello.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

Hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copiez la valeur hello `primaryMasterKey`. Vous avez besoin de ces informations dans l’étape suivante de hello.

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Configurer la chaîne de connexion hello dans votre application Node.js

Dans votre référentiel MEAN.js, ouvrez _config/env/production.js_.

Bonjour `db` d’objet, de mettre à jour la valeur hello `uri`:

* Remplacez hello deux  *\<cosmosdb_name >* des espaces réservés avec votre nom de base de données de base de données Cosmos.
* Remplacez hello  *\<primary_master_key >* espace réservé avec clé hello copiée à l’étape précédente de hello.

Hello de code suivant montre hello `db` objet :

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

Hello `ssl=true` option est requise car [Cosmos DB requiert SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 

Enregistrez vos modifications.

### <a name="test-hello-application-in-production-mode"></a>Tester l’application hello en mode de production 

Exécutez hello suivant des scripts de commande toominify et de groupe pour l’environnement de production hello. Ce processus génère des fichiers hello requis par l’environnement de production hello.

```bash
gulp prod
```

Exécution hello suivant de chaîne de connexion commande toouse hello vous avez configuré dans _config/env/production.js_.

```bash
NODE_ENV=production node server.js
```

`NODE_ENV=production`définit la variable d’environnement hello indiquant Node.js toorun dans l’environnement de production hello.  `node server.js`démarre hello serveur Node.js avec `server.js` racine du référentiel. Voici comment est chargée votre application Node.js dans Azure. 

Lors de l’application hello est chargée, vérifiez toomake qu’il fonctionne dans un environnement de production hello :

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

Accédez toohttp://localhost:8443 dans un navigateur. Cliquez sur **s’inscrire** hello menu supérieur et créer un utilisateur de test. Si vous êtes réussi de création d’un utilisateur et de l’ouverture de session, puis votre application est l’écriture de base de données toohello Cosmos DB dans Azure. 

Bonjour Terminal Server, arrêtez Node.js en tapant `Ctrl+C`. 

## <a name="deploy-app-tooazure"></a>Déployer l’application tooAzure

Dans cette étape, vous déployez votre tooAzure d’application connectée MongoDB de Node.js du Service d’applications.

### <a name="create-an-app-service-plan"></a>Créer un plan App Service

Créer un plan App Service avec hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hello exemple suivant crée un plan App Service nommé _myAppServicePlan_ à l’aide de hello **libre** niveau tarifaire :

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Lorsque hello plan App Service est créé, hello CLI d’Azure s’affiche des informations similaires toohello est l’exemple suivant :

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a>Créer une application web

Créer une application web Bonjour `myAppServicePlan` plan App Service avec hello [az webapp créer](/cli/azure/webapp#create) commande. 

fournit les application Hello web vous un hébergement toodeploy votre code et de l’espace fournit une URL pour vous tooview hello déployé l’application. Utilisez l’application web toocreate hello. 

Bonjour suivant de commande, remplacez hello  *\<nom_application >* espace réservé avec un nom d’application unique. Ce nom est utilisé en tant que partie hello d’URL par défaut de hello pour l’application web de hello, le nom hello doit toobe unique entre toutes les applications dans Azure App Service. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Lors de l’application hello web a été créée, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant : 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a>Configurer une variable d’environnement

Plus haut dans hello didacticiel, vous codé en dur hello de base de données chaîne de connexion dans _config/env/production.js_. En fonction de la meilleure pratique de sécurité, vous souhaitez tookeep les données sensibles en dehors de votre référentiel Git. Pour l’application en cours d’exécution dans Azure, vous utiliserez plutôt une variable d’environnement.

Dans le Service d’application, vous définissez les variables d’environnement _paramètres de l’application_ à l’aide de hello [az webapp configuration appsettings mettre à jour](/cli/azure/webapp/config/appsettings#update) commande. 

Hello exemple suivant configure un `MONGODB_URI` paramètre d’application dans votre application web Azure. Remplacez hello  *\<nom_application >*,  *\<cosmosdb_name >*, et  *\<primary_master_key >* des espaces réservés.

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

Dans le code Node.js, vous accédez à ce paramètre d’application avec `process.env.MONGODB_URI`, comme vous accéderiez à n’importe quelle variable d’environnement. 

Annuler maintenant, votre too_config/env/production.js_ modifications par hello de commande suivante :

```bash
git checkout -- .
```

Ouvrez à nouveau _config/env/production.js_. Notez cette application de MEAN.js hello par défaut est déjà configuré toouse hello `MONGODB_URI` variable d’environnement que vous avez créé.

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a>Configurer le déploiement Git local 

Hello d’utilisation [az webapp utilisateur de déploiement défini](/cli/azure/webapp/deployment/user#set) toocreate les informations d’identification pour le déploiement de la commande.

Vous pouvez déployer votre application de tooAzure du Service d’applications de différentes manières, notamment FTP, Git local, GitHub, Visual Studio Team Services et BitBucket. Pour FTP et Git local, il est nécessaire toohave un utilisateur du déploiement configuré sur hello server tooauthenticate votre déploiement. Cet utilisateur de déploiement se situe au niveau des comptes et est différent de votre compte d’abonnement Azure. Vous ne devez tooconfigure cet utilisateur de déploiement une fois.

Bonjour suivant de commande, remplacez  *\<nom d’utilisateur >* et  *\<mot de passe >* avec un nouveau nom d’utilisateur et un mot de passe. nom d’utilisateur Hello doit être unique. Hello mot de passe doit comporter au moins huit caractères, avec deux hello suivant trois éléments : des lettres, des chiffres, des symboles. Si vous obtenez un ` 'Conflict'. Details: 409` erreur, le nom d’utilisateur de modification hello. Si vous obtenez une erreur ` 'Bad Request'. Details: 400`, utilisez un mot de passe plus fort.

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

Enregistrement hello nom utilisateur et mot de passe pour une utilisation dans les étapes ultérieures lorsque vous déployez l’application hello.

Hello d’utilisation [source liée à un déploiement de webapp dans az-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) commande tooconfigure Git accès toohello Azure l’application web locale. 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

Lorsque l’utilisateur du déploiement hello est configuré, hello CLI d’Azure affiche hello les URL de déploiement pour votre application web Azure Bonjour suivant le format :

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

Copiez hello la sortie à partir de Terminal Server hello, car il sera utilisé à l’étape suivante de hello. 

### <a name="push-tooazure-from-git"></a>TooAzure par émission de données à partir de Git

Ajouter un référentiel Git Azure tooyour à distance. 

```bash
git remote add azure <paste_copied_url_here> 
```

Push toohello Azure toodeploy à distance de votre application Node.js. Vous demandera de mot de passe hello fourni précédemment dans le cadre de la création de l’utilisateur du déploiement hello hello. 

```bash
git push azure master
```

Au cours du déploiement, Azure App Service communique sa progression avec Git.

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

Vous pouvez remarquer que le processus de déploiement hello s’exécute [Gulp](http://gulpjs.com/) après `npm install`. Service de l’application ne s’exécute pas Gulp ou Grunt tâches durant le déploiement, donc ce référentiel exemple a deux autres fichiers dans son tooenable du répertoire racine qu’il : 

- _.Deployment_ -ce fichier indique au Service d’applications toorun `bash deploy.sh` en tant que script de déploiement personnalisé hello.
- _Deploy.sh_ -hello du script de déploiement personnalisé. Si vous passez en revue le fichier de hello, vous verrez qu’il s’exécute `gulp prod` après `npm install` et `bower install`. 

Vous pouvez utiliser cette approche tooadd tout tooyour étape déploiement Git. Notez que si vous redémarrez votre application web Azure à tout moment, App Service ne réexécute pas ces tâches d’automatisation.

### <a name="browse-toohello-azure-web-app"></a>Parcourir toohello Azure web app 

Parcourir l’application web toohello déployé à l’aide de votre navigateur web. 

```bash 
http://<app_name>.azurewebsites.net 
``` 

Cliquez sur **s’inscrire** dans hello menu supérieur et créez un utilisateur fictif. 

Si vous êtes réussie et l’application hello se connecte automatiquement toohello créé l’utilisateur, puis votre application MEAN.js dans Azure a base de données de connectivité toohello (DB Cosmos) de MongoDB. 

![Application MEAN.js exécutée dans Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Sélectionnez **administration > Gérer les Articles** tooadd certains articles. 

**Félicitations !** Vous exécutez une application Node.js orientée données dans Azure App Service.

## <a name="update-data-model-and-redeploy"></a>Mettre à jour le modèle de données et redéployer

Dans cette étape, vous modifiez hello `article` de modèle de données et publier votre tooAzure de modification.

### <a name="update-hello-data-model"></a>Mettre à jour le modèle de données hello

Ouvrez _modules/articles/server/models/article.server.model.js_.

Dans `ArticleSchema`, ajoutez un type `String` appelé `comment`. Lorsque vous aurez terminé, votre code de schéma doit ressembler à ceci :

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-hello-articles-code"></a>Mettre à jour le code d’articles hello

Mettre à jour des autres hello votre `articles` toouse de code `comment`.

Il existe cinq fichiers toomodify : serveur de contrôleur de hello et vues du client hello quatre. 

Ouvrez _modules/articles/server/controllers/articles.server.controller.js_.

Bonjour `update` de fonction, ajouter une affectation pour `article.comment`. Hello de code suivant montre hello terminée `update` fonction :

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

Ouvrez _modules/articles/client/views/view-article.client.view.html_.

Juste au-dessus de fermeture de hello `</section>` , ajoutez hello suivant ligne toodisplay `comment` ainsi que d’autres données de l’article hello hello :

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

Ouvrez _modules/articles/client/views/list-articles.client.view.html_.

Juste au-dessus de fermeture de hello `</a>` , ajoutez hello suivant ligne toodisplay `comment` ainsi que d’autres données de l’article hello hello :

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

Ouvrez _modules/articles/client/views/admin/list-articles.client.view.html_.

À l’intérieur hello `<div class="list-group">` élément et juste au-dessus de fermeture de hello `</a>` , ajoutez hello suivant ligne toodisplay `comment` ainsi que d’autres données de l’article hello hello :

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

Ouvrez _modules/articles/client/views/admin/form-article.client.view.html_.

Recherche hello `<div class="form-group">` élément qui contient le bouton d’envoi hello, qui ressemble à ceci :

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

Juste au-dessus de cette balise, ajoutez un autre `<div class="form-group">` élément permettant aux utilisateurs de modifier hello `comment` champ. Votre nouvel élément doit avoir l’aspect suivant :

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a>Tester vos modifications en local

Enregistrez toutes vos modifications.

Testez de nouveau vos modifications en mode de production.

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> N’oubliez pas que votre _config/env/production.js_ a été annulée et hello `MONGODB_URI` variable d’environnement est définie uniquement dans votre application web Azure et non sur votre ordinateur local. Si vous examinez le fichier de configuration hello, vous trouvez que hello configuration de production par défaut est toouse une base de données MongoDB local. Cela vous évite de toucher aux données de production lorsque vous testez vos changements de code en local.

Accédez trop`http://localhost:8443` dans un navigateur et assurez-vous que vous êtes connecté.

Sélectionnez **administration > Gérer les Articles**, puis ajouter un article en sélectionnant hello  **+**  bouton.

Vous consultez hello nouvelle `Comment` textbox maintenant.

![TooArticles de champ de commentaire ajouté](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

Bonjour Terminal Server, arrêtez Node.js en tapant `Ctrl+C`. 

### <a name="publish-changes-tooazure"></a>Publier les modifications tooAzure

Valider les modifications apportées dans Git, puis push tooAzure de modifications de code hello.

```bash
git commit -am "added article comment"
git push azure master
```

Une fois hello `git push` terminée, accédez tooyour Azure web app et tester les nouvelles fonctionnalités de hello.

![Les modifications de modèle et de la base de données publiées tooAzure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

Si vous avez ajouté des articles précédemment, vous pouvez toujours les visualiser. Les données existantes dans votre Cosmos DB ne sont pas perdues. En outre, votre schéma de données pour les mises à jour toohello et conserve vos données existantes intact.

## <a name="stream-diagnostic-logs"></a>Diffuser les journaux de diagnostic 

Pendant l’exécution de votre application Node.js dans Azure App Service, vous pouvez obtenir hello console journaux dirigée tooyour Terminal Server. De cette façon, vous pouvez obtenir hello des messages de diagnostic mêmes toohelp vous déboguez des erreurs d’application.

journal toostart de diffusion en continu, utilisez hello [la fin du journal de az webapp](/cli/azure/webapp/log#tail) commande.

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

Une fois que le journal de diffusion en continu a démarré, actualisez votre application web Azure dans hello navigateur tooget certains types de trafic web. Vous voyez maintenant les journaux de la console dirigés tooyour Terminal Server.

Pour arrêter la diffusion de journaux à tout moment, tapez `Ctrl+C`. 

## <a name="manage-your-azure-web-app"></a>Gérer votre application web Azure

Accédez toohello [portail Azure](https://portal.azure.com) toosee vous avez créé l’application web hello.

Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.

![Application de navigation du portail tooAzure web](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

Par défaut, le portail de hello affiche de votre application web **vue d’ensemble** page. Cette page propose un aperçu de votre application. Ici, vous pouvez également effectuer des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple). onglets Hello sur le côté gauche de hello de page de hello affichent les pages de configuration différents hello que vous pouvez l’ouvrir.

![Page App Service du Portail Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>Étapes suivantes

Vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer une base de données MongoDB dans Azure
> * Se connecter à un tooMongoDB d’application Node.js
> * Déployer hello application tooAzure
> * Mettre à jour le modèle de données hello et redéployer l’application hello
> * Journaux des flux de données à partir d’Azure tooyour Terminal Server
> * Gérer l’application hello Bonjour portail Azure

Avancer toolearn de didacticiel suivant toohello tooyour l’application web de noms toomap DNS personnalisé.

> [!div class="nextstepaction"] 
> [Mapper une tooAzure de nom DNS personnalisé existant Web Apps](app-service-web-tutorial-custom-domain.md)
