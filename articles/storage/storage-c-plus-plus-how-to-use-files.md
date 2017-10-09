---
title: aaaDevelop pour le stockage de fichiers Azure avec C++ | Documents Microsoft
description: "Découvrez comment toodevelop C++ applications et services qui utilisent des fichiers Azure storage toostore fichier de données."
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
ms.openlocfilehash: 40c3aac94214a91121913e2ded315031aeed1c30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="8b2df-103">Développer pour le stockage de fichiers Azure avec C++</span><span class="sxs-lookup"><span data-stu-id="8b2df-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="8b2df-104">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="8b2df-104">About this tutorial</span></span>

<span data-ttu-id="8b2df-105">Dans ce didacticiel, vous allez apprendre comment tooperform les opérations de base sur le stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="8b2df-105">In this tutorial, you'll learn how tooperform basic operations on Azure File storage.</span></span> <span data-ttu-id="8b2df-106">Via exemples écrits en C++, vous allez apprendre comment toocreate partage et de répertoires, télécharger, liste et supprimer des fichiers.</span><span class="sxs-lookup"><span data-stu-id="8b2df-106">Through samples written in C++, you'll learn how toocreate shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="8b2df-107">Si vous êtes de nouveau stockage de fichier tooAzure, traverser des concepts hello dans les sections hello qui suivent sera utile pour comprendre les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="8b2df-107">If you are new tooAzure File storage , going through hello concepts in hello sections that follow will be helpful in understanding hello samples.</span></span>


* <span data-ttu-id="8b2df-108">Créer et supprimer des partages de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="8b2df-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="8b2df-109">Créer et supprimer des répertoires</span><span class="sxs-lookup"><span data-stu-id="8b2df-109">Create and delete directories</span></span>
* <span data-ttu-id="8b2df-110">Énumérer des fichiers et répertoires dans un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="8b2df-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="8b2df-111">Charger, télécharger et supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="8b2df-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="8b2df-112">Définir le quota de hello (taille maximale) pour un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="8b2df-112">Set hello quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="8b2df-113">Créer une signature d’accès partagé (clé SAS) pour un fichier qui utilise une stratégie d’accès partagé définie sur le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="8b2df-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>

