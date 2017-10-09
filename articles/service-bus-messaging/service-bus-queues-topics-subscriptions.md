---
title: "aaaOverview de messagerie des files d’attente, rubriques et abonnements Azure Service Bus | Documents Microsoft"
description: "Présentation des entités de messagerie Service Bus"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a>Files d’attente, rubriques et abonnements Service Bus

Microsoft Azure Service Bus prend en charge un ensemble de technologies middleware Cloud orientées messages, notamment la mise en file d’attente de messages fiable et la messagerie de publication/abonnement durable. Ces fonctionnalités de messagerie « réparties » peuvent être considérées comme découplée fonctionnalités prise en charge la publication-abonnement de messagerie, temporelle découplage et scénarios à l’aide de la structure de messagerie Service Bus hello d’équilibrage de charge. La communication découplée présente de nombreux avantages ; par exemple, les clients et les serveurs peuvent se connecter en fonction des besoins et exécuter leurs opérations de manière asynchrone.

entités de messagerie Hello qui forment le cœur de hello de hello fonctionnalités dans le Bus des services de messagerie sont les files d’attente, rubriques et abonnements et règles/actions.

## <a name="queues"></a>Files d’attente

Les files d’attente offrent *First In, First Out* tooone de remise de message (FIFO) ou plusieurs consommateurs concurrents. Autrement dit, les messages sont généralement attendu toobe reçu et traité par les récepteurs hello dans l’ordre de hello dans lequel ils ont été ajoutés à la file d’attente de toohello, et chaque message est reçu et traité par un consommateur d’un seul message. Des principaux avantages de l’utilisation de files d’attente est tooachieve « découplage temporel » des composants d’application. Hello en d’autres termes, les producteurs (expéditeurs) et de consommateurs (récepteurs) n’ont pas de toobe envoi et de réception des messages à hello même temps, car les messages sont stockés durablement dans la file d’attente hello. En outre, le producteur de hello ne pas ont toowait pour une réponse à un consommateur de hello dans l’ordre toocontinue tooprocess et envoyer des messages.

Un avantage connexe est « chargement d’audit, » qui permet des producteurs et consommateurs toosend et recevoir des messages à différentes vitesses. Dans de nombreuses applications, la charge système hello varie dans le temps ; Toutefois, le temps de traitement de hello requis pour chaque unité de travail est généralement constant. Fait message producteurs et consommateurs avec une file d’attente signifie que hello consommation d’application uniquement a toobe toobe approvisionné toohandle en mesure de charge moyenne au lieu de pics de charge. profondeur Hello de file d’attente hello augmente et diminue comme hello les charge entrante varie. Cela plus économique avec le montant de toohello se charge de l’infrastructure requise tooservice hello application. En tant que hello charge augmente, plusieurs processus de travail peuvent être ajouté tooread à partir de la file d’attente hello. Chaque message est traité par un seul hello de processus de travail. En outre, cette extraction d’équilibrage de charge permet une utilisation optimale des ordinateurs de travail hello même si hello ceux-ci diffèrent avec respect tooprocessing de puissance, car ils extrairont les messages à leur propre taux maximal. Ce modèle est souvent appelé modèle avec le modèle de « consommateurs concurrents » hello.

À l’aide de toointermediate les files d’attente entre les producteurs de message et les consommateurs fournit un couplage faible inhérent entre les composants de hello. Producteurs et consommateurs n’étant pas prenant en charge les unes des autres, un consommateur peut être mis à niveau sans avoir aucun effet sur les producteurs de hello.

La création d’une file d’attente est un processus en plusieurs étapes. Effectuer des opérations de gestion pour les entités (files d’attente et rubriques) via hello de messagerie Service Bus [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) (classe), qui est construit en fournissant l’adresse de base hello Hello Service Bus espace de noms et hello informations d’identification. [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) fournit les méthodes toocreate, énumérer et supprimer des entités de messagerie. Après avoir créé un [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) objet hello SAS nom et la clé et une gestion d’espace de noms de service de l’objet, vous pouvez utiliser hello [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) file d’attente de méthode toocreate hello. Par exemple :

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

