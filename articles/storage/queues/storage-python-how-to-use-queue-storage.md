---
title: "aaaHow toouse stockage de file d’attente à partir de Python | Documents Microsoft"
description: "Découvrez comment toouse hello du service de file d’attente Azure à partir de Python toocreate et supprimer des files d’attente et insérer, obtenir et supprimer les messages."
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
ms.openlocfilehash: f4f902a2c314401e5c1768fbc80566c8ba25c058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a><span data-ttu-id="6c64e-103">Comment toouse stockage de file d’attente à partir de Python</span><span class="sxs-lookup"><span data-stu-id="6c64e-103">How toouse Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="6c64e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6c64e-104">Overview</span></span>
<span data-ttu-id="6c64e-105">Ce guide vous explique comment tooperform des scénarios courants utilisant hello service de stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="6c64e-105">This guide shows you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="6c64e-106">exemples de Hello sont écrites dans Python et utiliser hello [le stockage Microsoft Azure SDK pour Python].</span><span class="sxs-lookup"><span data-stu-id="6c64e-106">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="6c64e-107">Hello scénarios abordés incluent **insertion**, **lecture**, **mise en route**, et **suppression** file d’attente de messages, ainsi que  **Création et suppression de files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="6c64e-107">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="6c64e-108">Pour plus d’informations sur les files d’attente, consultez toohello [étapes] section.</span><span class="sxs-lookup"><span data-stu-id="6c64e-108">For more information on queues, refer toohello [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="6c64e-109">Création d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="6c64e-109">How To: Create a Queue</span></span>
<span data-ttu-id="6c64e-110">Hello **QueueService** objet vous permet de travailler avec les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="6c64e-110">hello **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="6c64e-111">Hello de code suivant crée un **QueueService** objet.</span><span class="sxs-lookup"><span data-stu-id="6c64e-111">hello following code creates a **QueueService** object.</span></span> <span data-ttu-id="6c64e-112">Ajoutez les éléments suivants de hello haut hello de n’importe quel fichier Python dans lequel vous souhaitez tooprogrammatically accès Azure Storage :</span><span class="sxs-lookup"><span data-stu-id="6c64e-112">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="6c64e-113">Hello de code suivant crée un **QueueService** objet à l’aide de la clé de compte et le nom du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="6c64e-113">hello following code creates a **QueueService** object using hello storage account name and account key.</span></span> <span data-ttu-id="6c64e-114">Remplacez « myaccount » et « mykey » par le nom et la clé réels de votre compte.</span><span class="sxs-lookup"><span data-stu-id="6c64e-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="6c64e-115">Insertion d'un message dans une file d'attente</span><span class="sxs-lookup"><span data-stu-id="6c64e-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="6c64e-116">tooinsert un message dans une file d’attente, utilisez hello **put\_message** méthode pour créer un nouveau message et l’ajouter à la file d’attente de toohello.</span><span class="sxs-lookup"><span data-stu-id="6c64e-116">tooinsert a message into a queue, use hello **put\_message** method to create a new message and add it toohello queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="6c64e-117">Comment : Lire des hello Message suivant</span><span class="sxs-lookup"><span data-stu-id="6c64e-117">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="6c64e-118">Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **aperçu\_messages** (méthode).</span><span class="sxs-lookup"><span data-stu-id="6c64e-118">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages** method.</span></span> <span data-ttu-id="6c64e-119">Par défaut, **peek\_messages** lit furtivement un seul message.</span><span class="sxs-lookup"><span data-stu-id="6c64e-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="6c64e-120">Retrait des messages de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="6c64e-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="6c64e-121">Votre code supprime un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="6c64e-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="6c64e-122">Lorsque vous appelez **obtenir\_messages**, vous obtenez un message de type hello suivante dans une file d’attente par défaut.</span><span class="sxs-lookup"><span data-stu-id="6c64e-122">When you call **get\_messages**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="6c64e-123">Un message retourné à partir de **obtenir\_messages** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="6c64e-123">A message returned from **get\_messages** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="6c64e-124">Par défaut, ce message reste invisible pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="6c64e-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="6c64e-125">toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez également appeler **supprimer\_message**.</span><span class="sxs-lookup"><span data-stu-id="6c64e-125">toofinish removing hello message from hello queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="6c64e-126">Ce processus en deux étapes de la suppression d’un message garantit que lorsque votre code échoue tooprocess un message en raison d’une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et recommencez l’opération.</span><span class="sxs-lookup"><span data-stu-id="6c64e-126">This two-step process of removing a message assures that when your code fails tooprocess a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="6c64e-127">Votre code appelle **supprimer\_message** avec le bouton droit une fois le message de salutation a été traité.</span><span class="sxs-lookup"><span data-stu-id="6c64e-127">Your code calls **delete\_message** right after hello message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="6c64e-128">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="6c64e-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="6c64e-129">Tout d’abord, vous pouvez obtenir un lot de messages (haut too32).</span><span class="sxs-lookup"><span data-stu-id="6c64e-129">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="6c64e-130">Ensuite, vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message.</span><span class="sxs-lookup"><span data-stu-id="6c64e-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="6c64e-131">code Hello suivant utilise le **obtenir\_messages** messages tooget 16 de méthode dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="6c64e-131">hello following code example uses the **get\_messages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="6c64e-132">Ensuite, il traite chaque message à l'aide d'une boucle for.</span><span class="sxs-lookup"><span data-stu-id="6c64e-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="6c64e-133">Il définit également le délai d’attente de hello invisibilité à cinq minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="6c64e-133">It also sets hello invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="6c64e-134">Comment : Modifier hello du contenu d’un Message en file d’attente</span><span class="sxs-lookup"><span data-stu-id="6c64e-134">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="6c64e-135">Vous pouvez modifier le contenu de hello d’un message en place dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="6c64e-135">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="6c64e-136">Si le message représente une tâche de travail, vous pouvez utiliser cette fonctionnalité de tooupdate l’état de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="6c64e-136">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="6c64e-137">code Hello ci-dessous utilise hello **mettre à jour\_message** méthode tooupdate un message.</span><span class="sxs-lookup"><span data-stu-id="6c64e-137">hello code below uses hello **update\_message** method tooupdate a message.</span></span> <span data-ttu-id="6c64e-138">délai de visibilité Hello a la valeur too0, ce qui signifie que le message s’affiche immédiatement et hello de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="6c64e-138">hello visibility timeout is set too0, meaning the message appears immediately and hello content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="6c64e-139">Comment : Obtenir hello longueur de file d’attente</span><span class="sxs-lookup"><span data-stu-id="6c64e-139">How To: Get hello Queue Length</span></span>
<span data-ttu-id="6c64e-140">Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="6c64e-140">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="6c64e-141">Le **obtenir\_file d’attente\_métadonnées** méthode demande hello des métadonnées de tooreturn service de file d’attente sur la file d’attente hello et hello **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="6c64e-141">The **get\_queue\_metadata** method asks hello queue service tooreturn metadata about hello queue, and hello **approximate_message_count**.</span></span> <span data-ttu-id="6c64e-142">résultat de Hello est uniquement approximative, car les messages peuvent être ajoutées ou supprimées une fois le service de file d’attente répond tooyour demande.</span><span class="sxs-lookup"><span data-stu-id="6c64e-142">hello result is only approximate because messages can be added or removed after the queue service responds tooyour request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="6c64e-143">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="6c64e-143">How To: Delete a Queue</span></span>
<span data-ttu-id="6c64e-144">toodelete une file d’attente et tous les messages hello qu’il contient, appelez le **supprimer\_file d’attente** (méthode).</span><span class="sxs-lookup"><span data-stu-id="6c64e-144">toodelete a queue and all hello messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="6c64e-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c64e-145">Next Steps</span></span>
<span data-ttu-id="6c64e-146">Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="6c64e-146">Now that you've learned hello basics of Queue storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="6c64e-147">Centre de développement Python</span><span class="sxs-lookup"><span data-stu-id="6c64e-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="6c64e-148">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="6c64e-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="6c64e-149">[Blog de l'équipe Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="6c64e-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="6c64e-150">[le stockage Microsoft Azure SDK pour Python]</span><span class="sxs-lookup"><span data-stu-id="6c64e-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog de l'équipe Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/
[le stockage Microsoft Azure SDK pour Python]: https://github.com/Azure/azure-storage-python