---
title: "Utilisation du stockage d’objets blob (Stockage Blob Azure) à partir de Python | Microsoft Docs"
description: "Stockez des données non structurées dans le cloud avec Azure Blob Storage (stockage d’objets)."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 1cab8407be6fc8932b68e50d0c301e8ea37ea3ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-blob-storage-from-python"></a><span data-ttu-id="0a910-103">Utilisation du stockage d’objets blob Azure à partir de Python</span><span class="sxs-lookup"><span data-stu-id="0a910-103">How to use Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="0a910-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0a910-104">Overview</span></span>
<span data-ttu-id="0a910-105">Le stockage d’objets blob Azure est un service qui stocke des données non structurées dans le cloud en tant qu’objets/blobs.</span><span class="sxs-lookup"><span data-stu-id="0a910-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="0a910-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="0a910-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="0a910-107">Le stockage d’objets blob est également appelé Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="0a910-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="0a910-108">Cet article décrit le déroulement de scénarios courants dans le cadre de l’utilisation du service de stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="0a910-108">This article will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="0a910-109">Les exemples sont écrits en Python et utilisent le [Kit de développement logiciel (SDK) Microsoft Azure Storage pour Python].</span><span class="sxs-lookup"><span data-stu-id="0a910-109">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="0a910-110">Les scénarios traités incluent le chargement, l'énumération, le téléchargement et la suppression d'objets blob.</span><span class="sxs-lookup"><span data-stu-id="0a910-110">The scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="0a910-111">Créer un conteneur</span><span class="sxs-lookup"><span data-stu-id="0a910-111">Create a container</span></span>
<span data-ttu-id="0a910-112">Selon le type d’objet blob que vous souhaitez utiliser, créez un objet **BlockBlobService**, **AppendBlobService** ou **PageBlobService**.</span><span class="sxs-lookup"><span data-stu-id="0a910-112">Based on the type of blob you would like to use, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="0a910-113">Le code suivant utilise un objet **BlockBlobService** .</span><span class="sxs-lookup"><span data-stu-id="0a910-113">The following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="0a910-114">Ajoutez ce qui suit vers le début de chaque fichier Python dans lequel vous souhaitez accéder au stockage d’objet blob de blocs Azure par programme.</span><span class="sxs-lookup"><span data-stu-id="0a910-114">Add the following near the top of any Python file in which you wish to programmatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="0a910-115">Le code suivant crée un objet **BlockBlobService** à l’aide du nom et de la clé du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0a910-115">The following code creates a **BlockBlobService** object using the storage account name and account key.</span></span>  <span data-ttu-id="0a910-116">Remplacez « myaccount » et « mykey » par le nom et la clé réels de votre compte.</span><span class="sxs-lookup"><span data-stu-id="0a910-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="0a910-117">Dans l’exemple de code suivant, vous pouvez utiliser un objet **BlockBlobService** pour créer le conteneur s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="0a910-117">In the following code example, you can use a **BlockBlobService** object to create the container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="0a910-118">Par défaut, le nouveau conteneur est privé. Vous devez donc indiquer votre clé d’accès au stockage (comme précédemment) pour télécharger des objets blob depuis ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="0a910-118">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span> <span data-ttu-id="0a910-119">Si vous voulez que les objets blob du conteneur soient accessibles à tout le monde, vous pouvez créer le conteneur et lui attribuer le niveau d’accès public en utilisant le code suivant.</span><span class="sxs-lookup"><span data-stu-id="0a910-119">If you want to make the blobs within the container available to everyone, you can create the container and pass the public access level using the following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="0a910-120">L’autre possibilité consiste à modifier un conteneur déjà créé, à l’aide du code suivant.</span><span class="sxs-lookup"><span data-stu-id="0a910-120">Alternatively, you can modify a container after you have created it using the following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="0a910-121">Après cette modification, tous les utilisateurs d'Internet peuvent afficher les objets blob d'un conteneur public, mais vous êtes le seul à pouvoir les modifier ou les supprimer.</span><span class="sxs-lookup"><span data-stu-id="0a910-121">After this change, anyone on the Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="0a910-122">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="0a910-122">Upload a blob into a container</span></span>
<span data-ttu-id="0a910-123">Pour créer un objet blob de blocs et télécharger des données, utilisez les méthodes **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** ou **create\_blob\_from\_text**.</span><span class="sxs-lookup"><span data-stu-id="0a910-123">To create a block blob and upload data, use the **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="0a910-124">Il s'agit de méthodes de haut niveau qui effectuent la segmentation nécessaire lorsque la taille des données est supérieure à 64 Mo.</span><span class="sxs-lookup"><span data-stu-id="0a910-124">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="0a910-125">**create\_blob\_from\_path** télécharge le contenu d’un fichier à partir du chemin spécifié, et **create\_blob\_from\_stream** télécharge le contenu à partir d’un flux/fichier déjà ouvert.</span><span class="sxs-lookup"><span data-stu-id="0a910-125">**create\_blob\_from\_path** uploads the contents of a file from the specified path, and **create\_blob\_from\_stream** uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="0a910-126">**create\_blob\_from\_bytes** télécharge un tableau d’octets, et **create\_blob\_from\_text** télécharge la valeur texte spécifiée à l’aide de l’encodage spécifié (par défaut UTF-8).</span><span class="sxs-lookup"><span data-stu-id="0a910-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="0a910-127">L’exemple suivant charge le contenu du fichier **sunset.png** dans l’objet blob **myblob**.</span><span class="sxs-lookup"><span data-stu-id="0a910-127">The following example uploads the contents of the **sunset.png** file into the **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="0a910-128">Création d'une liste d'objets blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="0a910-128">List the blobs in a container</span></span>
<span data-ttu-id="0a910-129">Pour répertorier les objets blob dans un conteneur, utilisez la méthode **list\_blobs**.</span><span class="sxs-lookup"><span data-stu-id="0a910-129">To list the blobs in a container, use the **list\_blobs** method.</span></span> <span data-ttu-id="0a910-130">Cette méthode retourne un générateur.</span><span class="sxs-lookup"><span data-stu-id="0a910-130">This method returns a generator.</span></span> <span data-ttu-id="0a910-131">Le code suivant sort le **nom** de chaque objet blob d'un conteneur sur la console.</span><span class="sxs-lookup"><span data-stu-id="0a910-131">The following code outputs the **name** of each blob in a container to the console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="0a910-132">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="0a910-132">Download blobs</span></span>
<span data-ttu-id="0a910-133">Pour télécharger des données d’un objet blob, utilisez **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes** ou **get\_blob\_to\_text**.</span><span class="sxs-lookup"><span data-stu-id="0a910-133">To download data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="0a910-134">Il s'agit de méthodes de haut niveau qui effectuent la segmentation nécessaire lorsque la taille des données est supérieure à 64 Mo.</span><span class="sxs-lookup"><span data-stu-id="0a910-134">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="0a910-135">L’exemple suivant illustre l’utilisation de **get\_blob\_to\_path** pour télécharger le contenu de l’objet blob **myblob** et le stocker dans le fichier **out-sunset.png**.</span><span class="sxs-lookup"><span data-stu-id="0a910-135">The following example demonstrates using **get\_blob\_to\_path** to download the contents of the **myblob** blob and store it to the **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="0a910-136">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="0a910-136">Delete a blob</span></span>
<span data-ttu-id="0a910-137">Pour supprimer un objet blob, appelez **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="0a910-137">Finally, to delete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="0a910-138">Écriture dans un objet blob d’ajout</span><span class="sxs-lookup"><span data-stu-id="0a910-138">Writing to an append blob</span></span>
<span data-ttu-id="0a910-139">Il est optimisé pour les opérations d’ajout, telles que la journalisation.</span><span class="sxs-lookup"><span data-stu-id="0a910-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="0a910-140">Comme un objet blob de blocs, un objet blob d’ajout est composé de blocs. Mais lorsqu’il est ajouté à un objet blob d’ajout, un nouveau bloc l’est toujours à la fin.</span><span class="sxs-lookup"><span data-stu-id="0a910-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="0a910-141">Vous ne pouvez pas mettre à jour ou supprimer un bloc dans un objet blob d’ajout.</span><span class="sxs-lookup"><span data-stu-id="0a910-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="0a910-142">Les ID de bloc dans un objet blob d’ajout ne sont pas visibles, comme pour un objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="0a910-142">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="0a910-143">Chaque bloc d’un objet blob d’ajout peut avoir une taille différente (jusqu’à 4 Mo), et un objet blob d’ajout peut contenir au maximum 50 000 blocs.</span><span class="sxs-lookup"><span data-stu-id="0a910-143">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="0a910-144">La taille maximale d’un objet blob d’ajout est donc légèrement supérieure à 195 Go (4 Mo x 50 000 blocs).</span><span class="sxs-lookup"><span data-stu-id="0a910-144">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="0a910-145">L’exemple ci-dessous crée un objet blob d’ajout et y ajoute des données pour simuler une opération de journalisation simple.</span><span class="sxs-lookup"><span data-stu-id="0a910-145">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# The same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="0a910-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0a910-146">Next steps</span></span>
<span data-ttu-id="0a910-147">Maintenant que vous connaissez les bases du stockage d’objets blob, consultez les liens suivants pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="0a910-147">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="0a910-148">Centre de développement Python</span><span class="sxs-lookup"><span data-stu-id="0a910-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="0a910-149">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0a910-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="0a910-150">[Blog de l'équipe Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="0a910-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="0a910-151">[Kit de développement logiciel (SDK) Microsoft Azure Storage pour Python]</span><span class="sxs-lookup"><span data-stu-id="0a910-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog de l'équipe Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/
[Kit de développement logiciel (SDK) Microsoft Azure Storage pour Python]: https://github.com/Azure/azure-storage-python
