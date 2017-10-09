---
title: "aaaWrite les applications qui utilisent des files d’attente du Bus des services Azure | Documents Microsoft"
description: "Comment toowrite une application simple basée sur la file d’attente qui utilise Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 754d91b3-1426-405e-84b4-fd36d65b114a
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 93b75902a06becd6e33e05298e09f5669d0e2aef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-queues"></a>Création d'applications qui utilisent les files d'attente Service Bus
Cette rubrique décrit les files d’attente Service Bus et montre comment toowrite une application simple basée sur la file d’attente qui utilise le Service Bus.

Envisagez un scénario de vente au détail dans lequel les données de ventes à partir des sale (POS) terminaux doivent être routé de système de gestion de l’inventaire tooan qui utilise hello données toodetermine quand toobe réapprovisionné hello world. Cette solution utilise le Bus des services de messagerie pour la communication hello entre les terminaux hello et système de gestion des stocks hello, comme illustré dans la figure suivante de hello :

![Image 1 Files d’attente Service Bus](./media/service-bus-create-queues/IC657161.gif)

Chaque terminal de PDV fournit ses données de vente en envoyant des messages toohello **DataCollectionQueue**. Ces messages restent dans cette file d’attente jusqu'à ce qu’ils soient récupérés par le système de gestion des stocks hello. Ce modèle est souvent appelé *messagerie asynchrone*, car le terminal de PDV de hello n’a pas de toowait pour une réponse à partir du traitement de toocontinue hello inventaire administration système.

## <a name="why-queuing"></a>Avantages de la file d'attente
Avant d’examiner code hello requis tooset configuration de cette application, envisagez les avantages de hello de l’utilisation d’une file d’attente dans ce scénario, au lieu d’avoir des terminaux de PDV de hello parler directement (synchrone) toohello d’inventaire système de gestion.

### <a name="temporal-decoupling"></a>Découplage temporel
Avec le modèle de messagerie asynchrone hello, producteurs et consommateurs n’ont pas toobe en ligne au hello même temps. infrastructure de messagerie Hello stocke les messages de manière fiable jusqu'à ce que le récepteur hello est prêt tooreceive les. Cela signifie que les composants hello de l’application hello distribué peuvent être déconnectés, soit volontairement ; par exemple, pour la maintenance ou en raison du blocage d’un composant tooa, sans affecter l’ensemble du système hello. En outre, hello consommation d’application peut avoir uniquement toobe en ligne à certaines heures de la journée de hello. Par exemple, dans ce scénario de vente au détail, système de gestion des stocks hello peut avoir uniquement toocome en ligne après la fin de hello du jour ouvrable hello.

### <a name="load-leveling"></a>Niveau de charge
Dans de nombreuses applications charge système varie au fil du temps, alors que le temps de traitement de hello requis pour chaque unité de travail est généralement constant. Le fait de message producteurs et consommateurs un moyen de la file d’attente qui hello application consommatrice (traitement hello) n’a toobe configuré tooservice une moyenne de charge au lieu d’une charge de pointe. profondeur Hello de file d’attente hello augmentera et contrat comme hello charge entrante varie. Cela plus économique avec le montant de toohello se charge de l’infrastructure requise tooservice hello application.

