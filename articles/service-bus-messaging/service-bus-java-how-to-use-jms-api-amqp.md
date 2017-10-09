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
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="462c4-103">Comment toouse hello Service JMS (Java Message) API avec Service Bus et AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="462c4-103">How toouse hello Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="462c4-104">Bonjour Advanced Message Queuing Protocol (AMQP) 1.0 est un protocole de messagerie efficace et fiable, au niveau du réseau que vous pouvez utiliser toobuild robuste inter-plateformes applications de messagerie.</span><span class="sxs-lookup"><span data-stu-id="462c4-104">hello Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use toobuild robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="462c4-105">Prise en charge d’AMQP 1.0 dans Service Bus signifie que vous pouvez utiliser hello queuing et publication/abonnement de fonctionnalités de messagerie répartie dans une plage de plateformes à l’aide d’un protocole binaire efficace.</span><span class="sxs-lookup"><span data-stu-id="462c4-105">Support for AMQP 1.0 in Service Bus means that you can use hello queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="462c4-106">De plus, vous pouvez générer des applications constituées de composants créés à l'aide de divers langages, structures et systèmes d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="462c4-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="462c4-107">Cet article explique comment toouse Service Bus des fonctionnalités de messagerie (files d’attente et publication/abonnement rubriques) à partir d’applications Java à l’aide de hello populaires Service JMS (Java Message) API standard.</span><span class="sxs-lookup"><span data-stu-id="462c4-107">This article explains how toouse Service Bus messaging features (queues and publish/subscribe topics) from Java applications using hello popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="462c4-108">Il existe un [article complément](service-bus-amqp-dotnet.md) qui explique comment toodo hello même à l’aide de hello les API .NET Service Bus.</span><span class="sxs-lookup"><span data-stu-id="462c4-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how toodo hello same using hello Service Bus .NET API.</span></span> <span data-ttu-id="462c4-109">Vous pouvez utiliser ces toolearn ensemble deux guides sur la messagerie multiplateforme à l’aide d’AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="462c4-109">You can use these two guides together toolearn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="462c4-110">Prise en main de Service Bus</span><span class="sxs-lookup"><span data-stu-id="462c4-110">Get started with Service Bus</span></span>
<span data-ttu-id="462c4-111">Ce guide présuppose que vous disposez déjà d’un espace de noms Service Bus contenant une file d’attente nommée **queue1**.</span><span class="sxs-lookup"><span data-stu-id="462c4-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="462c4-112">Si vous ne spécifiez aucune, vous pouvez [créer l’espace de noms hello et file d’attente](service-bus-create-namespace-portal.md) à l’aide de hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="462c4-112">If you do not, then you can [create hello namespace and queue](service-bus-create-namespace-portal.md) using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="462c4-113">Pour plus d’informations sur comment les espaces de noms Service Bus toocreate et files d’attente, consultez [prise en main les files d’attente Service Bus](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="462c4-113">For more information about how toocreate Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="462c4-114">Les files d’attente et rubriques partitionnées prennent également en charge AMQP.</span><span class="sxs-lookup"><span data-stu-id="462c4-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="462c4-115">Pour plus d’informations, consultez [Files d’attente et rubriques partitionnées](service-bus-partitioning.md) et [Prise en charge d’AMQP 1.0 dans les rubriques et files d’attente partitionnées Service Bus](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="462c4-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a><span data-ttu-id="462c4-116">Bibliothèque cliente de téléchargement hello AMQP 1.0 JMS</span><span class="sxs-lookup"><span data-stu-id="462c4-116">Downloading hello AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="462c4-117">Pour savoir où toodownload hello version la plus récente de la bibliothèque cliente de hello Apache Qpid JMS AMQP 1.0, visitez [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="462c4-117">For information about where toodownload hello latest version of hello Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="462c4-118">Vous devez ajouter hello suivant quatre fichiers JAR hello Apache Qpid JMS AMQP 1.0 distribution archive toohello CLASSPATH Java lors de la création et l’exécution des applications JMS avec Service Bus :</span><span class="sxs-lookup"><span data-stu-id="462c4-118">You must add hello following four JAR files from hello Apache Qpid JMS AMQP 1.0 distribution archive toohello Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="462c4-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="462c4-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="462c4-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="462c4-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="462c4-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="462c4-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="462c4-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="462c4-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="462c4-123">Codage d’applications Java</span><span class="sxs-lookup"><span data-stu-id="462c4-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="462c4-124">JNDI (Java Naming and Directory Interface)</span><span class="sxs-lookup"><span data-stu-id="462c4-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="462c4-125">JMS utilise hello toocreate Java Naming and Directory Interface JNDI () une séparation entre les noms logiques et physique.</span><span class="sxs-lookup"><span data-stu-id="462c4-125">JMS uses hello Java Naming and Directory Interface (JNDI) toocreate a separation between logical names and physical names.</span></span> <span data-ttu-id="462c4-126">Deux types d’objets JMS sont résolus à l’aide de JNDI : ConnectionFactory et Destination.</span><span class="sxs-lookup"><span data-stu-id="462c4-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="462c4-127">JNDI utilise un modèle de fournisseur dans lequel vous pouvez incorporer des tâches de résolution de nom autre répertoire services toohandle.</span><span class="sxs-lookup"><span data-stu-id="462c4-127">JNDI uses a provider model into which you can plug different directory services toohandle name resolution duties.</span></span> <span data-ttu-id="462c4-128">Hello Apache Qpid JMS AMQP 1.0 bibliothèque est fourni avec les propriétés d’un simple fournisseur JNDI basé sur un fichier qui est configuré à l’aide d’un fichier de propriétés suivantes de hello format :</span><span class="sxs-lookup"><span data-stu-id="462c4-128">hello Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of hello following format:</span></span>

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

#### <a name="configure-hello-connectionfactory"></a><span data-ttu-id="462c4-129">Configurer hello ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="462c4-129">Configure hello ConnectionFactory</span></span>
<span data-ttu-id="462c4-130">Hello entrée utilisée toodefine un **ConnectionFactory** Bonjour Qpid fournisseur JNDI de fichiers propriétés est Hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="462c4-130">hello entry used toodefine a **ConnectionFactory** in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="462c4-131">Où **[jndi_name]** et **[ConnectionURL]** ont hello suivant significations :</span><span class="sxs-lookup"><span data-stu-id="462c4-131">Where **[jndi_name]** and **[ConnectionURL]** have hello following meanings:</span></span>

* <span data-ttu-id="462c4-132">**[jndi_name]** : nom logique de hello Hello ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="462c4-132">**[jndi_name]**: hello logical name of hello ConnectionFactory.</span></span> <span data-ttu-id="462c4-133">Il s’agit de nom hello qui sera résolu dans une application Java de hello à l’aide de la méthode de JNDI Intialcontext.Lookup hello.</span><span class="sxs-lookup"><span data-stu-id="462c4-133">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="462c4-134">**[ConnectionURL]** : Une URL qui fournit la bibliothèque de hello JMS avec les informations de hello requis service broker de toohello AMQP.</span><span class="sxs-lookup"><span data-stu-id="462c4-134">**[ConnectionURL]**: A URL that provides hello JMS library with hello information required toohello AMQP broker.</span></span>

<span data-ttu-id="462c4-135">format Hello Hello **ConnectionURL** est comme suit :</span><span class="sxs-lookup"><span data-stu-id="462c4-135">hello format of hello **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="462c4-136">Où **[namespace]**, **[SASPolicyName]** et **[SASPolicyKey]** ont hello suivant significations :</span><span class="sxs-lookup"><span data-stu-id="462c4-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have hello following meanings:</span></span>

* <span data-ttu-id="462c4-137">**[espace de noms]** : hello d’espace de noms Service Bus.</span><span class="sxs-lookup"><span data-stu-id="462c4-137">**[namespace]**: hello Service Bus namespace.</span></span>
* <span data-ttu-id="462c4-138">**[SASPolicyName]** : nom de stratégie de file d’attente SAS hello.</span><span class="sxs-lookup"><span data-stu-id="462c4-138">**[SASPolicyName]**: hello Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="462c4-139">**[SASPolicyKey]** : clé de stratégie de file d’attente SAS hello.</span><span class="sxs-lookup"><span data-stu-id="462c4-139">**[SASPolicyKey]**: hello Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="462c4-140">Vous devez coder par URL le mot de passe hello manuellement.</span><span class="sxs-lookup"><span data-stu-id="462c4-140">You must URL-encode hello password manually.</span></span> <span data-ttu-id="462c4-141">Un utilitaire efficace d’encodage dans une URL est disponible à l’adresse [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="462c4-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="462c4-142">Configurer des destinations</span><span class="sxs-lookup"><span data-stu-id="462c4-142">Configure destinations</span></span>
<span data-ttu-id="462c4-143">Hello toodefine entrée utilisée qu'une destination dans le fournisseur JNDI de fichiers de propriétés hello Qpid est Hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="462c4-143">hello entry used toodefine a destination in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="462c4-144">ou</span><span class="sxs-lookup"><span data-stu-id="462c4-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="462c4-145">Où **[jndi\_nom]** et **[physique\_nom]** ont hello suivant significations :</span><span class="sxs-lookup"><span data-stu-id="462c4-145">Where **[jndi\_name]** and **[physical\_name]** have hello following meanings:</span></span>

* <span data-ttu-id="462c4-146">**[jndi_name]** : nom logique de hello de destination de hello.</span><span class="sxs-lookup"><span data-stu-id="462c4-146">**[jndi_name]**: hello logical name of hello destination.</span></span> <span data-ttu-id="462c4-147">Il s’agit de nom hello qui sera résolu dans une application Java de hello à l’aide de la méthode de JNDI Intialcontext.Lookup hello.</span><span class="sxs-lookup"><span data-stu-id="462c4-147">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="462c4-148">**[physical_name]** : nom hello Hello application de Service Bus entité toowhich hello envoie ou reçoit des messages.</span><span class="sxs-lookup"><span data-stu-id="462c4-148">**[physical_name]**: hello name of hello Service Bus entity toowhich hello application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="462c4-149">Lors de la réception à partir d’un abonnement à une rubrique Service Bus, le nom physique de hello spécifié dans JNDI doit être nom hello de rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="462c4-149">When receiving from a Service Bus topic subscription, hello physical name specified in JNDI should be hello name of hello topic.</span></span> <span data-ttu-id="462c4-150">nom de l’abonnement Hello est fourni lors de l’abonnement durable de hello est créé dans le code d’application JMS de hello.</span><span class="sxs-lookup"><span data-stu-id="462c4-150">hello subscription name is provided when hello durable subscription is created in hello JMS application code.</span></span> <span data-ttu-id="462c4-151">Hello [Guide du développeur Service Bus AMQP 1.0](service-bus-amqp-dotnet.md) fournit plus de détails sur l’utilisation des rubriques Service Bus à partir de JMS.</span><span class="sxs-lookup"><span data-stu-id="462c4-151">hello [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-hello-jms-application"></a><span data-ttu-id="462c4-152">Écrire l’application de JMS hello</span><span class="sxs-lookup"><span data-stu-id="462c4-152">Write hello JMS application</span></span>
<span data-ttu-id="462c4-153">Il n’existe aucune API ou option particulière nécessaire à l’utilisation de JMS avec Service Bus.</span><span class="sxs-lookup"><span data-stu-id="462c4-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="462c4-154">Toutefois, il existe quelques restrictions qui seront abordées ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="462c4-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="462c4-155">Comme avec n’importe quelle application JMS, hello première requise est configuration d’environnement de JNDI hello, tooresolve en mesure de toobe un **ConnectionFactory** et les destinations.</span><span class="sxs-lookup"><span data-stu-id="462c4-155">As with any JMS application, hello first thing required is configuration of hello JNDI environment, toobe able tooresolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-hello-jndi-initialcontext"></a><span data-ttu-id="462c4-156">Configurer hello JNDI InitialContext</span><span class="sxs-lookup"><span data-stu-id="462c4-156">Configure hello JNDI InitialContext</span></span>
<span data-ttu-id="462c4-157">environnement de JNDI Hello est configuré en passant d’une table de hachage des informations de configuration dans le constructeur hello de classe de javax.naming.InitialContext hello.</span><span class="sxs-lookup"><span data-stu-id="462c4-157">hello JNDI environment is configured by passing a hashtable of configuration information into hello constructor of hello javax.naming.InitialContext class.</span></span> <span data-ttu-id="462c4-158">deux éléments requis Hello dans la table de hachage hello sont nom de la classe de fabrique de contexte Initial de hello hello et hello URL du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="462c4-158">hello two required elements in hello hashtable are hello class name of hello Initial Context Factory and hello Provider URL.</span></span> <span data-ttu-id="462c4-159">Hello de code suivant montre comment le fichier de propriétés Qpid environnement toouse hello tooconfigure hello JNDI basé fournisseur JNDI avec un fichier de propriétés nommé **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="462c4-159">hello following code shows how tooconfigure hello JNDI environment toouse hello Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="462c4-160">Une simple application JMS utilisant une file d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="462c4-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="462c4-161">Bonjour exemple de programme suivant envoie la file d’attente du Service Bus JMS TextMessages tooa avec le nom logique de JNDI hello de file d’attente et reçoit des messages hello précédent.</span><span class="sxs-lookup"><span data-stu-id="462c4-161">hello following example program sends JMS TextMessages tooa Service Bus queue with hello JNDI logical name of QUEUE, and receives hello messages back.</span></span>

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

### <a name="run-hello-application"></a><span data-ttu-id="462c4-162">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="462c4-162">Run hello application</span></span>
<span data-ttu-id="462c4-163">Exécute l’application hello génère la sortie sous forme de hello :</span><span class="sxs-lookup"><span data-stu-id="462c4-163">Running hello application produces output of hello form:</span></span>

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

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="462c4-164">Messagerie interplateforme entre JMS et .NET</span><span class="sxs-lookup"><span data-stu-id="462c4-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="462c4-165">Ce guide a montré comment toosend et de recevoir des messages tooand de Bus de Service à l’aide de JMS.</span><span class="sxs-lookup"><span data-stu-id="462c4-165">This guide showed how toosend and receive messages tooand from Service Bus using JMS.</span></span> <span data-ttu-id="462c4-166">Toutefois, un des avantages clés de hello AMQP 1.0 est qu’il permet des toobe applications générée à partir de composants écrits dans différentes langues, avec des messages échangés et de manière fiable avec une fidélité optimale.</span><span class="sxs-lookup"><span data-stu-id="462c4-166">However, one of hello key benefits of AMQP 1.0 is that it enables applications toobe built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="462c4-167">À l’aide de hello exemple d’application JMS décrites ci-dessus et d’une application .NET similaire obtenue à partir d’un article d’accompagnement, [à l’aide de Service Bus à partir de .NET avec AMQP 1.0](service-bus-amqp-dotnet.md), vous pouvez échanger des messages entre .NET et Java.</span><span class="sxs-lookup"><span data-stu-id="462c4-167">Using hello sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="462c4-168">Lisez cet article pour plus d’informations sur les détails de hello de messagerie à l’aide du Service Bus et AMQP 1.0 inter-plateformes.</span><span class="sxs-lookup"><span data-stu-id="462c4-168">Read this article for more information about hello details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-toonet"></a><span data-ttu-id="462c4-169">JMS too.NET</span><span class="sxs-lookup"><span data-stu-id="462c4-169">JMS too.NET</span></span>
<span data-ttu-id="462c4-170">toodemonstrate JMS too.NET de messagerie :</span><span class="sxs-lookup"><span data-stu-id="462c4-170">toodemonstrate JMS too.NET messaging:</span></span>

* <span data-ttu-id="462c4-171">Démarrer l’application d’exemple hello .NET sans arguments de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="462c4-171">Start hello .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="462c4-172">Démarrez l’exemple d’application Java hello avec l’argument de ligne de commande « sendonly » hello.</span><span class="sxs-lookup"><span data-stu-id="462c4-172">Start hello Java sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="462c4-173">Dans ce mode, hello application ne reçoit pas de messages à partir de la file d’attente de hello, elle n’envoie.</span><span class="sxs-lookup"><span data-stu-id="462c4-173">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="462c4-174">Appuyez sur **entrée** plusieurs fois dans la console de l’application Java hello, ce qui entraîne une toobe de messages envoyé.</span><span class="sxs-lookup"><span data-stu-id="462c4-174">Press **Enter** a few times in hello Java application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="462c4-175">Ces messages sont reçus par hello application .NET.</span><span class="sxs-lookup"><span data-stu-id="462c4-175">These messages are received by hello .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="462c4-176">Résultat de l'application JMS</span><span class="sxs-lookup"><span data-stu-id="462c4-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="462c4-177">Résultat de l'application .NET</span><span class="sxs-lookup"><span data-stu-id="462c4-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a><span data-ttu-id="462c4-178">.NET tooJMS</span><span class="sxs-lookup"><span data-stu-id="462c4-178">.NET tooJMS</span></span>
<span data-ttu-id="462c4-179">toodemonstrate tooJMS de .NET de messagerie :</span><span class="sxs-lookup"><span data-stu-id="462c4-179">toodemonstrate .NET tooJMS messaging:</span></span>

* <span data-ttu-id="462c4-180">Démarrez l’exemple d’application .NET hello avec l’argument de ligne de commande « sendonly » hello.</span><span class="sxs-lookup"><span data-stu-id="462c4-180">Start hello .NET sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="462c4-181">Dans ce mode, hello application ne reçoit pas de messages à partir de la file d’attente de hello, elle n’envoie.</span><span class="sxs-lookup"><span data-stu-id="462c4-181">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="462c4-182">Démarrer l’application d’exemple hello Java sans arguments de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="462c4-182">Start hello Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="462c4-183">Appuyez sur **entrée** plusieurs fois dans la console de l’application hello .NET, ce qui entraîne une toobe de messages envoyé.</span><span class="sxs-lookup"><span data-stu-id="462c4-183">Press **Enter** a few times in hello .NET application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="462c4-184">Ces messages sont reçus par hello application Java.</span><span class="sxs-lookup"><span data-stu-id="462c4-184">These messages are received by hello Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="462c4-185">Résultat de l'application .NET</span><span class="sxs-lookup"><span data-stu-id="462c4-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="462c4-186">Résultat de l'application JMS</span><span class="sxs-lookup"><span data-stu-id="462c4-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="462c4-187">Fonctionnalités non prises en charge et restrictions</span><span class="sxs-lookup"><span data-stu-id="462c4-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="462c4-188">Hello suivant des restrictions existe lors de l’utilisation de JMS via AMQP 1.0 avec Service Bus, à savoir :</span><span class="sxs-lookup"><span data-stu-id="462c4-188">hello following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="462c4-189">Un seul **MessageProducer** ou **MessageConsumer** est autorisé par **Session**.</span><span class="sxs-lookup"><span data-stu-id="462c4-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="462c4-190">Si vous avez besoin de toocreate plusieurs **MessageProducers** ou **MessageConsumers** dans une application, créez une dédiée **Session** pour chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="462c4-190">If you need toocreate multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="462c4-191">Les abonnements aux rubriques volatiles ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="462c4-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="462c4-192">Les **MessageSelectors** ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="462c4-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="462c4-193">Destinations temporaires ; par exemple, **TemporaryQueue**, **TemporaryTopic** ne sont pas actuellement pris en charge, ainsi que de hello **QueueRequestor** et **TopicRequestor**API qui les utilisent.</span><span class="sxs-lookup"><span data-stu-id="462c4-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with hello **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="462c4-194">Les sessions traitées et les transactions distribuées ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="462c4-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="462c4-195">Résumé</span><span class="sxs-lookup"><span data-stu-id="462c4-195">Summary</span></span>
<span data-ttu-id="462c4-196">Cette procédure-tooguide a montré comment toouse répartie de Service Bus des fonctionnalités de messagerie (files d’attente et publication/abonnement rubriques) à partir de Java à l’aide de hello populaires API JMS et AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="462c4-196">This how-tooguide showed how toouse Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using hello popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="462c4-197">Vous pouvez également utiliser l'AMQP 1.0 de Service Bus depuis d'autres langages, notamment .NET, C, Python et PHP.</span><span class="sxs-lookup"><span data-stu-id="462c4-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="462c4-198">Composants créés à l’aide de ces langages différents peuvent échanger des messages et de manière fiable avec une fidélité optimale à l’aide de la prise en charge hello AMQP 1.0 dans Service Bus.</span><span class="sxs-lookup"><span data-stu-id="462c4-198">Components built using these different languages can exchange messages reliably and at full fidelity using hello AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="462c4-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="462c4-199">Next steps</span></span>
* [<span data-ttu-id="462c4-200">Prise en charge d’AMQP 1.0 dans Service Bus</span><span class="sxs-lookup"><span data-stu-id="462c4-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="462c4-201">Comment toouse AMQP 1.0 avec hello les API .NET Service Bus</span><span class="sxs-lookup"><span data-stu-id="462c4-201">How toouse AMQP 1.0 with hello Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="462c4-202">Guide du développeur sur l’utilisation de Service Bus avec AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="462c4-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="462c4-203">Prise en main des files d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="462c4-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="462c4-204">Centre de développement Java</span><span class="sxs-lookup"><span data-stu-id="462c4-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

