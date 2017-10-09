---
title: "aaaHow toouse stockage d’objets Blob à partir de Node.js | Documents Microsoft"
description: "Stocker des données non structurées dans le cloud hello avec le stockage d’objets Blob Azure (stockage d’objets)."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a>Comment toouse stockage d’objets Blob à partir de Node.js
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Vue d'ensemble
Cet article vous montre comment les scénarios courants tooperform à l’aide du stockage d’objets Blob. exemples de Hello sont écrites via hello Node.js API. scénarios de Hello couvertes incluent comment tooupload, répertorier, télécharger et supprimer des objets BLOB.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Création d’une application Node.js
Pour obtenir des instructions sur la façon de toocreate une application Node.js, consultez [créer une application web de Node.js dans Azure App Service], [générer et déployer un tooan d’application Node.js Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) --à l’aide de Windows PowerShell, ou [générer et déployer un tooAzure d’application web Node.js à l’aide de Web Matrix](https://www.microsoft.com/web/webmatrix/).

## <a name="configure-your-application-tooaccess-storage"></a>Configurer votre stockage tooaccess d’application
toouse stockage Azure, vous devez hello SDK de stockage Azure pour Node.js, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utiliser le Gestionnaire de Package de nœud (NPM) tooobtain hello package
1. Utiliser une interface de ligne de commande comme **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), dossier de toohello toonavigate où vous avez créé votre exemple application.
2. Type **npm installer le stockage azure** dans la fenêtre de commande hello. Sortie de commande hello est similaire toohello exemple de code suivant.

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
3. Vous pouvez exécuter manuellement hello **ls** tooverify de commande qui un **nœud\_modules** dossier a été créé. Dans ce dossier, recherche hello **le stockage azure** package qui contient les bibliothèques hello que vous avez besoin de stockage de tooaccess.

### <a name="import-hello-package"></a>Importer un package hello
Utilisez le bloc-notes ou un autre éditeur de texte, ajoutez hello suivant en haut de toohello de hello **server.js** fichier de l’application hello où vous avez l’intention toouse stockage :

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Configurer une connexion Azure Storage
Bonjour Azure module lit les variables d’environnement hello `AZURE_STORAGE_ACCOUNT` et `AZURE_STORAGE_ACCESS_KEY`, ou `AZURE_STORAGE_CONNECTION_STRING`, pour plus d’informations requises au compte de stockage Azure tooconnect tooyour. Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello lors de l’appel **createBlobService**.

