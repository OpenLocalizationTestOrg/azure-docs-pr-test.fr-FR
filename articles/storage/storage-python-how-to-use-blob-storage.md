---
title: "aaaHow toouse le stockage Blob Azure (stockage d’objets) à partir de Python | Documents Microsoft"
description: "Stocker des données non structurées dans le cloud hello avec le stockage d’objets Blob Azure (stockage d’objets)."
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
ms.openlocfilehash: 6efc61aa89e6d2544b7a18c80ce3546640f90462
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a><span data-ttu-id="a4bbe-103">Comment toouse le stockage Blob Azure à partir de Python</span><span class="sxs-lookup"><span data-stu-id="a4bbe-103">How toouse Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="a4bbe-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a4bbe-104">Overview</span></span>
<span data-ttu-id="a4bbe-105">Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="a4bbe-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="a4bbe-107">Stockage d’objets BLOB est également référencé tooas stockage d’objets.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="a4bbe-108">Cet article vous indiquent comment les scénarios courants tooperform à l’aide du stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-108">This article will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="a4bbe-109">exemples de Hello sont écrites dans Python et utiliser hello [le stockage Microsoft Azure SDK pour Python].</span><span class="sxs-lookup"><span data-stu-id="a4bbe-109">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="a4bbe-110">les scénarios de Hello couvertes incluent le téléchargement, liste, le téléchargement et suppression d’objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-110">hello scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="a4bbe-111">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-111">Create a container</span></span>
<span data-ttu-id="a4bbe-112">En fonction de type hello d’objet blob vous aimeriez toouse, créez un **BlockBlobService**, **AppendBlobService**, ou **PageBlobService** objet.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-112">Based on hello type of blob you would like toouse, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="a4bbe-113">code Hello suivant utilise un **BlockBlobService** objet.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-113">hello following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="a4bbe-114">Ajoutez les éléments suivants de hello haut hello de n’importe quel fichier Python dans lequel vous souhaitez tooprogrammatically accès stockage d’objets Blob Azure bloc.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-114">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="a4bbe-115">Hello de code suivant crée un **BlockBlobService** objet à l’aide de la clé de compte et le nom du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-115">hello following code creates a **BlockBlobService** object using hello storage account name and account key.</span></span>  <span data-ttu-id="a4bbe-116">Remplacez « myaccount » et « mykey » par le nom et la clé réels de votre compte.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="a4bbe-117">Bonjour exemple de code suivant, vous pouvez utiliser un **BlockBlobService** le conteneur objet toocreate hello si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-117">In hello following code example, you can use a **BlockBlobService** object toocreate hello container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="a4bbe-118">Par défaut, le nouveau conteneur de hello est privé, vous devez spécifier votre clé d’accès (comme précédemment) BLOB toodownload à partir de ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-118">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span> <span data-ttu-id="a4bbe-119">Si vous souhaitez que les objets BLOB toomake hello tooeveryone disponibles du conteneur hello, vous pouvez créer un conteneur de hello et passer le niveau d’accès public hello à l’aide de hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-119">If you want toomake hello blobs within hello container available tooeveryone, you can create hello container and pass hello public access level using hello following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="a4bbe-120">Ou bien, vous pouvez modifier un conteneur une fois que vous avez créé à l’aide de hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-120">Alternatively, you can modify a container after you have created it using hello following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="a4bbe-121">Après cette modification, toute personne sur Internet de hello peut voir les objets BLOB dans un conteneur public, mais vous pouvez uniquement modifier ou les supprimer.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-121">After this change, anyone on hello Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="a4bbe-122">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="a4bbe-122">Upload a blob into a container</span></span>
<span data-ttu-id="a4bbe-123">toocreate un objet blob de blocs et les données de téléchargement, utilisez hello **créer\_blob\_de\_chemin d’accès**, **créer\_blob\_de\_flux**, **créer\_blob\_de\_octets** ou **créer\_blob\_de\_texte** méthodes.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-123">toocreate a block blob and upload data, use hello **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="a4bbe-124">Ce sont des méthodes de haut niveau qui effectuent la segmentation nécessaire hello lorsque la taille de hello de données de hello dépasse 64 Mo.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-124">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="a4bbe-125">**créer\_blob\_de\_chemin d’accès** téléchargements hello le contenu d’un fichier à partir du chemin d’accès spécifié hello, et **créer\_blob\_de\_flux** téléchargements hello contenu à partir d’un flux de fichier/déjà ouvert.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-125">**create\_blob\_from\_path** uploads hello contents of a file from hello specified path, and **create\_blob\_from\_stream** uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="a4bbe-126">**créer\_blob\_de\_octets** télécharge un tableau d’octets, et **créer\_blob\_de\_texte** télécharge hello spécifié valeur de texte à l’aide de hello spécifié d’encodage (valeurs par défaut tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="a4bbe-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="a4bbe-127">exemple Hello télécharge contenu hello Hello **sunset.png** fichier hello **myblob** blob.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-127">hello following example uploads hello contents of hello **sunset.png** file into hello **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="a4bbe-128">Répertorier les objets BLOB hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="a4bbe-128">List hello blobs in a container</span></span>
<span data-ttu-id="a4bbe-129">objets BLOB de hello toolist dans un conteneur, utilisez hello **liste\_BLOB** (méthode).</span><span class="sxs-lookup"><span data-stu-id="a4bbe-129">toolist hello blobs in a container, use hello **list\_blobs** method.</span></span> <span data-ttu-id="a4bbe-130">Cette méthode retourne un générateur.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-130">This method returns a generator.</span></span> <span data-ttu-id="a4bbe-131">Hello de code suivant génère hello **nom** de chaque objet blob dans une console toohello de conteneur.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-131">hello following code outputs hello **name** of each blob in a container toohello console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="a4bbe-132">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="a4bbe-132">Download blobs</span></span>
<span data-ttu-id="a4bbe-133">toodownload des données à partir d’un objet blob, utilisez **obtenir\_blob\_à\_chemin d’accès**, **obtenir\_blob\_à\_flux**, **obtenir\_blob\_à\_octets**, ou **obtenir\_blob\_à\_texte**.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-133">toodownload data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="a4bbe-134">Ce sont des méthodes de haut niveau qui effectuent la segmentation nécessaire hello lorsque la taille de hello de données de hello dépasse 64 Mo.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-134">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="a4bbe-135">Hello exemple suivant montre comment utiliser **obtenir\_blob\_à\_chemin d’accès** contenu de hello toodownload Hello **myblob** d’objets blob et le stocker toohello **hors-sunset.png** fichier.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-135">hello following example demonstrates using **get\_blob\_to\_path** toodownload hello contents of hello **myblob** blob and store it toohello **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="a4bbe-136">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="a4bbe-136">Delete a blob</span></span>
<span data-ttu-id="a4bbe-137">Enfin, toodelete un objet blob, appelez **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-137">Finally, toodelete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="a4bbe-138">Écriture tooan ajouter des objets blob</span><span class="sxs-lookup"><span data-stu-id="a4bbe-138">Writing tooan append blob</span></span>
<span data-ttu-id="a4bbe-139">Il est optimisé pour les opérations d’ajout, telles que la journalisation.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="a4bbe-140">Comme un objet blob de blocs, un objet blob d’ajout est constitué de blocs, mais lorsque vous ajoutez un nouvel objet blob bloc tooan append, il est toujours ajouté toohello de fin de l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="a4bbe-141">Vous ne pouvez pas mettre à jour ou supprimer un bloc dans un objet blob d’ajout.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="a4bbe-142">ID de bloc Hello pour un objet blob d’ajout ne sont pas exposés à ceux d’un objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-142">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="a4bbe-143">Chaque bloc dans un objet blob d’ajout peut avoir une taille différente, les tooa au maximum de 4 Mo, et un objet blob d’ajout peut inclure un maximum de 50 000 blocs.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-143">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="a4bbe-144">Hello taille maximale d’un objet blob d’ajout est par conséquent légèrement supérieur à 195 Go (4 Mo X avec 50 000 blocs).</span><span class="sxs-lookup"><span data-stu-id="a4bbe-144">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="a4bbe-145">exemple Hello ci-dessous crée un nouvel objet blob d’ajout et ajoute certaines tooit de données, en simulant une opération de journalisation simple.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-145">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="a4bbe-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a4bbe-146">Next steps</span></span>
<span data-ttu-id="a4bbe-147">Maintenant que vous avez appris les notions de base de hello du stockage Blob, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="a4bbe-147">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="a4bbe-148">Centre de développement Python</span><span class="sxs-lookup"><span data-stu-id="a4bbe-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="a4bbe-149">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a4bbe-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="a4bbe-150">[Blog de l'équipe Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="a4bbe-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="a4bbe-151">[le stockage Microsoft Azure SDK pour Python]</span><span class="sxs-lookup"><span data-stu-id="a4bbe-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog de l'équipe Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/
[le stockage Microsoft Azure SDK pour Python]: https://github.com/Azure/azure-storage-python
