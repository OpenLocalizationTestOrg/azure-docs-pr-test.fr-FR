---
title: aaaCreate les applications qui utilisent des rubriques et abonnements Azure Service Bus | Documents Microsoft
description: "Introduction toohello publication-abonnement fonctionnalités offertes par les abonnements et les rubriques Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: sethm
ms.openlocfilehash: f6d7de46ace7bd5b49de612db213ced789308d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Création d’applications qui utilisent des rubriques et des abonnements Service Bus
Azure Service Bus prend en charge un ensemble de technologies interlogicielles Cloud orientées messages, notamment une mise en file d'attente des messages fiable et une messagerie de publication/abonnement durable. Cet article s’appuie sur les informations de hello fournies dans [créer des applications qui utilisent des files d’attente Service Bus](service-bus-create-queues.md) et offre une introduction toohello des fonctionnalités de publication/abonnement offertes par les rubriques Service Bus.

## <a name="evolving-retail-scenario"></a>Scénario de vente au détail - La suite
Cet article poursuit le scénario de vente au détail hello utilisé dans [créer des applications qui utilisent des files d’attente Service Bus](service-bus-create-queues.md). Rappelez-vous que les données de vente des terminaux de Point de vente (PDV) individuels doivent être routé tooan inventaire gestion système qui utilise ce toodetermine données quand toobe réapprovisionné. Chaque terminal de PDV fournit ses données de vente en envoyant des messages toohello **DataCollectionQueue** file d’attente, où elles restent jusqu'à ce qu’ils sont reçus par le système de gestion des stocks hello, comme illustré ici :

