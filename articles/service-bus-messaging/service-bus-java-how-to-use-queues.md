---
title: "les files d’attente d’aaaHow toouse Azure Service Bus avec Java | Documents Microsoft"
description: "Découvrez comment toouse Service Bus de files d’attente dans Azure. Exemples de code écrits en Java."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a>Comment toouse Service Bus de files d’attente avec Java
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Cet article décrit comment les files d’attente de toouse Service Bus. exemples de Hello sont écrits en Java et utiliser hello [SDK Azure pour Java][Azure SDK for Java]. Hello scénarios abordés incluent **création de files d’attente**, **envoyer et recevoir des messages**, et **la suppression de files d’attente**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurer votre toouse application Service Bus
Vérifiez que vous avez installé hello [SDK Azure pour Java] [ Azure SDK for Java] avant de générer cet exemple. Si vous utilisez Eclipse, vous pouvez installer hello [boîte à outils Azure pour Eclipse] [ Azure Toolkit for Eclipse] incluant hello SDK Azure pour Java. Vous pouvez ensuite ajouter hello **bibliothèques Microsoft Azure pour Java** tooyour projet :

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

Ajoutez hello suit `import` haut de toohello instructions hello du fichier de Java :

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a>Création d’une file d’attente
Vous pouvez effectuer des opérations de gestion pour les files d’attente Service Bus via la classe **ServiceBusContract**. A **ServiceBusContract** objet est construit avec une configuration appropriée qui encapsule le jeton SAS avec les autorisations toomanage et hello **ServiceBusContract** classe est point unique de hello de la communication avec Azure.

Hello **ServiceBusService** classe fournit des méthodes toocreate, énumérer et supprimer des files d’attente. Hello exemple ci-dessous montre comment un **ServiceBusService** objet peut être utilisé toocreate une file d’attente nommée `TestQueue`, avec un espace de noms `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Il existe des méthodes sur `QueueInfo` qui autorisent des propriétés de toobe de file d’attente hello paramétrés (par exemple : tooset hello par défaut time-to-live (TTL) valeur toobe appliqué toomessages envoyé la file d’attente toohello). Hello suivant montre comment toocreate une file d’attente nommée `TestQueue` avec une taille maximale de 5 Go :

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

Notez que vous pouvez utiliser hello `listQueues` méthode sur **ServiceBusContract** objets toocheck si une file d’attente portant le nom spécifié existe déjà dans un espace de noms de service.

## <a name="send-messages-tooa-queue"></a>Envoyer la file d’attente de messages tooa
toosend une file d’attente Service Bus de messages tooa, votre application obtient un **ServiceBusContract** objet. Hello suivant de code montre comment toosend un message pour hello `TestQueue` file d’attente créée précédemment Bonjour `HowToSample` espace de noms :

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Les messages envoyés à et provenant du Service Bus files d’attente sont des instances de hello [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage] [ BrokeredMessage] objets comportent un ensemble de propriétés standard (tels que [étiquette](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) et [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un dictionnaire qui est utilisé toohold personnalisé les propriétés spécifiques à l’application et un corps de données d’application arbitraire. Une application peut définir le corps de hello du message de type hello en passant tout objet sérialisable dans le constructeur hello Hello [BrokeredMessage][BrokeredMessage], et le sérialiseur approprié de hello sera ensuite utilisée objet de hello tooserialize. Vous pouvez également fournir un objet **java.IO.InputStream**.

Hello exemple suivant montre comment les messages de test de toosend cinq toothe `TestQueue` **MessageSender** nous avons obtenu dans l’extrait de code précédent hello :

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

Les files d’attente Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md). en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko. Il n’existe aucune limite du nombre de hello de messages dans une file d’attente mais hello de taille totale des messages hello détenus par une file d’attente est une extrémité de fin. Cette taille de file d'attente est définie au moment de la création. La limite maximale est de 5 Go.

## <a name="receive-messages-from-a-queue"></a>Réception des messages d'une file d'attente
messages de tooreceive Hello moyen principal à partir d’une file d’attente est toouse un **ServiceBusContract** objet. Ces messages reçus peuvent fonctionner dans deux modes différents : **ReceiveAndDelete** et **PeekLock**.

Lors de l’utilisation de hello **ReceiveAndDelete** , le mode de réception est une opération coup - autrement dit, lorsque le Service Bus reçoit une demande de lecture d’un message dans une file d’attente, il marque le message de type hello comme ayant été consommé et le retourne toohello application. **ReceiveAndDelete** mode (mode par défaut de hello) est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec. toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter.
Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.

Dans **PeekLock** , le mode de réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application. Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant **supprimer** sur le message de salutation reçu. Lorsque le Service Bus voit hello **supprimer** appel, il marque le message de type hello comme ayant été consommé et supprimez-le de la file d’attente hello.

Hello exemple suivant montre comment les messages peuvent être reçus et traités à l’aide de **PeekLock** mode (pas le mode hello par défaut). Hello exemple ci-dessous effectue une boucle infinie et traite les messages lorsqu’ils arrivent dans notre `TestQueue`:

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
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
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
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
Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message. Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello **unlockMessage** méthode sur le message de salutation reçu (au lieu de hello **deleteMessage** méthode). Cela entraîne hello toounlock de Service Bus de messages dans la file d’attente hello et le rendre disponible toobe reçu, soit par Bonjour même consommation d’application ou par une autre application consommatrice.

Il existe également un délai d’attente d’un message verrouillé dans la file d’attente, et si application hello échoue tooprocess hello message avant l’expiration du délai d’attente de verrou (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille le message de type hello automatiquement et rend disponible toobe de nouveau reçu.

Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello **deleteMessage** demande est émise, puis le message de type hello est redistribué toohello application lors de son redémarrage. Cela est souvent appelé *au moins une fois le traitement*; autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué. Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message. Cela est souvent obtenue à l’aide de hello **getMessageId** méthode de message de type hello, qui reste constante entre les tentatives de remise.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de files d’attente Service Bus, consultez [les files d’attente, rubriques et abonnements] [ Queues, topics, and subscriptions] pour plus d’informations.

Pour plus d’informations, consultez hello [centre de développement Java](https://azure.microsoft.com/develop/java/).

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
