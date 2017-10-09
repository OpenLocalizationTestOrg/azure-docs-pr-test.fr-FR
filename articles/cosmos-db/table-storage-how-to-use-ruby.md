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
# <a name="how-toouse-azure-table-storage-from-ruby"></a>Comment toouse le stockage de Table à partir de Ruby
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Vue d'ensemble
Ce guide vous explique comment tooperform des scénarios courants utilisant hello service Table Azure. exemples de Hello sont écrites à l’aide de hello Ruby API. Hello scénarios abordés incluent **création et suppression d’une table, insérer et l’interrogation des entités dans une table**.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Création d'une application Ruby
Pour obtenir des instructions toocreate une application Ruby, voir [Ruby sur l’application Web de Rails sur une machine virtuelle Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurer votre application de tooaccess stockage
toouse stockage Azure, vous devez toodownload et utilisez hello Ruby package azure qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services de stockage reste hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utiliser le package hello tooobtain RubyGems
1. Ouvrez une interface de ligne de commande, telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).
2. Type **azure d’installation marque** de marque de hello commande fenêtre tooinstall hello et des dépendances.

### <a name="import-hello-package"></a>Importer un package hello
Éditeur de texte favori, ajoutez hello suivant haut toohello Hello Ruby fichier où vous avez l’intention toouse stockage :

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Configurer une connexion Azure Storage
Bonjour azure module lit les variables d’environnement hello **AZURE\_stockage\_compte** et **AZURE\_stockage\_accès\_clé**pour plus d’informations requises au compte de stockage Azure tooconnect tooyour. Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello avant d’utiliser **Azure::TableService** avec hello suivant de code :

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain ces valeurs à partir d’un classique ou de stockage du Gestionnaire de ressources du compte Bonjour portail Azure :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Accédez à compte de stockage toohello que vous souhaitez toouse.
3. Dans le panneau des paramètres hello sur hello droit, cliquez sur **clés d’accès**.
4. Dans hello accès clés panneau qui s’affiche, vous verrez la clé d’accès hello 1 et la clé d’accès 2. Vous pouvez utiliser les deux.
5. Cliquez sur le Presse-papiers toocopy hello toohello clé hello copie icône.

## <a name="create-a-table"></a>Création d’une table
Hello **Azure::TableService** objet vous permet de travailler avec des tables et des entités. toocreate une table, utilisez hello **créer\_table()** (méthode). Hello exemple suivant crée une table ou commander des photos hello erreur cas échéant.

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a>Ajouter une table de tooa d’entité
tooadd une entité, d’abord créer un objet de hachage qui définit les propriétés de l’entité. Notez que pour chaque entité, vous devez spécifier les clés **PartitionKey** et **RowKey**. Ces sont des identificateurs uniques de vos entités hello et sont des valeurs qui peuvent être interrogées beaucoup plus rapidement que les autres propriétés. Le stockage Azure utilise **PartitionKey** tooautomatically distribuer les entités de la table hello sur plusieurs nœuds de stockage. Les entités avec hello même **PartitionKey** sont stockés sur hello même nœud. Hello **RowKey** est hello des ID unique de l’entité hello au sein de la partition hello auquel il appartient.

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>Mise à jour d'une entité
Il existe plusieurs tooupdate de méthodes disponibles pour une entité existante :

* **update\_entity() :** met à jour une entité existante en la remplaçant.
* **fusion\_entity() :** met à jour une entité existante en fusionnant les nouvelles valeurs de propriété dans une entité existante de hello.
* **insert\_or\_merge\_entity() :** met à jour une entité existante en la remplaçant. En l'absence d'entité, une nouvelle entité est insérée.
* **Insérer\_ou\_remplacer\_entity() :** met à jour une entité existante en fusionnant les nouvelles valeurs de propriété dans une entité existante de hello. En l'absence d'entité, une nouvelle entité est insérée.

Hello exemple suivant illustre la mise à jour une entité à l’aide de **mettre à jour\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

Avec **mettre à jour\_entity()** et **fusion\_entity()**, si l’entité hello que vous mettez à jour n’existe pas, opération de mise à jour hello échouera. Par conséquent, si vous le souhaitez toostore une entité, même si elle existe déjà, vous devez utiliser **insérer\_ou\_remplacer\_entity()** ou **insérer\_ou \_fusion\_entity()**.

## <a name="work-with-groups-of-entities"></a>Utilisation des groupes d'entités
Il est parfois sens toosubmit plusieurs opérations ensemble dans un lot tooensure atomique de traitement par le serveur de hello. tooaccomplish, tout d’abord créer un **lot** de l’objet, puis utilisez hello **exécuter\_batch()** méthode sur **TableService**. Hello exemple suivant montre envoi de deux entités dotées de RowKey 2 et 3 dans un lot. Notez qu’il uniquement fonctionne pour les entités avec hello même PartitionKey.

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>Interrogation d’une entité
tooquery une entité dans une table, utilisez hello **obtenir\_entity()** (méthode), en passant le nom de la table hello, **PartitionKey** et **RowKey**.

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>Interrogation d’un ensemble d’entités
tooquery un ensemble d’entités dans une table, créez un objet de hachage de requête et utilisez hello **requête\_entities()** (méthode). Hello exemple suivant illustre l’obtention de toutes les entités de hello avec hello même **PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> Si le jeu de résultats hello est trop grande pour un tooreturn de requête unique, un jeton de liaison est retourné que vous pouvez utiliser les pages suivantes de tooretrieve.
>
>

## <a name="query-a-subset-of-entity-properties"></a>Interrogation d’un sous-ensemble de propriétés d’entité
Une table de tooa de requête peut récupérer des propriétés peu d’une entité. Cette technique, nommée « projection », réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses. Clause select de hello utilisation et les noms de hello passe de hello propriétés que vous aimeriez toobring sur toohello client.

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>Suppression d’une entité
toodelete une entité, utilisez hello **supprimer\_entity()** (méthode). Vous devez toopass nom hello de table hello qui contient l’entité de hello, hello PartitionKey et RowKey d’entité de hello.

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>Suppression d’une table
toodelete une table, utilisez hello **supprimer\_table()** (méthode) et passez nom hello de hello table que vous souhaitez toodelete.

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>Étapes suivantes

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.
* [Kit de développement logiciel (SDK) Azure pour Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) sur GitHub