> [!Note]  
> <span data-ttu-id="8b2df-114">Stockage de fichiers Azure sont accessibles sur SMB, il est toowrite possible les applications simples qui accéder au partage de fichiers Azure hello à l’aide des fonctions et classes C++ d’e/s standards de hello.</span><span class="sxs-lookup"><span data-stu-id="8b2df-114">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard C++ I/O classes and functions.</span></span> <span data-ttu-id="8b2df-115">Cet article décrit comment toowrite les applications qui utilisent hello SDK Azure Storage C++, qui utilise hello [le stockage de fichiers Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="8b2df-115">This article will describe how toowrite applications that use hello Azure Storage C++ SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="8b2df-116">Création d’une application C++</span><span class="sxs-lookup"><span data-stu-id="8b2df-116">Create a C++ application</span></span>
<span data-ttu-id="8b2df-117">exemples de hello toobuild, vous devez tooinstall hello bibliothèque cliente de stockage Azure 2.4.0 pour C++.</span><span class="sxs-lookup"><span data-stu-id="8b2df-117">toobuild hello samples, you will need tooinstall hello Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="8b2df-118">Vous devez également avoir préalablement créé un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8b2df-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="8b2df-119">tooinstall hello Client de stockage Azure 2.4.0 pour C++, vous pouvez utiliser une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="8b2df-119">tooinstall hello Azure Storage Client 2.4.0 for C++, you can use one of hello following methods:</span></span>

* <span data-ttu-id="8b2df-120">**Linux :** suivez instructions hello de hello [bibliothèque cliente de stockage Azure pour C++ Lisez-moi](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span><span class="sxs-lookup"><span data-stu-id="8b2df-120">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="8b2df-121">**Windows :** dans Visual Studio, cliquez sur **Outils &gt; Gestionnaire de package NuGet &gt; Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="8b2df-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="8b2df-122">Tapez ce qui suit hello commande dans hello [console du Gestionnaire de Package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="8b2df-122">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="8b2df-123">Configurer votre toouse application stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8b2df-123">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="8b2df-124">Ajouter suivant de hello inclure haut de toohello instructions du fichier source de hello C++ où vous souhaitez le stockage de fichiers Azure toomanipulate :</span><span class="sxs-lookup"><span data-stu-id="8b2df-124">Add hello following include statements toohello top of hello C++ source file where you want toomanipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="8b2df-125">Configuration d’une chaîne de connexion au stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8b2df-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="8b2df-126">toouse stockage de fichiers, vous avez besoin de compte de stockage Azure tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="8b2df-126">toouse File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="8b2df-127">Hello première étape serait tooconfigure une chaîne de connexion, que nous allons utiliser compte de stockage tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="8b2df-127">hello first step would be tooconfigure a connection string, which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="8b2df-128">Nous allons définir une toodo variable statique qui.</span><span class="sxs-lookup"><span data-stu-id="8b2df-128">Let's define a static variable toodo that.</span></span>

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="8b2df-129">Connexion de compte de stockage Azure tooan</span><span class="sxs-lookup"><span data-stu-id="8b2df-129">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="8b2df-130">Vous pouvez utiliser hello **cloud_storage_account** classe toorepresent vos informations de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8b2df-130">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="8b2df-131">tooretrieve plus d’informations à partir de la chaîne de connexion de stockage hello du compte de votre stockage, vous pouvez utiliser hello **analyser** (méthode).</span><span class="sxs-lookup"><span data-stu-id="8b2df-131">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="8b2df-132">Création d’un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="8b2df-132">Create an Azure File share</span></span>
<span data-ttu-id="8b2df-133">Tous les fichiers et répertoires d’un stockage de fichiers Azure se trouvent dans un conteneur appelé **Partage**.</span><span class="sxs-lookup"><span data-stu-id="8b2df-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="8b2df-134">Votre compte de stockage peut avoir autant de partages que le permet la capacité de votre compte.</span><span class="sxs-lookup"><span data-stu-id="8b2df-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="8b2df-135">partage de tooa accès tooobtain et son contenu, vous devez toouse un client de stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="8b2df-135">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="8b2df-136">À l’aide du client de stockage de fichier Azure hello, vous pouvez ensuite obtenir un partage de tooa de référence.</span><span class="sxs-lookup"><span data-stu-id="8b2df-136">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="8b2df-137">partage de hello toocreate, utilisez hello **create_if_not_exists** méthode Hello **cloud_file_share** objet.</span><span class="sxs-lookup"><span data-stu-id="8b2df-137">toocreate hello share, use hello **create_if_not_exists** method of hello **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="8b2df-138">À ce stade, **partager** contient un partage de tooa référence nommé **mon exemple-partage**.</span><span class="sxs-lookup"><span data-stu-id="8b2df-138">At this point, **share** holds a reference tooa share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="8b2df-139">Suppression d’un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="8b2df-139">Delete an Azure File share</span></span>
<span data-ttu-id="8b2df-140">Suppression d’un partage est effectuée en appelant hello **delete_if_exists** méthode sur un objet cloud_file_share.</span><span class="sxs-lookup"><span data-stu-id="8b2df-140">Deleting a share is done by calling hello **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="8b2df-141">Voici un exemple de code permettant d’effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="8b2df-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="8b2df-142">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="8b2df-142">Create a directory</span></span>
<span data-ttu-id="8b2df-143">Vous pouvez organiser le stockage en plaçant les fichiers à l’intérieur des sous-répertoires au lieu d’avoir tous les dans le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="8b2df-143">You can organize storage by putting files inside subdirectories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="8b2df-144">Stockage de fichier Azure vous permet de toocreate car autorise de nombreux répertoires car votre compte.</span><span class="sxs-lookup"><span data-stu-id="8b2df-144">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="8b2df-145">code Hello ci-dessous crée un répertoire nommé **répertoire Mes exemple** sous le répertoire racine de hello ainsi que d’un sous-répertoire nommé **mon exemple-sous-répertoire**.</span><span class="sxs-lookup"><span data-stu-id="8b2df-145">hello code below will create a directory named **my-sample-directory** under hello root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="8b2df-146">Supprimer un répertoire</span><span class="sxs-lookup"><span data-stu-id="8b2df-146">Delete a directory</span></span>
<span data-ttu-id="8b2df-147">La suppression d’un répertoire est une tâche simple, mais il convient de noter que vous ne pouvez pas supprimer de répertoire contenant des fichiers ou d’autres répertoires.</span><span class="sxs-lookup"><span data-stu-id="8b2df-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="8b2df-148">Énumérer des fichiers et répertoires dans un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="8b2df-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="8b2df-149">Il est facile d’obtenir la liste de fichiers et de répertoires d’un partage en appelant **list_files_and_directories** sur une référence **cloud_file_directory**.</span><span class="sxs-lookup"><span data-stu-id="8b2df-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="8b2df-150">tooaccess hello ensemble complet des propriétés et méthodes pour retourné **list_file_and_directory_item**, vous devez appeler hello **list_file_and_directory_item.as_file** méthode tooget un **cloud_ fichier** objet ou hello **list_file_and_directory_item.as_directory** méthode tooget un **cloud_file_directory** objet.</span><span class="sxs-lookup"><span data-stu-id="8b2df-150">tooaccess hello rich set of properties and methods for a returned **list_file_and_directory_item**, you must call hello **list_file_and_directory_item.as_file** method tooget a **cloud_file** object, or hello **list_file_and_directory_item.as_directory** method tooget a **cloud_file_directory** object.</span></span>

<span data-ttu-id="8b2df-151">Hello suivant de code montre comment tooretrieve et sortie hello URI de chaque élément dans le répertoire racine de hello du partage de hello.</span><span class="sxs-lookup"><span data-stu-id="8b2df-151">hello following code demonstrates how tooretrieve and output hello URI of each item in hello root directory of hello share.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
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

## <a name="upload-a-file"></a><span data-ttu-id="8b2df-152">Charger un fichier</span><span class="sxs-lookup"><span data-stu-id="8b2df-152">Upload a file</span></span>
<span data-ttu-id="8b2df-153">À hello très moins, un partage de fichiers Azure contient un répertoire racine où les fichiers peuvent résider.</span><span class="sxs-lookup"><span data-stu-id="8b2df-153">At hello very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="8b2df-154">Dans cette section, vous allez apprendre comment tooupload un fichier à partir du stockage local sur hello racine du répertoire d’un partage.</span><span class="sxs-lookup"><span data-stu-id="8b2df-154">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="8b2df-155">première étape de Hello lors du téléchargement d’un fichier est tooobtain un répertoire toohello de référence où elle doit résider.</span><span class="sxs-lookup"><span data-stu-id="8b2df-155">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="8b2df-156">Pour ce faire, l’appelant hello **get_root_directory_reference** méthode d’objet de partage hello.</span><span class="sxs-lookup"><span data-stu-id="8b2df-156">You do this by calling hello **get_root_directory_reference** method of hello share object.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="8b2df-157">Maintenant que vous avez un répertoire de racine référence toohello du partage de hello, vous pouvez télécharger un fichier sur lui.</span><span class="sxs-lookup"><span data-stu-id="8b2df-157">Now that you have a reference toohello root directory of hello share, you can upload a file onto it.</span></span> <span data-ttu-id="8b2df-158">Cet exemple télécharge à partir d’un fichier, d’un texte et d’un flux.</span><span class="sxs-lookup"><span data-stu-id="8b2df-158">This example uploads from a file, from text, and from a stream.</span></span>

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

## <a name="download-a-file"></a><span data-ttu-id="8b2df-159">Téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="8b2df-159">Download a file</span></span>
<span data-ttu-id="8b2df-160">les fichiers toodownload, tout d’abord extraire une référence de fichier et appelez ensuite hello **download_to_stream** méthode tootransfer hello fichier contenu tooa objet de flux, ce qui vous pouvez alors être conservées tooa des fichiers locaux.</span><span class="sxs-lookup"><span data-stu-id="8b2df-160">toodownload files, first retrieve a file reference and then call hello **download_to_stream** method tootransfer hello file contents tooa stream object, which you can then persist tooa local file.</span></span> <span data-ttu-id="8b2df-161">Vous pouvez également utiliser hello **download_to_file** contenu de hello méthode toodownload d’un fichier local tooa.</span><span class="sxs-lookup"><span data-stu-id="8b2df-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a file tooa local file.</span></span> <span data-ttu-id="8b2df-162">Vous pouvez utiliser hello **download_text** contenu de hello méthode toodownload d’un fichier comme une chaîne de texte.</span><span class="sxs-lookup"><span data-stu-id="8b2df-162">You can use hello **download_text** method toodownload hello contents of a file as a text string.</span></span>

<span data-ttu-id="8b2df-163">exemple Hello utilise hello **download_to_stream** et **download_text** toodemonstrate méthodes téléchargement de fichiers hello, qui ont été créées dans les sections précédentes.</span><span class="sxs-lookup"><span data-stu-id="8b2df-163">hello following example uses hello **download_to_stream** and **download_text** methods toodemonstrate downloading hello files, which were created in previous sections.</span></span>

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

## <a name="delete-a-file"></a><span data-ttu-id="8b2df-164">Supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="8b2df-164">Delete a file</span></span>
<span data-ttu-id="8b2df-165">La suppression de fichiers est également une opération courante liée au stockage des fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="8b2df-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="8b2df-166">Hello de code suivant supprime un fichier nommé my-exemple-fichier-3 stocké sous le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="8b2df-166">hello following code deletes a file named my-sample-file-3 stored under hello root directory.</span></span>

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="8b2df-167">Définir le quota de hello (taille maximale) pour un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="8b2df-167">Set hello quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="8b2df-168">Vous pouvez définir le quota de hello (ou la taille maximale) pour un partage de fichiers, en gigaoctets.</span><span class="sxs-lookup"><span data-stu-id="8b2df-168">You can set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="8b2df-169">Vous pouvez également vérifier toosee la quantité de données est actuellement stocké sur le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="8b2df-169">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="8b2df-170">En définissant le quota de hello pour un partage, vous pouvez limiter la taille totale de hello hello les fichiers stockés sur le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="8b2df-170">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="8b2df-171">Si hello la taille totale des fichiers sur le partage de hello dépasse quota de hello défini sur le partage de hello, les clients seront taille de hello tooincrease impossible des fichiers existants ou créer de nouveaux fichiers, à moins que ces fichiers sont vides.</span><span class="sxs-lookup"><span data-stu-id="8b2df-171">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="8b2df-172">exemple Hello ci-dessous montre comment toocheck hello en cours d’utilisation pour un partage et comment tooset hello quota pour le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="8b2df-172">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="8b2df-173">Génération d’une signature d’accès partagé pour un fichier ou partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="8b2df-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="8b2df-174">Vous pouvez générer une signature d’accès partagé (SAP) pour un partage de fichiers ou un fichier individuel.</span><span class="sxs-lookup"><span data-stu-id="8b2df-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="8b2df-175">Vous pouvez également créer une stratégie d’accès partagé sur un toomanage partagé accès au partage de fichier signatures.</span><span class="sxs-lookup"><span data-stu-id="8b2df-175">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="8b2df-176">Création d’une stratégie d’accès partagé est recommandée, car elle fournit un moyen de révocation hello SAS si elle doit être compromise.</span><span class="sxs-lookup"><span data-stu-id="8b2df-176">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="8b2df-177">Bonjour à l’exemple suivant crée une stratégie d’accès partagé sur un partage, puis utilise que tooprovide hello les contraintes de stratégie pour une SAP sur un fichier dans hello partagent.</span><span class="sxs-lookup"><span data-stu-id="8b2df-177">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
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

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="8b2df-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8b2df-178">Next steps</span></span>
<span data-ttu-id="8b2df-179">toolearn en savoir plus sur le stockage Azure, Explorez ces ressources :</span><span class="sxs-lookup"><span data-stu-id="8b2df-179">toolearn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="8b2df-180">Bibliothèque cliente de stockage pour C++</span><span class="sxs-lookup"><span data-stu-id="8b2df-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="8b2df-181">[Exemples de service de fichier de Stockage Azure en C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="8b2df-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="8b2df-182">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="8b2df-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="8b2df-183">Documentation d'Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8b2df-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)