---
title: "aaaHow toouse stockage de file d’attente à partir de Ruby | Documents Microsoft"
description: "Découvrez comment toouse hello file d’attente Azure service toocreate et les files d’attente de suppression, insertion, obtenir et supprimer les messages. Les exemples sont écrits en Ruby."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a>Comment toouse stockage de file d’attente à partir de Ruby
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Vue d'ensemble
Ce guide vous explique comment tooperform des scénarios courants utilisant hello service de stockage de file d’attente Microsoft Azure. exemples de Hello sont écrites à l’aide de hello Ruby Azure API.
Hello scénarios abordés incluent **insertion**, **lecture**, **mise en route**, et **suppression** file d’attente de messages, ainsi que  **Création et suppression de files d’attente**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Création d'une application Ruby
Créez une application Ruby. Pour obtenir des instructions, consultez [Application web Ruby on Rails sur une machine virtuelle Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurer votre Application tooAccess stockage
toouse stockage Azure, vous devez toodownload et utilisez hello Ruby package azure, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utiliser le package hello tooobtain RubyGems
1. Ouvrez une interface de ligne de commande, telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).
2. Tapez « marque installer azure » dans les dépendances et le marque hello tooinstall hello commande fenêtre.

### <a name="import-hello-package"></a>Importer un package hello
Éditeur de texte favori, ajoutez hello suivant haut toohello Hello Ruby fichier où vous avez l’intention toouse stockage :

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a>Configuration d'une connexion Azure Storage
module de Hello azure lira des variables d’environnement hello **AZURE\_stockage\_compte** et **AZURE\_stockage\_ACCESS_KEY** pour compte de stockage Azure tooconnect tooyour les informations requises. Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello avant d’utiliser **Azure::QueueService** avec hello suivant de code :

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
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
4. Vous verrez dans la boîte de dialogue de hello, nom de compte de stockage hello, clé d’accès primaire et clé d’accès secondaire. Pour la clé d’accès, vous pouvez utiliser hello principale ou hello secondaire. 
5. Cliquez sur le Presse-papiers toocopy hello toohello clé hello copie icône.

## <a name="how-to-create-a-queue"></a>Création d'une file d'attente
Hello de code suivant crée un **Azure::QueueService** objet, ce qui vous permet de toowork avec les files d’attente.

```ruby
azure_queue_service = Azure::QueueService.new
```

Hello d’utilisation **create_queue()** méthode toocreate une file d’attente avec hello spécifié de nom.

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Insertion d'un message dans une file d'attente
tooinsert un message dans une file d’attente, utilisez hello **create_message()** méthode toocreate un nouveau message et l’ajouter à la file d’attente de toohello.

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a>Comment : Lire des hello Message suivant
Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **aperçu\_messages()** (méthode). Par défaut, **peek\_messages()** lit furtivement un seul message. Vous pouvez également spécifier le nombre de messages souhaité toopeek.

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a>Procédure : Enlever hello Message suivant
Vous pouvez supprimer un message d'une file d'attente en deux étapes.

1. Lorsque vous appelez **liste\_messages()**, vous obtenez un message de type hello suivante dans une file d’attente par défaut. Vous pouvez également spécifier le nombre de messages souhaité tooget. Hello les messages retournés à partir de **liste\_messages()** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente. Vous passez dans un délai de visibilité hello dans les secondes sous la forme d’un paramètre.
2. toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez également appeler **delete_message()**.

Ce processus en deux étapes de la suppression d’un message garantit que lorsque votre tooprocess échoue de code un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message et essayez à nouveau. Votre code appelle **supprimer\_message()** juste après le message de salutation a été traité.

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Comment : Modifier hello du contenu d’un Message en file d’attente
Vous pouvez modifier le contenu de hello d’un message en place dans la file d’attente hello. code Hello ci-dessous utilise hello **update_message()** méthode tooupdate un message. méthode Hello retourne un tuple qui contient l’accusé de réception pop hello du message de file d’attente hello et une valeur d’heure date UTC représentant le moment où le message de type hello seront visible sur la file d’attente hello.

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Options supplémentaires pour la suppression des messages dans la file d'attente
Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.

1. Vous pouvez obtenir un lot de messages.
2. Vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message.

exemple de code suivant Hello utilise hello **liste\_messages()** messages tooget 15 de méthode dans un seul appel. Ensuite, il imprime et supprime chaque message. Il définit également hello invisibilité délai d’expiration toofive minutes pour chaque message.

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a>Comment : Obtenir hello longueur de file d’attente
Vous pouvez obtenir une estimation du nombre de hello de messages dans la file d’attente hello. Hello **obtenir\_file d’attente\_metadata()** méthode demande nombre approximatif de messages de hello file d’attente service tooreturn hello et les métadonnées sur la file d’attente hello.

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a>Suppression d'une file d'attente
toodelete une file d’attente et tous les messages hello qu’il contient, appel hello **supprimer\_queue()** méthode sur un objet de file d’attente hello.

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente, suivez ces toolearn des liens sur les tâches de stockage plus complexes.

* Visitez hello [Blog de l’équipe stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Visitez hello [Azure SDK pour Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) référentiel sur GitHub

Pour obtenir une comparaison entre hello Service de file d’attente Azure présentés dans cet article et les files d’attente de Azure Service Bus présentés dans hello [comment toouse files d’attente du Bus de Service](/develop/ruby/how-to-guides/service-bus-queues/) l’article, consultez [files d’attente Azure et files d’attente de Service Bus - comparées et Différences](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)
