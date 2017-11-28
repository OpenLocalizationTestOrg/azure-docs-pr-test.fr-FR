---
title: "aaaHow toouse stockage d’objets Blob (stockage d’objets) à partir de Ruby | Documents Microsoft"
description: "Stocker des données non structurées dans le cloud hello avec le stockage d’objets Blob Azure (stockage d’objets)."
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
ms.openlocfilehash: 638826777f5a7ae8330fd67cdbb51d5eee1736a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="962cf-103">Comment toouse stockage d’objets Blob à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="962cf-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="962cf-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="962cf-104">Overview</span></span>
<span data-ttu-id="962cf-105">Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB.</span><span class="sxs-lookup"><span data-stu-id="962cf-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="962cf-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="962cf-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="962cf-107">Stockage d’objets BLOB est également référencé tooas stockage d’objets.</span><span class="sxs-lookup"><span data-stu-id="962cf-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="962cf-108">Ce guide vous explique comment les scénarios courants tooperform à l’aide du stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="962cf-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="962cf-109">exemples de Hello sont écrites à l’aide de hello Ruby API.</span><span class="sxs-lookup"><span data-stu-id="962cf-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="962cf-110">Hello scénarios abordés incluent **téléchargement, en téléchargeant,** et **suppression** objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="962cf-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="962cf-111">Création d'une application Ruby</span><span class="sxs-lookup"><span data-stu-id="962cf-111">Create a Ruby application</span></span>
<span data-ttu-id="962cf-112">Créez une application Ruby.</span><span class="sxs-lookup"><span data-stu-id="962cf-112">Create a Ruby application.</span></span> <span data-ttu-id="962cf-113">Pour obtenir des instructions, consultez [Application web Ruby on Rails sur une machine virtuelle Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="962cf-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="962cf-114">Configurer votre application de tooaccess stockage</span><span class="sxs-lookup"><span data-stu-id="962cf-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="962cf-115">toouse stockage Azure, vous devez toodownload et utilisez hello Ruby package azure, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="962cf-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="962cf-116">Utiliser le package hello tooobtain RubyGems</span><span class="sxs-lookup"><span data-stu-id="962cf-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="962cf-117">Ouvrez une interface de ligne de commande, telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="962cf-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="962cf-118">Tapez « marque installer azure » dans les dépendances et le marque hello tooinstall hello commande fenêtre.</span><span class="sxs-lookup"><span data-stu-id="962cf-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="962cf-119">Importer un package hello</span><span class="sxs-lookup"><span data-stu-id="962cf-119">Import hello package</span></span>
<span data-ttu-id="962cf-120">À l’aide de votre éditeur de texte favori, ajoutez hello suivant haut toohello Hello Ruby fichier où vous avez l’intention toouse stockage :</span><span class="sxs-lookup"><span data-stu-id="962cf-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="962cf-121">Configuration d’une connexion Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="962cf-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="962cf-122">module de Hello azure lira des variables d’environnement hello **AZURE\_stockage\_compte** et **AZURE\_stockage\_ACCESS_KEY** pour compte de stockage Azure tooconnect tooyour les informations requises.</span><span class="sxs-lookup"><span data-stu-id="962cf-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="962cf-123">Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello avant d’utiliser **Azure::Blob::BlobService** avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="962cf-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="962cf-124">tooobtain ces valeurs à partir d’un classique ou de stockage du Gestionnaire de ressources du compte Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="962cf-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="962cf-125">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="962cf-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="962cf-126">Accédez à compte de stockage toohello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="962cf-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="962cf-127">Dans le panneau des paramètres hello sur hello droit, cliquez sur **clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="962cf-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="962cf-128">Dans hello accès clés panneau qui s’affiche, vous verrez la clé d’accès hello 1 et la clé d’accès 2.</span><span class="sxs-lookup"><span data-stu-id="962cf-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="962cf-129">Vous pouvez utiliser les deux.</span><span class="sxs-lookup"><span data-stu-id="962cf-129">You can use either of these.</span></span>
5. <span data-ttu-id="962cf-130">Cliquez sur le Presse-papiers toocopy hello toohello clé hello copie icône.</span><span class="sxs-lookup"><span data-stu-id="962cf-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

<span data-ttu-id="962cf-131">tooobtain ces valeurs à partir d’un stockage classique compte dans le portail Azure classic de hello :</span><span class="sxs-lookup"><span data-stu-id="962cf-131">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="962cf-132">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="962cf-132">Log in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="962cf-133">Accédez à compte de stockage toohello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="962cf-133">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="962cf-134">Cliquez sur **gérer les clés d’accès** bas hello hello du volet de navigation.</span><span class="sxs-lookup"><span data-stu-id="962cf-134">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="962cf-135">Vous verrez dans la boîte de dialogue contextuelle hello, nom de compte de stockage hello, clé d’accès primaire et clé d’accès secondaire.</span><span class="sxs-lookup"><span data-stu-id="962cf-135">In hello pop-up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="962cf-136">Pour la clé d’accès, vous pouvez utiliser hello principale ou hello secondaire.</span><span class="sxs-lookup"><span data-stu-id="962cf-136">For access key, you can use either hello primary one or hello secondary one.</span></span>
5. <span data-ttu-id="962cf-137">Cliquez sur le Presse-papiers toocopy hello toohello clé hello copie icône.</span><span class="sxs-lookup"><span data-stu-id="962cf-137">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="962cf-138">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="962cf-138">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="962cf-139">Hello **Azure::Blob::BlobService** objet vous permet de travailler avec les conteneurs et objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="962cf-139">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="962cf-140">toocreate un conteneur, utilisez hello **créer\_container()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="962cf-140">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="962cf-141">Hello exemple de code suivant crée un conteneur ou imprime les erreurs de hello cas échéant.</span><span class="sxs-lookup"><span data-stu-id="962cf-141">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="962cf-142">Si vous souhaitez toomake les fichiers de hello dans le conteneur de hello public, vous pouvez définir les autorisations du conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="962cf-142">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="962cf-143">Vous pouvez modifier uniquement hello <strong>créer\_container()</strong> appel toopass hello **: public\_accès\_niveau** option :</span><span class="sxs-lookup"><span data-stu-id="962cf-143">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="962cf-144">Les valeurs valides pour hello **: public\_accès\_niveau** option sont :</span><span class="sxs-lookup"><span data-stu-id="962cf-144">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="962cf-145">**blob :** spécifie un accès public en lecture pour les objets blob.</span><span class="sxs-lookup"><span data-stu-id="962cf-145">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="962cf-146">Les données d'objets blob à l'intérieur de ce conteneur peuvent être lues via une demande anonyme, mais les données du conteneur ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="962cf-146">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="962cf-147">Les clients ne peuvent pas énumérer les objets BLOB conteneur hello via une demande anonyme.</span><span class="sxs-lookup"><span data-stu-id="962cf-147">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="962cf-148">**conteneur** : spécifie un accès public total en lecture pour le conteneur et les données d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="962cf-148">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="962cf-149">Les clients peuvent énumérer des objets BLOB dans le conteneur hello via une demande anonyme, mais ne peut pas énumérer des conteneurs dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="962cf-149">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="962cf-150">Ou bien, vous pouvez modifier le niveau d’accès public hello d’un conteneur à l’aide de **définir\_conteneur\_acl()** le niveau d’accès public de méthode toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="962cf-150">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="962cf-151">Hello modifications hello le niveau d’accès public trop des exemple de code suivant**conteneur**:</span><span class="sxs-lookup"><span data-stu-id="962cf-151">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="962cf-152">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="962cf-152">Upload a blob into a container</span></span>
<span data-ttu-id="962cf-153">objet blob de contenu tooa tooupload, utilisez hello **créer\_bloc\_blob()** objet blob de méthode toocreate hello, utilisez un fichier ou de chaîne en tant que contenu hello d’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="962cf-153">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="962cf-154">Hello de code suivant télécharge les fichiers hello **test.png** comme un nouvel objet blob nommé « image-objet blob « hello conteneur.</span><span class="sxs-lookup"><span data-stu-id="962cf-154">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="962cf-155">Répertorier les objets BLOB hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="962cf-155">List hello blobs in a container</span></span>
<span data-ttu-id="962cf-156">utiliser des conteneurs de hello toolist **list_containers()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="962cf-156">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="962cf-157">utiliser des objets BLOB de hello toolist dans un conteneur, **liste\_blobs()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="962cf-157">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="962cf-158">Cela génère des URL hello de tous les objets BLOB de hello dans tous les conteneurs de hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="962cf-158">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="962cf-159">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="962cf-159">Download blobs</span></span>
<span data-ttu-id="962cf-160">objets BLOB toodownload, utilisez hello **obtenir\_blob()** contenu de méthode tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="962cf-160">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="962cf-161">Hello exemple de code suivant montre comment utiliser **obtenir\_blob()** toodownload hello le contenu de «-objet blob d’image » et de les écrire tooa des fichiers locaux.</span><span class="sxs-lookup"><span data-stu-id="962cf-161">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="962cf-162">Suppression d'un objet blob</span><span class="sxs-lookup"><span data-stu-id="962cf-162">Delete a Blob</span></span>
<span data-ttu-id="962cf-163">Enfin, toodelete un objet blob, utilisez hello **supprimer\_blob()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="962cf-163">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="962cf-164">Hello exemple de code suivant montre comment toodelete un objet blob.</span><span class="sxs-lookup"><span data-stu-id="962cf-164">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="962cf-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="962cf-165">Next steps</span></span>
<span data-ttu-id="962cf-166">toolearn sur les tâches de stockage plus complexes, suivez ces liens :</span><span class="sxs-lookup"><span data-stu-id="962cf-166">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="962cf-167">Blog de l’équipe Azure Storage</span><span class="sxs-lookup"><span data-stu-id="962cf-167">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="962cf-168">[Kit de développement logiciel (SDK) Azure pour Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) sur GitHub</span><span class="sxs-lookup"><span data-stu-id="962cf-168">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="962cf-169">Transfert de données avec l’utilitaire de ligne de commande AzCopy de hello</span><span class="sxs-lookup"><span data-stu-id="962cf-169">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

