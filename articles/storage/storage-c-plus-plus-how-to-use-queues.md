---
title: "stockage de file d’attente toouse aaaHow (C++) | Documents Microsoft"
description: "Découvrez comment toouse hello service de stockage de file d’attente dans Azure. Les exemples sont écrits en C++."
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
ms.openlocfilehash: 755380824890ad83774e14d258975915e10cfede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a><span data-ttu-id="578f8-104">Comment toouse stockage de file d’attente à partir de C++</span><span class="sxs-lookup"><span data-stu-id="578f8-104">How toouse Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="578f8-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="578f8-105">Overview</span></span>
<span data-ttu-id="578f8-106">Ce guide vous explique comment tooperform des scénarios courants utilisant hello service de stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="578f8-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="578f8-107">exemples de Hello sont écrits en C++ et utiliser hello [bibliothèque cliente de stockage Azure pour C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="578f8-107">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="578f8-108">Hello scénarios abordés incluent **insertion**, **lecture**, **mise en route**, et **suppression** file d’attente de messages, ainsi que  **Création et suppression de files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="578f8-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="578f8-109">Les cibles de ce guide hello bibliothèque cliente Azure Storage pour C++ version 1.0.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="578f8-109">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="578f8-110">Hello recommandé de version est la bibliothèque cliente de stockage 2.2.0, qui est disponible via [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="578f8-110">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="578f8-111">Création d’une application C++</span><span class="sxs-lookup"><span data-stu-id="578f8-111">Create a C++ application</span></span>
<span data-ttu-id="578f8-112">Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application C++.</span><span class="sxs-lookup"><span data-stu-id="578f8-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="578f8-113">toodo par conséquent, vous devez tooinstall hello bibliothèque cliente Azure Storage pour C++ et créer un compte de stockage Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="578f8-113">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="578f8-114">tooinstall hello bibliothèque cliente Azure Storage pour C++, vous pouvez utiliser hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="578f8-114">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="578f8-115">**Linux :** suivez instructions hello de hello [bibliothèque cliente de stockage Azure pour C++ Lisez-moi](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span><span class="sxs-lookup"><span data-stu-id="578f8-115">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="578f8-116">**Windows :** dans Visual Studio, cliquez sur **Outils &gt; Gestionnaire de package NuGet &gt; Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="578f8-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="578f8-117">Tapez ce qui suit hello commande dans hello [console du Gestionnaire de Package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="578f8-117">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="578f8-118">Configurer votre stockage de file d’attente de tooaccess application</span><span class="sxs-lookup"><span data-stu-id="578f8-118">Configure your application tooaccess Queue Storage</span></span>
<span data-ttu-id="578f8-119">Ajouter suivant de hello inclure haut de toohello instructions du fichier de C++ hello où vous souhaitez les files d’attente de stockage Azure API tooaccess toouse hello :</span><span class="sxs-lookup"><span data-stu-id="578f8-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="578f8-120">Configuration d’une chaîne de connexion au stockage Azure</span><span class="sxs-lookup"><span data-stu-id="578f8-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="578f8-121">Un client de stockage Azure utilise une terminaison de stockage connexion chaîne toostore et informations d’identification pour accéder aux services de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="578f8-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="578f8-122">Lors de l’exécution dans une application cliente, vous devez fournir la chaîne de connexion de stockage hello Bonjour suivant le format, à l’aide du nom hello de votre compte et hello stockage clé d’accès de compte de stockage hello Bonjour [Azure Portal](https://portal.azure.com)pour hello *AccountName* et *AccountKey* valeurs.</span><span class="sxs-lookup"><span data-stu-id="578f8-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="578f8-123">Pour plus d'informations sur les comptes et les clés d'accès de stockage, consultez la page [À propos des comptes Azure Storage](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="578f8-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="578f8-124">Cet exemple montre comment vous pouvez déclarer une chaîne de connexion de champ statique toohold hello :</span><span class="sxs-lookup"><span data-stu-id="578f8-124">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="578f8-125">tootest votre application sur votre ordinateur local de Windows, vous pouvez utiliser hello Microsoft Azure [l’émulateur de stockage](storage-use-emulator.md) qui est installé avec hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="578f8-125">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="578f8-126">l’émulateur de stockage Hello est un utilitaire qui simule hello Blob, file d’attente et Table services disponibles dans Azure sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="578f8-126">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="578f8-127">Hello suivant montre comment vous pouvez déclarer un champ statique toohold hello connexion chaîne tooyour local l’émulateur de stockage :</span><span class="sxs-lookup"><span data-stu-id="578f8-127">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="578f8-128">l’émulateur de stockage Azure hello toostart, sélectionnez hello **Démarrer** hello bouton ou appuyez sur **Windows** clé.</span><span class="sxs-lookup"><span data-stu-id="578f8-128">toostart hello Azure storage emulator, select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="578f8-129">Commencez à taper **émulateur de stockage Azure**, puis sélectionnez **émulateur de stockage Microsoft Azure** à partir de la liste des applications hello.</span><span class="sxs-lookup"><span data-stu-id="578f8-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>

<span data-ttu-id="578f8-130">Hello exemples suivants supposent que vous avez utilisé une de ces chaînes de connexion de stockage de deux méthodes tooget hello.</span><span class="sxs-lookup"><span data-stu-id="578f8-130">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="578f8-131">Récupération de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="578f8-131">Retrieve your connection string</span></span>
<span data-ttu-id="578f8-132">Vous pouvez utiliser hello **cloud_storage_account** classe toorepresent vos informations de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="578f8-132">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="578f8-133">tooretrieve plus d’informations à partir de la chaîne de connexion de stockage hello du compte de votre stockage, vous pouvez utiliser hello **analyser** (méthode).</span><span class="sxs-lookup"><span data-stu-id="578f8-133">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="578f8-134">Création d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="578f8-134">How to: Create a queue</span></span>
<span data-ttu-id="578f8-135">Un objet **cloud_queue_client** vous permet d’obtenir les objets de référence pour les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="578f8-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="578f8-136">Hello de code suivant crée un **cloud_queue_client** objet.</span><span class="sxs-lookup"><span data-stu-id="578f8-136">hello following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="578f8-137">Hello d’utilisation **cloud_queue_client** tooget une référence toohello file d’attente toouse de l’objet.</span><span class="sxs-lookup"><span data-stu-id="578f8-137">Use hello **cloud_queue_client** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="578f8-138">Vous pouvez créer la file d’attente hello si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="578f8-138">You can create hello queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="578f8-139">Insertion d'un message dans une file d'attente</span><span class="sxs-lookup"><span data-stu-id="578f8-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="578f8-140">tooinsert un message dans une file d’attente existante, commencez par créer un **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="578f8-140">tooinsert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="578f8-141">Ensuite, appelez hello **add_message** (méthode).</span><span class="sxs-lookup"><span data-stu-id="578f8-141">Next, call hello **add_message** method.</span></span> <span data-ttu-id="578f8-142">Un **cloud_queue_message** peut être créé à partir d’une chaîne ou d’un tableau **d’octets**.</span><span class="sxs-lookup"><span data-stu-id="578f8-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="578f8-143">Voici le code qui crée une file d’attente (s’il n’existe pas) et le message de type hello insertions « Hello, World » :</span><span class="sxs-lookup"><span data-stu-id="578f8-143">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="578f8-144">Comment : lire des message de type hello suivant</span><span class="sxs-lookup"><span data-stu-id="578f8-144">How to: Peek at hello next message</span></span>
<span data-ttu-id="578f8-145">Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **peek_message** (méthode).</span><span class="sxs-lookup"><span data-stu-id="578f8-145">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="578f8-146">Comment : modifier le contenu de hello d’un message en file d’attente</span><span class="sxs-lookup"><span data-stu-id="578f8-146">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="578f8-147">Vous pouvez modifier le contenu de hello d’un message en place dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="578f8-147">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="578f8-148">Si le message de type hello représente une tâche de travail, vous pouvez utiliser cet état de hello tooupdate la fonctionnalité de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="578f8-148">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="578f8-149">Hello suivant code met à jour le message de file d’attente hello avec le nouveau contenu et jeux hello tooextend de délai d’attente de visibilité un autre 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="578f8-149">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="578f8-150">Cela enregistre l’état hello du travail associé au message de type hello, ainsi que les clients hello un autre toocontinue minute travaillant sur un message de type hello.</span><span class="sxs-lookup"><span data-stu-id="578f8-150">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="578f8-151">Vous pouvez utiliser ce flux de travail à plusieurs étapes de tootrack technique sur les messages de la file d’attente, sans avoir toostart sur du début de hello si une étape de traitement échoue en raison de l’erreur toohardware ou logicielle.</span><span class="sxs-lookup"><span data-stu-id="578f8-151">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="578f8-152">En règle générale, vous conservez ainsi un nombre de tentatives, et si le message de type hello est retentée n plusieurs fois, vous le supprimez.</span><span class="sxs-lookup"><span data-stu-id="578f8-152">Typically, you would keep a retry count as well, and if hello message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="578f8-153">Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.</span><span class="sxs-lookup"><span data-stu-id="578f8-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a><span data-ttu-id="578f8-154">Comment : annuler file d’attente de message de type hello suivant</span><span class="sxs-lookup"><span data-stu-id="578f8-154">How to: De-queue hello next message</span></span>
<span data-ttu-id="578f8-155">Votre code enlève un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="578f8-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="578f8-156">Lorsque vous appelez **get_message**, vous obtenez un message de type hello suivante dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="578f8-156">When you call **get_message**, you get hello next message in a queue.</span></span> <span data-ttu-id="578f8-157">Un message retourné à partir de **get_message** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="578f8-157">A message returned from **get_message** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="578f8-158">toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez également appeler **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="578f8-158">toofinish removing hello message from hello queue, you must also call **delete_message**.</span></span> <span data-ttu-id="578f8-159">Ce processus en deux étapes de la suppression d’un message garantit que si votre code échoue tooprocess qu'un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="578f8-159">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="578f8-160">Votre code appelle **delete_message** avec le bouton droit une fois le message de salutation a été traité.</span><span class="sxs-lookup"><span data-stu-id="578f8-160">Your code calls **delete_message** right after hello message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="578f8-161">Utilisation d'options supplémentaires pour l'enlèvement des messages</span><span class="sxs-lookup"><span data-stu-id="578f8-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="578f8-162">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="578f8-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="578f8-163">Tout d’abord, vous pouvez obtenir un lot de messages (haut too32).</span><span class="sxs-lookup"><span data-stu-id="578f8-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="578f8-164">Ensuite, vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message.</span><span class="sxs-lookup"><span data-stu-id="578f8-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="578f8-165">exemple de code suivant Hello utilise hello **get_messages** messages tooget 20 de méthode dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="578f8-165">hello following code example uses hello **get_messages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="578f8-166">Ensuite, il traite chaque message à l'aide d'une boucle **for** .</span><span class="sxs-lookup"><span data-stu-id="578f8-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="578f8-167">Il définit également hello invisibilité délai d’expiration toofive minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="578f8-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="578f8-168">Notez que hello 5 minutes démarre pour tous les messages à hello même moment, après que les 5 minutes se sont écoulées depuis l’appel de hello trop**get_messages**, tous les messages qui n’ont pas été supprimés devient visibles à nouveau.</span><span class="sxs-lookup"><span data-stu-id="578f8-168">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="578f8-169">Comment : obtenir la longueur de file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="578f8-169">How to: Get hello queue length</span></span>
<span data-ttu-id="578f8-170">Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="578f8-170">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="578f8-171">Hello **download_attributes** méthode demande tooretrieve de service de file d’attente hello attributs de file d’attente hello, y compris le nombre de messages hello.</span><span class="sxs-lookup"><span data-stu-id="578f8-171">hello **download_attributes** method asks hello Queue service tooretrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="578f8-172">Hello **approximate_message_count** méthode obtient le nombre approximatif de hello de messages dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="578f8-172">hello **approximate_message_count** method gets hello approximate number of messages in hello queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="578f8-173">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="578f8-173">How to: Delete a queue</span></span>
<span data-ttu-id="578f8-174">toodelete une file d’attente et tous les messages hello qu’il contient, appel hello **delete_queue_if_exists** méthode sur un objet de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="578f8-174">toodelete a queue and all hello messages contained in it, call hello **delete_queue_if_exists** method on hello queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="578f8-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="578f8-175">Next steps</span></span>
<span data-ttu-id="578f8-176">Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente, suivez ces liens de toolearn plus d’informations sur le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="578f8-176">Now that you've learned hello basics of Queue storage, follow these links toolearn more about Azure Storage.</span></span>

* [<span data-ttu-id="578f8-177">Comment toouse stockage d’objets Blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="578f8-177">How toouse Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="578f8-178">Comment toouse le stockage de Table à partir de C++</span><span class="sxs-lookup"><span data-stu-id="578f8-178">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="578f8-179">Listage des ressources Azure Storage en C++</span><span class="sxs-lookup"><span data-stu-id="578f8-179">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="578f8-180">Référence de la bibliothèque cliente de stockage pour C++</span><span class="sxs-lookup"><span data-stu-id="578f8-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="578f8-181">Documentation d'Azure Storage</span><span class="sxs-lookup"><span data-stu-id="578f8-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)