---
title: "Utilisation du stockage d’objets blob à partir de Ruby | Microsoft Docs"
description: "Stockez des données non structurées dans le cloud avec Azure Blob Storage (stockage d’objets)."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 7f7d0c52b2b50a360711477e8e0eafc07ddcf374
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-ruby"></a><span data-ttu-id="b3d01-103">Utilisation du stockage d'objets blob à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="b3d01-103">How to use Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="b3d01-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b3d01-104">Overview</span></span>
<span data-ttu-id="b3d01-105">Le stockage d’objets blob Azure est un service qui stocke des données non structurées dans le cloud en tant qu’objets/blobs.</span><span class="sxs-lookup"><span data-stu-id="b3d01-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="b3d01-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="b3d01-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="b3d01-107">Le stockage d’objets blob est également appelé Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b3d01-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="b3d01-108">Ce guide décrit le déroulement de scénarios courants dans le cadre de l’utilisation de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b3d01-108">This guide will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="b3d01-109">Les exemples sont écrits à l'aide de l'API Ruby.</span><span class="sxs-lookup"><span data-stu-id="b3d01-109">The samples are written using the Ruby API.</span></span> <span data-ttu-id="b3d01-110">Les scénarios traités incluent le **chargement, l’énumération, le téléchargement** et la **suppression** d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="b3d01-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="b3d01-111">Création d'une application Ruby</span><span class="sxs-lookup"><span data-stu-id="b3d01-111">Create a Ruby application</span></span>
<span data-ttu-id="b3d01-112">Créez une application Ruby.</span><span class="sxs-lookup"><span data-stu-id="b3d01-112">Create a Ruby application.</span></span> <span data-ttu-id="b3d01-113">Pour obtenir des instructions, consultez [Application web Ruby on Rails sur une machine virtuelle Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="b3d01-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="b3d01-114">Configuration de votre application pour accéder au stockage</span><span class="sxs-lookup"><span data-stu-id="b3d01-114">Configure your application to access Storage</span></span>
<span data-ttu-id="b3d01-115">Pour utiliser Azure Storage, vous devez télécharger et utiliser le package Azure Ruby, qui inclut un ensemble de bibliothèques permettant de communiquer avec les services de stockage REST.</span><span class="sxs-lookup"><span data-stu-id="b3d01-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="b3d01-116">Utilisation de RubyGems pour obtenir le package</span><span class="sxs-lookup"><span data-stu-id="b3d01-116">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="b3d01-117">Ouvrez une interface de ligne de commande, telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="b3d01-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="b3d01-118">Tapez « gem install azure » dans la fenêtre de commande pour installer gem et les dépendances.</span><span class="sxs-lookup"><span data-stu-id="b3d01-118">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="b3d01-119">Importation du package</span><span class="sxs-lookup"><span data-stu-id="b3d01-119">Import the package</span></span>
<span data-ttu-id="b3d01-120">À l'aide de votre éditeur de texte, ajoutez la commande suivante au début du fichier Ruby où vous comptez utiliser le stockage :</span><span class="sxs-lookup"><span data-stu-id="b3d01-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="b3d01-121">Configuration d’une connexion Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="b3d01-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="b3d01-122">Le module Azure lit les variables d’environnement **AZURE\_STORAGE\_ACCOUNT** et **AZURE\_STORAGE\_ACCESS_KEY** pour obtenir les informations nécessaires à la connexion à votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b3d01-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="b3d01-123">Si ces variables d'environnement ne sont pas définies, vous devez spécifier les informations de compte avant d'utiliser **Azure::Blob::BlobService** avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="b3d01-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="b3d01-124">Pour obtenir ces valeurs à partir d’un compte de stockage classique ou Resource Manager sur le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="b3d01-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="b3d01-125">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3d01-125">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b3d01-126">Accédez au compte de stockage que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="b3d01-126">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="b3d01-127">Dans le panneau Paramètres à droite, cliquez sur **Clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="b3d01-127">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="b3d01-128">Dans le panneau Clés d’accès qui apparaît, la clé d’accès 1 et la clé d’accès 2 sont affichées.</span><span class="sxs-lookup"><span data-stu-id="b3d01-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="b3d01-129">Vous pouvez utiliser les deux.</span><span class="sxs-lookup"><span data-stu-id="b3d01-129">You can use either of these.</span></span>
5. <span data-ttu-id="b3d01-130">Cliquez sur l'icône de copie pour copier la clé dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="b3d01-130">Click the copy icon to copy the key to the clipboard.</span></span>

<span data-ttu-id="b3d01-131">Pour obtenir ces valeurs à partir d’un compte de stockage classique sur le portail Azure Classic :</span><span class="sxs-lookup"><span data-stu-id="b3d01-131">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="b3d01-132">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b3d01-132">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b3d01-133">Accédez au compte de stockage que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="b3d01-133">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="b3d01-134">Cliquez sur **GÉRER LES CLÉS D’ACCÈS** en bas du volet de navigation.</span><span class="sxs-lookup"><span data-stu-id="b3d01-134">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="b3d01-135">Dans la boîte de dialogue contextuelle, vous voyez le nom du compte de stockage et la clé d’accès primaire ou secondaire.</span><span class="sxs-lookup"><span data-stu-id="b3d01-135">In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="b3d01-136">Vous pouvez utiliser soit la clé d'accès primaire, soit la clé d'accès secondaire.</span><span class="sxs-lookup"><span data-stu-id="b3d01-136">For access key, you can use either the primary one or the secondary one.</span></span>
5. <span data-ttu-id="b3d01-137">Cliquez sur l'icône de copie pour copier la clé dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="b3d01-137">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="b3d01-138">Créer un conteneur</span><span class="sxs-lookup"><span data-stu-id="b3d01-138">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="b3d01-139">L'objet **Azure::Blob::BlobService** permet d'utiliser des conteneurs et des objets blob.</span><span class="sxs-lookup"><span data-stu-id="b3d01-139">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="b3d01-140">Pour créer un conteneur, utilisez la méthode **create\_container()**.</span><span class="sxs-lookup"><span data-stu-id="b3d01-140">To create a container, use the **create\_container()** method.</span></span>

<span data-ttu-id="b3d01-141">L’exemple de code suivant crée un conteneur ou imprime l’erreur le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="b3d01-141">The following code example creates a container or prints the error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="b3d01-142">Si vous souhaitez que les fichiers du conteneur soient publics, vous pouvez définir le niveau d'accès du conteneur.</span><span class="sxs-lookup"><span data-stu-id="b3d01-142">If you want to make the files in the container public, you can set the container's permissions.</span></span>

<span data-ttu-id="b3d01-143">Vous pouvez simplement modifier l’appel à <strong>create\_container()</strong> pour passer l’option **:public\_access\_level** :</span><span class="sxs-lookup"><span data-stu-id="b3d01-143">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="b3d01-144">Les valeurs valides pour l’option **:public\_access\_level** sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3d01-144">Valid values for the **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="b3d01-145">**blob :** spécifie un accès public en lecture pour les objets blob.</span><span class="sxs-lookup"><span data-stu-id="b3d01-145">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="b3d01-146">Les données d'objets blob à l'intérieur de ce conteneur peuvent être lues via une demande anonyme, mais les données du conteneur ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="b3d01-146">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="b3d01-147">Les clients ne peuvent pas énumérer les objets blob à l’intérieur du conteneur via une demande anonyme.</span><span class="sxs-lookup"><span data-stu-id="b3d01-147">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="b3d01-148">**conteneur** : spécifie un accès public total en lecture pour le conteneur et les données d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="b3d01-148">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="b3d01-149">Les clients peuvent énumérer les objets blob à l’intérieur du conteneur via une demande anonyme, mais ne peuvent pas énumérer les conteneurs dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="b3d01-149">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="b3d01-150">Vous pouvez également modifier le niveau d’accès public d’un conteneur en utilisant la méthode **set\_container\_acl()** afin de spécifier le niveau d’accès public.</span><span class="sxs-lookup"><span data-stu-id="b3d01-150">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span></span>

<span data-ttu-id="b3d01-151">Dans l'exemple de code suivant, le niveau d'accès public du **conteneur**est modifié :</span><span class="sxs-lookup"><span data-stu-id="b3d01-151">The following code example changes the public access level to **container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="b3d01-152">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="b3d01-152">Upload a blob into a container</span></span>
<span data-ttu-id="b3d01-153">Pour télécharger du contenu dans un objet blob, utilisez la méthode **create\_block\_blob()** pour créer l’objet blob, utiliser un fichier ou une chaîne en tant que contenu de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="b3d01-153">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span></span>

<span data-ttu-id="b3d01-154">Le code suivant télécharge le fichier **test.png** en tant que nouvel objet blob nommé « image-blob » dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="b3d01-154">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="b3d01-155">Création d'une liste d'objets blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="b3d01-155">List the blobs in a container</span></span>
<span data-ttu-id="b3d01-156">Pour énumérer les conteneurs, utilisez la méthode **list_containers()**.</span><span class="sxs-lookup"><span data-stu-id="b3d01-156">To list the containers, use **list_containers()** method.</span></span>
<span data-ttu-id="b3d01-157">Pour énumérer les objets blob à l’intérieur d’un conteneur, utilisez la méthode **list\_blobs()**.</span><span class="sxs-lookup"><span data-stu-id="b3d01-157">To list the blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="b3d01-158">Cette action génère les URL de tous les objets blob de tous les conteneurs pour le compte.</span><span class="sxs-lookup"><span data-stu-id="b3d01-158">This outputs the urls of all the blobs in all the containers for the account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="b3d01-159">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="b3d01-159">Download blobs</span></span>
<span data-ttu-id="b3d01-160">Pour télécharger des objets blob, utilisez la méthode **get\_blob()** afin d’extraire le contenu.</span><span class="sxs-lookup"><span data-stu-id="b3d01-160">To download blobs, use the **get\_blob()** method to retrieve the contents.</span></span>

<span data-ttu-id="b3d01-161">L’exemple de code suivant illustre l’utilisation de **get\_blob()** pour télécharger le contenu d’« image-blob » et l’écrire dans un fichier local.</span><span class="sxs-lookup"><span data-stu-id="b3d01-161">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="b3d01-162">Suppression d'un objet blob</span><span class="sxs-lookup"><span data-stu-id="b3d01-162">Delete a Blob</span></span>
<span data-ttu-id="b3d01-163">Pour supprimer un objet blob, utilisez la méthode **delete\_blob()**.</span><span class="sxs-lookup"><span data-stu-id="b3d01-163">Finally, to delete a blob, use the **delete\_blob()** method.</span></span> <span data-ttu-id="b3d01-164">L'exemple de code suivant illustre la suppression d'un objet blob.</span><span class="sxs-lookup"><span data-stu-id="b3d01-164">The following code example demonstrates how to delete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="b3d01-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b3d01-165">Next steps</span></span>
<span data-ttu-id="b3d01-166">Pour en savoir plus sur les tâches de stockage plus complexes, cliquez sur les liens ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b3d01-166">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="b3d01-167">Blog de l'équipe Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b3d01-167">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="b3d01-168">[Kit de développement logiciel (SDK) Azure pour Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) sur GitHub</span><span class="sxs-lookup"><span data-stu-id="b3d01-168">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="b3d01-169">Transfert de données avec l'utilitaire de ligne de commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="b3d01-169">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

