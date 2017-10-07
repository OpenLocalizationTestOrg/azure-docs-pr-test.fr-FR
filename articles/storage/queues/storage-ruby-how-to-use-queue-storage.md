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
ms.openlocfilehash: c8eacac058442419cb9e8fe62cb69ad7ef1e2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a><span data-ttu-id="4b6d0-104">Comment toouse stockage de file d’attente à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="4b6d0-104">How toouse Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="4b6d0-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4b6d0-105">Overview</span></span>
<span data-ttu-id="4b6d0-106">Ce guide vous explique comment tooperform des scénarios courants utilisant hello service de stockage de file d’attente Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="4b6d0-107">exemples de Hello sont écrites à l’aide de hello Ruby Azure API.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-107">hello samples are written using hello Ruby Azure API.</span></span>
<span data-ttu-id="4b6d0-108">Hello scénarios abordés incluent **insertion**, **lecture**, **mise en route**, et **suppression** file d’attente de messages, ainsi que  **Création et suppression de files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="4b6d0-109">Création d'une application Ruby</span><span class="sxs-lookup"><span data-stu-id="4b6d0-109">Create a Ruby Application</span></span>
<span data-ttu-id="4b6d0-110">Créez une application Ruby.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-110">Create a Ruby application.</span></span> <span data-ttu-id="4b6d0-111">Pour obtenir des instructions, consultez [Application web Ruby on Rails sur une machine virtuelle Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="4b6d0-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="4b6d0-112">Configurer votre Application tooAccess stockage</span><span class="sxs-lookup"><span data-stu-id="4b6d0-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="4b6d0-113">toouse stockage Azure, vous devez toodownload et utilisez hello Ruby package azure, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-113">toouse Azure storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="4b6d0-114">Utiliser le package hello tooobtain RubyGems</span><span class="sxs-lookup"><span data-stu-id="4b6d0-114">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="4b6d0-115">Ouvrez une interface de ligne de commande, telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="4b6d0-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="4b6d0-116">Tapez « marque installer azure » dans les dépendances et le marque hello tooinstall hello commande fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-116">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="4b6d0-117">Importer un package hello</span><span class="sxs-lookup"><span data-stu-id="4b6d0-117">Import hello package</span></span>
<span data-ttu-id="4b6d0-118">Éditeur de texte favori, ajoutez hello suivant haut toohello Hello Ruby fichier où vous avez l’intention toouse stockage :</span><span class="sxs-lookup"><span data-stu-id="4b6d0-118">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="4b6d0-119">Configuration d'une connexion Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4b6d0-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="4b6d0-120">module de Hello azure lira des variables d’environnement hello **AZURE\_stockage\_compte** et **AZURE\_stockage\_ACCESS_KEY** pour compte de stockage Azure tooconnect tooyour les informations requises.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-120">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="4b6d0-121">Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello avant d’utiliser **Azure::QueueService** avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="4b6d0-121">If these environment variables are not set, you must specify hello account information before using **Azure::QueueService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="4b6d0-122">tooobtain ces valeurs à partir d’un classique ou de stockage du Gestionnaire de ressources du compte Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="4b6d0-122">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="4b6d0-123">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b6d0-123">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4b6d0-124">Accédez à compte de stockage toohello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-124">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="4b6d0-125">Dans le panneau des paramètres hello sur hello droit, cliquez sur **clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-125">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="4b6d0-126">Dans hello accès clés panneau qui s’affiche, vous verrez la clé d’accès hello 1 et la clé d’accès 2.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-126">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="4b6d0-127">Vous pouvez utiliser les deux.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-127">You can use either of these.</span></span> 
5. <span data-ttu-id="4b6d0-128">Cliquez sur le Presse-papiers toocopy hello toohello clé hello copie icône.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-128">Click hello copy icon toocopy hello key toohello clipboard.</span></span> 