![Service Bus 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

tooevolve ce scénario, une nouvelle spécification a été ajouté toohello système : propriétaire du magasin hello veut toobe toomonitor en mesure de performances de magasin de hello en temps réel.

tooaddress cette exigence, hello système doit « puiser » désactiver le flux de données de ventes hello. Nous voulons toujours que chaque message envoyé par toobe de terminaux de PDV hello envoyé toohello inventaire système de gestion des, mais nous voulons une autre copie de chaque message que nous pouvons utiliser le propriétaire du magasin vue toohello toopresent hello du tableau de bord.

Dans tous les cas comme celui-ci, dans lequel vous avez besoin de chaque toobe message consommé par plusieurs parties, vous pouvez utiliser Service Bus *rubriques*. Rubriques fournissent un modèle de publication/abonnement dans lequel chaque message publié devient disponible tooone ou plusieurs abonnements inscrit auprès de rubrique de hello. Au contraire, avec les files d'attente, chaque message est reçu par un seul consommateur.

Les messages sont envoyés tooa rubrique Bonjour même façon qu’ils sont envoyés à la file d’attente de tooa. Toutefois, les messages ne sont pas reçues à partir de la rubrique de hello directement ; ils sont reçus à partir d’abonnements. Vous pouvez considérer une rubrique de tooa abonnement comme une file d’attente virtuelle qui reçoit des copies de messages hello envoyés toothat rubrique. Les messages sont reçus à partir d’un abonnement hello même façon qu’ils sont reçus à partir d’une file d’attente.

Revenons un scénario de vente au détail toohello, file d’attente hello est remplacé par une rubrique et un abonnement est ajouté, le composant de système de gestion hello inventaire peut utiliser. système de Hello apparaît désormais comme suit :

![Service Bus 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

configuration de Hello ici identique conception basée sur la file d’attente précédente de toohello. Autrement dit, les messages envoyés toohello rubrique sont routé toohello **inventaire** abonnement, à partir de quels hello **système de gestion des stocks** les consomme.

Dans le tableau de bord de gestion de commande toosupport hello, nous créons un deuxième abonnement sur la rubrique de hello, comme indiqué ici :

![Service Bus 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

Avec cette configuration, chaque message des terminaux de PDV de hello est mis à disposition tooboth hello **tableau de bord** et **inventaire** abonnements.

## <a name="show-me-hello-code"></a>Afficher le code de hello
article de Hello [créer des applications qui utilisent des files d’attente Service Bus](service-bus-create-queues.md) décrit comment toosign pour un compte Azure et créez un espace de noms de service. dépendances du Service Bus tooreference Hello plus simple moyen est tooinstall hello Service Bus [package Nuget](https://www.nuget.org/packages/WindowsAzure.ServiceBus/). Vous pouvez également trouver hello bibliothèques Service Bus dans le cadre de hello Azure SDK. Bonjour téléchargement est disponible à l’adresse hello [page de téléchargement de Windows Azure SDK](https://azure.microsoft.com/downloads/).

### <a name="create-hello-topic-and-subscriptions"></a>Créer des abonnements et la rubrique de hello
Opérations de gestion de Service Bus entités de messagerie (files d’attente et publication/abonnement rubriques) sont effectuent via hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) classe. Informations d’identification appropriées sont requises dans la commande toocreate un **NamespaceManager** instance pour un espace de noms particulier. Service Bus utilise un modèle de sécurité basé sur une [signature d’accès partagé (SAP)](service-bus-sas.md). Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) classe représente un fournisseur de jetons de sécurité avec les méthodes de fabrique intégrées retournant des fournisseurs de jeton bien connus. Nous allons utiliser un [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) informations d’identification de méthode toohold hello SAP. Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) instance est ensuite créée avec l’adresse de base hello d’espace de noms Service Bus hello et le fournisseur de jetons hello.

Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) classe fournit des méthodes toocreate, énumérer et supprimer des entités de messagerie. Hello code fourni ici montre comment hello **NamespaceManager** instance est créé et utilisé toocreate hello **DataCollectionTopic** rubrique.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Notez qu’il existe des surcharges de hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) méthode qui vous permettent de tooset les propriétés de la rubrique de hello. Par exemple, vous pouvez définir hello time-to-live (TTL) par défaut pour les messages envoyés toohello rubrique. Ensuite, ajoutez hello **inventaire** et **tableau de bord** abonnements.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-toohello-topic"></a>Rubrique toohello de messages d’envoi
Pour des opérations d’exécution sur les entités Service Bus ; par exemple, pour l’envoi et la réception de messages, une application doit tout d’abord créer un objet [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory). Similaire toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) classe hello **MessagingFactory** instance est créée à partir de l’adresse de base hello d’espace de noms de service hello et le fournisseur de jetons hello.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

