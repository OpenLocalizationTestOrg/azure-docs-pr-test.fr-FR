---
title: "Prise en main du Stockage File d’attente Azure et des services connectés de Visual Studio (ASP.NET) | Microsoft Docs"
description: "Comment prendre en main le Stockage File d’attente Azure dans un projet ASP.NET dans Visual Studio après s’être connecté à un compte de stockage à l’aide des services connectés de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: kraigb
ms.openlocfilehash: 4687e5dfce72583728068c176d86d100313badf6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="104e8-103">Prise en main du Stockage File d’attente Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="104e8-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="104e8-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="104e8-104">Overview</span></span>

<span data-ttu-id="104e8-105">Le stockage de files d’attente Azure fournit une messagerie cloud entre les composants d’application.</span><span class="sxs-lookup"><span data-stu-id="104e8-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="104e8-106">Lors de la conception d'applications pour la mise à l'échelle, des composants d'application sont souvent découplés, de sorte qu'ils peuvent être mis à l'échelle indépendamment.</span><span class="sxs-lookup"><span data-stu-id="104e8-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="104e8-107">Le stockage de files d’attente offre une messagerie asynchrone pour la communication entre les composants d’application, qu’ils soient exécutés dans le cloud, sur le bureau, sur un serveur local ou sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="104e8-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="104e8-108">Le stockage de files d’attente prend également en charge la gestion des tâches asynchrones et la création des flux de travail de processus.</span><span class="sxs-lookup"><span data-stu-id="104e8-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="104e8-109">Ce didacticiel montre comment écrire du code ASP.NET pour des scénarios courants en utilisant des entités de stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="104e8-109">This tutorial shows how to write ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="104e8-110">Ces scénarios incluent des tâches courantes telles que la création d’une file d’attente Azure, l'ajout, la modification, la lecture et la suppression de messages de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="104e8-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="104e8-111">Prerequisites</span></span>