Vous pouvez ensuite créer un objet de file d’attente et une fabrique de messagerie avec hello URI Service Bus en tant qu’argument. Par exemple :

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

Vous pouvez ensuite envoyer file d’attente de messages toohello. Par exemple, si vous avez une liste de messages répartis appelée `MessageList`, de code hello apparaît similaire toohello suivantes :

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

Vous recevez les messages à partir de la file d’attente hello comme suit :

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

Bonjour [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) de réception hello mode, l’opération est prise de vue unique ; autrement dit, lorsque le Service Bus reçoit la demande de hello, il marque le message de type hello comme ayant été consommé et le retourne toohello application. **ReceiveAndDelete** mode est le modèle le plus simple hello et convient le mieux pour les scénarios qui Bonjour application tolère ne pas le traitement de message dans l’événement hello d’un échec. toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter. Étant donné que le Service Bus marque le message comme ayant été consommé, quand l’application hello redémarre et commence à consommer des messages de type hello, elle aura manqué message de type hello qui a été consommée toohello préalable incident.

Dans [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) , le mode de réception hello devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit la demande de hello, il recherche hello toobe de message suivant consommée, il verrouille tooprevent autres consommateurs de le recevoir, puis retourne toohello application. Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) sur le message de salutation reçu. Lorsque le Service Bus voit hello **Complete** appel, il marque de message de type hello comme ayant été consommé.

Si l’application hello ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello [abandonner](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) méthode sur le message de salutation reçu (au lieu de [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Cela permet de message de type hello toounlock Service Bus et le rendre disponible toobe de nouveau reçu, soit en hello même consommateur ou par un autre consommateur concurrent. Deuxièmement, il est un délai d’attente associé de verrou de hello et si application hello échoue tooprocess hello message avant de délai d’attente de verrou hello expire (par exemple, si de l’application hello se bloque), Service Bus déverrouille le message de type hello et rend disponible toobe de nouveau reçu (essentiellement en effectuant un [abandonner](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) opération par défaut).

Notez que dans hello événement hello application se bloque après le traitement de message de type hello, mais avant hello **Complete** demande est émise, le message de type hello est redistribué toohello application lors de son redémarrage. Cette opération est souvent appelée *Au moins une fois*. Chaque message est traité au moins une fois. Toutefois, dans certain hello situations même message peut être redistribué. Si le scénario de hello ne tolère pas le traitement dupliqué, puis une logique supplémentaire est requise dans les doublons toodetect hello application qui peuvent être obtenus en fonction de hello **MessageId** propriété de message de type hello, qui reste constante entre les tentatives de remise. Cette opération est connue sous le nom de traitement *seulement une fois*.

## <a name="topics-and-subscriptions"></a>Rubriques et abonnements
Dans tooqueues contraste, dans lequel chaque message est traité par un seul consommateur, *rubriques* et *abonnements* fournissent un formulaire de type un-à-plusieurs de communication dans un *depublication/abonnement* modèle. Utile pour la mise à l’échelle toovery un grand nombre de destinataires, chaque message publié est mis abonnement disponible tooeach inscrit auprès de hello rubrique. Les messages sont envoyés tooa rubrique et remis tooone ou plus les abonnements associés, en fonction des règles de filtrage qui peuvent être définis sur par abonnement. les abonnements de Hello peuvent utiliser des messages de type hello toorestrict des filtres supplémentaires qu’ils souhaitent tooreceive. Les messages sont envoyés tooa rubrique Bonjour même façon qu’ils sont envoyés file d’attente tooa, mais les messages ne sont pas reçus directement à partir de la rubrique de hello. Ils sont envoyés depuis les abonnements. Un abonnement à une rubrique ressemble à une file d’attente virtuelle qui reçoit des copies de messages hello envoyés toohello rubrique. Les messages sont reçus à partir d’un abonnement identique moyen toohello ils sont reçus à partir d’une file d’attente.

À titre de comparaison, hello fonctionnalité d’envoi de message d’une file d’attente est mappé directement tooa rubrique et ses fonctionnalités de réception de messages mappé tooa abonnement. Entre autres choses, cela signifie que les abonnements prennent en charge hello mêmes modèles décrits précédemment dans cette section avec respect tooqueues : consommateur concurrent, découplage temporel, nivellement de charge et l’équilibrage de charge.

Création d’une rubrique d’est similaire toocreating une file d’attente, comme indiqué dans l’exemple hello dans la section précédente de hello. Créer l’URI du service hello et utilisez hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) client espace de noms de classe toocreate hello. Vous pouvez ensuite créer une rubrique à l’aide de hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) (méthode). Par exemple :

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

