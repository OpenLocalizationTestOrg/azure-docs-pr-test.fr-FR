---
title: "Utilisation de Microsoft Azure Service Bus avec le Kit de développement logiciel (SDK) WebJobs"
description: "Apprenez à utiliser les files d’attente et les rubriques Azure Service Bus avec le Kit de développement logiciel (SDK) WebJobs."
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
ms.openlocfilehash: 7cec03cae5d20d1ead9eb24e99415c33d8b76f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a><span data-ttu-id="d4a2f-103">Utilisation de Microsoft Azure Service Bus avec le Kit de développement logiciel (SDK) WebJobs</span><span class="sxs-lookup"><span data-stu-id="d4a2f-103">How to use Azure Service Bus with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="d4a2f-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="d4a2f-104">Overview</span></span>
<span data-ttu-id="d4a2f-105">Ce guide fournit des exemples de code c# qui montrent comment déclencher un processus lors de la réception d’un message Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-105">This guide provides C# code samples that show how to trigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="d4a2f-106">Les exemples de code utilisent le [Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-106">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="d4a2f-107">Ce guide suppose que vous savez [comment créer un projet WebJob dans Visual Studio avec des chaînes de connexion qui pointent vers votre compte de stockage](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d4a2f-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="d4a2f-108">Les extraits de code présentent uniquement les fonctions, et non le code chargé de créer l’objet `JobHost` comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="d4a2f-108">The code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="d4a2f-109">Le référentiel azure-webjobs-sdk-samples sur GitHub.com contient un [exemple de code complet Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) .</span><span class="sxs-lookup"><span data-stu-id="d4a2f-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in the azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="d4a2f-110"><a id="prerequisites"></a> Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="d4a2f-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="d4a2f-111">Pour utiliser Service Bus, vous devez installer le package NuGet [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) en plus des autres packages du Kit de développement logiciel (SDK) WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-111">To work with Service Bus you have to install the [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition to the other WebJobs SDK packages.</span></span> 

