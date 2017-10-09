---
title: aaaHow toouse Azure Service Bus avec hello WebJobs SDK
description: "Découvrez comment les files d’attente du Bus des services Azure toouse et des rubriques avec hello WebJobs SDK."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a><span data-ttu-id="71e22-103">Comment toouse Azure Service Bus avec hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="71e22-103">How toouse Azure Service Bus with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="71e22-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="71e22-104">Overview</span></span>
<span data-ttu-id="71e22-105">Ce guide fournit des c# des exemples de code qui montrent comment tootrigger un processus lors de la réception d’un message d’Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="71e22-105">This guide provides C# code samples that show how tootrigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="71e22-106">utilisation des exemples de code de Hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="71e22-106">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="71e22-107">guide de Hello suppose que vous connaissez [comment toocreate un projet de la tâche Web dans Visual Studio avec connexion chaînes ce compte de stockage point tooyour](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="71e22-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="71e22-108">extraits de code Hello affichent uniquement les fonctions, ne Hello pas de code qui crée hello `JobHost` objet comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="71e22-108">hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

<span data-ttu-id="71e22-109">A [exemple de code complet Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) est dans le référentiel de tâches Web azure-exemples sdk hello sur GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="71e22-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in hello azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="71e22-110"><a id="prerequisites"></a> Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="71e22-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="71e22-111">toowork avec Service Bus vous avez tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package en outre toohello autres packages WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="71e22-111">toowork with Service Bus you have tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition toohello other WebJobs SDK packages.</span></span> 

