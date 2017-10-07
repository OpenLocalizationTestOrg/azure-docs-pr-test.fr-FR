---
title: "pratiques aaaBest pour améliorer les performances à l’aide d’Azure Service Bus | Documents Microsoft"
description: "Décrit comment toouse les performances de toooptimize Service Bus lors de l’échange répartie des messages."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e756c15d-31fc-45c0-8df4-0bca0da10bb2
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2017
ms.author: sethm
ms.openlocfilehash: 52764d227757cbb11246675878933f21685817f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-performance-improvements-using-service-bus-messaging"></a>Meilleures pratiques relatives aux améliorations de performances à l’aide de la messagerie Service Bus

Cet article décrit comment toouse [messagerie Azure Service Bus](https://azure.microsoft.com/services/service-bus/) toooptimize performances lors de l’échange répartie des messages. Hello première partie de cette rubrique décrit les mécanismes de différents hello offerts toohelp augmentation des performances. deuxième partie de Hello fournit des conseils sur la toouse Service Bus d’une façon qui peut offrir hello des performances optimales dans un scénario donné.

Dans cette rubrique, le terme hello « client » fait référence entité tooany qui accède au Service Bus. Un client peut prendre le rôle hello d’un expéditeur ou récepteur. le terme Hello « expéditeur » est utilisé pour un client de file d’attente ou rubrique Service Bus qui envoie la file d’attente Service Bus de messages tooa ou une rubrique. le terme Hello « récepteur » fait référence client de file d’attente ou d’un abonnement de Bus de Service tooa qui reçoit les messages d’une file d’attente du Bus de Service ou d’abonnement.

Les sections suivantes présentent plusieurs concepts que Service Bus utilise toohelp améliorer les performances.

## <a name="protocols"></a>Protocoles
Service Bus permet les clients toosend et recevoir des messages via l’une des trois protocoles :

1. Advanced Message Queuing Protocol (AMQP)
2. Service Bus Messaging Protocol (SBMP)
3. HTTP

SBMP et AMQP sont plus efficaces, car elles conservent hello connexion tooService Bus tant que fabrique de messagerie hello existe. Il permet également le traitement par lot et la lecture anticipée. Sauf mention explicite, tout le contenu de cette rubrique suppose l’utilisation de hello d’AMQP ou SBMP.

## <a name="reusing-factories-and-clients"></a>Réutilisation de structures et de clients
Des objets client Service Bus, tels que [QueueClient][QueueClient] ou [MessageSender][MessageSender], sont créés via un objet [MessagingFactory][MessagingFactory], qui assure également la gestion interne des connexions. Vous ne devez pas fermer fabriques de messageries ou file d’attente, rubrique et clients de l’abonnement après l’envoi d’un message et puis de les recréer lorsque vous envoyez le message de type hello suivant. Fermeture d’une fabrique de messagerie supprime hello connexion toohello Service service Bus, et une nouvelle connexion est établie lorsque vous recréez la fabrique de hello. Objets de l’établissement de qu'une connexion est une opération coûteuse que vous pouvez éviter en réutilisant hello même fabrique et client pour plusieurs opérations. Vous pouvez utiliser en toute sécurité hello [QueueClient] [ QueueClient] objet pour envoyer des messages à partir de plusieurs threads et les opérations asynchrones simultanées. 

## <a name="concurrent-operations"></a>Opérations simultanées
L’exécution d’une opération (envoi, réception, suppression, etc.) prend un certain temps. Ce temps inclut traitement hello d’opération de hello en hello Service service Bus de latence de toohello d’ajout de la demande de hello et réponse de hello. nombre de hello tooincrease d’opérations par période, les opérations doivent s’exécuter simultanément. Pour cela, vous pouvez procéder de plusieurs façons différentes :

* **Opérations asynchrones**: client de hello planifie les opérations en effectuant des opérations asynchrones. demande suivante de Hello est démarré avant de la demande précédente de hello est terminée. Hello Voici un exemple d’une opération d’envoi asynchrone :
  
 ```csharp
  BrokeredMessage m1 = new BrokeredMessage(body);
  BrokeredMessage m2 = new BrokeredMessage(body);
  
  Task send1 = queueClient.SendAsync(m1).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #1");
    });
  Task send2 = queueClient.SendAsync(m2).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #2");
    });
  Task.WaitAll(send1, send2);
  Console.WriteLine("All messages sent");
  ```
  
  Voici un exemple d’opération de réception asynchrone :
  
  ```csharp
  Task receive1 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  Task receive2 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  
  Task.WaitAll(receive1, receive2);
  Console.WriteLine("All messages received");
  
  async void ProcessReceivedMessage(Task<BrokeredMessage> t)
  {
    BrokeredMessage m = t.Result;
    Console.WriteLine("{0} received", m.Label);
    await m.CompleteAsync();
    Console.WriteLine("{0} complete", m.Label);
  }
  ```
* **Plusieurs fabriques**: tous les clients (expéditeurs dans Ajout tooreceivers) qui sont créés par hello même fabrique partage une connexion TCP. débit de message maximale Hello est limité par nombre de hello d’opérations pouvant circuler via cette connexion TCP. débit Hello qui peut être obtenu avec une seule fabrique varie grandement en fonction des durées de parcours circulaire TCP et la taille des messages. taux de débit supérieurs tooobtain, vous devez utiliser plusieurs fabriques de messageries.

## <a name="receive-mode"></a>Mode de réception
Lorsque vous créez un client de file d’attente ou d’abonnement, vous pouvez spécifier un mode de réception : *verrouillage* ou *recevoir et supprimer*. mode de réception par défaut de Hello est [PeekLock][PeekLock]. Lors du fonctionnement dans ce mode, client de hello envoie à un tooreceive demande un message à partir de Service Bus. Une fois que le client de hello a reçu le message de type hello, il envoie un message de type hello toocomplete demande.

Lorsque la définition de hello mode de réception trop[ReceiveAndDelete][ReceiveAndDelete], les deux étapes sont combinées dans une demande unique. Cela réduit le nombre total d’opérations de hello et peut améliorer les hello débit général des messages. Ce gain de performances est fourni à des risques de perdre des messages hello.

Service Bus ne gère pas les transactions des opérations de réception-suppression. En outre, les sémantiques afficher-verrouiller sont requis pour les scénarios qui Bonjour client veut toodefer ou [mortes](service-bus-dead-letter-queues.md) un message.

## <a name="client-side-batching"></a>Traitement par lots côté client
Le traitement par lots côté client permet à une file d’attente ou rubrique client toodelay hello envoi d’un message pour un certain temps. Si le client de hello envoie d’autres messages pendant cette période, il transmet les messages hello dans un lot unique. Le traitement par lots côté client entraîne également une toobatch de client de file d’attente ou abonnement plusieurs **Complete** requêtes en une seule requête. Le traitement par lots n’est disponible que pour les opérations **d’envoi** et **complètes** asynchrones. Opérations synchrones sont envoyées immédiatement toohello Service service Bus. Le traitement par lots ne peut pas concerner des opérations de verrouillage ou de réception, ou plusieurs clients.

Par défaut, un client utilise un intervalle 20 ms entre les lots. Vous pouvez modifier l’intervalle de lot hello en définissant un hello [BatchFlushInterval] [ BatchFlushInterval] propriété avant de créer hello fabrique de messagerie. Ce paramètre affecte tous les clients créés par cette structure.

toodisable de traitement par lot, définissez hello [BatchFlushInterval] [ BatchFlushInterval] propriété trop**TimeSpan.Zero**. Par exemple :

```csharp
MessagingFactorySettings mfs = new MessagingFactorySettings();
mfs.TokenProvider = tokenProvider;
mfs.NetMessagingTransportSettings.BatchFlushInterval = TimeSpan.FromSeconds(0.05);
MessagingFactory messagingFactory = MessagingFactory.Create(namespaceUri, mfs);
```

Le traitement par lot n’affecte pas le nombre de hello d’opérations de messagerie facturables et est disponible uniquement pour hello protocole client de Service Bus. Hello protocole HTTP ne prend pas en charge le traitement par lot.

## <a name="batching-store-access"></a>Accès au dispositif de stockage de traitement par lot
débit hello tooincrease de file d’attente, rubrique ou abonnement Service Bus regroupe plusieurs messages lors de l’écriture de magasin interne de tooits. S’il est activé sur une file d’attente ou une rubrique, l’écriture de messages dans le magasin de hello est traités par lot. S’il est activé sur une file d’attente ou un abonnement, suppression des messages à partir du magasin de hello est traités par lot. Si l’accès au magasin par lot est activée pour une entité, Service Bus retarde une opération d’écriture de magasin concernant cette entité par des too20ms. Les opérations de magasin supplémentaires qui se produisent pendant cet intervalle sont ajoutées toohello lot. L’accès au dispositif de stockage par lot affecte seulement les opérations **d’envoi** et **complètes** ; les opérations de réception ne sont pas affectées. L’accès au dispositif de stockage est une propriété d’entité. Le traitement par lot se produit sur toutes les entités qui permettent l’accès au stockage par lot.

Lorsque vous créez une file d’attente, une rubrique ou un abonnement, l’accès au stockage par lot est activé par défaut. toodisable traités par lot d’accès au magasin, jeu hello [EnableBatchedOperations] [ EnableBatchedOperations] propriété trop**false** avant de créer l’entité de hello. Par exemple :

```csharp
QueueDescription qd = new QueueDescription();
qd.EnableBatchedOperations = false;
Queue q = namespaceManager.CreateQueue(qd);
```

Accès au magasin par lot n’affecte pas le nombre de hello d’opérations de messagerie facturables et est une propriété d’une file d’attente, rubrique ou abonnement. Elle est indépendante de hello mode et hello le protocole utilisé entre un client et un hello service Bus de Service de réception.

## <a name="prefetching"></a>Lecture anticipée
Lecture anticipée permet hello file d’attente ou abonnement client tooload supplémentaire des messages à partir du service de hello lorsqu’elle effectue une opération de réception. client de Hello stocke ces messages dans un cache local. taille de Hello du cache de hello est déterminée par hello [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] ou [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] Propriétés. Chaque client qui permet la lecture anticipée gère son propre cache. Un cache n’est pas partagé par plusieurs clients. Si le client de hello initie une opération de réception et son cache est vide, le service de hello transmet un lot de messages. taille de Hello du lot de hello est égale à la taille de hello du cache de hello ou 256 Ko, plus faible l’emportant. Si le client de hello initie une opération de réception et hello cache contient un message, message de type hello est extraite du cache de hello.

Lorsqu’un message est prérécupéré, message de salutation de verrous service hello prérécupérées. Ce faisant, message de type hello prérécupérées ne peut pas être reçu par un autre récepteur. Si le récepteur de hello ne peut pas effectuer de message de type hello avant expiration du verrouillage hello, message de salutation devient disponible tooother récepteurs. copie de Hello prérécupéré du message de type hello reste dans le cache de hello. Hello récepteur qui consomme hello expiré mis en cache copie reçoit une exception lorsqu’il tente de toocomplete ce message. Par défaut, le verrouillage du message hello expire au bout de 60 secondes. Cette valeur peut être étendue too5 minutes. tooprevent hello la consommation de messages arrivés à expiration, la taille du cache hello doit toujours être inférieure au nombre de hello de messages qui peuvent être utilisés par un client au sein de l’intervalle de délai d’attente de verrou hello.

Lors de l’expiration de verrou hello par défaut de 60 secondes, une bonne valeur pour [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] est hello 20 fois maximal vitesses de traitement tous les récepteurs de fabrique de hello. Par exemple, une fabrique crée 3 récepteurs, et chaque récepteur peut traiter les messages too10 par seconde. nombre de prérécupérations Hello ne doit pas dépasser 20 X 3 X 10 = 600. Par défaut, [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] est too0 ensemble, ce qui signifie qu’aucun message supplémentaire n’est récupéré à partir du service de hello.

La prérécupération des messages augmente hello débit global d’une file d’attente ou un abonnement, car il réduit le nombre total d’opérations de message, ou que les boucles de hello. L’extraction du premier message de type hello, toutefois, prendra plus de temps (en raison de taille de message toohello augmenté). Réception de messages prérécupérées seront plus rapide, car ces messages ont déjà été téléchargés par le client de hello.

Hello time-to-live (TTL) propriété d’un message est vérifiée par le serveur de hello au moment de hello server de hello envoie client toohello de message hello. client de Hello ne vérifie pas la propriété de durée de vie du message de type hello lors de la réception du message de type hello. Au lieu de cela, le message de type hello peut être reçu même si hello sa durée de vie est dépassée, pendant que le message de salutation a été mis en cache par le client de hello.

La prérécupération n’affecte pas le nombre de hello d’opérations de messagerie facturables et est disponible uniquement pour hello protocole client de Service Bus. Hello protocole HTTP ne prend pas en charge la lecture anticipée. La lecture anticipée est disponible pour les opérations de réception synchrones et asynchrones.

## <a name="express-queues-and-topics"></a>Files d’attente et les rubriques rapides

Entités Express activer un débit élevé et des scénarios de latence réduite et sont pris en charge uniquement dans la couche de messagerie Standard hello. Entités créées dans [espaces de noms Premium](service-bus-premium-messaging.md) ne prennent pas en charge l’option express de hello. Avec des entités rapides, si un message est envoyé à la file d’attente de tooa ou une rubrique, message de type hello n'est pas immédiatement stocké dans la banque de messages hello. Au lieu de cela, le message est mis en cache. Si un message reste dans la file d’attente hello plus de quelques secondes, il est automatiquement écrit toostable stockage, afin de le protéger contre la perte d’échéance tooan panne. L’écriture de message de type hello dans une mémoire cache augmente le débit et réduit la latence, car il n’existe aucun toostable accès stockage au message de type hello temps hello est envoyé. Les messages consommés en quelques secondes ne sont pas écrites toohello banque d’informations. Bonjour à l’exemple suivant crée une rubrique expresse.

```csharp
TopicDescription td = new TopicDescription(TopicName);
td.EnableExpress = true;
namespaceManager.CreateTopic(td);
```

Si un message contenant des informations sensibles qui ne doivent pas être égarées est envoyé tooan des entités express, l’expéditeur de hello peut forcer le Service Bus tooimmediately conserver stockage toostable des messages hello en définissant un hello [ForcePersistence] [ ForcePersistence] propriété trop**true**.

> [!NOTE]
> Les entités rapides ne prennent pas en charge les transactions.

## <a name="use-of-partitioned-queues-or-topics"></a>Utilisation de files d’attente partitionnées ou de rubriques
En interne, Service Bus utilise hello même nœud et tooprocess de la banque de messagerie et stocker tous les messages pour une entité de messagerie (file d’attente ou rubrique). Une file d’attente partitionnée ou une rubrique, sur hello autre part, est distribué sur plusieurs nœuds et banques de messages. Les rubriques et files d’attente partitionnées donnent non seulement un débit plus élevé que les rubriques et files d’attente standard, mais ils présentent également une disponibilité supérieure. toocreate une entité partitionnée, jeu hello [EnablePartitioning] [ EnablePartitioning] propriété trop**true**, comme indiqué dans hello l’exemple suivant. Pour plus d’informations sur les entités partitionnées, consultez [Files d’attente et rubriques partitionnées][Partitioned messaging entities].

```csharp
// Create partitioned queue.
QueueDescription qd = new QueueDescription(QueueName);
qd.EnablePartitioning = true;
namespaceManager.CreateQueue(qd);
```

## <a name="use-of-multiple-queues"></a>Utilisation de plusieurs files d’attente

Si elle n’est pas possible de toouse qu'une file d’attente partitionnée ou une rubrique ou un hello attendu de charge ne peut pas être gérée par une seule file d’attente partitionnée ou une rubrique, vous devez utiliser plusieurs entités de messagerie. Lorsque vous utilisez plusieurs entités, créez un client dédié pour chaque entité, au lieu d’utiliser hello même client pour toutes les entités.

## <a name="development-and-testing-features"></a>Fonctionnalités de développement et de test

Service Bus possède une fonctionnalité qui est utilisée spécifiquement pour le développement, qui **ne doit jamais être utilisée dans les configurations de production** : [TopicDescription.EnableFilteringMessagesBeforePublishing][].

Lorsque de nouvelles règles ou des filtres sont ajoutés toohello rubrique, vous pouvez utiliser [TopicDescription.EnableFilteringMessagesBeforePublishing][] tooverify qui hello nouvelle expression de filtre fonctionne comme prévu.

## <a name="scenarios"></a>Scénarios
Bonjour les sections suivantes décrivent des scénarios de messagerie classiques et montrer les paramètres de Service Bus hello préféré. Les débits sont classés dans la catégorie Petit (moins d’1 message/seconde), Modéré (1 message/s ou plus, mais moins de 100 messages par seconde) et Élevé (100 messages/seconde ou plus). Hello nombre de clients est classé en tant que petite modéré (5 ou moins), (plus de 5, mais inférieur à ou égal too20) et de grande taille (plus de 20).

### <a name="high-throughput-queue"></a>File d’attente à débit élevé
Objectif : Maximiser le débit de hello d’une file d’attente unique. nombre de Hello d’expéditeurs et de récepteurs est faible.

* Utilisez une file d’attente partitionnée pour améliorer les performances et la disponibilité.
* hello tooincrease globale taux d’envoi dans la file d’attente hello, utilisez plusieurs expéditeurs de toocreate de fabriques de messages. Pour chaque expéditeur, utilisez des opérations asynchrones ou plusieurs threads.
* hello tooincrease globale taux de réception à partir de la file d’attente hello, utilisez plusieurs destinataires toocreate fabriques.
* Utilisez parti de tootake d’opérations asynchrones de traitement par lot côté client.
* Définissez hello too50ms tooreduce hello fréquence de transmissions de protocoles clients Service Bus de traitement par lot. Si plusieurs expéditeurs sont utilisés, augmentez hello too100ms d’intervalle de traitement par lot.
* Désactivez l’accès au magasin par lot. Cela augmente hello globale vitesse à laquelle les messages peuvent être écrits dans la file d’attente hello.
* Définir des vitesses de traitement maximales hello de tous les destinataires d’une fabrique de décompte too20 fois hello prérécupération. Cela réduit le nombre de hello de transmissions de protocoles clients Service Bus.

### <a name="multiple-high-throughput-queues"></a>Plusieurs files d’attente haut débit
Objectif : Optimiser le débit global de plusieurs files d’attente. débit Hello d’une file d’attente individuelle est modéré ou élevé.

tooobtain débit maximal sur plusieurs files d’attente, utiliser les paramètres hello décrites débit de hello toomaximize d’une file d’attente unique. En outre, utilisez les clients toocreate différentes fabriques qui envoient ou reçoivent à partir de différentes files d’attente.

### <a name="low-latency-queue"></a>File d’attente à latence faible
Objectif : réduire la latence de bout en bout d’une file d’attente ou d’une rubrique. nombre de Hello d’expéditeurs et de récepteurs est faible. débit Hello de file d’attente hello est faible ou modérée.

* Utiliser une file d’attente partitionnée pour améliorer les performances et la disponibilité.
* Désactiver le traitement par lots côté client. client de Hello envoie immédiatement un message.
* Désactiver l’accès au magasin par lot. service de Hello écrit immédiatement banque toohello hello.
* Si vous utilisez un seul client, définissez hello prérécupération nombre too20 fois hello vitesse de traitement du récepteur de hello. Si plusieurs messages arrivent à la file d’attente de hello hello même moment, hello protocole client de Service Bus les transmet tous à hello même temps. Lorsque les clients hello reçoit un message de suivant de hello, ce message est déjà dans le cache local hello. cache de Hello doit être faible.
* Si vous utilisez plusieurs clients, définir hello prérécupération nombre too0. Ce faisant, deuxième client de hello peut hello deuxième message alors que le premier client de hello traite toujours premier message de type hello.

### <a name="queue-with-a-large-number-of-senders"></a>File d’attente comportant un grand nombre d’expéditeurs
Objectif : maximiser le débit d’une file d’attente ou d’une rubrique comportant un grand nombre d’expéditeurs. Chaque expéditeur envoie des messages à une vitesse modérée. nombre de Hello de récepteurs est faible.

Service Bus permet des tooa de connexions simultanées too1000 entité de messagerie (ou 5 000 en utilisant AMQP). Cette limite est appliquée au niveau d’espace de noms hello et rubriques/files d’attente/abonnements sont restreintes par limite de hello de connexions simultanées par espace de noms. Pour les files d’attente, ce nombre est partagé entre les expéditeurs et les destinataires. Si toutes les connexions de 1000 sont requises pour les expéditeurs, vous devez remplacer la file d’attente hello avec une rubrique et un seul abonnement. Une rubrique accepte des connexions simultanées de too1000 des expéditeurs, alors que les abonnements hello accepte un 1000 simultanées des connexions supplémentaires à partir de récepteurs. Si plus de 1000 expéditeurs simultanés sont requis, les expéditeurs hello doivent envoyer des messages toohello protocole de Service Bus via HTTP.

débit de toomaximize, hello suivant :

* Utilisez une file d’attente partitionnée pour améliorer les performances et la disponibilité.
* Si chaque expéditeur réside dans un processus différent, utilisez uniquement une structure par processus.
* Utilisez parti de tootake d’opérations asynchrones de traitement par lot côté client.
* Utiliser par défaut de hello intervalle nombre 20 ms tooreduce hello de transmissions de protocoles clients Service Bus de traitement par lot.
* Désactivez l’accès au magasin par lot. Cela augmente hello globale vitesse à laquelle les messages peuvent être écrits dans la file d’attente hello ou une rubrique.
* Définir des vitesses de traitement maximales hello de tous les destinataires d’une fabrique de décompte too20 fois hello prérécupération. Cela réduit le nombre de hello de transmissions de protocoles clients Service Bus.

### <a name="queue-with-a-large-number-of-receivers"></a>File d’attente comportant un grand nombre de destinataires
Objectif : Optimiser hello taux d’une file d’attente ou d’abonnement avec un grand nombre de récepteurs de réception. Chaque destinataire reçoit les messages à une vitesse modérée. nombre de Hello d’expéditeurs est faible.

Service Bus permet des entités de tooan too1000 connexions simultanées. Si une file d’attente nécessite plus de 1000 récepteurs, vous devez remplacer la file d’attente hello avec une rubrique et plusieurs abonnements. Chaque abonnement peut prendre en charge les connexions simultanées de too1000. Récepteurs peuvent également accéder à la file d’attente de hello via hello le protocole HTTP.

débit de toomaximize, hello suivant :

* Utilisez une file d’attente partitionnée pour améliorer les performances et la disponibilité.
* Si chaque destinataire réside dans un processus différent, utilisez uniquement une structure par processus.
* Les récepteurs peuvent utiliser des opérations synchronisées ou asynchrones. Donné hello modéré des taux d’un récepteur individuel de réception, traitement côté client d’une demande complète n’affecte pas le débit du récepteur.
* Désactivez l’accès au magasin par lot. Cela réduit hello charge globale de l’entité de hello. Cela réduit également hello taux global auquel les messages peuvent être écrits dans la file d’attente hello ou une rubrique.
* La valeur hello prérécupération nombre tooa petit (par exemple, PrefetchCount = 10). Cela empêche les destinataires de rester oisifs pendant que les autres destinataires mettent en cache un grand nombre de messages.

### <a name="topic-with-a-small-number-of-subscriptions"></a>Rubrique comportant un petit nombre d’abonnements
Objectif : Maximiser le débit de hello d’une rubrique comportant un petit nombre d’abonnements. Un message est reçu par un grand nombre d’abonnements, ce qui signifie que hello combinée de réception vitesse sur tous les abonnements est supérieure à la vitesse de transmission hello. nombre de Hello d’expéditeurs est faible. nombre de Hello de récepteurs par abonnement est faible.

débit de toomaximize, hello suivant :

* Utilisez une rubrique partitionnée pour améliorer les performances et la disponibilité.
* hello tooincrease globale taux d’envoi dans la rubrique de hello, utilisez plusieurs expéditeurs de toocreate de fabriques de messages. Pour chaque expéditeur, utilisez des opérations asynchrones ou plusieurs threads.
* hello tooincrease globale taux de réception d’un abonnement, utilisez plusieurs destinataires toocreate fabriques. Pour chaque destinataire, utilisez des opérations asynchrones ou plusieurs threads.
* Utilisez parti de tootake d’opérations asynchrones de traitement par lot côté client.
* Utiliser par défaut de hello intervalle nombre 20 ms tooreduce hello de transmissions de protocoles clients Service Bus de traitement par lot.
* Désactivez l’accès au magasin par lot. Cela augmente hello globale vitesse à laquelle les messages peuvent être écrits dans la rubrique de hello.
* Définir des vitesses de traitement maximales hello de tous les destinataires d’une fabrique de décompte too20 fois hello prérécupération. Cela réduit le nombre de hello de transmissions de protocoles clients Service Bus.

### <a name="topic-with-a-large-number-of-subscriptions"></a>Rubrique comportant un grand nombre d’abonnements
Objectif : Maximiser le débit de hello d’une rubrique comportant un grand nombre d’abonnements. Un message est reçu par un grand nombre d’abonnements, ce qui signifie que hello combinée de réception taux sur tous les abonnements est largement supérieur au taux d’envoi hello. nombre de Hello d’expéditeurs est faible. nombre de Hello de récepteurs par abonnement est faible.

Rubriques de procédures avec un grand nombre d’abonnements exposent généralement un faible débit global si tous les messages sont routés tooall abonnements. Cela est dû au fait hello que chaque message est reçu plusieurs fois et tous les messages qui sont contenus dans une rubrique et tous ses abonnements sont stockés dans hello même stocker. Il est supposé que le nombre de hello d’expéditeurs et de nombre de récepteurs par abonnement sont petites. Service Bus prend en charge jusqu'à too2, 000 abonnements par rubrique.

débit de toomaximize, hello suivant :

* Utilisez une rubrique partitionnée pour améliorer les performances et la disponibilité.
* Utilisez parti de tootake d’opérations asynchrones de traitement par lot côté client.
* Utiliser par défaut de hello intervalle nombre 20 ms tooreduce hello de transmissions de protocoles clients Service Bus de traitement par lot.
* Désactivez l’accès au magasin par lot. Cela augmente hello globale vitesse à laquelle les messages peuvent être écrits dans la rubrique de hello.
* Définir des temps de too20 du nombre de prérécupération hello hello attendu de réception taux en secondes. Cela réduit le nombre de hello de transmissions de protocoles clients Service Bus.

## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur l’optimisation des performances du Service Bus, consultez [partitionnée des entités de messagerie][Partitioned messaging entities].

[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[PeekLock]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[ReceiveAndDelete]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[BatchFlushInterval]: /dotnet/api/microsoft.servicebus.messaging.netmessagingtransportsettings.batchflushinterval#Microsoft_ServiceBus_Messaging_NetMessagingTransportSettings_BatchFlushInterval
[EnableBatchedOperations]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablebatchedoperations#Microsoft_ServiceBus_Messaging_QueueDescription_EnableBatchedOperations
[QueueClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.queueclient.prefetchcount#Microsoft_ServiceBus_Messaging_QueueClient_PrefetchCount
[SubscriptionClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.subscriptionclient.prefetchcount#Microsoft_ServiceBus_Messaging_SubscriptionClient_PrefetchCount
[ForcePersistence]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage.forcepersistence#Microsoft_ServiceBus_Messaging_BrokeredMessage_ForcePersistence
[EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablepartitioning#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[Partitioned messaging entities]: service-bus-partitioning.md
[TopicDescription.EnableFilteringMessagesBeforePublishing]: /dotnet/api/microsoft.servicebus.messaging.topicdescription.enablefilteringmessagesbeforepublishing#Microsoft_ServiceBus_Messaging_TopicDescription_EnableFilteringMessagesBeforePublishing
