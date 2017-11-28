---
title: "Utilisation d’AMQP 1.0 avec l’API Java Service Bus | Microsoft Docs"
description: "Découvrez comment utiliser Java Message Service (JMS) avec Azure Service Bus et le protocole Advanced Message Queuing Protocol (AMQP) 1.0."
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
ms.openlocfilehash: 0848facd764c4fb0d7f95c1ae89ecb02a32257e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="00b79-103">Utilisation de l’API Java Message Service (JMS) avec Service Bus et AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="00b79-103">How to use the Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="00b79-104">Advanced Message Queuing Protocol (AMQP) 1.0 est un protocole de messagerie « wire-level » efficace et fiable qui peut être utilisé pour créer des applications de messagerie interplateforme robustes.</span><span class="sxs-lookup"><span data-stu-id="00b79-104">The Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="00b79-105">La prise en charge d'AMQP 1.0 dans Service Bus signifie que vous pouvez utiliser des fonctionnalités de messagerie répartie de mise en file d’attente et de publication/d'abonnement à partir de diverses plateformes, à l'aide d'un protocole binaire efficace.</span><span class="sxs-lookup"><span data-stu-id="00b79-105">Support for AMQP 1.0 in Service Bus means that you can use the queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="00b79-106">De plus, vous pouvez générer des applications constituées de composants créés à l'aide de divers langages, structures et systèmes d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="00b79-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="00b79-107">Cet article explique comment utiliser les fonctionnalités de messagerie de Service Bus (files d’attente et rubriques de publication/d’abonnement) à partir d’applications Java en utilisant la populaire API standard Java Message Service (JMS).</span><span class="sxs-lookup"><span data-stu-id="00b79-107">This article explains how to use Service Bus messaging features (queues and publish/subscribe topics) from Java applications using the popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="00b79-108">Un [article complémentaire](service-bus-amqp-dotnet.md) explique comment réaliser les mêmes opérations à l’aide de l’API .NET Service Bus.</span><span class="sxs-lookup"><span data-stu-id="00b79-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how to do the same using the Service Bus .NET API.</span></span> <span data-ttu-id="00b79-109">Vous pouvez utiliser ces deux guides ensemble pour découvrir la messagerie interplateforme en utilisant AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="00b79-109">You can use these two guides together to learn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="00b79-110">Prise en main de Service Bus</span><span class="sxs-lookup"><span data-stu-id="00b79-110">Get started with Service Bus</span></span>
<span data-ttu-id="00b79-111">Ce guide présuppose que vous disposez déjà d’un espace de noms Service Bus contenant une file d’attente nommée **queue1**.</span><span class="sxs-lookup"><span data-stu-id="00b79-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="00b79-112">Dans le cas contraire, vous pouvez [créer l’espace de noms et la file d’attente](service-bus-create-namespace-portal.md) à l’aide du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="00b79-112">If you do not, then you can [create the namespace and queue](service-bus-create-namespace-portal.md) using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="00b79-113">Pour plus d’informations sur la création d’espaces de noms et de files d’attente Service Bus, consultez [Prise en main des files d’attente Service Bus](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="00b79-113">For more information about how to create Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="00b79-114">Les files d’attente et rubriques partitionnées prennent également en charge AMQP.</span><span class="sxs-lookup"><span data-stu-id="00b79-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="00b79-115">Pour plus d’informations, consultez [Files d’attente et rubriques partitionnées](service-bus-partitioning.md) et [Prise en charge d’AMQP 1.0 dans les rubriques et files d’attente partitionnées Service Bus](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="00b79-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-the-amqp-10-jms-client-library"></a><span data-ttu-id="00b79-116">Téléchargement des bibliothèques clientes JMS d’AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="00b79-116">Downloading the AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="00b79-117">Pour plus d’informations sur l’adresse de téléchargement de la dernière version de la bibliothèque cliente Apache Qpid JMS AMQP 1.0, accédez à [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="00b79-117">For information about where to download the latest version of the Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="00b79-118">Vous devez ajouter les quatre fichiers JAR suivants de l’archive de distribution Apache Qpid JMS AMQP 1.0 au CLASSPATH Java lors de la création et de l’exécution des applications JMS avec Service Bus :</span><span class="sxs-lookup"><span data-stu-id="00b79-118">You must add the following four JAR files from the Apache Qpid JMS AMQP 1.0 distribution archive to the Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="00b79-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="00b79-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="00b79-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="00b79-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="00b79-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="00b79-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="00b79-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="00b79-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="00b79-123">Codage d’applications Java</span><span class="sxs-lookup"><span data-stu-id="00b79-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="00b79-124">JNDI (Java Naming and Directory Interface)</span><span class="sxs-lookup"><span data-stu-id="00b79-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="00b79-125">JMS utilise l’interface JNDI (Java Naming and Directory Interface) pour créer une séparation entre les noms logiques et les noms physiques.</span><span class="sxs-lookup"><span data-stu-id="00b79-125">JMS uses the Java Naming and Directory Interface (JNDI) to create a separation between logical names and physical names.</span></span> <span data-ttu-id="00b79-126">Deux types d’objets JMS sont résolus à l’aide de JNDI : ConnectionFactory et Destination.</span><span class="sxs-lookup"><span data-stu-id="00b79-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="00b79-127">JNDI utilise un modèle de fournisseur auquel vous pouvez connecter différents services d’annuaire afin de gérer les tâches de résolution de noms.</span><span class="sxs-lookup"><span data-stu-id="00b79-127">JNDI uses a provider model into which you can plug different directory services to handle name resolution duties.</span></span> <span data-ttu-id="00b79-128">La bibliothèque Apache Qpid JMS AMQP 1.0 est dotée d’un simple fournisseur JNDI fondé sur un fichier de propriétés qui est configuré à l’aide d’un fichier de propriétés au format suivant :</span><span class="sxs-lookup"><span data-stu-id="00b79-128">The Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of the following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using the form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using the form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-the-connectionfactory"></a><span data-ttu-id="00b79-129">Configurer ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="00b79-129">Configure the ConnectionFactory</span></span>
<span data-ttu-id="00b79-130">L’entrée utilisée pour définir une **ConnectionFactory** dans le fournisseur JNDI de fichier de propriétés Qpid est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="00b79-130">The entry used to define a **ConnectionFactory** in the Qpid properties file JNDI provider is of the following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="00b79-131">Où **[jndi_name]** et **[ConnectionURL]** ont les significations suivantes :</span><span class="sxs-lookup"><span data-stu-id="00b79-131">Where **[jndi_name]** and **[ConnectionURL]** have the following meanings:</span></span>

* <span data-ttu-id="00b79-132">**[jndi_name]** : nom logique de la ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="00b79-132">**[jndi_name]**: The logical name of the ConnectionFactory.</span></span> <span data-ttu-id="00b79-133">Ce nom est résolu dans l’application Java à l’aide de la méthode JNDI IntialContext.lookup().</span><span class="sxs-lookup"><span data-stu-id="00b79-133">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="00b79-134">**[ConnectionURL]** : URL fournissant à la bibliothèque JMS les informations nécessaires au répartiteur AMQP.</span><span class="sxs-lookup"><span data-stu-id="00b79-134">**[ConnectionURL]**: A URL that provides the JMS library with the information required to the AMQP broker.</span></span>

<span data-ttu-id="00b79-135">Le format de **ConnectionURL** est le suivant :</span><span class="sxs-lookup"><span data-stu-id="00b79-135">The format of the **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="00b79-136">Où **[namespace]**, **[SASPolicyName]** et **[SASPolicyKey]** ont les significations suivantes :</span><span class="sxs-lookup"><span data-stu-id="00b79-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have the following meanings:</span></span>

* <span data-ttu-id="00b79-137">**[namespace]** : espace de noms Service Bus.</span><span class="sxs-lookup"><span data-stu-id="00b79-137">**[namespace]**: The Service Bus namespace.</span></span>
* <span data-ttu-id="00b79-138">**[SASPolicyName]** : nom de la stratégie de signature d’accès partagé de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="00b79-138">**[SASPolicyName]**: The Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="00b79-139">**[SASPolicyKey]** : clé de la stratégie de signature d’accès partagé de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="00b79-139">**[SASPolicyKey]**: The Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="00b79-140">vous devez encoder manuellement le mot de passe dans une URL.</span><span class="sxs-lookup"><span data-stu-id="00b79-140">You must URL-encode the password manually.</span></span> <span data-ttu-id="00b79-141">Un utilitaire efficace d’encodage dans une URL est disponible à l’adresse [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="00b79-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="00b79-142">Configurer des destinations</span><span class="sxs-lookup"><span data-stu-id="00b79-142">Configure destinations</span></span>
<span data-ttu-id="00b79-143">L’entrée qui définit une destination dans le fournisseur JNDI de fichier de propriétés Qpid est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="00b79-143">The entry used to define a destination in the Qpid properties file JNDI provider is of the following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="00b79-144">ou</span><span class="sxs-lookup"><span data-stu-id="00b79-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="00b79-145">Où **[jndi\_name]** et **[physical\_name]** ont les significations suivantes :</span><span class="sxs-lookup"><span data-stu-id="00b79-145">Where **[jndi\_name]** and **[physical\_name]** have the following meanings:</span></span>

* <span data-ttu-id="00b79-146">**[jndi_name]** : nom logique de la destination.</span><span class="sxs-lookup"><span data-stu-id="00b79-146">**[jndi_name]**: The logical name of the destination.</span></span> <span data-ttu-id="00b79-147">Ce nom est résolu dans l’application Java à l’aide de la méthode JNDI IntialContext.lookup().</span><span class="sxs-lookup"><span data-stu-id="00b79-147">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="00b79-148">**[physical_name]** : nom de l’entité Service Bus avec laquelle l’application échange des messages.</span><span class="sxs-lookup"><span data-stu-id="00b79-148">**[physical_name]**: The name of the Service Bus entity to which the application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="00b79-149">lors de la réception d’un abonnement à une rubrique Service Bus, le nom physique spécifié dans JNDI doit être le nom de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="00b79-149">When receiving from a Service Bus topic subscription, the physical name specified in JNDI should be the name of the topic.</span></span> <span data-ttu-id="00b79-150">Le nom de l’abonnement est fourni lors de la création de l’abonnement durable dans le code d’application JMS.</span><span class="sxs-lookup"><span data-stu-id="00b79-150">The subscription name is provided when the durable subscription is created in the JMS application code.</span></span> <span data-ttu-id="00b79-151">Le [guide du développeur sur l’utilisation de Service Bus avec AMQP 1.0](service-bus-amqp-dotnet.md) fournit des informations détaillées sur l’utilisation des rubriques Service Bus à partir de JMS.</span><span class="sxs-lookup"><span data-stu-id="00b79-151">The [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-the-jms-application"></a><span data-ttu-id="00b79-152">Écrire l’application JMS</span><span class="sxs-lookup"><span data-stu-id="00b79-152">Write the JMS application</span></span>
<span data-ttu-id="00b79-153">Il n’existe aucune API ou option particulière nécessaire à l’utilisation de JMS avec Service Bus.</span><span class="sxs-lookup"><span data-stu-id="00b79-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="00b79-154">Toutefois, il existe quelques restrictions qui seront abordées ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="00b79-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="00b79-155">Comme dans toute application JMS, il convient de configurer l’environnement JNDI avant de pouvoir résoudre une **ConnectionFactory** et les destinations.</span><span class="sxs-lookup"><span data-stu-id="00b79-155">As with any JMS application, the first thing required is configuration of the JNDI environment, to be able to resolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-the-jndi-initialcontext"></a><span data-ttu-id="00b79-156">Configurer JNDI InitialContext</span><span class="sxs-lookup"><span data-stu-id="00b79-156">Configure the JNDI InitialContext</span></span>
<span data-ttu-id="00b79-157">L’environnement JNDI est configuré en transmettant une table de hachage d’informations de configuration dans le constructeur de la classe javax.naming.InitialContext.</span><span class="sxs-lookup"><span data-stu-id="00b79-157">The JNDI environment is configured by passing a hashtable of configuration information into the constructor of the javax.naming.InitialContext class.</span></span> <span data-ttu-id="00b79-158">Les deux éléments requis dans la table de hachage sont le nom de classe de la fabrique de contexte initial et l’URL du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="00b79-158">The two required elements in the hashtable are the class name of the Initial Context Factory and the Provider URL.</span></span> <span data-ttu-id="00b79-159">Le code suivant montre comment configurer l’environnement JNDI afin d’utiliser le fournisseur JNDI fondé sur le fichier de propriétés Qpid avec un fichier de propriétés nommé **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="00b79-159">The following code shows how to configure the JNDI environment to use the Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="00b79-160">Une simple application JMS utilisant une file d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="00b79-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="00b79-161">L’exemple de programme suivant envoie JMS TextMessages vers une file d’attente Service Bus avec le nom logique JNDI « QUEUE » et reçoit les messages en retour.</span><span class="sxs-lookup"><span data-stu-id="00b79-161">The following example program sends JMS TextMessages to a Service Bus queue with the JNDI logical name of QUEUE, and receives the messages back.</span></span>

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
            System.out.println("Press [enter] to send a message. Type 'exit' + [enter] to quit.");
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

### <a name="run-the-application"></a><span data-ttu-id="00b79-162">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="00b79-162">Run the application</span></span>
<span data-ttu-id="00b79-163">L'exécution de l'application produit un résultat ressemblant à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="00b79-163">Running the application produces output of the form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] to send a message. Type 'exit' + [enter] to quit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="00b79-164">Messagerie interplateforme entre JMS et .NET</span><span class="sxs-lookup"><span data-stu-id="00b79-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="00b79-165">Ce guide a expliqué comment envoyer et recevoir des messages depuis et vers Service Bus à l’aide de JMS.</span><span class="sxs-lookup"><span data-stu-id="00b79-165">This guide showed how to send and receive messages to and from Service Bus using JMS.</span></span> <span data-ttu-id="00b79-166">Néanmoins, l'un des avantages clés d'AMQP 1.0 est qu'il permet aux applications d'être créées à partir de composants écrits en différents langages, avec un échange de messages fiable d'une fidélité optimale.</span><span class="sxs-lookup"><span data-stu-id="00b79-166">However, one of the key benefits of AMQP 1.0 is that it enables applications to be built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="00b79-167">À l’aide de l’exemple d’application JMS décrit ci-dessus et d’une application .NET similaire extraite d’un article complémentaire, [Utilisation de Service Bus à partir de .NET avec AMQP 1.0](service-bus-amqp-dotnet.md), il est possible d’échanger des messages entre .NET et Java.</span><span class="sxs-lookup"><span data-stu-id="00b79-167">Using the sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="00b79-168">Lisez cet article pour plus d’informations sur les détails de la messagerie interplateforme utilisant Service Bus et AMQP 1.0 .</span><span class="sxs-lookup"><span data-stu-id="00b79-168">Read this article for more information about the details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-to-net"></a><span data-ttu-id="00b79-169">De JMS à .NET</span><span class="sxs-lookup"><span data-stu-id="00b79-169">JMS to .NET</span></span>
<span data-ttu-id="00b79-170">Démonstration de la messagerie entre JMS et .NET :</span><span class="sxs-lookup"><span data-stu-id="00b79-170">To demonstrate JMS to .NET messaging:</span></span>

* <span data-ttu-id="00b79-171">Démarrez l'exemple d'application .NET sans argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="00b79-171">Start the .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="00b79-172">Démarrez l'exemple d'application Java avec l'argument de ligne de commande « sendonly ».</span><span class="sxs-lookup"><span data-stu-id="00b79-172">Start the Java sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="00b79-173">Dans ce mode, l’application ne reçoit pas de messages provenant de la file d’attente, elle ne fait qu’en envoyer.</span><span class="sxs-lookup"><span data-stu-id="00b79-173">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="00b79-174">Appuyez plusieurs fois sur **Entrée** dans la console d’application Java, ce qui provoquera l’envoi des messages.</span><span class="sxs-lookup"><span data-stu-id="00b79-174">Press **Enter** a few times in the Java application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="00b79-175">Ces messages sont reçus par l'application .NET.</span><span class="sxs-lookup"><span data-stu-id="00b79-175">These messages are received by the .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="00b79-176">Résultat de l'application JMS</span><span class="sxs-lookup"><span data-stu-id="00b79-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="00b79-177">Résultat de l'application .NET</span><span class="sxs-lookup"><span data-stu-id="00b79-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-to-jms"></a><span data-ttu-id="00b79-178">De .NET à JMS</span><span class="sxs-lookup"><span data-stu-id="00b79-178">.NET to JMS</span></span>
<span data-ttu-id="00b79-179">Démonstration de la messagerie entre .NET et JMS :</span><span class="sxs-lookup"><span data-stu-id="00b79-179">To demonstrate .NET to JMS messaging:</span></span>

* <span data-ttu-id="00b79-180">Démarrez l’exemple d’application .NET avec l’argument de ligne de commande « sendonly ».</span><span class="sxs-lookup"><span data-stu-id="00b79-180">Start the .NET sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="00b79-181">Dans ce mode, l’application ne reçoit pas de messages provenant de la file d’attente, elle ne fait qu’en envoyer.</span><span class="sxs-lookup"><span data-stu-id="00b79-181">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="00b79-182">Démarrez l’exemple d’application Java sans argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="00b79-182">Start the Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="00b79-183">Appuyez plusieurs fois sur **Entrée** dans la console d’application .NET, ce qui provoquera l’envoi des messages.</span><span class="sxs-lookup"><span data-stu-id="00b79-183">Press **Enter** a few times in the .NET application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="00b79-184">Ces messages sont reçus par l'application Java.</span><span class="sxs-lookup"><span data-stu-id="00b79-184">These messages are received by the Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="00b79-185">Résultat de l'application .NET</span><span class="sxs-lookup"><span data-stu-id="00b79-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="00b79-186">Résultat de l'application JMS</span><span class="sxs-lookup"><span data-stu-id="00b79-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="00b79-187">Fonctionnalités non prises en charge et restrictions</span><span class="sxs-lookup"><span data-stu-id="00b79-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="00b79-188">Les restrictions suivantes existent pour l’utilisation de JMS sur AMQP 1.0 avec Service Bus, à savoir :</span><span class="sxs-lookup"><span data-stu-id="00b79-188">The following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="00b79-189">Un seul **MessageProducer** ou **MessageConsumer** est autorisé par **Session**.</span><span class="sxs-lookup"><span data-stu-id="00b79-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="00b79-190">Si vous devez créer plusieurs **MessageProducers** ou **MessageConsumers** dans une application, créez une **Session** dédiée pour chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="00b79-190">If you need to create multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="00b79-191">Les abonnements aux rubriques volatiles ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="00b79-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="00b79-192">Les **MessageSelectors** ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="00b79-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="00b79-193">Les destinations temporaires, par exemple **TemporaryQueue**, **TemporaryTopic**, ne sont actuellement pas prises en charge, à l’instar des API **QueueRequestor** et **TopicRequestor** qui les utilisent.</span><span class="sxs-lookup"><span data-stu-id="00b79-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with the **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="00b79-194">Les sessions traitées et les transactions distribuées ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="00b79-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="00b79-195">Résumé</span><span class="sxs-lookup"><span data-stu-id="00b79-195">Summary</span></span>
<span data-ttu-id="00b79-196">Ce manuel d’utilisation vous a montré comment mettre en œuvre les fonctionnalités de messagerie répartie Service Bus (rubriques files d’attente et publication/abonnement) depuis Java en utilisant l’API JMS (Java Message Service) connue et AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="00b79-196">This how-to guide showed how to use Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using the popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="00b79-197">Vous pouvez également utiliser l'AMQP 1.0 de Service Bus depuis d'autres langages, notamment .NET, C, Python et PHP.</span><span class="sxs-lookup"><span data-stu-id="00b79-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="00b79-198">Les composants intégrés avec ces différents langages peuvent échanger des messages de manière fiable et fidèle en utilisant le support AMQP 1.0 dans Service Bus. </span><span class="sxs-lookup"><span data-stu-id="00b79-198">Components built using these different languages can exchange messages reliably and at full fidelity using the AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00b79-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00b79-199">Next steps</span></span>
* [<span data-ttu-id="00b79-200">Prise en charge d’AMQP 1.0 dans Service Bus</span><span class="sxs-lookup"><span data-stu-id="00b79-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="00b79-201">Utilisation d’AMQP 1.0 avec l’API .NET Service Bus</span><span class="sxs-lookup"><span data-stu-id="00b79-201">How to use AMQP 1.0 with the Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="00b79-202">Guide du développeur sur l’utilisation de Service Bus avec AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="00b79-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="00b79-203">Prise en main des files d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="00b79-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="00b79-204">Centre de développement Java</span><span class="sxs-lookup"><span data-stu-id="00b79-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

