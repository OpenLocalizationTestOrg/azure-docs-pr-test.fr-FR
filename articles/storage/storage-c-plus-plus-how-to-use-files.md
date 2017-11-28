---
title: "Développer pour le stockage de fichiers Azure avec C++ | Microsoft Docs"
description: "Apprenez à développer des services et applications C++ qui utilisent le stockage de fichiers Azure pour stocker les données de fichiers."
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: fc0d8451442f1337db4a36718c3fc746f8eb5125
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="0c07e-103">Développer pour le stockage de fichiers Azure avec C++</span><span class="sxs-lookup"><span data-stu-id="0c07e-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="0c07e-104">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="0c07e-104">About this tutorial</span></span>

<span data-ttu-id="0c07e-105">Ce didacticiel explique comment effectuer des opérations de base sur le service de stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="0c07e-105">In this tutorial, you'll learn how to perform basic operations on Azure File storage.</span></span> <span data-ttu-id="0c07e-106">Au moyen d’exemples écrits en C++, vous allez apprendre à créer des partages et des répertoires, ainsi qu’à charger, lister et supprimer des fichiers.</span><span class="sxs-lookup"><span data-stu-id="0c07e-106">Through samples written in C++, you'll learn how to create shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="0c07e-107">Si vous ne connaissez pas le stockage de fichiers Azure, l’étude des concepts abordés dans les sections suivantes vous sera utile pour comprendre les exemples.</span><span class="sxs-lookup"><span data-stu-id="0c07e-107">If you are new to Azure File storage , going through the concepts in the sections that follow will be helpful in understanding the samples.</span></span>


* <span data-ttu-id="0c07e-108">Créer et supprimer des partages de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="0c07e-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="0c07e-109">Créer et supprimer des répertoires</span><span class="sxs-lookup"><span data-stu-id="0c07e-109">Create and delete directories</span></span>
* <span data-ttu-id="0c07e-110">Énumérer des fichiers et répertoires dans un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="0c07e-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="0c07e-111">Charger, télécharger et supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="0c07e-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="0c07e-112">Définir le quota (taille maximale) d’un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="0c07e-112">Set the quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="0c07e-113">Créer une signature d’accès partagé pour un fichier qui utilise une stratégie d’accès partagé définie sur le partage</span><span class="sxs-lookup"><span data-stu-id="0c07e-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>

> [!Note]  
> <span data-ttu-id="0c07e-114">Étant donné que le stockage de fichiers Azure est accessible sur SMB, il est possible d’écrire de simples applications qui accèdent au partage de fichiers Azure à l’aide des fonctions et des classes d’E/S C++ standard.</span><span class="sxs-lookup"><span data-stu-id="0c07e-114">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard C++ I/O classes and functions.</span></span> <span data-ttu-id="0c07e-115">Cet article indique comment écrire des applications qui utilisent le kit de développement logiciel (SDK) C++ de stockage Azure, lequel utilise [l’API REST de stockage de fichiers Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) pour communiquer avec le stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="0c07e-115">This article will describe how to write applications that use the Azure Storage C++ SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="0c07e-116">Création d’une application C++</span><span class="sxs-lookup"><span data-stu-id="0c07e-116">Create a C++ application</span></span>
<span data-ttu-id="0c07e-117">Pour générer les exemples, vous devez installer la bibliothèque cliente de stockage Azure 2.4.0 pour C++.</span><span class="sxs-lookup"><span data-stu-id="0c07e-117">To build the samples, you will need to install the Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="0c07e-118">Vous devez également avoir préalablement créé un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0c07e-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="0c07e-119">Pour installer le client de stockage Azure 2.4.0 pour C++, vous pouvez utiliser l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0c07e-119">To install the Azure Storage Client 2.4.0 for C++, you can use one of the following methods:</span></span>

