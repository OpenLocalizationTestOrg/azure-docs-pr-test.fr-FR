---
title: "Utilisation du stockage de files d’attente à partir de Ruby | Microsoft Docs"
description: "Découvrez comment utiliser le service de File d'attente Azure pour créer et supprimer des files d'attente, ainsi que pour insérer, récupérer et supprimer des messages. Les exemples sont écrits en Ruby."
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
ms.openlocfilehash: b1a7dd36af6c45bf085342cdf9c1c926a5040792
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-ruby"></a><span data-ttu-id="930d5-104">Utilisation du stockage de files d'attente à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="930d5-104">How to use Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="930d5-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="930d5-105">Overview</span></span>
<span data-ttu-id="930d5-106">Ce guide décrit le déroulement de scénarios courants dans le cadre de l’utilisation du service de stockage de files d’attente Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="930d5-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="930d5-107">Les exemples sont écrits à l'aide de l'API Ruby Azure.</span><span class="sxs-lookup"><span data-stu-id="930d5-107">The samples are written using the Ruby Azure API.</span></span>
<span data-ttu-id="930d5-108">Les scénarios traités incluent **l’insertion**, la **lecture furtive**, la **récupération** et la **suppression** des messages de file d’attente, ainsi que la **création et suppression des files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="930d5-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="930d5-109">Création d'une application Ruby</span><span class="sxs-lookup"><span data-stu-id="930d5-109">Create a Ruby Application</span></span>
<span data-ttu-id="930d5-110">Créez une application Ruby.</span><span class="sxs-lookup"><span data-stu-id="930d5-110">Create a Ruby application.</span></span> <span data-ttu-id="930d5-111">Pour obtenir des instructions, consultez [Application web Ruby on Rails sur une machine virtuelle Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="930d5-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="930d5-112">Configuration de votre application pour accéder au stockage</span><span class="sxs-lookup"><span data-stu-id="930d5-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="930d5-113">Pour utiliser Azure Storage, vous devez télécharger et utiliser le package Azure Ruby, qui inclut un ensemble de bibliothèques permettant de communiquer avec les services de stockage REST.</span><span class="sxs-lookup"><span data-stu-id="930d5-113">To use Azure storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="930d5-114">Utilisation de RubyGems pour obtenir le package</span><span class="sxs-lookup"><span data-stu-id="930d5-114">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="930d5-115">Ouvrez une interface de ligne de commande, telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="930d5-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="930d5-116">Tapez « gem install azure » dans la fenêtre de commande pour installer gem et les dépendances.</span><span class="sxs-lookup"><span data-stu-id="930d5-116">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="930d5-117">Importation du package</span><span class="sxs-lookup"><span data-stu-id="930d5-117">Import the package</span></span>
<span data-ttu-id="930d5-118">À l'aide de votre éditeur de texte, ajoutez la commande suivante au début du fichier Ruby où vous comptez utiliser le stockage :</span><span class="sxs-lookup"><span data-stu-id="930d5-118">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="930d5-119">Configuration d'une connexion Azure Storage</span><span class="sxs-lookup"><span data-stu-id="930d5-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="930d5-120">Le module Azure lit les variables d’environnement **AZURE\_STORAGE\_ACCOUNT** et **AZURE\_STORAGE\_ACCESS_KEY** pour obtenir les informations nécessaires à la connexion à votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="930d5-120">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="930d5-121">Si ces variables d'environnement ne sont pas définies, vous devez spécifier les informations de compte avant d'utiliser **Azure::QueueService** avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="930d5-121">If these environment variables are not set, you must specify the account information before using **Azure::QueueService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="930d5-122">Pour obtenir ces valeurs à partir d’un compte de stockage classique ou Resource Manager sur le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="930d5-122">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="930d5-123">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="930d5-123">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="930d5-124">Accédez au compte de stockage que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="930d5-124">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="930d5-125">Dans le panneau Paramètres à droite, cliquez sur **Clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="930d5-125">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="930d5-126">Dans le panneau Clés d’accès qui apparaît, la clé d’accès 1 et la clé d’accès 2 sont affichées.</span><span class="sxs-lookup"><span data-stu-id="930d5-126">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="930d5-127">Vous pouvez utiliser les deux.</span><span class="sxs-lookup"><span data-stu-id="930d5-127">You can use either of these.</span></span> 
5. <span data-ttu-id="930d5-128">Cliquez sur l'icône de copie pour copier la clé dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="930d5-128">Click the copy icon to copy the key to the clipboard.</span></span> 

## <a name="how-to-create-a-queue"></a><span data-ttu-id="930d5-129">Création d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="930d5-129">How To: Create a Queue</span></span>
<span data-ttu-id="930d5-130">Le code suivant crée un objet **Azure::QueueService** , ce qui vous permet d'utiliser les files d'attente.</span><span class="sxs-lookup"><span data-stu-id="930d5-130">The following code creates a **Azure::QueueService** object, which enables you to work with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="930d5-131">Utilisez la méthode **create_queue()** pour créer une file d’attente comportant le nom spécifié.</span><span class="sxs-lookup"><span data-stu-id="930d5-131">Use the **create_queue()** method to create a queue with the specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="930d5-132">Insertion d'un message dans une file d'attente</span><span class="sxs-lookup"><span data-stu-id="930d5-132">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="930d5-133">Pour insérer un message dans une file d’attente, utilisez la méthode **create_message()** pour créer un message et l’ajouter à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="930d5-133">To insert a message into a queue, use the **create_message()** method to create a new message and add it to the queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="930d5-134">Lecture furtive du message suivant</span><span class="sxs-lookup"><span data-stu-id="930d5-134">How To: Peek at the Next Message</span></span>
<span data-ttu-id="930d5-135">Vous pouvez lire furtivement le message au début de la file d’attente sans l’enlever de la file d’attente en appelant la méthode **peek\_messages()**.</span><span class="sxs-lookup"><span data-stu-id="930d5-135">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages()** method.</span></span> <span data-ttu-id="930d5-136">Par défaut, **peek\_messages()** lit furtivement un seul message.</span><span class="sxs-lookup"><span data-stu-id="930d5-136">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="930d5-137">Vous pouvez également spécifier le nombre de messages que vous souhaitez lire furtivement.</span><span class="sxs-lookup"><span data-stu-id="930d5-137">You can also specify how many messages you want to peek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="930d5-138">Suppression du message suivant dans la file d'attente</span><span class="sxs-lookup"><span data-stu-id="930d5-138">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="930d5-139">Vous pouvez supprimer un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="930d5-139">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="930d5-140">Lorsque vous appelez **list\_messages()**, vous obtenez le message suivant dans une file d’attente par défaut.</span><span class="sxs-lookup"><span data-stu-id="930d5-140">When you call **list\_messages()**, you get the next message in a queue by default.</span></span> <span data-ttu-id="930d5-141">Vous pouvez également spécifier le nombre de messages que vous souhaitez obtenir.</span><span class="sxs-lookup"><span data-stu-id="930d5-141">You can also specify how many messages you want to get.</span></span> <span data-ttu-id="930d5-142">Les messages renvoyés par **list\_messages()** deviennent invisibles aux autres codes lisant les messages de cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="930d5-142">The messages returned from **list\_messages()** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="930d5-143">Vous transmettez le délai d'expiration de la visibilité en secondes en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="930d5-143">You pass in the visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="930d5-144">Pour finaliser la suppression du message de la file d’attente, vous devez aussi appeler **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="930d5-144">To finish removing the message from the queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="930d5-145">Ce processus de suppression d’un message en deux étapes garantit que, si votre code ne parvient pas à traiter un message à cause d’une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et réessayer.</span><span class="sxs-lookup"><span data-stu-id="930d5-145">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="930d5-146">Votre code appelle **delete\_message()** juste après le traitement du message.</span><span class="sxs-lookup"><span data-stu-id="930d5-146">Your code calls **delete\_message()** right after the message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="930d5-147">Modification du contenu d'un message en file d'attente</span><span class="sxs-lookup"><span data-stu-id="930d5-147">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="930d5-148">Vous pouvez modifier le contenu d'un message placé dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="930d5-148">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="930d5-149">Le code ci-dessous utilise la méthode **update_message()** pour mettre à jour un message.</span><span class="sxs-lookup"><span data-stu-id="930d5-149">The code below uses the **update_message()** method to update a message.</span></span> <span data-ttu-id="930d5-150">La méthode renvoie un tuple qui contient l'accusé pop du message de file d'attente et une valeur de date et d'heure TUC représentant le moment où le message sera visible dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="930d5-150">The method will return a tuple which contains the pop receipt of the queue message and a UTC date time value that represents when the message will be visible on the queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="930d5-151">Options supplémentaires pour la suppression des messages dans la file d'attente</span><span class="sxs-lookup"><span data-stu-id="930d5-151">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="930d5-152">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="930d5-152">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="930d5-153">Vous pouvez obtenir un lot de messages.</span><span class="sxs-lookup"><span data-stu-id="930d5-153">You can get a batch of message.</span></span>
2. <span data-ttu-id="930d5-154">Vous pouvez définir un délai d'expiration de l'invisibilité plus long ou plus court afin d'accorder à votre code plus ou moins de temps pour traiter complètement chaque message.</span><span class="sxs-lookup"><span data-stu-id="930d5-154">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="930d5-155">L’exemple de code suivant utilise la méthode **list\_messages()** pour obtenir 15 messages en un appel.</span><span class="sxs-lookup"><span data-stu-id="930d5-155">The following code example uses the **list\_messages()** method to get 15 messages in one call.</span></span> <span data-ttu-id="930d5-156">Ensuite, il imprime et supprime chaque message.</span><span class="sxs-lookup"><span data-stu-id="930d5-156">Then it prints and deletes each message.</span></span> <span data-ttu-id="930d5-157">Il définit également le délai d'expiration de l'invisibilité sur cinq minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="930d5-157">It also sets the invisibility timeout to five minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="930d5-158">Obtention de la longueur de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="930d5-158">How To: Get the Queue Length</span></span>
<span data-ttu-id="930d5-159">Vous pouvez obtenir une estimation du nombre de messages dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="930d5-159">You can get an estimation of the number of messages in the queue.</span></span> <span data-ttu-id="930d5-160">La méthode **get\_queue\_metadata()** demande au service de File d’attente de renvoyer le nombre de messages approximatif et les métadonnées relatives à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="930d5-160">The **get\_queue\_metadata()** method asks the queue service to return the approximate message count and metadata about the queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="930d5-161">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="930d5-161">How To: Delete a Queue</span></span>
<span data-ttu-id="930d5-162">Pour supprimer une file d’attente et tous les messages qu’elle contient, appelez la méthode **delete\_queue()** sur l’objet file d’attente.</span><span class="sxs-lookup"><span data-stu-id="930d5-162">To delete a queue and all the messages contained in it, call the **delete\_queue()** method on the queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="930d5-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="930d5-163">Next Steps</span></span>
<span data-ttu-id="930d5-164">Maintenant que vous connaissez les bases du stockage des files d'attente, consultez les liens suivants pour apprendre à exécuter les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="930d5-164">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="930d5-165">Consultez le [blog de l'équipe Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="930d5-165">Visit the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="930d5-166">Accédez au référentiel du [Kit de développement logiciel (SDK) Azure pour Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="930d5-166">Visit the [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="930d5-167">Pour obtenir une comparaison entre le service de File d’attente Azure abordé dans cette rubrique et les files d’attente Azure Service Bus abordées dans la rubrique [Utilisation des files d’attente Service Bus](/develop/ruby/how-to-guides/service-bus-queues/), consultez la page [Files d’attente Azure et files d’attente Service Bus : comparaison et différences](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md).</span><span class="sxs-lookup"><span data-stu-id="930d5-167">For a comparison between the Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in the [How to use Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>