![Image 2 Files d’attente Service Bus](./media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a>Équilibrage de la charge
En tant que hello charge augmente, plusieurs processus de travail peuvent être ajouté tooread à partir de la file d’attente de travail hello. Chaque message est traité par un seul hello de processus de travail. En outre, cette extraction d’équilibrage de charge permet une utilisation optimale des ordinateurs de travail hello même si hello ceux-ci diffèrent avec respect tooprocessing de puissance, car ils extrairont les messages à leur propre taux maximal. Ce modèle est souvent appelé modèle avec un modèle de consommateur concurrent hello.

![Image 3 Files d’attente Service Bus](./media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a>Couplage faible
À l’aide de toointermediate de files d’attente de messages entre les producteurs de message et les consommateurs fournit un couplage faible intrinsèque entre les composants de hello. Producteurs et consommateurs n’étant pas prenant en charge les unes des autres, un consommateur peut être mis à niveau sans avoir aucun effet sur les producteurs de hello. En outre, les hello topologie de messagerie peut évoluer sans affecter les points de terminaison existants hello. Nous y reviendrons plus en détail lorsque nous aborderons la publication/l'abonnement.

## <a name="show-me-hello-code"></a>Afficher le code de hello
Hello suivant indique la section Comment toouse Service Bus toobuild cette application.

### <a name="sign-up-for-an-azure-account"></a>Créer un compte Azure
Vous devez avoir un compte Azure dans toostart de commande fonctionne avec Service Bus. Si vous n’en avez pas, vous pouvez vous inscrire [ici](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF) pour obtenir un compte gratuit.

### <a name="create-a-namespace"></a>Créer un espace de noms
Une fois que vous avez un abonnement, vous pouvez [créer un espace de noms de service](service-bus-create-namespace-portal.md). Un espace de noms est un conteneur d’étendue pour un jeu d’entités Service Bus. Donnez un nom unique à votre nouvel espace de noms sur tous les comptes Service Bus. 

### <a name="install-hello-nuget-package"></a>Installation du package NuGet de hello
espace de noms Service Bus de hello toouse, une application doit faire référence hello assembly Service Bus, Microsoft.ServiceBus.dll. Vous pouvez trouver cet assembly dans le cadre de hello Microsoft Azure SDK et téléchargement de hello est disponible à l’adresse hello [page de téléchargement de Windows Azure SDK](https://azure.microsoft.com/downloads/). Toutefois, hello [package NuGet Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus) est hello de tooget de façon plus simple hello API Service Bus et tooconfigure votre application avec toutes les dépendances du Service Bus hello.

### <a name="create-hello-queue"></a>Créer la file d’attente hello
Opérations de gestion de Service Bus entités de messagerie (files d’attente et publication/abonnement rubriques) sont effectuent via hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) classe. Service Bus utilise un modèle de sécurité basé sur une [signature d’accès partagé (SAP)](service-bus-sas.md). Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) classe représente un fournisseur de jetons de sécurité avec les méthodes de fabrique intégrées retournant des fournisseurs de jeton bien connus. Nous allons utiliser un [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) informations d’identification de méthode toohold hello SAP. Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) instance est ensuite créée avec l’adresse de base hello d’espace de noms Service Bus hello et le fournisseur de jetons hello.

Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) classe fournit des méthodes toocreate, énumérer et supprimer des entités de messagerie. Hello code fourni ici montre comment hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) instance est créé et utilisé toocreate hello **DataCollectionQueue** file d’attente.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", 
                "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = 
    TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = 
    new NamespaceManager(uri, tokenProvider);
