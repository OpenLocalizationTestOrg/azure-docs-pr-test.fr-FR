---
title: exceptions de messagerie Service Bus aaaAzure | Documents Microsoft
description: "Liste des exceptions de la messagerie Service Bus et les actions suggérées."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3d8526fe-6e47-4119-9f3e-c56d916a98f9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: sethm
ms.openlocfilehash: 0a206b7bbc808c1190044c1dfd6ffd47b9d454fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-exceptions"></a>Exceptions de la messagerie Service Bus
Cet article répertorie certaines exceptions générées par hello Microsoft Azure Service Bus API de messagerie. Cette référence est toochange de sujet, par conséquent, vérifiez de nouveau les mises à jour.

## <a name="exception-categories"></a>Catégories d'exceptions
API de messagerie Hello génère des exceptions qui peuvent appartenir à hello suivant des catégories, ainsi que de l’action de hello associée, vous pouvez prendre tootry toofix les. Notez que la signification de hello et les causes d’une exception peuvent varier en fonction de type hello d’entité de messagerie (files d’attente ou rubriques ou concentrateurs d’événements) :

1. Erreur de codage utilisateur ([System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx)). Action générale : essayez le code de hello toofix avant de continuer.
2. Erreur d’installation ou de configuration ([Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Action générale : révisez la configuration et modifiez-la si besoin.
3. Exceptions temporaires ([Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)). Action générale : recommencez l’opération de hello ou informer les utilisateurs.
4. Autres exceptions ([System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception)). Action générale : type d’exception spécifique toohello ; consultez la table toohello Bonjour suivant la section. 

## <a name="exception-types"></a>Types d'exceptions
Hello tableau suivant répertorie les types d’exception messagerie, leurs causes et action suggérée de notes que vous pouvez prendre.

| **Type d'exception** | **Description/Cause/Exemples** | **Action suggérée** | **Remarques sur la nouvelle tentative automatique/immédiate** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello serveur n’a pas répondu toohello a demandé l’opération dans hello spécifié temps qui est contrôlé par [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). serveur de Hello a peut-être été terminée hello a demandé l’opération. Cela peut se produire en raison de toonetwork ou autres délais d’infrastructure. |Vérifiez l’état du système hello par souci de cohérence, puis réessayez si nécessaire. Consultez [Exceptions au délai d’expiration](#timeoutexception). |Nouvelle tentative peut vous aider dans certains cas ; Ajoutez toocode logique de nouvelle tentative. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hello a demandé l’opération utilisateur n’est pas autorisée dans hello serveur ou le service. Message d’exception hello pour plus d’informations, consultez. Par exemple, [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) génère cette exception si le message de salutation reçu [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode. |Vérifiez le code de hello et la documentation de hello. Vérifiez que hello opération demandée n’est valide. |Une nouvelle tentative ne sera pas bénéfique. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Une tentative est effectuée tooinvoke une opération sur un objet qui a déjà été fermée, interrompue ou supprimée. Dans de rares cas, la transaction ambiante de hello est déjà supprimée. |Code de hello et assurez-vous qu’il n’appelle pas les opérations sur un objet supprimé. |Une nouvelle tentative ne sera pas bénéfique. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) objet n’a pas pu obtenir un jeton, jeton de hello n’est pas valide ou jeton de hello ne contient pas de hello revendications tooperform requis hello opération. |Assurez-vous que le fournisseur de jetons hello est créé avec les valeurs correctes hello. Vérifiez la configuration de hello Hello service de contrôle d’accès. |Nouvelle tentative peut vous aider dans certains cas ; Ajoutez toocode logique de nouvelle tentative. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Un ou plusieurs arguments de type fournis (méthode) toohello ne sont pas valides.<br /> Hello URI fourni trop[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [créer](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) contient des segments de chemin d’accès.<br /> schéma d’URI Hello fourni trop[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [créer](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) n’est pas valide. <br />valeur de la propriété Hello est supérieure à 32 Ko. |Vérifiez le code d’appel hello et assurez-vous que les arguments hello sont corrects. |Une nouvelle tentative ne sera pas bénéfique. |
| [MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) |Entité associée hello opération n’existe pas ou il a été supprimé. |Assurez-vous que l’entité hello existe. |Une nouvelle tentative ne sera pas bénéfique. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Tenter de tooreceive un message avec un numéro de séquence donné. Ce message est introuvable. |Assurez-vous que le message de salutation n’a pas déjà été reçu. Vérifiez toosee de file d’attente de lettres mortes hello si le message de salutation a été lettre morte. |Une nouvelle tentative ne sera pas bénéfique. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Client n’est pas en mesure de tooestablish une tooService connexion Bus. |Assurez-vous que le nom d’hôte hello fourni est correct et hello hôte est accessible. |Une nouvelle tentative peut aider en cas de problèmes de connectivité intermittents. |
| [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Service n’est pas demande de hello en mesure de tooprocess pour l’instant. |Client, vous pouvez attendre un certain temps, puis recommencez l’opération de hello. |Le client peut réessayer après un certain temps. Si une nouvelle tentative provoque une exception différente, vérifiez le comportement de nouvelle tentative de cette exception. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Lock-token associé au message de salutation a expiré ou lock-token hello est introuvable. |Supprimer le message de type hello. |Une nouvelle tentative ne sera pas bénéfique. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Le verrou associé à cette session est perdu. |Abandonner hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) objet. |Une nouvelle tentative ne sera pas bénéfique. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Générique d’exception peut être levée dans hello suivant les cas de messagerie :<br /> Une tentative est faite toocreate un [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) à l’aide d’un nom ou le chemin d’accès auquel appartient le type d’entité différent tooa (par exemple, une rubrique).<br />  Une tentative est agrandie toosend un message à 256 Ko. Hello serveur ou le service a rencontré une erreur lors du traitement de demande de hello. Consultez le message d’exception hello pour plus d’informations. Il s'agit généralement d'une exception temporaire. |Vérifier le code de hello et garantir que seuls les objets sérialisables sont utilisés pour le corps du message hello (ou utiliser un sérialiseur personnalisé). Consultez la documentation de hello pour hello pris en charge les types de valeur des propriétés de hello et uniquement les types de prises en charge. Vérifiez hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) propriété. S’il s’agit **true**, vous pouvez retenter hello opération. |Le comportement de la nouvelle tentative n'est pas défini et peut ne pas être utile. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Essayez de toocreate une entité dont le nom est déjà utilisé par une autre entité dans cet espace de noms de service. |Supprimer l’entité existante de hello ou choisissez un autre nom pour hello entité toobe est créé. |Une nouvelle tentative ne sera pas bénéfique. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Hello entité de messagerie a atteint sa taille maximale autorisée, ou hello le nombre maximal de connexions tooa espace de noms a été dépassé. |Créer l’espace dans l’entité de hello par la réception de messages à partir de l’entité de hello ou ses files d’attente secondaire. Consultez [QuotaExceededException](#quotaexceededexception). |Nouvelle tentative peut vous aider si les messages ont été supprimés dans hello entre-temps. |
| [RuleActionException](/dotnet/api/microsoft.servicebus.messaging.ruleactionexception) |Bus de service renvoie cette exception si vous essayez de toocreate une action de règle non valide. Bus de service joint ce message d’exception tooa lettre morte si une erreur se produit lors du traitement d’action de règle hello pour ce message. |Vérifier l’action de règle hello est correcte. |Une nouvelle tentative ne sera pas bénéfique. |
| [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) |Bus de service renvoie cette exception si vous essayez de toocreate un filtre non valide. Bus de service joint ce message d’exception tooa lettre morte si une erreur s’est produite lors du traitement de filtre hello pour ce message. |Vérifiez le filtre hello est correcte. |Une nouvelle tentative ne sera pas bénéfique. |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Essayez de tooaccept qu'une session avec un ID de session spécifique, mais que la session de hello est actuellement verrouillée par un autre client. |Assurez-vous que la session de hello est déverrouillée par d’autres clients. |Nouvelle tentative peut vous aider si la session de hello a été libérée Bonjour intermédiaires. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Trop d’opérations font partie de la transaction de hello. |Réduire le nombre de hello d’opérations qui font partie de cette transaction. |Une nouvelle tentative ne sera pas bénéfique. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Demande d'une opération d'exécution sur une entité désactivée. |Activer l’entité de hello. |Nouvelle tentative peut vous aider si les entités hello a été activée dans hello intermédiaire. |
| [NoMatchingSubscriptionException](/dotnet/api/microsoft.servicebus.messaging.nomatchingsubscriptionexception) |Bus de service renvoie cette exception si vous envoyez une rubrique tooa de message qui a filtrage préalable activé et aucun des filtres de hello correspond aux. |Assurez-vous qu'au moins un filtre correspond. |Une nouvelle tentative ne sera pas bénéfique. |
| [MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Une charge utile du message dépasse la limite de 256 Ko hello. Notez que cette limite de 256 Ko hello est la taille totale des messages hello, qui peut inclure des propriétés système et toute surcharge .NET. |Réduire la taille de hello de charge utile de message hello, puis recommencez l’opération de hello. |Une nouvelle tentative ne sera pas bénéfique. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Hello transaction ambiante (*Transaction.Current*) n’est pas valide. Elle a peut-être été terminée ou annulée. Une exception en interne peut fournir des informations supplémentaires. | |Une nouvelle tentative ne sera pas bénéfique. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Une opération est tentée sur une transaction incertaine, ou une tentative d’opération de hello toocommit et transaction de hello devient incertaine. |Votre application doit gérer cette exception (comme un cas spécial), comme les transactions hello ait déjà été validée. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indique que le quota d’une entité spécifique a été dépassé.

### <a name="queues-and-topics"></a>Files d’attente et rubriques
Pour les files d’attente et aux rubriques, il s’agit souvent taille hello de file d’attente hello. propriété de message d’erreur Hello contiendra plus de détails, comme dans hello l’exemple suivant :

```
Microsoft.ServiceBus.Messaging.QuotaExceededException
Message: hello maximum entity size has been reached or exceeded for Topic: ‘xxx-xxx-xxx’. 
    Size of entity in bytes:1073742326, Max entity size in bytes:
1073741824..TrackingId:xxxxxxxxxxxxxxxxxxxxxxxxxx, TimeStamp:3/15/2013 7:50:18 AM
```

message de type Hello indique cette rubrique hello a dépassé sa limite de taille, dans ce cas 1 Go (hello taille limite par défaut). 

### <a name="namespaces"></a>Espaces de noms

Pour les espaces de noms, [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) peut indiquer qu’une application a dépassé de nombre maximal de hello d’espace de noms de connexions tooa. Par exemple :

```
Microsoft.ServiceBus.Messaging.QuotaExceededException: ConnectionsQuotaExceeded for namespace xxx.
<tracking-id-guid>_G12 ---> 
System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: 
ConnectionsQuotaExceeded for namespace xxx.
```

#### <a name="common-causes"></a>Causes courantes
Il existe deux causes courantes de cette erreur : hello file d’attente de lettres mortes et les récepteurs de messages non opérationnelle.

1. **File d’attente de lettres mortes** toocomplete messages ne réussit pas un lecteur et messages hello sont retournés toohello file d’attente/rubrique lors de l’expiration du verrouillage hello. Cela peut se produire si le lecteur de hello rencontre une exception qui l’empêche d’appeler [BrokeredMessage.Complete](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.complete.aspx). Une fois un message a été lu 10 fois, il déplace la file d’attente de lettres mortes toohello par défaut. Ce comportement est contrôlé par hello [QueueDescription.MaxDeliveryCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.maxdeliverycount.aspx) propriété et a la valeur par défaut de 10. Comme les messages s’accumuler dans la file d’attente de lettres mortes hello, ils prennent place.
   
    problème de hello tooresolve, messages hello complète et de lecture à partir de la file d’attente de lettres mortes hello, comme vous sont à partir de n’importe quel autre file d’attente. Hello [QueueClient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.aspx) classe même contient une [FormatDeadLetterPath](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.formatdeadletterpath.aspx) chemin d’accès de la file d’attente de lettres mortes de méthode toohelp format hello.
2. **Récepteur arrêté** Un récepteur a arrêté de recevoir des messages d’une file d’attente ou d’un abonnement. Hello tooidentify de la façon dont il s’agit de toolook à hello [QueueDescription.MessageCountDetails](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.messagecountdetails.aspx) propriété, qui affiche hello de décomposition complète de messages de type hello. Si hello [ActiveMessageCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagecountdetails.activemessagecount.aspx) propriété est élevé ou croissant, puis les messages hello ne sont pas lus aussi rapidement qu’ils sont en cours d’écriture.

### <a name="event-hubs"></a>Event Hubs
Event Hubs a une limite de 20 groupes de consommateurs par Event Hub. Lorsque vous essayez de toocreate plus, vous recevez un [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indique qu’une opération initiée par l’utilisateur prend plus de temps que le délai d’attente de hello opération. 

Vous devez vérifier la valeur hello hello [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) propriété, telle que cette limite atteinte peut également entraîner une [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

### <a name="queues-and-topics"></a>Files d’attente et rubriques
Pour les files d’attente et aux rubriques, délai d’attente hello est spécifiée dans hello [MessagingFactorySettings.OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout) propriété, dans le cadre de la chaîne de connexion hello, ou par [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). message d’erreur Hello lui-même peut-être varier, mais il contient toujours la valeur de délai d’attente hello spécifié pour l’opération en cours hello. 

### <a name="event-hubs"></a>Event Hubs
Pour les concentrateurs d’événements, délai d’attente hello est spécifiée dans le cadre de la chaîne de connexion hello, ou par [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). message d’erreur Hello lui-même peut-être varier, mais il contient toujours la valeur de délai d’attente hello spécifié pour l’opération en cours hello. 

### <a name="common-causes"></a>Causes courantes
Il existe deux causes communes pour cette erreur : une configuration incorrecte ou une erreur de service temporaire.

1. **Une configuration incorrecte** le délai d’attente de hello opération peut-être être trop petit pour la condition de fonctionnement hello. valeur par défaut de Hello hello opération délai de connexion dans le client hello SDK est de 60 secondes. Vérifiez toosee si votre code possède la valeur de hello toosomething trop petite. Notez cette condition hello du réseau de hello et l’utilisation du processeur peut affecter hello temps d’une opération particulière toocomplete, donc le délai d’attente de hello opération ne doit pas être défini tooa très petite valeur.
2. **Erreur du service temporaire** parfois hello service Bus de Service peut subir des retards de traitement des requêtes, par exemple, pendant les périodes de trafic élevé. Dans ce cas, vous pouvez réessayer l’opération après un délai, jusqu'à ce que l’opération de hello a réussi. Hello même opération échoue encore après plusieurs tentatives, visitez hello [site d’état des services Azure](https://azure.microsoft.com/status/) toosee s’il existe des interruptions de service connu.

## <a name="next-steps"></a>Étapes suivantes

Pour hello complète les API .NET Service Bus, consultez hello [référence de l’API .NET de Azure](/dotnet/api/overview/azure/servicebus).

toolearn plus [Service Bus](https://azure.microsoft.com/services/service-bus/), consultez les rubriques suivantes de hello.

* [Présentation de la messagerie Service Bus](service-bus-messaging-overview.md)
* [Concepts de base de Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Architecture de Service Bus](service-bus-architecture.md)

