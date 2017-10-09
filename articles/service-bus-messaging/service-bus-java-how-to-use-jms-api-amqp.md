---
title: aaaHow toouse AMQP 1.0 avec hello API Java Service Bus | Documents Microsoft
description: Comment toouse hello Service JMS (Java Message) avec Azure Service Bus et Message Queuing Protodol AMQP (Advanced) 1.0.
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: be766f42-6fd1-410c-b275-8c400c811519
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3e1d0329f2675a2273e12bb7389d3ce38b156a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a>Comment toouse hello Service JMS (Java Message) API avec Service Bus et AMQP 1.0
Bonjour Advanced Message Queuing Protocol (AMQP) 1.0 est un protocole de messagerie efficace et fiable, au niveau du réseau que vous pouvez utiliser toobuild robuste inter-plateformes applications de messagerie.

Prise en charge d’AMQP 1.0 dans Service Bus signifie que vous pouvez utiliser hello queuing et publication/abonnement de fonctionnalités de messagerie répartie dans une plage de plateformes à l’aide d’un protocole binaire efficace. De plus, vous pouvez générer des applications constituées de composants créés à l'aide de divers langages, structures et systèmes d'exploitation.

Cet article explique comment toouse Service Bus des fonctionnalités de messagerie (files d’attente et publication/abonnement rubriques) à partir d’applications Java à l’aide de hello populaires Service JMS (Java Message) API standard. Il existe un [article complément](service-bus-amqp-dotnet.md) qui explique comment toodo hello même à l’aide de hello les API .NET Service Bus. Vous pouvez utiliser ces toolearn ensemble deux guides sur la messagerie multiplateforme à l’aide d’AMQP 1.0.