<span data-ttu-id="d4a2f-112">Vous devez aussi définir la chaîne de connexion AzureWebJobsServiceBus en plus des chaînes de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-112">You also have to set the AzureWebJobsServiceBus connection string in addition to the storage connection strings.</span></span>  <span data-ttu-id="d4a2f-113">Pour cela, vous pouvez utiliser la section `connectionStrings` du fichier App.config, comme illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d4a2f-113">You can do this in the `connectionStrings` section of the App.config file, as shown in the following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="d4a2f-114">Pour un exemple de projet incluant la valeur de la chaîne de connexion de Service Bus dans le fichier App.config, consultez [Exemple de Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="d4a2f-114">For a sample project that includes the Service Bus connection string setting in the App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="d4a2f-115">Les chaînes de connexion peuvent également être définies dans l’environnement d’exécution Azure, qui remplace ensuite les valeurs de App.config quand la tâche web s’exécute dans Azure. Pour plus d’informations, consultez [Prise en main du SDK WebJobs](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d4a2f-115">The connection strings can also be set in the Azure runtime environment, which then overrides the App.config settings when the WebJob runs in Azure; for more information, see [Get Started with the WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="d4a2f-116"><a id="trigger"></a> Déclenchement d’une fonction durant la réception d’un message en file d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="d4a2f-116"><a id="trigger"></a> How to trigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="d4a2f-117">Pour écrire une fonction que le Kit de développement logiciel (SDK) WebJobs appelle durant la réception d’un message en file d’attente, utilisez l’attribut `ServiceBusTrigger` .</span><span class="sxs-lookup"><span data-stu-id="d4a2f-117">To write a function that the WebJobs SDK calls when a queue message is received, use the `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="d4a2f-118">Le constructeur d’attribut prend un paramètre qui spécifie le nom de la file d’attente à interroger.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-118">The attribute constructor takes a parameter that specifies the name of the queue to poll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="d4a2f-119">Fonctionnement de ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="d4a2f-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="d4a2f-120">Le Kit de développement logiciel (SDK) reçoit un message en mode `PeekLock` et appelle l’élément `Complete` sur le message si la fonction se termine correctement. Si la fonction échoue, il appelle l’élément `Abandon`.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-120">The SDK receives a message in `PeekLock` mode and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> <span data-ttu-id="d4a2f-121">Si la fonction s’exécute au-delà du délai imparti à `PeekLock`, le verrou est automatiquement renouvelé.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-121">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<span data-ttu-id="d4a2f-122">Service Bus effectue sa propre gestion de la file d’attente de messages incohérents, qui ne peut pas être contrôlée ou configurée par le Kit de développement logiciel (SDK) WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-122">Service Bus does its own poison queue handling which cannot be controlled or configured by the WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="d4a2f-123">Message de file d’attente de chaîne</span><span class="sxs-lookup"><span data-stu-id="d4a2f-123">String queue message</span></span>
<span data-ttu-id="d4a2f-124">L’exemple de code suivant lit un message de file d’attente qui contient une chaîne qu’il écrit dans le tableau de bord du Kit de développement logiciel (SDK) WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-124">The following code sample reads a queue message that contains a string and writes the string to the WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="d4a2f-125">**Remarque :** si vous créez les messages en file d’attente dans une application qui n’utilise pas le Kit de développement logiciel (SDK) WebJobs, veillez à attribuer au paramètre [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) la valeur « text/plain ».</span><span class="sxs-lookup"><span data-stu-id="d4a2f-125">**Note:** If you are creating the queue messages in an application that doesn't use the WebJobs SDK, make sure to set [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) to "text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="d4a2f-126">Message de file d’attente POCO</span><span class="sxs-lookup"><span data-stu-id="d4a2f-126">POCO queue message</span></span>
<span data-ttu-id="d4a2f-127">Le Kit de développement logiciel (SDK) désérialise automatiquement un message en file d’attente qui contient JSON pour un type d’objet POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)).</span><span class="sxs-lookup"><span data-stu-id="d4a2f-127">The SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="d4a2f-128">L’exemple de code suivant lit un message en file d’attente qui contient un objet `BlobInformation` doté d’une propriété `BlobName` :</span><span class="sxs-lookup"><span data-stu-id="d4a2f-128">The following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="d4a2f-129">Pour obtenir des exemples de code montrant comment utiliser les propriétés de l’objet POCO de façon à les rendre compatibles avec les objets blob et les tables contenus d’une même fonction, consultez la [version de cet article qui traite des files d’attente de stockage](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="d4a2f-129">For code samples showing how to use properties of the POCO to work with blobs and tables in the same function, see the [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="d4a2f-130">Si votre code qui crée le message de la file d'attente n'utilise pas le SDK WebJobs, utilisez du code similaire à l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d4a2f-130">If your code that creates the queue message doesn't use the WebJobs SDK, use code similar to the following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="d4a2f-131">Types utilisés par ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="d4a2f-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="d4a2f-132">Outre les types d’objet POCO et `string`, vous pouvez utiliser l’attribut `ServiceBusTrigger` avec un tableau d’octets ou un objet `BrokeredMessage`.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-132">Besides `string` and POCO  types, you can use the `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="d4a2f-133"><a id="create"></a> Création de messages de file d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="d4a2f-133"><a id="create"></a> How to create Service Bus queue messages</span></span>
<span data-ttu-id="d4a2f-134">Pour écrire une fonction qui crée un message de file d’attente, utilisez l’attribut `ServiceBus` et transmettez le nom de la file d’attente au constructeur d’attribut.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-134">To write a function that creates a new queue message use the `ServiceBus` attribute and pass in the queue name to the attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="d4a2f-135">Création d’un message de file d’attente unique dans une fonction non asynchrone</span><span class="sxs-lookup"><span data-stu-id="d4a2f-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="d4a2f-136">L’exemple de code suivant utilise un paramètre de sortie pour créer un message dans la file d’attente « outputqueue » avec le même contenu que le message reçu dans la file d’attente « inputqueue ».</span><span class="sxs-lookup"><span data-stu-id="d4a2f-136">The following code sample uses an output parameter to create a new message in the queue named "outputqueue" with the same content as the message received in the queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="d4a2f-137">Le paramètre de sortie utilisé pour créer un message de file d’attente unique peut être de l’un des types suivants :</span><span class="sxs-lookup"><span data-stu-id="d4a2f-137">The output parameter for creating a single queue message can be any of the following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="d4a2f-138">Type POCO sérialisable que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="d4a2f-139">Sérialisé automatiquement au format JSON.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="d4a2f-140">Pour les paramètres de type POCO, un message de file d’attente est toujours créé au moment où la fonction se termine ; si le paramètre a la valeur null, le Kit de développement logiciel (SDK) crée un message de file d’attente qui retourne la valeur null quand le message est reçu et désérialisé.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-140">For POCO type parameters, a queue message is always created when the function ends; if the parameter is null, the SDK creates a queue message that will return null when the message is received and deserialized.</span></span> <span data-ttu-id="d4a2f-141">Pour les autres types, si le paramètre a la valeur null, aucun message de file d’attente n’est créé.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-141">For the other types, if the parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="d4a2f-142">Création de plusieurs messages de file d’attente dans des fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="d4a2f-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="d4a2f-143">Pour créer plusieurs messages, utilisez l’attribut `ServiceBus` avec `ICollector<T>` ou `IAsyncCollector<T>`, comme illustré dans l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="d4a2f-143">To create multiple messages, use  the `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="d4a2f-144">Chaque message de file d’attente est créé immédiatement après l’appel de la méthode `Add` .</span><span class="sxs-lookup"><span data-stu-id="d4a2f-144">Each queue message is created immediately when the `Add` method is called.</span></span>

## <span data-ttu-id="d4a2f-145"><a id="topics"></a>Utilisation des rubriques Service Bus</span><span class="sxs-lookup"><span data-stu-id="d4a2f-145"><a id="topics"></a>How to work with Service Bus topics</span></span>
<span data-ttu-id="d4a2f-146">Pour écrire une fonction que le Kit de développement logiciel (SDK) appelle au moment où un message est reçu sur une rubrique Service Bus, utilisez l’attribut `ServiceBusTrigger` avec le constructeur qui prend le nom de rubrique et le nom d’abonnement, comme illustré dans l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="d4a2f-146">To write a function that the SDK calls when a message is received on a Service Bus topic, use the `ServiceBusTrigger` attribute with the constructor that takes topic name and subscription name, as shown in the following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="d4a2f-147">Pour créer un message sur une rubrique, utilisez l’attribut `ServiceBus` avec un nom de rubrique, comme vous le faites avec un nom de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-147">To create a message on a topic, use the `ServiceBus` attribute with a topic name the same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="d4a2f-148">Fonctionnalités ajoutées dans la version 1.1</span><span class="sxs-lookup"><span data-stu-id="d4a2f-148">Features added in release 1.1</span></span>
<span data-ttu-id="d4a2f-149">Les fonctionnalités suivantes ont été ajoutées dans la version 1.1 :</span><span class="sxs-lookup"><span data-stu-id="d4a2f-149">The following features were added in release 1.1:</span></span>

* <span data-ttu-id="d4a2f-150">Autoriser la personnalisation complète du traitement des messages via `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="d4a2f-151">`MessagingProvider` prend en charge la personnalisation de `MessagingFactory` et `NamespaceManager` de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-151">`MessagingProvider` supports customization of the Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="d4a2f-152">Un modèle de stratégie `MessageProcessor` vous permet de spécifier un processeur par file d'attente/rubrique.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-152">A `MessageProcessor` strategy pattern allows you to specify a processor per queue/topic.</span></span>
* <span data-ttu-id="d4a2f-153">L'accès concurrentiel de traitement des message est pris en charge par défaut.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="d4a2f-154">Personnalisation facile de `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="d4a2f-155">Autoriser la spécification des [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) sur `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (pour les scénarios où vous ne disposez pas des droits de gestion).</span><span class="sxs-lookup"><span data-stu-id="d4a2f-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) to be specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="d4a2f-156">Notez qu’Azure WebJobs ne peut pas configurer automatiquement des files d’attente et des rubriques inexistantes sans gérer les droits d’accès.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-156">Note that Azure WebJobs is unable to automatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="d4a2f-157"><a id="queues"></a>Sujets connexes traités dans l’article de procédure relatif aux files d’attente de stockage</span><span class="sxs-lookup"><span data-stu-id="d4a2f-157"><a id="queues"></a>Related topics covered by the storage queues how-to article</span></span>
<span data-ttu-id="d4a2f-158">Pour en savoir plus sur les scénarios de Kit de développement logiciel (SDK) WebJobs non spécifiques de Service Bus, voir [Utilisation du stockage de file d’attente Azure avec le Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="d4a2f-158">For information about WebJobs SDK scenarios not specific to Service Bus, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="d4a2f-159">Les sujets abordés dans cet article sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="d4a2f-159">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="d4a2f-160">Fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="d4a2f-160">Async functions</span></span>
* <span data-ttu-id="d4a2f-161">Instances multiples</span><span class="sxs-lookup"><span data-stu-id="d4a2f-161">Multiple instances</span></span>
* <span data-ttu-id="d4a2f-162">Arrêt approprié</span><span class="sxs-lookup"><span data-stu-id="d4a2f-162">Graceful shutdown</span></span>
* <span data-ttu-id="d4a2f-163">Utilisation des attributs du Kit de développement logiciel (SDK) WebJobs dans le corps d’une fonction</span><span class="sxs-lookup"><span data-stu-id="d4a2f-163">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="d4a2f-164">Définition des chaînes de connexion du SDK dans le code</span><span class="sxs-lookup"><span data-stu-id="d4a2f-164">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="d4a2f-165">Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code</span><span class="sxs-lookup"><span data-stu-id="d4a2f-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="d4a2f-166">Déclenchement manuel d’une fonction</span><span class="sxs-lookup"><span data-stu-id="d4a2f-166">Trigger a function manually</span></span>
* <span data-ttu-id="d4a2f-167">Écriture de journaux</span><span class="sxs-lookup"><span data-stu-id="d4a2f-167">Write logs</span></span>

## <span data-ttu-id="d4a2f-168"><a id="nextsteps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4a2f-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="d4a2f-169">Ce guide fournit des exemples de code qui indiquent comment gérer des scénarios courants pour l’utilisation d’Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d4a2f-169">This guide has provided code samples that show how to handle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="d4a2f-170">Pour plus d’informations sur l’utilisation d’Azure Webjobs et du Kit de développement logiciel (SDK) WebJobs Azure, consultez la rubrique [Azure Webjobs - Ressources recommandées](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="d4a2f-170">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

