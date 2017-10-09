---
title: "aaaGet démarré avec stockage de file d’attente Azure et Visual Studio connecté Services (ASP.NET) | Documents Microsoft"
description: "Comment tooget démarrer à l’aide du stockage de file d’attente Azure dans un projet ASP.NET dans Visual Studio après la connexion de compte de stockage tooa à l’aide de Visual Studio Services connectés"
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
ms.openlocfilehash: 415a437c4ce60b1e2e328f8e937c73b0d5c50e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="f3453-103">Prise en main du Stockage File d’attente Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f3453-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="f3453-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="f3453-104">Overview</span></span>

<span data-ttu-id="f3453-105">Le stockage de files d’attente Azure fournit une messagerie cloud entre les composants d’application.</span><span class="sxs-lookup"><span data-stu-id="f3453-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="f3453-106">Lors de la conception d'applications pour la mise à l'échelle, des composants d'application sont souvent découplés, de sorte qu'ils peuvent être mis à l'échelle indépendamment.</span><span class="sxs-lookup"><span data-stu-id="f3453-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="f3453-107">Stockage de file d’attente fournit une messagerie asynchrone pour la communication entre les composants d’application, qu’elles s’exécutent dans le cloud hello, sur le bureau de hello, sur un serveur local ou sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="f3453-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="f3453-108">Le stockage de files d’attente prend également en charge la gestion des tâches asynchrones et la création des flux de travail de processus.</span><span class="sxs-lookup"><span data-stu-id="f3453-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="f3453-109">Ce didacticiel montre comment toowrite ASP.NET de code pour les scénarios courants à l’aide des entités de stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="f3453-109">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="f3453-110">Ces scénarios incluent des tâches courantes telles que la création d’une file d’attente Azure, l'ajout, la modification, la lecture et la suppression de messages de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="f3453-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f3453-111">Prerequisites</span></span>

