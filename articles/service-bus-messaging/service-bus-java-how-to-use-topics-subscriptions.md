---
title: rubriques de Azure Service Bus aaaHow toouse avec Java | Documents Microsoft
description: Utilisez les rubriques et abonnements Service Bus dans Azure.
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a>Comment toouse Service Bus rubriques et les abonnements avec Java

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Ce guide décrit comment toouse Service Bus rubriques et abonnements. exemples de Hello sont écrits en Java et utiliser hello [SDK Azure pour Java][Azure SDK for Java]. Hello scénarios abordés incluent **création de rubriques et abonnements**, **création de filtres d’abonnement**, **envoi rubrique tooa de messages**, **réception les messages à partir d’un abonnement**, et **suppression des rubriques et abonnements**.

## <a name="what-are-service-bus-topics-and-subscriptions"></a>Présentation des rubriques et des abonnements Service Bus
Les rubriques et les abonnements Service Bus prennent en charge un modèle de communication de messagerie *de publication et d'abonnement* . Lors de l’utilisation de rubriques et d’abonnements, les composants d’une application distribuée ne communiquent pas directement entre eux ; ils échangent plutôt des messages via une rubrique, qui fait office d’intermédiaire.

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

Contrairement aux files d’attente Service Bus, où chaque message est traité par un seul consommateur, les rubriques et les abonnements fournissent une forme de communication « un-à-plusieurs », à l'aide d'un modèle de publication et d'abonnement. Il est possible d’inscrire la rubrique de tooa plusieurs abonnements. Lorsqu’un message est envoyé à tooa rubrique, il est alors effectuée indépendamment disponible tooeach toohandle/processus d’inscription.

Une rubrique de tooa abonnement ressemble à une file d’attente virtuelle qui reçoit des copies des messages de type hello qui ont été envoyés toohello rubrique. Vous pouvez éventuellement enregistrer les règles de filtre pour une rubrique à la fois par abonnement, ce qui vous permet de restreindre/toofilter le sujet tooa messages sont reçus par les abonnements à la rubrique.

Abonnements et rubriques Service Bus permettent tooscale tooprocess un très grand nombre de messages sur un très grand nombre d’utilisateurs et des applications.

## <a name="create-a-service-namespace"></a>Création d'un espace de noms de service
toobegin à l’aide des rubriques et abonnements Service Bus dans Azure, vous devez d’abord créer un espace de noms, qui fournit un conteneur d’étendue pour adresser les ressources Service Bus au sein de votre application.

toocreate un espace de noms :

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurer votre toouse application Service Bus
Vérifiez que vous avez installé hello [SDK Azure pour Java] [ Azure SDK for Java] avant de générer cet exemple. Si vous utilisez Eclipse, vous pouvez installer hello [boîte à outils Azure pour Eclipse] [ Azure Toolkit for Eclipse] incluant hello SDK Azure pour Java. Vous pouvez ensuite ajouter hello **bibliothèques Microsoft Azure pour Java** tooyour projet :

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

Ajoutez hello suit `import` haut de toohello instructions hello du fichier de Java :

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

Ajoutez hello les bibliothèques Azure pour Java tooyour générer le chemin d’accès et l’inclure dans votre assembly de déploiement du projet.

## <a name="create-a-topic"></a>Création d'une rubrique
Les opérations de gestion des rubriques Service Bus peuvent être effectuées par le biais de la classe **ServiceBusContract**. A **ServiceBusContract** objet est construit avec une configuration appropriée qui encapsule le jeton SAS avec les autorisations toomanage et hello **ServiceBusContract** classe est point unique de hello de la communication avec Azure.

