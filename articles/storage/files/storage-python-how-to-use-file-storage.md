---
title: aaaDevelop pour le stockage de fichiers Azure avec Python | Documents Microsoft
description: "Découvrez comment les applications Python toodevelop et les services qui utilisent des fichiers Azure storage toostore fichier des données."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 2adc5aac2765b98a8022ab1f706c1fcdbca1b43c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="7af24-103">Développer pour le stockage de fichiers Azure avec Python</span><span class="sxs-lookup"><span data-stu-id="7af24-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="7af24-104">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="7af24-104">About this tutorial</span></span>
<span data-ttu-id="7af24-105">Ce didacticiel va vous montrer des bases de hello de l’utilisation des applications de toodevelop Python ou services qui utilisent des données de fichier toostore fichier Azure storage.</span><span class="sxs-lookup"><span data-stu-id="7af24-105">This tutorial will demonstrate hello basics of using Python toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="7af24-106">Dans ce didacticiel, nous crée une application console simple et montrent comment tooperform les actions de base avec le stockage de Python et des fichiers Azure :</span><span class="sxs-lookup"><span data-stu-id="7af24-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="7af24-107">Créer des partages de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="7af24-107">Create Azure File shares</span></span>
* <span data-ttu-id="7af24-108">Créer des répertoires</span><span class="sxs-lookup"><span data-stu-id="7af24-108">Create directories</span></span>
* <span data-ttu-id="7af24-109">Énumérer des fichiers et répertoires dans un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="7af24-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="7af24-110">Charger, télécharger et supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="7af24-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="7af24-111">Stockage de fichiers Azure sont accessibles sur SMB, il est toowrite possible les applications simples qui accéder au partage de fichiers Azure hello à l’aide des fonctions et des classes d’e/s de Python standards hello.</span><span class="sxs-lookup"><span data-stu-id="7af24-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Python I/O classes and functions.</span></span> <span data-ttu-id="7af24-112">Cet article décrit comment toowrite les applications qui utilisent hello SDK Azure Storage Python, qui utilise hello [le stockage de fichiers Azure API REST](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="7af24-112">This article will describe how toowrite applications that use hello Azure Storage Python SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

