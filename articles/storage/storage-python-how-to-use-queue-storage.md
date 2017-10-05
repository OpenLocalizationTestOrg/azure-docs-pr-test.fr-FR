---
title: "Utilisation du stockage de files d’attente à partir de Python | Microsoft Docs"
description: "Découvrez comment utiliser le service de File d’attente Azure à partir de Python pour créer et supprimer des files d’attente, ainsi que pour insérer, récupérer et supprimer des messages."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 1ad3ba6853edda93034b84996823262cb017c71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-python"></a><span data-ttu-id="5e6b9-103">Utilisation du stockage de files d'attente à partir de Python</span><span class="sxs-lookup"><span data-stu-id="5e6b9-103">How to use Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="5e6b9-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5e6b9-104">Overview</span></span>
<span data-ttu-id="5e6b9-105">Ce guide décrit le déroulement de scénarios courants dans le cadre de l'utilisation du service de stockage de files d'attente Azure.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-105">This guide shows you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="5e6b9-106">Les exemples sont écrits en Python et utilisent le [Kit de développement logiciel (SDK) Microsoft Azure Storage pour Python].</span><span class="sxs-lookup"><span data-stu-id="5e6b9-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="5e6b9-107">Les scénarios traités incluent **l’insertion**, la **lecture furtive**, la **récupération** et la **suppression** des messages de file d’attente, ainsi que la **création et suppression des files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-107">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="5e6b9-108">Pour plus d’informations sur les files d’attente, consultez la section [Étapes suivantes].</span><span class="sxs-lookup"><span data-stu-id="5e6b9-108">For more information on queues, refer to the [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="5e6b9-109">Création d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="5e6b9-109">How To: Create a Queue</span></span>
<span data-ttu-id="5e6b9-110">L'objet **QueueService** permet d'utiliser des files d'attente.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-110">The **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="5e6b9-111">Le code suivant permet de créer un objet **QueueService** .</span><span class="sxs-lookup"><span data-stu-id="5e6b9-111">The following code creates a **QueueService** object.</span></span> <span data-ttu-id="5e6b9-112">Ajoutez ce qui suit vers le début de chaque fichier Python dans lequel vous souhaitez accéder à Azure Storage par programme :</span><span class="sxs-lookup"><span data-stu-id="5e6b9-112">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="5e6b9-113">Le code suivant permet de créer un objet **QueueService** en utilisant le nom et la clé du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-113">The following code creates a **QueueService** object using the storage account name and account key.</span></span> <span data-ttu-id="5e6b9-114">Remplacez « myaccount » et « mykey » par le nom et la clé réels de votre compte.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="5e6b9-115">Insertion d'un message dans une file d'attente</span><span class="sxs-lookup"><span data-stu-id="5e6b9-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="5e6b9-116">Pour insérer un message dans une file d’attente, utilisez la méthode **put\_message** pour créer un nouveau message et l’ajouter à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-116">To insert a message into a queue, use the **put\_message** method to create a new message and add it to the queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="5e6b9-117">Lecture furtive du message suivant</span><span class="sxs-lookup"><span data-stu-id="5e6b9-117">How To: Peek at the Next Message</span></span>
<span data-ttu-id="5e6b9-118">Vous pouvez lire furtivement le message au début de la file d’attente sans l’enlever de la file d’attente en appelant la méthode **peek\_messages**.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-118">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages** method.</span></span> <span data-ttu-id="5e6b9-119">Par défaut, **peek\_messages** lit furtivement un seul message.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="5e6b9-120">Retrait des messages de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="5e6b9-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="5e6b9-121">Votre code supprime un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="5e6b9-122">Lorsque vous appelez **get\_messages**, vous obtenez le message suivant dans une file d’attente par défaut.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-122">When you call **get\_messages**, you get the next message in a queue by default.</span></span> <span data-ttu-id="5e6b9-123">Un message renvoyé par **get\_messages** devient invisible par les autres codes lisant les messages de cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-123">A message returned from **get\_messages** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="5e6b9-124">Par défaut, ce message reste invisible pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="5e6b9-125">Pour finaliser la suppression du message de la file d’attente, vous devez aussi appeler **delete\_message**.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-125">To finish removing the message from the queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="5e6b9-126">Ce processus de suppression d’un message en deux étapes garantit que, si votre code ne parvient pas à traiter un message à cause d’une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et réessayer.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-126">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="5e6b9-127">Votre code appelle **delete\_message** juste après le traitement du message.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-127">Your code calls **delete\_message** right after the message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="5e6b9-128">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="5e6b9-129">Premièrement, vous pouvez obtenir un lot de messages (jusqu'à 32).</span><span class="sxs-lookup"><span data-stu-id="5e6b9-129">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="5e6b9-130">Deuxièmement, vous pouvez définir un délai d'expiration de l'invisibilité plus long ou plus court afin d'accorder à votre code plus ou moins de temps pour traiter complètement chaque message.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="5e6b9-131">L’exemple de code suivant utilise la méthode **get\_messages** pour obtenir 16 messages en un appel.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-131">The following code example uses the **get\_messages** method to get 16 messages in one call.</span></span> <span data-ttu-id="5e6b9-132">Ensuite, il traite chaque message à l'aide d'une boucle for.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="5e6b9-133">Il définit également le délai d'expiration de l'invisibilité sur cinq minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-133">It also sets the invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="5e6b9-134">Modification du contenu d'un message en file d'attente</span><span class="sxs-lookup"><span data-stu-id="5e6b9-134">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="5e6b9-135">Vous pouvez modifier le contenu d'un message placé dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-135">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="5e6b9-136">Si le message représente une tâche, vous pouvez utiliser cette fonctionnalité pour mettre à jour l'état de la tâche.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-136">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="5e6b9-137">Le code ci-dessous utilise la méthode **update\_message** pour mettre à jour un message.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-137">The code below uses the **update\_message** method to update a message.</span></span> <span data-ttu-id="5e6b9-138">Ce délai de visibilité est défini sur 0, ce qui signifie que le message s’affiche immédiatement et que le contenu est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-138">The visibility timeout is set to 0, meaning the message appears immediately and the content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="5e6b9-139">Obtention de la longueur de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="5e6b9-139">How To: Get the Queue Length</span></span>
<span data-ttu-id="5e6b9-140">Vous pouvez obtenir une estimation du nombre de messages dans une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-140">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="5e6b9-141">La méthode **get\_queue\_metadata** demande au service de File d’attente de renvoyer les métadonnées relatives à la file d’attente, et la valeur **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-141">The **get\_queue\_metadata** method asks the queue service to return metadata about the queue, and the **approximate_message_count**.</span></span> <span data-ttu-id="5e6b9-142">Le résultat est seulement approximatif, car des messages peuvent être ajoutés ou supprimés après que le service de file d'attente a répondu à votre demande.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-142">The result is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="5e6b9-143">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="5e6b9-143">How To: Delete a Queue</span></span>
<span data-ttu-id="5e6b9-144">Pour supprimer une file d’attente et tous les messages qu’elle contient, appelez la méthode **delete\_queue**.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-144">To delete a queue and all the messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="5e6b9-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e6b9-145">Next Steps</span></span>
<span data-ttu-id="5e6b9-146">Maintenant que vous connaissez les bases du stockage de files d’attente, consultez les liens suivants pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="5e6b9-146">Now that you've learned the basics of Queue storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="5e6b9-147">Centre de développement Python</span><span class="sxs-lookup"><span data-stu-id="5e6b9-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="5e6b9-148">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5e6b9-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="5e6b9-149">[Blog de l'équipe Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="5e6b9-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="5e6b9-150">[Kit de développement logiciel (SDK) Microsoft Azure Storage pour Python]</span><span class="sxs-lookup"><span data-stu-id="5e6b9-150">[Microsoft Azure Storage SDK for Python]</span></span>

<span data-ttu-id="5e6b9-151">[Blog de l'équipe Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/</span><span class="sxs-lookup"><span data-stu-id="5e6b9-151">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/</span></span>
<span data-ttu-id="5e6b9-152">[Kit de développement logiciel (SDK) Microsoft Azure Storage pour Python]: https://github.com/Azure/azure-storage-python</span><span class="sxs-lookup"><span data-stu-id="5e6b9-152">[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python</span></span>