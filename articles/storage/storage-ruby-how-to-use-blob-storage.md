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
# <a name="how-toouse-blob-storage-from-ruby"></a>Comment toouse stockage d’objets Blob à partir de Ruby
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Vue d'ensemble
Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB. Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application. Stockage d’objets BLOB est également référencé tooas stockage d’objets.

Ce guide vous explique comment les scénarios courants tooperform à l’aide du stockage d’objets Blob. exemples de Hello sont écrites à l’aide de hello Ruby API. Hello scénarios abordés incluent **téléchargement, en téléchargeant,** et **suppression** objets BLOB.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Création d'une application Ruby
Créez une application Ruby. Pour obtenir des instructions, consultez [Application web Ruby on Rails sur une machine virtuelle Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)

## <a name="configure-your-application-tooaccess-storage"></a>Configurer votre application de tooaccess stockage
toouse stockage Azure, vous devez toodownload et utilisez hello Ruby package azure, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utiliser le package hello tooobtain RubyGems
1. Ouvrez une interface de ligne de commande, telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).
2. Tapez « marque installer azure » dans les dépendances et le marque hello tooinstall hello commande fenêtre.

### <a name="import-hello-package"></a>Importer un package hello
À l’aide de votre éditeur de texte favori, ajoutez hello suivant haut toohello Hello Ruby fichier où vous avez l’intention toouse stockage :

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Configuration d’une connexion Stockage Azure
module de Hello azure lira des variables d’environnement hello **AZURE\_stockage\_compte** et **AZURE\_stockage\_ACCESS_KEY** pour compte de stockage Azure tooconnect tooyour les informations requises. Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello avant d’utiliser **Azure::Blob::BlobService** avec hello suivant de code :

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

tooobtain ces valeurs à partir d’un stockage classique compte dans le portail Azure classic de hello :

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Accédez à compte de stockage toohello que vous souhaitez toouse.
3. Cliquez sur **gérer les clés d’accès** bas hello hello du volet de navigation.
4. Vous verrez dans la boîte de dialogue contextuelle hello, nom de compte de stockage hello, clé d’accès primaire et clé d’accès secondaire. Pour la clé d’accès, vous pouvez utiliser hello principale ou hello secondaire.
5. Cliquez sur le Presse-papiers toocopy hello toohello clé hello copie icône.

## <a name="create-a-container"></a>Créez un conteneur.
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Hello **Azure::Blob::BlobService** objet vous permet de travailler avec les conteneurs et objets BLOB. toocreate un conteneur, utilisez hello **créer\_container()** (méthode).

Hello exemple de code suivant crée un conteneur ou imprime les erreurs de hello cas échéant.

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

Si vous souhaitez toomake les fichiers de hello dans le conteneur de hello public, vous pouvez définir les autorisations du conteneur hello.

Vous pouvez modifier uniquement hello <strong>créer\_container()</strong> appel toopass hello **: public\_accès\_niveau** option :

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

Les valeurs valides pour hello **: public\_accès\_niveau** option sont :

* **blob :** spécifie un accès public en lecture pour les objets blob. Les données d'objets blob à l'intérieur de ce conteneur peuvent être lues via une demande anonyme, mais les données du conteneur ne sont pas disponibles. Les clients ne peuvent pas énumérer les objets BLOB conteneur hello via une demande anonyme.
* **conteneur** : spécifie un accès public total en lecture pour le conteneur et les données d’objets blob. Les clients peuvent énumérer des objets BLOB dans le conteneur hello via une demande anonyme, mais ne peut pas énumérer des conteneurs dans le compte de stockage hello.

Ou bien, vous pouvez modifier le niveau d’accès public hello d’un conteneur à l’aide de **définir\_conteneur\_acl()** le niveau d’accès public de méthode toospecify hello.

Hello modifications hello le niveau d’accès public trop des exemple de code suivant**conteneur**:

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a>Charger un objet blob dans un conteneur
objet blob de contenu tooa tooupload, utilisez hello **créer\_bloc\_blob()** objet blob de méthode toocreate hello, utilisez un fichier ou de chaîne en tant que contenu hello d’objet blob de hello.

Hello de code suivant télécharge les fichiers hello **test.png** comme un nouvel objet blob nommé « image-objet blob « hello conteneur.

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a>Répertorier les objets BLOB hello dans un conteneur
utiliser des conteneurs de hello toolist **list_containers()** (méthode).
utiliser des objets BLOB de hello toolist dans un conteneur, **liste\_blobs()** (méthode).

Cela génère des URL hello de tous les objets BLOB de hello dans tous les conteneurs de hello pour le compte de hello.

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a>Télécharger des objets blob
objets BLOB toodownload, utilisez hello **obtenir\_blob()** contenu de méthode tooretrieve hello.

Hello exemple de code suivant montre comment utiliser **obtenir\_blob()** toodownload hello le contenu de «-objet blob d’image » et de les écrire tooa des fichiers locaux.

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a>Suppression d'un objet blob
Enfin, toodelete un objet blob, utilisez hello **supprimer\_blob()** (méthode). Hello exemple de code suivant montre comment toodelete un objet blob.

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a>Étapes suivantes
toolearn sur les tâches de stockage plus complexes, suivez ces liens :

* [Blog de l’équipe Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)
* [Kit de développement logiciel (SDK) Azure pour Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) sur GitHub
* [Transfert de données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md)

