---
title: "les files d’attente d’aaaHow toouse Azure Service Bus avec Python | Documents Microsoft"
description: "Découvrez comment toouse Azure Service Bus de files d’attente à partir de Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a>Comment toouse Service Bus de files d’attente avec Python

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Cet article décrit comment les files d’attente de toouse Service Bus. exemples de Hello sont écrites dans Python et utiliser hello [package Python Azure Service Bus][Python Azure Service Bus package]. Hello scénarios abordés incluent **création de files d’attente, envoyer et recevoir des messages**, et **la suppression de files d’attente**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> tooinstall Python ou hello [package Python Azure Service Bus][Python Azure Service Bus package], consultez hello [Guide d’Installation de Python](../python-how-to-install.md).
> 
> 

## <a name="create-a-queue"></a>Création d’une file d’attente
Hello **ServiceBusService** objet vous permet de toowork avec les files d’attente. Ajoutez hello suivant code haut hello de n’importe quel fichier Python dans lequel vous souhaitez tooprogrammatically accès Service Bus :

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

Hello de code suivant crée un **ServiceBusService** objet. Remplacez `mynamespace`, `sharedaccesskeyname` et `sharedaccesskey` par votre espace de noms, le nom et la valeur de clé de signature d’accès partagé (SAP).

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Hello valeurs pour le nom de la clé SAS hello et valeur sont accessibles dans hello [portail Azure] [ Azure portal] informations de connexion, ou dans Visual Studio de hello **propriétés** volet lors de la sélection Bonjour espace de noms Service Bus dans l’Explorateur de serveurs (comme indiqué dans la section précédente de hello).

```python
bus_service.create_queue('taskqueue')
```

Hello `create_queue` méthode prend également en charge des options supplémentaires, qui vous permettent de paramètres de file d’attente par défaut toooverride telles que message toolive TTL (time) ou taille maximale de file d’attente. Hello exemple suivant définit hello file d’attente maximale taille too5 Go et à la minute de too1 de valeur de durée de vie hello :

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a>Envoyer la file d’attente de messages tooa
toosend une file d’attente Service Bus de messages tooa, votre application appelle hello `send_queue_message` méthode sur hello **ServiceBusService** objet.

Hello exemple suivant montre comment toosend une file d’attente toohello test nommé `taskqueue` à l’aide de `send_queue_message`:

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

Les files d’attente Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md). en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko. Il n’existe aucune limite du nombre de hello de messages dans une file d’attente mais hello de taille totale des messages hello détenus par une file d’attente est une extrémité de fin. Cette taille de file d'attente est définie au moment de la création. La limite maximale est de 5 Go. Pour plus d’informations sur les quotas, consultez [Quotas Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Réception des messages d'une file d'attente
Les messages sont reçus à partir d’une file d’attente à l’aide de hello `receive_queue_message` méthode sur hello **ServiceBusService** objet :

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

Les messages sont supprimés de la file d’attente hello lorsqu’elles sont lues lorsque hello paramètre `peek_lock` est défini trop**False**. Vous pouvez lire (aperçu) et verrouiller le message de type hello sans le supprimer de la file d’attente hello en définissant le paramètre hello `peek_lock` trop**True**.

Hello le comportement de la lecture et de suppression de message de type hello comme partie de hello opération de réception est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec. toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter. Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.

Si hello `peek_lock` paramètre est défini trop**True**, hello réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application. Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant hello **supprimer** méthode sur hello **Message** objet. Hello **supprimer** méthode marquer le message de type hello comme ayant été consommé et supprimez-le de la file d’attente hello.

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Comment toohandle application tombe en panne et messages illisibles
Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message. Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello **déverrouiller** méthode sur hello **Message** objet. Cette opération provoquent le message de type hello toounlock Service Bus au sein de la file d’attente hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.

Il existe également un délai d’attente d’un message verrouillé dans la file d’attente hello, et si l’échec de l’application hello tooprocess hello message avant hello délai d’attente de verrou expire (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.

Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello **supprimer** méthode est appelée, puis le message de type hello sera redistribué toohello application lors de son redémarrage. Cela est souvent appelé **au moins une fois le traitement**, autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué. Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message. Cela est souvent obtenue à l’aide de hello **MessageId** propriété de message de type hello, qui reste constante entre les tentatives de remise.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de files d’attente Service Bus, consultez ces articles de toolearn plus.

* [Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions]

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