### <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="7af24-113">Configurer votre toouse application stockage Azure</span><span class="sxs-lookup"><span data-stu-id="7af24-113">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="7af24-114">Ajoutez les éléments suivants de hello haut hello de n’importe quel fichier de source de Python dans lesquels vous souhaitez tooprogrammatically accès Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7af24-114">Add hello following near hello top of any Python source file in which you wish tooprogrammatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a><span data-ttu-id="7af24-115">Configurer une connexion de tooAzure stockage de fichiers</span><span class="sxs-lookup"><span data-stu-id="7af24-115">Set up a connection tooAzure File storage</span></span> 
<span data-ttu-id="7af24-116">Hello `FileService` objet vous permet de travailler avec les partages, répertoires et fichiers.</span><span class="sxs-lookup"><span data-stu-id="7af24-116">hello `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="7af24-117">Hello de code suivant crée un `FileService` objet à l’aide de la clé de compte et le nom du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="7af24-117">hello following code creates a `FileService` object using hello storage account name and account key.</span></span> <span data-ttu-id="7af24-118">Remplacez `<myaccount>` et `<mykey>` par le nom et la clé de votre compte.</span><span class="sxs-lookup"><span data-stu-id="7af24-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="7af24-119">Création d’un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="7af24-119">Create an Azure File share</span></span>
<span data-ttu-id="7af24-120">Bonjour exemple de code suivant, vous pouvez utiliser un `FileService` partage de hello toocreate objet si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="7af24-120">In hello following code example, you can use a `FileService` object toocreate hello share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="7af24-121">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="7af24-121">Create a directory</span></span>
<span data-ttu-id="7af24-122">Vous pouvez également organiser le stockage en plaçant les fichiers dans les sous-répertoires au lieu d’avoir tous les dans le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="7af24-122">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="7af24-123">Stockage de fichier Azure vous permet de toocreate car autorise de nombreux répertoires car votre compte.</span><span class="sxs-lookup"><span data-stu-id="7af24-123">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="7af24-124">code Hello ci-dessous crée un sous-répertoire nommé **sampledir** sous le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="7af24-124">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="7af24-125">Énumérer des fichiers et répertoires dans un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="7af24-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="7af24-126">fichiers de hello toolist et des répertoires dans un partage, utilisez hello **liste\_répertoires\_et\_fichiers** (méthode).</span><span class="sxs-lookup"><span data-stu-id="7af24-126">toolist hello files and directories in a share, use hello **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="7af24-127">Cette méthode retourne un générateur.</span><span class="sxs-lookup"><span data-stu-id="7af24-127">This method returns a generator.</span></span> <span data-ttu-id="7af24-128">Hello de code suivant génère hello **nom** de chaque fichier et le répertoire dans une console toohello de partage.</span><span class="sxs-lookup"><span data-stu-id="7af24-128">hello following code outputs hello **name** of each file and directory in a share toohello console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="7af24-129">Charger un fichier</span><span class="sxs-lookup"><span data-stu-id="7af24-129">Upload a file</span></span> 
<span data-ttu-id="7af24-130">Fichier Azure partage contient de hello très moins, un répertoire racine où les fichiers peuvent résider.</span><span class="sxs-lookup"><span data-stu-id="7af24-130">Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="7af24-131">Dans cette section, vous allez apprendre comment tooupload un fichier à partir du stockage local sur hello racine du répertoire d’un partage.</span><span class="sxs-lookup"><span data-stu-id="7af24-131">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="7af24-132">toocreate un fichier et les données de téléchargement, utilisez hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` ou `create_file_from_text` méthodes.</span><span class="sxs-lookup"><span data-stu-id="7af24-132">toocreate a file and upload data, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="7af24-133">Ce sont des méthodes de haut niveau qui effectuent la segmentation nécessaire hello lorsque la taille de hello de données de hello dépasse 64 Mo.</span><span class="sxs-lookup"><span data-stu-id="7af24-133">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="7af24-134">`create_file_from_path`téléchargements hello le contenu d’un fichier à partir du chemin d’accès spécifié hello, et `create_file_from_stream` téléchargements hello contenu à partir d’un flux de fichier/déjà ouvert.</span><span class="sxs-lookup"><span data-stu-id="7af24-134">`create_file_from_path` uploads hello contents of a file from hello specified path, and `create_file_from_stream` uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="7af24-135">`create_file_from_bytes`télécharge un tableau d’octets, et `create_file_from_text` téléchargements hello spécifié la valeur de texte à l’aide de hello spécifié encodage (valeurs par défaut tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="7af24-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="7af24-136">exemple Hello télécharge contenu hello Hello **sunset.png** fichier hello **myfile** fichier.</span><span class="sxs-lookup"><span data-stu-id="7af24-136">hello following example uploads hello contents of hello **sunset.png** file into hello **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="7af24-137">Téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="7af24-137">Download a file</span></span>
<span data-ttu-id="7af24-138">toodownload des données à partir d’un fichier, utilisez `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, ou `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="7af24-138">toodownload data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="7af24-139">Ce sont des méthodes de haut niveau qui effectuent la segmentation nécessaire hello lorsque la taille de hello de données de hello dépasse 64 Mo.</span><span class="sxs-lookup"><span data-stu-id="7af24-139">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="7af24-140">Hello exemple suivant montre comment utiliser `get_file_to_path` contenu de hello toodownload Hello **myfile** de fichier et le stocker toohello **hors-sunset.png** fichier.</span><span class="sxs-lookup"><span data-stu-id="7af24-140">hello following example demonstrates using `get_file_to_path` toodownload hello contents of hello **myfile** file and store it toohello **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="7af24-141">Supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="7af24-141">Delete a file</span></span>
<span data-ttu-id="7af24-142">Enfin, toodelete un fichier, appelez `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="7af24-142">Finally, toodelete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="7af24-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7af24-143">Next steps</span></span>
<span data-ttu-id="7af24-144">Maintenant que vous avez appris comment toomanipulate stockage Azure files avec Python, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="7af24-144">Now that you've learned how toomanipulate Azure File storage with Python, follow these links toolearn more.</span></span>

* [<span data-ttu-id="7af24-145">Centre de développement Python</span><span class="sxs-lookup"><span data-stu-id="7af24-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="7af24-146">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7af24-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="7af24-147">Kit de développement logiciel (SDK) Microsoft Azure Storage pour Python</span><span class="sxs-lookup"><span data-stu-id="7af24-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)