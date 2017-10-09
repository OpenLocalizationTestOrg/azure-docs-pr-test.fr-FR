---
title: "files d’attente de stockage aaaAzure et files d’attente de Service Bus - comparaison et différences | Documents Microsoft"
description: "Analyse les différences et les similitudes entre les deux types de files d'attente proposés par Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: f07301dc-ca9b-465c-bd5b-a0f99bab606b
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: f8b915e73ea3c82d823a96bf23c8c9e24c96aa42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-queues-and-service-bus-queues---compared-and-contrasted"></a>Files d’attente Azure et files d’attente Service Bus : comparaison et différences
Cet article analyse les différences de hello et les ressemblances entre types hello deux des files d’attente proposées par Microsoft Azure : les files d’attente de stockage et les files d’attente Service Bus. À l’aide de ces informations, vous pouvez comparer et créer un contraste avec les technologies respectives hello et être en mesure de toomake une décision plus avisée sur la solution qui répond à vos besoins.

## <a name="introduction"></a>Introduction
Azure prend en charge deux types de mécanismes de file d’attente : les **files d’attente de stockage** et les **files d’attente Service Bus**.

**Les files d’attente de stockage**, qui font partie de hello [le stockage Azure](https://azure.microsoft.com/services/storage/) infrastructure, fonctionnalité une simple interface basée sur REST GET/PUT/PEEK, en fournissant la messagerie fiable et persistante dans et entre les services.

Les **files d’attente Service Bus** font partie d’une infrastructure de [messagerie Azure](https://azure.microsoft.com/services/service-bus/) plus large qui prend en charge la mise en file d’attente, ainsi que la publication/l’abonnement, l’accès distant au service Web et les modèles d’intégration. Pour plus d’informations sur les files d’attente/aux rubriques/abonnements Service Bus, consultez hello [vue d’ensemble du Service Bus](service-bus-messaging-overview.md).

Bien que les deux technologies de file d’attente coexistent, les files d’attente Azure sont apparues en premier, en tant que mécanisme de stockage en file d’attente dédié, basé sur les services de stockage Azure. Les files d’attente Service Bus sont appuient sur hello plus large de « messagerie » infrastructure conçue toointegrate applications ou des composants d’application qui peuvent s’étendre sur plusieurs protocoles de communication, contrats de données, domaines d’approbation et/ou environnements réseau.

## <a name="technology-selection-considerations"></a>Considérations relatives à la sélection de la technologie
Les files d’attente de stockage et les files d’attente Service Bus sont des implémentations de hello service message queuing actuellement proposé sur Microsoft Azure. Chacune a un ensemble de fonctionnalités légèrement différent, ce qui signifie que vous pouvez choisir l’une ou autre hello ou utilisez les deux, selon les besoins de hello de votre solution ou d’un problème d’entreprise/technique à résoudre.

Pour déterminer quelle technologie de file d’attente adaptée à hello pour une solution donnée, les développeurs et aux architectes de solutions doivent tenez compte des recommandations de hello ci-dessous. Pour plus d’informations, consultez la section suivante de hello.

En tant que développeur/architecte de solutions, **vous devez envisager d’utiliser les files d’attente Azure** dans les cas de figure suivants :

* Votre application doit stocker plus de 80 Go de messages dans une file d’attente, où les messages de type hello ont une durée de vie inférieure à 7 jours.
* Votre application veut tootrack progression pour le traitement d’un message à l’intérieur de file d’attente hello. Cela est utile en cas de panne de travail hello du traitement d’un message. Un thread de travail suivant peut ensuite utiliser ce toocontinue informations à partir de là où le thread de travail précédent hello était arrêté.
* Vous avez besoin de journaux côté serveur de toutes les transactions de hello exécutées sur les files d’attente.

En tant que développeur/architecte de solutions, **vous devez envisager d’utiliser les files d’attente Service Bus** lorsque :

* Votre solution doit être en mesure de tooreceive des messages sans avoir de file d’attente de toopoll hello. Avec Service Bus, cela peut être obtenue via hello réception d’interrogation longue hello opération à l’aide des protocoles TCP hello qui prend en charge du Service Bus.
* Votre solution nécessite hello tooprovide de file d’attente une garantie first-in-first-out livraison chronologique des messages (FIFO).
* Vous souhaitez créer une expérience symétrique dans Azure et Windows Server (cloud privé). Pour plus d’informations, consultez [Service Bus pour Windows Server](https://msdn.microsoft.com/library/dn282144.aspx).
* Votre solution doit être en mesure de toosupport détection automatique des doublons.
* Vous souhaitez que vos messages de tooprocess d’application en tant que flux long parallèles (les messages sont associés à un flux de données à l’aide de hello [SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) propriété de message de type hello). Dans ce modèle, chaque nœud hello consommation d’application est en concurrence pour les flux, en tant que toomessages exécutés. Lorsqu’un flux de données reçoit tooa consommation de nœud, hello peut examiner état hello d’état de flux de données d’application hello à l’aide de transactions.
* Votre solution nécessite un comportement transactionnel et l'atomicité lors de l'envoi ou de la réception de plusieurs messages à partir d'une file d'attente.
* Hello time-to-live (TTL) caractéristique de charge de travail spécifique à l’application hello peut dépasser la période de 7 jours hello.
* Votre application gère les messages qui peuvent dépasser 64 Ko, mais est probablement pas approche hello 256 Ko.
* Vous ne traitez une exigence tooprovide un toohello de modèle d’accès basé sur le rôle de files d’attente et les droits/autorisations différents pour les expéditeurs et destinataires.
* La taille de la file d'attente ne sera pas supérieure à 80 Go.
* Vous souhaitez toouse hello AMQP 1.0 basé sur des normes protocole de messagerie. Pour plus d’informations sur AMQP, consultez [Présentation d’AMQP Service Bus](service-bus-amqp-overview.md).
* Vous pouvez prévoir une migration éventuelle de point à point basées sur la file d’attente de communication tooa modèle échange de messages qui permet une intégration transparente des récepteurs (abonnés), chacun d’eux recevant des copies indépendantes de tout ou partie les messages envoyés à la file d’attente de toohello. Hello ce dernier fait référence à capacité de publication/abonnement toohello en mode natif fournie par Service Bus.
* Votre solution de messagerie doit être en mesure de toosupport garantie de remise hello » à la plupart-une fois » sans avoir besoin de hello de composants d’infrastructure supplémentaires toobuild hello.
* Vous aimez toopublish en mesure de toobe et utiliser des lots de messages.

## <a name="comparing-storage-queues-and-service-bus-queues"></a>Comparaison des files d’attente Azure et des files d’attente Service Bus
tables Hello Bonjour les sections suivantes fournissent un regroupement logique des fonctionnalités de file d’attente et vous permettent de comparer un coup de œil, les fonctions hello disponibles dans les files d’attente de stockage et les files d’attente Service Bus.

## <a name="foundational-capabilities"></a>Fonctions de base
Cette rubrique compare certaines des fonctions files d’attente de base hello fournies par les files d’attente de stockage et les files d’attente Service Bus.

| Critères de comparaison | Files d’attente de stockage | Files d'attente Service Bus |
| --- | --- | --- |
| Garantie de classement |**Non** <br/><br>Pour plus d’informations, consultez hello première note de hello section « Informations supplémentaires ».</br> |**Oui - Premier entré premier sorti (PEPS)**<br/><br>(via l’utilisation de hello de sessions de messagerie) |
| Garantie de livraison |**Au moins une fois** |**Au moins une fois**<br/><br/>**Une fois au maximum** |
| Prise en charge des opérations atomiques |**Non** |**Oui**<br/><br/> |
| Comportement de réception |**Non bloquant**<br/><br/>(se termine immédiatement si aucun nouveau message n’est trouvé) |**Blocage avec ou sans délai d’expiration**<br/><br/>(offre de l’interrogation longue ou hello [« Comètes »](http://go.microsoft.com/fwlink/?LinkId=613759))<br/><br/>**Non bloquant**<br/><br/>(via hello utiliser .NET API managée uniquement) |
| API style Push |**Non** |**Oui**<br/><br/>API .NET [OnMessage](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage#Microsoft_ServiceBus_Messaging_QueueClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__) et sessions **OnMessage**. |
| Mode de réception |**Aperçu et attribution** |**Aperçu et verrouillage**<br/><br/>**Réception et suppression** |
| Mode d'accès exclusif |**Basé sur attribution** |**Basé sur verrouillage** |
| Durée attribution/verrouillage |**30 secondes (par défaut)**<br/><br/>**7 jours (maximum)** (vous pouvez renouveler ou libérer un bail de message à l’aide de hello [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API.) |**60 secondes (par défaut)**<br/><br/>Vous pouvez renouveler le verrou d’un message à l’aide de hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API. |
| Précision attribution/verrouillage |**Au niveau du message**<br/><br/>(chaque message peut avoir une valeur de délai d’attente différente, que vous pouvez ensuite de mettre à jour en cas de besoin lors du traitement du message de type hello, à l’aide de hello [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API) |**Au niveau de la file d’attente**<br/><br/>(chaque file d’attente a un tooall précision appliquée de verrou de ses messages, mais vous pouvez renouveler le verrou hello à l’aide de hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API.) |
| Réception par lots |**Oui**<br/><br/>(spécifiant explicitement le nombre de messages lors de la récupération des messages, des tooa au maximum 32 messages) |**Oui**<br/><br/>(implicitement l’activation d’une propriété de prérécupération ou explicitement via hello l’utilisation de transactions) |
| Envoi par lots |**Non** |**Oui**<br/><br/>(via l’utilisation de hello de transactions ou le traitement par lots côté client) |

### <a name="additional-information"></a>Informations supplémentaires
* Les messages dans les files d’attente de stockage se voient en général appliquer la méthode Premier entré, premier sorti. Mais ils peuvent parfois être dans le désordre. C’est le cas lorsque le délai de visibilité d’un message expire (par exemple, à cause du blocage d’une application cliente pendant le traitement). Lors de l’expiration du délai de visibilité hello, message de type hello redevient visible sur la file d’attente de hello pour un autre travail toodequeue il. À ce stade, peut-être être placé de message de type hello qui vient d’être visible dans la file d’attente hello (dépilé toobe à nouveau) après un message qui a été initialement en file d’attente après lui.
* Hello garantie modèle FIFO dans les files d’attente Service Bus nécessite l’utilisation de hello de sessions de messagerie. Bonjour événement hello application se bloque lors du traitement d’un message reçu en hello **Aperçu & Verrouiller** mode, hello prochaine un récepteur de file d’attente accepte une session de messagerie, il démarre avec le message d’échec hello après son durée de vie (TTL) écoulée.
* Les files d’attente de stockage sont les scénarios de files d’attente toosupport conçue standard, tels que le découplage d’extensibilité de l’application composants tooincrease et la tolérance des échecs, le lissage de charge et création de flux de processus.
* Les files d’attente Service Bus prend en charge hello *au moins une* garantie de remise. En outre, hello *-plus-une fois au* sémantique peut être pris en charge à l’aide d’état de l’application hello toostore état session et recevoir des messages à l’aide de transactions tooatomically et mettre à jour l’état de session hello.
* Les files d’attente de stockage fournissent un modèle de programmation uniforme et cohérent entre les files d’attente, les tables et les objets blob, pour les développeurs et les équipes d’exploitation.
* Les files d’attente Service Bus prennent en charge les transactions locales dans le contexte de hello d’une file d’attente unique.
* Hello **recevoir et supprimer** mode pris en charge par le Service Bus fournit hello de tooreduce de capacité hello messagerie nombre d’opérations (et le coût associé) en échange de la garantie de remise.
* Les files d’attente de stockage fournissent des baux avec des baux de hello tooextend hello possibilité pour les messages. Ainsi, les travailleurs hello toomaintain baux de courte durée sur les messages. Par conséquent, si un processus de travail se bloque, message de type hello peut être rapidement traité par un autre processus de travail. En outre, un processus de travail peut étendre bail hello sur un message si elle a besoin tooprocess il délai de bail plus longtemps que hello actuel.
* Les files d’attente de stockage offrent un délai de visibilité que vous pouvez définir lors de hello empilage ou du dépilage d’un message. En outre, vous pouvez mettre à jour un message avec des valeurs de bail différentes au moment de l’exécution et des valeurs de mise à jour différents sur des messages Bonjour même file d’attente. Délais d’attente du verrou de Bus de service sont définis dans les métadonnées de file d’attente hello ; Toutefois, vous pouvez renouveler le verrou de hello en appelant hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) (méthode).
* délai d’attente maximal de Hello pour un blocage opération de réception dans les files d’attente Service Bus est de 24 jours. Toutefois, les délais d'attente basés sur REST ont une valeur maximale de 55 secondes.
* Le traitement par lots côté client fournies par Service Bus permet un toobatch de client de file d’attente plusieurs messages dans une seule opération d’envoi. Le traitement par lots n'est disponible que pour les opérations d'envoi asynchrones.
* Fonctionnalités telles que la limite de 200 to hello de files d’attente de stockage (plus lorsque vous virtualisez des comptes) et les files d’attente illimitées en font une plateforme idéale pour les fournisseurs SaaS.
* Les files d’attente de stockage fournissent un mécanisme performant et flexible de contrôle d’accès délégué.

## <a name="advanced-capabilities"></a>Fonctionnalités avancées
Cette section compare les fonctionnalités avancées des files d’attente Azure et des files d’attente Service Bus.

| Critères de comparaison | Files d’attente de stockage | Files d'attente Service Bus |
| --- | --- | --- |
| Remise planifiée |**Oui** |**Oui** |
| Lettre morte automatique |**Non** |**Oui** |
| Augmenter la valeur de durée de vie de la file d'attente |**Oui**<br/><br/>(par le biais de la mise à jour sur place du délai de visibilité) |**Oui**<br/><br/>(par le biais d’une fonction API dédiée) |
| Prise en charge des messages incohérents |**Oui** |**Oui** |
| Mise à jour sur place |**Oui** |**Oui** |
| Journal des transactions côté serveur |**Oui** |**Non** |
| Métriques de stockage |**Oui**<br/><br/>**Métriques par minute** : fournit des métriques en temps réel pour la disponibilité, le TPS, le nombre d’appels API, le nombre d’erreurs, etc., le tout en temps réel (métriques agrégées par minute et consignées en l’espace de quelques minutes à partir de ce qui vient de se passer en production). Pour plus d’informations, voir la page [À propos des mesures Storage Analytics](/rest/api/storageservices/fileservices/About-Storage-Analytics-Metrics). |**Oui**<br/><br/>(requêtes en bloc en appelant [GetQueues](/dotnet/api/microsoft.servicebus.namespacemanager.getqueues#Microsoft_ServiceBus_NamespaceManager_GetQueues)) |
| Gestion de l'état |**Non** |**Oui**<br/><br/>[Microsoft.ServiceBus.Messaging.EntityStatus.Active](/dotnet/api/microsoft.servicebus.messaging.entitystatus.active), [Microsoft.ServiceBus.Messaging.EntityStatus.Disabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.disabled), [Microsoft.ServiceBus.Messaging.EntityStatus.SendDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.senddisabled), [Microsoft.ServiceBus.Messaging.EntityStatus.ReceiveDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.receivedisabled) |
| Transfert automatique des messages |**Non** |**Oui** |
| Fonction de purge de la file d'attente |**Oui** |**Non** |
| Groupes de messages |**Non** |**Oui**<br/><br/>(via l’utilisation de hello de sessions de messagerie) |
| État de l'application par groupe de messages |**Non** |**Oui** |
| Détection des doublons |**Non** |**Oui**<br/><br/>(configurable côté expéditeur de hello) |
| Consultation des groupes de messages |**Non** |**Oui** |
| Récupération des sessions de messagerie par ID |**Non** |**Oui** |

### <a name="additional-information"></a>Informations supplémentaires
* Les deux technologies de file d’attente permettent une toobe message planifié pour une remise à une date ultérieure.
* File d’attente de transfert automatique permet à des milliers de files d’attente tooauto transférer leur messages tooa file d’attente unique, à partir de l’application de réception qui hello consomme le message de type hello. Vous pouvez utiliser ce mécanisme tooachieve sécurité, flux de contrôle et isoler stockage entre chaque serveur de publication du message.
* Les files d’attente de stockage prennent en charge la mise à jour du contenu des messages. Vous pouvez utiliser cette fonctionnalité pour les informations d’état persistantes et les mises à jour incrémentielles de progression dans le message de salutation afin que celui-ci puisse être traité à partir de hello dernier point de contrôle connu, au lieu de démarrer à partir de zéro. Avec les files d’attente du Bus des services, vous pouvez activer hello même scénario à l’aide de hello de sessions de message. Sessions vous toosave et récupérer l’état de traitement de l’application hello (à l’aide de [SetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_) et [GetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.getstate#Microsoft_ServiceBus_Messaging_MessageSession_GetState)).
* [Lettres mortes](service-bus-dead-letter-queues.md), qui est uniquement prise en charge par les files d’attente du Bus des services, peut être utile pour isoler les messages qui ne peuvent pas être traités correctement par l’application de réception hello ou lorsque les messages n’atteignent pas leur destination en raison tooan expiré propriété (TTL) Time-to-live. Hello valeur TTL spécifie la durée pendant laquelle un message reste dans la file d’attente hello. Avec Service Bus, message de type hello sera la file d’attente spéciale tooa déplacé appelé $DeadLetterQueue lors de la durée de vie hello expire.
* toofind de messages « poison » dans les files d’attente de stockage, lors de la file d’attente une application hello de message examine hello  **[DequeueCount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.dequeuecount.aspx)**  propriété de message de type hello. Si **DequeueCount** est supérieur à un seuil donné, l’application hello transfère hello tooan définies par l’application « lettres mortes » file d’attente.
* Les files d’attente de stockage permettent de tooobtain un journal détaillé de toutes les transactions hello exécutées sur la file d’attente hello, ainsi qu’agrégées des mesures. Ces deux options sont utiles pour déboguer et comprendre comment votre application utilise les files d’attente de stockage. Ils sont également utiles pour régler les performances de votre application et la réduction des coûts de hello d’utilisation des files d’attente.
* concept Hello de « sessions de message » pris en charge par le Service Bus permet des messages qui appartiennent tooa certaine toobe groupe logique associé à un récepteur spécifique, ce qui crée ensuite une affinité de session entre les messages et leurs récepteurs respectifs. Vous pouvez activer cette fonctionnalité avancée dans Service Bus en définissant un hello [SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) propriété d’un message. Récepteurs peuvent ensuite écouter un ID de session spécifique et recevoir des messages qui partagent hello spécifié identificateur de session.
* Hello fonctionnalité de détection des doublons pris en charge par les files d’attente Service Bus automatiquement supprime file d’attente de messages en double envoyés tooa ou une rubrique, selon la valeur hello hello [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.messageid#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) propriété.

## <a name="capacity-and-quotas"></a>Capacité et quotas
Cette section compare les files d’attente de stockage et les files d’attente Service Bus à partir de la perspective hello de [capacité et des quotas](service-bus-quotas.md) qui peuvent s’appliquer.

| Critères de comparaison | Files d’attente de stockage | Files d'attente Service Bus |
| --- | --- | --- |
| Taille de file d'attente maximale |**500 To**<br/><br/>(limitée tooa [unique capacité de compte de stockage](../storage/common/storage-introduction.md#queue-storage)) |**1 Go too80 Go**<br/><br/>(défini lors de la création d’une file d’attente et [activation du partitionnement](service-bus-partitioning.md) – consultez hello section « Informations supplémentaires ») |
| Taille de message maximale |**64 Ko**<br/><br/>(48 Ko avec un codage en **Base64**)<br/><br/>Azure prend en charge les messages volumineux en combinant les files d’attente et des objets BLOB à partir de laquelle vous pouvez empiler des too200GB pour un seul élément. |**256 Ko** ou **1 Mo**<br/><br/>(y compris l’en-tête et le corps, taille maximale d’en-tête : 64 Ko).<br/><br/>Dépend de hello [niveau de service](service-bus-premium-messaging.md). |
| Durée de vie maximale des messages |**7 jours** |**`TimeSpan.Max`** |
| Nombre maximal de files d'attente |**Illimité** |**10,000**<br/><br/>(par espace de noms de service, peut être augmenté) |
| Nombre maximal de clients simultanés |**Illimité** |**Illimité**<br/><br/>(100 connexions simultanées s’applique uniquement communication basée sur le protocole de tooTCP) |

### <a name="additional-information"></a>Informations supplémentaires
* Service Bus applique les limites en termes de taille de file d'attente. taille de file d’attente maximale Hello est spécifiée lors de la création de file d’attente hello et peut avoir une valeur comprise entre 1 et 80 Go. Si la valeur de taille de file d’attente hello lors de la création de file d’attente hello est atteinte, les messages entrants supplémentaires seront rejetés et une exception sera reçue par hello appeler du code. Pour plus d’informations sur les quotas dans Service Bus, consultez [Quotas Service Bus](service-bus-quotas.md).
* Bonjour [niveau Standard](service-bus-premium-messaging.md), vous pouvez créer des files d’attente Service Bus dans des tailles de 1, 2, 3, 4 ou 5 Go (valeur par défaut hello est 1 Go). Dans la couche de Premium hello, vous pouvez créer les files d’attente des too80 go. Dans la norme niveau, avec le partitionnement activé (qui est par défaut de hello), Service Bus crée 16 partitions pour chaque Go que vous spécifiez. Par conséquent, si vous créez une file d’attente est de 5 Go de taille, avec 16 partitions taille de file d’attente maximale hello devient (5 * 16) = 80 Go. Vous pouvez voir la taille maximale de hello de votre file d’attente partitionnée ou une rubrique en examinant son entrée sur hello [portail Azure][Azure portal]. Dans le niveau Premium hello uniquement 2 partitions sont créées par file d’attente.
* Avec les files d’attente de stockage, si hello contenu du message de type hello n’est pas sécurisé XML, il doit être **Base64** encodé. Si vous **Base64**-encoder le message de type hello, la charge utile de hello utilisateur peut être des Ko too48, au lieu de 64 Ko.
* Avec les files d’attente Service Bus, chaque message stocké dans une file d’attente est composé de deux parties : un en-tête et un corps. taille totale de Hello de message de type hello ne peut pas dépasser maximale des messages hello taille prise en charge par niveau de service hello.
* Lorsque les clients communiquent avec les files d’attente Service Bus via le protocole TCP de hello, nombre maximal de hello de file d’attente Service Bus unique connexions simultanées tooa est too100 limité. Ce nombre est partagé entre les expéditeurs et les destinataires. Si ce quota est atteint, les demandes suivantes pour les connexions supplémentaires sont rejetées et une exception sera reçue par hello appeler du code. Cette limite n’est pas appliquée aux clients qui se connectent les files d’attente toohello à l’aide des API basée sur REST.
* Si vous avez besoin de plus de 10 000 files d’attente dans un espace de noms Service Bus, vous pouvez contacter l’équipe de support Azure hello et demander une augmentation. tooscale au-delà de 10 000 files d’attente avec le Bus de Service, vous pouvez également créer des espaces de noms supplémentaires à l’aide de hello [portail Azure][Azure portal].

## <a name="management-and-operations"></a>Gestion et opérations
Cette section compare les fonctionnalités de gestion hello fournies par les files d’attente de stockage et les files d’attente Service Bus.

| Critères de comparaison | Files d’attente de stockage | Files d’attente Service Bus |
| --- | --- | --- |
| Protocole de gestion |**REST sur HTTP/HTTPS** |**REST sur HTTPS** |
| Protocole d'exécution |**REST sur HTTP/HTTPS** |**REST sur HTTPS**<br/><br/>**Norme AMQP 1.0 (TCP avec TLS)** |
| API .NET |**Oui**<br/><br/>(API de client de stockage .NET) |**Oui**<br/><br/>(API Service Bus .NET) |
| C++ natif |**Oui** |**Oui** |
| API Java |**Oui** |**Oui** |
| API PHP |**Oui** |**Oui** |
| API Node.js |**Oui** |**Oui** |
| Prise en charge des métadonnées arbitraires |**Oui** |**Non** |
| Règles d'affectation des noms aux files d'attente |**Les caractères too63**<br/><br/>(les lettres dans un nom de file d’attente doivent être en minuscules) |**Les caractères too260**<br/><br/>(les chemins d’accès et noms des files d’attente ne sont pas sensibles à la casse) |
| Fonction d'obtention de la longueur de la file d'attente |**Oui**<br/><br/>(Valeur approximative si l’expiration des messages au-delà de la durée de vie de hello sans les supprimer.) |**Oui**<br/><br/>(valeur exacte, à un moment donné) |
| Fonction Peek (aperçu) |**Oui** |**Oui** |

### <a name="additional-information"></a>Informations supplémentaires
* Les files d’attente de stockage prennent en charge les attributs arbitraires qui peuvent être appliqués toohello file d’attente description, sous forme de hello de paires nom/valeur.
* Les deux technologies de file d’attente offrent hello capacité toopeek un message sans avoir toolock informatique, qui peut être utile lors de l’implémentation d’un outil Explorateur/navigateur de file d’attente.
* Hello .NET Service Bus répartie messagerie API tirer parti en duplex intégral des connexions TCP pour améliorer les performances lorsque comparées tooREST via HTTP, et ils prennent en charge le protocole standard de hello AMQP 1.0.
* Les noms des files d’attente de stockage peuvent compter entre 3 et 63 caractères, et contenir des lettres minuscules, des nombres et des traits d’union. Pour plus d’informations, consultez [Affectation de noms pour les files d’attente et les métadonnées](/rest/api/storageservices/fileservices/Naming-Queues-and-Metadata).
* Les noms de file d’attente de Bus de service peuvent comporter des caractères too260 et des règles d’affectation de noms moins restrictives. Les noms des files d’attente Service Bus peuvent contenir des lettres, des nombres, des points (.), des traits d’union (-) et des traits de soulignement (_).

## <a name="authentication-and-authorization"></a>Authentification et autorisation
Cette section traite des fonctionnalités d’authentification et d’autorisation hello pris en charge par les files d’attente de stockage et les files d’attente Service Bus.

| Critères de comparaison | Files d’attente de stockage | Files d'attente Service Bus |
| --- | --- | --- |
| Authentification |**Clé symétrique** |**Clé symétrique** |
| Modèle de sécurité |Accès délégué via des jetons SAS. |SAS |
| Fédération de fournisseur d’identité |**Non** |**Oui** |

### <a name="additional-information"></a>Informations supplémentaires
* Chaque tooeither demande Hello queuing technologies doit être authentifiée. Les files d'attente publiques avec accès anonyme ne sont pas prises en charge. À l’aide de la [SAP](service-bus-sas.md), vous pouvez résoudre ce scénario en publiant une SAP en écriture seule, une SAP en lecture seule ou une SAP à accès total.
* Hello schéma d’authentification fournies par le stockage files d’attente implique l’utilisation de hello d’une clé symétrique, qui est un hachage HMAC-based Message Authentication Code (), calculé avec l’algorithme de hello SHA-256 et encodée sous la forme un **Base64** chaîne. Pour plus d’informations sur le protocole respectif de hello, consultez [l’authentification pour hello Services de stockage Azure](/rest/api/storageservices/fileservices/Authentication-for-the-Azure-Storage-Services). Les files d'attente Service Bus prennent en charge un modèle similaire utilisant des clés symétriques. Pour plus d’informations, consultez [Authentification par signature d’accès partagé avec Service Bus](service-bus-sas.md).

## <a name="conclusion"></a>Conclusion
En ayant une meilleure compréhension des technologies de hello deux, vous allez être en mesure de toomake une décision plus avisée sur lequel la file d’attente technologie toouse et lorsque. Hello décision sur lorsque les files d’attente de toouse stockage ou Service Bus des files d’attente clairement dépend de plusieurs facteurs. Ces facteurs dépendent largement des besoins de votre application et son architecture hello. Si votre application utilise déjà les capacités de hello de Microsoft Azure, vous pouvez préférer les files d’attente de stockage toochoose, surtout si vous avez besoin de communication de base et de messagerie entre les services ou les files d’attente nécessaire peuvent être supérieures à 80 Go.

Étant donné que les files d'attente Service Bus fournissent plusieurs fonctionnalités avancées, comme les sessions, les transactions, la détection de doublons, la lettre morte automatique et des fonctions de publication/d'abonnement durables, elles peuvent constituer un meilleur choix si vous créez une application hybride ou si votre application nécessite ces fonctionnalités.

## <a name="next-steps"></a>Étapes suivantes
Hello suivant des articles des plus des conseils et des informations sur l’utilisation des files d’attente de stockage ou les files d’attente Service Bus.

* [Prise en main des files d’attente Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Comment tooUse hello Service de stockage de file d’attente](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Meilleures pratiques relatives aux améliorations de performances à l’aide de la messagerie répartie Service Bus](service-bus-performance-improvements.md)
* [Présentation des files d’attente et des rubriques dans Azure Service Bus (blog)](http://www.code-magazine.com/article.aspx?quickid=1112041)
* [Hello tooService du Guide du développeur Bus](http://www.cloudcasts.net/devguide/Default.aspx?id=11030)
* [À l’aide de hello Queuing Service dans Azure](http://www.developerfusion.com/article/120197/using-the-queuing-service-in-windows-azure/)

[Azure portal]: https://portal.azure.com