Pour obtenir un exemple de la définition de variables d’environnement hello Bonjour [portail Azure](https://portal.azure.com) pour une application web Azure, consultez [à l’aide de Node.js web application hello Service de Table Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-container"></a>Créez un conteneur.
Hello **BlobService** objet vous permet de travailler avec les conteneurs et objets BLOB. Hello de code suivant crée un **BlobService** objet. Ajoutez suit hello vers haut hello de **server.js**:

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> Vous pouvez accéder à un objet blob de manière anonyme à l’aide de **createBlobServiceAnonymous** et de fournir l’adresse de l’hôte hello. Par exemple, utilisez `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

toocreate un nouveau conteneur, utilisez **createContainerIfNotExists**. Hello exemple de code suivant crée un nouveau conteneur nommé « mycontainer » :

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

Si le conteneur de hello a été créé récemment, `result.created` a la valeur true. Si le conteneur de hello existe déjà, `result.created` a la valeur false. `response`contient des informations sur les opération hello, y compris les informations d’ETag hello pour le conteneur de hello.

### <a name="container-security"></a>Sécurité du conteneur
Par défaut, les nouveaux conteneurs sont privés et ne sont pas accessibles de façon anonyme. conteneur de hello toomake public afin que vous pouvez y accéder anonymement, vous pouvez définir niveau d’accès du conteneur hello trop**blob** ou **conteneur**.

* **objet BLOB** -permet l’accès en lecture anonyme tooblob contenu et les métadonnées de ce conteneur, mais pas toocontainer métadonnées telles que la liste de tous les objets BLOB dans un conteneur
* **conteneur** -permet l’accès en lecture anonyme tooblob contenu et les métadonnées ainsi que les métadonnées de conteneur

Hello exemple de code suivant illustre le niveau de l’accès paramètre hello trop**blob**:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

Ou bien, vous pouvez modifier le niveau d’accès hello d’un conteneur à l’aide de **setContainerAcl** niveau d’accès toospecify hello. exemple modifications hello accès niveau toocontainer de code suivant de Hello :

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

Hello résultat contient plus d’informations sur l’opération hello, y compris le courant de hello **ETag** pour le conteneur de hello.

### <a name="filters"></a>Filtres
Vous pouvez appliquer l’option filtrage operations toooperations effectuées à l’aide de **BlobService**. Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature de hello :

```nodejs
function handle (requestOptions, next)
```

Après son prétraitement sur les options de demande hello, méthode hello doit toocall « suivant », en passant un rappel avec hello après signature :

```nodejs
function (returnObject, finalCallback, next)
```

Dans ce rappel et après le traitement hello returnObject (réponse hello du serveur de toohello hello demande), le rappel de hello doit tooeither appeler ensuite s’il existe des toocontinue du traitement des autres filtres ou simplement appeler le service de hello finalCallback tooend appel.

Deux filtres qui implémentent la logique de nouvelle tentative sont incluses avec hello Azure SDK pour Node.js, **ExponentialRetryPolicyFilter** et **LinearRetryPolicyFilter**. Hello suivante permet de créer un **BlobService** objet qui utilise hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a>Charger un objet blob dans un conteneur
Il existe trois types d’objets blob : les objets blob de blocs, les objets blob d’ajouts et les objets blob de pages. Objets BLOB de blocs permettre de toomore efficacement télécharger des données de grande taille. Les objets blob d’ajout sont optimisés pour les opérations d’ajout. Les objets blob de pages sont optimisés pour les opérations de lecture/écriture. Pour plus d’informations, consultez [Présentation des objets blob de blocs, des objets blob d’ajout et des objets blob de pages](http://msdn.microsoft.com/library/azure/ee691964.aspx).

### <a name="block-blobs"></a>Objets blob de blocs
tooupload données tooa objet blob de blocs, hello utilisation suivant :

* **createBlockBlobFromLocalFile** - crée un nouvel objet blob et télécharge le contenu hello d’un fichier
* **createBlockBlobFromStream** - crée un nouvel objet blob et télécharge le contenu hello d’un flux
* **createBlockBlobFromText** - crée un nouvel objet blob et télécharge le contenu hello d’une chaîne
* **createWriteStreamToBlockBlob** -fournit un objet blob de blocs écriture flux tooa

exemple de code suivant Hello télécharge contenu hello Hello **test.txt** fichier dans **myblob**.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

Hello `result` retournés par ces méthodes contient des informations sur l’opération de hello, par exemple hello **ETag** d’objet blob de hello.

### <a name="append-blobs"></a>Objets blob d’ajout
tooa de données tooupload nouveau ajouter l’objet blob, utilisez hello qui suit :

* **createAppendBlobFromLocalFile** - crée un nouvel objet blob d’ajout et télécharge le contenu hello d’un fichier
* **createAppendBlobFromStream** - crée un nouvel objet blob d’ajout et télécharge le contenu hello d’un flux
* **createAppendBlobFromText** - crée un nouvel objet blob d’ajout et télécharge le contenu hello d’une chaîne
* **createWriteStreamToNewAppendBlob** - crée un nouvel objet blob d’ajout et fournit un tooit toowrite de flux de données

exemple de code suivant Hello télécharge contenu hello Hello **test.txt** fichier dans **myappendblob**.

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

tooappend un tooan de bloc existant ajouter blob, hello utilisation suivant :

* **appendFromLocalFile** -ajouter hello contenu d’un fichier tooan existant ajouter des objets blob
* **appendFromStream** -ajouter hello contenu d’un flux tooan existant ajouter blob
* **appendFromText** -ajouter hello contenu d’une chaîne de tooan existant ajouter des objets blob
* **appendBlockFromStream** -ajouter hello contenu d’un flux tooan existant ajouter blob
* **appendBlockFromText** -ajouter hello contenu d’une chaîne de tooan existant ajouter des objets blob

> [!NOTE]
> appendFromXXX API effectuera des appels de validation côté client toofail tooavoid rapide inutile du serveur. Ce n’est pas le cas des API appendBlockFromXXX.
>
>

exemple de code suivant Hello télécharge contenu hello Hello **test.txt** fichier dans **myappendblob**.

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a>Objets blob de pages
tooupload données tooa objet blob de pages, hello utilisation suivant :

* **createPageBlob** : permet de créer un objet blob de pages d’une longueur spécifique
* **createPageBlobFromLocalFile** - crée un nouvel objet blob de page et télécharge le contenu hello d’un fichier
* **createPageBlobFromStream** - crée un nouvel objet blob de page et télécharge le contenu hello d’un flux
* **createWriteStreamToExistingPageBlob** -fournit un blob de pages écriture flux tooan existant
* **createWriteStreamToNewPageBlob** - crée un nouvel objet blob de page et fournit un tooit toowrite de flux de données

exemple de code suivant Hello télécharge contenu hello Hello **test.txt** fichier dans **mypageblob**.

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> Les objets blob de pages sont constitués de « pages » de 512 octets. Une erreur se produit lors du téléchargement de données lorsque leur taille n’est pas un multiple de 512.
>
>

## <a name="list-hello-blobs-in-a-container"></a>Répertorier les objets BLOB hello dans un conteneur
objets BLOB de hello toolist dans un conteneur, utilisez hello **listBlobsSegmented** (méthode). Si vous souhaitez que les objets BLOB de tooreturn avec un préfixe spécifique, utilisez **listBlobsSegmentedWithPrefix**.

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

Hello `result` contient un `entries` collection, qui est un tableau d’objets qui décrivent chaque objet blob. Si tous les objets BLOB ne peut pas être retournés, hello `result` fournit également un `continuationToken`, que vous pouvez utiliser comme hello deuxième paramètre tooretrieve des entrées supplémentaires.

## <a name="download-blobs"></a>Télécharger des objets blob
données toodownload à partir d’un objet blob, utilisez hello qui suit :

* **getBlobToLocalFile** -écrit hello blob contenu toofile
* **getBlobToStream** -écrit hello blob contenu tooa flux
* **getBlobToText** -écrit contenu d’objet blob hello tooa chaîne
* **createReadStream** -fournit une tooread de flux de données à partir de l’objet blob de hello

Hello exemple de code suivant montre comment utiliser **getBlobToStream** contenu de hello toodownload Hello **myblob** d’objets blob et le stocker toohello **output.txt** fichier à l’aide un flux de données :

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

Hello `result` contient des informations sur les objets blob hello, y compris **ETag** plus d’informations.

## <a name="delete-a-blob"></a>Supprimer un objet blob
Enfin, toodelete un objet blob, appelez **deleteBlob**. Hello l’exemple de code supprime hello objet blob nommé suivant **myblob**.

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a>Accès simultané
toosupport le blob tooa accès simultanés à partir de plusieurs clients ou de plusieurs instances de processus, vous pouvez utiliser **ETags** ou **baux**.

* **ETag** -fournit un toodetect de façon que hello blob ou conteneur a été modifié par un autre processus
* **Bail** - fournit une manière tooobtain exclusif, renouvelables, d’écriture ou de supprimer l’accès tooa objet blob pour une période donnée

### <a name="etag"></a>ETag
Utilisez les ETags si vous avez besoin tooallow plusieurs clients ou instances toowrite toohello bloc Blob ou page d’objets Blob simultanément. Hello ETag vous permet de toodetermine si hello conteneur ou un objet blob a été modifié depuis lecture initiale ou créé, ce qui vous permet de tooavoid remplacer les modifications validées par un autre client ou processus.

Vous pouvez définir des conditions de l’ETag à l’aide de hello facultatif `options.accessConditions` paramètre. Hello exemple de code suivant télécharge uniquement les hello **test.txt** fichier si l’objet blob de hello existe déjà et a la valeur d’ETag hello contenus par `etagToMatch`.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

Lorsque vous utilisez l’ETag, le modèle général de hello est :

1. Obtenir hello ETag en tant que résultat de hello de créer, de liste ou d’opération get.
2. Exécuter une action, la vérification de cette valeur ETag hello n’a pas été modifiée.

Si la valeur de hello a été modifié, cela indique que client ou une autre instance modifiée blob de hello ou un conteneur dans la mesure où vous avez obtenu la valeur de l’ETag hello.

### <a name="lease"></a>Lease
Vous pouvez acquérir un nouveau bail à l’aide de hello **acquireLease** méthode, en spécifiant l’objet blob de hello ou un conteneur que vous souhaitez tooobtain un bail sur. Par exemple, hello suivant code acquiert un bail sur **myblob**.

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

Les opérations suivantes sur **myblob** doit fournir hello `options.leaseId` paramètre. bail Hello ID est retourné en tant que `result.id` de **acquireLease**.

> [!NOTE]
> Par défaut, la durée du bail hello est infinie. Vous pouvez spécifier une durée non infini (entre 15 et 60 secondes) en fournissant hello `options.leaseDuration` paramètre.
>
>

tooremove un bail, utilisez **releaseLease**. toobreak un bail, mais empêcher les autres utilisateurs d’obtenir un nouveau bail tant que la durée d’origine du hello a expiré, utilisez **breakLease**.

## <a name="work-with-shared-access-signatures"></a>Utilisation des signatures d'accès partagé
Signatures d’accès partagé (SAS) sont un tooblobs d’un accès granulaire de tooprovide sûre et conteneurs sans fournir votre nom de compte de stockage ou vos clés. Signatures d’accès partagé sont souvent utilisés tooprovide limitée accès tooyour, par exemple pour autoriser une application mobile tooaccess BLOB.

> [!NOTE]
> Pendant que vous pouvez également autoriser l’accès anonyme tooblobs, signatures d’accès partagé permettent l’accès tooprovide plus contrôlé, que vous devez générer hello SAS.
>
>

Une application de confiance, tel qu’un service nuage génère des signatures d’accès partagé à l’aide de hello **generateSharedAccessSignature** Hello **BlobService**et il fournit tooan non fiable ou niveau de confiance partiel d’application comme une application mobile. Accès partagé sont générées à l’aide d’une stratégie qui décrit le démarrage de hello et les dates de fin pendant le hello signatures d’accès partagé sont valides, mais aussi hello détenteur de signatures d’accès partagé de toohello accordé au niveau d’accès.

exemple de code suivant Hello génère une nouvelle stratégie d’accès partagé qui permet de hello partagé accès signatures titulaire tooperform opérations de lecture sur hello **myblob** d’objets blob et 100 minutes après hello sa création n’expire.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

Notez que les informations sur l’hôte hello doivent être fournie, comme requis lorsque détenteur de signatures d’accès partagé hello tente également conteneur de hello tooaccess.

Hello client application utilise ensuite les signatures d’accès partagé avec **BlobServiceWithSAS** tooperform des opérations par rapport à l’objet blob de hello. Hello suivante obtient des informations sur **myblob**.

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

Étant donné que les signatures d’accès hello partagé a été générés avec un accès en lecture seule, si une tentative d’objet blob de hello toomodify, une erreur est renvoyée.

### <a name="access-control-lists"></a>Listes de contrôle d'accès
Vous pouvez également utiliser une stratégie d’accès hello tooset accès contrôle liste (ACL) pour les associations de sécurité. Cela est utile si vous souhaitez tooallow plusieurs clients tooaccess un conteneur, mais fournissez des stratégies d’accès différents pour chaque client.

Une liste de contrôle d'accès est implémentée à l'aide d'un tableau de stratégies d'accès, dans lequel un ID est associé à chaque stratégie. Hello, exemple de code suivant définit deux stratégies, un pour « user1 » et un pour « user2 » :

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hello suivant obtient d’exemple de code hello ACL actuel pour **mycontainer**, puis ajoute hello nouvelles stratégies à l’aide de **setBlobAcl**. Cette approche permet :

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Une fois hello QU'ACL est définie, vous pouvez ensuite créer des signatures d’accès partagé en fonction de ID hello pour une stratégie. Hello, exemple de code suivant crée les nouvelles signatures d’accès partagé pour « user2 » :

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello suivant des ressources.

* [Kit de développement logiciel (SDK) Stockage Azure pour la référence de l’API Node][Kit de développement logiciel (SDK) Stockage Azure pour la référence de l'API Node]
* [Blog de l’équipe Stockage Azure] [Blog de l’équipe Stockage Azure]
* Référentiel [Kit de développement logiciel (SDK) Stockage Azure pour Node][Azure Storage SDK for Node] sur GitHub
* [Centre pour développeurs Node.js](https://azure.microsoft.com/develop/nodejs/)
* [Transfert de données avec hello utilitaire de ligne de commande AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[Application web Node.js à l’aide de hello Service de Table Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)    
[Générer et déployer un tooAzure d’application web Node.js à l’aide de Web Matrix] : https://www.microsoft.com/web/webmatrix/  
[À l’aide de hello API REST] : http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal] : https://portal.azure.com [générer et déployer un tooan d’application Node.js Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Blog de l’équipe stockage Azure] : http:// blogs.msdn.com/b/windowsazurestorage/ [Azure SDK pour le nœud référence de l’API de stockage] : http://dl.windowsazure.com/nodestoragedocs/index.html
