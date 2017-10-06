---
title: "aaaConnect un tooAzure d’application MongoDB Cosmos DB à l’aide de Node.js | Documents Microsoft"
description: "Découvrez comment tooconnect un tooAzure d’application existant Node.js MongoDB Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a>Azure Cosmos DB : migrer une application web MongoDB Node.js existante 

Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale. Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur. 

Ce démarrage rapide montre comment toouse existant [MongoDB](mongodb-introduction.md) application écrite en Node.js et le connecter à base de données de base de données Azure Cosmos tooyour, qui prend en charge les connexions clientes MongoDB. En d’autres termes, votre application Node.js sait uniquement qu’il se connecte à l’aide de MongoDB APIs de la base de données tooa. Il est transparent toohello application hello les données est stockée dans la base de données Azure Cosmos.

Lorsque vous aurez terminé, vous disposerez d’une MEAN (MongoDB, Express, AngularJS et Node.js) exécutée sous [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). 

![Application MEAN.js exécutée dans Azure App Service](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prerequisites"></a>Composants requis 
En outre tooAzure CLI, vous devez [Node.js](https://nodejs.org/) et [Git](http://www.git-scm.com/downloads) installé localement toorun `npm` et `git` commandes.

Vous devriez avoir une bonne connaissance de Node.js. Ce démarrage rapide n’est pas prévue toohelp vous avec le développement d’applications Node.js en général.

## <a name="clone-hello-sample-application"></a>Exemple d’application hello de cloner

Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.  

Exécutez hello suivant le dépôt d’exemples de commandes tooclone hello. Ce dépôt d’exemples contient la valeur par défaut hello [MEAN.js](http://meanjs.org/) application. 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a>Exécutez l’application hello

Installer des packages hello requis et démarrer l’application hello.

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Si vous utilisez une installation CLI d’Azure, connectez-vous tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran. Vous pouvez ignorer cette étape si vous utilisez hello Azure Cloud Shell.

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a>Ajouter le module de base de données Azure Cosmos hello

Si vous utilisez une CLI d’Azure installés, vérifiez toosee si hello `cosmosdb` composant est déjà installé, exécutez hello `az` commande. Si `cosmosdb` est hello la liste des commandes de base, continuer toohello prochaine commande. Vous pouvez ignorer cette étape si vous utilisez hello Azure Cloud Shell.

Si `cosmosdb` n’est pas en hello la liste des commandes de base, réinstallez [Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) avec hello [az groupe créer](/cli/azure/group#create). Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure comme les applications web, les bases de données et les comptes de stockage sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources dans la région Europe de l’ouest hello. Choisissez un nom unique pour le groupe de ressources hello.

Si vous utilisez un environnement de Cloud Azure, cliquez sur **essayer**, suivez toologin des invites à l’écran hello, puis copiez la commande hello dans l’invite de commandes hello.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a>Création d’un compte Azure Cosmos DB

Créer un compte de base de données Azure Cosmos avec hello [az cosmosdb créer](/cli/azure/cosmosdb#create) commande.

Bonjour suivant de commande, veuillez remplacer votre propre nom de compte de base de données Azure Cosmos unique dans lequel vous consultez hello `<cosmosdb-name>` espace réservé. Ce nom unique sera utilisé dans le cadre de votre point de terminaison de base de données Azure Cosmos (`https://<cosmosdb-name>.documents.azure.com/`), de sorte que le nom hello doit toobe unique dans tous les comptes de base de données Azure Cosmos dans Azure. 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

Hello `--kind MongoDB` paramètre permet les connexions clientes MongoDB.

Hello compte de base de données Azure Cosmos est créé, hello CLI d’Azure indique des informations similaires toohello est l’exemple suivant. 

> [!NOTE]
> Cet exemple utilise JSON comme format de sortie hello CLI d’Azure, qui est la valeur par défaut hello. toouse une autre sortie de format, consultez [formats pour les commandes de Azure CLI 2.0 de sortie](https://docs.microsoft.com/cli/azure/format-output-azure-cli).

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a>Se connecter à votre base de données toohello d’application Node.js

Dans cette étape, vous vous connectez votre MEAN.js application tooan base de données Azure Cosmos base de données exemple que vous venez de créer, à l’aide d’une chaîne de connexion MongoDB. 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Configurer la chaîne de connexion hello dans votre application Node.js

Dans votre référentiel MEAN.js, ouvrez `config/env/local-development.js`.

Remplacez le contenu de ce fichier hello hello suivant de code. Veillez tooalso remplacer hello deux `<cosmosdb-name>` des espaces réservés avec le nom de votre compte de base de données Azure Cosmos.

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a>Récupérer la clé de hello

Dans la base de données de base de données Azure Cosmos de commande tooconnect tooan, vous devez la clé de base de données hello. Hello d’utilisation [liste clés az cosmosdb](/cli/azure/cosmosdb#list-keys) clé primaire de commande tooretrieve hello.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

Hello CLI d’Azure génère des informations similaires toohello est l’exemple suivant. 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

Copiez la valeur hello `primaryMasterKey`. Coller sur hello `<primary_master_key>` dans `local-development.js`.

Enregistrez vos modifications.

### <a name="run-hello-application-again"></a>Relancez l’application hello.

Exécutez de nouveau `npm start`. 

```bash
npm start
```

Un message de console doit indiquer maintenant de que cet environnement de développement hello est en cours d’exécution. 

Accédez trop`http://localhost:3000` dans un navigateur. Cliquez sur **s’inscrire** dans toocreate supérieur de menu, puis réessayez de hello deux factice des utilisateurs. 

Hello MEAN.js exemple d’application stocke les données utilisateur dans la base de données hello. Si vous êtes réussie et MEAN.js se connecte automatiquement à hello créé l’utilisateur, puis l’utilisation de votre connexion de base de données Azure Cosmos. 

![MEAN.js se connecte correctement tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a>Afficher les données dans l’Explorateur de données

Les données stockées par une base de données Azure Cosmos soient tooview disponible, requête et exécution d’une logique métier sur Bonjour portail Azure.

tooview, interroger et manipuler les données d’utilisateur hello créées à l’étape précédente hello, connexion toohello [portail Azure](https://portal.azure.com) dans votre navigateur web.

Dans la zone de recherche supérieure hello, type de base de données Azure Cosmos. Lorsque le panneau de votre compte Cosmos DB s’ouvre, sélectionnez votre compte Cosmos DB. Bonjour barre de navigation gauche, cliquez sur Explorateur de données. Développez votre collection dans le volet de Collections hello, puis vous pouvez afficher des documents de hello dans la collection de hello, interroger des données hello et même créer et exécuter des procédures stockées, des déclencheurs et des UDF. 

![Explorateur de données Bonjour portail Azure](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a>Déployer hello Node.js application tooAzure

Dans cette étape, vous déployez votre tooAzure d’application connectée MongoDB de Node.js Cosmos DB.

Vous avez peut-être remarqué ce fichier de configuration hello que vous avez modifié précédemment est pour l’environnement de développement hello (`/config/env/local-development.js`). Lorsque vous déployez votre tooApp application Service, il s’exécute dans un environnement de production hello par défaut. Maintenant, vous devez toomake hello même modifier le fichier de configuration respectifs toohello.

Dans votre référentiel MEAN.js, ouvrez `config/env/production.js`.

Bonjour `db` d’objet, remplacez la valeur hello `uri` comme indiqué dans hello l’exemple suivant. Être vraiment tooreplace hello des espaces réservés comme avant.

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> Hello `ssl=true` option est importante car [base de données Azure Cosmos requiert SSL](connect-mongodb-account.md#connection-string-requirements). 
>
>

Bonjour terminal, valider toutes vos modifications dans Git. Vous pouvez copier les deux toorun commandes ensemble.

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :

1. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé. 
2. Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Ce guide de démarrage rapide, vous avez appris comment toocreate une base de données Azure Cosmos compte et créez une collection de MongoDB à l’aide de hello Explorateur de données. Vous pouvez désormais migrer votre tooAzure de données MongoDB Cosmos DB.  

> [!div class="nextstepaction"]
> [Importer des données MongoDB dans Azure Cosmos DB](mongodb-migrate.md)
