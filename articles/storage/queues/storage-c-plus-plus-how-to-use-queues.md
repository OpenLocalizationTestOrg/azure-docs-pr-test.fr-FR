---
title: Utilisation du stockage de files d'attente (C++) | Microsoft Docs
description: "Découvrez comment utiliser le service de stockage de files d’attente dans Azure. Les exemples sont écrits en C++."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: 5e81d5e0af9871099b7f921f355cf94249e4d30c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-c"></a><span data-ttu-id="94170-104">Utilisation du stockage de files d'attente à partir de C++</span><span class="sxs-lookup"><span data-stu-id="94170-104">How to use Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="94170-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="94170-105">Overview</span></span>
<span data-ttu-id="94170-106">Ce guide décrit le déroulement de scénarios courants dans le cadre de l'utilisation du service de stockage des files d'attente Azure.</span><span class="sxs-lookup"><span data-stu-id="94170-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="94170-107">Les exemples ont été écrits en C++ et utilisent la [bibliothèque cliente Azure Storage pour C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="94170-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="94170-108">Les scénarios traités incluent **l’insertion**, la **lecture furtive**, la **récupération** et la **suppression** des messages de file d’attente, ainsi que la **création et suppression des files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="94170-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="94170-109">Ce guide cible la bibliothèque cliente Azure Storage pour C++ version 1.0.0 et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="94170-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="94170-110">La version recommandée est la bibliothèque cliente de stockage version 2.2.0, disponible par le biais de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="94170-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="94170-111">Création d’une application C++</span><span class="sxs-lookup"><span data-stu-id="94170-111">Create a C++ application</span></span>
<span data-ttu-id="94170-112">Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application C++.</span><span class="sxs-lookup"><span data-stu-id="94170-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="94170-113">Pour ce faire, vous devez installer la bibliothèque cliente Azure Storage pour C++ et créer un compte Azure Storage dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="94170-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="94170-114">Pour installer la bibliothèque cliente Azure Storage pour C++, vous pouvez procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="94170-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="94170-115">**Linux :** suivez les instructions disponibles sur la page [Bibliothèque cliente Azure Storage pour C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="94170-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="94170-116">**Windows :** dans Visual Studio, cliquez sur **Outils > Gestionnaire de package NuGet > Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="94170-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="94170-117">Entrez la commande suivante dans la [console du gestionnaire du package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur **ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="94170-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="94170-118">Configuration de votre application pour accéder au stockage de files d'attente</span><span class="sxs-lookup"><span data-stu-id="94170-118">Configure your application to access Queue Storage</span></span>
<span data-ttu-id="94170-119">Ajoutez les instructions import suivantes au début du fichier Java dans lequel vous voulez utiliser des API de stockage Azure pour accéder aux files d'attente :</span><span class="sxs-lookup"><span data-stu-id="94170-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="94170-120">Configuration d’une chaîne de connexion au stockage Azure</span><span class="sxs-lookup"><span data-stu-id="94170-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="94170-121">Un client de stockage Azure utilise une chaîne de connexion de stockage pour stocker des points de terminaison et des informations d’identification permettant d’accéder aux services de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="94170-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="94170-122">Lors de l’exécution d’une application cliente, vous devez spécifier la chaîne de connexion au stockage au format suivant, en indiquant le nom de votre compte de stockage et sa clé d’accès de stockage, correspondant aux valeurs *AccountName* et *AccountKey*, sur le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="94170-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="94170-123">Pour plus d'informations sur les comptes et les clés d'accès de stockage, consultez la page [À propos des comptes Azure Storage](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="94170-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="94170-124">Cet exemple vous montre comment déclarer un champ statique pour qu’il contienne une chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="94170-124">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="94170-125">Pour tester votre application sur votre ordinateur Windows local, vous pouvez utiliser [l’émulateur de stockage Microsoft Azure](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) installé avec le [Kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="94170-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="94170-126">L'émulateur de stockage est un utilitaire qui simule sur votre ordinateur de développement local les objets blob, les files d'attente et les services de Table disponibles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="94170-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="94170-127">L’exemple suivant vous montre comment déclarer un champ statique pour qu’il contienne une chaîne de connexion vers votre émulateur de stockage local :</span><span class="sxs-lookup"><span data-stu-id="94170-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="94170-128">Pour démarrer l’émulateur de stockage Azure, sélectionnez le bouton **Démarrer** ou appuyez sur la touche **Windows**.</span><span class="sxs-lookup"><span data-stu-id="94170-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="94170-129">Commencez à taper **Émulateur de stockage Azure**, puis sélectionnez **Émulateur de stockage Microsoft Azure** dans la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="94170-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>

