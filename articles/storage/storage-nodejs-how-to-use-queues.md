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
# <a name="how-toouse-queue-storage-from-nodejs"></a><span data-ttu-id="a41cb-104">Comment toouse stockage de file d’attente à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="a41cb-104">How toouse Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="a41cb-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a41cb-105">Overview</span></span>
<span data-ttu-id="a41cb-106">Ce guide vous explique comment tooperform des scénarios courants utilisant hello service file d’attente de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a41cb-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue service.</span></span> <span data-ttu-id="a41cb-107">exemples de Hello sont écrites à l’aide de hello Node.js API.</span><span class="sxs-lookup"><span data-stu-id="a41cb-107">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="a41cb-108">Hello scénarios abordés incluent **insertion**, **lecture**, **mise en route**, et **suppression** file d’attente de messages, ainsi que  **Création et suppression de files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="a41cb-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="a41cb-109">Création d'une application Node.js</span><span class="sxs-lookup"><span data-stu-id="a41cb-109">Create a Node.js Application</span></span>
<span data-ttu-id="a41cb-110">Créez une application Node.js vide.</span><span class="sxs-lookup"><span data-stu-id="a41cb-110">Create a blank Node.js application.</span></span> <span data-ttu-id="a41cb-111">Pour des instructions de la création d’une application Node.js, consultez [créer une application web de Node.js dans Azure App Service], [générer et déployer un tooan d’application Node.js Azure Cloud Service] à l’aide de Windows PowerShell ou [ Créer et déployer un tooAzure d’application web Node.js à l’aide de Web Matrix].</span><span class="sxs-lookup"><span data-stu-id="a41cb-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix].</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="a41cb-112">Configurer votre Application tooAccess stockage</span><span class="sxs-lookup"><span data-stu-id="a41cb-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="a41cb-113">toouse stockage Azure, vous devez hello SDK de stockage Azure pour Node.js, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="a41cb-113">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="a41cb-114">Utiliser le Gestionnaire de Package de nœud (NPM) tooobtain hello package</span><span class="sxs-lookup"><span data-stu-id="a41cb-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="a41cb-115">Utiliser une interface de ligne de commande comme **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), accédez dossier toohello où vous avez créé votre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="a41cb-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="a41cb-116">Type **npm installer le stockage azure** dans la fenêtre de commande hello.</span><span class="sxs-lookup"><span data-stu-id="a41cb-116">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="a41cb-117">Sortie de commande hello est similaire toohello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="a41cb-117">Output from hello command is similar toohello following example.</span></span>
 
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

3. <span data-ttu-id="a41cb-118">Vous pouvez exécuter manuellement hello **ls** tooverify de commande qui un **nœud\_modules** dossier a été créé.</span><span class="sxs-lookup"><span data-stu-id="a41cb-118">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="a41cb-119">Dans ce dossier, vous trouverez hello **le stockage azure** package qui contient les bibliothèques hello vous avez besoin pour accéder au stockage.</span><span class="sxs-lookup"><span data-stu-id="a41cb-119">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need to access storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="a41cb-120">Importer un package hello</span><span class="sxs-lookup"><span data-stu-id="a41cb-120">Import hello package</span></span>
<span data-ttu-id="a41cb-121">Utilisez le bloc-notes ou un autre éditeur de texte, ajoutez hello suivant toohello haut la **server.js** fichier de l’application hello où vous avez l’intention toouse stockage :</span><span class="sxs-lookup"><span data-stu-id="a41cb-121">Using Notepad or another text editor, add hello following toohello top the **server.js** file of hello application where you intend toouse storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="a41cb-122">Configuration d'une connexion Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a41cb-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="a41cb-123">module de Hello azure lira des variables d’environnement hello AZURE\_stockage\_compte et AZURE\_stockage\_accès\_clé ou AZURE\_stockage\_connexion \_Chaîne pour les informations requises tooconnect tooyour compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="a41cb-123">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="a41cb-124">Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello lors de l’appel **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="a41cb-124">If these environment variables are not set, you must specify hello account information when calling **createQueueService**.</span></span>

