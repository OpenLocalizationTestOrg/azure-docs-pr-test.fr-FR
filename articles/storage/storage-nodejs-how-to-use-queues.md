---
title: "Utilisation du stockage de files d’attente à partir de Node.js | Microsoft Docs"
description: "Découvrez comment utiliser le service de File d'attente Azure pour créer et supprimer des files d'attente, ainsi que pour insérer, récupérer et supprimer des messages. Les exemples sont écrits en Node.js."
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
ms.openlocfilehash: e30297bd0cc65105c92d6428035d2e6c156448af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-nodejs"></a><span data-ttu-id="dedb9-104">Utilisation du stockage de files d'attente à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="dedb9-104">How to use Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="dedb9-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="dedb9-105">Overview</span></span>
<span data-ttu-id="dedb9-106">Ce guide décrit le déroulement de scénarios courants dans le cadre de l’utilisation du service de File d’attente Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dedb9-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue service.</span></span> <span data-ttu-id="dedb9-107">Les exemples sont écrits en utilisant l'API Node.js.</span><span class="sxs-lookup"><span data-stu-id="dedb9-107">The samples are written using the Node.js API.</span></span> <span data-ttu-id="dedb9-108">Les scénarios traités incluent **l’insertion**, la **lecture furtive**, la **récupération** et la **suppression** des messages de file d’attente, ainsi que la **création et suppression des files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="dedb9-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="dedb9-109">Création d'une application Node.js</span><span class="sxs-lookup"><span data-stu-id="dedb9-109">Create a Node.js Application</span></span>
<span data-ttu-id="dedb9-110">Créez une application Node.js vide.</span><span class="sxs-lookup"><span data-stu-id="dedb9-110">Create a blank Node.js application.</span></span> <span data-ttu-id="dedb9-111">Pour obtenir des instructions sur la création d’une application Node.js, consultez [Créer une application web Node.js dans Azure App Service], [Création et déploiement d’une application Node.js dans un service cloud Azure] à l’aide de Windows PowerShell, ou [Créer et déployer une application web Node.js dans Azure à l’aide de WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="dedb9-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix].</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="dedb9-112">Configuration de votre application pour accéder au stockage</span><span class="sxs-lookup"><span data-stu-id="dedb9-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="dedb9-113">Pour utiliser le stockage Azure, vous avez besoin du Kit de développement logiciel (SDK) Azure Storage pour Node.js, qui inclut un ensemble de bibliothèques pratiques qui communiquent avec les services REST de stockage.</span><span class="sxs-lookup"><span data-stu-id="dedb9-113">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="dedb9-114">Utilisation de Node Package Manager (NPM) pour obtenir le package</span><span class="sxs-lookup"><span data-stu-id="dedb9-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="dedb9-115">Utilisez une interface de ligne de commande telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix) pour accéder au dossier dans lequel vous avez créé votre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="dedb9-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="dedb9-116">Tapez **npm install azure-storage** dans la fenêtre de commande.</span><span class="sxs-lookup"><span data-stu-id="dedb9-116">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="dedb9-117">Le résultat de la commande ressemble à l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="dedb9-117">Output from the command is similar to the following example.</span></span>
 
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

3. <span data-ttu-id="dedb9-118">Vous pouvez exécuter manuellement la commande **ls** pour vérifier que le dossier **node\_modules** a été créé.</span><span class="sxs-lookup"><span data-stu-id="dedb9-118">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="dedb9-119">Dans ce dossier, recherchez le dossier **azure-storage** , qui contient les bibliothèques dont vous avez besoin pour accéder au stockage.</span><span class="sxs-lookup"><span data-stu-id="dedb9-119">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="dedb9-120">Importation du package</span><span class="sxs-lookup"><span data-stu-id="dedb9-120">Import the package</span></span>
<span data-ttu-id="dedb9-121">À l'aide d'un éditeur de texte, comme le Bloc-notes, ajoutez la commande suivante au début du fichier **server.js** de l'application dans laquelle vous souhaitez utiliser le stockage :</span><span class="sxs-lookup"><span data-stu-id="dedb9-121">Using Notepad or another text editor, add the following to the top the **server.js** file of the application where you intend to use storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="dedb9-122">Configuration d'une connexion Azure Storage</span><span class="sxs-lookup"><span data-stu-id="dedb9-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="dedb9-123">Le module Azure lit les variables d’environnement AZURE\_STORAGE\_ACCOUNT et AZURE\_STORAGE\_ACCESS\_KEY, ou AZURE\_STORAGE\_CONNECTION\_STRING pour obtenir les informations nécessaires à la connexion à votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="dedb9-123">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="dedb9-124">Si ces variables d'environnement ne sont pas définies, vous devez spécifier les informations de compte lors de l'appel de **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="dedb9-124">If these environment variables are not set, you must specify the account information when calling **createQueueService**.</span></span>

<span data-ttu-id="dedb9-125">Pour obtenir un exemple de configuration des variables d’environnement dans le [portail Azure](https://portal.azure.com) pour un site web Azure, consultez [Application web Node.js avec le service de Table Azure].</span><span class="sxs-lookup"><span data-stu-id="dedb9-125">For an example of setting the environment variables in the [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="dedb9-126">Création d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="dedb9-126">How To: Create a Queue</span></span>
<span data-ttu-id="dedb9-127">Le code suivant crée un objet **QueueService** , ce qui vous permet d'utiliser les files d'attente.</span><span class="sxs-lookup"><span data-stu-id="dedb9-127">The following code creates a **QueueService** object, which enables you to work with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="dedb9-128">Utilisez la méthode **createQueueIfNotExists** , qui renvoie la file d'attente spécifiée si elle existe déjà ou qui en crée une avec le nom spécifié dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="dedb9-128">Use the **createQueueIfNotExists** method, which returns the specified queue if it already exists or creates a new queue with the specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="dedb9-129">Si la file d’attente est créée, `result.created` a la valeur true.</span><span class="sxs-lookup"><span data-stu-id="dedb9-129">If the queue is created, `result.created` is true.</span></span> <span data-ttu-id="dedb9-130">Si la file d’attente existe, `result.created` a la valeur false.</span><span class="sxs-lookup"><span data-stu-id="dedb9-130">If the queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="dedb9-131">Filtres</span><span class="sxs-lookup"><span data-stu-id="dedb9-131">Filters</span></span>
<span data-ttu-id="dedb9-132">Des opérations facultatives de filtrage peuvent être appliquées aux opérations exécutées par le biais de **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="dedb9-132">Optional filtering operations can be applied to operations performed using **QueueService**.</span></span> <span data-ttu-id="dedb9-133">Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature :</span><span class="sxs-lookup"><span data-stu-id="dedb9-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="dedb9-134">Après le prétraitement des options de la requête, la méthode doit appeler « next » en passant un rappel avec la signature suivante :</span><span class="sxs-lookup"><span data-stu-id="dedb9-134">After doing its preprocessing on the request options, the method needs to call "next" passing a callback with the following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="dedb9-135">Dans ce rappel, et après le traitement de returnObject (la réponse de la requête au serveur), le rappel doit appeler la fonction next, si elle existe, pour continuer à traiter d’autres filtres ou simplement appeler finalCallback pour terminer l’utilisation du service.</span><span class="sxs-lookup"><span data-stu-id="dedb9-135">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end up the service invocation.</span></span>

<span data-ttu-id="dedb9-136">Deux filtres qui implémentent la logique de relance sont inclus dans le Kit de développement logiciel (SDK) Azure pour Node.js : **ExponentialRetryPolicyFilter** et **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="dedb9-136">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="dedb9-137">Le code suivant crée un objet **QueueService** qui utilise le filtre **ExponentialRetryPolicyFilter** :</span><span class="sxs-lookup"><span data-stu-id="dedb9-137">The following creates a **QueueService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="dedb9-138">Insertion d'un message dans une file d'attente</span><span class="sxs-lookup"><span data-stu-id="dedb9-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="dedb9-139">Pour insérer un message dans une file d'attente, utilisez la méthode **createMessage** afin de créer un message et de l'ajouter dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="dedb9-139">To insert a message into a queue, use the **createMessage** method to create a new message and add it to the queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="dedb9-140">Lecture furtive du message suivant</span><span class="sxs-lookup"><span data-stu-id="dedb9-140">How To: Peek at the Next Message</span></span>
<span data-ttu-id="dedb9-141">Vous pouvez lire furtivement le message au début de la file d'attente sans l'enlever de la file d'attente en appelant la méthode **peekMessages** .</span><span class="sxs-lookup"><span data-stu-id="dedb9-141">You can peek at the message in the front of a queue without removing it from the queue by calling the **peekMessages** method.</span></span> <span data-ttu-id="dedb9-142">Par défaut, **peekMessages** lit un seul message.</span><span class="sxs-lookup"><span data-stu-id="dedb9-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="dedb9-143">`result` contient le message.</span><span class="sxs-lookup"><span data-stu-id="dedb9-143">The `result` contains the message.</span></span>

> [!NOTE]
> <span data-ttu-id="dedb9-144">L’utilisation de **peekMessages** alors qu’il n’y a pas de message dans la file d’attente ne renvoie pas d’erreur, mais ne renvoie pas non plus de message.</span><span class="sxs-lookup"><span data-stu-id="dedb9-144">Using **peekMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="dedb9-145">Suppression du message suivant dans la file d'attente</span><span class="sxs-lookup"><span data-stu-id="dedb9-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="dedb9-146">Le traitement d'un message se fait en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="dedb9-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="dedb9-147">Enlever le message de la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="dedb9-147">Dequeue the message.</span></span>
2. <span data-ttu-id="dedb9-148">Supprimer le message.</span><span class="sxs-lookup"><span data-stu-id="dedb9-148">Delete the message.</span></span>

<span data-ttu-id="dedb9-149">Pour enlever un message de la file d’attente, utilisez **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="dedb9-149">To dequeue a message, use **getMessages**.</span></span> <span data-ttu-id="dedb9-150">Cela rend les messages invisibles dans la file d'attente, et aucun autre client ne peut les traiter.</span><span class="sxs-lookup"><span data-stu-id="dedb9-150">This makes the messages invisible in the queue, so no other clients can process them.</span></span> <span data-ttu-id="dedb9-151">Lorsque votre application a traité un message, appelez **deleteMessage** pour supprimer le message de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="dedb9-151">Once your application has processed a message, call **deleteMessage** to delete it from the queue.</span></span> <span data-ttu-id="dedb9-152">L'exemple suivant obtient un message, puis le supprime :</span><span class="sxs-lookup"><span data-stu-id="dedb9-152">The following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="dedb9-153">Par défaut, un message est masqué uniquement pendant 30 secondes avant d'être de nouveau visible pour les autres clients.</span><span class="sxs-lookup"><span data-stu-id="dedb9-153">By default, a message is only hidden for 30 seconds, after which it is visible to other clients.</span></span> <span data-ttu-id="dedb9-154">Vous pouvez indiquer une autre valeur en utilisant `options.visibilityTimeout` avec **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="dedb9-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="dedb9-155">L’utilisation de **getMessages** alors qu’il n’y a pas de message dans la file d’attente ne renvoie pas d’erreur, mais ne renvoie pas non plus de message.</span><span class="sxs-lookup"><span data-stu-id="dedb9-155">Using **getMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="dedb9-156">Modification du contenu d'un message en file d'attente</span><span class="sxs-lookup"><span data-stu-id="dedb9-156">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="dedb9-157">Vous pouvez changer le contenu d'un message qui se trouve dans la file d'attente en utilisant **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="dedb9-157">You can change the contents of a message in-place in the queue using **updateMessage**.</span></span> <span data-ttu-id="dedb9-158">L'exemple suivant met à jour le texte d'un message :</span><span class="sxs-lookup"><span data-stu-id="dedb9-158">The following example updates the text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got the message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="dedb9-159">Options supplémentaires pour la suppression des messages dans la file d'attente</span><span class="sxs-lookup"><span data-stu-id="dedb9-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="dedb9-160">Il existe deux méthodes pour personnaliser l'extraction d'un message d'une file d'attente :</span><span class="sxs-lookup"><span data-stu-id="dedb9-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="dedb9-161">`options.numOfMessages` - Extraire un lot de messages (jusqu’à 32).</span><span class="sxs-lookup"><span data-stu-id="dedb9-161">`options.numOfMessages` - Retrieve a batch of messages (up to 32.)</span></span>
* <span data-ttu-id="dedb9-162">`options.visibilityTimeout` - Définir une durée d’invisibilité plus longue ou plus courte.</span><span class="sxs-lookup"><span data-stu-id="dedb9-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="dedb9-163">L'exemple suivant utilise la méthode **getMessages** pour obtenir 15 messages dans un appel.</span><span class="sxs-lookup"><span data-stu-id="dedb9-163">The following example uses the **getMessages** method to get 15 messages in one call.</span></span> <span data-ttu-id="dedb9-164">Ensuite, il traite chaque message à l'aide d'une boucle for.</span><span class="sxs-lookup"><span data-stu-id="dedb9-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="dedb9-165">La durée d'invisibilité est passée à cinq minutes pour tous les messages renvoyés par cette méthode.</span><span class="sxs-lookup"><span data-stu-id="dedb9-165">It also sets the invisibility timeout to five minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="dedb9-166">Obtention de la longueur de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="dedb9-166">How To: Get the Queue Length</span></span>
<span data-ttu-id="dedb9-167">**getQueueMetadata** renvoie des métadonnées sur la file d'attente, y compris le nombre approximatif de messages en attente dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="dedb9-167">The **getQueueMetadata** returns metadata about the queue, including the approximate number of messages waiting in the queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="dedb9-168">Procédure : Affichage de la liste de disques</span><span class="sxs-lookup"><span data-stu-id="dedb9-168">How To: List Queues</span></span>
<span data-ttu-id="dedb9-169">Pour extraire une liste de files d'attente, utilisez **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="dedb9-169">To retrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="dedb9-170">Pour extraire une liste filtrée par un certain préfixe, utilisez **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="dedb9-170">To retrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains the list of queues
  }
});
```

<span data-ttu-id="dedb9-171">Si aucune file d’attente ne peut être renvoyée, `result.continuationToken` peut servir de premier paramètre de **listQueuesSegmented** ou de second paramètre de **listQueuesSegmentedWithPrefix** pour récupérer plus de résultats.</span><span class="sxs-lookup"><span data-stu-id="dedb9-171">If all queues cannot be returned, `result.continuationToken` can be used as the first parameter of **listQueuesSegmented** or the second parameter of **listQueuesSegmentedWithPrefix** to retrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="dedb9-172">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="dedb9-172">How To: Delete a Queue</span></span>
<span data-ttu-id="dedb9-173">Pour supprimer une file d'attente et tous les messages qu'elle contient, appelez la méthode **deleteQueue** sur l'objet file d'attente.</span><span class="sxs-lookup"><span data-stu-id="dedb9-173">To delete a queue and all the messages contained in it, call the **deleteQueue** method on the queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="dedb9-174">Pour effacer tous les messages d'une file d'attente sans supprimer cette dernière, utilisez **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="dedb9-174">To clear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="dedb9-175">Procédure : Utilisation des signatures d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="dedb9-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="dedb9-176">Les signatures d'accès partagé sont un moyen sécurisé de fournir un accès précis aux files d'attente sans fournir le nom ni les clés de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dedb9-176">Shared Access Signatures (SAS) are a secure way to provide granular access to queues without providing your storage account name or keys.</span></span> <span data-ttu-id="dedb9-177">Elles servent souvent à fournir un accès limité à vos files d'attente, par exemple pour autoriser une application mobile à soumettre des messages.</span><span class="sxs-lookup"><span data-stu-id="dedb9-177">SAS are often used to provide limited access to your queues, such as allowing a mobile app to submit messages.</span></span>

<span data-ttu-id="dedb9-178">Une application approuvée, comme un service cloud, génère une signature d’accès partagé à l’aide de **generateSharedAccessSignature** de **QueueService**, et la fournit à une application non approuvée ou à moitié approuvée.</span><span class="sxs-lookup"><span data-stu-id="dedb9-178">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **QueueService**, and provides it to an untrusted or semi-trusted application.</span></span> <span data-ttu-id="dedb9-179">Par exemple, une application mobile.</span><span class="sxs-lookup"><span data-stu-id="dedb9-179">For example, a mobile app.</span></span> <span data-ttu-id="dedb9-180">La signature d'accès partagé est générée à l'aide d'une stratégie, qui décrit les dates de début et de fin de validité de la signature, et le niveau d'accès accordé au détenteur de la signature.</span><span class="sxs-lookup"><span data-stu-id="dedb9-180">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="dedb9-181">L'exemple suivant génère une nouvelle stratégie d'accès partagé qui autorise le détenteur de la signature d'accès partagé à ajouter des messages à la file d'attente et expire 100 minutes après son heure de création.</span><span class="sxs-lookup"><span data-stu-id="dedb9-181">The following example generates a new shared access policy that will allow the SAS holder to add messages to the queue, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="dedb9-182">Notez que les informations sur l'hôte doivent également être fournies, car elles sont obligatoires lorsque le détenteur de la signature d'accès partagé tente d'accéder à la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="dedb9-182">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the queue.</span></span>

<span data-ttu-id="dedb9-183">L'application cliente utilise les signatures d'accès partagé avec **QueueServiceWithSAS** pour effectuer les opérations sur la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="dedb9-183">The client application then uses the SAS with **QueueServiceWithSAS** to perform operations against the queue.</span></span> <span data-ttu-id="dedb9-184">L'exemple suivant se connecte à la file d'attente et crée un message.</span><span class="sxs-lookup"><span data-stu-id="dedb9-184">The following example connects to the queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="dedb9-185">Comme la signature d'accès partagé a été générée avec un accès en ajout, une erreur sera renvoyée en cas de tentative de lecture, de mise à jour ou de suppression des messages.</span><span class="sxs-lookup"><span data-stu-id="dedb9-185">Since the SAS was generated with add access, if an attempt were made to read, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="dedb9-186">Listes de contrôle d'accès</span><span class="sxs-lookup"><span data-stu-id="dedb9-186">Access control lists</span></span>
<span data-ttu-id="dedb9-187">Vous pouvez également utiliser une liste de contrôle d'accès (ACL) pour définir la stratégie d'accès pour une signature d'accès partagé.</span><span class="sxs-lookup"><span data-stu-id="dedb9-187">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="dedb9-188">Cela est utile si vous voulez autoriser plusieurs clients à accéder à une file d'attente, mais fournir des stratégies d'accès différentes à chaque client.</span><span class="sxs-lookup"><span data-stu-id="dedb9-188">This is useful if you wish to allow multiple clients to access the queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="dedb9-189">Une liste de contrôle d'accès est implémentée à l'aide d'un tableau de stratégies d'accès, dans lequel un ID est associé à chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="dedb9-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="dedb9-190">L’exemple suivant définit deux stratégies ; une pour « user1 » et une pour « user2 » :</span><span class="sxs-lookup"><span data-stu-id="dedb9-190">The  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="dedb9-191">L’exemple suivant obtient la liste de contrôle d’accès active pour **myqueue**, puis ajoute les nouvelles stratégies à l’aide de **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="dedb9-191">The following example gets the current ACL for **myqueue**, then adds the new policies using **setQueueAcl**.</span></span> <span data-ttu-id="dedb9-192">Cette approche permet :</span><span class="sxs-lookup"><span data-stu-id="dedb9-192">This approach allows:</span></span>

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

<span data-ttu-id="dedb9-193">Lorsque la liste de contrôle d'accès est définie, vous pouvez créer une signature d'accès partagé basée sur l'ID pour une stratégie.</span><span class="sxs-lookup"><span data-stu-id="dedb9-193">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="dedb9-194">L'exemple suivant crée une signature d'accès partagé pour « user2 » :</span><span class="sxs-lookup"><span data-stu-id="dedb9-194">The following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="dedb9-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dedb9-195">Next Steps</span></span>
<span data-ttu-id="dedb9-196">Maintenant que vous connaissez les bases du stockage des files d'attente, consultez les liens suivants pour apprendre à exécuter les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="dedb9-196">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="dedb9-197">Consultez le [Blog de l’équipe Stockage Azure][Azure Storage Team Blog].</span><span class="sxs-lookup"><span data-stu-id="dedb9-197">Visit the [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="dedb9-198">Consultez le référentiel [Kit de développement logiciel (SDK) Stockage Azure pour Node][Azure Storage SDK for Node] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="dedb9-198">Visit the [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="dedb9-199">[Créer une application web Node.js dans Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="dedb9-199">[Create a Node.js web app in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="dedb9-200">[Application web Node.js avec le service de Table Azure]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span><span class="sxs-lookup"><span data-stu-id="dedb9-200">[Node.js web app using the Azure Table Service]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span></span>


<span data-ttu-id="dedb9-201">[Création et déploiement d’une application Node.js dans un service cloud Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span><span class="sxs-lookup"><span data-stu-id="dedb9-201">[Build and deploy a Node.js application to an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span></span>
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
<span data-ttu-id="dedb9-202">[Créer et déployer une application web Node.js dans Azure à l’aide de WebMatrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span><span class="sxs-lookup"><span data-stu-id="dedb9-202">[Build and deploy a Node.js web app to Azure using Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span></span>