ensuite, ajoutez les abonnements comme souhaité :

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

vous pouvez ensuite créer un client de rubrique. Par exemple :

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

À l’aide de l’expéditeur du message hello, vous pouvez envoyer et recevoir des messages tooand à partir de la rubrique de hello, comme indiqué dans la section précédente de hello. Par exemple :

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

Tooqueues similaires, les messages sont reçus à partir d’un abonnement à l’aide un [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) de l’objet au lieu d’un [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) objet. Créez hello abonnement client, en passant le nom hello de rubrique hello, nom hello d’abonnement de hello, et (éventuellement) hello mode de réception en tant que paramètres. Par exemple, avec hello **inventaire** abonnement :

```csharp
// Create hello subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a>Règles et actions
Dans de nombreux scénarios, les messages ayant des caractéristiques spécifiques doivent être traités différemment. tooenable, vous pouvez configurer les messages toofind abonnements qui possèdent les propriétés souhaitées, puis effectuez certaines propriétés toothose de modifications. Bien que les abonnements Service Bus afficher tous les messages envoyés toohello rubrique, vous pouvez copier uniquement un sous-ensemble de ces files d’attente de messages toohello virtuelle des abonnements. Pour ce faire, il faut utiliser des filtres d’abonnement. Ces modifications sont appelées *actions de filtrage*. Lorsqu’un abonnement est créé, vous pouvez fournir une expression de filtre qui opère sur les propriétés hello de message de type hello, les deux hello propriétés système (par exemple, **étiquette**) et les propriétés personnalisées (par exemple, **StoreName**.) hello expression de filtre SQL est facultative dans ce cas ; sans une expression de filtre SQL, toute action de filtre définie sur un abonnement sera effectuée sur tous les messages hello pour cet abonnement.

À l’aide de hello précédent exemple, les messages toofilter provenant uniquement de **Store1**, vous devez créer des abonnements du tableau de bord hello comme suit :

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

Avec ce filtre d’abonnement en place, seuls les messages hello `StoreName` propriété trop`Store1` sont copiés toohello la file d’attente virtuelle pour hello `Dashboard` abonnement.

Pour plus d’informations sur les valeurs de filtre possibles, consultez la documentation hello pour hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) et [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classes. Voir aussi hello [messagerie répartie : les filtres avancés](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) et [rubrique filtres](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) exemples.

## <a name="next-steps"></a>Étapes suivantes
Consultez les rubriques suivantes de hello rubriques pour plus d’informations et des exemples d’utilisation de messagerie Service Bus avancées.

* [Présentation de la messagerie Service Bus](service-bus-messaging-overview.md)
* [Didacticiel .NET sur la messagerie répartie Service Bus](service-bus-brokered-tutorial-dotnet.md)
* [Didacticiel REST sur la messagerie répartie Service Bus](service-bus-brokered-tutorial-rest.md)
* [Topic Filters sample ](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters) (Exemple de filtres de rubrique)
* [Brokered Messaging: Advanced Filters sample](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) (Messagerie répartie : exemples de filtres avancés)

