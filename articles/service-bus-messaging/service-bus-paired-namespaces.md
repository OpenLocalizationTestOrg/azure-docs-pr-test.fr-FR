---
title: "aaaAzure Service Bus associé d’espaces de noms | Documents Microsoft"
description: "Détails sur l'implémentation de l'espace de noms associé et coût"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2440c8d3-ed2e-47e0-93cf-ab7fbb855d2e
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: 4c44b2b95d2228e1ad8075b52634d88a1593d3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="paired-namespace-implementation-details-and-cost-implications"></a>Détails sur l'implémentation de l'espace de noms associé et implications en termes de coût
Hello [PairNamespaceAsync] [ PairNamespaceAsync] (méthode), à l’aide un [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] d’une instance, effectue des tâches visibles à votre place. Coût lorsque vous utilisez la fonctionnalité de hello, il est utile toounderstand ces tâches afin que vous attendez le comportement de hello lorsque cela se produit. Hello API engage hello suivant comportement automatique à votre place :

* Création de files d'attente de travaux en souffrance.
* La création d’un [MessageSender] [ MessageSender] objet qui communique avec tooqueues ou aux rubriques.
* Lorsqu’une entité de messagerie devient indisponible, envoie messages ping toohello entité dans un toodetect tentative lorsque cette entité est à nouveau disponible.
* Création éventuelle d’un ensemble de « pompes de messages » que déplacer les messages à partir de hello files d’attente du backlog files d’attente toohello principal.
* Coordonne la clôture/défaillance de hello principaux et secondaire [MessagingFactory] [ MessagingFactory] instances.

À un niveau élevé, la fonctionnalité de hello fonctionne comme suit : lors de l’entité principale de hello est intègre, aucun changement de comportement se produit. Hello lorsque [FailoverInterval] [ FailoverInterval] durée écoulée, et entité principale de hello ne voit aucun envoi réussi après non temporaire [MessagingException] [ MessagingException] ou un [TimeoutException][TimeoutException], hello suivant comportement se produit :

1. Envoyer des opérations toohello principal entité sont désactivées et les tests ping système hello hello entité principale jusqu'à ce que les commandes ping aboutissent correctement.
2. Une file d'attente de travaux en souffrance aléatoire est sélectionnée.
3. [BrokeredMessage] [ BrokeredMessage] objets sont routé toohello choisi de file d’attente.
4. Si un toohello d’opération envoi choisi de file d’attente échoue, cette file d’attente est extraite de la rotation de hello et une file d’attente est sélectionné. Tous les expéditeurs sur hello [MessagingFactory] [ MessagingFactory] instance apprendre de défaillance de hello.

Hello suivant chiffres représentent séquence de hello. Tout d’abord, l’expéditeur de hello envoie des messages.

![Espaces de noms associés][0]

Sur la file d’attente de la fonctionnalité principale de toohello d’échec toosend, l’expéditeur de hello commence à envoyer des tooa messages sélectionné aléatoire de file d’attente. Simultanément, il démarre une tâche ping.

![Espaces de noms associés][1]

À ce stade, les messages hello sont toujours dans la file d’attente secondaire de hello et toohello la file d’attente principale n’ont pas été remis. Une fois que la file d’attente principale de hello est à nouveau intègre, au moins un processus doit être exécuté SIPHON de hello. SIPHON de Hello remet les messages de hello de hello toutes les différentes backlog entités de destination appropriées de files d’attente toohello (files d’attente et rubriques).

![Espaces de noms associés][2]

Hello reste de cette rubrique présente des détails spécifiques hello du fonctionnement de ces éléments.

## <a name="creation-of-backlog-queues"></a>Création de files d'attente de travaux en souffrance
Hello [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] objet passé toohello [PairNamespaceAsync] [ PairNamespaceAsync] méthode indique hello nombre de file d’attente des files d’attente vous souhaitez toouse. Chaque file d’attente est alors créée avec hello propriétés suivantes explicitement défini (toutes les autres valeurs sont définies toohello [QueueDescription] [ QueueDescription] par défaut) :

