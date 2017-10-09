---
title: "aaaHow toouse le stockage de Table à partir de Ruby | Documents Microsoft"
description: "Stocker des données structurées dans le cloud hello avec le stockage Table Azure, un magasin de données NoSQL."
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 2f9eb5a9160b551d6d1d198869787070c402b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a><span data-ttu-id="c5850-103">Comment toouse le stockage de Table à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="c5850-103">How toouse Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="c5850-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c5850-104">Overview</span></span>
<span data-ttu-id="c5850-105">Ce guide vous explique comment tooperform des scénarios courants utilisant hello service Table Azure.</span><span class="sxs-lookup"><span data-stu-id="c5850-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="c5850-106">exemples de Hello sont écrites à l’aide de hello Ruby API.</span><span class="sxs-lookup"><span data-stu-id="c5850-106">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="c5850-107">Hello scénarios abordés incluent **création et suppression d’une table, insérer et l’interrogation des entités dans une table**.</span><span class="sxs-lookup"><span data-stu-id="c5850-107">hello scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="c5850-108">Création d'une application Ruby</span><span class="sxs-lookup"><span data-stu-id="c5850-108">Create a Ruby application</span></span>
<span data-ttu-id="c5850-109">Pour obtenir des instructions toocreate une application Ruby, voir [Ruby sur l’application Web de Rails sur une machine virtuelle Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="c5850-109">For instructions how toocreate a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="c5850-110">Configurer votre application de tooaccess stockage</span><span class="sxs-lookup"><span data-stu-id="c5850-110">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="c5850-111">toouse stockage Azure, vous devez toodownload et utilisez hello Ruby package azure qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services de stockage reste hello.</span><span class="sxs-lookup"><span data-stu-id="c5850-111">toouse Azure Storage, you need toodownload and use hello Ruby azure package which includes a set of convenience libraries that communicate with hello Storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="c5850-112">Utiliser le package hello tooobtain RubyGems</span><span class="sxs-lookup"><span data-stu-id="c5850-112">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="c5850-113">Ouvrez une interface de ligne de commande, telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="c5850-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="c5850-114">Type **azure d’installation marque** de marque de hello commande fenêtre tooinstall hello et des dépendances.</span><span class="sxs-lookup"><span data-stu-id="c5850-114">Type **gem install azure** in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="c5850-115">Importer un package hello</span><span class="sxs-lookup"><span data-stu-id="c5850-115">Import hello package</span></span>
<span data-ttu-id="c5850-116">Éditeur de texte favori, ajoutez hello suivant haut toohello Hello Ruby fichier où vous avez l’intention toouse stockage :</span><span class="sxs-lookup"><span data-stu-id="c5850-116">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="c5850-117">Configurer une connexion Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c5850-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="c5850-118">Bonjour azure module lit les variables d’environnement hello **AZURE\_stockage\_compte** et **AZURE\_stockage\_accès\_clé**pour plus d’informations requises au compte de stockage Azure tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="c5850-118">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required tooconnect tooyour Azure Storage account.</span></span> <span data-ttu-id="c5850-119">Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello avant d’utiliser **Azure::TableService** avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="c5850-119">If these environment variables are not set, you must specify hello account information before using **Azure::TableService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="c5850-120">tooobtain ces valeurs à partir d’un classique ou de stockage du Gestionnaire de ressources du compte Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="c5850-120">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="c5850-121">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c5850-121">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c5850-122">Accédez à compte de stockage toohello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="c5850-122">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="c5850-123">Dans le panneau des paramètres hello sur hello droit, cliquez sur **clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="c5850-123">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="c5850-124">Dans hello accès clés panneau qui s’affiche, vous verrez la clé d’accès hello 1 et la clé d’accès 2.</span><span class="sxs-lookup"><span data-stu-id="c5850-124">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="c5850-125">Vous pouvez utiliser les deux.</span><span class="sxs-lookup"><span data-stu-id="c5850-125">You can use either of these.</span></span>
5. <span data-ttu-id="c5850-126">Cliquez sur le Presse-papiers toocopy hello toohello clé hello copie icône.</span><span class="sxs-lookup"><span data-stu-id="c5850-126">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="c5850-127">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="c5850-127">Create a table</span></span>
<span data-ttu-id="c5850-128">Hello **Azure::TableService** objet vous permet de travailler avec des tables et des entités.</span><span class="sxs-lookup"><span data-stu-id="c5850-128">hello **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="c5850-129">toocreate une table, utilisez hello **créer\_table()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c5850-129">toocreate a table, use hello **create\_table()** method.</span></span> <span data-ttu-id="c5850-130">Hello exemple suivant crée une table ou commander des photos hello erreur cas échéant.</span><span class="sxs-lookup"><span data-stu-id="c5850-130">hello following example creates a table or prints hello error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="c5850-131">Ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="c5850-131">Add an entity tooa table</span></span>
<span data-ttu-id="c5850-132">tooadd une entité, d’abord créer un objet de hachage qui définit les propriétés de l’entité.</span><span class="sxs-lookup"><span data-stu-id="c5850-132">tooadd an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="c5850-133">Notez que pour chaque entité, vous devez spécifier les clés **PartitionKey** et **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="c5850-133">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="c5850-134">Ces sont des identificateurs uniques de vos entités hello et sont des valeurs qui peuvent être interrogées beaucoup plus rapidement que les autres propriétés.</span><span class="sxs-lookup"><span data-stu-id="c5850-134">These are hello unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="c5850-135">Le stockage Azure utilise **PartitionKey** tooautomatically distribuer les entités de la table hello sur plusieurs nœuds de stockage.</span><span class="sxs-lookup"><span data-stu-id="c5850-135">Azure Storage uses **PartitionKey** tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="c5850-136">Les entités avec hello même **PartitionKey** sont stockés sur hello même nœud.</span><span class="sxs-lookup"><span data-stu-id="c5850-136">Entities with hello same **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="c5850-137">Hello **RowKey** est hello des ID unique de l’entité hello au sein de la partition hello auquel il appartient.</span><span class="sxs-lookup"><span data-stu-id="c5850-137">hello **RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="c5850-138">Mise à jour d'une entité</span><span class="sxs-lookup"><span data-stu-id="c5850-138">Update an entity</span></span>
<span data-ttu-id="c5850-139">Il existe plusieurs tooupdate de méthodes disponibles pour une entité existante :</span><span class="sxs-lookup"><span data-stu-id="c5850-139">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="c5850-140">**update\_entity() :** met à jour une entité existante en la remplaçant.</span><span class="sxs-lookup"><span data-stu-id="c5850-140">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="c5850-141">**fusion\_entity() :** met à jour une entité existante en fusionnant les nouvelles valeurs de propriété dans une entité existante de hello.</span><span class="sxs-lookup"><span data-stu-id="c5850-141">**merge\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span>
* <span data-ttu-id="c5850-142">**insert\_or\_merge\_entity() :** met à jour une entité existante en la remplaçant.</span><span class="sxs-lookup"><span data-stu-id="c5850-142">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="c5850-143">En l'absence d'entité, une nouvelle entité est insérée.</span><span class="sxs-lookup"><span data-stu-id="c5850-143">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="c5850-144">**Insérer\_ou\_remplacer\_entity() :** met à jour une entité existante en fusionnant les nouvelles valeurs de propriété dans une entité existante de hello.</span><span class="sxs-lookup"><span data-stu-id="c5850-144">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span> <span data-ttu-id="c5850-145">En l'absence d'entité, une nouvelle entité est insérée.</span><span class="sxs-lookup"><span data-stu-id="c5850-145">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="c5850-146">Hello exemple suivant illustre la mise à jour une entité à l’aide de **mettre à jour\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="c5850-146">hello following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="c5850-147">Avec **mettre à jour\_entity()** et **fusion\_entity()**, si l’entité hello que vous mettez à jour n’existe pas, opération de mise à jour hello échouera.</span><span class="sxs-lookup"><span data-stu-id="c5850-147">With **update\_entity()** and **merge\_entity()**, if hello entity that you are updating doesn't exist then hello update operation will fail.</span></span> <span data-ttu-id="c5850-148">Par conséquent, si vous le souhaitez toostore une entité, même si elle existe déjà, vous devez utiliser **insérer\_ou\_remplacer\_entity()** ou **insérer\_ou \_fusion\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="c5850-148">Therefore if you wish toostore an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="c5850-149">Utilisation des groupes d'entités</span><span class="sxs-lookup"><span data-stu-id="c5850-149">Work with groups of entities</span></span>
<span data-ttu-id="c5850-150">Il est parfois sens toosubmit plusieurs opérations ensemble dans un lot tooensure atomique de traitement par le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="c5850-150">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="c5850-151">tooaccomplish, tout d’abord créer un **lot** de l’objet, puis utilisez hello **exécuter\_batch()** méthode sur **TableService**.</span><span class="sxs-lookup"><span data-stu-id="c5850-151">tooaccomplish that, you first create a **Batch** object and then use hello **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="c5850-152">Hello exemple suivant montre envoi de deux entités dotées de RowKey 2 et 3 dans un lot.</span><span class="sxs-lookup"><span data-stu-id="c5850-152">hello following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="c5850-153">Notez qu’il uniquement fonctionne pour les entités avec hello même PartitionKey.</span><span class="sxs-lookup"><span data-stu-id="c5850-153">Notice that it only works for entities with hello same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="c5850-154">Interrogation d’une entité</span><span class="sxs-lookup"><span data-stu-id="c5850-154">Query for an entity</span></span>
<span data-ttu-id="c5850-155">tooquery une entité dans une table, utilisez hello **obtenir\_entity()** (méthode), en passant le nom de la table hello, **PartitionKey** et **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="c5850-155">tooquery an entity in a table, use hello **get\_entity()** method, by passing hello table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="c5850-156">Interrogation d’un ensemble d’entités</span><span class="sxs-lookup"><span data-stu-id="c5850-156">Query a set of entities</span></span>
<span data-ttu-id="c5850-157">tooquery un ensemble d’entités dans une table, créez un objet de hachage de requête et utilisez hello **requête\_entities()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c5850-157">tooquery a set of entities in a table, create a query hash object and use hello **query\_entities()** method.</span></span> <span data-ttu-id="c5850-158">Hello exemple suivant illustre l’obtention de toutes les entités de hello avec hello même **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="c5850-158">hello following example demonstrates getting all hello entities with hello same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="c5850-159">Si le jeu de résultats hello est trop grande pour un tooreturn de requête unique, un jeton de liaison est retourné que vous pouvez utiliser les pages suivantes de tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="c5850-159">If hello result set is too large for a single query tooreturn, a continuation token will be returned which you can use tooretrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="c5850-160">Interrogation d’un sous-ensemble de propriétés d’entité</span><span class="sxs-lookup"><span data-stu-id="c5850-160">Query a subset of entity properties</span></span>
<span data-ttu-id="c5850-161">Une table de tooa de requête peut récupérer des propriétés peu d’une entité.</span><span class="sxs-lookup"><span data-stu-id="c5850-161">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="c5850-162">Cette technique, nommée « projection », réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses.</span><span class="sxs-lookup"><span data-stu-id="c5850-162">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="c5850-163">Clause select de hello utilisation et les noms de hello passe de hello propriétés que vous aimeriez toobring sur toohello client.</span><span class="sxs-lookup"><span data-stu-id="c5850-163">Use hello select clause and pass hello names of hello properties you would like toobring over toohello client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="c5850-164">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="c5850-164">Delete an entity</span></span>
<span data-ttu-id="c5850-165">toodelete une entité, utilisez hello **supprimer\_entity()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c5850-165">toodelete an entity, use hello **delete\_entity()** method.</span></span> <span data-ttu-id="c5850-166">Vous devez toopass nom hello de table hello qui contient l’entité de hello, hello PartitionKey et RowKey d’entité de hello.</span><span class="sxs-lookup"><span data-stu-id="c5850-166">You need toopass in hello name of hello table which contains hello entity, hello PartitionKey and RowKey of hello entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="c5850-167">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="c5850-167">Delete a table</span></span>
<span data-ttu-id="c5850-168">toodelete une table, utilisez hello **supprimer\_table()** (méthode) et passez nom hello de hello table que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="c5850-168">toodelete a table, use hello **delete\_table()** method and pass in hello name of hello table you want toodelete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="c5850-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c5850-169">Next steps</span></span>

* <span data-ttu-id="c5850-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="c5850-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="c5850-171">[Kit de développement logiciel (SDK) Azure pour Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) sur GitHub</span><span class="sxs-lookup"><span data-stu-id="c5850-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

