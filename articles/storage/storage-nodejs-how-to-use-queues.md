---
title: "aaaHow toouse stockage de file d’attente à partir de Node.js | Documents Microsoft"
description: "Découvrez comment toouse hello file d’attente Azure service toocreate et les files d’attente de suppression, insertion, obtenir et supprimer les messages. Les exemples sont écrits en Node.js."
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 977e5994c0be1b5d71c60b7479698ccb694ab860
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a>Comment toouse stockage de file d’attente à partir de Node.js
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Vue d'ensemble
Ce guide vous explique comment tooperform des scénarios courants utilisant hello service file d’attente de Microsoft Azure. exemples de Hello sont écrites à l’aide de hello Node.js API. Hello scénarios abordés incluent **insertion**, **lecture**, **mise en route**, et **suppression** file d’attente de messages, ainsi que  **Création et suppression de files d’attente**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Création d'une application Node.js
Créez une application Node.js vide. Pour des instructions de la création d’une application Node.js, consultez [créer une application web de Node.js dans Azure App Service], [générer et déployer un tooan d’application Node.js Azure Cloud Service] à l’aide de Windows PowerShell ou [ Créer et déployer un tooAzure d’application web Node.js à l’aide de Web Matrix].

## <a name="configure-your-application-tooaccess-storage"></a>Configurer votre Application tooAccess stockage
toouse stockage Azure, vous devez hello SDK de stockage Azure pour Node.js, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utiliser le Gestionnaire de Package de nœud (NPM) tooobtain hello package
1. Utiliser une interface de ligne de commande comme **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), accédez dossier toohello où vous avez créé votre exemple d’application.
2. Type **npm installer le stockage azure** dans la fenêtre de commande hello. Sortie de commande hello est similaire toohello l’exemple suivant.
 
    ```
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
    ```

3. Vous pouvez exécuter manuellement hello **ls** tooverify de commande qui un **nœud\_modules** dossier a été créé. Dans ce dossier, vous trouverez hello **le stockage azure** package qui contient les bibliothèques hello vous avez besoin pour accéder au stockage.

### <a name="import-hello-package"></a>Importer un package hello
Utilisez le bloc-notes ou un autre éditeur de texte, ajoutez hello suivant toohello haut la **server.js** fichier de l’application hello où vous avez l’intention toouse stockage :

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a>Configuration d'une connexion Azure Storage
module de Hello azure lira des variables d’environnement hello AZURE\_stockage\_compte et AZURE\_stockage\_accès\_clé ou AZURE\_stockage\_connexion \_Chaîne pour les informations requises tooconnect tooyour compte de stockage Azure. Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello lors de l’appel **createQueueService**.

