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
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a>Prise en main du Stockage File d’attente Azure et des services connectés de Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Vue d’ensemble

Le stockage de files d’attente Azure fournit une messagerie cloud entre les composants d’application. Lors de la conception d'applications pour la mise à l'échelle, des composants d'application sont souvent découplés, de sorte qu'ils peuvent être mis à l'échelle indépendamment. Stockage de file d’attente fournit une messagerie asynchrone pour la communication entre les composants d’application, qu’elles s’exécutent dans le cloud hello, sur le bureau de hello, sur un serveur local ou sur un appareil mobile. Le stockage de files d’attente prend également en charge la gestion des tâches asynchrones et la création des flux de travail de processus.

Ce didacticiel montre comment toowrite ASP.NET de code pour les scénarios courants à l’aide des entités de stockage de file d’attente Azure. Ces scénarios incluent des tâches courantes telles que la création d’une file d’attente Azure, l'ajout, la modification, la lecture et la suppression de messages de file d’attente.

##<a name="prerequisites"></a>Composants requis

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Créer un contrôleur MVC 

1. Bonjour **l’Explorateur de solutions**, avec le bouton droit **contrôleurs**et, dans le menu contextuel de hello, sélectionnez **Ajouter -> contrôleur**.

    ![Ajouter une application ASP.NET MVC de tooan contrôleur](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. Sur hello **ajouter une vue de structure** boîte de dialogue, sélectionnez **contrôleur MVC 5 - vide**, puis sélectionnez **ajouter**.

    ![Spécifier le type de contrôleur MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. Sur hello **ajouter un contrôleur** boîte de dialogue, nom hello du contrôleur *QueuesController*, puis sélectionnez **ajouter**.

    ![Contrôleur MVC de hello nom](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. Ajoutez hello suivant *à l’aide de* directives toohello `QueuesController.cs` fichier :

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a>Création d’une file d’attente

Hello étapes suivantes illustrent comment toocreate une file d’attente :

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment). 

1. Ouvrez hello `QueuesController.cs` fichier. 

1. Ajoutez une méthode appelée **CreateQueue** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Au sein de hello **CreateQueue** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. Obtenir un **CloudQueue** objet qui représente un nom de file d’attente de toohello de référence. Hello **CloudQueueClient.GetQueueReference** méthode ne rend pas une demande de stockage de la file d’attente. référence de Hello est retournée que file d’attente hello existe ou non. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Appelez hello **CloudQueue.CreateIfNotExists** file d’attente de hello de toocreate méthode s’il n’existe pas encore. Hello **CloudQueue.CreateIfNotExists** méthode retourne **true** si la file d’attente hello n’existe pas et a été correctement créé. Sinon, la valeur **false** est retournée.    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. Hello de mise à jour **ViewBag** avec nom hello de file d’attente hello.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **CreateQueue** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `CreateQueue.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. Exécutez l’application hello et sélectionnez **Create queue** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Créer la file d’attente](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    Comme mentionné précédemment, hello **CloudQueue.CreateIfNotExists** méthode retourne **true** uniquement lorsque la file d’attente de hello n’existe pas et est créée. Par conséquent, si vous exécutez une application hello lors de la file d’attente hello existe, méthode hello retourne **false**. toorun hello application plusieurs fois, vous devez la supprimer hello avant de réexécuter l’application hello. File d’attente de suppression hello peut être effectuée via hello **CloudQueue.Delete** (méthode). Vous pouvez également supprimer la file d’attente hello à l’aide de hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-a-message-tooa-queue"></a>Ajouter une file d’attente de messages tooa

Une fois que vous avez [créé une file d’attente](#create-a-queue), vous pouvez ajouter la file d’attente de messages toothat. Cette section vous explique comment ajouter une file d’attente de messages tooa *test-file d’attente*. 

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment). 

1. Ouvrez hello `QueuesController.cs` fichier.

1. Ajoutez une méthode appelée **AddMessage** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Au sein de hello **AddMessage** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obtenir un **CloudQueueContainer** objet qui représente une file d’attente de toohello de référence. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Créer hello **CloudQueueMessage** objet représentant la file d’attente de tooadd toohello message de type hello. Un objet **CloudQueueMessage** peut être créé à partir d'une chaîne (au format UTF-8) ou d'un tableau d'octets.

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. Appelez hello **CloudQueue.AddMessage** file d’attente de méthode tooadd hello toohello de messages.

    ```csharp
    queue.AddMessage(message);
    ```

1. Créez et définissez quelques **ViewBag** propriétés à afficher dans la vue de hello.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **AddMessage** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `AddMessage.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. Exécutez l’application hello et sélectionnez **Ajouter message** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Ajouter un message](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

Hello deux sections - [lire un message à partir d’une file d’attente sans le supprimer](#read-a-message-from-a-queue-without-removing-it) et [lire et supprimer un message à partir d’une file d’attente](#read-and-remove-a-message-from-a-queue) -illustrent comment tooread les messages à partir d’une file d’attente.  

## <a name="read-a-message-from-a-queue-without-removing-it"></a>Lire un message depuis une file d’attente, sans le supprimer

Cette section illustre comment toopeek un message en file d’attente (lecture hello premier message sans le supprimer).  

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment). 

1. Ouvrez hello `QueuesController.cs` fichier.

1. Ajoutez une méthode appelée **PeekMessage** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Au sein de hello **PeekMessage** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obtenir un **CloudQueueContainer** objet qui représente une file d’attente de toohello de référence. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Appelez hello **CloudQueue.PeekMessage** méthode tooread premier message de type hello dans la file d’attente hello sans le supprimer de la file d’attente hello. 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. Hello de mise à jour **ViewBag** avec deux valeurs : nom de file d’attente hello et le message de type hello qui a été lu. Hello **CloudQueueMessage** objet expose deux propriétés pour obtenir la valeur de l’objet hello : **CloudQueueMessage.AsBytes** et **CloudQueueMessage.AsString**. **AsString** (utilisé dans cet exemple) retourne une chaîne, tandis que **AsBytes** retourne un tableau d’octets.

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **PeekMessage** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `PeekMessage.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

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

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. Exécutez l’application hello et sélectionnez **Peek messages** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Lire furtivement un message](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a>Lire et supprimer un message dans une file d’attente

Dans cette section, vous apprendrez comment tooread et supprimer un message d’une file d’attente.   

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment). 

1. Ouvrez hello `QueuesController.cs` fichier.

1. Ajoutez une méthode appelée **ReadMessage** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Au sein de hello **lueMessage** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obtenir un **CloudQueueContainer** objet qui représente une file d’attente de toohello de référence. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Appelez hello **CloudQueue.GetMessage** méthode tooread premier message de type hello dans la file d’attente hello. Hello **CloudQueue.GetMessage** méthode rend hello invisible du message pour tooany de 30 secondes (par défaut) de tout autre code afin qu’aucun autre code pour modifier ou supprimer le message de type hello votre traitement lors de la lecture des messages. toochange hello de message de type hello temps est invisible, modifier hello **visibilityTimeout** paramètre passé toohello **CloudQueue.GetMessage** (méthode).

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. Appelez hello **CloudQueueMessage.Delete** message d’appel de méthode toodelete à partir de la file d’attente hello.

    ```csharp
    queue.DeleteMessage(message);
    ```

1. Hello de mise à jour **ViewBag** avec hello message supprimé et hello nom de file d’attente hello.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **lueMessage** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `ReadMessage.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

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

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. Exécutez l’application hello et sélectionnez **lecture ou suppression message** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Lire et supprimer un message](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a>Obtenir la longueur de file d’attente hello

Cette section illustre comment tooget hello longueur de file d’attente (nombre de messages). 

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment). 

1. Ouvrez hello `QueuesController.cs` fichier.

1. Ajoutez une méthode appelée **GetQueueLength** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Au sein de hello **lueMessage** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obtenir un **CloudQueueContainer** objet qui représente une file d’attente de toohello de référence. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Appelez hello **CloudQueue.FetchAttributes** les attributs de méthode tooretrieve hello la file d’attente (y compris sa longueur). 

    ```csharp
    queue.FetchAttributes();
    ```

6. Hello d’accès **CloudQueue.ApproximateMessageCount** longueur de la propriété tooget hello la file d’attente.
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. Hello de mise à jour **ViewBag** avec nom hello de file d’attente hello et sa longueur.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **GetQueueLength** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `GetQueueLengthMessage.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. Exécutez l’application hello et sélectionnez **obtenir la longueur de file d’attente** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Obtention de la longueur de la file d'attente](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a>Suppression d'une file d'attente
Cette section illustre comment toodelete une file d’attente. 

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello [configuration d’environnement de développement hello](#set-up-the-development-environment). 

1. Ouvrez hello `QueuesController.cs` fichier.

1. Ajoutez une méthode appelée **DeleteQueue** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Au sein de hello **DeleteQueue** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenez un objet **CloudQueueClient** représentant un client du service de File d’attente.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obtenir un **CloudQueueContainer** objet qui représente une file d’attente de toohello de référence. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Appelez hello **CloudQueue.Delete** file d’attente de méthode toodelete hello représenté par hello **CloudQueue** objet.

    ```csharp
    queue.Delete();
    ```

1. Hello de mise à jour **ViewBag** avec nom hello de file d’attente hello et sa longueur.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **les files d’attente**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **DeleteQueue** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `DeleteQueue.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. Exécutez l’application hello et sélectionnez **obtenir la longueur de file d’attente** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Supprimer une file d'attente](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a>Étapes suivantes
Permet d’afficher plusieurs toolearn de repères de fonctionnalité sur les options supplémentaires pour le stockage des données dans Azure.

  * [Prise en main du stockage d’objets blob Azure et des services connectés de Visual Studio (ASP.NET)](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [Prise en main du stockage de tables Azure et des services connectés de Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-tables.md)
