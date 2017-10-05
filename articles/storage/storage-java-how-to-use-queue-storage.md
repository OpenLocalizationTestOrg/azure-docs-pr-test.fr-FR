---
title: "Utilisation du stockage de files d’attente à partir de Java | Microsoft Docs"
description: "Découvrez comment utiliser le service de File d'attente Azure pour créer et supprimer des files d'attente, ainsi que pour insérer, récupérer et supprimer des messages. Les exemples sont écrits en Java."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 03faea986221453d1862ff0f0d6d1ec21f92f3bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-java"></a><span data-ttu-id="52c05-104">Utilisation du stockage de files d'attente à partir de Java</span><span class="sxs-lookup"><span data-stu-id="52c05-104">How to use Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="52c05-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="52c05-105">Overview</span></span>
<span data-ttu-id="52c05-106">Ce guide décrit le déroulement de scénarios courants dans le cadre de l'utilisation du service de stockage des files d'attente Azure.</span><span class="sxs-lookup"><span data-stu-id="52c05-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="52c05-107">Les exemples sont écrits en Java et utilisent le [Kit de développement logiciel (SDK) Stockage Azure pour Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="52c05-107">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="52c05-108">Les scénarios traités incluent **l’insertion**, la **lecture furtive**, la **récupération** et la **suppression** des messages de file d’attente, ainsi que la **création** et **suppression** des files d’attente.</span><span class="sxs-lookup"><span data-stu-id="52c05-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="52c05-109">Pour plus d’informations sur les files d’attente, consultez la section [Étapes suivantes](#Next-Steps).</span><span class="sxs-lookup"><span data-stu-id="52c05-109">For more information on queues, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="52c05-110">Remarque : un Kit de développement logiciel (SDK) est disponible pour les développeurs qui utilisent Azure Storage sur des appareils Android.</span><span class="sxs-lookup"><span data-stu-id="52c05-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="52c05-111">Pour plus d’informations, consultez la page [Kit de développement logiciel (SDK) Stockage Azure pour Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="52c05-111">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="52c05-112">Création d’une application Java</span><span class="sxs-lookup"><span data-stu-id="52c05-112">Create a Java application</span></span>
<span data-ttu-id="52c05-113">Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application Java en local, ou dans le code s'exécutant dans un rôle Web ou un rôle de travail dans Azure.</span><span class="sxs-lookup"><span data-stu-id="52c05-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="52c05-114">Pour ce faire, vous devez installer le Kit de développement Java (JDK) et créer un compte Azure Storage dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="52c05-114">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="52c05-115">Vous devez ensuite vérifier que votre système de développement répond à la configuration minimale requise et aux dépendances répertoriées dans le référentiel [Kit de développement logiciel (SDK) Stockage Azure pour Java][Azure Storage SDK for Java] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="52c05-115">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="52c05-116">Si tel est le cas, vous pouvez suivre les instructions relatives au téléchargement et à l'installation des bibliothèques Azure Storage pour Java sur votre système à partir du référentiel.</span><span class="sxs-lookup"><span data-stu-id="52c05-116">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="52c05-117">Une fois ces tâches effectuées, vous pouvez créer une application Java utilisant les exemples de cet article.</span><span class="sxs-lookup"><span data-stu-id="52c05-117">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="52c05-118">Configuration de votre application pour accéder au stockage de files d'attente</span><span class="sxs-lookup"><span data-stu-id="52c05-118">Configure your application to access queue storage</span></span>
<span data-ttu-id="52c05-119">Ajoutez les instructions import suivantes au début du fichier Java dans lequel vous voulez utiliser des API de stockage Azure pour accéder aux files d'attente :</span><span class="sxs-lookup"><span data-stu-id="52c05-119">Add the following import statements to the top of the Java file where you want to use Azure storage APIs to access queues:</span></span>

```java
// Include the following imports to use queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="52c05-120">Configuration d’une chaîne de connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="52c05-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="52c05-121">Un client de stockage Azure utilise une chaîne de connexion de stockage pour stocker des points de terminaison et des informations d’identification permettant d’accéder aux services de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="52c05-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="52c05-122">Lors de l’exécution dans une application cliente, vous devez spécifier la chaîne de connexion au stockage au format suivant, en indiquant le nom de votre compte de stockage et sa clé d’accès primaire, correspondant aux valeurs *AccountName* et *AccountKey*, sur le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="52c05-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="52c05-123">Cet exemple vous montre comment déclarer un champ statique pour qu’il contienne une chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="52c05-123">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="52c05-124">Dans une application exécutée au sein d'un rôle dans Microsoft Azure, cette chaîne peut être stockée dans le fichier de configuration de service *ServiceConfiguration.cscfg*et elle est accessible en appelant la méthode **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="52c05-124">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="52c05-125">Voici un exemple de code vous permettant d'extraire la chaîne de connexion à partir d'un élément **Setting** nommé *StorageConnectionString* dans le fichier de configuration de service :</span><span class="sxs-lookup"><span data-stu-id="52c05-125">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="52c05-126">Les exemples ci-dessous partent du principe que vous avez utilisé l’une de ces deux méthodes pour obtenir la chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="52c05-126">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="52c05-127">Création d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="52c05-127">How to: Create a queue</span></span>
<span data-ttu-id="52c05-128">Un objet **CloudQueueClient** vous permet d'obtenir les objets de référence pour les files d'attente.</span><span class="sxs-lookup"><span data-stu-id="52c05-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="52c05-129">Le code suivant crée un objet **CloudQueueClient** .</span><span class="sxs-lookup"><span data-stu-id="52c05-129">The following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="52c05-130">(Remarque : d’autres méthodes permettent de créer des objets **CloudStorageAccount**. Pour plus d’informations, reportez-vous à la classe **CloudStorageAccount** dans la page [Référence du Kit de développement logiciel (SDK) du client Azure Storage].)</span><span class="sxs-lookup"><span data-stu-id="52c05-130">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="52c05-131">Utilisez l'objet **CloudQueueClient** pour obtenir une référence pointant vers la file d'attente à utiliser.</span><span class="sxs-lookup"><span data-stu-id="52c05-131">Use the **CloudQueueClient** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="52c05-132">Si la file d'attente n'existe pas, vous pouvez la créer :</span><span class="sxs-lookup"><span data-stu-id="52c05-132">You can create the queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create the queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference to a queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create the queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-to-a-queue"></a><span data-ttu-id="52c05-133">Ajout d'un message à une file d'attente</span><span class="sxs-lookup"><span data-stu-id="52c05-133">How to: Add a message to a queue</span></span>
<span data-ttu-id="52c05-134">Pour insérer un message dans une file d'attente existante, commencez par créer un **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="52c05-134">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="52c05-135">Appelez ensuite la méthode **addMessage** .</span><span class="sxs-lookup"><span data-stu-id="52c05-135">Next, call the **addMessage** method.</span></span> <span data-ttu-id="52c05-136">Un **CloudQueueMessage** peut être créé à partir d'une chaîne (au format UTF-8) ou d'un tableau d'octets.</span><span class="sxs-lookup"><span data-stu-id="52c05-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="52c05-137">Voici le code qui crée une file d'attente (si elle n'existe pas) et insère le message « Hello, World ».</span><span class="sxs-lookup"><span data-stu-id="52c05-137">Here is code which creates a queue (if it doesn't exist) and inserts the message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create the queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="52c05-138">Lecture furtive du message suivant</span><span class="sxs-lookup"><span data-stu-id="52c05-138">How to: Peek at the next message</span></span>
<span data-ttu-id="52c05-139">Vous pouvez lire furtivement le message au début de la file d'attente sans l'enlever de la file d'attente en appelant **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="52c05-139">You can peek at the message in the front of a queue without removing it from the queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at the next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output the message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="52c05-140">Modification du contenu d'un message en file d'attente</span><span class="sxs-lookup"><span data-stu-id="52c05-140">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="52c05-141">Vous pouvez modifier le contenu d'un message placé dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="52c05-141">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="52c05-142">Si le message représente une tâche, vous pouvez utiliser cette fonctionnalité pour mettre à jour l'état de la tâche.</span><span class="sxs-lookup"><span data-stu-id="52c05-142">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="52c05-143">Le code suivant met à jour le message de la file d'attente avec un nouveau contenu et ajoute 60 secondes au délai d'expiration de la visibilité.</span><span class="sxs-lookup"><span data-stu-id="52c05-143">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="52c05-144">Cette opération enregistre l'état de la tâche associée au message et accorde une minute supplémentaire au client pour traiter le message.</span><span class="sxs-lookup"><span data-stu-id="52c05-144">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="52c05-145">Vous pouvez utiliser cette technique pour suivre des flux de travail à plusieurs étapes sur les messages de file d'attente, sans devoir reprendre du début si une étape du traitement échoue à cause d'une défaillance matérielle ou logicielle.</span><span class="sxs-lookup"><span data-stu-id="52c05-145">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="52c05-146">Normalement, vous conservez aussi un nombre de nouvelles tentatives et si le message est retenté plus de *n* fois, vous le supprimez.</span><span class="sxs-lookup"><span data-stu-id="52c05-146">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="52c05-147">Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.</span><span class="sxs-lookup"><span data-stu-id="52c05-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="52c05-148">L'exemple de code suivant effectue une recherche dans la file d'attente de messages, recherche le premier message dont le contenu correspond à « Hello, World », modifie le contenu du message, puis se ferme.</span><span class="sxs-lookup"><span data-stu-id="52c05-148">The following code sample searches through the queue of messages, locates the first message that matches "Hello, World" for the content, then modifies the message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // The maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through the messages in the queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify the content of the first matching message.
            message.setMessageContent("Updated contents.");
            // Set it to be visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update the message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="52c05-149">L'exemple de code suivant met simplement à jour le premier message visible dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="52c05-149">Alternatively, the following code sample updates just the first visible message on the queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify the message content.
        message.setMessageContent("Updated contents.");
        // Set it to be visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update the message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="52c05-150">Obtention de la longueur de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="52c05-150">How to: Get the queue length</span></span>
<span data-ttu-id="52c05-151">Vous pouvez obtenir une estimation du nombre de messages dans une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="52c05-151">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="52c05-152">La méthode **downloadAttributes** demande au service de File d'attente plusieurs valeurs actives, y compris le nombre de messages dans une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="52c05-152">The **downloadAttributes** method asks the Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="52c05-153">Ce nombre est approximatif étant donné que des messages peuvent être ajoutés ou supprimés une fois que le service de File d'attente a répondu à votre demande.</span><span class="sxs-lookup"><span data-stu-id="52c05-153">The count is only approximate because messages can be added or removed after the Queue service responds to your request.</span></span> <span data-ttu-id="52c05-154">La méthode **getApproximateMessageCount** renvoie la dernière valeur extraite par l’appel à **downloadAttributes**, sans appeler le service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="52c05-154">The **getApproximateMessageCount** method returns the last value retrieved by the call to **downloadAttributes**, without calling the Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download the approximate message count from the server.
    queue.downloadAttributes();

    // Retrieve the newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display the queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="52c05-155">Procédure : Suppression du message suivant dans la file d’attente</span><span class="sxs-lookup"><span data-stu-id="52c05-155">How to: Dequeue the next message</span></span>
<span data-ttu-id="52c05-156">Votre code enlève un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="52c05-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="52c05-157">Lorsque vous appelez **retrieveMessage**, vous obtenez le message suivant dans une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="52c05-157">When you call **retrieveMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="52c05-158">Un message renvoyé par **retrieveMessage** devient invisible de tout autre code lisant les messages de cette file d'attente.</span><span class="sxs-lookup"><span data-stu-id="52c05-158">A message returned from **retrieveMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="52c05-159">Par défaut, ce message reste invisible pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="52c05-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="52c05-160">Pour finaliser la suppression du message de la file d'attente, vous devez aussi appeler **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="52c05-160">To finish removing the message from the queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="52c05-161">Ce processus de suppression d'un message en deux étapes garantit que, si votre code ne parvient pas à traiter un message à cause d'une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et réessayer.</span><span class="sxs-lookup"><span data-stu-id="52c05-161">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="52c05-162">Votre code appelle **deleteMessage** juste après le traitement du message.</span><span class="sxs-lookup"><span data-stu-id="52c05-162">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process the message in less than 30 seconds, and then delete the message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="52c05-163">Options supplémentaires pour la suppression des messages dans la file d'attente</span><span class="sxs-lookup"><span data-stu-id="52c05-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="52c05-164">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="52c05-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="52c05-165">Premièrement, vous pouvez obtenir un lot de messages (jusqu'à 32).</span><span class="sxs-lookup"><span data-stu-id="52c05-165">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="52c05-166">Deuxièmement, vous pouvez définir un délai d'expiration de l'invisibilité plus long ou plus court afin d'accorder à votre code plus ou moins de temps pour traiter complètement chaque message.</span><span class="sxs-lookup"><span data-stu-id="52c05-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="52c05-167">L'exemple de code suivant utilise la méthode **retrieveMessages** pour obtenir 20 messages en un appel.</span><span class="sxs-lookup"><span data-stu-id="52c05-167">The following code example uses the **retrieveMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="52c05-168">Ensuite, il traite chaque message à l'aide d'une boucle **for** .</span><span class="sxs-lookup"><span data-stu-id="52c05-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="52c05-169">Il définit également le délai d'expiration de l'invisibilité sur cinq minutes (300 secondes) pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="52c05-169">It also sets the invisibility timeout to five minutes (300 seconds) for each message.</span></span> <span data-ttu-id="52c05-170">Notez que le délai de cinq minutes démarre en même temps pour tous les messages, donc une fois les cinq minutes écoulées après l'appel de **retrieveMessages**, tous les messages n'ayant pas été supprimés redeviennent visibles.</span><span class="sxs-lookup"><span data-stu-id="52c05-170">Note that the five minutes starts for all messages at the same time, so when five minutes have passed since the call to **retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-queues"></a><span data-ttu-id="52c05-171">Procédure : Obtention de la liste des files d’attente</span><span class="sxs-lookup"><span data-stu-id="52c05-171">How to: List the queues</span></span>
<span data-ttu-id="52c05-172">Pour obtenir la liste des files d’attente en cours, appelez la méthode **CloudQueueClient.listQueues()**, qui renvoie une collection d’objets **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="52c05-172">To obtain a list of the current queues, call the **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through the collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="52c05-173">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="52c05-173">How to: Delete a queue</span></span>
<span data-ttu-id="52c05-174">Pour supprimer une file d’attente et tous les messages qu’elle contient, appelez la méthode **deleteIfExists** sur l’objet **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="52c05-174">To delete a queue and all the messages contained in it, call the **deleteIfExists** method on the **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete the queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="52c05-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52c05-175">Next steps</span></span>
<span data-ttu-id="52c05-176">Maintenant que vous connaissez les bases du stockage des files d'attente, consultez les liens suivants pour apprendre à exécuter les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="52c05-176">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="52c05-177">[Kit de développement logiciel (SDK) Stockage Azure pour Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="52c05-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="52c05-178">[Référence du Kit de développement logiciel (SDK) du client Azure Storage][Référence du Kit de développement logiciel (SDK) du client Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="52c05-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="52c05-179">[API REST services Stockage Azure][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="52c05-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="52c05-180">[Blog de l’équipe Stockage Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="52c05-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="52c05-181">[Référence du Kit de développement logiciel (SDK) du client Azure Storage]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="52c05-181">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