<span data-ttu-id="94170-130">Les exemples ci-dessous partent du principe que vous avez utilisé l’une de ces deux méthodes pour obtenir la chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="94170-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="94170-131">Récupération de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="94170-131">Retrieve your connection string</span></span>
<span data-ttu-id="94170-132">Vous pouvez utiliser la classe **cloud_storage_account** pour représenter les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="94170-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="94170-133">Pour extraire les informations de votre compte de stockage de la chaîne de connexion de stockage, vous pouvez utiliser la méthode **parse** .</span><span class="sxs-lookup"><span data-stu-id="94170-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="94170-134">Création d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="94170-134">How to: Create a queue</span></span>
<span data-ttu-id="94170-135">Un objet **cloud_queue_client** vous permet d’obtenir les objets de référence pour les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="94170-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="94170-136">Le code suivant crée un objet **cloud_queue_client**.</span><span class="sxs-lookup"><span data-stu-id="94170-136">The following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="94170-137">Utilisez l’objet **cloud_queue_client** pour obtenir une référence pointant vers la file d’attente à utiliser.</span><span class="sxs-lookup"><span data-stu-id="94170-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="94170-138">Si la file d'attente n'existe pas, vous pouvez la créer :</span><span class="sxs-lookup"><span data-stu-id="94170-138">You can create the queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="94170-139">Insertion d'un message dans une file d'attente</span><span class="sxs-lookup"><span data-stu-id="94170-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="94170-140">Pour insérer un message dans une file d’attente existante, commencez par créer un **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="94170-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="94170-141">Appelez ensuite la méthode **add_message**.</span><span class="sxs-lookup"><span data-stu-id="94170-141">Next, call the **add_message** method.</span></span> <span data-ttu-id="94170-142">Un **cloud_queue_message** peut être créé à partir d’une chaîne ou d’un tableau **d’octets**.</span><span class="sxs-lookup"><span data-stu-id="94170-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="94170-143">Voici le code qui crée une file d'attente (si elle n'existe pas) et insère le message « Hello, World » :</span><span class="sxs-lookup"><span data-stu-id="94170-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it to the queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="94170-144">Lecture furtive du message suivant</span><span class="sxs-lookup"><span data-stu-id="94170-144">How to: Peek at the next message</span></span>
<span data-ttu-id="94170-145">Vous pouvez lire furtivement le message au début de la file d’attente sans le supprimer de la file d’attente en appelant la méthode **peek_message**.</span><span class="sxs-lookup"><span data-stu-id="94170-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at the next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output the message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="94170-146">Modification du contenu d'un message en file d'attente</span><span class="sxs-lookup"><span data-stu-id="94170-146">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="94170-147">Vous pouvez modifier le contenu d'un message placé dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="94170-147">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="94170-148">Si le message représente une tâche, vous pouvez utiliser cette fonctionnalité pour mettre à jour l'état de la tâche.</span><span class="sxs-lookup"><span data-stu-id="94170-148">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="94170-149">Le code suivant met à jour le message de la file d'attente avec un nouveau contenu et ajoute 60 secondes au délai d'expiration de la visibilité.</span><span class="sxs-lookup"><span data-stu-id="94170-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="94170-150">Cette opération enregistre l'état de la tâche associée au message et accorde une minute supplémentaire au client pour traiter le message.</span><span class="sxs-lookup"><span data-stu-id="94170-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="94170-151">Vous pouvez utiliser cette technique pour suivre des flux de travail à plusieurs étapes sur les messages de file d'attente, sans devoir reprendre du début si une étape du traitement échoue à cause d'une défaillance matérielle ou logicielle.</span><span class="sxs-lookup"><span data-stu-id="94170-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="94170-152">Normalement, vous conservez aussi un nombre de nouvelles tentatives et si le message est retenté plus de n fois, vous le supprimez.</span><span class="sxs-lookup"><span data-stu-id="94170-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="94170-153">Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.</span><span class="sxs-lookup"><span data-stu-id="94170-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the message from the queue and update the message contents.
// The visibility timeout "0" means make it visible immediately.
// The visibility timeout "60" means the client can get another minute to continue
// working on the message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output the message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-the-next-message"></a><span data-ttu-id="94170-154">Suppression du message suivant dans la file d'attente</span><span class="sxs-lookup"><span data-stu-id="94170-154">How to: De-queue the next message</span></span>
<span data-ttu-id="94170-155">Votre code enlève un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="94170-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="94170-156">Lorsque vous appelez **get_message**, vous obtenez le message suivant dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="94170-156">When you call **get_message**, you get the next message in a queue.</span></span> <span data-ttu-id="94170-157">Un message renvoyé par **get_message** devient invisible de tout autre code lisant les messages de cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="94170-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="94170-158">Pour finaliser la suppression du message de la file d’attente, vous devez aussi appeler **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="94170-158">To finish removing the message from the queue, you must also call **delete_message**.</span></span> <span data-ttu-id="94170-159">Ce processus de suppression d'un message en deux étapes garantit que, si votre code ne parvient pas à traiter un message à cause d'une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et réessayer.</span><span class="sxs-lookup"><span data-stu-id="94170-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="94170-160">Votre code appelle **delete_message** juste après le traitement du message.</span><span class="sxs-lookup"><span data-stu-id="94170-160">Your code calls **delete_message** right after the message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete the message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="94170-161">Utilisation d'options supplémentaires pour l'enlèvement des messages</span><span class="sxs-lookup"><span data-stu-id="94170-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="94170-162">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="94170-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="94170-163">Premièrement, vous pouvez obtenir un lot de messages (jusqu'à 32).</span><span class="sxs-lookup"><span data-stu-id="94170-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="94170-164">Deuxièmement, vous pouvez définir un délai d'expiration de l'invisibilité plus long ou plus court afin d'accorder à votre code plus ou moins de temps pour traiter complètement chaque message.</span><span class="sxs-lookup"><span data-stu-id="94170-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="94170-165">L’exemple de code suivant utilise la méthode **get_messages** pour obtenir 20 messages en un appel.</span><span class="sxs-lookup"><span data-stu-id="94170-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span></span> <span data-ttu-id="94170-166">Ensuite, il traite chaque message à l'aide d'une boucle **for** .</span><span class="sxs-lookup"><span data-stu-id="94170-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="94170-167">Il définit également le délai d'expiration de l'invisibilité sur cinq minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="94170-167">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="94170-168">Notez que le délai de 5 minutes démarre en même temps pour tous les messages, donc une fois les 5 minutes écoulées après l’appel de **get_messages**, tous les messages n’ayant pas été supprimés redeviennent visibles.</span><span class="sxs-lookup"><span data-stu-id="94170-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display the contents of the message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="94170-169">Obtention de la longueur de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="94170-169">How to: Get the queue length</span></span>
<span data-ttu-id="94170-170">Vous pouvez obtenir une estimation du nombre de messages dans une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="94170-170">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="94170-171">La méthode **download_attributes** demande au service de files d’attente d’extraire les attributs de la file d’attente, y compris le nombre de messages.</span><span class="sxs-lookup"><span data-stu-id="94170-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="94170-172">La méthode **approximate_message_count** obtient le nombre approximatif de messages dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="94170-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch the queue attributes.
queue.download_attributes();

// Retrieve the cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="94170-173">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="94170-173">How to: Delete a queue</span></span>
<span data-ttu-id="94170-174">Pour supprimer une file d’attente et tous les messages qu’elle contient, appelez la méthode **delete_queue_if_exists** sur l’objet file d’attente.</span><span class="sxs-lookup"><span data-stu-id="94170-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If the queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="94170-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="94170-175">Next steps</span></span>
<span data-ttu-id="94170-176">Maintenant que vous connaissez les bases du stockage de files d'attente, consultez les liens suivants pour en savoir plus sur Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="94170-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span></span>

* [<span data-ttu-id="94170-177">Utilisation du stockage d'objets blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="94170-177">How to use Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="94170-178">Utilisation du stockage de tables à partir de C++</span><span class="sxs-lookup"><span data-stu-id="94170-178">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="94170-179">Listage des ressources Azure Storage en C++</span><span class="sxs-lookup"><span data-stu-id="94170-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="94170-180">Référence de la bibliothèque cliente de stockage pour C++</span><span class="sxs-lookup"><span data-stu-id="94170-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="94170-181">Documentation d'Azure Storage</span><span class="sxs-lookup"><span data-stu-id="94170-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)