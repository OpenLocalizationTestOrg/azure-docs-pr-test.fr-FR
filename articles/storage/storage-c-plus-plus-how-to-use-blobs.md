---
title: "stockage d’objets blob aaaHow toouse (stockage d’objets) à partir de C++ | Documents Microsoft"
description: "Stocker des données non structurées dans le cloud hello avec le stockage d’objets Blob Azure (stockage d’objets)."
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 0d7e7436a109ef54fc07cc238c03cfc7cf2caac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a>Comment toouse stockage d’objets Blob à partir de C++
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Vue d'ensemble
Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB. Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application. Stockage d’objets BLOB est également référencé tooas stockage d’objets.

Ce guide va vous montrer comment tooperform des scénarios courants utilisant hello service de stockage d’objets Blob Azure. exemples de Hello sont écrits en C++ et utiliser hello [bibliothèque cliente de stockage Azure pour C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello scénarios abordés incluent **téléchargement**, **liste**, **téléchargement**, et **suppression** objets BLOB.  

> [!NOTE]
> Les cibles de ce guide hello bibliothèque cliente Azure Storage pour C++ version 1.0.0 et versions ultérieures. Hello recommandé de version est la bibliothèque cliente de stockage 2.2.0, qui est disponible via [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Création d’une application C++
Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application C++.  

toodo par conséquent, vous devez tooinstall hello bibliothèque cliente Azure Storage pour C++ et créer un compte de stockage Azure dans votre abonnement Azure.   

tooinstall hello bibliothèque cliente Azure Storage pour C++, vous pouvez utiliser hello méthodes suivantes :

* **Linux :** suivez instructions hello de hello [bibliothèque cliente de stockage Azure pour C++ Lisez-moi](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.  
* **Windows :** dans Visual Studio, cliquez sur **Outils &gt; Gestionnaire de package NuGet &gt; Console du gestionnaire de package**. Tapez ce qui suit hello commande dans hello [console du Gestionnaire de Package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur **entrée**.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-blob-storage"></a>Configurer votre application de tooaccess stockage d’objets Blob
Ajouter suivant de hello inclure haut de toohello d’instructions de hello C++ fichier dans lequel le BLOB tooaccess API toouse hello stockage Azure :  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a>Configuration d’une chaîne de connexion de stockage Azure
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

Ensuite, obtenez une référence tooa **cloud_blob_client** classe car elle vous permet de tooretrieve les objets qui représentent les conteneurs et objets BLOB stockés dans hello Service de stockage d’objets Blob. Hello de code suivant crée un **cloud_blob_client** objet à l’aide d’objet de compte de stockage hello nous récupérées ci-dessus :  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a>Création d’un conteneur
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Cet exemple montre comment toocreate un conteneur s’il n’existe pas déjà :  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

Par défaut, conteneur hello est privé, et vous devez spécifier vos objets BLOB de stockage accès toodownload clé à partir de ce conteneur. Si vous souhaitez que les fichiers hello toomake (BLOB) dans tooeveryone disponibles du conteneur hello, vous pouvez définir hello conteneur toobe public à l’aide de hello suivant de code :  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

Toute personne sur Internet de hello peut voir les objets BLOB dans un conteneur public, mais vous pouvez modifier ou les supprimer que si vous disposez de la clé d’accès appropriées hello.  

## <a name="how-to-upload-a-blob-into-a-container"></a>Téléchargement d’un objet blob dans un conteneur
Le service de stockage d’objets blob Azure prend en charge les objets blob de blocs et de page. Dans la majorité de hello des cas, objet blob de blocs est hello recommandé toouse de type.  

tooupload fichier tooa objet blob de blocs, obtenir une référence de conteneur et utiliser tooget une référence d’objet blob de bloc. Une fois que vous avez une référence d’objet blob, vous pouvez télécharger n’importe quel flux de données tooit en appelant hello **upload_from_stream** (méthode). Cette opération va créer l’objet blob de hello si elle n’a pas été précédemment existe, ou remplacer s’il existe. Hello suivant montre l’exemple de comment tooupload un objet blob dans un conteneur et suppose que le conteneur de hello a déjà été créé.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

Vous pouvez également utiliser hello **upload_from_file** tooupload de méthode objet blob de blocs tooa fichier.

## <a name="how-to-list-hello-blobs-in-a-container"></a>Comment : répertorier les objets BLOB de hello dans un conteneur
objets BLOB de hello toolist dans un conteneur, d’abord obtenir une référence de conteneur. Vous pouvez ensuite utiliser du conteneur hello **list_blobs** objets BLOB de méthode tooretrieve hello et/ou les répertoires qu’il contient. tooaccess hello ensemble complet des propriétés et méthodes pour retourné **list_blob_item**, vous devez appeler hello **list_blob_item.as_blob** méthode tooget un **cloud_blob** objet, ou hello **list_blob.as_directory** méthode tooget un objet cloud_blob_directory. Hello de code suivant montre comment tooretrieve et sortie hello URI de chaque élément Bonjour **mon conteneur-exemple** conteneur :

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

Pour plus d’informations sur les opérations de listage, consultez [Listage des ressources Azure Storage en C++](storage-c-plus-plus-enumeration.md).

## <a name="how-to-download-blobs"></a>Téléchargement d’objets blob
objets BLOB toodownload, tout d’abord extraire une référence d’objet blob et ensuite appeler hello **download_to_stream** (méthode). exemple Hello utilise hello **download_to_stream** méthode tootransfer hello contenu tooa flux de données objet blob que peuvent alors être conservées tooa des fichiers locaux.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

Vous pouvez également utiliser hello **download_to_file** contenu de hello méthode toodownload d’un fichier de tooa d’objets blob.
En outre, vous pouvez également utiliser hello **download_text** contenu de hello toodownload de méthode d’un objet blob comme une chaîne de texte.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a>Suppression d’objets blob
tout d’abord obtenir une référence d’objet blob de toodelete un objet blob et ensuite appeler hello **delete_blob** méthode dessus.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello du stockage blob, suivez ces liens de toolearn plus d’informations sur le stockage Azure.  

* [Comment toouse stockage de file d’attente à partir de C++](storage-c-plus-plus-how-to-use-queues.md)
* [Comment toouse le stockage de Table à partir de C++](storage-c-plus-plus-how-to-use-tables.md)
* [Listage des ressources Azure Storage en C++](storage-c-plus-plus-enumeration.md)
* [Référence de la bibliothèque cliente de stockage pour C++](http://azure.github.io/azure-storage-cpp)
* [Documentation d’Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Transfert de données avec hello utilitaire de ligne de commande AzCopy](storage-use-azcopy.md)