* <span data-ttu-id="0c07e-120">**Linux :** suivez les instructions disponibles sur la page [Bibliothèque cliente Azure Storage pour C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="0c07e-120">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="0c07e-121">**Windows :** dans Visual Studio, cliquez sur **Outils &gt; Gestionnaire de package NuGet &gt; Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="0c07e-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="0c07e-122">Entrez la commande suivante dans la [console du gestionnaire du package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur **ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="0c07e-122">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="0c07e-123">Configuration de votre application pour l’utilisation du stockage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="0c07e-123">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="0c07e-124">Ajoutez les instructions include suivantes au début du fichier source C++ dans lequel vous voulez manipuler le stockage de fichiers Azure :</span><span class="sxs-lookup"><span data-stu-id="0c07e-124">Add the following include statements to the top of the C++ source file where you want to manipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="0c07e-125">Configuration d’une chaîne de connexion au stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0c07e-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="0c07e-126">Pour pouvoir utiliser le stockage de fichiers, vous devez vous connecter à votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0c07e-126">To use File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="0c07e-127">La première étape consiste à configurer une chaîne de connexion, que nous allons utiliser pour nous connecter à votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0c07e-127">The first step would be to configure a connection string, which we'll use to connect to your storage account.</span></span> <span data-ttu-id="0c07e-128">Pour cela, nous allons définir une variable statique.</span><span class="sxs-lookup"><span data-stu-id="0c07e-128">Let's define a static variable to do that.</span></span>

```cpp
// Define the connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="0c07e-129">Connexion à un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0c07e-129">Connecting to an Azure storage account</span></span>
<span data-ttu-id="0c07e-130">Vous pouvez utiliser la classe **cloud_storage_account** pour représenter les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0c07e-130">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="0c07e-131">Pour extraire les informations de votre compte de stockage de la chaîne de connexion de stockage, vous pouvez utiliser la méthode **parse** .</span><span class="sxs-lookup"><span data-stu-id="0c07e-131">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="0c07e-132">Création d’un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="0c07e-132">Create an Azure File share</span></span>
<span data-ttu-id="0c07e-133">Tous les fichiers et répertoires d’un stockage de fichiers Azure se trouvent dans un conteneur appelé **Partage**.</span><span class="sxs-lookup"><span data-stu-id="0c07e-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="0c07e-134">Votre compte de stockage peut avoir autant de partages que le permet la capacité de votre compte.</span><span class="sxs-lookup"><span data-stu-id="0c07e-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="0c07e-135">Pour pouvoir accéder à un partage et à son contenu, vous devez utiliser un client de stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="0c07e-135">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```cpp
// Create the Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="0c07e-136">À l’aide de ce dernier, vous pouvez ensuite obtenir une référence à un partage.</span><span class="sxs-lookup"><span data-stu-id="0c07e-136">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```cpp
// Get a reference to the file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="0c07e-137">Pour créer le partage, utilisez la méthode **create_if_not_exists** de l’objet **cloud_file_share**.</span><span class="sxs-lookup"><span data-stu-id="0c07e-137">To create the share, use the **create_if_not_exists** method of the **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="0c07e-138">À ce stade, le **partage** contient une référence à un partage nommé **my-sample-share**.</span><span class="sxs-lookup"><span data-stu-id="0c07e-138">At this point, **share** holds a reference to a share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="0c07e-139">Suppression d’un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="0c07e-139">Delete an Azure File share</span></span>
<span data-ttu-id="0c07e-140">La suppression d’un partage s’effectue en appelant la méthode **delete_if_exists** sur un objet cloud_file_share.</span><span class="sxs-lookup"><span data-stu-id="0c07e-140">Deleting a share is done by calling the **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="0c07e-141">Voici un exemple de code permettant d’effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="0c07e-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete the share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="0c07e-142">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="0c07e-142">Create a directory</span></span>
<span data-ttu-id="0c07e-143">Vous pouvez organiser le stockage en plaçant des fichiers dans des sous-répertoires, plutôt que de tous les mettre dans le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="0c07e-143">You can organize storage by putting files inside subdirectories instead of having all of them in the root directory.</span></span> <span data-ttu-id="0c07e-144">Le stockage de fichiers Azure vous permet de créer autant de répertoires que le permet votre compte.</span><span class="sxs-lookup"><span data-stu-id="0c07e-144">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="0c07e-145">Le code ci-dessous crée un répertoire nommé **my-sample-directory** sous le répertoire racine, ainsi qu’un sous-répertoire nommé **my-sample-subdirectory**.</span><span class="sxs-lookup"><span data-stu-id="0c07e-145">The code below will create a directory named **my-sample-directory** under the root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference to a directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if the share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="0c07e-146">Supprimer un répertoire</span><span class="sxs-lookup"><span data-stu-id="0c07e-146">Delete a directory</span></span>
<span data-ttu-id="0c07e-147">La suppression d’un répertoire est une tâche simple, mais il convient de noter que vous ne pouvez pas supprimer de répertoire contenant des fichiers ou d’autres répertoires.</span><span class="sxs-lookup"><span data-stu-id="0c07e-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference to the directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference to the subdirectory you want to delete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete the subdirectory and the sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="0c07e-148">Énumérer des fichiers et répertoires dans un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="0c07e-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="0c07e-149">Il est facile d’obtenir la liste de fichiers et de répertoires d’un partage en appelant **list_files_and_directories** sur une référence **cloud_file_directory**.</span><span class="sxs-lookup"><span data-stu-id="0c07e-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="0c07e-150">Pour accéder à l’ensemble complet des propriétés et méthodes d’un **list_file_and_directory_item** renvoyé, vous devez appeler la méthode **list_file_and_directory_item.as_file** afin d’obtenir un objet **cloud_file** ou la méthode **list_file_and_directory_item.as_directory** afin d’obtenir un objet **cloud_file_directory**.</span><span class="sxs-lookup"><span data-stu-id="0c07e-150">To access the rich set of properties and methods for a returned **list_file_and_directory_item**, you must call the **list_file_and_directory_item.as_file** method to get a **cloud_file** object, or the **list_file_and_directory_item.as_directory** method to get a **cloud_file_directory** object.</span></span>

<span data-ttu-id="0c07e-151">Le code suivant illustre la récupération et la génération de l’URI de chaque élément du répertoire racine du partage.</span><span class="sxs-lookup"><span data-stu-id="0c07e-151">The following code demonstrates how to retrieve and output the URI of each item in the root directory of the share.</span></span>

```cpp
//Get a reference to the root directory for the share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a><span data-ttu-id="0c07e-152">Charger un fichier</span><span class="sxs-lookup"><span data-stu-id="0c07e-152">Upload a file</span></span>
<span data-ttu-id="0c07e-153">Un partage de fichiers Azure contient au minimum un répertoire racine dans lequel les fichiers peuvent résider.</span><span class="sxs-lookup"><span data-stu-id="0c07e-153">At the very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="0c07e-154">Cette section décrit comment télécharger un fichier du stockage local vers le répertoire racine d’un partage.</span><span class="sxs-lookup"><span data-stu-id="0c07e-154">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="0c07e-155">La première étape du téléchargement d’un fichier consiste à obtenir une référence au répertoire dans lequel ce fichier doit résider.</span><span class="sxs-lookup"><span data-stu-id="0c07e-155">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="0c07e-156">Pour cela, vous devez appeler la méthode **get_root_directory_reference** de l’objet de partage.</span><span class="sxs-lookup"><span data-stu-id="0c07e-156">You do this by calling the **get_root_directory_reference** method of the share object.</span></span>

```cpp
//Get a reference to the root directory for the share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="0c07e-157">Maintenant que vous avez une référence au répertoire racine du partage, vous pouvez télécharger un fichier vers ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="0c07e-157">Now that you have a reference to the root directory of the share, you can upload a file onto it.</span></span> <span data-ttu-id="0c07e-158">Cet exemple télécharge à partir d’un fichier, d’un texte et d’un flux.</span><span class="sxs-lookup"><span data-stu-id="0c07e-158">This example uploads from a file, from text, and from a stream.</span></span>

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a><span data-ttu-id="0c07e-159">Téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="0c07e-159">Download a file</span></span>
<span data-ttu-id="0c07e-160">Pour télécharger des fichiers, commencez par récupérer une référence de fichier, puis appelez la méthode **download_to_stream** pour transférer le contenu du fichier vers un objet de flux, que vous pouvez enregistrer sous forme de fichier local.</span><span class="sxs-lookup"><span data-stu-id="0c07e-160">To download files, first retrieve a file reference and then call the **download_to_stream** method to transfer the file contents to a stream object, which you can then persist to a local file.</span></span> <span data-ttu-id="0c07e-161">Vous pouvez également utiliser la méthode **download_to_file** pour télécharger le contenu d’un fichier dans un fichier local.</span><span class="sxs-lookup"><span data-stu-id="0c07e-161">Alternatively, you can use the **download_to_file** method to download the contents of a file to a local file.</span></span> <span data-ttu-id="0c07e-162">Vous pouvez utiliser la méthode **download_text** pour télécharger le contenu d’un fichier en tant que chaîne de texte.</span><span class="sxs-lookup"><span data-stu-id="0c07e-162">You can use the **download_text** method to download the contents of a file as a text string.</span></span>

<span data-ttu-id="0c07e-163">L’exemple suivant utilise les méthodes **download_to_stream** et **download_text** afin d’illustrer le téléchargement des fichiers, qui ont été créés dans les sections précédentes.</span><span class="sxs-lookup"><span data-stu-id="0c07e-163">The following example uses the **download_to_stream** and **download_text** methods to demonstrate downloading the files, which were created in previous sections.</span></span>

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a><span data-ttu-id="0c07e-164">Supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="0c07e-164">Delete a file</span></span>
<span data-ttu-id="0c07e-165">La suppression de fichiers est également une opération courante liée au stockage des fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="0c07e-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="0c07e-166">Le code suivant supprime un fichier nommé my-sample-file-3 stocké dans le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="0c07e-166">The following code deletes a file named my-sample-file-3 stored under the root directory.</span></span>

```cpp
// Get a reference to the root directory for the share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-the-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="0c07e-167">Définir le quota (taille maximale) d’un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="0c07e-167">Set the quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="0c07e-168">Vous pouvez définir le quota (ou la taille maximale) pour un partage de fichiers, en gigaoctets.</span><span class="sxs-lookup"><span data-stu-id="0c07e-168">You can set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="0c07e-169">Vous pouvez également vérifier la quantité de données actuellement stockée sur le partage.</span><span class="sxs-lookup"><span data-stu-id="0c07e-169">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="0c07e-170">En définissant le quota pour un partage, vous pouvez limiter la taille totale des fichiers stockés sur ce partage.</span><span class="sxs-lookup"><span data-stu-id="0c07e-170">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="0c07e-171">Si la taille totale des fichiers sur le partage dépasse le quota défini sur celui-ci, les clients ne peuvent pas augmenter la taille des fichiers existants ou créer des fichiers, sauf si ces fichiers sont vides.</span><span class="sxs-lookup"><span data-stu-id="0c07e-171">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="0c07e-172">L’exemple ci-dessous illustre comment vérifier l’utilisation actuelle pour un partage et comment définir le quota pour le partage.</span><span class="sxs-lookup"><span data-stu-id="0c07e-172">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets the quota to 2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="0c07e-173">Génération d’une signature d’accès partagé pour un fichier ou partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="0c07e-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="0c07e-174">Vous pouvez générer une signature d’accès partagé (SAP) pour un partage de fichiers ou un fichier individuel.</span><span class="sxs-lookup"><span data-stu-id="0c07e-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="0c07e-175">Vous pouvez également créer une stratégie d’accès partagé sur un partage de fichiers pour gérer les signatures d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="0c07e-175">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="0c07e-176">Créer une stratégie d’accès partagé est recommandé, car cette opération permet de révoquer la SAP si elle doit être compromise.</span><span class="sxs-lookup"><span data-stu-id="0c07e-176">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="0c07e-177">L’exemple suivant crée une stratégie d’accès partagé sur un partage, puis utilise cette stratégie pour fournir les contraintes pour une SAP sur un fichier du partage.</span><span class="sxs-lookup"><span data-stu-id="0c07e-177">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client and get a reference to the share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions to expire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for the share
    azure::storage::file_share_permissions permissions;    

    //retrieve the current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add the new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save the updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve the root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in the share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from the SAS, and write some text to the file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="0c07e-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0c07e-178">Next steps</span></span>
<span data-ttu-id="0c07e-179">Pour en savoir plus sur Azure Storage, explorez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="0c07e-179">To learn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="0c07e-180">Bibliothèque cliente de stockage pour C++</span><span class="sxs-lookup"><span data-stu-id="0c07e-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="0c07e-181">[Exemples de service de fichier de Stockage Azure en C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="0c07e-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="0c07e-182">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="0c07e-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="0c07e-183">Documentation d'Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0c07e-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)