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
# <a name="how-toouse-queue-storage-from-c"></a>Comment toouse stockage de file d’attente à partir de C++
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Vue d'ensemble
Ce guide vous explique comment tooperform des scénarios courants utilisant hello service de stockage de file d’attente Azure. exemples de Hello sont écrits en C++ et utiliser hello [bibliothèque cliente de stockage Azure pour C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello scénarios abordés incluent **insertion**, **lecture**, **mise en route**, et **suppression** file d’attente de messages, ainsi que  **Création et suppression de files d’attente**.

> [!NOTE]
> Les cibles de ce guide hello bibliothèque cliente Azure Storage pour C++ version 1.0.0 et versions ultérieures. Hello recommandé de version est la bibliothèque cliente de stockage 2.2.0, qui est disponible via [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](http://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Création d’une application C++
Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application C++.

toodo par conséquent, vous devez tooinstall hello bibliothèque cliente Azure Storage pour C++ et créer un compte de stockage Azure dans votre abonnement Azure.

tooinstall hello bibliothèque cliente Azure Storage pour C++, vous pouvez utiliser hello méthodes suivantes :

* **Linux :** suivez instructions hello de hello [bibliothèque cliente de stockage Azure pour C++ Lisez-moi](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.
* **Windows :** dans Visual Studio, cliquez sur **Outils &gt; Gestionnaire de package NuGet &gt; Console du gestionnaire de package**. Tapez ce qui suit hello commande dans hello [console du Gestionnaire de Package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur **entrée**.

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurer votre stockage de file d’attente de tooaccess application
Ajouter suivant de hello inclure haut de toohello instructions du fichier de C++ hello où vous souhaitez les files d’attente de stockage Azure API tooaccess toouse hello :  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configuration d’une chaîne de connexion au stockage Azure
Un client de stockage Azure utilise une terminaison de stockage connexion chaîne toostore et informations d’identification pour accéder aux services de gestion de données. Lors de l’exécution dans une application cliente, vous devez fournir la chaîne de connexion de stockage hello Bonjour suivant le format, à l’aide du nom hello de votre compte et hello stockage clé d’accès de compte de stockage hello Bonjour [Azure Portal](https://portal.azure.com)pour hello *AccountName* et *AccountKey* valeurs. Pour plus d'informations sur les comptes et les clés d'accès de stockage, consultez la page [À propos des comptes Azure Storage](storage-create-storage-account.md). Cet exemple montre comment vous pouvez déclarer une chaîne de connexion de champ statique toohold hello :  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest votre application sur votre ordinateur local de Windows, vous pouvez utiliser hello Microsoft Azure [l’émulateur de stockage](storage-use-emulator.md) qui est installé avec hello [Azure SDK](https://azure.microsoft.com/downloads/). l’émulateur de stockage Hello est un utilitaire qui simule hello Blob, file d’attente et Table services disponibles dans Azure sur votre ordinateur de développement local. Hello suivant montre comment vous pouvez déclarer un champ statique toohold hello connexion chaîne tooyour local l’émulateur de stockage :  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

l’émulateur de stockage Azure hello toostart, sélectionnez hello **Démarrer** hello bouton ou appuyez sur **Windows** clé. Commencez à taper **émulateur de stockage Azure**, puis sélectionnez **émulateur de stockage Microsoft Azure** à partir de la liste des applications hello.

Hello exemples suivants supposent que vous avez utilisé une de ces chaînes de connexion de stockage de deux méthodes tooget hello.

## <a name="retrieve-your-connection-string"></a>Récupération de votre chaîne de connexion
Vous pouvez utiliser hello **cloud_storage_account** classe toorepresent vos informations de compte de stockage. tooretrieve plus d’informations à partir de la chaîne de connexion de stockage hello du compte de votre stockage, vous pouvez utiliser hello **analyser** (méthode).

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a>Création d'une file d'attente
Un objet **cloud_queue_client** vous permet d’obtenir les objets de référence pour les files d’attente. Hello de code suivant crée un **cloud_queue_client** objet.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

Hello d’utilisation **cloud_queue_client** tooget une référence toohello file d’attente toouse de l’objet. Vous pouvez créer la file d’attente hello si elle n’existe pas.

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Insertion d'un message dans une file d'attente
tooinsert un message dans une file d’attente existante, commencez par créer un **cloud_queue_message**. Ensuite, appelez hello **add_message** (méthode). Un **cloud_queue_message** peut être créé à partir d’une chaîne ou d’un tableau **d’octets**. Voici le code qui crée une file d’attente (s’il n’existe pas) et le message de type hello insertions « Hello, World » :

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

## <a name="how-to-peek-at-hello-next-message"></a>Comment : lire des message de type hello suivant
Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **peek_message** (méthode).

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Comment : modifier le contenu de hello d’un message en file d’attente
Vous pouvez modifier le contenu de hello d’un message en place dans la file d’attente hello. Si le message de type hello représente une tâche de travail, vous pouvez utiliser cet état de hello tooupdate la fonctionnalité de tâche hello. Hello suivant code met à jour le message de file d’attente hello avec le nouveau contenu et jeux hello tooextend de délai d’attente de visibilité un autre 60 secondes. Cela enregistre l’état hello du travail associé au message de type hello, ainsi que les clients hello un autre toocontinue minute travaillant sur un message de type hello. Vous pouvez utiliser ce flux de travail à plusieurs étapes de tootrack technique sur les messages de la file d’attente, sans avoir toostart sur du début de hello si une étape de traitement échoue en raison de l’erreur toohardware ou logicielle. En règle générale, vous conservez ainsi un nombre de tentatives, et si le message de type hello est retentée n plusieurs fois, vous le supprimez. Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.

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

## <a name="how-to-de-queue-hello-next-message"></a>Comment : annuler file d’attente de message de type hello suivant
Votre code enlève un message d'une file d'attente en deux étapes. Lorsque vous appelez **get_message**, vous obtenez un message de type hello suivante dans une file d’attente. Un message retourné à partir de **get_message** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente. toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez également appeler **delete_message**. Ce processus en deux étapes de la suppression d’un message garantit que si votre code échoue tooprocess qu'un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message puis réessayez. Votre code appelle **delete_message** avec le bouton droit une fois le message de salutation a été traité.

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

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a>Utilisation d'options supplémentaires pour l'enlèvement des messages
Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente. Tout d’abord, vous pouvez obtenir un lot de messages (haut too32). Ensuite, vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message. exemple de code suivant Hello utilise hello **get_messages** messages tooget 20 de méthode dans un seul appel. Ensuite, il traite chaque message à l'aide d'une boucle **for** . Il définit également hello invisibilité délai d’expiration toofive minutes pour chaque message. Notez que hello 5 minutes démarre pour tous les messages à hello même moment, après que les 5 minutes se sont écoulées depuis l’appel de hello trop**get_messages**, tous les messages qui n’ont pas été supprimés devient visibles à nouveau.

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

## <a name="how-to-get-hello-queue-length"></a>Comment : obtenir la longueur de file d’attente hello
Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente. Hello **download_attributes** méthode demande tooretrieve de service de file d’attente hello attributs de file d’attente hello, y compris le nombre de messages hello. Hello **approximate_message_count** méthode obtient le nombre approximatif de hello de messages dans la file d’attente hello.

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

## <a name="how-to-delete-a-queue"></a>Suppression d'une file d'attente
toodelete une file d’attente et tous les messages hello qu’il contient, appel hello **delete_queue_if_exists** méthode sur un objet de file d’attente hello.

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

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente, suivez ces liens de toolearn plus d’informations sur le stockage Azure.

* [Comment toouse stockage d’objets Blob à partir de C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Comment toouse le stockage de Table à partir de C++](storage-c-plus-plus-how-to-use-tables.md)
* [Listage des ressources Azure Storage en C++](storage-c-plus-plus-enumeration.md)
* [Référence de la bibliothèque cliente de stockage pour C++](http://azure.github.io/azure-storage-cpp)
* [Documentation d'Azure Storage](https://azure.microsoft.com/documentation/services/storage/)