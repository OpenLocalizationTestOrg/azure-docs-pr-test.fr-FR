---
title: "Utilisation des rubriques Azure Service Bus avec Java | Microsoft Docs"
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
ms.openlocfilehash: b561d6fdcf4fb2839908ac8f53832fb0830dd576
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="c9999-103">Utilisation des rubriques et abonnements Service Bus avec Java</span><span class="sxs-lookup"><span data-stu-id="c9999-103">How to use Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="c9999-104">Ce guide décrit l’utilisation des rubriques et des abonnements Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c9999-104">This guide describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="c9999-105">Les exemples sont écrits en Java et utilisent le [Kit de développement logiciel (SDK) Azure pour Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="c9999-105">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="c9999-106">Les scénarios couverts incluent la **création de rubriques et d’abonnements**, la **création de filtres d’abonnement**, **l’envoi de messages à une rubrique**, la **réception de messages en provenance d’un abonnement** et enfin la **suppression de rubriques et d’abonnements**.</span><span class="sxs-lookup"><span data-stu-id="c9999-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="c9999-107">Présentation des rubriques et des abonnements Service Bus</span><span class="sxs-lookup"><span data-stu-id="c9999-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="c9999-108">Les rubriques et les abonnements Service Bus prennent en charge un modèle de communication de messagerie *de publication et d'abonnement* .</span><span class="sxs-lookup"><span data-stu-id="c9999-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="c9999-109">Lors de l’utilisation de rubriques et d’abonnements, les composants d’une application distribuée ne communiquent pas directement entre eux ; ils échangent plutôt des messages via une rubrique, qui fait office d’intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="c9999-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="c9999-111">Contrairement aux files d’attente Service Bus, où chaque message est traité par un seul consommateur, les rubriques et les abonnements fournissent une forme de communication « un-à-plusieurs », à l'aide d'un modèle de publication et d'abonnement.</span><span class="sxs-lookup"><span data-stu-id="c9999-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="c9999-112">Il est possible d’inscrire plusieurs abonnements à une rubrique.</span><span class="sxs-lookup"><span data-stu-id="c9999-112">It is possible to register multiple subscriptions to a topic.</span></span> <span data-ttu-id="c9999-113">Lorsqu’un message est envoyé à une rubrique, il est alors mis à disposition de chaque abonnement pour être géré ou traité indépendamment.</span><span class="sxs-lookup"><span data-stu-id="c9999-113">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span></span>