Tooand envoyés des messages reçu à partir des rubriques Service Bus, sont des instances de hello [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) classe. Cette classe se compose d’un ensemble de propriétés standard (tels que [étiquette](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) et [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un dictionnaire de propriétés de l’application toohold utilisées et un corps de données d’application arbitraire. Une application peut définir le corps de hello en passant tout objet sérialisable (hello exemple suivant passe dans un **SalesData** objet qui représente les données de ventes hello de terminal de PDV de hello), qui sera utilisée hello [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) objet de hello tooserialize. Une autre possibilité consiste à fournir un objet [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx).

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

rubrique de Hello plus simple façon toosend messages toohello est toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate un [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) objet directement à partir de hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instance :

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>Réception des messages d’un abonnement
Les files d’attente de toousing similaire, tooreceive des messages à partir d’un abonnement, vous pouvez utiliser un [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objet que vous créez directement à partir de hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) à l’aide de [ CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Vous pouvez utiliser l’une de hello deux différents modes de réception (**ReceiveAndDelete** et **PeekLock**), comme indiqué dans [créer des applications qui utilisent des files d’attente Service Bus](service-bus-create-queues.md).

Notez que lorsque vous créez un **MessageReceiver** pour les abonnements, hello *entityPath* paramètre se présente sous forme de hello `topicPath/subscriptions/subscriptionName`. Par conséquent, toocreate un **MessageReceiver** pour hello **inventaire** abonnement Hello **DataCollectionTopic** rubrique, *entityPath*doit être défini trop`DataCollectionTopic/subscriptions/Inventory`. code de Hello apparaît comme suit :

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

## <a name="subscription-filters"></a>Filtres d’abonnement
Jusqu'à présent, dans ce scénario, tous les messages envoyés toohello rubrique sont effectuées les abonnements disponibles tooall inscrit. expression de clé Hello ici est « accessible. » Bien que les abonnements Service Bus afficher tous les messages envoyés toohello rubrique, vous pouvez copier uniquement un sous-ensemble de ces files d’attente de messages toohello virtuelle des abonnements. Pour ce faire, il faut utiliser des *filtres* d’abonnement. Lorsque vous créez un abonnement, vous pouvez fournir une expression de filtre sous forme de hello d’un prédicat de type SQL92 qui opère sur les propriétés de message de type hello hello, les deux hello propriétés système (par exemple, [étiquette](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) et l’application hello propriétés, telles que **StoreName** dans l’exemple précédent de hello.

Évolution hello scénario tooillustrate cela, un deuxième magasin est scénario de vente au détail toobe tooour ajouté. Chiffres des ventes de tous les terminaux hello POS à partir des deux magasins ont toujours système de gestion du stock toobe routé toohello centralisée, mais un gestionnaire de magasin à l’aide d’outil de tableau de bord hello est uniquement intéressé par les performances de hello de ce magasin. Vous pouvez utiliser l’abonnement filtrage tooachieve cela. Notez que lorsque les terminaux de PDV de hello publient des messages, ils définir hello **StoreName** propriété d’application sur le message de type hello. Étant donné deux magasins, par exemple **Redmond** et **Seattle**, terminaux hello POS Bonjour Redmond stockent horodatage leurs données de ventes des messages avec un **StoreName** égal trop **Redmond**, alors que hello Seattle stocker l’utilisation des terminaux de PDV un **StoreName** égal trop**Seattle**. le Gestionnaire de magasins Hello Hello Redmond stocker uniquement souhaite toosee des données à partir de ses terminaux de PDV. système de Hello apparaît comme suit :

![Service-Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

tooset ce routage, vous créez hello **tableau de bord** abonnement comme suit :

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

Avec cette [filtre d’abonnement](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), seuls les messages hello **StoreName** propriété trop**Redmond** sera copié toohello la file d’attente virtuelle pour hello **Tableau de bord** abonnement. Il est beaucoup plus toosubscription le filtrage, toutefois. Applications peuvent avoir plusieurs règles de filtrage par abonnement dans Ajout toohello capacité toomodify hello les propriétés d’un message lorsqu’il passe de file d’attente virtuelle de l’abonnement tooa.

## <a name="summary"></a>Résumé
Tous les hello raisons toouse queuing décrits dans [créer des applications qui utilisent des files d’attente Service Bus](service-bus-create-queues.md) s’appliquent également tootopics, en particulier :

* Découplage temporel : message producteurs et consommateurs n’ont pas de toobe en ligne à hello même temps.
* Nivellement de charge : les pics de charge sont nivelés par rubrique hello l’activation de consommation toobe d’applications configuré pour une charge moyenne au lieu de pics de charge.
* Équilibrage : file d’attente de tooa similaires, vous pouvez avoir plusieurs consommateurs concurrents à l’écoute sur un seul abonnement avec chaque message remis tooonly un des consommateurs hello, ce qui équilibre la charge.
* Faible couplage : vous pouvez faire évoluer hello réseau de messagerie sans affecter les points de terminaison existants ; par exemple, ajouter des abonnements ou modifier les filtres tooa rubrique tooallow de nouveaux consommateurs.

## <a name="next-steps"></a>Étapes suivantes

Consultez [créer des applications qui utilisent des files d’attente Service Bus](service-bus-create-queues.md) pour plus d’informations sur comment toouse les files d’attente dans un scénario de vente au détail hello POS.