## <a name="how-to-create-a-queue"></a><span data-ttu-id="4b6d0-129">Création d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="4b6d0-129">How To: Create a Queue</span></span>
<span data-ttu-id="4b6d0-130">Hello de code suivant crée un **Azure::QueueService** objet, ce qui vous permet de toowork avec les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-130">hello following code creates a **Azure::QueueService** object, which enables you toowork with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="4b6d0-131">Hello d’utilisation **create_queue()** méthode toocreate une file d’attente avec hello spécifié de nom.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-131">Use hello **create_queue()** method toocreate a queue with hello specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="4b6d0-132">Insertion d'un message dans une file d'attente</span><span class="sxs-lookup"><span data-stu-id="4b6d0-132">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="4b6d0-133">tooinsert un message dans une file d’attente, utilisez hello **create_message()** méthode toocreate un nouveau message et l’ajouter à la file d’attente de toohello.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-133">tooinsert a message into a queue, use hello **create_message()** method toocreate a new message and add it toohello queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="4b6d0-134">Comment : Lire des hello Message suivant</span><span class="sxs-lookup"><span data-stu-id="4b6d0-134">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="4b6d0-135">Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **aperçu\_messages()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="4b6d0-135">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages()** method.</span></span> <span data-ttu-id="4b6d0-136">Par défaut, **peek\_messages()** lit furtivement un seul message.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-136">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="4b6d0-137">Vous pouvez également spécifier le nombre de messages souhaité toopeek.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-137">You can also specify how many messages you want toopeek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="4b6d0-138">Procédure : Enlever hello Message suivant</span><span class="sxs-lookup"><span data-stu-id="4b6d0-138">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="4b6d0-139">Vous pouvez supprimer un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-139">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="4b6d0-140">Lorsque vous appelez **liste\_messages()**, vous obtenez un message de type hello suivante dans une file d’attente par défaut.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-140">When you call **list\_messages()**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="4b6d0-141">Vous pouvez également spécifier le nombre de messages souhaité tooget.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-141">You can also specify how many messages you want tooget.</span></span> <span data-ttu-id="4b6d0-142">Hello les messages retournés à partir de **liste\_messages()** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-142">hello messages returned from **list\_messages()** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="4b6d0-143">Vous passez dans un délai de visibilité hello dans les secondes sous la forme d’un paramètre.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-143">You pass in hello visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="4b6d0-144">toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez également appeler **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-144">toofinish removing hello message from hello queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="4b6d0-145">Ce processus en deux étapes de la suppression d’un message garantit que lorsque votre tooprocess échoue de code un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message et essayez à nouveau.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-145">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="4b6d0-146">Votre code appelle **supprimer\_message()** juste après le message de salutation a été traité.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-146">Your code calls **delete\_message()** right after hello message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="4b6d0-147">Comment : Modifier hello du contenu d’un Message en file d’attente</span><span class="sxs-lookup"><span data-stu-id="4b6d0-147">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="4b6d0-148">Vous pouvez modifier le contenu de hello d’un message en place dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-148">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="4b6d0-149">code Hello ci-dessous utilise hello **update_message()** méthode tooupdate un message.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-149">hello code below uses hello **update_message()** method tooupdate a message.</span></span> <span data-ttu-id="4b6d0-150">méthode Hello retourne un tuple qui contient l’accusé de réception pop hello du message de file d’attente hello et une valeur d’heure date UTC représentant le moment où le message de type hello seront visible sur la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-150">hello method will return a tuple which contains hello pop receipt of hello queue message and a UTC date time value that represents when hello message will be visible on hello queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="4b6d0-151">Options supplémentaires pour la suppression des messages dans la file d'attente</span><span class="sxs-lookup"><span data-stu-id="4b6d0-151">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="4b6d0-152">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-152">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="4b6d0-153">Vous pouvez obtenir un lot de messages.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-153">You can get a batch of message.</span></span>
2. <span data-ttu-id="4b6d0-154">Vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-154">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="4b6d0-155">exemple de code suivant Hello utilise hello **liste\_messages()** messages tooget 15 de méthode dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-155">hello following code example uses hello **list\_messages()** method tooget 15 messages in one call.</span></span> <span data-ttu-id="4b6d0-156">Ensuite, il imprime et supprime chaque message.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-156">Then it prints and deletes each message.</span></span> <span data-ttu-id="4b6d0-157">Il définit également hello invisibilité délai d’expiration toofive minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-157">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="4b6d0-158">Comment : Obtenir hello longueur de file d’attente</span><span class="sxs-lookup"><span data-stu-id="4b6d0-158">How To: Get hello Queue Length</span></span>
<span data-ttu-id="4b6d0-159">Vous pouvez obtenir une estimation du nombre de hello de messages dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-159">You can get an estimation of hello number of messages in hello queue.</span></span> <span data-ttu-id="4b6d0-160">Hello **obtenir\_file d’attente\_metadata()** méthode demande nombre approximatif de messages de hello file d’attente service tooreturn hello et les métadonnées sur la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-160">hello **get\_queue\_metadata()** method asks hello queue service tooreturn hello approximate message count and metadata about hello queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="4b6d0-161">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="4b6d0-161">How To: Delete a Queue</span></span>
<span data-ttu-id="4b6d0-162">toodelete une file d’attente et tous les messages hello qu’il contient, appel hello **supprimer\_queue()** méthode sur un objet de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-162">toodelete a queue and all hello messages contained in it, call hello **delete\_queue()** method on hello queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="4b6d0-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b6d0-163">Next Steps</span></span>
<span data-ttu-id="4b6d0-164">Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente, suivez ces toolearn des liens sur les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="4b6d0-164">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="4b6d0-165">Visitez hello [Blog de l’équipe stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="4b6d0-165">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="4b6d0-166">Visitez hello [Azure SDK pour Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) référentiel sur GitHub</span><span class="sxs-lookup"><span data-stu-id="4b6d0-166">Visit hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="4b6d0-167">Pour obtenir une comparaison entre hello Service de file d’attente Azure présentés dans cet article et les files d’attente de Azure Service Bus présentés dans hello [comment toouse files d’attente du Bus de Service](/develop/ruby/how-to-guides/service-bus-queues/) l’article, consultez [files d’attente Azure et files d’attente de Service Bus - comparées et Différences](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="4b6d0-167">For a comparison between hello Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in hello [How toouse Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>