<span data-ttu-id="c9999-114">Un abonnement à une rubrique ressemble à une file d’attente virtuelle qui reçoit des copies des messages envoyés à la rubrique.</span><span class="sxs-lookup"><span data-stu-id="c9999-114">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span></span> <span data-ttu-id="c9999-115">Vous pouvez éventuellement inscrire des règles de filtre pour une rubrique par abonnement, ce qui vous permet de filtrer et de restreindre les messages d’une rubrique reçus en fonction des abonnements à une rubrique.</span><span class="sxs-lookup"><span data-stu-id="c9999-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you to filter/restrict which messages to a topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="c9999-116">Les rubriques et les abonnements Service Bus vous permettent de mettre votre infrastructure à l’échelle pour traiter de très nombreux messages parmi un très grand nombre d’utilisateurs et d’applications.</span><span class="sxs-lookup"><span data-stu-id="c9999-116">Service Bus topics and subscriptions enable you to scale to process a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="c9999-117">Création d'un espace de noms de service</span><span class="sxs-lookup"><span data-stu-id="c9999-117">Create a service namespace</span></span>
<span data-ttu-id="c9999-118">Pour commencer à utiliser les rubriques et abonnements Service Bus dans Azure, vous devez d’abord créer un espace de noms, qui fournit un conteneur d’étendue pour l’adressage de ressources Service Bus au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="c9999-118">To begin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="c9999-119">Pour créer un espace de noms :</span><span class="sxs-lookup"><span data-stu-id="c9999-119">To create a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="c9999-120">Configuration de votre application pour l’utilisation de Service Bus</span><span class="sxs-lookup"><span data-stu-id="c9999-120">Configure your application to use Service Bus</span></span>
<span data-ttu-id="c9999-121">Vérifiez que vous avez installé le [Kit de développement logiciel (SDK) Azure pour Java][Azure SDK for Java] avant de créer cet exemple.</span><span class="sxs-lookup"><span data-stu-id="c9999-121">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="c9999-122">Si vous utilisez Eclipse, vous pouvez installer le [Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse] qui inclut le Kit de développement logiciel (SDK) Azure pour Java.</span><span class="sxs-lookup"><span data-stu-id="c9999-122">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="c9999-123">Vous pouvez ensuite ajouter les **bibliothèques Microsoft Azure pour Java** à votre projet :</span><span class="sxs-lookup"><span data-stu-id="c9999-123">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="c9999-124">Ajoutez les instructions `import` suivantes au début du fichier Java :</span><span class="sxs-lookup"><span data-stu-id="c9999-124">Add the following `import` statements to the top of the Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="c9999-125">Ajoutez les bibliothèques Azure pour Java au chemin de votre build et incluez-le dans votre assembly de déploiement du projet.</span><span class="sxs-lookup"><span data-stu-id="c9999-125">Add the Azure Libraries for Java to your build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="c9999-126">Création d'une rubrique</span><span class="sxs-lookup"><span data-stu-id="c9999-126">Create a topic</span></span>
<span data-ttu-id="c9999-127">Les opérations de gestion des rubriques Service Bus peuvent être effectuées par le biais de la classe **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="c9999-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="c9999-128">Un objet **ServiceBusContract** est construit avec une configuration appropriée qui encapsule le jeton SAP avec des autorisations pour le gérer, et la classe **ServiceBusContract** est le point de communication unique avec Azure.</span><span class="sxs-lookup"><span data-stu-id="c9999-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="c9999-129">La classe **ServiceBusService** fournit des méthodes pour créer, énumérer et supprimer des rubriques.</span><span class="sxs-lookup"><span data-stu-id="c9999-129">The **ServiceBusService** class provides methods to create, enumerate, and delete topics.</span></span> <span data-ttu-id="c9999-130">L’exemple suivant présente un objet **ServiceBusService** qui peut être utilisé pour créer une rubrique nommée `TestTopic` avec un espace de noms appelé `HowToSample` :</span><span class="sxs-lookup"><span data-stu-id="c9999-130">The following example shows how a **ServiceBusService** object can be used to create a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

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