<span data-ttu-id="71e22-112">Vous avez également la chaîne de connexion AzureWebJobsServiceBus tooset hello dans les chaînes de connexion de stockage toohello Ajout.</span><span class="sxs-lookup"><span data-stu-id="71e22-112">You also have tooset hello AzureWebJobsServiceBus connection string in addition toohello storage connection strings.</span></span>  <span data-ttu-id="71e22-113">Cela Bonjour `connectionStrings` section du fichier App.config de hello, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="71e22-113">You can do this in hello `connectionStrings` section of hello App.config file, as shown in hello following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="71e22-114">Pour un exemple de projet qui inclut un paramètre de chaîne de connexion de Service Bus hello dans le fichier App.config hello, consultez [exemple de Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="71e22-114">For a sample project that includes hello Service Bus connection string setting in hello App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="71e22-115">chaînes de connexion Hello peuvent également être définies dans l’environnement d’exécution Azure hello, qui remplace ensuite les paramètres App.config hello lorsque hello la tâche Web s’exécute dans Azure. Pour plus d’informations, consultez [prise en main hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="71e22-115">hello connection strings can also be set in hello Azure runtime environment, which then overrides hello App.config settings when hello WebJob runs in Azure; for more information, see [Get Started with hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="71e22-116"><a id="trigger"></a>Comment tootrigger une fonction quand un Bus de Service de file d’attente de message est reçu</span><span class="sxs-lookup"><span data-stu-id="71e22-116"><a id="trigger"></a> How tootrigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="71e22-117">toowrite une fonction qui hello WebJobs SDK appelle lors de la réception d’un message de la file d’attente, utilisez hello `ServiceBusTrigger` attribut.</span><span class="sxs-lookup"><span data-stu-id="71e22-117">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="71e22-118">constructeur d’attribut Hello prend un paramètre qui spécifie le nom hello de toopoll de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="71e22-118">hello attribute constructor takes a parameter that specifies hello name of hello queue toopoll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="71e22-119">Fonctionnement de ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="71e22-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="71e22-120">Kit de développement logiciel Hello reçoit un message dans `PeekLock` mode et les appels `Complete` sur le message de type hello si hello est terminée avec succès, ou des appels `Abandon` si hello fonction échoue.</span><span class="sxs-lookup"><span data-stu-id="71e22-120">hello SDK receives a message in `PeekLock` mode and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> <span data-ttu-id="71e22-121">Si la fonction hello s’exécute plus longtemps que hello `PeekLock` délai d’attente, les verrous hello est automatiquement renouvelée.</span><span class="sxs-lookup"><span data-stu-id="71e22-121">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<span data-ttu-id="71e22-122">Bus de service effectue sa propre gestion de la file d’attente de messages incohérents qui ne peut pas être contrôlée ou configurée par hello WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="71e22-122">Service Bus does its own poison queue handling which cannot be controlled or configured by hello WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="71e22-123">Message de file d’attente de chaîne</span><span class="sxs-lookup"><span data-stu-id="71e22-123">String queue message</span></span>
<span data-ttu-id="71e22-124">Hello exemple de code suivant lit un message de la file d’attente qui contient une chaîne et écrit la chaîne de hello toohello du tableau de bord WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="71e22-124">hello following code sample reads a queue message that contains a string and writes hello string toohello WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="71e22-125">**Remarque :** si vous créez hello messages de la file d’attente dans une application qui n’utilise pas hello WebJobs SDK, assurez-vous que tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) trop « text/plain ».</span><span class="sxs-lookup"><span data-stu-id="71e22-125">**Note:** If you are creating hello queue messages in an application that doesn't use hello WebJobs SDK, make sure tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) too"text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="71e22-126">Message de file d’attente POCO</span><span class="sxs-lookup"><span data-stu-id="71e22-126">POCO queue message</span></span>
<span data-ttu-id="71e22-127">Hello SDK désérialise automatiquement un message de la file d’attente contenant du texte JSON pour un POCO [(objet CLR simple](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span><span class="sxs-lookup"><span data-stu-id="71e22-127">hello SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="71e22-128">Hello exemple de code suivant lit un message de la file d’attente qui contient un `BlobInformation` objet qui a un `BlobName` propriété :</span><span class="sxs-lookup"><span data-stu-id="71e22-128">hello following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="71e22-129">Pour obtenir des exemples de code montrant comment les propriétés de toouse de toowork POCO hello avec les objets BLOB et tables dans hello même fonction, consultez hello [version de files d’attente de stockage de cet article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="71e22-129">For code samples showing how toouse properties of hello POCO toowork with blobs and tables in hello same function, see hello [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="71e22-130">Si votre code qui crée le message de file d’attente hello n’utilise pas hello WebJobs SDK, utilisez toohello similaire de code exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="71e22-130">If your code that creates hello queue message doesn't use hello WebJobs SDK, use code similar toohello following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="71e22-131">Types utilisés par ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="71e22-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="71e22-132">En outre `string` et types POCO, vous pouvez utiliser hello `ServiceBusTrigger` attribut avec un tableau d’octets ou un `BrokeredMessage` objet.</span><span class="sxs-lookup"><span data-stu-id="71e22-132">Besides `string` and POCO  types, you can use hello `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="71e22-133"><a id="create"></a>Comment toocreate Bus de Service de file d’attente des messages</span><span class="sxs-lookup"><span data-stu-id="71e22-133"><a id="create"></a> How toocreate Service Bus queue messages</span></span>
<span data-ttu-id="71e22-134">une fonction qui crée un nouveau message de file d’attente de toowrite utiliser hello `ServiceBus` d’attribut et passez dans le constructeur d’attribut toohello nom hello file d’attente.</span><span class="sxs-lookup"><span data-stu-id="71e22-134">toowrite a function that creates a new queue message use hello `ServiceBus` attribute and pass in hello queue name toohello attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="71e22-135">Création d’un message de file d’attente unique dans une fonction non asynchrone</span><span class="sxs-lookup"><span data-stu-id="71e22-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="71e22-136">Hello suivant l’exemple de code utilise un toocreate de paramètre de sortie un nouveau message dans la file d’attente hello nommé « outputqueue » avec hello même contenu en tant que hello message reçu dans la file d’attente hello nommé « inputqueue ».</span><span class="sxs-lookup"><span data-stu-id="71e22-136">hello following code sample uses an output parameter toocreate a new message in hello queue named "outputqueue" with hello same content as hello message received in hello queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="71e22-137">le paramètre de sortie Hello pour la création d’un message de la file d’attente unique peut être un des types suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="71e22-137">hello output parameter for creating a single queue message can be any of hello following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="71e22-138">Type POCO sérialisable que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="71e22-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="71e22-139">Sérialisé automatiquement au format JSON.</span><span class="sxs-lookup"><span data-stu-id="71e22-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="71e22-140">Pour les paramètres de type POCO, un message de la file d’attente est toujours créé lors de la fonction hello se termine. Si le paramètre hello est null, hello SDK crée un message de la file d’attente qui retourne la valeur null lorsque le message de type hello est reçu et désérialisé.</span><span class="sxs-lookup"><span data-stu-id="71e22-140">For POCO type parameters, a queue message is always created when hello function ends; if hello parameter is null, hello SDK creates a queue message that will return null when hello message is received and deserialized.</span></span> <span data-ttu-id="71e22-141">Pour hello autres types, si le paramètre hello est null aucun message de la file d’attente n’est créée.</span><span class="sxs-lookup"><span data-stu-id="71e22-141">For hello other types, if hello parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="71e22-142">Création de plusieurs messages de file d’attente dans des fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="71e22-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="71e22-143">toocreate plusieurs messages, utilisez hello `ServiceBus` d’attribut avec `ICollector<T>` ou `IAsyncCollector<T>`, comme indiqué dans hello suivant l’exemple de code :</span><span class="sxs-lookup"><span data-stu-id="71e22-143">toocreate multiple messages, use  hello `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="71e22-144">Chaque message de la file d’attente est créée immédiatement lorsque hello `Add` méthode est appelée.</span><span class="sxs-lookup"><span data-stu-id="71e22-144">Each queue message is created immediately when hello `Add` method is called.</span></span>

## <span data-ttu-id="71e22-145"><a id="topics"></a>Comment toowork avec des rubriques Service Bus</span><span class="sxs-lookup"><span data-stu-id="71e22-145"><a id="topics"></a>How toowork with Service Bus topics</span></span>
<span data-ttu-id="71e22-146">toowrite une fonction qui hello du Kit de développement appelle lorsqu’un message est reçu sur une rubrique Service Bus, utilisez hello `ServiceBusTrigger` attribut avec constructeur hello qui prend le nom de la rubrique et le nom d’abonnement, comme indiqué dans hello suivant l’exemple de code :</span><span class="sxs-lookup"><span data-stu-id="71e22-146">toowrite a function that hello SDK calls when a message is received on a Service Bus topic, use hello `ServiceBusTrigger` attribute with hello constructor that takes topic name and subscription name, as shown in hello following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="71e22-147">toocreate un message à une rubrique, utilisez hello `ServiceBus` d’attribut avec un Bonjour de nom de rubrique même façon que vous l’utilisez avec un nom de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="71e22-147">toocreate a message on a topic, use hello `ServiceBus` attribute with a topic name hello same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="71e22-148">Fonctionnalités ajoutées dans la version 1.1</span><span class="sxs-lookup"><span data-stu-id="71e22-148">Features added in release 1.1</span></span>
<span data-ttu-id="71e22-149">Hello suivant les fonctionnalités ont été ajoutée dans la version 1.1 :</span><span class="sxs-lookup"><span data-stu-id="71e22-149">hello following features were added in release 1.1:</span></span>

* <span data-ttu-id="71e22-150">Autoriser la personnalisation complète du traitement des messages via `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="71e22-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="71e22-151">`MessagingProvider`prend en charge la personnalisation de hello Service Bus `MessagingFactory` et `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="71e22-151">`MessagingProvider` supports customization of hello Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="71e22-152">A `MessageProcessor` modèle de stratégie vous permet de toospecify un processeur par file d’attente/rubrique.</span><span class="sxs-lookup"><span data-stu-id="71e22-152">A `MessageProcessor` strategy pattern allows you toospecify a processor per queue/topic.</span></span>
* <span data-ttu-id="71e22-153">L'accès concurrentiel de traitement des message est pris en charge par défaut.</span><span class="sxs-lookup"><span data-stu-id="71e22-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="71e22-154">Personnalisation facile de `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="71e22-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="71e22-155">Autoriser [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe spécifié sur `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (pour les scénarios où vous ne disposez pas gérer les droits).</span><span class="sxs-lookup"><span data-stu-id="71e22-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="71e22-156">Notez que les tâches Web Azure est files d’attente d’inexistant tooautomatically Impossible de configurer et de rubriques sans AccessRights de gérer.</span><span class="sxs-lookup"><span data-stu-id="71e22-156">Note that Azure WebJobs is unable tooautomatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="71e22-157"><a id="queues"></a>Rubriques connexes couvertes par les files d’attente de stockage hello procédure-tooarticle</span><span class="sxs-lookup"><span data-stu-id="71e22-157"><a id="queues"></a>Related topics covered by hello storage queues how-tooarticle</span></span>
<span data-ttu-id="71e22-158">Pour plus d’informations sur les scénarios de WebJobs SDK tooService non spécifique des Bus, consultez [comment toouse Azure file d’attente de stockage avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="71e22-158">For information about WebJobs SDK scenarios not specific tooService Bus, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="71e22-159">Les sujets abordés dans cet article hello suivants :</span><span class="sxs-lookup"><span data-stu-id="71e22-159">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="71e22-160">Fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="71e22-160">Async functions</span></span>
* <span data-ttu-id="71e22-161">Instances multiples</span><span class="sxs-lookup"><span data-stu-id="71e22-161">Multiple instances</span></span>
* <span data-ttu-id="71e22-162">Arrêt approprié</span><span class="sxs-lookup"><span data-stu-id="71e22-162">Graceful shutdown</span></span>
* <span data-ttu-id="71e22-163">Utiliser les attributs de WebJobs SDK dans le corps d’une fonction de hello</span><span class="sxs-lookup"><span data-stu-id="71e22-163">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="71e22-164">Définir des chaînes de connexion du Kit de développement logiciel hello dans le code</span><span class="sxs-lookup"><span data-stu-id="71e22-164">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="71e22-165">Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code</span><span class="sxs-lookup"><span data-stu-id="71e22-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="71e22-166">Déclenchement manuel d’une fonction</span><span class="sxs-lookup"><span data-stu-id="71e22-166">Trigger a function manually</span></span>
* <span data-ttu-id="71e22-167">Écriture de journaux</span><span class="sxs-lookup"><span data-stu-id="71e22-167">Write logs</span></span>

## <span data-ttu-id="71e22-168"><a id="nextsteps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71e22-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="71e22-169">Ce guide a fourni le code des exemples qui montrent comment toohandle des scénarios courants pour l’utilisation avec Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="71e22-169">This guide has provided code samples that show how toohandle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="71e22-170">Pour plus d’informations sur la façon dont toouse tâches Web Azure et hello WebJobs SDK, consultez [Azure WebJobs recommandé de ressources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="71e22-170">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