## <a name="get-started-with-service-bus"></a>Prise en main de Service Bus
Ce guide présuppose que vous disposez déjà d’un espace de noms Service Bus contenant une file d’attente nommée **queue1**. Si vous ne spécifiez aucune, vous pouvez [créer l’espace de noms hello et file d’attente](service-bus-create-namespace-portal.md) à l’aide de hello [portail Azure](https://portal.azure.com). Pour plus d’informations sur comment les espaces de noms Service Bus toocreate et files d’attente, consultez [prise en main les files d’attente Service Bus](service-bus-dotnet-get-started-with-queues.md).

> [!NOTE]
> Les files d’attente et rubriques partitionnées prennent également en charge AMQP. Pour plus d’informations, consultez [Files d’attente et rubriques partitionnées](service-bus-partitioning.md) et [Prise en charge d’AMQP 1.0 dans les rubriques et files d’attente partitionnées Service Bus](service-bus-partitioned-queues-and-topics-amqp-overview.md).
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a>Bibliothèque cliente de téléchargement hello AMQP 1.0 JMS
Pour savoir où toodownload hello version la plus récente de la bibliothèque cliente de hello Apache Qpid JMS AMQP 1.0, visitez [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).

Vous devez ajouter hello suivant quatre fichiers JAR hello Apache Qpid JMS AMQP 1.0 distribution archive toohello CLASSPATH Java lors de la création et l’exécution des applications JMS avec Service Bus :

* geronimo-jms\_1.1\_spec-1.0.jar
* qpid-amqp-1-0-client-[version].jar
* qpid-amqp-1-0-client-jms-[version].jar
* qpid-amqp-1-0-common-[version].jar

## <a name="coding-java-applications"></a>Codage d’applications Java
### <a name="java-naming-and-directory-interface-jndi"></a>JNDI (Java Naming and Directory Interface)
JMS utilise hello toocreate Java Naming and Directory Interface JNDI () une séparation entre les noms logiques et physique. Deux types d’objets JMS sont résolus à l’aide de JNDI : ConnectionFactory et Destination. JNDI utilise un modèle de fournisseur dans lequel vous pouvez incorporer des tâches de résolution de nom autre répertoire services toohandle. Hello Apache Qpid JMS AMQP 1.0 bibliothèque est fourni avec les propriétés d’un simple fournisseur JNDI basé sur un fichier qui est configuré à l’aide d’un fichier de propriétés suivantes de hello format :

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using hello form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using hello form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-hello-connectionfactory"></a>Configurer hello ConnectionFactory
Hello entrée utilisée toodefine un **ConnectionFactory** Bonjour Qpid fournisseur JNDI de fichiers propriétés est Hello suivant le format :

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

Où **[jndi_name]** et **[ConnectionURL]** ont hello suivant significations :

* **[jndi_name]** : nom logique de hello Hello ConnectionFactory. Il s’agit de nom hello qui sera résolu dans une application Java de hello à l’aide de la méthode de JNDI Intialcontext.Lookup hello.
* **[ConnectionURL]** : Une URL qui fournit la bibliothèque de hello JMS avec les informations de hello requis service broker de toohello AMQP.

format Hello Hello **ConnectionURL** est comme suit :

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
Où **[namespace]**, **[SASPolicyName]** et **[SASPolicyKey]** ont hello suivant significations :

* **[espace de noms]** : hello d’espace de noms Service Bus.
* **[SASPolicyName]** : nom de stratégie de file d’attente SAS hello.
* **[SASPolicyKey]** : clé de stratégie de file d’attente SAS hello.

> [!NOTE]
> Vous devez coder par URL le mot de passe hello manuellement. Un utilitaire efficace d’encodage dans une URL est disponible à l’adresse [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).
> 
> 

#### <a name="configure-destinations"></a>Configurer des destinations
Hello toodefine entrée utilisée qu'une destination dans le fournisseur JNDI de fichiers de propriétés hello Qpid est Hello suivant le format :

```
queue.[jndi_name] = [physical_name]
```

ou

```
topic.[jndi_name] = [physical_name]
```

Où **[jndi\_nom]** et **[physique\_nom]** ont hello suivant significations :

* **[jndi_name]** : nom logique de hello de destination de hello. Il s’agit de nom hello qui sera résolu dans une application Java de hello à l’aide de la méthode de JNDI Intialcontext.Lookup hello.
* **[physical_name]** : nom hello Hello application de Service Bus entité toowhich hello envoie ou reçoit des messages.

> [!NOTE]
> Lors de la réception à partir d’un abonnement à une rubrique Service Bus, le nom physique de hello spécifié dans JNDI doit être nom hello de rubrique de hello. nom de l’abonnement Hello est fourni lors de l’abonnement durable de hello est créé dans le code d’application JMS de hello. Hello [Guide du développeur Service Bus AMQP 1.0](service-bus-amqp-dotnet.md) fournit plus de détails sur l’utilisation des rubriques Service Bus à partir de JMS.
> 
> 

### <a name="write-hello-jms-application"></a>Écrire l’application de JMS hello
Il n’existe aucune API ou option particulière nécessaire à l’utilisation de JMS avec Service Bus. Toutefois, il existe quelques restrictions qui seront abordées ultérieurement. Comme avec n’importe quelle application JMS, hello première requise est configuration d’environnement de JNDI hello, tooresolve en mesure de toobe un **ConnectionFactory** et les destinations.

#### <a name="configure-hello-jndi-initialcontext"></a>Configurer hello JNDI InitialContext
environnement de JNDI Hello est configuré en passant d’une table de hachage des informations de configuration dans le constructeur hello de classe de javax.naming.InitialContext hello. deux éléments requis Hello dans la table de hachage hello sont nom de la classe de fabrique de contexte Initial de hello hello et hello URL du fournisseur. Hello de code suivant montre comment le fichier de propriétés Qpid environnement toouse hello tooconfigure hello JNDI basé fournisseur JNDI avec un fichier de propriétés nommé **servicebus.properties**.

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a>Une simple application JMS utilisant une file d’attente Service Bus
Bonjour exemple de programme suivant envoie la file d’attente du Service Bus JMS TextMessages tooa avec le nom logique de JNDI hello de file d’attente et reçoit des messages hello précédent.

```java
// SimpleSenderReceiver.java

import javax.jms.*;
import javax.naming.Context;
import javax.naming.InitialContext;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Hashtable;
import java.util.Random;

public class SimpleSenderReceiver implements MessageListener {
    private static boolean runReceiver = true;
    private Connection connection;
    private Session sendSession;
    private Session receiveSession;
    private MessageProducer sender;
    private MessageConsumer receiver;
    private static Random randomGenerator = new Random();

    public SimpleSenderReceiver() throws Exception {
        // Configure JNDI environment
        Hashtable<String, String> env = new Hashtable<String, String>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, 
                   "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory");
        env.put(Context.PROVIDER_URL, "servicebus.properties");
        Context context = new InitialContext(env);

        // Look up ConnectionFactory and Queue
        ConnectionFactory cf = (ConnectionFactory) context.lookup("SBCF");
        Destination queue = (Destination) context.lookup("QUEUE");

        // Create Connection
        connection = cf.createConnection();

        // Create sender-side Session and MessageProducer
        sendSession = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        sender = sendSession.createProducer(queue);

        if (runReceiver) {
            // Create receiver-side Session, MessageConsumer,and MessageListener
            receiveSession = connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
            receiver = receiveSession.createConsumer(queue);
            receiver.setMessageListener(this);
            connection.start();
        }
    }

    public static void main(String[] args) {
        try {

            if ((args.length > 0) && args[0].equalsIgnoreCase("sendonly")) {
                runReceiver = false;
            }

            SimpleSenderReceiver simpleSenderReceiver = new SimpleSenderReceiver();
            System.out.println("Press [enter] toosend a message. Type 'exit' + [enter] tooquit.");
            BufferedReader commandLine = new java.io.BufferedReader(new InputStreamReader(System.in));

            while (true) {
                String s = commandLine.readLine();
                if (s.equalsIgnoreCase("exit")) {
                    simpleSenderReceiver.close();
                    System.exit(0);
                } else {
                    simpleSenderReceiver.sendMessage();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void sendMessage() throws JMSException {
        TextMessage message = sendSession.createTextMessage();
        message.setText("Test AMQP message from JMS");
        long randomMessageID = randomGenerator.nextLong() >>>1;
        message.setJMSMessageID("ID:" + randomMessageID);
        sender.send(message);
        System.out.println("Sent message with JMSMessageID = " + message.getJMSMessageID());
    }

    public void close() throws JMSException {
        connection.close();
    }

    public void onMessage(Message message) {
        try {
            System.out.println("Received message with JMSMessageID = " + message.getJMSMessageID());
            message.acknowledge();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}    
```

### <a name="run-hello-application"></a>Exécutez l’application hello
Exécute l’application hello génère la sortie sous forme de hello :

```
> java SimpleSenderReceiver
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a>Messagerie interplateforme entre JMS et .NET
Ce guide a montré comment toosend et de recevoir des messages tooand de Bus de Service à l’aide de JMS. Toutefois, un des avantages clés de hello AMQP 1.0 est qu’il permet des toobe applications générée à partir de composants écrits dans différentes langues, avec des messages échangés et de manière fiable avec une fidélité optimale.

À l’aide de hello exemple d’application JMS décrites ci-dessus et d’une application .NET similaire obtenue à partir d’un article d’accompagnement, [à l’aide de Service Bus à partir de .NET avec AMQP 1.0](service-bus-amqp-dotnet.md), vous pouvez échanger des messages entre .NET et Java. Lisez cet article pour plus d’informations sur les détails de hello de messagerie à l’aide du Service Bus et AMQP 1.0 inter-plateformes.

### <a name="jms-toonet"></a>JMS too.NET
toodemonstrate JMS too.NET de messagerie :

* Démarrer l’application d’exemple hello .NET sans arguments de ligne de commande.
* Démarrez l’exemple d’application Java hello avec l’argument de ligne de commande « sendonly » hello. Dans ce mode, hello application ne reçoit pas de messages à partir de la file d’attente de hello, elle n’envoie.
* Appuyez sur **entrée** plusieurs fois dans la console de l’application Java hello, ce qui entraîne une toobe de messages envoyé.
* Ces messages sont reçus par hello application .NET.

#### <a name="output-from-jms-application"></a>Résultat de l'application JMS
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a>Résultat de l'application .NET
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a>.NET tooJMS
toodemonstrate tooJMS de .NET de messagerie :

* Démarrez l’exemple d’application .NET hello avec l’argument de ligne de commande « sendonly » hello. Dans ce mode, hello application ne reçoit pas de messages à partir de la file d’attente de hello, elle n’envoie.
* Démarrer l’application d’exemple hello Java sans arguments de ligne de commande.
* Appuyez sur **entrée** plusieurs fois dans la console de l’application hello .NET, ce qui entraîne une toobe de messages envoyé.
* Ces messages sont reçus par hello application Java.

#### <a name="output-from-net-application"></a>Résultat de l'application .NET
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a>Résultat de l'application JMS
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a>Fonctionnalités non prises en charge et restrictions
Hello suivant des restrictions existe lors de l’utilisation de JMS via AMQP 1.0 avec Service Bus, à savoir :

* Un seul **MessageProducer** ou **MessageConsumer** est autorisé par **Session**. Si vous avez besoin de toocreate plusieurs **MessageProducers** ou **MessageConsumers** dans une application, créez une dédiée **Session** pour chacun d’eux.
* Les abonnements aux rubriques volatiles ne sont actuellement pas pris en charge.
* Les **MessageSelectors** ne sont actuellement pas pris en charge.
* Destinations temporaires ; par exemple, **TemporaryQueue**, **TemporaryTopic** ne sont pas actuellement pris en charge, ainsi que de hello **QueueRequestor** et **TopicRequestor**API qui les utilisent.
* Les sessions traitées et les transactions distribuées ne sont pas prises en charge.

## <a name="summary"></a>Résumé
Cette procédure-tooguide a montré comment toouse répartie de Service Bus des fonctionnalités de messagerie (files d’attente et publication/abonnement rubriques) à partir de Java à l’aide de hello populaires API JMS et AMQP 1.0.

Vous pouvez également utiliser l'AMQP 1.0 de Service Bus depuis d'autres langages, notamment .NET, C, Python et PHP. Composants créés à l’aide de ces langages différents peuvent échanger des messages et de manière fiable avec une fidélité optimale à l’aide de la prise en charge hello AMQP 1.0 dans Service Bus.

## <a name="next-steps"></a>Étapes suivantes
* [Prise en charge d’AMQP 1.0 dans Service Bus](service-bus-amqp-overview.md)
* [Comment toouse AMQP 1.0 avec hello les API .NET Service Bus](service-bus-dotnet-advanced-message-queuing.md)
* [Guide du développeur sur l’utilisation de Service Bus avec AMQP 1.0](service-bus-amqp-dotnet.md)
* [Prise en main des files d’attente Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Centre de développement Java](https://azure.microsoft.com/develop/java/)

