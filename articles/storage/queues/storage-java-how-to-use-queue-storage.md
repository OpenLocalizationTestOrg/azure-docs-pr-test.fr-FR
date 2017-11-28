---
title: "aaaHow toouse stockage de file d’attente à partir de Java | Documents Microsoft"
description: "Découvrez comment toouse hello file d’attente Azure service toocreate et les files d’attente de suppression, insertion, obtenir et supprimer les messages. Les exemples sont écrits en Java."
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
ms.openlocfilehash: 297f89c9d21a38d2b4a5f4346f66f59f9d487010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a><span data-ttu-id="f9822-104">Comment toouse stockage de file d’attente à partir de Java</span><span class="sxs-lookup"><span data-stu-id="f9822-104">How toouse Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="f9822-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f9822-105">Overview</span></span>
<span data-ttu-id="f9822-106">Ce guide vous explique comment tooperform des scénarios courants utilisant hello service de stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="f9822-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="f9822-107">exemples de Hello sont écrits en Java et utiliser hello [SDK de stockage Azure pour Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="f9822-107">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="f9822-108">Hello scénarios abordés incluent **insertion**, **lecture**, **mise en route**, et **suppression** file d’attente de messages, ainsi que  **Création** et **suppression** les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="f9822-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="f9822-109">Pour plus d’informations sur les files d’attente, consultez hello [étapes](#Next-Steps) section.</span><span class="sxs-lookup"><span data-stu-id="f9822-109">For more information on queues, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="f9822-110">Remarque : un Kit de développement logiciel (SDK) est disponible pour les développeurs qui utilisent Azure Storage sur des appareils Android.</span><span class="sxs-lookup"><span data-stu-id="f9822-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="f9822-111">Pour plus d’informations, consultez hello [stockage de Azure SDK pour Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="f9822-111">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="f9822-112">Création d’une application Java</span><span class="sxs-lookup"><span data-stu-id="f9822-112">Create a Java application</span></span>
<span data-ttu-id="f9822-113">Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application Java en local, ou dans le code s'exécutant dans un rôle Web ou un rôle de travail dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f9822-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="f9822-114">toodo par conséquent, vous devez tooinstall hello du Kit de développement Java (JDK) et créer un compte de stockage Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f9822-114">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="f9822-115">Une fois que vous l’avez fait, vous devez tooverify votre système de développement répond aux exigences minimales de hello et les dépendances qui sont répertoriées dans hello [SDK de stockage Azure pour Java] [ Azure Storage SDK for Java] référentiel sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="f9822-115">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="f9822-116">Si votre système répond à ces exigences, vous pouvez suivre les instructions de hello pour télécharger et installer les bibliothèques de stockage Azure hello pour Java sur votre système à partir de ce référentiel.</span><span class="sxs-lookup"><span data-stu-id="f9822-116">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="f9822-117">Une fois ces tâches terminées, vous serez en mesure de toocreate une application Java qui utilise des exemples de hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f9822-117">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="f9822-118">Configurer votre stockage de file d’attente d’application tooaccess</span><span class="sxs-lookup"><span data-stu-id="f9822-118">Configure your application tooaccess queue storage</span></span>
<span data-ttu-id="f9822-119">Ajoutez hello après importation instructions toohello en haut de hello Java fichier dans lequel les files d’attente de toouse stockage Azure API tooaccess :</span><span class="sxs-lookup"><span data-stu-id="f9822-119">Add hello following import statements toohello top of hello Java file where you want toouse Azure storage APIs tooaccess queues:</span></span>

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="f9822-120">Configuration d’une chaîne de connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="f9822-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="f9822-121">Un client de stockage Azure utilise une terminaison de stockage connexion chaîne toostore et informations d’identification pour accéder aux services de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="f9822-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="f9822-122">Lors de l’exécution dans une application cliente, vous devez fournir la chaîne de connexion de stockage hello Bonjour suivant le format, à l’aide du nom de hello de votre compte de stockage et clé d’accès primaire pour le compte de stockage hello dans hello de hello [Azure Portal](https://portal.azure.com)pour hello *AccountName* et *AccountKey* valeurs.</span><span class="sxs-lookup"><span data-stu-id="f9822-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="f9822-123">Cet exemple montre comment vous pouvez déclarer une chaîne de connexion de champ statique toohold hello :</span><span class="sxs-lookup"><span data-stu-id="f9822-123">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="f9822-124">Dans une application en cours d’exécution au sein d’un rôle dans Microsoft Azure, cette chaîne peut être stockée dans le fichier de configuration de service hello, *ServiceConfiguration.cscfg*et sont accessibles avec un appel toohello  **RoleEnvironment.getConfigurationSettings** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f9822-124">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="f9822-125">Voici un exemple de mise en route de la chaîne de connexion hello un **paramètre** élément nommé *StorageConnectionString* dans le fichier de configuration de service hello :</span><span class="sxs-lookup"><span data-stu-id="f9822-125">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="f9822-126">Hello exemples suivants supposent que vous avez utilisé une de ces chaînes de connexion de stockage de deux méthodes tooget hello.</span><span class="sxs-lookup"><span data-stu-id="f9822-126">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="f9822-127">Création d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="f9822-127">How to: Create a queue</span></span>
<span data-ttu-id="f9822-128">Un objet **CloudQueueClient** vous permet d'obtenir les objets de référence pour les files d'attente.</span><span class="sxs-lookup"><span data-stu-id="f9822-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="f9822-129">Hello de code suivant crée un **CloudQueueClient** objet.</span><span class="sxs-lookup"><span data-stu-id="f9822-129">hello following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="f9822-130">(Remarque : il existe des méthodes supplémentaires toocreate **CloudStorageAccount** objets ; pour plus d’informations, consultez **CloudStorageAccount** Bonjour [référence SDK cliente de stockage Azure].)</span><span class="sxs-lookup"><span data-stu-id="f9822-130">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="f9822-131">Hello d’utilisation **CloudQueueClient** tooget une référence toohello file d’attente toouse de l’objet.</span><span class="sxs-lookup"><span data-stu-id="f9822-131">Use hello **CloudQueueClient** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="f9822-132">Vous pouvez créer la file d’attente hello si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="f9822-132">You can create hello queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a><span data-ttu-id="f9822-133">Comment : ajouter une file d’attente de messages tooa</span><span class="sxs-lookup"><span data-stu-id="f9822-133">How to: Add a message tooa queue</span></span>
<span data-ttu-id="f9822-134">tooinsert un message dans une file d’attente existante, commencez par créer un **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="f9822-134">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="f9822-135">Ensuite, appelez hello **addMessage** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f9822-135">Next, call hello **addMessage** method.</span></span> <span data-ttu-id="f9822-136">Un **CloudQueueMessage** peut être créé à partir d'une chaîne (au format UTF-8) ou d'un tableau d'octets.</span><span class="sxs-lookup"><span data-stu-id="f9822-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="f9822-137">Voici le code qui crée une file d’attente (s’il n’existe pas) et le message de type hello insertions « Hello, World ».</span><span class="sxs-lookup"><span data-stu-id="f9822-137">Here is code which creates a queue (if it doesn't exist) and inserts hello message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="f9822-138">Comment : lire des message de type hello suivant</span><span class="sxs-lookup"><span data-stu-id="f9822-138">How to: Peek at hello next message</span></span>
<span data-ttu-id="f9822-139">Vous pouvez lire message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="f9822-139">You can peek at hello message in hello front of a queue without removing it from hello queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="f9822-140">Comment : modifier le contenu de hello d’un message en file d’attente</span><span class="sxs-lookup"><span data-stu-id="f9822-140">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="f9822-141">Vous pouvez modifier le contenu de hello d’un message en place dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="f9822-141">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="f9822-142">Si le message de type hello représente une tâche de travail, vous pouvez utiliser cet état de hello tooupdate la fonctionnalité de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="f9822-142">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="f9822-143">Hello suivant code met à jour le message de file d’attente hello avec le nouveau contenu et jeux hello tooextend de délai d’attente de visibilité un autre 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="f9822-143">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="f9822-144">Cela enregistre l’état hello du travail associé au message de type hello, ainsi que les clients hello un autre toocontinue minute travaillant sur un message de type hello.</span><span class="sxs-lookup"><span data-stu-id="f9822-144">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="f9822-145">Vous pouvez utiliser ce flux de travail à plusieurs étapes de tootrack technique sur les messages de la file d’attente, sans avoir toostart sur du début de hello si une étape de traitement échoue en raison de l’erreur toohardware ou logicielle.</span><span class="sxs-lookup"><span data-stu-id="f9822-145">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="f9822-146">En règle générale, vous conservez ainsi un nombre de tentatives, et si hello message est retentée plusieurs  *n*  fois, vous le supprimez.</span><span class="sxs-lookup"><span data-stu-id="f9822-146">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="f9822-147">Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.</span><span class="sxs-lookup"><span data-stu-id="f9822-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="f9822-148">suivant de Hello code recherche d’exemple via la file d’attente hello de messages, localise hello premier message qui correspond à « Hello, World » pour le contenu de hello, puis modifie le contenu du message hello et se termine.</span><span class="sxs-lookup"><span data-stu-id="f9822-148">hello following code sample searches through hello queue of messages, locates hello first message that matches "Hello, World" for hello content, then modifies hello message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="f9822-149">Vous pouvez également hello exemple de code suivant met à jour uniquement hello premier message d’erreur sur la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="f9822-149">Alternatively, hello following code sample updates just hello first visible message on hello queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="f9822-150">Comment : obtenir la longueur de file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="f9822-150">How to: Get hello queue length</span></span>
<span data-ttu-id="f9822-151">Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="f9822-151">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="f9822-152">Hello **downloadAttributes** méthode vous demande de service de file d’attente hello plusieurs valeurs en cours, y compris un nombre du nombre de messages dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="f9822-152">hello **downloadAttributes** method asks hello Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="f9822-153">nombre de Hello uniquement est approximatif, car les messages peuvent être ajoutées ou supprimées une fois le service de file d’attente de hello répond tooyour demande.</span><span class="sxs-lookup"><span data-stu-id="f9822-153">hello count is only approximate because messages can be added or removed after hello Queue service responds tooyour request.</span></span> <span data-ttu-id="f9822-154">Hello **getApproximateMessageCount** méthode renvoie hello dernière valeur récupérée par l’appel de hello trop**downloadAttributes**, sans appeler le service de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="f9822-154">hello **getApproximateMessageCount** method returns hello last value retrieved by hello call too**downloadAttributes**, without calling hello Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="f9822-155">Comment : message d’appel suivant de retrait</span><span class="sxs-lookup"><span data-stu-id="f9822-155">How to: Dequeue hello next message</span></span>
<span data-ttu-id="f9822-156">Votre code enlève un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="f9822-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="f9822-157">Lorsque vous appelez **retrieveMessage**, vous obtenez un message de type hello suivante dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="f9822-157">When you call **retrieveMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="f9822-158">Un message retourné à partir de **retrieveMessage** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="f9822-158">A message returned from **retrieveMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="f9822-159">Par défaut, ce message reste invisible pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="f9822-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="f9822-160">toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez également appeler **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="f9822-160">toofinish removing hello message from hello queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="f9822-161">Ce processus en deux étapes de la suppression d’un message garantit que si votre code échoue tooprocess qu'un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="f9822-161">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="f9822-162">Votre code appelle **deleteMessage** juste après le message de salutation a été traité.</span><span class="sxs-lookup"><span data-stu-id="f9822-162">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="f9822-163">Options supplémentaires pour la suppression des messages dans la file d'attente</span><span class="sxs-lookup"><span data-stu-id="f9822-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="f9822-164">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="f9822-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="f9822-165">Tout d’abord, vous pouvez obtenir un lot de messages (haut too32).</span><span class="sxs-lookup"><span data-stu-id="f9822-165">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="f9822-166">Ensuite, vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message.</span><span class="sxs-lookup"><span data-stu-id="f9822-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="f9822-167">exemple de code suivant Hello utilise hello **retrieveMessages** messages tooget 20 de méthode dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="f9822-167">hello following code example uses hello **retrieveMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="f9822-168">Ensuite, il traite chaque message à l'aide d'une boucle **for** .</span><span class="sxs-lookup"><span data-stu-id="f9822-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="f9822-169">Il définit également hello invisibilité du délai d’attente toofive minutes (300 secondes pour chaque message).</span><span class="sxs-lookup"><span data-stu-id="f9822-169">It also sets hello invisibility timeout toofive minutes (300 seconds) for each message.</span></span> <span data-ttu-id="f9822-170">Notez que hello cinq minutes démarre pour tous les messages à hello même heure, par conséquent, si cinq minutes se sont écoulées depuis l’appel de hello trop**retrieveMessages**, tous les messages qui n’ont pas été supprimés devient visibles à nouveau.</span><span class="sxs-lookup"><span data-stu-id="f9822-170">Note that hello five minutes starts for all messages at hello same time, so when five minutes have passed since hello call too**retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a><span data-ttu-id="f9822-171">Comment : répertorier les files d’attente hello</span><span class="sxs-lookup"><span data-stu-id="f9822-171">How to: List hello queues</span></span>
<span data-ttu-id="f9822-172">tooobtain une liste de files d’attente en cours de hello, appel hello **CloudQueueClient.listQueues()** méthode qui retourne une collection de **CloudQueue** objets.</span><span class="sxs-lookup"><span data-stu-id="f9822-172">tooobtain a list of hello current queues, call hello **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="f9822-173">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="f9822-173">How to: Delete a queue</span></span>
<span data-ttu-id="f9822-174">toodelete une file d’attente et tous les messages hello qu’il contient, appel hello **deleteIfExists** méthode sur hello **CloudQueue** objet.</span><span class="sxs-lookup"><span data-stu-id="f9822-174">toodelete a queue and all hello messages contained in it, call hello **deleteIfExists** method on hello **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="f9822-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9822-175">Next steps</span></span>
<span data-ttu-id="f9822-176">Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente, suivez ces toolearn des liens sur les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="f9822-176">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="f9822-177">[Kit de développement logiciel (SDK) Azure Storage pour Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="f9822-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="f9822-178">[référence SDK cliente de stockage Azure][référence SDK cliente de stockage Azure]</span><span class="sxs-lookup"><span data-stu-id="f9822-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="f9822-179">[API REST services Stockage Azure][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="f9822-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="f9822-180">[Blog de l’équipe Stockage Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="f9822-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[référence SDK cliente de stockage Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