* [<span data-ttu-id="104e8-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="104e8-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="104e8-113">Compte Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="104e8-113">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="104e8-114">Créer un contrôleur MVC</span><span class="sxs-lookup"><span data-stu-id="104e8-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="104e8-115">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Contrôleurs**, puis sélectionnez **Ajouter -> Contrôleur** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="104e8-115">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Ajouter un contrôleur à une application ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="104e8-117">Dans la boîte de dialogue **Ajouter la structure**, cliquez sur **Contrôleur MVC 5 - vide**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="104e8-117">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Spécifier le type de contrôleur MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="104e8-119">Dans la boîte de dialogue **Ajouter un contrôleur**, nommez le contrôleur *QueuesController*, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="104e8-119">On the **Add Controller** dialog, name the controller *QueuesController*, and select **Add**.</span></span>

    ![Nommer le contrôleur MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="104e8-121">Ajoutez les directives *using* suivantes au fichier `QueuesController.cs` :</span><span class="sxs-lookup"><span data-stu-id="104e8-121">Add the following *using* directives to the `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="104e8-122">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="104e8-122">Create a queue</span></span>

<span data-ttu-id="104e8-123">Les étapes suivantes montrent comment créer une file d'attente :</span><span class="sxs-lookup"><span data-stu-id="104e8-123">The following steps illustrate how to create a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="104e8-124">Cette section suppose que vous avez effectué les étapes [Configuration de l’environnement de développement](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="104e8-124">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="104e8-125">Ouvrez le fichier `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="104e8-125">Open the `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="104e8-126">Ajoutez une méthode appelée **CreateQueue** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="104e8-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="104e8-127">Dans la méthode **CreateQueue**, ajoutez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="104e8-127">Within the **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="104e8-128">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure : (Remplacez *&lt;storage-account-name>* par le nom du compte de stockage Azure auquel accéder.)</span><span class="sxs-lookup"><span data-stu-id="104e8-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="104e8-129">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="104e8-130">Obtenez un objet **CloudQueue** représentant une référence au nom de la file d’attente souhaitée.</span><span class="sxs-lookup"><span data-stu-id="104e8-130">Get a **CloudQueue** object that represents a reference to the desired queue name.</span></span> <span data-ttu-id="104e8-131">La méthode **CloudQueueClient.GetQueueReference** n’effectue pas de demande auprès du stockage de files d'attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-131">The **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="104e8-132">La référence est renvoyée, que la file d'attente existe ou non.</span><span class="sxs-lookup"><span data-stu-id="104e8-132">The reference is returned whether or not the queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="104e8-133">Appelez la méthode **CloudQueue.CreateIfNotExists** pour créer la file d’attente, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="104e8-133">Call the **CloudQueue.CreateIfNotExists** method to create the queue if it does not yet exist.</span></span> <span data-ttu-id="104e8-134">La méthode **CloudQueue.CreateIfNotExists** renvoie **true** si la file d’attente n’existe pas et a été correctement créée.</span><span class="sxs-lookup"><span data-stu-id="104e8-134">The **CloudQueue.CreateIfNotExists** method returns **true** if the queue does not exist, and is successfully created.</span></span> <span data-ttu-id="104e8-135">Sinon, la valeur **false** est retournée.</span><span class="sxs-lookup"><span data-stu-id="104e8-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="104e8-136">Mettez à jour l’objet **ViewBag** avec le nom de la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-136">Update the **ViewBag** with the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="104e8-137">Dans l’**Explorateur de solutions** de Visual Studio, développez le dossier **Vues**, cliquez avec le bouton droit sur **Files d'attente**, puis sélectionnez **Ajouter -> Vue** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="104e8-137">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="104e8-138">Dans la boîte de dialogue **Ajouter une vue**, entrez **CreateQueue** pour le nom de la vue, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="104e8-138">On the **Add View** dialog, enter **CreateQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="104e8-139">Ouvrez le fichier `CreateQueue.cshtml` et modifiez-le pour qu’il se présente comme l'extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-139">Open `CreateQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="104e8-140">Dans l’**Explorateur de solutions**, développez le dossier **Vues -> Partagé** et ouvrez le fichier `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="104e8-140">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="104e8-141">Après le dernier élément **Html.ActionLink**, ajoutez l’élément **Html.ActionLink** suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-141">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="104e8-142">Exécutez l’application, puis sélectionnez **Créer une file d'attente** pour afficher des résultats similaires à la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="104e8-142">Run the application, and select **Create queue** to see results similar to the following screen shot:</span></span>
  
    ![Créer la file d’attente](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="104e8-144">Comme mentionné précédemment, la méthode **CloudQueue.CreateIfNotExists** renvoie **true** uniquement lorsque la file d'attente n’existe pas et est créée.</span><span class="sxs-lookup"><span data-stu-id="104e8-144">As mentioned previously, the **CloudQueue.CreateIfNotExists** method returns **true** only when the queue doesn't exist and is created.</span></span> <span data-ttu-id="104e8-145">Par conséquent, si vous exécutez l’application alors que la file d'attente existe, la méthode renverra **false**.</span><span class="sxs-lookup"><span data-stu-id="104e8-145">Therefore, if you run the app when the queue exists, the method returns **false**.</span></span> <span data-ttu-id="104e8-146">Pour exécuter l’application plusieurs fois, vous devez supprimer la file d'attente avant d’exécuter à nouveau l’application.</span><span class="sxs-lookup"><span data-stu-id="104e8-146">To run the app multiple times, you must delete the queue before running the app again.</span></span> <span data-ttu-id="104e8-147">La suppression de la file d’attente peut être effectuée via la méthode **CloudQueue.Delete**.</span><span class="sxs-lookup"><span data-stu-id="104e8-147">Deleting the queue can be done via the **CloudQueue.Delete** method.</span></span> <span data-ttu-id="104e8-148">Vous pouvez également le faire à partir du [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou de l’[Explorateur de stockage Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="104e8-148">You can also delete the queue using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="104e8-149">Ajout d'un message à une file d'attente</span><span class="sxs-lookup"><span data-stu-id="104e8-149">Add a message to a queue</span></span>

<span data-ttu-id="104e8-150">Une fois que vous avez [créé une file d’attente](#create-a-queue), vous pouvez y ajouter des messages.</span><span class="sxs-lookup"><span data-stu-id="104e8-150">Once you've [created a queue](#create-a-queue), you can add messages to that queue.</span></span> <span data-ttu-id="104e8-151">Cette section vous guide dans le processus d'ajout d’un message à une file d’attente *test-queue*.</span><span class="sxs-lookup"><span data-stu-id="104e8-151">This section walks you through adding a message to a queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="104e8-152">Cette section suppose que vous avez effectué les étapes [Configuration de l’environnement de développement](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="104e8-152">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="104e8-153">Ouvrez le fichier `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="104e8-153">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="104e8-154">Ajoutez une méthode appelée **AddMessage** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="104e8-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="104e8-155">Dans la méthode **AddMessage**, ajoutez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="104e8-155">Within the **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="104e8-156">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure : (Remplacez *&lt;storage-account-name>* par le nom du compte de stockage Azure auquel accéder.)</span><span class="sxs-lookup"><span data-stu-id="104e8-156">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="104e8-157">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="104e8-158">Obtenez un objet **CloudQueueContainer** représentant une référence à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-158">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="104e8-159">Créez l’objet **CloudQueueMessage** représentant le message que vous souhaitez ajouter à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-159">Create the **CloudQueueMessage** object representing the message you want to add to the queue.</span></span> <span data-ttu-id="104e8-160">Un objet **CloudQueueMessage** peut être créé à partir d'une chaîne (au format UTF-8) ou d'un tableau d'octets.</span><span class="sxs-lookup"><span data-stu-id="104e8-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="104e8-161">Appelez la méthode **CloudQueue.AddMessage** pour ajouter le message à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-161">Call the **CloudQueue.AddMessage** method to add the messaged to the queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="104e8-162">Créez et définissez quelques propriétés**ViewBag** à afficher dans la vue.</span><span class="sxs-lookup"><span data-stu-id="104e8-162">Create and set a couple of **ViewBag** properties for display in the view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="104e8-163">Dans l’**Explorateur de solutions** de Visual Studio, développez le dossier **Vues**, cliquez avec le bouton droit sur **Files d'attente**, puis sélectionnez **Ajouter -> Vue** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="104e8-163">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="104e8-164">Dans la boîte de dialogue **Ajouter une vue**, entrez **AddMessage** pour le nom de la vue, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="104e8-164">On the **Add View** dialog, enter **AddMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="104e8-165">Ouvrez le fichier `AddMessage.cshtml` et modifiez-le pour qu’il se présente comme l'extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-165">Open `AddMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    The message '@ViewBag.Message' was added to the queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="104e8-166">Dans l’**Explorateur de solutions**, développez le dossier **Vues -> Partagé** et ouvrez le fichier `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="104e8-166">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="104e8-167">Après le dernier élément **Html.ActionLink**, ajoutez l’élément **Html.ActionLink** suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-167">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="104e8-168">Exécutez l’application, puis sélectionnez **Ajouter un message** pour afficher des résultats similaires à la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="104e8-168">Run the application, and select **Add message** to see results similar to the following screen shot:</span></span>
  
    ![Ajouter un message](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="104e8-170">Les deux sections - [Lire un message depuis une file d’attente, sans le supprimer](#read-a-message-from-a-queue-without-removing-it) et [Lire et supprimer un message dans une file d’attente](#read-and-remove-a-message-from-a-queue) montrent comment lire les messages d’une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-170">The two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how to read messages from a queue.</span></span>    

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="104e8-171">Lire un message depuis une file d’attente, sans le supprimer</span><span class="sxs-lookup"><span data-stu-id="104e8-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="104e8-172">Cette section illustre comment lire rapidement un message mis en file d’attente (c’est-à-dire lire le premier message sans le supprimer).</span><span class="sxs-lookup"><span data-stu-id="104e8-172">This section illustrates how to peek at a queued message (read the first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="104e8-173">Cette section suppose que vous avez effectué les étapes [Configuration de l’environnement de développement](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="104e8-173">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="104e8-174">Ouvrez le fichier `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="104e8-174">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="104e8-175">Ajoutez une méthode appelée **PeekMessage** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="104e8-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="104e8-176">Dans la méthode **PeekMessage**, ajoutez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="104e8-176">Within the **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="104e8-177">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure : (Remplacez *&lt;storage-account-name>* par le nom du compte de stockage Azure auquel accéder.)</span><span class="sxs-lookup"><span data-stu-id="104e8-177">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="104e8-178">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="104e8-179">Obtenez un objet **CloudQueueContainer** représentant une référence à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-179">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="104e8-180">Appelez la méthode **CloudQueue.PeekMessage** pour lire le premier message de la file d’attente, sans le supprimer.</span><span class="sxs-lookup"><span data-stu-id="104e8-180">Call the **CloudQueue.PeekMessage** method to read the first message in the queue without removing it from the queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="104e8-181">Mettez à jour l'objet **ViewBag** avec deux valeurs : le nom de la file d’attente et le message qui été lu.</span><span class="sxs-lookup"><span data-stu-id="104e8-181">Update the **ViewBag** with two values: the queue name and the message that was read.</span></span> <span data-ttu-id="104e8-182">L'objet **CloudQueueMessage** expose deux propriétés permettant d'obtenir la valeur de l'objet : **CloudQueueMessage.AsBytes** et **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="104e8-182">The **CloudQueueMessage** object exposes two properties for getting the object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="104e8-183">**AsString** (utilisé dans cet exemple) retourne une chaîne, tandis que **AsBytes** retourne un tableau d’octets.</span><span class="sxs-lookup"><span data-stu-id="104e8-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="104e8-184">Dans l’**Explorateur de solutions** de Visual Studio, développez le dossier **Vues**, cliquez avec le bouton droit sur **Files d'attente**, puis sélectionnez **Ajouter -> Vue** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="104e8-184">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="104e8-185">Dans la boîte de dialogue **Ajouter une vue**, entrez **PeekMessage** pour le nom de la vue, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="104e8-185">On the **Add View** dialog, enter **PeekMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="104e8-186">Ouvrez le fichier `PeekMessage.cshtml` et modifiez-le pour qu’il se présente comme l'extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-186">Open `PeekMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. <span data-ttu-id="104e8-187">Dans l’**Explorateur de solutions**, développez le dossier **Vues -> Partagé** et ouvrez le fichier `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="104e8-187">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="104e8-188">Après le dernier élément **Html.ActionLink**, ajoutez l’élément **Html.ActionLink** suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-188">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="104e8-189">Exécutez l’application, puis sélectionnez **Lire furtivement un message** pour afficher des résultats similaires à la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="104e8-189">Run the application, and select **Peek message** to see results similar to the following screen shot:</span></span>
  
    ![Lire furtivement un message](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="104e8-191">Lire et supprimer un message dans une file d’attente</span><span class="sxs-lookup"><span data-stu-id="104e8-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="104e8-192">Dans cette section, vous allez apprendre à lire et à supprimer un message d’une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-192">In this section, you learn how to read and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="104e8-193">Cette section suppose que vous avez effectué les étapes [Configuration de l’environnement de développement](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="104e8-193">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="104e8-194">Ouvrez le fichier `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="104e8-194">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="104e8-195">Ajoutez une méthode appelée **ReadMessage** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="104e8-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="104e8-196">Dans la méthode **ReadMessage**, ajoutez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="104e8-196">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="104e8-197">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure : (Remplacez *&lt;storage-account-name>* par le nom du compte de stockage Azure auquel accéder.)</span><span class="sxs-lookup"><span data-stu-id="104e8-197">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="104e8-198">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="104e8-199">Obtenez un objet **CloudQueueContainer** représentant une référence à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-199">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="104e8-200">Appelez la méthode **CloudQueue.GetMessage** pour lire le premier message de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-200">Call the **CloudQueue.GetMessage** method to read the first message in the queue.</span></span> <span data-ttu-id="104e8-201">La méthode **CloudQueue.GetMessage** rend le message invisible pendant 30 secondes (par défaut) pour tout autre code lisant les messages, afin qu’aucun autre code ne puisse modifier ou supprimer ce message pendant le traitement.</span><span class="sxs-lookup"><span data-stu-id="104e8-201">The **CloudQueue.GetMessage** method makes the message invisible for 30 seconds (by default) to any other code reading messages so that no other code can modify or delete the message while your processing it.</span></span> <span data-ttu-id="104e8-202">Pour modifier la durée d’invisibilité d’un message, changez la valeur du paramètre **visibilityTimeout** passé à la méthode **CloudQueue.GetMessage**.</span><span class="sxs-lookup"><span data-stu-id="104e8-202">To change the amount of time the message is invisible, modify the **visibilityTimeout** parameter being passed to the **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible to other code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="104e8-203">Appelez la méthode **CloudQueueMessage.Delete** pour supprimer le message dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-203">Call the **CloudQueueMessage.Delete** method to delete the message from the queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="104e8-204">Mettez à jour l’objet **ViewBag** avec le message supprimé et le nom de la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-204">Update the **ViewBag** with the message deleted, and the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="104e8-205">Dans l’**Explorateur de solutions** de Visual Studio, développez le dossier **Vues**, cliquez avec le bouton droit sur **Files d'attente**, puis sélectionnez **Ajouter -> Vue** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="104e8-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="104e8-206">Dans la boîte de dialogue **Ajouter une vue**, entrez **ReadMessage** pour le nom de la vue, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="104e8-206">On the **Add View** dialog, enter **ReadMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="104e8-207">Ouvrez le fichier `ReadMessage.cshtml` et modifiez-le pour qu’il se présente comme l'extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-207">Open `ReadMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. <span data-ttu-id="104e8-208">Dans l’**Explorateur de solutions**, développez le dossier **Vues -> Partagé** et ouvrez le fichier `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="104e8-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="104e8-209">Après le dernier élément **Html.ActionLink**, ajoutez l’élément **Html.ActionLink** suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="104e8-210">Exécutez l’application, puis sélectionnez **Lire et supprimer un message** pour afficher des résultats similaires à la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="104e8-210">Run the application, and select **Read/Delete message** to see results similar to the following screen shot:</span></span>
  
    ![Lire et supprimer un message](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-the-queue-length"></a><span data-ttu-id="104e8-212">Obtention de la longueur de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="104e8-212">Get the queue length</span></span>

<span data-ttu-id="104e8-213">Cette section montre comment obtenir la longueur de la file d’attente (nombre de messages).</span><span class="sxs-lookup"><span data-stu-id="104e8-213">This section illustrates how to get the queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="104e8-214">Cette section suppose que vous avez effectué les étapes [Configuration de l’environnement de développement](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="104e8-214">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="104e8-215">Ouvrez le fichier `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="104e8-215">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="104e8-216">Ajoutez une méthode appelée **GetQueueLength** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="104e8-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="104e8-217">Dans la méthode **ReadMessage**, ajoutez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="104e8-217">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="104e8-218">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure : (Remplacez *&lt;storage-account-name>* par le nom du compte de stockage Azure auquel accéder.)</span><span class="sxs-lookup"><span data-stu-id="104e8-218">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="104e8-219">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="104e8-220">Obtenez un objet **CloudQueueContainer** représentant une référence à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-220">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="104e8-221">Appelez la méthode **CloudQueue.FetchAttributes** pour récupérer les attributs de la file d’attente (y compris sa longueur).</span><span class="sxs-lookup"><span data-stu-id="104e8-221">Call the **CloudQueue.FetchAttributes** method to retrieve the queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="104e8-222">Accédez à la propriété **CloudQueue.ApproximateMessageCount** pour obtenir la longueur de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-222">Access the **CloudQueue.ApproximateMessageCount** property to get the queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="104e8-223">Mettez à jour l’objet **ViewBag** avec le nom de la file d'attente et sa longueur.</span><span class="sxs-lookup"><span data-stu-id="104e8-223">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="104e8-224">Dans l’**Explorateur de solutions** de Visual Studio, développez le dossier **Vues**, cliquez avec le bouton droit sur **Files d'attente**, puis sélectionnez **Ajouter -> Vue** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="104e8-224">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="104e8-225">Dans la boîte de dialogue **Ajouter une vue**, entrez **GetQueueLength** pour le nom de la vue, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="104e8-225">On the **Add View** dialog, enter **GetQueueLength** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="104e8-226">Ouvrez le fichier `GetQueueLengthMessage.cshtml` et modifiez-le pour qu’il se présente comme l'extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    The queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="104e8-227">Dans l’**Explorateur de solutions**, développez le dossier **Vues -> Partagé** et ouvrez le fichier `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="104e8-227">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="104e8-228">Après le dernier élément **Html.ActionLink**, ajoutez l’élément **Html.ActionLink** suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-228">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="104e8-229">Exécutez l’application, puis sélectionnez **Obtention de la longueur de la file d'attente** pour afficher des résultats similaires à la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="104e8-229">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Obtention de la longueur de la file d'attente](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="104e8-231">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="104e8-231">Delete a queue</span></span>
<span data-ttu-id="104e8-232">Cette section montre comment supprimer une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-232">This section illustrates how to delete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="104e8-233">Cette section suppose que vous avez effectué les étapes [Configuration de l’environnement de développement](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="104e8-233">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="104e8-234">Ouvrez le fichier `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="104e8-234">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="104e8-235">Ajoutez une méthode appelée **DeleteQueue** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="104e8-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="104e8-236">Dans la méthode **DeleteQueue**, ajoutez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="104e8-236">Within the **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="104e8-237">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure : (Remplacez *&lt;storage-account-name>* par le nom du compte de stockage Azure auquel accéder.)</span><span class="sxs-lookup"><span data-stu-id="104e8-237">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="104e8-238">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="104e8-239">Obtenez un objet **CloudQueueContainer** représentant une référence à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="104e8-239">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="104e8-240">Appelez la méthode **CloudQueue.Delete** pour supprimer la file d’attente représentée par l’objet **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="104e8-240">Call the **CloudQueue.Delete** method to delete the queue represented by the **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="104e8-241">Mettez à jour l’objet **ViewBag** avec le nom de la file d'attente et sa longueur.</span><span class="sxs-lookup"><span data-stu-id="104e8-241">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="104e8-242">Dans l’**Explorateur de solutions** de Visual Studio, développez le dossier **Vues**, cliquez avec le bouton droit sur **Files d'attente**, puis sélectionnez **Ajouter -> Vue** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="104e8-242">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="104e8-243">Dans la boîte de dialogue **Ajouter une vue**, entrez **DeleteQueue** pour le nom de la vue, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="104e8-243">On the **Add View** dialog, enter **DeleteQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="104e8-244">Ouvrez le fichier `DeleteQueue.cshtml` et modifiez-le pour qu’il se présente comme l'extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="104e8-245">Dans l’**Explorateur de solutions**, développez le dossier **Vues -> Partagé** et ouvrez le fichier `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="104e8-245">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="104e8-246">Après le dernier élément **Html.ActionLink**, ajoutez l’élément **Html.ActionLink** suivant :</span><span class="sxs-lookup"><span data-stu-id="104e8-246">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="104e8-247">Exécutez l’application, puis sélectionnez **Obtention de la longueur de la file d'attente** pour afficher des résultats similaires à la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="104e8-247">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Supprimer une file d'attente](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="104e8-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="104e8-249">Next steps</span></span>
<span data-ttu-id="104e8-250">Pour plus d’informations sur les autres options de stockage de données dans Azure, consultez d’autres guides de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="104e8-250">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="104e8-251">Prise en main du stockage d’objets blob Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="104e8-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="104e8-252">Prise en main du stockage de tables Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="104e8-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