| Chemin | [primary namespace]/x-servicebus-transfer/[index] où [index] est une valeur dans [0, BacklogQueueCount) |
| --- | --- |
| MaxSizeInMegabytes |5120 |
| MaxDeliveryCount |int.MaxValue |
| DefaultMessageTimeToLive |TimeSpan.MaxValue |
| AutoDeleteOnIdle |TimeSpan.MaxValue |
| LockDuration |1 minute |
| EnableDeadLetteringOnMessageExpiration |true |
| EnableBatchedOperations |true |

Par exemple, hello première file d’attente créée pour l’espace de noms **contoso** est nommé `contoso/x-servicebus-transfer/0`.

Lors de la création des files d’attente hello, code de hello vérifie d’abord toosee si une file d’attente existe. Si la file d’attente hello n’existe pas, la file d’attente hello est créé. n’est pas le cas du code de Hello nettoyer les files d’attente de la file d’attente « supplémentaire ». Plus précisément, si hello application hello espace de noms principal **contoso** demande cinq files d’attente du backlog, mais une file d’attente du backlog avec le chemin d’accès hello `contoso/x-servicebus-transfer/7` existe, cette file d’attente excédentaire reste présente, mais n’est pas utilisé. système de Hello autorise explicitement tooexist de files d’attente du backlog supplémentaires qui ne serait utilisée. En tant que propriétaire d’espace de noms hello, vous êtes chargé de nettoyer les files d’attente de la file d’attente inutilisées ou indésirables. Hello pour prendre cette décision parce que le Service Bus ne peut pas savoir quelles fins existent pour toutes les files d’attente de hello dans votre espace de noms. En outre, si une file d’attente existe avec le nom donné de hello mais ne répond pas aux hello supposé [QueueDescription][QueueDescription], puis votre raisons sont les vôtre pour modification par défaut hello. Ne sont nullement garanties pour les files d’attente du backlog de modifications toohello par votre code. Modifiez tootest vraiment soigneusement.

## <a name="custom-messagesender"></a>MessageSender personnalisé
Lors de l’envoi, tous les messages passent par interne [MessageSender] [ MessageSender] objet qui se comporte normalement lorsque tout fonctionne et redirige les files d’attente du backlog toohello en «. » Lors de la réception d'une défaillance non temporaire, une minuterie démarre. Après un [TimeSpan] [ TimeSpan] période consistant à hello [FailoverInterval] [ FailoverInterval] au cours de laquelle aucun message de réussite est envoyé de valeur de propriété , hello basculement est engagé. À ce stade, hello événements suivants se produisent pour chaque entité :

* Une tâche ping exécute chaque [PingPrimaryInterval] [ PingPrimaryInterval] toocheck si l’entité de hello est disponible. Une fois cette tâche accomplie, tout le code client qui utilise les entités hello immédiatement commence à envoyer de nouveaux messages toohello espace de noms principal.
* Toothat toosend de futures demandes même entité à partir de n’importe quel autre expéditeur entraîne hello [BrokeredMessage] [ BrokeredMessage] envoyé toobe modifié toosit dans la file d’attente du backlog hello. modification de Hello supprime certaines propriétés hello [BrokeredMessage] [ BrokeredMessage] de l’objet et les stocke ailleurs. Hello propriétés suivantes sont effacées et ajoutées sous un nouvel alias, ce qui permet Service Bus et hello SDK tooprocess messages uniformément :

| Nom de l'ancienne propriété | Nom de la nouvelle propriété |
| --- | --- |
| SessionId |x-ms-sessionid |
| TimeToLive |x-ms-timetolive |
| ScheduledEnqueueTimeUtc |x-ms-path |

chemin d’accès de destination d’origine Hello est également stockée dans le message de type hello en tant que propriété nommée x-ms-chemin d’accès. Cette conception permet de messages pour nombreuses entités toocoexist dans une file d’attente unique. propriétés de Hello sont traduites par SIPHON de hello.