<span data-ttu-id="c9999-131">Il existe des méthodes sur **TopicInfo** qui permettent de paramétrer des propriétés de la rubrique (par exemple, la valeur par défaut « time-to-live » (TTL) à appliquer aux messages envoyés à la rubrique).</span><span class="sxs-lookup"><span data-stu-id="c9999-131">There are methods on **TopicInfo** that enable properties of the topic to be set (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the topic).</span></span> <span data-ttu-id="c9999-132">L’exemple suivant montre comment créer une rubrique nommée `TestTopic` avec une taille maximale de 5 Go :</span><span class="sxs-lookup"><span data-stu-id="c9999-132">The following example shows how to create a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="c9999-133">Notez que vous pouvez utiliser la méthode **listTopics** sur les objets **ServiceBusContract** afin de vérifier si une rubrique avec le nom spécifié existe dans l’espace de noms d’un service.</span><span class="sxs-lookup"><span data-stu-id="c9999-133">Note that you can use the **listTopics** method on **ServiceBusContract** objects to check if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="c9999-134">Création d’abonnements</span><span class="sxs-lookup"><span data-stu-id="c9999-134">Create subscriptions</span></span>
<span data-ttu-id="c9999-135">Les abonnements à des rubriques sont également créés avec la classe **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="c9999-135">Subscriptions to topics are also created with the **ServiceBusService** class.</span></span> <span data-ttu-id="c9999-136">Les abonnements sont nommés et peuvent être assortis d'un filtre facultatif qui limite l'ensemble des messages transmis à la file d'attente virtuelle de l'abonnement.</span><span class="sxs-lookup"><span data-stu-id="c9999-136">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="c9999-137">Création d’un abonnement avec le filtre par défaut (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="c9999-137">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="c9999-138">Le filtre **MatchAll** est le filtre utilisé par défaut si aucun filtre n’est spécifié lors de la création d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="c9999-138">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="c9999-139">Lorsque le filtre **MatchAll** est utilisé, tous les messages publiés dans la rubrique sont placés dans la file d’attente virtuelle de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="c9999-139">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="c9999-140">Dans l’exemple suivant, l’abonnement « AllMessages » qui est créé utilise le filtre par défaut **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="c9999-140">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="c9999-141">Création d’abonnements avec des filtres</span><span class="sxs-lookup"><span data-stu-id="c9999-141">Create subscriptions with filters</span></span>
<span data-ttu-id="c9999-142">Vous pouvez également créer des filtres pour spécifier quels sont les messages, parmi ceux envoyés à une rubrique, qui doivent apparaître dans un abonnement de rubrique spécifique.</span><span class="sxs-lookup"><span data-stu-id="c9999-142">You can also create filters that enable you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="c9999-143">Parmi les types de filtre pris en charge par les abonnements, [SqlFilter][SqlFilter] est le plus flexible. Il implémente un sous-ensemble de SQL92.</span><span class="sxs-lookup"><span data-stu-id="c9999-143">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="c9999-144">Les filtres SQL opèrent au niveau des propriétés des messages publiés dans la rubrique.</span><span class="sxs-lookup"><span data-stu-id="c9999-144">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="c9999-145">Pour plus de détails sur les expressions utilisables avec un filtre SQL, examinez la syntaxe [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="c9999-145">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="c9999-146">Dans l’exemple suivant, l’abonnement nommé `HighMessages` est créé avec un objet [SqlFilter][SqlFilter] qui sélectionne uniquement les messages dont la propriété personnalisée **MessageNumber** a une valeur supérieure à 3 :</span><span class="sxs-lookup"><span data-stu-id="c9999-146">The following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="c9999-147">De même, l’exemple suivant crée l’abonnement nommé `LowMessages` avec un objet [SqlFilter][SqlFilter] qui sélectionne uniquement les messages dont la propriété **MessageNumber** a une valeur inférieure ou égale à 3 :</span><span class="sxs-lookup"><span data-stu-id="c9999-147">Similarly, the following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal to 3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="c9999-148">À présent, dès qu’un message est envoyé vers `TestTopic`, il est toujours remis aux destinataires abonnés à l’abonnement `AllMessages` et est remis de manière sélective aux destinataires abonnés aux abonnements `HighMessages` et `LowMessages` (en fonction du contenu du message).</span><span class="sxs-lookup"><span data-stu-id="c9999-148">When a message is now sent to `TestTopic`, it will always be delivered to receivers subscribed to the `AllMessages` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="c9999-149">Envoi de messages à une rubrique</span><span class="sxs-lookup"><span data-stu-id="c9999-149">Send messages to a topic</span></span>
<span data-ttu-id="c9999-150">Pour envoyer un message à une rubrique Service Bus, votre application obtient un objet **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="c9999-150">To send a message to a Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="c9999-151">Le code suivant montre comment envoyer un message à la rubrique `TestTopic` créée plus haut dans l’espace de noms `HowToSample` :</span><span class="sxs-lookup"><span data-stu-id="c9999-151">The following code demonstrates how to send a message for the `TestTopic` topic created previously within the `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="c9999-152">Les messages envoyés aux rubriques Service Bus sont des instances de la classe [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="c9999-152">Messages sent to Service Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="c9999-153">Les objets [BrokeredMessage][BrokeredMessage]* possèdent un ensemble de méthodes standard (telles que **setLabel** et **TimeToLive**), un dictionnaire servant à conserver les propriétés personnalisées propres à une application, ainsi qu’un corps de données d’application arbitraires.</span><span class="sxs-lookup"><span data-stu-id="c9999-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="c9999-154">Une application peut définir le corps du message en transmettant un objet sérialisable au constructeur de l’objet [BrokeredMessage][BrokeredMessage]. Le sérialiseur **DataContractSerializer** approprié est alors utilisé pour sérialiser l’objet.</span><span class="sxs-lookup"><span data-stu-id="c9999-154">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate **DataContractSerializer** will then be used to serialize the object.</span></span> <span data-ttu-id="c9999-155">Une autre possibilité consiste à fournir un **java.io.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="c9999-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="c9999-156">L’exemple suivant montre comment envoyer cinq messages de test au client **MessageSender** `TestTopic` obtenu dans l’extrait de code précédent.</span><span class="sxs-lookup"><span data-stu-id="c9999-156">The following example demonstrates how to send five test messages to the `TestTopic` **MessageSender** we obtained in the code snippet above.</span></span>
<span data-ttu-id="c9999-157">Notez que la valeur de la propriété **MessageNumber** de chaque message varie au niveau de l’itération de la boucle (détermine les abonnements qui le reçoivent) :</span><span class="sxs-lookup"><span data-stu-id="c9999-157">Note how the **MessageNumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for the body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message to the topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="c9999-158">Les rubriques Service Bus prennent en charge une taille de message maximale de 256 Ko dans le [niveau Standard](service-bus-premium-messaging.md) et de 1 Mo dans le [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="c9999-158">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="c9999-159">L’en-tête, qui comprend les propriétés d’application standard et personnalisées, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="c9999-159">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="c9999-160">Si une rubrique n’est pas limitée par le nombre de messages qu’elle peut contenir, elle l’est en revanche par la taille totale des messages qu’elle contient.</span><span class="sxs-lookup"><span data-stu-id="c9999-160">There is no limit on the number of messages held in a topic but there is a limit on the total size of the messages held by a topic.</span></span> <span data-ttu-id="c9999-161">Cette taille de rubrique est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="c9999-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-subscription"></a><span data-ttu-id="c9999-162">Réception des messages d'un abonnement</span><span class="sxs-lookup"><span data-stu-id="c9999-162">How to receive messages from a subscription</span></span>
<span data-ttu-id="c9999-163">Pour recevoir les messages d’un abonnement, utilisez un objet **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="c9999-163">To receive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="c9999-164">Ces messages reçus peuvent fonctionner dans deux modes différents : **ReceiveAndDelete** et **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="c9999-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="c9999-165">Lorsque le mode **ReceiveAndDelete** est utilisé, la réception est une opération unique : quand Service Bus reçoit une demande de lecture pour un message, il marque ce message comme étant consommé et le renvoie à l’application.</span><span class="sxs-lookup"><span data-stu-id="c9999-165">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="c9999-166">Le mode **ReceiveAndDelete** est le modèle le plus simple et le mieux adapté aux scénarios dans lesquels une application est capable de tolérer le non-traitement d’un message en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="c9999-166">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="c9999-167">Pour mieux comprendre, imaginez un scénario dans lequel le consommateur émet la demande de réception et subit un incident avant de la traiter.</span><span class="sxs-lookup"><span data-stu-id="c9999-167">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="c9999-168">Comme Service Bus a marqué le message comme étant consommé, lorsque l’application redémarre et recommence à consommer des messages, elle manque le message consommé avant l’incident.</span><span class="sxs-lookup"><span data-stu-id="c9999-168">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="c9999-169">En mode **PeekLock**, la réception devient une opération en deux étapes, qui autorise une prise en charge des applications qui ne peuvent pas tolérer les messages manquants.</span><span class="sxs-lookup"><span data-stu-id="c9999-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="c9999-170">Lorsque Service Bus reçoit une demande, il recherche le prochain message à consommer, le verrouille pour empêcher d'autres consommateurs de le recevoir, puis le renvoie à l'application.</span><span class="sxs-lookup"><span data-stu-id="c9999-170">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="c9999-171">Dès lors que l’application a terminé le traitement du message (ou qu’elle l’a stocké de manière fiable pour un traitement ultérieur), elle accomplit la deuxième étape du processus de réception en appelant **Delete** pour le message reçu.</span><span class="sxs-lookup"><span data-stu-id="c9999-171">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="c9999-172">Lorsque Service Bus obtient l’appel **Delete**, il marque le message comme étant consommé et le supprime de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="c9999-172">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the topic.</span></span>

<span data-ttu-id="c9999-173">L’exemple ci-dessous montre comment les messages peuvent être reçus et traités avec le mode **PeekLock** (et non le mode par défaut).</span><span class="sxs-lookup"><span data-stu-id="c9999-173">The example below demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="c9999-174">L'exemple ci-dessous lance une boucle qui traite les messages de l'abonnement HighMessages, qui s'arrête lorsqu'il n'y a plus de messages (cette boucle peut aussi être configurée pour attendre de nouveaux messages).</span><span class="sxs-lookup"><span data-stu-id="c9999-174">The example below performs a loop and processes messages in the "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set to wait for new messages).</span></span>

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
            // Display the topic message.
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
            // Added to handle no more messages.
            // Could instead wait for more messages to be added.
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="c9999-175">Gestion des blocages d’application et des messages illisibles</span><span class="sxs-lookup"><span data-stu-id="c9999-175">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="c9999-176">Service Bus intègre des fonctionnalités destinées à faciliter la récupération à la suite d’erreurs survenues dans votre application ou de difficultés à traiter un message.</span><span class="sxs-lookup"><span data-stu-id="c9999-176">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="c9999-177">Si une application réceptrice ne parvient pas à traiter le message pour une raison quelconque, elle appelle la méthode **unlockMessage** pour le message reçu (au lieu de la méthode **deleteMessage**).</span><span class="sxs-lookup"><span data-stu-id="c9999-177">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="c9999-178">Cela amène Service Bus à déverrouiller le message dans la rubrique et à le rendre à nouveau disponible en réception, pour la même application consommatrice ou pour une autre.</span><span class="sxs-lookup"><span data-stu-id="c9999-178">This will cause Service Bus to unlock the message within the topic and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="c9999-179">De même, il faut savoir qu’un message verrouillé dans la rubrique est assorti d’un délai d’expiration et que, si l’application ne parvient pas à traiter le message dans le temps imparti (par exemple, si l’application subit un incident), Service Bus déverrouille le message automatiquement et le rend à nouveau disponible en réception.</span><span class="sxs-lookup"><span data-stu-id="c9999-179">There is also a timeout associated with a message locked within the topic, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="c9999-180">Si l’application subit un incident après le traitement du message, mais avant l’émission de la demande **deleteMessage**, le message est à nouveau remis à l’application lorsqu’elle redémarre.</span><span class="sxs-lookup"><span data-stu-id="c9999-180">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="c9999-181">Dans ce type de traitement, souvent appelé **Au moins une fois**, chaque message est traité au moins une fois. Toutefois, dans certaines circonstances, un même message peut être remis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="c9999-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="c9999-182">Toutefois, dans certaines circonstances, un même message peut être remis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="c9999-182">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="c9999-183">Ceci est souvent obtenu grâce à la propriété **getMessageId** du message, qui reste constante pendant les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="c9999-183">This is often achieved using the **getMessageId** method of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="c9999-184">Suppression de rubriques et d'abonnements</span><span class="sxs-lookup"><span data-stu-id="c9999-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="c9999-185">Le principal moyen de supprimer des rubriques et des abonnements est d’utiliser un objet **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="c9999-185">The primary way to delete topics and subscriptions is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="c9999-186">La suppression d’une rubrique a également pour effet de supprimer les abonnements inscrits au niveau de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="c9999-186">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="c9999-187">Les abonnements peuvent aussi être supprimés de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="c9999-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="c9999-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c9999-188">Next Steps</span></span>
<span data-ttu-id="c9999-189">Maintenant que vous connaissez les principes de base des files d’attente Service Bus, consultez la rubrique traitant des [Files d’attente, rubriques et abonnements Service Bus][Service Bus queues, topics, and subscriptions] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="c9999-189">Now that you've learned the basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
