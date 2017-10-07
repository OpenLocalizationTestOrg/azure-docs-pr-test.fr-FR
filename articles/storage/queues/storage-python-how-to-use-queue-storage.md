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
# <a name="how-toouse-queue-storage-from-python"></a>Comment toouse stockage de file d’attente à partir de Python
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Vue d'ensemble
Ce guide vous explique comment tooperform des scénarios courants utilisant hello service de stockage de file d’attente Azure. exemples de Hello sont écrites dans Python et utiliser hello [le stockage Microsoft Azure SDK pour Python]. Hello scénarios abordés incluent **insertion**, **lecture**, **mise en route**, et **suppression** file d’attente de messages, ainsi que  **Création et suppression de files d’attente**. Pour plus d’informations sur les files d’attente, consultez toohello [étapes] section.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a>Création d'une file d'attente
Hello **QueueService** objet vous permet de travailler avec les files d’attente. Hello de code suivant crée un **QueueService** objet. Ajoutez les éléments suivants de hello haut hello de n’importe quel fichier Python dans lequel vous souhaitez tooprogrammatically accès Azure Storage :

```python
from azure.storage.queue import QueueService
```

Hello de code suivant crée un **QueueService** objet à l’aide de la clé de compte et le nom du compte de stockage hello. Remplacez « myaccount » et « mykey » par le nom et la clé réels de votre compte.

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Insertion d'un message dans une file d'attente
tooinsert un message dans une file d’attente, utilisez hello **put\_message** méthode pour créer un nouveau message et l’ajouter à la file d’attente de toohello.

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a>Comment : Lire des hello Message suivant
Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **aperçu\_messages** (méthode). Par défaut, **peek\_messages** lit furtivement un seul message.

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a>Retrait des messages de la file d’attente
Votre code supprime un message d'une file d'attente en deux étapes. Lorsque vous appelez **obtenir\_messages**, vous obtenez un message de type hello suivante dans une file d’attente par défaut. Un message retourné à partir de **obtenir\_messages** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente. Par défaut, ce message reste invisible pendant 30 secondes. toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez également appeler **supprimer\_message**. Ce processus en deux étapes de la suppression d’un message garantit que lorsque votre code échoue tooprocess un message en raison d’une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et recommencez l’opération. Votre code appelle **supprimer\_message** avec le bouton droit une fois le message de salutation a été traité.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.
Tout d’abord, vous pouvez obtenir un lot de messages (haut too32). Ensuite, vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message. code Hello suivant utilise le **obtenir\_messages** messages tooget 16 de méthode dans un seul appel. Ensuite, il traite chaque message à l'aide d'une boucle for. Il définit également le délai d’attente de hello invisibilité à cinq minutes pour chaque message.

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Comment : Modifier hello du contenu d’un Message en file d’attente
Vous pouvez modifier le contenu de hello d’un message en place dans la file d’attente hello. Si le message représente une tâche de travail, vous pouvez utiliser cette fonctionnalité de tooupdate l’état de tâche hello. code Hello ci-dessous utilise hello **mettre à jour\_message** méthode tooupdate un message. délai de visibilité Hello a la valeur too0, ce qui signifie que le message s’affiche immédiatement et hello de mise à jour.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a>Comment : Obtenir hello longueur de file d’attente
Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente. Le **obtenir\_file d’attente\_métadonnées** méthode demande hello des métadonnées de tooreturn service de file d’attente sur la file d’attente hello et hello **approximate_message_count**. résultat de Hello est uniquement approximative, car les messages peuvent être ajoutées ou supprimées une fois le service de file d’attente répond tooyour demande.

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a>Suppression d'une file d'attente
toodelete une file d’attente et tous les messages hello qu’il contient, appelez le **supprimer\_file d’attente** (méthode).

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente, suivez ces liens de toolearn plus.

* [Centre de développement Python](/develop/python/)
* [API REST des services d’Azure Storage](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog de l'équipe Azure Storage]
* [le stockage Microsoft Azure SDK pour Python]

[Blog de l'équipe Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/
[le stockage Microsoft Azure SDK pour Python]: https://github.com/Azure/azure-storage-python