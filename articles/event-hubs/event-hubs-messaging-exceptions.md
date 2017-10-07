---
title: "exceptions de messagerie les concentrateurs d’événements aaaAzure | Documents Microsoft"
description: "Liste des exceptions de la messagerie Azure Event Hubs et les actions suggérées."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2c6273de-0106-47e5-b45d-59040e51f2c5
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 9c164e76612c26607219f08407f689aaab4050a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-messaging-exceptions"></a>Exceptions de la messagerie Event Hubs
Cet article présente certains des exceptions hello générées par hello Azure Service Bus API, qui incluent des concentrateurs d’événements de messagerie. Cette référence est toochange de sujet, par conséquent, vérifiez de nouveau les mises à jour.

## <a name="exception-categories"></a>Catégories d'exceptions
API de concentrateurs d’événements Hello génère des exceptions qui peuvent appartenir à hello suivant des catégories, ainsi que de l’action de hello associée, vous pouvez prendre tootry toofix les.

1. Erreur de codage utilisateur : [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). Action générale : essayez le code de hello toofix avant de continuer.
2. Erreur d’installation ou de configuration : [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Action générale : révisez la configuration et modifiez-la si besoin.
3. Exceptions temporaires : [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](#serverbusyexception), [Microsoft.Azure.EventHubs.ServerBusyException](#serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). Action générale : recommencez l’opération de hello ou informer les utilisateurs.
4. Autres exceptions : [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](#timeoutexception), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception). Action générale : type d’exception spécifique toohello ; consultez la table toohello Bonjour suivant la section. 

## <a name="exception-types"></a>Types d'exceptions
Hello tableau suivant répertorie les types d’exception messagerie, leurs causes et action suggérée de notes que vous pouvez prendre.

| **Type d'exception** | **Description/Cause/Exemples** | **Action suggérée** | **Remarques sur la nouvelle tentative automatique/immédiate** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello serveur n’a pas répondu toohello a demandé l’opération dans hello spécifié temps, ce qui est contrôlé par [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). serveur de Hello a peut-être été terminée hello a demandé l’opération. Cela peut se produire en raison de toonetwork ou autres délais d’infrastructure. |Vérifiez l’état du système hello par souci de cohérence, puis réessayez si nécessaire.<br /> Consultez [TimeoutException](#timeoutexception). |Nouvelle tentative peut vous aider dans certains cas ; Ajoutez toocode logique de nouvelle tentative. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hello a demandé l’opération utilisateur n’est pas autorisée dans hello serveur ou le service. Message d’exception hello pour plus d’informations, consultez. Par exemple, [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) génère cette exception si le message de salutation reçu [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode. |Vérifiez le code de hello et la documentation de hello. Vérifiez que hello opération demandée n’est valide. |Une nouvelle tentative ne sera pas bénéfique. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Une tentative est effectuée tooinvoke une opération sur un objet qui a déjà été fermée, interrompue ou supprimée. Dans de rares cas, la transaction ambiante de hello est déjà supprimée. |Code de hello et assurez-vous qu’il n’appelle pas les opérations sur un objet supprimé. |Une nouvelle tentative ne sera pas bénéfique. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) objet n’a pas pu obtenir un jeton, jeton de hello n’est pas valide ou jeton de hello ne contient pas de hello revendications tooperform requis hello opération. |Assurez-vous que le fournisseur de jetons hello est créé avec les valeurs correctes hello. Vérifiez la configuration de hello Hello service de contrôle d’accès. |Nouvelle tentative peut vous aider dans certains cas ; Ajoutez toocode logique de nouvelle tentative. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Un ou plusieurs arguments de type fournis (méthode) toohello ne sont pas valides. Hello URI fourni trop[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [créer](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) contient des segments de chemin d’accès. schéma d’URI Hello fourni trop[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [créer](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) n’est pas valide. valeur de la propriété Hello est supérieure à 32 Ko. |Vérifiez le code d’appel hello et assurez-vous que les arguments hello sont corrects. |Une nouvelle tentative ne sera pas bénéfique. |
| [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) <br /> [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception) |Entité associée hello opération n’existe pas ou il a été supprimé. |Assurez-vous que l’entité hello existe. |Une nouvelle tentative ne sera pas bénéfique. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Tenter de tooreceive un message avec un numéro de séquence donné. Ce message est introuvable. |Assurez-vous que le message de salutation n’a pas déjà été reçu. Vérifiez toosee de file d’attente de lettres mortes hello si le message de salutation a été lettre morte. |Une nouvelle tentative ne sera pas bénéfique. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Client n’est pas en mesure de tooestablish une tooEvent connexion Hub. |Assurez-vous que le nom d’hôte hello fourni est correct et hello hôte est accessible. |Une nouvelle tentative peut aider en cas de problèmes de connectivité intermittents. |
| [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) <br /> [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) |Service n’est pas demande de hello en mesure de tooprocess pour l’instant. |Client, vous pouvez attendre un certain temps, puis recommencez l’opération de hello. <br /> Consultez [ServerBusyException](#serverbusyexception). |Le client peut réessayer après un certain temps. Si une nouvelle tentative provoque une exception différente, vérifiez le comportement de nouvelle tentative de cette exception. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Lock-token associé au message de salutation a expiré ou lock-token hello est introuvable. |Supprimer le message de type hello. |Une nouvelle tentative ne sera pas bénéfique. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Le verrou associé à cette session est perdu. | Abandonner hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) objet. |Une nouvelle tentative ne sera pas bénéfique. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Générique exception peut être levée dans hello suivant les cas de messagerie : une tentative est faite toocreate un [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) à l’aide d’un nom ou le chemin d’accès auquel appartient le type d’entité différent tooa (par exemple, une rubrique). Une tentative est agrandie toosend un message à 256 Ko. Hello serveur ou le service a rencontré une erreur lors du traitement de demande de hello. Consultez le message d’exception hello pour plus d’informations. Il s'agit généralement d'une exception temporaire. |Vérifier le code de hello et garantir que seuls les objets sérialisables sont utilisés pour le corps du message hello (ou utiliser un sérialiseur personnalisé). Consultez la documentation de hello pour hello pris en charge les types de valeur des propriétés de hello et uniquement les types de prises en charge. Vérifiez hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) propriété. S’il s’agit **true**, vous pouvez retenter hello opération. |Le comportement de la nouvelle tentative n'est pas défini et peut ne pas être utile. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Essayez de toocreate une entité dont le nom est déjà utilisé par une autre entité dans cet espace de noms de service. |Supprimer l’entité existante de hello ou choisissez un autre nom pour hello entité toobe est créé. |Une nouvelle tentative ne sera pas bénéfique. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Hello entité de messagerie a atteint sa taille maximale autorisée. Cela peut se produire si le nombre maximal hello de récepteurs (ce qui est de 5) a déjà été ouverte sur un niveau de regroupement par consommateur. |Créer l’espace dans l’entité de hello par la réception de messages à partir de l’entité de hello ou ses files d’attente secondaire. <br /> Consultez [QuotaExceededException](#quotaexceededexception). |Nouvelle tentative peut vous aider si les messages ont été supprimés dans hello entre-temps. |
|  | | | |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Essayez de tooaccept qu'une session avec un ID de session spécifique, mais que la session de hello est actuellement verrouillée par un autre client. |Assurez-vous que la session de hello est déverrouillée par d’autres clients. |Nouvelle tentative peut vous aider si la session de hello a été libérée Bonjour intermédiaires. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Trop d’opérations font partie de la transaction de hello. |Réduire le nombre de hello d’opérations qui font partie de cette transaction. |Une nouvelle tentative ne sera pas bénéfique. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Demande d'une opération d'exécution sur une entité désactivée. |Activer l’entité de hello. |Nouvelle tentative peut vous aider si les entités hello a été activée dans hello intermédiaire. |
| [Microsoft.ServiceBus.Messaging.MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) <br /> [Microsoft.Azure.EventHubs.MessageSizeExceededException](/dotnet/api/microsoft.azure.eventhubs.messagesizeexceededexception) | Une charge utile du message dépasse la limite de hello 256 Ko. Notez que la limite de 256 Ko de hello est hello taille totale du message, qui peut inclure des propriétés système et toute surcharge .NET. |Réduire la taille de hello de charge utile de message hello, puis recommencez l’opération de hello. |Une nouvelle tentative ne sera pas bénéfique. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Hello transaction ambiante (*Transaction.Current*) n’est pas valide. Elle a peut-être été terminée ou annulée. Une exception en interne peut fournir des informations supplémentaires. | |Une nouvelle tentative ne sera pas bénéfique. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Une opération est tentée sur une transaction incertaine, ou une tentative d’opération de hello toocommit et transaction de hello devient incertaine. |Votre application doit gérer cette exception (comme un cas spécial), comme les transactions hello ait déjà été validée. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indique que le quota d’une entité spécifique a été dépassé.

Cela peut se produire si le nombre maximal de hello de récepteurs (5) a déjà été ouverte sur un niveau de regroupement par consommateur.

### <a name="event-hubs"></a>Event Hubs
Event Hubs a une limite de 20 groupes de consommateurs par Event Hub. Lorsque vous essayez de toocreate plus, vous recevez un [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indique qu’une opération initiée par l’utilisateur prend plus de temps que le délai d’attente de hello opération. 

Pour les concentrateurs d’événements, délai d’attente hello est spécifiée dans le cadre de la chaîne de connexion hello, ou par [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). message d’erreur Hello lui-même peut-être varier, mais il contient toujours la valeur de délai d’attente hello spécifié pour l’opération en cours hello. 

### <a name="common-causes"></a>Causes courantes
Il existe deux causes communes pour cette erreur : une configuration incorrecte ou une erreur de service temporaire.

1. **Une configuration incorrecte** le délai d’attente de hello opération peut-être être trop petit pour la condition de fonctionnement hello. valeur par défaut de Hello hello opération délai de connexion dans le client hello SDK est de 60 secondes. Vérifiez toosee si votre code possède la valeur de hello toosomething trop petite. Notez cette condition hello du réseau de hello et l’utilisation du processeur peut affecter hello temps d’une opération particulière toocomplete, donc le délai d’attente de hello opération ne doit pas être défini tooa très petite valeur.
2. **Erreur du service temporaire** parfois hello service Event Hubs peut subir des retards de traitement des requêtes, par exemple, pendant les périodes de trafic élevé. Dans ce cas, vous pouvez réessayer l’opération après un délai, jusqu'à ce que l’opération de hello a réussi. Hello même opération échoue encore après plusieurs tentatives, visitez hello [site d’état des services Azure](https://azure.microsoft.com/status/) toosee s’il existe des interruptions de service connu.

## <a name="serverbusyexception"></a>ServerBusyException

Une exception [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) ou [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) indique qu’un serveur est surchargé. Il existe deux codes d’erreur pertinents pour cette exception.

### <a name="error-code-50002"></a>Code d’erreur 50002

Cette erreur peut se produire pour deux raisons :

1. charge de Hello n’est pas distribué uniformément entre toutes les partitions sur hello concentrateur d’événements et une partition accès hello débit local unité limitation.
    
    Solution : Révision de la stratégie de distribution hello partition ou la tentative de [EventHubClient.Send(eventDataWithOutPartitionKey)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) peut vous aider.

2. espace de noms Hello concentrateurs d’événements n’a pas suffisamment d’unités de débit (vous pouvez vérifier hello **métriques** panneau dans le panneau espace de noms de concentrateurs d’événements Bonjour [portail Azure](https://portal.azure.com) tooconfirm). Notez que le portail de hello affiche des informations agrégées (1 minute), mais nous mesurer le débit de hello en temps réel : il est qu’une estimation.

    Résolution : Augmente le débit de hello unités sur l’espace de noms hello peuvent aider. Cela sur le portail de hello hello **échelle** panneau du panneau espace de noms des concentrateurs d’événements hello.

### <a name="error-code-50001"></a>Code d’erreur 50001

Cette erreur survient rarement. Il se produit lorsque le conteneur hello exécute le code de votre espace de noms est faible sur le processeur : charger des concentrateurs d’événements pas plus de quelques secondes avant hello équilibrage commence.


## <a name="next-steps"></a>Étapes suivantes
Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)
* [Create an Event Hub](event-hubs-create.md) (Créer un Event Hub)
* [FAQ sur les hubs d'événements](event-hubs-faq.md)
