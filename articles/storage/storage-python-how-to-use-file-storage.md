---
title: "Développer pour le stockage de fichiers Azure avec Python | Microsoft Docs"
description: "Apprenez à développer des services et applications Python qui utilisent le stockage de fichiers Azure pour stocker les données de fichiers."
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
ms.openlocfilehash: a1a37266908277b54e7b42d85b9b4873af77e622
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="6fd72-103">Développer pour le stockage de fichiers Azure avec Python</span><span class="sxs-lookup"><span data-stu-id="6fd72-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="6fd72-104">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="6fd72-104">About this tutorial</span></span>
<span data-ttu-id="6fd72-105">Ce didacticiel vous montre les principes fondamentaux de l’utilisation de Python pour développer des applications ou services qui utilisent le stockage de fichiers Azure pour stocker les données de fichiers.</span><span class="sxs-lookup"><span data-stu-id="6fd72-105">This tutorial will demonstrate the basics of using Python to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="6fd72-106">Dans ce didacticiel, nous allons créer une application de console simple et effectuer des actions de base avec Python et le stockage de fichiers Azure :</span><span class="sxs-lookup"><span data-stu-id="6fd72-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="6fd72-107">Créer des partages de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="6fd72-107">Create Azure File shares</span></span>
* <span data-ttu-id="6fd72-108">Créer des répertoires</span><span class="sxs-lookup"><span data-stu-id="6fd72-108">Create directories</span></span>
* <span data-ttu-id="6fd72-109">Énumérer des fichiers et répertoires dans un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="6fd72-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="6fd72-110">Charger, télécharger et supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="6fd72-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="6fd72-111">Étant donné que le stockage de fichiers Azure est accessible sur SMB, il est possible d’écrire de simples applications qui accèdent au partage de fichiers Azure à l’aide des fonctions et des classes d’E/S Python standard.</span><span class="sxs-lookup"><span data-stu-id="6fd72-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Python I/O classes and functions.</span></span> <span data-ttu-id="6fd72-112">Cet article indique comment écrire des applications qui utilisent le kit de développement logiciel (SDK) Python de stockage Azure, lequel utilise [l’API REST de stockage de fichiers Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) pour communiquer avec le stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd72-112">This article will describe how to write applications that use the Azure Storage Python SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