Pour obtenir un exemple de la définition de variables d’environnement hello Bonjour [Azure Portal](https://portal.azure.com) pour un site Web Azure, consultez [à l’aide de Node.js web application hello Service de Table Azure].

## <a name="how-to-create-a-queue"></a>Création d'une file d'attente
Hello de code suivant crée un **QueueService** objet, ce qui vous permet de toowork avec les files d’attente.

```
var queueSvc = azure.createQueueService();
```

Hello d’utilisation **createQueueIfNotExists** (méthode), qui renvoie la file d’attente spécifiée de hello si elle existe déjà ou crée une nouvelle file d’attente avec le nom spécifié de hello si elle n’existe pas déjà.

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

Si la file d’attente hello est créé, `result.created` a la valeur true. Si la file d’attente hello existe, `result.created` a la valeur false.

### <a name="filters"></a>Filtres
Les opérations de filtrage facultatif peuvent être appliquées toooperations effectuées à l’aide **QueueService**. Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature de hello :

```
function handle (requestOptions, next)
```

Après avoir effectué le son de prétraitement sur les options de demande hello, méthode hello doit toocall « suivant » en passant un rappel avec hello après signature :

```
function (returnObject, finalCallback, next)
```

Dans ce rappel et après le traitement hello returnObject (réponse hello du serveur de toohello hello demande), le rappel de hello doit tooeither appeler ensuite s’il existe des toocontinue du traitement des autres filtres ou simplement appeler finalCallback tooend sinon des hello appel de service.

Deux filtres qui implémentent la logique de nouvelle tentative sont incluses avec hello Azure SDK pour Node.js, **ExponentialRetryPolicyFilter** et **LinearRetryPolicyFilter**. Hello suivante permet de créer un **QueueService** objet qui utilise hello **ExponentialRetryPolicyFilter**:

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Insertion d'un message dans une file d'attente
tooinsert un message dans une file d’attente, utilisez hello **createMessage** méthode pour créer un nouveau message et l’ajouter à la file d’attente de toohello.

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a>Comment : Lire des hello Message suivant
Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **peekMessages** (méthode). Par défaut, **peekMessages** lit un seul message.

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

Hello `result` contient le message de type hello.

> [!NOTE]
> À l’aide de **peekMessages** lorsqu’il y a aucun message dans la file d’attente hello ne retourne pas d’erreur, mais aucun message ne s’affichera.
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a>Procédure : Enlever hello Message suivant
Le traitement d'un message se fait en deux étapes :

1. Enlever un message de type hello.
2. Supprimer le message de type hello.

toodequeue un message, utilisez **getMessages**. Cela rend les messages hello invisibles dans la file d’attente de hello, donc aucun autre client ne peut les traiter. Une fois que votre application a traité un message, appelez **deleteMessage** toodelete à partir de la file d’attente hello. Hello, l’exemple suivant obtient un message, puis la supprime :

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> Par défaut, un message est masqué uniquement pour les 30 secondes, après laquelle il est visible tooother clients. Vous pouvez indiquer une autre valeur en utilisant `options.visibilityTimeout` avec **getMessages**.
> 
> [!NOTE]
> À l’aide de **getMessages** lorsqu’il y a aucun message dans la file d’attente hello ne retourne pas d’erreur, mais aucun message ne s’affichera.
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Comment : Modifier hello du contenu d’un Message en file d’attente
Vous pouvez modifier le contenu de hello d’un message en place à l’aide de file d’attente hello **updateMessage**. Bonjour à l’exemple suivant met à jour le texte hello d’un message :

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Options supplémentaires pour la suppression des messages dans la file d'attente
Il existe deux méthodes pour personnaliser l'extraction d'un message d'une file d'attente :

* `options.numOfMessages`-Récupérer un lot de messages (haut too32.)
* `options.visibilityTimeout` - Définir une durée d’invisibilité plus longue ou plus courte.

exemple Hello utilise hello **getMessages** messages tooget 15 de méthode dans un seul appel. Ensuite, il traite chaque message à l'aide d'une boucle for. Il définit également hello invisibilité délai d’expiration toofive minutes pour tous les messages retournés par cette méthode.

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a>Comment : Obtenir hello longueur de file d’attente
Hello **getQueueMetadata** retourne des métadonnées sur une file d’attente hello, y compris le nombre approximatif de hello de messages en attente dans la file d’attente hello.

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a>Procédure : Affichage de la liste de disques
tooretrieve une liste de files d’attente, utilisez **listQueuesSegmented**. tooretrieve une liste filtrée par un préfixe spécifique, utilisez **listQueuesSegmentedWithPrefix**.

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

Si les files d’attente ne peut pas être retournés, `result.continuationToken` peut être utilisée comme hello du premier paramètre de **listQueuesSegmented** ou hello du deuxième paramètre de **listQueuesSegmentedWithPrefix** tooretrieve résultats supplémentaires.

## <a name="how-to-delete-a-queue"></a>Suppression d'une file d'attente
toodelete une file d’attente et tous les messages hello qu’il contient, appelez le **deleteQueue** méthode sur un objet de file d’attente hello.

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

l’utilisation de tous les messages à partir d’une file d’attente sans la supprimer, tooclear **clearMessages**.

## <a name="how-to-work-with-shared-access-signatures"></a>Procédure : Utilisation des signatures d’accès partagé
Les Signatures d’accès partagé (SAS) sont un tooqueues d’un accès granulaire tooprovide sûre sans fournir votre nom de compte de stockage ou vos clés. Associations de sécurité sont souvent utilisés tooprovide limitée accès tooyour files d’attente, par exemple pour autoriser une application mobile toosubmit messages.

Une application de confiance, tel qu’un service nuage génère une SAP à l’aide de hello **generateSharedAccessSignature** Hello **QueueService**et il fournit tooan application non approuvée ou niveau de confiance partiel. Par exemple, une application mobile. Hello SAS est générée à l’aide d’une stratégie qui décrit le démarrage de hello et fin pendant le hello SAS est valide, ainsi que hello détenteur SAS toohello accordé au niveau de l’accès.

Bonjour, l’exemple suivant génère une nouvelle stratégie d’accès partagé qui permettra de hello SAS titulaire tooadd messages toohello file d’attente et expire minutes une 100 fois hello, qu'il est créé.

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

Notez que les informations sur l’hôte hello doivent être fourni en outre, comme requis lorsque détenteur SAS hello tente de file d’attente de tooaccess hello.

Hello application cliente, puis utilise hello SAS avec **QueueServiceWithSAS** tooperform des opérations par rapport à la file d’attente hello. Bonjour à l’exemple suivant connecte à la file d’attente de toohello et crée un message.

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

Hello SAP a été générée avec un accès d’ajouter, si une tentative a été faite tooread, mettre à jour ou supprimer des messages, une erreur est retournée.

### <a name="access-control-lists"></a>Listes de contrôle d'accès
Vous pouvez également utiliser une stratégie d’accès de liste de contrôle d’accès (ACL) tooset hello pour une SAP. Cela est utile si vous souhaitez tooallow file d’attente de plusieurs clients tooaccess hello, mais fournissez des stratégies d’accès différents pour chaque client.

Une liste de contrôle d'accès est implémentée à l'aide d'un tableau de stratégies d'accès, dans lequel un ID est associé à chaque stratégie. Bonjour à l’exemple suivant définit deux stratégies ; une valeur pour « user1 » et l’autre pour « user2 » :

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hello suivant obtient de l’exemple hello ACL actuel pour **myqueue**, puis ajoute hello nouvelles stratégies à l’aide de **setQueueAcl**. Cette approche permet :

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Une fois hello QU'ACL a été défini, vous pouvez ensuite créer un SAS en fonction de ID hello pour une stratégie. Bonjour à l’exemple suivant crée une nouvelle SAP pour « user2 » :

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente, suivez ces toolearn des liens sur les tâches de stockage plus complexes.

* Visitez hello [Blog de l’équipe stockage Azure][Azure Storage Team Blog].
* Visitez hello [Kit de développement logiciel pour le nœud de stockage Azure] [ Azure Storage SDK for Node] référentiel sur GitHub.

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[créer une application web de Node.js dans Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md
[à l’aide de Node.js web application hello Service de Table Azure]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[générer et déployer un tooan d’application Node.js Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[ Créer et déployer un tooAzure d’application web Node.js à l’aide de Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
