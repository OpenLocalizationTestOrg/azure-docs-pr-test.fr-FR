---
title: rubriques de Azure Service Bus aaaHow toouse avec Python | Documents Microsoft
description: "Découvrez comment toouse Azure Service Bus rubriques et abonnements à partir de Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a>Comment toouse Service Bus rubriques et les abonnements avec Python

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Cet article décrit comment toouse Service Bus rubriques et abonnements. exemples de Hello sont écrites dans Python et utiliser hello [package SDK de Python Azure][Azure Python package]. Hello scénarios abordés incluent **création de rubriques et abonnements**, **création de filtres d’abonnement**, **envoi rubrique tooa de messages**, **réception les messages à partir d’un abonnement**, et **suppression des rubriques et abonnements**. Pour plus d’informations sur les rubriques et les abonnements, consultez hello [étapes](#next-steps) section.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> Si vous avez besoin tooinstall Python ou hello [package Azure Python][Azure Python package], consultez hello [Guide d’Installation de Python](../python-how-to-install.md).

## <a name="create-a-topic"></a>Création d'une rubrique
Hello **ServiceBusService** objet vous permet de toowork aux rubriques. Ajoutez les éléments suivants de hello haut hello de n’importe quel fichier Python dans lequel vous souhaitez tooprogrammatically accès Service Bus :

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

Hello de code suivant crée un **ServiceBusService** objet. Remplacez `mynamespace`, `sharedaccesskeyname` et `sharedaccesskey` par un espace de noms, un nom et une valeur de clé de signature d’accès partagé (SAP) réels.

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Vous pouvez obtenir les valeurs hello pour le nom de la clé SAS hello et la valeur à partir de hello [portail Azure][Azure portal].

```python
bus_service.create_topic('mytopic')
```

Hello `create_topic` méthode prend également en charge des options supplémentaires, qui permettent de paramètres de rubrique toooverride par défaut comme taille de rubrique toolive ou maximale de temps de message. Hello exemple suivant définit hello rubrique maximale taille too5 Go et heure toolive (TTL) de 1 minute :

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a>Création d’abonnements
Abonnements tootopics sont également créés par hello **ServiceBusService** objet. Les abonnements sont nommés et peuvent avoir un filtre facultatif qui limite l’ensemble hello de messages remis de file d’attente virtuelle de l’abonnement toohello.

> [!NOTE]
> Abonnements sont persistantes et continuent jusqu'à ce que soit leur tooexist ou hello rubrique toowhich êtes abonné, elles sont supprimées.
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Créer un abonnement avec le filtre par défaut (MatchAll) hello
Hello **MatchAll** filtre est hello par défaut qui est utilisé si aucun filtre n’est spécifiée lors de la création d’un abonnement. Hello lorsque **MatchAll** filtre est utilisé, la rubrique de toohello publié tous les messages sont placés dans la file d’attente virtuelle de l’abonnement hello. Hello exemple suivant crée un abonnement nommé `AllMessages` et utilise hello par défaut **MatchAll** filtre.

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a>Création d’abonnements avec des filtres
Vous pouvez également définir des filtres qui vous permettent de toospecify lesquelles messages envoyés tooa rubrique doit apparaître dans un abonnement à une rubrique spécifique.

Bonjour type de filtre pris en charge par les abonnements plus souple est un **SqlFilter**, qui implémente un sous-ensemble de SQL92. Filtres SQL fonctionnent sur les propriétés hello de messages hello qui sont publiées toohello rubrique. Pour plus d’informations sur les expressions hello qui peut être utilisé avec un filtre SQL, consultez hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxe.

Vous pouvez ajouter des filtres tooa abonnement à l’aide de hello **créer\_règle** méthode Hello **ServiceBusService** objet. Cette méthode vous permet d’abonnement existant tooadd nouveaux filtres tooan.

> [!NOTE]
> Étant donné que le filtre par défaut de hello est appliqué automatiquement tooall nouveaux abonnements, vous devez d’abord supprimer filtre par défaut de hello ou hello **MatchAll** remplace tous les autres filtres que vous pouvez spécifier. Vous pouvez supprimer la règle par défaut de hello à l’aide de hello `delete_rule` méthode Hello **ServiceBusService** objet.
> 
> 

Hello exemple suivant crée un abonnement nommé `HighMessages` avec un **SqlFilter** qui sélectionne uniquement les messages qui ont personnalisé `messagenumber` propriété supérieure à 3 :

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

De même, hello exemple suivant crée un abonnement nommé `LowMessages` avec un **SqlFilter** qui sélectionne uniquement les messages qui ont un `messagenumber` propriété inférieur ou égal too3 :

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

Désormais, lorsqu’un message est envoyé trop`mytopic` qu’il est toujours remis tooreceivers abonné toohello **AllMessages** abonnement à une rubrique et remis de manière sélective tooreceivers abonné toohello **HighMessages**  et **LowMessages** abonnements à la rubrique (selon le contenu du message hello).

## <a name="send-messages-tooa-topic"></a>Rubrique tooa de messages d’envoi
toosend une rubrique de Service Bus message tooa, votre application doit utiliser hello `send_topic_message` méthode Hello **ServiceBusService** objet.

Hello exemple suivant montre comment le test de toosend cinq messages trop`mytopic`. Notez que hello `messagenumber` varie en fonction de valeur de la propriété de chaque message sur l’itération hello de boucle de hello (détermine les abonnements reçoivent) :

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

Rubriques Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md). en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko. Il n’existe aucune limite sur le nombre de hello de messages conservés dans une rubrique mais hello de taille totale des messages hello détenus par une rubrique est une extrémité de fin. Cette taille de rubrique est définie au moment de la création. La limite maximale est de 5 Go. Pour plus d’informations sur les quotas, consultez [Quotas Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Réception des messages d’un abonnement
Les messages sont reçus à partir d’un abonnement à l’aide de hello `receive_subscription_message` méthode sur hello **ServiceBusService** objet :

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

Les messages sont supprimés de l’abonnement de hello lorsqu’elles sont lues lorsque hello paramètre `peek_lock` est défini trop**False**. Vous pouvez lire (aperçu) et verrouiller le message de type hello sans le supprimer de la file d’attente hello en définissant le paramètre hello `peek_lock` trop**True**.

Hello le comportement de la lecture et de suppression de message de type hello comme partie de hello opération de réception est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec. toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter. Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.

Si hello `peek_lock` paramètre est défini trop**True**, hello réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application. Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant `delete` méthode sur hello **Message** objet. Hello `delete` méthode marque le message de type hello comme ayant été consommé et le supprime de l’abonnement de hello.

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Comment toohandle application tombe en panne et messages illisibles
Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message. Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlock` méthode sur hello **Message** objet. Cette opération provoquent le message de type hello toounlock Service Bus au sein de l’abonnement de hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.

Il existe également un délai d’attente d’un message verrouillé au sein de l’abonnement de hello, et si l’application hello échoue le message de type hello tooprocess avant de délai d’attente de verrou hello expire (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille le message de type hello automatiquement et le rend disponible toobe de nouveau reçu.

Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `delete` méthode est appelée, puis le message de type hello sera redistribué toohello application lors de son redémarrage. Cela est souvent appelé *au moins une fois le traitement*, autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué. Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message. Cela est souvent obtenue à l’aide de hello **MessageId** propriété de message de type hello, qui reste constante entre les tentatives de remise.

## <a name="delete-topics-and-subscriptions"></a>Suppression de rubriques et d'abonnements
Rubriques et les abonnements sont persistants et doivent être explicitement supprimés via hello [portail Azure] [ Azure portal] ou par programme. Hello suivant montre comment la rubrique de hello toodelete nommé `mytopic`:

```python
bus_service.delete_topic('mytopic')
```

Suppression d’une rubrique supprime également tous les abonnements qui sont inscrits auprès de rubrique de hello. Les abonnements peuvent aussi être supprimés de manière indépendante. Hello de code suivant montre comment toodelete un abonnement nommé `HighMessages` de hello `mytopic` rubrique :

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello des rubriques Service Bus, suivez ces liens de toolearn plus.

* Consultez [Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions].
* Référence pour [SqlFilter.SqlExpression][SqlFilter.SqlExpression].

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
