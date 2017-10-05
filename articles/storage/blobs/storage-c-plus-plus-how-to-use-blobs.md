---
title: "Utilisation du stockage d’objets blob à partir de C++ | Microsoft Docs"
description: "Stockez des données non structurées dans le cloud avec Azure Blob Storage (stockage d’objets)."
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
ms.openlocfilehash: daf480b7be78dc001712010eac6386d4744c3c1d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-c"></a><span data-ttu-id="c1e9e-103">Utilisation du stockage d'objets blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="c1e9e-103">How to use Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="c1e9e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c1e9e-104">Overview</span></span>
<span data-ttu-id="c1e9e-105">Le stockage d’objets blob Azure est un service qui stocke des données non structurées dans le cloud en tant qu’objets/blobs.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="c1e9e-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="c1e9e-107">Le stockage d’objets blob est également appelé Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="c1e9e-108">Ce guide explique le déroulement des scénarios courants dans le cadre de l’utilisation du service de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span></span> <span data-ttu-id="c1e9e-109">Les exemples ont été écrits en C++ et utilisent la [bibliothèque cliente Azure Storage pour C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="c1e9e-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="c1e9e-110">Les scénarios traités incluent le **chargement**, l’**énumération**, le **téléchargement** et la **suppression** d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="c1e9e-111">Ce guide cible la bibliothèque cliente Azure Storage pour C++ version 1.0.0 et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="c1e9e-112">La version recommandée est la bibliothèque cliente de stockage version 2.2.0, disponible par le biais de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="c1e9e-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="c1e9e-113">Création d’une application C++</span><span class="sxs-lookup"><span data-stu-id="c1e9e-113">Create a C++ application</span></span>
<span data-ttu-id="c1e9e-114">Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application C++.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="c1e9e-115">Pour ce faire, vous devez installer la bibliothèque cliente Azure Storage pour C++ et créer un compte Azure Storage dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="c1e9e-116">Pour installer la bibliothèque cliente Azure Storage pour C++, vous pouvez procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="c1e9e-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="c1e9e-117">**Linux :** suivez les instructions disponibles sur la page [Bibliothèque cliente Azure Storage pour C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="c1e9e-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="c1e9e-118">**Windows :** dans Visual Studio, cliquez sur **Outils > Gestionnaire de package NuGet > Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="c1e9e-119">Entrez la commande suivante dans la [console du gestionnaire du package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur **ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="c1e9e-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="c1e9e-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="c1e9e-121">Configuration de votre application pour accéder au stockage d'objets blob</span><span class="sxs-lookup"><span data-stu-id="c1e9e-121">Configure your application to access Blob Storage</span></span>
<span data-ttu-id="c1e9e-122">Ajoutez l'instruction include suivante au début du fichier C++ dans lequel vous voulez utiliser des API de stockage Azure pour accéder aux objets blob :</span><span class="sxs-lookup"><span data-stu-id="c1e9e-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="c1e9e-123">Configuration d’une chaîne de connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c1e9e-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="c1e9e-124">Un client de stockage Azure utilise une chaîne de connexion de stockage pour stocker des points de terminaison et des informations d’identification permettant d’accéder aux services de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="c1e9e-125">Lors de l’exécution d’une application cliente, vous devez spécifier la chaîne de connexion au stockage au format suivant, en indiquant le nom de votre compte de stockage et sa clé d’accès de stockage, correspondant aux valeurs *AccountName* et *AccountKey*, sur le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c1e9e-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="c1e9e-126">Pour plus d'informations sur les comptes et les clés d'accès de stockage, consultez la page [À propos des comptes Azure Storage](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1e9e-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="c1e9e-127">Cet exemple vous montre comment déclarer un champ statique pour qu’il contienne une chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="c1e9e-127">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="c1e9e-128">Pour tester votre application sur votre ordinateur Windows local, vous pouvez utiliser [l’émulateur de stockage Microsoft Azure](../storage-use-emulator.md) installé avec le [Kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c1e9e-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="c1e9e-129">L'émulateur de stockage est un utilitaire qui simule sur votre ordinateur de développement local les objets blob, les files d'attente et les services de Table disponibles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="c1e9e-130">L’exemple suivant vous montre comment déclarer un champ statique pour qu’il contienne une chaîne de connexion vers votre émulateur de stockage local :</span><span class="sxs-lookup"><span data-stu-id="c1e9e-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="c1e9e-131">Pour démarrer l’émulateur de stockage Azure, sélectionnez le bouton **Démarrer** ou appuyez sur la touche **Windows**.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="c1e9e-132">Commencez à taper **Émulateur de stockage Azure**, puis sélectionnez **Émulateur de stockage Microsoft Azure** dans la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="c1e9e-133">Les exemples ci-dessous partent du principe que vous avez utilisé l’une de ces deux méthodes pour obtenir la chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="c1e9e-134">Récupération de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="c1e9e-134">Retrieve your connection string</span></span>
<span data-ttu-id="c1e9e-135">Vous pouvez utiliser la classe **cloud_storage_account** pour représenter les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="c1e9e-136">Pour extraire les informations de votre compte de stockage de la chaîne de connexion de stockage, vous pouvez utiliser la méthode **parse** .</span><span class="sxs-lookup"><span data-stu-id="c1e9e-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="c1e9e-137">Ensuite, récupérez une référence pointant vers une classe **cloud_blob_client**, car elle permet de récupérer des objets représentant des conteneurs et des objets blob stockés dans le serveur de stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span></span> <span data-ttu-id="c1e9e-138">Le code suivant crée un objet **cloud_blob_client** en utilisant l’objet de compte de stockage récupéré ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="c1e9e-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span></span>  

```cpp
// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="c1e9e-139">Création d’un conteneur</span><span class="sxs-lookup"><span data-stu-id="c1e9e-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="c1e9e-140">Cet exemple montre comment créer un conteneur, si celui-ci n’existe pas encore :</span><span class="sxs-lookup"><span data-stu-id="c1e9e-140">This example shows how to create a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create the blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference to a container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create the container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="c1e9e-141">Le nouveau conteneur est privé par défaut et vous devez indiquer votre clé d'accès de stockage pour télécharger des objets blob depuis ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="c1e9e-142">Si vous voulez que les fichiers (objets blob) du conteneur soient publics, vous pouvez configurer le conteneur en utilisant le code suivant :</span><span class="sxs-lookup"><span data-stu-id="c1e9e-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span></span>  

```cpp
// Make the blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="c1e9e-143">Tous les utilisateurs d’Internet peuvent afficher les objets blob d’un conteneur public, mais seuls ceux possédant la clé d’accès adéquate peuvent les modifier ou les supprimer.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="c1e9e-144">Téléchargement d’un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="c1e9e-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="c1e9e-145">Le service de stockage d’objets blob Azure prend en charge les objets blob de blocs et de page.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="c1e9e-146">Dans la plupart des cas, il est recommandé d’utiliser le type d’objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-146">In the majority of cases, block blob is the recommended type to use.</span></span>  

<span data-ttu-id="c1e9e-147">Pour télécharger un fichier vers un objet blob de blocs, obtenez une référence de conteneur et utilisez-la pour obtenir une référence d’objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="c1e9e-148">Lorsque vous disposez d’une référence d’objet blob, vous pouvez télécharger un flux de données vers cet objet en appelant la méthode **upload_from_stream**.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span></span> <span data-ttu-id="c1e9e-149">Si l’objet blob n’existe pas, cette opération entraîne sa création. S’il existe, il est remplacé.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="c1e9e-150">L’exemple suivant illustre le téléchargement d’un objet blob dans un conteneur en partant du principe que le conteneur existe déjà.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite the "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite the "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference to a blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="c1e9e-151">Vous pouvez également utiliser la méthode **upload_from_file** pour télécharger un fichier vers un objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span></span>

## <a name="how-to-list-the-blobs-in-a-container"></a><span data-ttu-id="c1e9e-152">Création d’une liste d’objets blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="c1e9e-152">How to: List the blobs in a container</span></span>
<span data-ttu-id="c1e9e-153">Pour créer une liste d’objets blob dans un conteneur, commencez par obtenir une référence pointant vers un conteneur.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-153">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="c1e9e-154">Vous pouvez ensuite utiliser la méthode **list_blobs** du conteneur pour récupérer les objets blob et/ou les répertoires qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="c1e9e-155">Pour accéder à l’ensemble complet des propriétés et méthodes d’un **list_blob_item** renvoyé, vous devez appeler la méthode **list_blob_item.as_blob** afin d’obtenir un objet **cloud_blob** ou la méthode **list_blob.as_directory** afin d’obtenir un objet cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span></span> <span data-ttu-id="c1e9e-156">Le code suivant illustre la récupération et la génération de l'URI de chaque élément du conteneur **my-sample-container** :</span><span class="sxs-lookup"><span data-stu-id="c1e9e-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
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

<span data-ttu-id="c1e9e-157">Pour plus d’informations sur les opérations de listage, consultez [Listage des ressources Azure Storage en C++](../storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="c1e9e-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="c1e9e-158">Téléchargement d’objets blob</span><span class="sxs-lookup"><span data-stu-id="c1e9e-158">How to: Download blobs</span></span>
<span data-ttu-id="c1e9e-159">Pour télécharger des objets blob, commencez par récupérer une référence d’objet blob, puis appelez la méthode **download_to_stream**.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span></span> <span data-ttu-id="c1e9e-160">L’exemple suivant utilise la méthode **download_to_stream** pour transférer les contenus d’objets blob vers un objet de flux pouvant être rendu persistant dans un fichier local.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents to a file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="c1e9e-161">Vous pouvez également utiliser la méthode **download_to_file** pour télécharger le contenu d’un objet blob dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span></span>
<span data-ttu-id="c1e9e-162">De plus, vous pouvez aussi utiliser la méthode **download_text** pour télécharger le contenu d’un objet blob en tant que chaîne de texte.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download the contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="c1e9e-163">Suppression d’objets blob</span><span class="sxs-lookup"><span data-stu-id="c1e9e-163">How to: Delete blobs</span></span>
<span data-ttu-id="c1e9e-164">Pour supprimer un objet blob, commencez par obtenir une référence d’objet blob, puis appelez la méthode **delete_blob** associée.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete the blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="c1e9e-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1e9e-165">Next steps</span></span>
<span data-ttu-id="c1e9e-166">Maintenant que vous connaissez les bases du stockage d'objets blob, consultez les liens suivants pour en savoir plus sur Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c1e9e-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span></span>  

* [<span data-ttu-id="c1e9e-167">Utilisation du service de stockage de files d'attente à partir de C++</span><span class="sxs-lookup"><span data-stu-id="c1e9e-167">How to use Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="c1e9e-168">Utilisation du stockage de tables à partir de C++</span><span class="sxs-lookup"><span data-stu-id="c1e9e-168">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="c1e9e-169">Listage des ressources Azure Storage en C++</span><span class="sxs-lookup"><span data-stu-id="c1e9e-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="c1e9e-170">Référence de la bibliothèque cliente de stockage pour C++</span><span class="sxs-lookup"><span data-stu-id="c1e9e-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="c1e9e-171">Documentation d'Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c1e9e-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="c1e9e-172">Transfert de données avec l’utilitaire de ligne de commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="c1e9e-172">Transfer data with the AzCopy command-line utility</span></span>](../storage-use-azcopy.md)