Hello **ServiceBusService** classe fournit des méthodes toocreate, énumérer et supprimer des rubriques. Hello suivant montre l’exemple de comment un **ServiceBusService** objet peut être utilisé toocreate une rubrique nommée `TestTopic`, avec un espace de noms appelé `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Il existe des méthodes sur **TopicInfo** qui permettent des propriétés de la rubrique hello à définir (par exemple : tooset hello par défaut time-to-live (TTL) valeur toobe appliqué toomessages envoyé toohello rubrique). Hello suivant montre comment toocreate une rubrique nommée `TestTopic` avec une taille maximale de 5 Go :

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

Notez que vous pouvez utiliser hello **listTopics** méthode sur **ServiceBusContract** objets toocheck si une rubrique portant le nom spécifié existe déjà dans un espace de noms de service.

## <a name="create-subscriptions"></a>Création d’abonnements
Abonnements tootopics sont également créés par hello **ServiceBusService** classe. Les abonnements sont nommés et peuvent avoir un filtre facultatif qui limite l’ensemble de hello de messages transmis de file d’attente virtuelle de l’abonnement toohello.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Créer un abonnement avec le filtre par défaut (MatchAll) hello
Hello **MatchAll** filtre est hello par défaut qui est utilisé si aucun filtre n’est spécifiée lors de la création d’un abonnement. Hello lorsque **MatchAll** filtre est utilisé, la rubrique de toohello publié tous les messages sont placés dans la file d’attente virtuelle de l’abonnement. Hello exemple suivant crée un abonnement nommé « AllMessages » et utilise hello par défaut **MatchAll** filtre.

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a>Création d’abonnements avec des filtres
Vous pouvez également créer des filtres qui vous tooscope lesquelles messages envoyés tooa rubrique doit apparaître dans un abonnement à une rubrique spécifique.

Bonjour type de filtre pris en charge par les abonnements plus souple est la [SqlFilter][SqlFilter], qui implémente un sous-ensemble de SQL92. Filtres SQL fonctionnent sur les propriétés hello de messages hello qui sont publiées toohello rubrique. Pour plus d’informations sur les expressions hello qui peuvent être utilisées avec un filtre SQL, consultez hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxe.

Hello exemple suivant crée un abonnement nommé `HighMessages` avec un [SqlFilter] [ SqlFilter] objet qui sélectionne uniquement les messages qui ont personnalisé **MessageNumber** propriété est supérieure à 3 :

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

De même, hello exemple suivant crée un abonnement nommé `LowMessages` avec un [SqlFilter] [ SqlFilter] objet qui sélectionne uniquement les messages qui ont un **MessageNumber** propriété inférieur ou égal too3 :

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

Lorsqu’un message est envoyé maintenant trop`TestTopic`, il sera toujours remis tooreceivers abonné toohello `AllMessages` abonnement et remis de manière sélective tooreceivers abonné toohello `HighMessages` et `LowMessages` (des abonnements selon le contenu du message).

## <a name="send-messages-tooa-topic"></a>Rubrique tooa de messages d’envoi
toosend une rubrique de Service Bus message tooa, votre application obtient un **ServiceBusContract** objet. Hello de code suivant montre comment toosend un message pour hello `TestTopic` rubrique créée précédemment dans hello `HowToSample` espace de noms :

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

Messages envoyés tooService Bus rubriques sont des instances de la [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage][BrokeredMessage]* objets comportent un ensemble de méthodes standard (tels que **setLabel** et **TimeToLive**), un dictionnaire qui est utilisé toohold personnalisé les propriétés spécifiques à l’application et un corps de données d’application arbitraire. Une application peut définir le corps du message de hello en passant tout objet sérialisable dans le constructeur hello de la [BrokeredMessage][BrokeredMessage]et hello approprié **DataContractSerializer**  puis sera utilisé tooserialize hello objet. Une autre possibilité consiste à fournir un **java.io.InputStream**.

Hello exemple suivant montre comment les messages de test de toosend cinq toothe `TestTopic` **MessageSender** nous avons obtenu dans l’extrait de code hello ci-dessus.
Notez comment hello **MessageNumber** varie en fonction de valeur de la propriété de chaque message sur l’itération hello de boucle de hello (Cela permet de déterminer les abonnements reçoivent) :

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

Rubriques Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md). en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko. Il n’existe aucune limite sur le nombre de hello de messages conservés dans une rubrique, mais il existe une limite de taille totale de hello de messages hello détenus par une rubrique. Cette taille de rubrique est définie au moment de la création. La limite maximale est de 5 Go.

## <a name="how-tooreceive-messages-from-a-subscription"></a>Comment tooreceive les messages à partir d’un abonnement
tooreceive des messages à partir d’un abonnement, utilisez un **ServiceBusContract** objet. Ces messages reçus peuvent fonctionner dans deux modes différents : **ReceiveAndDelete** et **PeekLock**.

Lors de l’utilisation de hello **ReceiveAndDelete** , le mode de réception est une opération coup - autrement dit, lorsque le Service Bus reçoit une demande de lecture d’un message, il marque le message de type hello comme ayant été consommé et le retourne toothe application. **ReceiveAndDelete** mode est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec. toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter. Étant donné que le Service Bus sera a marqué le message comme ayant été consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.

Dans **PeekLock** , le mode de réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application. Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant **supprimer** sur le message de salutation reçu. Lorsque le Service Bus voit hello **supprimer** appel, il marque le message de type hello comme ayant été consommé et supprimez-le de la rubrique de hello.

Hello exemple ci-dessous montre comment les messages peuvent être reçus et traités à l’aide de **PeekLock** mode (pas le mode hello par défaut). Hello exemple ci-dessous effectue une boucle et traite les messages hello « HighMessages » abonnement et se termine lorsqu’il n’y a plus aucun message (il peut également être définir toowait pour les nouveaux messages).

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Comment toohandle application tombe en panne et messages illisibles
Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message. Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello **unlockMessage** méthode sur le message de salutation reçu (au lieu de hello **deleteMessage** méthode). Cette opération provoquent le message de type hello toounlock Service Bus au sein de la rubrique de hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.

Il existe également un délai d’attente d’un message verrouillé dans la rubrique, et si l’application hello échoue le message de type hello tooprocess avant le délai d’attente de verrou expire (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.

Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello **deleteMessage** demande est émise, puis le message de type hello sera redistribué toohello application lors de son redémarrage. Cela est souvent appelé **au moins une fois le traitement**, autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué. Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message. Cela est souvent obtenue à l’aide de hello **getMessageId** méthode de message de type hello, qui reste constante entre les tentatives de remise.

## <a name="delete-topics-and-subscriptions"></a>Suppression de rubriques et d'abonnements
Hello rubriques toodelete de façon principal et d’abonnements est toouse un **ServiceBusContract** objet. Suppression d’une rubrique supprime également tous les abonnements qui sont inscrits auprès de rubrique de hello. Les abonnements peuvent aussi être supprimés de manière indépendante.

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de files d’attente Service Bus, consultez [files d’attente Service Bus, rubriques et abonnements] [ Service Bus queues, topics, and subscriptions] pour plus d’informations.

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