### <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="6fd72-113">Configuration de votre application pour l’utilisation du stockage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="6fd72-113">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="6fd72-114">Ajoutez ce qui suit vers le début de chaque fichier source Python dans lequel vous souhaitez accéder au stockage Azure Storage par programme.</span><span class="sxs-lookup"><span data-stu-id="6fd72-114">Add the following near the top of any Python source file in which you wish to programmatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a><span data-ttu-id="6fd72-115">Configuration d’une connexion au stockage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="6fd72-115">Set up a connection to Azure File storage</span></span> 
<span data-ttu-id="6fd72-116">L’objet `FileService` vous permet d’utiliser des partages, des répertoires et des fichiers.</span><span class="sxs-lookup"><span data-stu-id="6fd72-116">The `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="6fd72-117">Le code suivant crée un objet `FileService` à l’aide du nom et de la clé du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6fd72-117">The following code creates a `FileService` object using the storage account name and account key.</span></span> <span data-ttu-id="6fd72-118">Remplacez `<myaccount>` et `<mykey>` par le nom et la clé de votre compte.</span><span class="sxs-lookup"><span data-stu-id="6fd72-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="6fd72-119">Création d’un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="6fd72-119">Create an Azure File share</span></span>
<span data-ttu-id="6fd72-120">Dans l’exemple de code suivant, vous pouvez utiliser un objet `FileService` pour créer le partage s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="6fd72-120">In the following code example, you can use a `FileService` object to create the share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="6fd72-121">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="6fd72-121">Create a directory</span></span>
<span data-ttu-id="6fd72-122">Vous pouvez également organiser le stockage en plaçant des fichiers dans des sous-répertoires, plutôt que de tous les mettre dans le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="6fd72-122">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="6fd72-123">Le stockage de fichiers Azure vous permet de créer autant de répertoires que le permet votre compte.</span><span class="sxs-lookup"><span data-stu-id="6fd72-123">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="6fd72-124">Le code ci-dessous crée un sous-répertoire nommé **sampledir** sous le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="6fd72-124">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="6fd72-125">Énumérer des fichiers et répertoires dans un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="6fd72-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="6fd72-126">Pour répertorier les fichiers et répertoires d’un partage, utilisez la méthode **list\_directories\_and\_files**.</span><span class="sxs-lookup"><span data-stu-id="6fd72-126">To list the files and directories in a share, use the **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="6fd72-127">Cette méthode retourne un générateur.</span><span class="sxs-lookup"><span data-stu-id="6fd72-127">This method returns a generator.</span></span> <span data-ttu-id="6fd72-128">Le code suivant sort le **nom** de chaque fichier et répertoire d'un partage sur la console.</span><span class="sxs-lookup"><span data-stu-id="6fd72-128">The following code outputs the **name** of each file and directory in a share to the console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="6fd72-129">Charger un fichier</span><span class="sxs-lookup"><span data-stu-id="6fd72-129">Upload a file</span></span> 
<span data-ttu-id="6fd72-130">Un partage de fichiers Azure contient au minimum un répertoire racine dans lequel les fichiers peuvent résider.</span><span class="sxs-lookup"><span data-stu-id="6fd72-130">Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="6fd72-131">Cette section décrit comment télécharger un fichier du stockage local vers le répertoire racine d’un partage.</span><span class="sxs-lookup"><span data-stu-id="6fd72-131">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="6fd72-132">Pour créer un fichier et charger des données, utilisez les méthodes `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` ou `create_file_from_text`.</span><span class="sxs-lookup"><span data-stu-id="6fd72-132">To create a file and upload data, use the `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="6fd72-133">Il s'agit de méthodes de haut niveau qui effectuent la segmentation nécessaire lorsque la taille des données est supérieure à 64 Mo.</span><span class="sxs-lookup"><span data-stu-id="6fd72-133">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="6fd72-134">`create_file_from_path` charge le contenu d’un fichier à partir du chemin spécifié, et `create_file_from_stream` charge le contenu à partir d’un flux/fichier déjà ouvert.</span><span class="sxs-lookup"><span data-stu-id="6fd72-134">`create_file_from_path` uploads the contents of a file from the specified path, and `create_file_from_stream` uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="6fd72-135">`create_file_from_bytes` charge un tableau d’octets, et `create_file_from_text` charge la valeur texte spécifiée à l’aide de l’encodage spécifié (par défaut UTF-8).</span><span class="sxs-lookup"><span data-stu-id="6fd72-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="6fd72-136">L’exemple suivant charge le contenu du fichier **sunset.png** dans le fichier **myfile**.</span><span class="sxs-lookup"><span data-stu-id="6fd72-136">The following example uploads the contents of the **sunset.png** file into the **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="6fd72-137">Téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="6fd72-137">Download a file</span></span>
<span data-ttu-id="6fd72-138">Pour télécharger des données à partir d’un fichier, utilisez `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, ou `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="6fd72-138">To download data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="6fd72-139">Il s'agit de méthodes de haut niveau qui effectuent la segmentation nécessaire lorsque la taille des données est supérieure à 64 Mo.</span><span class="sxs-lookup"><span data-stu-id="6fd72-139">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="6fd72-140">L’exemple suivant illustre l’utilisation de `get_file_to_path` pour télécharger le contenu du fichier **myfile** et le stocker dans le fichier **out-sunset.png**.</span><span class="sxs-lookup"><span data-stu-id="6fd72-140">The following example demonstrates using `get_file_to_path` to download the contents of the **myfile** file and store it to the **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="6fd72-141">Supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="6fd72-141">Delete a file</span></span>
<span data-ttu-id="6fd72-142">Enfin, pour supprimer un fichier, appelez `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="6fd72-142">Finally, to delete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="6fd72-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6fd72-143">Next steps</span></span>
<span data-ttu-id="6fd72-144">Maintenant que vous avez appris comment manipuler le stockage de fichiers Azure avec Python, suivez ces liens pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="6fd72-144">Now that you've learned how to manipulate Azure File storage with Python, follow these links to learn more.</span></span>

* [<span data-ttu-id="6fd72-145">Centre de développement Python</span><span class="sxs-lookup"><span data-stu-id="6fd72-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="6fd72-146">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="6fd72-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="6fd72-147">Kit de développement logiciel (SDK) Microsoft Azure Storage pour Python</span><span class="sxs-lookup"><span data-stu-id="6fd72-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)