* [<span data-ttu-id="f3453-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f3453-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="f3453-113">Compte Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="f3453-113">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="f3453-114">Créer un contrôleur MVC</span><span class="sxs-lookup"><span data-stu-id="f3453-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="f3453-115">Bonjour **l’Explorateur de solutions**, avec le bouton droit **contrôleurs**et, dans le menu contextuel de hello, sélectionnez **Ajouter -> contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="f3453-115">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Ajouter une application ASP.NET MVC de tooan contrôleur](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="f3453-117">Sur hello **ajouter une vue de structure** boîte de dialogue, sélectionnez **contrôleur MVC 5 - vide**, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f3453-117">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Spécifier le type de contrôleur MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="f3453-119">Sur hello **ajouter un contrôleur** boîte de dialogue, nom hello du contrôleur *QueuesController*, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f3453-119">On hello **Add Controller** dialog, name hello controller *QueuesController*, and select **Add**.</span></span>

    ![Contrôleur MVC de hello nom](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="f3453-121">Ajoutez hello suivant *à l’aide de* directives toohello `QueuesController.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="f3453-121">Add hello following *using* directives toohello `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="f3453-122">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="f3453-122">Create a queue</span></span>

<span data-ttu-id="f3453-123">Hello étapes suivantes illustrent comment toocreate une file d’attente :</span><span class="sxs-lookup"><span data-stu-id="f3453-123">hello following steps illustrate how toocreate a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="f3453-124">Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="f3453-124">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="f3453-125">Ouvrez hello `QueuesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="f3453-125">Open hello `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="f3453-126">Ajoutez une méthode appelée **CreateQueue** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f3453-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="f3453-127">Au sein de hello **CreateQueue** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f3453-127">Within hello **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f3453-128">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="f3453-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="f3453-129">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="f3453-130">Obtenir un **CloudQueue** objet qui représente un nom de file d’attente de toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="f3453-130">Get a **CloudQueue** object that represents a reference toohello desired queue name.</span></span> <span data-ttu-id="f3453-131">Hello **CloudQueueClient.GetQueueReference** méthode ne rend pas une demande de stockage de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-131">hello **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="f3453-132">référence de Hello est retournée que file d’attente hello existe ou non.</span><span class="sxs-lookup"><span data-stu-id="f3453-132">hello reference is returned whether or not hello queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="f3453-133">Appelez hello **CloudQueue.CreateIfNotExists** file d’attente de hello de toocreate méthode s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="f3453-133">Call hello **CloudQueue.CreateIfNotExists** method toocreate hello queue if it does not yet exist.</span></span> <span data-ttu-id="f3453-134">Hello **CloudQueue.CreateIfNotExists** méthode retourne **true** si la file d’attente hello n’existe pas et a été correctement créé.</span><span class="sxs-lookup"><span data-stu-id="f3453-134">hello **CloudQueue.CreateIfNotExists** method returns **true** if hello queue does not exist, and is successfully created.</span></span> <span data-ttu-id="f3453-135">Sinon, la valeur **false** est retournée.</span><span class="sxs-lookup"><span data-stu-id="f3453-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="f3453-136">Hello de mise à jour **ViewBag** avec nom hello de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="f3453-136">Update hello **ViewBag** with hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="f3453-137">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="f3453-137">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f3453-138">Sur hello **ajouter une vue** boîte de dialogue, entrez **CreateQueue** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f3453-138">On hello **Add View** dialog, enter **CreateQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="f3453-139">Ouvrez `CreateQueue.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="f3453-139">Open `CreateQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="f3453-140">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f3453-140">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f3453-141">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f3453-141">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="f3453-142">Exécutez l’application hello et sélectionnez **Create queue** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="f3453-142">Run hello application, and select **Create queue** toosee results similar toohello following screen shot:</span></span>
  
    ![Créer la file d’attente](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="f3453-144">Comme mentionné précédemment, hello **CloudQueue.CreateIfNotExists** méthode retourne **true** uniquement lorsque la file d’attente de hello n’existe pas et est créée.</span><span class="sxs-lookup"><span data-stu-id="f3453-144">As mentioned previously, hello **CloudQueue.CreateIfNotExists** method returns **true** only when hello queue doesn't exist and is created.</span></span> <span data-ttu-id="f3453-145">Par conséquent, si vous exécutez une application hello lors de la file d’attente hello existe, méthode hello retourne **false**.</span><span class="sxs-lookup"><span data-stu-id="f3453-145">Therefore, if you run hello app when hello queue exists, hello method returns **false**.</span></span> <span data-ttu-id="f3453-146">toorun hello application plusieurs fois, vous devez la supprimer hello avant de réexécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="f3453-146">toorun hello app multiple times, you must delete hello queue before running hello app again.</span></span> <span data-ttu-id="f3453-147">File d’attente de suppression hello peut être effectuée via hello **CloudQueue.Delete** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f3453-147">Deleting hello queue can be done via hello **CloudQueue.Delete** method.</span></span> <span data-ttu-id="f3453-148">Vous pouvez également supprimer la file d’attente hello à l’aide de hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="f3453-148">You can also delete hello queue using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="f3453-149">Ajouter une file d’attente de messages tooa</span><span class="sxs-lookup"><span data-stu-id="f3453-149">Add a message tooa queue</span></span>

<span data-ttu-id="f3453-150">Une fois que vous avez [créé une file d’attente](#create-a-queue), vous pouvez ajouter la file d’attente de messages toothat.</span><span class="sxs-lookup"><span data-stu-id="f3453-150">Once you've [created a queue](#create-a-queue), you can add messages toothat queue.</span></span> <span data-ttu-id="f3453-151">Cette section vous explique comment ajouter une file d’attente de messages tooa *test-file d’attente*.</span><span class="sxs-lookup"><span data-stu-id="f3453-151">This section walks you through adding a message tooa queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="f3453-152">Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="f3453-152">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="f3453-153">Ouvrez hello `QueuesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="f3453-153">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="f3453-154">Ajoutez une méthode appelée **AddMessage** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f3453-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="f3453-155">Au sein de hello **AddMessage** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f3453-155">Within hello **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f3453-156">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="f3453-156">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="f3453-157">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="f3453-158">Obtenir un **CloudQueueContainer** objet qui représente une file d’attente de toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="f3453-158">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="f3453-159">Créer hello **CloudQueueMessage** objet représentant la file d’attente de tooadd toohello message de type hello.</span><span class="sxs-lookup"><span data-stu-id="f3453-159">Create hello **CloudQueueMessage** object representing hello message you want tooadd toohello queue.</span></span> <span data-ttu-id="f3453-160">Un objet **CloudQueueMessage** peut être créé à partir d'une chaîne (au format UTF-8) ou d'un tableau d'octets.</span><span class="sxs-lookup"><span data-stu-id="f3453-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="f3453-161">Appelez hello **CloudQueue.AddMessage** file d’attente de méthode tooadd hello toohello de messages.</span><span class="sxs-lookup"><span data-stu-id="f3453-161">Call hello **CloudQueue.AddMessage** method tooadd hello messaged toohello queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="f3453-162">Créez et définissez quelques **ViewBag** propriétés à afficher dans la vue de hello.</span><span class="sxs-lookup"><span data-stu-id="f3453-162">Create and set a couple of **ViewBag** properties for display in hello view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="f3453-163">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="f3453-163">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f3453-164">Sur hello **ajouter une vue** boîte de dialogue, entrez **AddMessage** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f3453-164">On hello **Add View** dialog, enter **AddMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="f3453-165">Ouvrez `AddMessage.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="f3453-165">Open `AddMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="f3453-166">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f3453-166">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f3453-167">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f3453-167">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="f3453-168">Exécutez l’application hello et sélectionnez **Ajouter message** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="f3453-168">Run hello application, and select **Add message** toosee results similar toohello following screen shot:</span></span>
  
    ![Ajouter un message](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="f3453-170">Hello deux sections - [lire un message à partir d’une file d’attente sans le supprimer](#read-a-message-from-a-queue-without-removing-it) et [lire et supprimer un message à partir d’une file d’attente](#read-and-remove-a-message-from-a-queue) -illustrent comment tooread les messages à partir d’une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-170">hello two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how tooread messages from a queue.</span></span>  

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="f3453-171">Lire un message depuis une file d’attente, sans le supprimer</span><span class="sxs-lookup"><span data-stu-id="f3453-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="f3453-172">Cette section illustre comment toopeek un message en file d’attente (lecture hello premier message sans le supprimer).</span><span class="sxs-lookup"><span data-stu-id="f3453-172">This section illustrates how toopeek at a queued message (read hello first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="f3453-173">Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="f3453-173">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="f3453-174">Ouvrez hello `QueuesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="f3453-174">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="f3453-175">Ajoutez une méthode appelée **PeekMessage** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f3453-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="f3453-176">Au sein de hello **PeekMessage** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f3453-176">Within hello **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f3453-177">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="f3453-177">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="f3453-178">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="f3453-179">Obtenir un **CloudQueueContainer** objet qui représente une file d’attente de toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="f3453-179">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="f3453-180">Appelez hello **CloudQueue.PeekMessage** méthode tooread premier message de type hello dans la file d’attente hello sans le supprimer de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="f3453-180">Call hello **CloudQueue.PeekMessage** method tooread hello first message in hello queue without removing it from hello queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="f3453-181">Hello de mise à jour **ViewBag** avec deux valeurs : nom de file d’attente hello et le message de type hello qui a été lu.</span><span class="sxs-lookup"><span data-stu-id="f3453-181">Update hello **ViewBag** with two values: hello queue name and hello message that was read.</span></span> <span data-ttu-id="f3453-182">Hello **CloudQueueMessage** objet expose deux propriétés pour obtenir la valeur de l’objet hello : **CloudQueueMessage.AsBytes** et **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="f3453-182">hello **CloudQueueMessage** object exposes two properties for getting hello object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="f3453-183">**AsString** (utilisé dans cet exemple) retourne une chaîne, tandis que **AsBytes** retourne un tableau d’octets.</span><span class="sxs-lookup"><span data-stu-id="f3453-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="f3453-184">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="f3453-184">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f3453-185">Sur hello **ajouter une vue** boîte de dialogue, entrez **PeekMessage** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f3453-185">On hello **Add View** dialog, enter **PeekMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="f3453-186">Ouvrez `PeekMessage.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="f3453-186">Open `PeekMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="f3453-187">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f3453-187">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f3453-188">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f3453-188">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="f3453-189">Exécutez l’application hello et sélectionnez **Peek messages** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="f3453-189">Run hello application, and select **Peek message** toosee results similar toohello following screen shot:</span></span>
  
    ![Lire furtivement un message](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="f3453-191">Lire et supprimer un message dans une file d’attente</span><span class="sxs-lookup"><span data-stu-id="f3453-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="f3453-192">Dans cette section, vous apprendrez comment tooread et supprimer un message d’une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-192">In this section, you learn how tooread and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="f3453-193">Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="f3453-193">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="f3453-194">Ouvrez hello `QueuesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="f3453-194">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="f3453-195">Ajoutez une méthode appelée **ReadMessage** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f3453-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="f3453-196">Au sein de hello **lueMessage** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f3453-196">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f3453-197">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="f3453-197">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="f3453-198">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="f3453-199">Obtenir un **CloudQueueContainer** objet qui représente une file d’attente de toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="f3453-199">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="f3453-200">Appelez hello **CloudQueue.GetMessage** méthode tooread premier message de type hello dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="f3453-200">Call hello **CloudQueue.GetMessage** method tooread hello first message in hello queue.</span></span> <span data-ttu-id="f3453-201">Hello **CloudQueue.GetMessage** méthode rend hello invisible du message pour tooany de 30 secondes (par défaut) de tout autre code afin qu’aucun autre code pour modifier ou supprimer le message de type hello votre traitement lors de la lecture des messages.</span><span class="sxs-lookup"><span data-stu-id="f3453-201">hello **CloudQueue.GetMessage** method makes hello message invisible for 30 seconds (by default) tooany other code reading messages so that no other code can modify or delete hello message while your processing it.</span></span> <span data-ttu-id="f3453-202">toochange hello de message de type hello temps est invisible, modifier hello **visibilityTimeout** paramètre passé toohello **CloudQueue.GetMessage** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f3453-202">toochange hello amount of time hello message is invisible, modify hello **visibilityTimeout** parameter being passed toohello **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="f3453-203">Appelez hello **CloudQueueMessage.Delete** message d’appel de méthode toodelete à partir de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="f3453-203">Call hello **CloudQueueMessage.Delete** method toodelete hello message from hello queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="f3453-204">Hello de mise à jour **ViewBag** avec hello message supprimé et hello nom de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="f3453-204">Update hello **ViewBag** with hello message deleted, and hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="f3453-205">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="f3453-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f3453-206">Sur hello **ajouter une vue** boîte de dialogue, entrez **lueMessage** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f3453-206">On hello **Add View** dialog, enter **ReadMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="f3453-207">Ouvrez `ReadMessage.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="f3453-207">Open `ReadMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="f3453-208">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f3453-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f3453-209">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f3453-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="f3453-210">Exécutez l’application hello et sélectionnez **lecture ou suppression message** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="f3453-210">Run hello application, and select **Read/Delete message** toosee results similar toohello following screen shot:</span></span>
  
    ![Lire et supprimer un message](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a><span data-ttu-id="f3453-212">Obtenir la longueur de file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="f3453-212">Get hello queue length</span></span>

<span data-ttu-id="f3453-213">Cette section illustre comment tooget hello longueur de file d’attente (nombre de messages).</span><span class="sxs-lookup"><span data-stu-id="f3453-213">This section illustrates how tooget hello queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="f3453-214">Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="f3453-214">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="f3453-215">Ouvrez hello `QueuesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="f3453-215">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="f3453-216">Ajoutez une méthode appelée **GetQueueLength** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f3453-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="f3453-217">Au sein de hello **lueMessage** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f3453-217">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f3453-218">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="f3453-218">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="f3453-219">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="f3453-220">Obtenir un **CloudQueueContainer** objet qui représente une file d’attente de toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="f3453-220">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="f3453-221">Appelez hello **CloudQueue.FetchAttributes** les attributs de méthode tooretrieve hello la file d’attente (y compris sa longueur).</span><span class="sxs-lookup"><span data-stu-id="f3453-221">Call hello **CloudQueue.FetchAttributes** method tooretrieve hello queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="f3453-222">Hello d’accès **CloudQueue.ApproximateMessageCount** longueur de la propriété tooget hello la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-222">Access hello **CloudQueue.ApproximateMessageCount** property tooget hello queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="f3453-223">Hello de mise à jour **ViewBag** avec nom hello de file d’attente hello et sa longueur.</span><span class="sxs-lookup"><span data-stu-id="f3453-223">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="f3453-224">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="f3453-224">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f3453-225">Sur hello **ajouter une vue** boîte de dialogue, entrez **GetQueueLength** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f3453-225">On hello **Add View** dialog, enter **GetQueueLength** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="f3453-226">Ouvrez `GetQueueLengthMessage.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="f3453-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="f3453-227">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f3453-227">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f3453-228">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f3453-228">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="f3453-229">Exécutez l’application hello et sélectionnez **obtenir la longueur de file d’attente** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="f3453-229">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Obtention de la longueur de la file d'attente](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="f3453-231">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="f3453-231">Delete a queue</span></span>
<span data-ttu-id="f3453-232">Cette section illustre comment toodelete une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-232">This section illustrates how toodelete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="f3453-233">Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="f3453-233">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="f3453-234">Ouvrez hello `QueuesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="f3453-234">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="f3453-235">Ajoutez une méthode appelée **DeleteQueue** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f3453-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="f3453-236">Au sein de hello **DeleteQueue** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f3453-236">Within hello **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f3453-237">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="f3453-237">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="f3453-238">Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="f3453-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="f3453-239">Obtenir un **CloudQueueContainer** objet qui représente une file d’attente de toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="f3453-239">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="f3453-240">Appelez hello **CloudQueue.Delete** file d’attente de méthode toodelete hello représenté par hello **CloudQueue** objet.</span><span class="sxs-lookup"><span data-stu-id="f3453-240">Call hello **CloudQueue.Delete** method toodelete hello queue represented by hello **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="f3453-241">Hello de mise à jour **ViewBag** avec nom hello de file d’attente hello et sa longueur.</span><span class="sxs-lookup"><span data-stu-id="f3453-241">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="f3453-242">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="f3453-242">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f3453-243">Sur hello **ajouter une vue** boîte de dialogue, entrez **DeleteQueue** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f3453-243">On hello **Add View** dialog, enter **DeleteQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="f3453-244">Ouvrez `DeleteQueue.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="f3453-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="f3453-245">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f3453-245">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f3453-246">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f3453-246">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="f3453-247">Exécutez l’application hello et sélectionnez **obtenir la longueur de file d’attente** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="f3453-247">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Supprimer une file d'attente](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="f3453-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f3453-249">Next steps</span></span>
<span data-ttu-id="f3453-250">Permet d’afficher plusieurs toolearn de repères de fonctionnalité sur les options supplémentaires pour le stockage des données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f3453-250">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="f3453-251">Prise en main du stockage d’objets blob Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f3453-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="f3453-252">Prise en main du stockage de tables Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f3453-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