<span data-ttu-id="a41cb-125">Pour obtenir un exemple de la définition de variables d’environnement hello Bonjour [Azure Portal](https://portal.azure.com) pour un site Web Azure, consultez [à l’aide de Node.js web application hello Service de Table Azure].</span><span class="sxs-lookup"><span data-stu-id="a41cb-125">For an example of setting hello environment variables in hello [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="a41cb-126">Création d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="a41cb-126">How To: Create a Queue</span></span>
<span data-ttu-id="a41cb-127">Hello de code suivant crée un **QueueService** objet, ce qui vous permet de toowork avec les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="a41cb-127">hello following code creates a **QueueService** object, which enables you toowork with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="a41cb-128">Hello d’utilisation **createQueueIfNotExists** (méthode), qui renvoie la file d’attente spécifiée de hello si elle existe déjà ou crée une nouvelle file d’attente avec le nom spécifié de hello si elle n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="a41cb-128">Use hello **createQueueIfNotExists** method, which returns hello specified queue if it already exists or creates a new queue with hello specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="a41cb-129">Si la file d’attente hello est créé, `result.created` a la valeur true.</span><span class="sxs-lookup"><span data-stu-id="a41cb-129">If hello queue is created, `result.created` is true.</span></span> <span data-ttu-id="a41cb-130">Si la file d’attente hello existe, `result.created` a la valeur false.</span><span class="sxs-lookup"><span data-stu-id="a41cb-130">If hello queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="a41cb-131">Filtres</span><span class="sxs-lookup"><span data-stu-id="a41cb-131">Filters</span></span>
<span data-ttu-id="a41cb-132">Les opérations de filtrage facultatif peuvent être appliquées toooperations effectuées à l’aide **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="a41cb-132">Optional filtering operations can be applied toooperations performed using **QueueService**.</span></span> <span data-ttu-id="a41cb-133">Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature de hello :</span><span class="sxs-lookup"><span data-stu-id="a41cb-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="a41cb-134">Après avoir effectué le son de prétraitement sur les options de demande hello, méthode hello doit toocall « suivant » en passant un rappel avec hello après signature :</span><span class="sxs-lookup"><span data-stu-id="a41cb-134">After doing its preprocessing on hello request options, hello method needs toocall "next" passing a callback with hello following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="a41cb-135">Dans ce rappel et après le traitement hello returnObject (réponse hello du serveur de toohello hello demande), le rappel de hello doit tooeither appeler ensuite s’il existe des toocontinue du traitement des autres filtres ou simplement appeler finalCallback tooend sinon des hello appel de service.</span><span class="sxs-lookup"><span data-stu-id="a41cb-135">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend up hello service invocation.</span></span>

<span data-ttu-id="a41cb-136">Deux filtres qui implémentent la logique de nouvelle tentative sont incluses avec hello Azure SDK pour Node.js, **ExponentialRetryPolicyFilter** et **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="a41cb-136">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="a41cb-137">Hello suivante permet de créer un **QueueService** objet qui utilise hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="a41cb-137">hello following creates a **QueueService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="a41cb-138">Insertion d'un message dans une file d'attente</span><span class="sxs-lookup"><span data-stu-id="a41cb-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="a41cb-139">tooinsert un message dans une file d’attente, utilisez hello **createMessage** méthode pour créer un nouveau message et l’ajouter à la file d’attente de toohello.</span><span class="sxs-lookup"><span data-stu-id="a41cb-139">tooinsert a message into a queue, use hello **createMessage** method to create a new message and add it toohello queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="a41cb-140">Comment : Lire des hello Message suivant</span><span class="sxs-lookup"><span data-stu-id="a41cb-140">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="a41cb-141">Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **peekMessages** (méthode).</span><span class="sxs-lookup"><span data-stu-id="a41cb-141">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peekMessages** method.</span></span> <span data-ttu-id="a41cb-142">Par défaut, **peekMessages** lit un seul message.</span><span class="sxs-lookup"><span data-stu-id="a41cb-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="a41cb-143">Hello `result` contient le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="a41cb-143">hello `result` contains hello message.</span></span>

> [!NOTE]
> <span data-ttu-id="a41cb-144">À l’aide de **peekMessages** lorsqu’il y a aucun message dans la file d’attente hello ne retourne pas d’erreur, mais aucun message ne s’affichera.</span><span class="sxs-lookup"><span data-stu-id="a41cb-144">Using **peekMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="a41cb-145">Procédure : Enlever hello Message suivant</span><span class="sxs-lookup"><span data-stu-id="a41cb-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="a41cb-146">Le traitement d'un message se fait en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="a41cb-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="a41cb-147">Enlever un message de type hello.</span><span class="sxs-lookup"><span data-stu-id="a41cb-147">Dequeue hello message.</span></span>
2. <span data-ttu-id="a41cb-148">Supprimer le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="a41cb-148">Delete hello message.</span></span>

<span data-ttu-id="a41cb-149">toodequeue un message, utilisez **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="a41cb-149">toodequeue a message, use **getMessages**.</span></span> <span data-ttu-id="a41cb-150">Cela rend les messages hello invisibles dans la file d’attente de hello, donc aucun autre client ne peut les traiter.</span><span class="sxs-lookup"><span data-stu-id="a41cb-150">This makes hello messages invisible in hello queue, so no other clients can process them.</span></span> <span data-ttu-id="a41cb-151">Une fois que votre application a traité un message, appelez **deleteMessage** toodelete à partir de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="a41cb-151">Once your application has processed a message, call **deleteMessage** toodelete it from hello queue.</span></span> <span data-ttu-id="a41cb-152">Hello, l’exemple suivant obtient un message, puis la supprime :</span><span class="sxs-lookup"><span data-stu-id="a41cb-152">hello following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="a41cb-153">Par défaut, un message est masqué uniquement pour les 30 secondes, après laquelle il est visible tooother clients.</span><span class="sxs-lookup"><span data-stu-id="a41cb-153">By default, a message is only hidden for 30 seconds, after which it is visible tooother clients.</span></span> <span data-ttu-id="a41cb-154">Vous pouvez indiquer une autre valeur en utilisant `options.visibilityTimeout` avec **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="a41cb-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="a41cb-155">À l’aide de **getMessages** lorsqu’il y a aucun message dans la file d’attente hello ne retourne pas d’erreur, mais aucun message ne s’affichera.</span><span class="sxs-lookup"><span data-stu-id="a41cb-155">Using **getMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="a41cb-156">Comment : Modifier hello du contenu d’un Message en file d’attente</span><span class="sxs-lookup"><span data-stu-id="a41cb-156">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="a41cb-157">Vous pouvez modifier le contenu de hello d’un message en place à l’aide de file d’attente hello **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="a41cb-157">You can change hello contents of a message in-place in hello queue using **updateMessage**.</span></span> <span data-ttu-id="a41cb-158">Bonjour à l’exemple suivant met à jour le texte hello d’un message :</span><span class="sxs-lookup"><span data-stu-id="a41cb-158">hello following example updates hello text of a message:</span></span>

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

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="a41cb-159">Options supplémentaires pour la suppression des messages dans la file d'attente</span><span class="sxs-lookup"><span data-stu-id="a41cb-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="a41cb-160">Il existe deux méthodes pour personnaliser l'extraction d'un message d'une file d'attente :</span><span class="sxs-lookup"><span data-stu-id="a41cb-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="a41cb-161">`options.numOfMessages`-Récupérer un lot de messages (haut too32.)</span><span class="sxs-lookup"><span data-stu-id="a41cb-161">`options.numOfMessages` - Retrieve a batch of messages (up too32.)</span></span>
* <span data-ttu-id="a41cb-162">`options.visibilityTimeout` - Définir une durée d’invisibilité plus longue ou plus courte.</span><span class="sxs-lookup"><span data-stu-id="a41cb-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="a41cb-163">exemple Hello utilise hello **getMessages** messages tooget 15 de méthode dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="a41cb-163">hello following example uses hello **getMessages** method tooget 15 messages in one call.</span></span> <span data-ttu-id="a41cb-164">Ensuite, il traite chaque message à l'aide d'une boucle for.</span><span class="sxs-lookup"><span data-stu-id="a41cb-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="a41cb-165">Il définit également hello invisibilité délai d’expiration toofive minutes pour tous les messages retournés par cette méthode.</span><span class="sxs-lookup"><span data-stu-id="a41cb-165">It also sets hello invisibility timeout toofive minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="a41cb-166">Comment : Obtenir hello longueur de file d’attente</span><span class="sxs-lookup"><span data-stu-id="a41cb-166">How To: Get hello Queue Length</span></span>
<span data-ttu-id="a41cb-167">Hello **getQueueMetadata** retourne des métadonnées sur une file d’attente hello, y compris le nombre approximatif de hello de messages en attente dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="a41cb-167">hello **getQueueMetadata** returns metadata about hello queue, including hello approximate number of messages waiting in hello queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="a41cb-168">Procédure : Affichage de la liste de disques</span><span class="sxs-lookup"><span data-stu-id="a41cb-168">How To: List Queues</span></span>
<span data-ttu-id="a41cb-169">tooretrieve une liste de files d’attente, utilisez **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="a41cb-169">tooretrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="a41cb-170">tooretrieve une liste filtrée par un préfixe spécifique, utilisez **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="a41cb-170">tooretrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

<span data-ttu-id="a41cb-171">Si les files d’attente ne peut pas être retournés, `result.continuationToken` peut être utilisée comme hello du premier paramètre de **listQueuesSegmented** ou hello du deuxième paramètre de **listQueuesSegmentedWithPrefix** tooretrieve résultats supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a41cb-171">If all queues cannot be returned, `result.continuationToken` can be used as hello first parameter of **listQueuesSegmented** or hello second parameter of **listQueuesSegmentedWithPrefix** tooretrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="a41cb-172">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="a41cb-172">How To: Delete a Queue</span></span>
<span data-ttu-id="a41cb-173">toodelete une file d’attente et tous les messages hello qu’il contient, appelez le **deleteQueue** méthode sur un objet de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="a41cb-173">toodelete a queue and all hello messages contained in it, call the **deleteQueue** method on hello queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="a41cb-174">l’utilisation de tous les messages à partir d’une file d’attente sans la supprimer, tooclear **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="a41cb-174">tooclear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="a41cb-175">Procédure : Utilisation des signatures d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="a41cb-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="a41cb-176">Les Signatures d’accès partagé (SAS) sont un tooqueues d’un accès granulaire tooprovide sûre sans fournir votre nom de compte de stockage ou vos clés.</span><span class="sxs-lookup"><span data-stu-id="a41cb-176">Shared Access Signatures (SAS) are a secure way tooprovide granular access tooqueues without providing your storage account name or keys.</span></span> <span data-ttu-id="a41cb-177">Associations de sécurité sont souvent utilisés tooprovide limitée accès tooyour files d’attente, par exemple pour autoriser une application mobile toosubmit messages.</span><span class="sxs-lookup"><span data-stu-id="a41cb-177">SAS are often used tooprovide limited access tooyour queues, such as allowing a mobile app toosubmit messages.</span></span>

<span data-ttu-id="a41cb-178">Une application de confiance, tel qu’un service nuage génère une SAP à l’aide de hello **generateSharedAccessSignature** Hello **QueueService**et il fournit tooan application non approuvée ou niveau de confiance partiel.</span><span class="sxs-lookup"><span data-stu-id="a41cb-178">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **QueueService**, and provides it tooan untrusted or semi-trusted application.</span></span> <span data-ttu-id="a41cb-179">Par exemple, une application mobile.</span><span class="sxs-lookup"><span data-stu-id="a41cb-179">For example, a mobile app.</span></span> <span data-ttu-id="a41cb-180">Hello SAS est générée à l’aide d’une stratégie qui décrit le démarrage de hello et fin pendant le hello SAS est valide, ainsi que hello détenteur SAS toohello accordé au niveau de l’accès.</span><span class="sxs-lookup"><span data-stu-id="a41cb-180">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="a41cb-181">Bonjour, l’exemple suivant génère une nouvelle stratégie d’accès partagé qui permettra de hello SAS titulaire tooadd messages toohello file d’attente et expire minutes une 100 fois hello, qu'il est créé.</span><span class="sxs-lookup"><span data-stu-id="a41cb-181">hello following example generates a new shared access policy that will allow hello SAS holder tooadd messages toohello queue, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="a41cb-182">Notez que les informations sur l’hôte hello doivent être fourni en outre, comme requis lorsque détenteur SAS hello tente de file d’attente de tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="a41cb-182">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello queue.</span></span>

<span data-ttu-id="a41cb-183">Hello application cliente, puis utilise hello SAS avec **QueueServiceWithSAS** tooperform des opérations par rapport à la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="a41cb-183">hello client application then uses hello SAS with **QueueServiceWithSAS** tooperform operations against hello queue.</span></span> <span data-ttu-id="a41cb-184">Bonjour à l’exemple suivant connecte à la file d’attente de toohello et crée un message.</span><span class="sxs-lookup"><span data-stu-id="a41cb-184">hello following example connects toohello queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="a41cb-185">Hello SAP a été générée avec un accès d’ajouter, si une tentative a été faite tooread, mettre à jour ou supprimer des messages, une erreur est retournée.</span><span class="sxs-lookup"><span data-stu-id="a41cb-185">Since hello SAS was generated with add access, if an attempt were made tooread, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="a41cb-186">Listes de contrôle d'accès</span><span class="sxs-lookup"><span data-stu-id="a41cb-186">Access control lists</span></span>
<span data-ttu-id="a41cb-187">Vous pouvez également utiliser une stratégie d’accès de liste de contrôle d’accès (ACL) tooset hello pour une SAP.</span><span class="sxs-lookup"><span data-stu-id="a41cb-187">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="a41cb-188">Cela est utile si vous souhaitez tooallow file d’attente de plusieurs clients tooaccess hello, mais fournissez des stratégies d’accès différents pour chaque client.</span><span class="sxs-lookup"><span data-stu-id="a41cb-188">This is useful if you wish tooallow multiple clients tooaccess hello queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="a41cb-189">Une liste de contrôle d'accès est implémentée à l'aide d'un tableau de stratégies d'accès, dans lequel un ID est associé à chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="a41cb-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="a41cb-190">Bonjour à l’exemple suivant définit deux stratégies ; une valeur pour « user1 » et l’autre pour « user2 » :</span><span class="sxs-lookup"><span data-stu-id="a41cb-190">hello  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="a41cb-191">Hello suivant obtient de l’exemple hello ACL actuel pour **myqueue**, puis ajoute hello nouvelles stratégies à l’aide de **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="a41cb-191">hello following example gets hello current ACL for **myqueue**, then adds hello new policies using **setQueueAcl**.</span></span> <span data-ttu-id="a41cb-192">Cette approche permet :</span><span class="sxs-lookup"><span data-stu-id="a41cb-192">This approach allows:</span></span>

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

<span data-ttu-id="a41cb-193">Une fois hello QU'ACL a été défini, vous pouvez ensuite créer un SAS en fonction de ID hello pour une stratégie.</span><span class="sxs-lookup"><span data-stu-id="a41cb-193">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="a41cb-194">Bonjour à l’exemple suivant crée une nouvelle SAP pour « user2 » :</span><span class="sxs-lookup"><span data-stu-id="a41cb-194">hello following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="a41cb-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a41cb-195">Next Steps</span></span>
<span data-ttu-id="a41cb-196">Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente, suivez ces toolearn des liens sur les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="a41cb-196">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="a41cb-197">Visitez hello [Blog de l’équipe stockage Azure][Azure Storage Team Blog].</span><span class="sxs-lookup"><span data-stu-id="a41cb-197">Visit hello [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="a41cb-198">Visitez hello [Kit de développement logiciel pour le nœud de stockage Azure] [ Azure Storage SDK for Node] référentiel sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a41cb-198">Visit hello [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[créer une application web de Node.js dans Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md
[à l’aide de Node.js web application hello Service de Table Azure]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[générer et déployer un tooan d’application Node.js Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[ Créer et déployer un tooAzure d’application web Node.js à l’aide de Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
