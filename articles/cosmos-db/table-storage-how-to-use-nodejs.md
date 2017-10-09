---
title: "aaaHow toouse stockage de Table Azure à partir de Node.js | Documents Microsoft"
description: "Stocker des données structurées dans le cloud hello avec le stockage Table Azure, un magasin de données NoSQL."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 21022491a9a21a5365628de93582ea3a325ed869
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a>Comment toouse stockage de Table Azure à partir de Node.js
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Vue d'ensemble
Cette rubrique montre comment les scénarios courants tooperform hello Table Azure à l’aide de service dans une application Node.js.

les exemples de code Hello dans cette rubrique supposent que vous disposez déjà d’une application Node.js. Pour plus d’informations sur la façon toocreate une application Node.js dans Azure, consultez une des rubriques suivantes :

* [Créer une application web Node.js dans Azure App Service](../app-service-web/app-service-web-get-started-nodejs.md)
* [Créer et déployer un tooAzure d’application web Node.js à l’aide de WebMatrix](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* [Créer et déployer un tooan d’application Node.js Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (à l’aide de Windows PowerShell)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a>Configurer votre tooaccess application Azure Storage
toouse stockage Azure, vous devez hello SDK de stockage Azure pour Node.js, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a>Utiliser le Gestionnaire de Package de nœud (NPM) tooinstall hello package
1. Utiliser une interface de ligne de commande tels que **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), puis accédez dossier toohello où vous avez créé votre application.
2. Type **npm installer le stockage azure** dans la fenêtre de commande hello. Sortie de commande hello est similaire toohello l’exemple suivant.

       azure-storage@0.5.0 node_modules\azure-storage
       +-- extend@1.2.1
       +-- xmlbuilder@0.4.3
       +-- mime@1.2.11
       +-- node-uuid@1.4.3
       +-- validator@3.22.2
       +-- underscore@1.4.4
       +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
       +-- xml2js@0.2.7 (sax@0.5.2)
       +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. Vous pouvez exécuter manuellement hello **ls** tooverify de commande qui un **nœud\_modules** dossier a été créé. Dans ce dossier, vous trouverez hello **le stockage azure** package qui contient les bibliothèques hello vous avez besoin de stockage de tooaccess.

### <a name="import-hello-package"></a>Importer un package hello
Ajouter hello suivant en haut de toohello code Hello **server.js** fichier dans votre application :

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Configurer une connexion Azure Storage
module de Hello azure lira des variables d’environnement hello AZURE\_stockage\_compte et AZURE\_stockage\_accès\_clé ou AZURE\_stockage\_connexion \_Chaîne pour les informations requises tooconnect tooyour compte de stockage Azure. Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello lors de l’appel **TableService**.

Pour obtenir un exemple de la définition de variables d’environnement hello Bonjour [portail Azure](https://portal.azure.com) pour un site Web Azure, consultez [à l’aide de Node.js web application hello Service de Table Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-table"></a>Création d’une table
Hello de code suivant crée un **TableService** de l’objet et l’utilise toocreate une nouvelle table. Ajoutez suit hello vers haut hello de **server.js**.

```nodejs
var tableSvc = azure.createTableService();
```

Hello appel trop**createTableIfNotExists** créera une nouvelle table avec le nom spécifié de hello si elle n’existe pas déjà. Hello exemple suivant crée une nouvelle table nommée « mytable » si elle n’existe pas déjà :

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

Hello `result.created` sera `true` si une nouvelle table est créée, et `false` si hello table existe déjà. Hello `response` contiennent des informations sur la demande de hello.

### <a name="filters"></a>Filtres
Les opérations de filtrage facultatif peuvent être appliquées toooperations effectuées à l’aide **TableService**. Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature de hello :

```nodejs
function handle (requestOptions, next)
```

Après son prétraitement sur les options de demande hello, méthode hello doit toocall « suivant », en passant un rappel avec hello après signature :

```nodejs
function (returnObject, finalCallback, next)
```

Dans ce rappel et après le traitement hello returnObject (réponse hello du serveur de toohello hello demande), le rappel de hello doit tooeither appeler ensuite s’il existe des toocontinue du traitement des autres filtres ou simplement appeler finalCallback sinon tooend hello appel de service.

Deux filtres qui implémentent la logique de nouvelle tentative sont incluses avec hello Azure SDK pour Node.js, **ExponentialRetryPolicyFilter** et **LinearRetryPolicyFilter**. Hello suivante permet de créer un **TableService** objet qui utilise hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a>Ajouter une table de tooa d’entité
tooadd une entité, d’abord créer un objet qui définit les propriétés de l’entité. Toutes les entités doivent contenir un **PartitionKey** et **RowKey**, qui sont des identificateurs uniques pour l’entité de hello.

* **PartitionKey** -détermine la partition de hello entité de hello est stockée dans
* **RowKey** - identifie de façon unique identifie l’entité hello au sein de la partition de hello

**PartitionKey** et **RowKey** doivent être des valeurs de chaîne. Pour plus d’informations, consultez [hello de présentation des modèle de données de Service de Table](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Hello Voici un exemple de définition d’une entité. Notez que **dueDate** est définie comme un type de **Edm.DateTime**. Spécifiant le type hello est facultatif et types seront déduits si n’est pas spécifiés.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> Il existe également un champ **Timestamp** pour chaque enregistrement, qui est défini par Azure quand une entité est insérée ou mise à jour.
>
>

Vous pouvez également utiliser hello **entityGenerator** toocreate entités. exemple Hello crée hello même entité de tâche à l’aide de hello **entityGenerator**.

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

tooadd une table de tooyour entité, passez hello entité objet toohello **insertEntity** (méthode).

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

Si l’opération de hello est réussie, `result` contiendra hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) Hello insérer enregistrement et `response` contiennent des informations sur l’opération de hello.

Exemple de réponse :

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> Par défaut, **insertEntity** ne retourne pas d’entité de hello inséré dans le cadre de hello `response` plus d’informations. Si vous prévoyez d’effectuer d’autres opérations sur cette entité, ou que vous souhaitez des informations toocache hello, il peut être utile toohave elle est retournée en tant que partie de hello `result`. Pour ce faire, activez **echoContent** comme suit :
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>Mise à jour d'une entité
Il existe plusieurs tooupdate de méthodes disponibles pour une entité existante :

* **replaceEntity** : met à jour une entité existante en la remplaçant
* **mergeEntity** -met à jour une entité existante en fusionnant les nouvelles valeurs de propriété dans une entité existante de hello
* **insertOrReplaceEntity** : met à jour une entité existante en la remplaçant. En l’absence d’entité, une nouvelle entité est insérée.
* **insertOrMergeEntity** -met à jour une entité existante en fusionnant des nouvelles valeurs de propriété dans hello existant. En l’absence d’entité, une nouvelle entité est insérée.

Hello exemple suivant illustre la mise à jour une entité à l’aide de **replaceEntity**:

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> Par défaut, la mise à jour une entité ne vérifie pas le toosee si les données de salutation mis à jour précédemment a été modifiées par un autre processus. mises à jour simultanées toosupport :
>
> 1. Obtenir hello ETag de l’objet hello mis à jour. Cela est retourné en tant que partie de hello `response` pour toute opération dépendant de l’entité et peuvent être récupérées via `response['.metadata'].etag`.
> 2. Lorsque vous effectuez une opération de mise à jour sur une entité, ajouter des informations d’ETag hello précédemment récupérées toohello nouvelle entité. Par exemple :
>
>       entity2['.metadata'].etag = currentEtag;
> 3. Effectuer l’opération de mise à jour hello. Si l’entité de hello a été modifiée depuis la récupération de valeur d’ETag hello, telles qu’une autre instance de votre application, un `error` s’affichera indiquant que la condition de mise à jour de hello spécifiée dans la demande de hello n’est pas remplie.
>
>

Avec **replaceEntity** et **mergeEntity**, si l’entité hello est en cours de mise à jour n’existe, opération de mise à jour hello échoue. Par conséquent, si vous le souhaitez toostore une entité, même si elle existe déjà, utilisez **insertOrReplaceEntity** ou **insertOrMergeEntity**.

Hello `result` pour la mise à jour réussie opérations contiendra hello **Etag** Hello mise à jour d’entité.

## <a name="work-with-groups-of-entities"></a>Utilisation des groupes d'entités
Il est parfois sens toosubmit plusieurs opérations ensemble dans un lot tooensure atomique de traitement par le serveur de hello. tooaccomplish qui, utilisez hello **TableBatch** toocreate un lot de la classe et ensuite utiliser hello **executeBatch** méthode **TableService** tooperform hello les opérations par lots.

 Hello l’exemple suivant illustre l’envoi de deux entités dans un lot :

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

Pour les opérations de traitement réussi, `result` contient des informations pour chaque opération de traitement par lots hello.

### <a name="work-with-batched-operations"></a>Ultiliser des opérations de traitement par lot
Opérations ajoutées tooa lot peut être inspecté en consultant hello `operations` propriété. Vous pouvez également utiliser hello suivant toowork méthodes avec des opérations :

* **clear** : permet de supprimer toutes les opérations d’un lot
* **getOperations** -obtient d’une opération de traitement par lots hello
* **hasOperations** -renvoie la valeur true si le traitement par lots hello contient des opérations
* **removeOperations** : permet de supprimer une opération
* **taille** -renvoie hello nombre d’opérations de traitement par lots hello

## <a name="retrieve-an-entity-by-key"></a>Récupération d'une entité par clé
tooreturn une entité spécifique en fonction de hello **PartitionKey** et **RowKey**, utilisez hello **retrieveEntity** (méthode).

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

Une fois cette opération terminée, `result` contiendra une entité de hello.

## <a name="query-a-set-of-entities"></a>Interrogation d’un ensemble d’entités
tooquery une table, utilisez hello **TableQuery** toobuild d’une expression de requête à l’aide de hello après des clauses de l’objet :

* **Sélectionnez** -hello champs toobe renvoyés par la requête de hello
* **où** - hello où clause

  * **and** : condition where `and`
  * **or** : condition where `or`
* **haut** -hello le nombre d’éléments toofetch

Hello exemple suivant crée une requête qui retournera hello supérieur cinq éléments avec un PartitionKey de 'hometasks'.

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

Comme **select** n'est pas utilisé, tous les champs sont renvoyés. requête de hello tooperform par rapport à une table, utilisez **queryEntities**. Hello exemple suivant utilise cette tooreturn interroger des entités à partir de « mytable ».

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

En cas de réussite, `result.entries` contient un tableau d’entités qui correspond à la requête de hello. Si la requête de hello a été tooreturn Impossible de toutes les entités, `result.continuationToken` sera non -*null* et peut être utilisé comme hello troisième paramètre de **queryEntities** tooretrieve résultats supplémentaires. Pour la requête initiale de hello, utilisez *null* pour le troisième paramètre de hello.

### <a name="query-a-subset-of-entity-properties"></a>Interrogation d’un sous-ensemble de propriétés d’entité
Une table de tooa de requête peut récupérer que quelques champs à partir d’une entité.
Ceci permet de réduire la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses. Hello d’utilisation **sélectionnez** clause et passez les noms hello de hello champs toobe retournés. Par exemple, hello requête suivante retournera uniquement hello **description** et **dueDate** champs.

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>Suppression d’une entité
Vous pouvez supprimer une entité en utilisant ses clés de partition et de ligne. Dans cet exemple, hello **task1** objet contient hello **RowKey** et **PartitionKey** valeurs hello entité toobe est supprimé. Objet de hello est transmis toohello **deleteEntity** (méthode).

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> Envisagez d’utiliser les ETags lors de la suppression d’éléments, tooensure hello élément n’a pas été modifiée par un autre processus. Consultez [Mise à jour d’une entité](#update-an-entity) pour plus d’informations sur l’utilisation des ETags.
>
>

## <a name="delete-a-table"></a>Suppression d’une table
Hello suivant code supprime une table à partir d’un compte de stockage.

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

Si vous ne savez pas si la table de hello existe, utilisez **deleteTableIfExists**.

## <a name="use-continuation-tokens"></a>Utiliser des jetons de liaison
Si vous interrogez des tables et que les résultats peuvent être volumineux, recherchez des jetons de liaison. Grandes quantités de données peuvent être disponibles pour votre requête que vous avez ne peut-être pas réalisé si vous ne générez pas toorecognize lorsqu’un jeton de continuation est présent.

résultats de Hello de l’objet retourné lors de l’interrogation de jeux d’entités un `continuationToken` propriété lorsque ce jeton est présent. Vous pouvez ensuite utiliser lors de l’exécution d’un toomove toocontinue de requête entre les entités de partition et table hello.

Lors de l’interrogation, un paramètre continuationToken peut être fourni entre l’instance d’objet de requête de hello et la fonction de rappel hello :

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

Si vous Inspectez hello `continuationToken` objet, vous rechercherez propriétés telles que `nextPartitionKey`, `nextRowKey` et `targetLocation`, ce qui peut être utilisé tooiterate via tous les résultats hello.

Il existe également un exemple de continuation dans le référentiel de Node.js de stockage Azure hello sur GitHub. Recherchez `examples/samples/continuationsample.js`.

## <a name="work-with-shared-access-signatures"></a>Utilisation des signatures d'accès partagé
Signatures d’accès partagé (SAS) sont un tootables d’un accès granulaire tooprovide sûre sans fournir votre nom de compte de stockage ou vos clés. Associations de sécurité sont souvent utilisés tooprovide limitée accès tooyour, par exemple pour autoriser une application mobile tooquery enregistrements.

Une application de confiance, tel qu’un service nuage génère une SAP à l’aide de hello **generateSharedAccessSignature** Hello **TableService**et il fournit tooan application non approuvée ou niveau de confiance partiel par exemple une application mobile. Hello SAS est générée à l’aide d’une stratégie qui décrit le démarrage de hello et fin pendant le hello SAS est valide, ainsi que hello détenteur SAS toohello accordé au niveau de l’accès.

Hello exemple suivant génère une nouvelle stratégie d’accès partagé qui permettra de hello de la table hello SAP titulaire tooquery (« r ») et expire 100 minutes après hello sa création.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

Notez que les informations sur l’hôte hello doivent être fournie, comme requis lorsque détenteur SAS hello tente également table de hello tooaccess.

Hello application cliente, puis utilise hello SAS avec **TableServiceWithSAS** tooperform des opérations par rapport à la table de hello. Bonjour à l’exemple suivant connecte toohello table et effectue une requête.

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

Hello SAP a été générée avec un accès de requête, si une tentative a été faite tooinsert, mettre à jour ou supprimer des entités, une erreur est retournée.

### <a name="access-control-lists"></a>Listes de contrôle d’accès
Vous pouvez également utiliser une stratégie d’accès de liste de contrôle d’accès (ACL) tooset hello pour une SAP. Cela est utile si vous souhaitez tooallow table hello de tooaccess plusieurs clients, mais fournissez des stratégies d’accès différents pour chaque client.

Une liste de contrôle d'accès est implémentée à l'aide d'un tableau de stratégies d'accès, dans lequel un ID est associé à chaque stratégie. Bonjour à l’exemple suivant définit deux stratégies, un pour « user1 » et un pour « user2 » :

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hello suivant obtient de l’exemple hello ACL actuel pour hello **hometasks** de table et y ajoute hello nouvelles stratégies à l’aide de **setTableAcl**. Cette approche permet :

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Une fois hello QU'ACL a été défini, vous pouvez ensuite créer un SAS en fonction de ID hello pour une stratégie. Bonjour à l’exemple suivant crée une nouvelle SAP pour « user2 » :

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello suivant des ressources.

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.
* [Kit de développement logiciel (SDK) Azure Storage pour Node](https://github.com/Azure/azure-storage-node) sur GitHub.
* [Centre pour développeurs Node.js](/develop/nodejs/)
* [Créer et déployer un tooan d’application Node.js site Web Azure](../app-service-web/app-service-web-get-started-nodejs.md)
