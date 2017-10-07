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
ms.openlocfilehash: e63df4683e5c10c9f8fbe4106c655df61be0e1a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a><span data-ttu-id="0399d-103">Comment toouse stockage d’objets Blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="0399d-103">How toouse Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="0399d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0399d-104">Overview</span></span>
<span data-ttu-id="0399d-105">Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB.</span><span class="sxs-lookup"><span data-stu-id="0399d-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="0399d-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="0399d-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="0399d-107">Stockage d’objets BLOB est également référencé tooas stockage d’objets.</span><span class="sxs-lookup"><span data-stu-id="0399d-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="0399d-108">Ce guide va vous montrer comment tooperform des scénarios courants utilisant hello service de stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0399d-108">This guide will demonstrate how tooperform common scenarios using hello Azure Blob storage service.</span></span> <span data-ttu-id="0399d-109">exemples de Hello sont écrits en C++ et utiliser hello [bibliothèque cliente de stockage Azure pour C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="0399d-109">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="0399d-110">Hello scénarios abordés incluent **téléchargement**, **liste**, **téléchargement**, et **suppression** objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="0399d-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="0399d-111">Les cibles de ce guide hello bibliothèque cliente Azure Storage pour C++ version 1.0.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="0399d-111">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="0399d-112">Hello recommandé de version est la bibliothèque cliente de stockage 2.2.0, qui est disponible via [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="0399d-112">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="0399d-113">Création d’une application C++</span><span class="sxs-lookup"><span data-stu-id="0399d-113">Create a C++ application</span></span>
<span data-ttu-id="0399d-114">Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application C++.</span><span class="sxs-lookup"><span data-stu-id="0399d-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="0399d-115">toodo par conséquent, vous devez tooinstall hello bibliothèque cliente Azure Storage pour C++ et créer un compte de stockage Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0399d-115">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="0399d-116">tooinstall hello bibliothèque cliente Azure Storage pour C++, vous pouvez utiliser hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0399d-116">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="0399d-117">**Linux :** suivez instructions hello de hello [bibliothèque cliente de stockage Azure pour C++ Lisez-moi](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span><span class="sxs-lookup"><span data-stu-id="0399d-117">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="0399d-118">**Windows :** dans Visual Studio, cliquez sur **Outils &gt; Gestionnaire de package NuGet &gt; Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="0399d-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="0399d-119">Tapez ce qui suit hello commande dans hello [console du Gestionnaire de Package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="0399d-119">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="0399d-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="0399d-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="0399d-121">Configurer votre application de tooaccess stockage d’objets Blob</span><span class="sxs-lookup"><span data-stu-id="0399d-121">Configure your application tooaccess Blob Storage</span></span>
<span data-ttu-id="0399d-122">Ajouter suivant de hello inclure haut de toohello d’instructions de hello C++ fichier dans lequel le BLOB tooaccess API toouse hello stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="0399d-122">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="0399d-123">Configuration d’une chaîne de connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0399d-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="0399d-124">Un client de stockage Azure utilise une terminaison de stockage connexion chaîne toostore et informations d’identification pour accéder aux services de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="0399d-124">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="0399d-125">Lors de l’exécution dans une application cliente, vous devez fournir la chaîne de connexion de stockage hello Bonjour suivant le format, à l’aide du nom hello de votre compte et hello stockage clé d’accès de compte de stockage hello Bonjour [Azure Portal](https://portal.azure.com)pour hello *AccountName* et *AccountKey* valeurs.</span><span class="sxs-lookup"><span data-stu-id="0399d-125">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="0399d-126">Pour plus d'informations sur les comptes et les clés d'accès de stockage, consultez la page [À propos des comptes Azure Storage](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0399d-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="0399d-127">Cet exemple montre comment vous pouvez déclarer une chaîne de connexion de champ statique toohold hello :</span><span class="sxs-lookup"><span data-stu-id="0399d-127">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="0399d-128">tootest votre application sur votre ordinateur local de Windows, vous pouvez utiliser hello Microsoft Azure [l’émulateur de stockage](../storage-use-emulator.md) qui est installé avec hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0399d-128">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="0399d-129">l’émulateur de stockage Hello est un utilitaire qui simule hello Blob, file d’attente et Table services disponibles dans Azure sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="0399d-129">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="0399d-130">Hello suivant montre comment vous pouvez déclarer un champ statique toohold hello connexion chaîne tooyour local l’émulateur de stockage :</span><span class="sxs-lookup"><span data-stu-id="0399d-130">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="0399d-131">l’émulateur de stockage Azure hello toostart, sélectionnez hello **Démarrer** hello bouton ou appuyez sur **Windows** clé.</span><span class="sxs-lookup"><span data-stu-id="0399d-131">toostart hello Azure storage emulator, Select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="0399d-132">Commencez à taper **émulateur de stockage Azure**, puis sélectionnez **émulateur de stockage Microsoft Azure** à partir de la liste des applications hello.</span><span class="sxs-lookup"><span data-stu-id="0399d-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="0399d-133">Hello exemples suivants supposent que vous avez utilisé une de ces chaînes de connexion de stockage de deux méthodes tooget hello.</span><span class="sxs-lookup"><span data-stu-id="0399d-133">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="0399d-134">Récupération de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="0399d-134">Retrieve your connection string</span></span>
<span data-ttu-id="0399d-135">Vous pouvez utiliser hello **cloud_storage_account** classe toorepresent vos informations de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0399d-135">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="0399d-136">tooretrieve plus d’informations à partir de la chaîne de connexion de stockage hello du compte de votre stockage, vous pouvez utiliser hello **analyser** (méthode).</span><span class="sxs-lookup"><span data-stu-id="0399d-136">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="0399d-137">Ensuite, obtenez une référence tooa **cloud_blob_client** classe car elle vous permet de tooretrieve les objets qui représentent les conteneurs et objets BLOB stockés dans hello Service de stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="0399d-137">Next, get a reference tooa **cloud_blob_client** class as it allows you tooretrieve objects that represent containers and blobs stored within hello Blob Storage Service.</span></span> <span data-ttu-id="0399d-138">Hello de code suivant crée un **cloud_blob_client** objet à l’aide d’objet de compte de stockage hello nous récupérées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="0399d-138">hello following code creates a **cloud_blob_client** object using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="0399d-139">Création d’un conteneur</span><span class="sxs-lookup"><span data-stu-id="0399d-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="0399d-140">Cet exemple montre comment toocreate un conteneur s’il n’existe pas déjà :</span><span class="sxs-lookup"><span data-stu-id="0399d-140">This example shows how toocreate a container if it does not already exist:</span></span>  

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

<span data-ttu-id="0399d-141">Par défaut, conteneur hello est privé, et vous devez spécifier vos objets BLOB de stockage accès toodownload clé à partir de ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="0399d-141">By default, hello new container is private and you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="0399d-142">Si vous souhaitez que les fichiers hello toomake (BLOB) dans tooeveryone disponibles du conteneur hello, vous pouvez définir hello conteneur toobe public à l’aide de hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="0399d-142">If you want toomake hello files (blobs) within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="0399d-143">Toute personne sur Internet de hello peut voir les objets BLOB dans un conteneur public, mais vous pouvez modifier ou les supprimer que si vous disposez de la clé d’accès appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="0399d-143">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="0399d-144">Téléchargement d’un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="0399d-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="0399d-145">Le service de stockage d’objets blob Azure prend en charge les objets blob de blocs et de page.</span><span class="sxs-lookup"><span data-stu-id="0399d-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="0399d-146">Dans la majorité de hello des cas, objet blob de blocs est hello recommandé toouse de type.</span><span class="sxs-lookup"><span data-stu-id="0399d-146">In hello majority of cases, block blob is hello recommended type toouse.</span></span>  

<span data-ttu-id="0399d-147">tooupload fichier tooa objet blob de blocs, obtenir une référence de conteneur et utiliser tooget une référence d’objet blob de bloc.</span><span class="sxs-lookup"><span data-stu-id="0399d-147">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="0399d-148">Une fois que vous avez une référence d’objet blob, vous pouvez télécharger n’importe quel flux de données tooit en appelant hello **upload_from_stream** (méthode).</span><span class="sxs-lookup"><span data-stu-id="0399d-148">Once you have a blob reference, you can upload any stream of data tooit by calling hello **upload_from_stream** method.</span></span> <span data-ttu-id="0399d-149">Cette opération va créer l’objet blob de hello si elle n’a pas été précédemment existe, ou remplacer s’il existe.</span><span class="sxs-lookup"><span data-stu-id="0399d-149">This operation will create hello blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="0399d-150">Hello suivant montre l’exemple de comment tooupload un objet blob dans un conteneur et suppose que le conteneur de hello a déjà été créé.</span><span class="sxs-lookup"><span data-stu-id="0399d-150">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>  

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

<span data-ttu-id="0399d-151">Vous pouvez également utiliser hello **upload_from_file** tooupload de méthode objet blob de blocs tooa fichier.</span><span class="sxs-lookup"><span data-stu-id="0399d-151">Alternatively, you can use hello **upload_from_file** method tooupload a file tooa block blob.</span></span>

## <a name="how-to-list-hello-blobs-in-a-container"></a><span data-ttu-id="0399d-152">Comment : répertorier les objets BLOB de hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="0399d-152">How to: List hello blobs in a container</span></span>
<span data-ttu-id="0399d-153">objets BLOB de hello toolist dans un conteneur, d’abord obtenir une référence de conteneur.</span><span class="sxs-lookup"><span data-stu-id="0399d-153">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="0399d-154">Vous pouvez ensuite utiliser du conteneur hello **list_blobs** objets BLOB de méthode tooretrieve hello et/ou les répertoires qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="0399d-154">You can then use hello container's **list_blobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="0399d-155">tooaccess hello ensemble complet des propriétés et méthodes pour retourné **list_blob_item**, vous devez appeler hello **list_blob_item.as_blob** méthode tooget un **cloud_blob** objet, ou hello **list_blob.as_directory** méthode tooget un objet cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="0399d-155">tooaccess hello rich set of properties and methods for a returned **list_blob_item**, you must call hello **list_blob_item.as_blob** method tooget a  **cloud_blob** object, or hello **list_blob.as_directory** method tooget a  cloud_blob_directory object.</span></span> <span data-ttu-id="0399d-156">Hello de code suivant montre comment tooretrieve et sortie hello URI de chaque élément Bonjour **mon conteneur-exemple** conteneur :</span><span class="sxs-lookup"><span data-stu-id="0399d-156">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **my-sample-container** container:</span></span>

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

<span data-ttu-id="0399d-157">Pour plus d’informations sur les opérations de listage, consultez [Listage des ressources Azure Storage en C++](../storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="0399d-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="0399d-158">Téléchargement d’objets blob</span><span class="sxs-lookup"><span data-stu-id="0399d-158">How to: Download blobs</span></span>
<span data-ttu-id="0399d-159">objets BLOB toodownload, tout d’abord extraire une référence d’objet blob et ensuite appeler hello **download_to_stream** (méthode).</span><span class="sxs-lookup"><span data-stu-id="0399d-159">toodownload blobs, first retrieve a blob reference and then call hello **download_to_stream** method.</span></span> <span data-ttu-id="0399d-160">exemple Hello utilise hello **download_to_stream** méthode tootransfer hello contenu tooa flux de données objet blob que peuvent alors être conservées tooa des fichiers locaux.</span><span class="sxs-lookup"><span data-stu-id="0399d-160">hello following example uses hello **download_to_stream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>  

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

<span data-ttu-id="0399d-161">Vous pouvez également utiliser hello **download_to_file** contenu de hello méthode toodownload d’un fichier de tooa d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="0399d-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a blob tooa file.</span></span>
<span data-ttu-id="0399d-162">En outre, vous pouvez également utiliser hello **download_text** contenu de hello toodownload de méthode d’un objet blob comme une chaîne de texte.</span><span class="sxs-lookup"><span data-stu-id="0399d-162">In addition, you can also use hello **download_text** method toodownload hello contents of a blob as a text string.</span></span>  

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

## <a name="how-to-delete-blobs"></a><span data-ttu-id="0399d-163">Suppression d’objets blob</span><span class="sxs-lookup"><span data-stu-id="0399d-163">How to: Delete blobs</span></span>
<span data-ttu-id="0399d-164">tout d’abord obtenir une référence d’objet blob de toodelete un objet blob et ensuite appeler hello **delete_blob** méthode dessus.</span><span class="sxs-lookup"><span data-stu-id="0399d-164">toodelete a blob, first get a blob reference and then call hello **delete_blob** method on it.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="0399d-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0399d-165">Next steps</span></span>
<span data-ttu-id="0399d-166">Maintenant que vous avez appris les notions de base de hello du stockage blob, suivez ces liens de toolearn plus d’informations sur le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0399d-166">Now that you've learned hello basics of blob storage, follow these links toolearn more about Azure Storage.</span></span>  

* [<span data-ttu-id="0399d-167">Comment toouse stockage de file d’attente à partir de C++</span><span class="sxs-lookup"><span data-stu-id="0399d-167">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="0399d-168">Comment toouse le stockage de Table à partir de C++</span><span class="sxs-lookup"><span data-stu-id="0399d-168">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="0399d-169">Listage des ressources Azure Storage en C++</span><span class="sxs-lookup"><span data-stu-id="0399d-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="0399d-170">Référence de la bibliothèque cliente de stockage pour C++</span><span class="sxs-lookup"><span data-stu-id="0399d-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="0399d-171">Documentation d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0399d-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="0399d-172">Transfert de données avec hello utilitaire de ligne de commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="0399d-172">Transfer data with hello AzCopy command-line utility</span></span>](../storage-use-azcopy.md)