namespaceManager.CreateQueue("DataCollectionQueue");
```

Notez qu’il existe des surcharges de hello [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) méthode qui permettent les propriétés de toobe de file d’attente hello paramétrées. Par exemple, vous pouvez définir hello time-to-live (TTL) par défaut pour les messages envoyés de file d’attente toohello.

### <a name="send-messages-toohello-queue"></a>Envoyer la file d’attente de messages toohello
Pour des opérations d’exécution sur les entités Service Bus ; par exemple, pour l’envoi et la réception de messages, une application doit tout d’abord créer un objet [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory). Similaire toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) classe hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instance est créée à partir de l’adresse de base hello d’espace de noms de service hello et le fournisseur de jetons hello.

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

Les messages envoyés à et provenant du Service Bus files d’attente sont des instances de hello [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) classe. Cette classe se compose d’un ensemble de propriétés standard (tels que [étiquette](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) et [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un dictionnaire de propriétés de l’application toohold utilisées et un corps de données d’application arbitraire. Une application peut définir le corps de hello en passant tout objet sérialisable (hello exemple suivant passe dans un **SalesData** objet qui représente les données de ventes hello de terminal de PDV de hello), qui sera utilisée hello [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) objet de hello tooserialize. Une autre possibilité consiste à fournir un objet [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx).

Hello plus simple façon toosend messages tooa donné de file d’attente, dans notre cas hello **DataCollectionQueue**, est toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate un [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) objet directement à partir de hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instance.

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-hello-queue"></a>Réception de messages à partir de la file d’attente hello
tooreceive des messages à partir de la file d’attente hello, vous pouvez utiliser un [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objet que vous créez directement à partir de hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) à l’aide de [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Les destinataires de message peuvent fonctionner dans deux modes différents : **ReceiveAndDelete** et **PeekLock**. Hello [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) est définie lors de la création de récepteur des messages hello, comme un paramètre toohello [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) appeler.

Lorsque vous utilisez hello **ReceiveAndDelete** , le mode de réception hello est une opération de prise de vue unique ; autrement dit, lorsque le Service Bus reçoit la demande de hello, il marque le message de type hello comme ayant été consommé et le retourne toohello application. **ReceiveAndDelete** mode est le modèle le plus simple hello et convient le mieux pour les scénarios qui Bonjour application tolère ne pas le traitement de message si un échec toooccur. toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter. Étant donné que le Service Bus marqué le message de type hello comme ayant été consommé, quand redémarrage de l’application hello et commence à consommer des messages, elle aura manqué message de type hello qui a été consommé avant la panne de hello.

Dans **PeekLock** , le mode de réception hello devient une opération de deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit la demande de hello, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application. Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) sur le message de salutation reçu. Lorsque le Service Bus voit hello [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) appel, il marque de message de type hello comme ayant été consommé.

Deux autres issues sont possibles. Tout d’abord, si l’application hello ne peut pas tooprocess hello message pour une raison quelconque, il peut appeler [abandonner](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) sur le message de salutation reçu (au lieu de [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Cela entraîne le message de type hello toounlock Service Bus et le rendre disponible toobe de nouveau reçu, soit en hello même consommateur ou par un consommateur concurrent. En second lieu, il existe un délai d’attente associé au verrou de hello et si l’application hello ne peut pas traiter de message de type hello avant hello verrou délai d’expiration (par exemple, si de l’application hello se bloque), puis le Service Bus ne déverrouille hello message et le rendre disponible toobe de nouveau reçu (essentiellement en effectuant un [abandonner](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) opération par défaut).

Notez que si hello application se bloque une fois qu’il traite le message de type hello mais avant hello [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) demande a été émise, le message de type hello sera redistribué toohello application lors de son redémarrage. On appelle cela * au moins une fois * le traitement. Cela signifie que chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué. Si le scénario de hello ne peut pas tolérer le traitement dupliqué, une logique supplémentaire est requis dans les doublons de hello application toodetect. Cela peut être obtenue en fonction de hello [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) propriété de message de type hello. valeur Hello de cette propriété reste constante entre les tentatives de remise. Cette opération est connue sous le nom de traitement *seulement une fois*.

Hello code fourni ici reçoit et traite un message à l’aide de hello **PeekLock** mode, qui est la valeur par défaut hello si aucun [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) valeur est explicitement fournie.

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionQueue");
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

### <a name="use-hello-queue-client"></a>Utiliser le client de file d’attente hello
Hello exemples plus haut dans cette section créé [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) et [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objets directement à partir de hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) toosend et recevoir des messages à partir de la file d’attente de hello, respectivement. Une autre approche consiste à toouse un [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) objet, qui prend en charge envoyer et recevoir des opérations dans Ajout toomore fonctionnalités avancées, telles que les sessions.

```csharp
QueueClient queueClient = factory.CreateQueueClient("DataCollectionQueue");
queueClient.Send(bm);

BrokeredMessage message = queueClient.Receive();

try
{
    ProcessMessage(message);
    message.Complete();
}
catch (Exception e)
{
    message.Abandon();
} 
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de files d’attente, consultez [créer des applications qui utilisent des rubriques et abonnements Service Bus](service-bus-create-topics-subscriptions.md) toocontinue cette discussion à l’aide des fonctionnalités de publication/abonnement hello des rubriques Service Bus et abonnements.