Hello personnalisé [MessageSender] [ MessageSender] objet peut rencontrer des problèmes lorsque les messages approchent de limite de 256 Ko hello et le basculement est activé. Hello personnalisé [MessageSender] [ MessageSender] objet stocke des messages pour toutes les files d’attente et rubriques dans les files d’attente du backlog hello. Cet objet combine des messages à partir de nombreuses couleurs primaires ensemble dans les files d’attente du backlog hello. toohandle équilibrage de charge entre plusieurs clients qui ne connaissez pas chaque hello autre, Kit de développement logiciel de façon aléatoire choisit une file d’attente du backlog pour chaque [QueueClient] [ QueueClient] ou [TopicClient] [ TopicClient] vous créez dans le code.

## <a name="pings"></a>Tests ping
Un message ping est vide [BrokeredMessage] [ BrokeredMessage] avec son [ContentType] [ ContentType] propriété définie tooapplication/vnd.ms-servicebus-ping et un [TimeToLive] [ TimeToLive] valeur de 1 seconde. Cette commande ping présente une caractéristique particulière dans Service Bus : hello serveur ne remet jamais une commande ping quand un appelant demande une [BrokeredMessage][BrokeredMessage]. Par conséquent, vous n’avez jamais toolearn comment tooreceive et ignorer ces messages. Chaque entité (file d’attente unique ou rubrique) par [MessagingFactory] [ MessagingFactory] sera être exécutée sur une instance par le client lorsqu’ils sont considérées toobe indisponible. Par défaut, cela se produit une fois par minute. Messages ping sont considérés comme des messages de Service Bus toobe standard et peuvent entraîner des frais liés à la bande passante et les messages. Dès que les clients de hello détectent que le système de hello est disponible, les messages de type hello arrêtent.

## <a name="hello-syphon"></a>SIPHON de Hello
Au moins un programme exécutable de l’application hello doit exécuter activement SIPHON de hello. SIPHON de Hello effectue un long réception d’interrogation qui dure 15 minutes. Lorsque toutes les entités sont disponibles et que vous avez 10 files d’attente du backlog, hello application qui héberge les appels de siphon hello hello réception opération 40 fois par heure, 960 fois par jour et 28 800 fois en 30 jours. Lorsque le siphon de hello déplace activement des messages à partir de la file d’attente principale hello backlog toohello, chaque message occasionne hello suivant frais (frais standards de taille des messages et la bande passante s’appliquent à toutes les étapes) :

1. Toohello file d’attente d’envoi.
2. Réception à partir de la file d’attente hello.
3. Envoyer toohello principal.
4. Réception de hello principal.

## <a name="closefault-behavior"></a>Comportement de fermeture/erreur
Dans une application qui héberge le siphon de hello, une fois les hello principal ou secondaire [MessagingFactory] [ MessagingFactory] défaillance ou est fermée sans son partenaire également est défaillant ou fermé et le hello SIPHON détecte cet état , fait Office de siphon de hello. Si des autres hello [MessagingFactory] [ MessagingFactory] n’est pas fermée dans les 5 secondes, SIPHON de hello entraîne une défaillance hello encore ouverte [MessagingFactory] [ MessagingFactory] .

## <a name="next-steps"></a>Étapes suivantes
Consultez [Modèles de messagerie asynchrone et haute disponibilité][Asynchronous messaging patterns and high availability] pour une discussion détaillée sur la messagerie asynchrone de Service Bus. 

[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[FailoverInterval]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions#Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_FailoverInterval
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[TimeoutException]: https://msdn.microsoft.com/library/azure/system.timeoutexception.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[TimeSpan]: https://msdn.microsoft.com/library/azure/system.timespan.aspx
[PingPrimaryInterval]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_PingPrimaryInterval
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[ContentType]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType
[TimeToLive]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md
[0]: ./media/service-bus-paired-namespaces/IC673405.png
[1]: ./media/service-bus-paired-namespaces/IC673406.png
[2]: ./media/service-bus-paired-namespaces/IC673407.png
