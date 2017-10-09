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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="550c6-103">Comment toouse Service Bus rubriques et les abonnements avec Java</span><span class="sxs-lookup"><span data-stu-id="550c6-103">How toouse Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="550c6-104">Ce guide décrit comment toouse Service Bus rubriques et abonnements.</span><span class="sxs-lookup"><span data-stu-id="550c6-104">This guide describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="550c6-105">exemples de Hello sont écrits en Java et utiliser hello [SDK Azure pour Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="550c6-105">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="550c6-106">Hello scénarios abordés incluent **création de rubriques et abonnements**, **création de filtres d’abonnement**, **envoi rubrique tooa de messages**, **réception les messages à partir d’un abonnement**, et **suppression des rubriques et abonnements**.</span><span class="sxs-lookup"><span data-stu-id="550c6-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="550c6-107">Présentation des rubriques et des abonnements Service Bus</span><span class="sxs-lookup"><span data-stu-id="550c6-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="550c6-108">Les rubriques et les abonnements Service Bus prennent en charge un modèle de communication de messagerie *de publication et d'abonnement* .</span><span class="sxs-lookup"><span data-stu-id="550c6-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="550c6-109">Lors de l’utilisation de rubriques et d’abonnements, les composants d’une application distribuée ne communiquent pas directement entre eux ; ils échangent plutôt des messages via une rubrique, qui fait office d’intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="550c6-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="550c6-111">Contrairement aux files d’attente Service Bus, où chaque message est traité par un seul consommateur, les rubriques et les abonnements fournissent une forme de communication « un-à-plusieurs », à l'aide d'un modèle de publication et d'abonnement.</span><span class="sxs-lookup"><span data-stu-id="550c6-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="550c6-112">Il est possible d’inscrire la rubrique de tooa plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="550c6-112">It is possible to register multiple subscriptions tooa topic.</span></span> <span data-ttu-id="550c6-113">Lorsqu’un message est envoyé à tooa rubrique, il est alors effectuée indépendamment disponible tooeach toohandle/processus d’inscription.</span><span class="sxs-lookup"><span data-stu-id="550c6-113">When a message is sent tooa topic, it is then made available tooeach subscription toohandle/process independently.</span></span>

<span data-ttu-id="550c6-114">Une rubrique de tooa abonnement ressemble à une file d’attente virtuelle qui reçoit des copies des messages de type hello qui ont été envoyés toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="550c6-114">A subscription tooa topic resembles a virtual queue that receives copies of hello messages that were sent toohello topic.</span></span> <span data-ttu-id="550c6-115">Vous pouvez éventuellement enregistrer les règles de filtre pour une rubrique à la fois par abonnement, ce qui vous permet de restreindre/toofilter le sujet tooa messages sont reçus par les abonnements à la rubrique.</span><span class="sxs-lookup"><span data-stu-id="550c6-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you toofilter/restrict which messages tooa topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="550c6-116">Abonnements et rubriques Service Bus permettent tooscale tooprocess un très grand nombre de messages sur un très grand nombre d’utilisateurs et des applications.</span><span class="sxs-lookup"><span data-stu-id="550c6-116">Service Bus topics and subscriptions enable you tooscale tooprocess a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="550c6-117">Création d'un espace de noms de service</span><span class="sxs-lookup"><span data-stu-id="550c6-117">Create a service namespace</span></span>
<span data-ttu-id="550c6-118">toobegin à l’aide des rubriques et abonnements Service Bus dans Azure, vous devez d’abord créer un espace de noms, qui fournit un conteneur d’étendue pour adresser les ressources Service Bus au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="550c6-118">toobegin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="550c6-119">toocreate un espace de noms :</span><span class="sxs-lookup"><span data-stu-id="550c6-119">toocreate a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="550c6-120">Configurer votre toouse application Service Bus</span><span class="sxs-lookup"><span data-stu-id="550c6-120">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="550c6-121">Vérifiez que vous avez installé hello [SDK Azure pour Java] [ Azure SDK for Java] avant de générer cet exemple.</span><span class="sxs-lookup"><span data-stu-id="550c6-121">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="550c6-122">Si vous utilisez Eclipse, vous pouvez installer hello [boîte à outils Azure pour Eclipse] [ Azure Toolkit for Eclipse] incluant hello SDK Azure pour Java.</span><span class="sxs-lookup"><span data-stu-id="550c6-122">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="550c6-123">Vous pouvez ensuite ajouter hello **bibliothèques Microsoft Azure pour Java** tooyour projet :</span><span class="sxs-lookup"><span data-stu-id="550c6-123">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="550c6-124">Ajoutez hello suit `import` haut de toohello instructions hello du fichier de Java :</span><span class="sxs-lookup"><span data-stu-id="550c6-124">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="550c6-125">Ajoutez hello les bibliothèques Azure pour Java tooyour générer le chemin d’accès et l’inclure dans votre assembly de déploiement du projet.</span><span class="sxs-lookup"><span data-stu-id="550c6-125">Add hello Azure Libraries for Java tooyour build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="550c6-126">Création d'une rubrique</span><span class="sxs-lookup"><span data-stu-id="550c6-126">Create a topic</span></span>
<span data-ttu-id="550c6-127">Les opérations de gestion des rubriques Service Bus peuvent être effectuées par le biais de la classe **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="550c6-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="550c6-128">A **ServiceBusContract** objet est construit avec une configuration appropriée qui encapsule le jeton SAS avec les autorisations toomanage et hello **ServiceBusContract** classe est point unique de hello de la communication avec Azure.</span><span class="sxs-lookup"><span data-stu-id="550c6-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="550c6-129">Hello **ServiceBusService** classe fournit des méthodes toocreate, énumérer et supprimer des rubriques.</span><span class="sxs-lookup"><span data-stu-id="550c6-129">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete topics.</span></span> <span data-ttu-id="550c6-130">Hello suivant montre l’exemple de comment un **ServiceBusService** objet peut être utilisé toocreate une rubrique nommée `TestTopic`, avec un espace de noms appelé `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="550c6-130">hello following example shows how a **ServiceBusService** object can be used toocreate a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

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

<span data-ttu-id="550c6-131">Il existe des méthodes sur **TopicInfo** qui permettent des propriétés de la rubrique hello à définir (par exemple : tooset hello par défaut time-to-live (TTL) valeur toobe appliqué toomessages envoyé toohello rubrique).</span><span class="sxs-lookup"><span data-stu-id="550c6-131">There are methods on **TopicInfo** that enable properties of hello topic to be set (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello topic).</span></span> <span data-ttu-id="550c6-132">Hello suivant montre comment toocreate une rubrique nommée `TestTopic` avec une taille maximale de 5 Go :</span><span class="sxs-lookup"><span data-stu-id="550c6-132">hello following example shows how toocreate a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="550c6-133">Notez que vous pouvez utiliser hello **listTopics** méthode sur **ServiceBusContract** objets toocheck si une rubrique portant le nom spécifié existe déjà dans un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="550c6-133">Note that you can use hello **listTopics** method on **ServiceBusContract** objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="550c6-134">Création d’abonnements</span><span class="sxs-lookup"><span data-stu-id="550c6-134">Create subscriptions</span></span>
<span data-ttu-id="550c6-135">Abonnements tootopics sont également créés par hello **ServiceBusService** classe.</span><span class="sxs-lookup"><span data-stu-id="550c6-135">Subscriptions tootopics are also created with hello **ServiceBusService** class.</span></span> <span data-ttu-id="550c6-136">Les abonnements sont nommés et peuvent avoir un filtre facultatif qui limite l’ensemble de hello de messages transmis de file d’attente virtuelle de l’abonnement toohello.</span><span class="sxs-lookup"><span data-stu-id="550c6-136">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="550c6-137">Créer un abonnement avec le filtre par défaut (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="550c6-137">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="550c6-138">Hello **MatchAll** filtre est hello par défaut qui est utilisé si aucun filtre n’est spécifiée lors de la création d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="550c6-138">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="550c6-139">Hello lorsque **MatchAll** filtre est utilisé, la rubrique de toohello publié tous les messages sont placés dans la file d’attente virtuelle de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="550c6-139">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="550c6-140">Hello exemple suivant crée un abonnement nommé « AllMessages » et utilise hello par défaut **MatchAll** filtre.</span><span class="sxs-lookup"><span data-stu-id="550c6-140">hello following example creates a subscription named "AllMessages" and uses hello default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="550c6-141">Création d’abonnements avec des filtres</span><span class="sxs-lookup"><span data-stu-id="550c6-141">Create subscriptions with filters</span></span>
<span data-ttu-id="550c6-142">Vous pouvez également créer des filtres qui vous tooscope lesquelles messages envoyés tooa rubrique doit apparaître dans un abonnement à une rubrique spécifique.</span><span class="sxs-lookup"><span data-stu-id="550c6-142">You can also create filters that enable you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="550c6-143">Bonjour type de filtre pris en charge par les abonnements plus souple est la [SqlFilter][SqlFilter], qui implémente un sous-ensemble de SQL92.</span><span class="sxs-lookup"><span data-stu-id="550c6-143">hello most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="550c6-144">Filtres SQL fonctionnent sur les propriétés hello de messages hello qui sont publiées toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="550c6-144">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="550c6-145">Pour plus d’informations sur les expressions hello qui peuvent être utilisées avec un filtre SQL, consultez hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxe.</span><span class="sxs-lookup"><span data-stu-id="550c6-145">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="550c6-146">Hello exemple suivant crée un abonnement nommé `HighMessages` avec un [SqlFilter] [ SqlFilter] objet qui sélectionne uniquement les messages qui ont personnalisé **MessageNumber** propriété est supérieure à 3 :</span><span class="sxs-lookup"><span data-stu-id="550c6-146">hello following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

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

<span data-ttu-id="550c6-147">De même, hello exemple suivant crée un abonnement nommé `LowMessages` avec un [SqlFilter] [ SqlFilter] objet qui sélectionne uniquement les messages qui ont un **MessageNumber** propriété inférieur ou égal too3 :</span><span class="sxs-lookup"><span data-stu-id="550c6-147">Similarly, hello following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal too3:</span></span>

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

<span data-ttu-id="550c6-148">Lorsqu’un message est envoyé maintenant trop`TestTopic`, il sera toujours remis tooreceivers abonné toohello `AllMessages` abonnement et remis de manière sélective tooreceivers abonné toohello `HighMessages` et `LowMessages` (des abonnements selon le contenu du message).</span><span class="sxs-lookup"><span data-stu-id="550c6-148">When a message is now sent too`TestTopic`, it will always be delivered tooreceivers subscribed toohello `AllMessages` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="550c6-149">Rubrique tooa de messages d’envoi</span><span class="sxs-lookup"><span data-stu-id="550c6-149">Send messages tooa topic</span></span>
<span data-ttu-id="550c6-150">toosend une rubrique de Service Bus message tooa, votre application obtient un **ServiceBusContract** objet.</span><span class="sxs-lookup"><span data-stu-id="550c6-150">toosend a message tooa Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="550c6-151">Hello de code suivant montre comment toosend un message pour hello `TestTopic` rubrique créée précédemment dans hello `HowToSample` espace de noms :</span><span class="sxs-lookup"><span data-stu-id="550c6-151">hello following code demonstrates how toosend a message for hello `TestTopic` topic created previously within hello `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="550c6-152">Messages envoyés tooService Bus rubriques sont des instances de la [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="550c6-152">Messages sent tooService Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="550c6-153">[BrokeredMessage][BrokeredMessage]* objets comportent un ensemble de méthodes standard (tels que **setLabel** et **TimeToLive**), un dictionnaire qui est utilisé toohold personnalisé les propriétés spécifiques à l’application et un corps de données d’application arbitraire.</span><span class="sxs-lookup"><span data-stu-id="550c6-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="550c6-154">Une application peut définir le corps du message de hello en passant tout objet sérialisable dans le constructeur hello de la [BrokeredMessage][BrokeredMessage]et hello approprié **DataContractSerializer**  puis sera utilisé tooserialize hello objet.</span><span class="sxs-lookup"><span data-stu-id="550c6-154">An application can set hello body of the message by passing any serializable object into hello constructor of the [BrokeredMessage][BrokeredMessage], and hello appropriate **DataContractSerializer** will then be used tooserialize hello object.</span></span> <span data-ttu-id="550c6-155">Une autre possibilité consiste à fournir un **java.io.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="550c6-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="550c6-156">Hello exemple suivant montre comment les messages de test de toosend cinq toothe `TestTopic` **MessageSender** nous avons obtenu dans l’extrait de code hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="550c6-156">hello following example demonstrates how toosend five test messages toothe `TestTopic` **MessageSender** we obtained in hello code snippet above.</span></span>
<span data-ttu-id="550c6-157">Notez comment hello **MessageNumber** varie en fonction de valeur de la propriété de chaque message sur l’itération hello de boucle de hello (Cela permet de déterminer les abonnements reçoivent) :</span><span class="sxs-lookup"><span data-stu-id="550c6-157">Note how hello **MessageNumber** property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="550c6-158">Rubriques Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="550c6-158">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="550c6-159">en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="550c6-159">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="550c6-160">Il n’existe aucune limite sur le nombre de hello de messages conservés dans une rubrique, mais il existe une limite de taille totale de hello de messages hello détenus par une rubrique.</span><span class="sxs-lookup"><span data-stu-id="550c6-160">There is no limit on hello number of messages held in a topic but there is a limit on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="550c6-161">Cette taille de rubrique est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="550c6-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-subscription"></a><span data-ttu-id="550c6-162">Comment tooreceive les messages à partir d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="550c6-162">How tooreceive messages from a subscription</span></span>
<span data-ttu-id="550c6-163">tooreceive des messages à partir d’un abonnement, utilisez un **ServiceBusContract** objet.</span><span class="sxs-lookup"><span data-stu-id="550c6-163">tooreceive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="550c6-164">Ces messages reçus peuvent fonctionner dans deux modes différents : **ReceiveAndDelete** et **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="550c6-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="550c6-165">Lors de l’utilisation de hello **ReceiveAndDelete** , le mode de réception est une opération coup - autrement dit, lorsque le Service Bus reçoit une demande de lecture d’un message, il marque le message de type hello comme ayant été consommé et le retourne toothe application.</span><span class="sxs-lookup"><span data-stu-id="550c6-165">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks hello message as being consumed and returns it toothe application.</span></span> <span data-ttu-id="550c6-166">**ReceiveAndDelete** mode est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec.</span><span class="sxs-lookup"><span data-stu-id="550c6-166">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="550c6-167">toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter.</span><span class="sxs-lookup"><span data-stu-id="550c6-167">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="550c6-168">Étant donné que le Service Bus sera a marqué le message comme ayant été consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.</span><span class="sxs-lookup"><span data-stu-id="550c6-168">Because Service Bus will have marked the message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="550c6-169">Dans **PeekLock** , le mode de réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants.</span><span class="sxs-lookup"><span data-stu-id="550c6-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="550c6-170">Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="550c6-170">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="550c6-171">Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant **supprimer** sur le message de salutation reçu.</span><span class="sxs-lookup"><span data-stu-id="550c6-171">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="550c6-172">Lorsque le Service Bus voit hello **supprimer** appel, il marque le message de type hello comme ayant été consommé et supprimez-le de la rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="550c6-172">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello topic.</span></span>

<span data-ttu-id="550c6-173">Hello exemple ci-dessous montre comment les messages peuvent être reçus et traités à l’aide de **PeekLock** mode (pas le mode hello par défaut).</span><span class="sxs-lookup"><span data-stu-id="550c6-173">hello example below demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="550c6-174">Hello exemple ci-dessous effectue une boucle et traite les messages hello « HighMessages » abonnement et se termine lorsqu’il n’y a plus aucun message (il peut également être définir toowait pour les nouveaux messages).</span><span class="sxs-lookup"><span data-stu-id="550c6-174">hello example below performs a loop and processes messages in hello "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set toowait for new messages).</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="550c6-175">Comment toohandle application tombe en panne et messages illisibles</span><span class="sxs-lookup"><span data-stu-id="550c6-175">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="550c6-176">Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message.</span><span class="sxs-lookup"><span data-stu-id="550c6-176">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="550c6-177">Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello **unlockMessage** méthode sur le message de salutation reçu (au lieu de hello **deleteMessage** méthode).</span><span class="sxs-lookup"><span data-stu-id="550c6-177">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="550c6-178">Cette opération provoquent le message de type hello toounlock Service Bus au sein de la rubrique de hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.</span><span class="sxs-lookup"><span data-stu-id="550c6-178">This will cause Service Bus toounlock hello message within hello topic and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="550c6-179">Il existe également un délai d’attente d’un message verrouillé dans la rubrique, et si l’application hello échoue le message de type hello tooprocess avant le délai d’attente de verrou expire (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.</span><span class="sxs-lookup"><span data-stu-id="550c6-179">There is also a timeout associated with a message locked within the topic, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="550c6-180">Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello **deleteMessage** demande est émise, puis le message de type hello sera redistribué toohello application lors de son redémarrage.</span><span class="sxs-lookup"><span data-stu-id="550c6-180">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="550c6-181">Cela est souvent appelé **au moins une fois le traitement**, autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué.</span><span class="sxs-lookup"><span data-stu-id="550c6-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="550c6-182">Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message.</span><span class="sxs-lookup"><span data-stu-id="550c6-182">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="550c6-183">Cela est souvent obtenue à l’aide de hello **getMessageId** méthode de message de type hello, qui reste constante entre les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="550c6-183">This is often achieved using hello **getMessageId** method of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="550c6-184">Suppression de rubriques et d'abonnements</span><span class="sxs-lookup"><span data-stu-id="550c6-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="550c6-185">Hello rubriques toodelete de façon principal et d’abonnements est toouse un **ServiceBusContract** objet.</span><span class="sxs-lookup"><span data-stu-id="550c6-185">hello primary way toodelete topics and subscriptions is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="550c6-186">Suppression d’une rubrique supprime également tous les abonnements qui sont inscrits auprès de rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="550c6-186">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="550c6-187">Les abonnements peuvent aussi être supprimés de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="550c6-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="550c6-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="550c6-188">Next Steps</span></span>
<span data-ttu-id="550c6-189">Maintenant que vous avez appris les notions de base de hello de files d’attente Service Bus, consultez [files d’attente Service Bus, rubriques et abonnements] [ Service Bus queues, topics, and subscriptions] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="550c6-189">Now that you've learned hello basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
