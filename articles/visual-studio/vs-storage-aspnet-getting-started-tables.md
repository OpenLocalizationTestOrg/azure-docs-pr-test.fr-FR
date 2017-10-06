---
title: "aaaGet a démarré avec le stockage de table Azure et Visual Studio connecté Services (ASP.NET) | Documents Microsoft"
description: "Comment tooget démarrer à l’aide du stockage de tables Azure dans un projet ASP.NET dans Visual Studio après la connexion de compte de stockage tooa à l’aide de Visual Studio Services connectés"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraigb
ms.openlocfilehash: 04f79db7aad60ca51c3c866da1f4b01d9e11ac52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="536ae-103">Prise en main du Stockage Table Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="536ae-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="536ae-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="536ae-104">Overview</span></span>

<span data-ttu-id="536ae-105">Stockage de Table Azure vous permet de toostore de grandes quantités de données structurées.</span><span class="sxs-lookup"><span data-stu-id="536ae-105">Azure Table storage enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="536ae-106">service de Hello est une banque de données NoSQL qui accepte des appels authentifiés provenant à l’intérieur et extérieur hello cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="536ae-106">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="536ae-107">Les tables Azure sont idéales pour le stockage des données structurées non relationnelles.</span><span class="sxs-lookup"><span data-stu-id="536ae-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="536ae-108">Ce didacticiel montre comment toowrite ASP.NET de code pour les scénarios courants à l’aide des entités de stockage de table Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="536ae-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="536ae-109">Ces scénarios incluent la création d’une table ainsi que l'ajout, l'interrogation et la suppression d’entités de table.</span><span class="sxs-lookup"><span data-stu-id="536ae-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="536ae-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="536ae-110">Prerequisites</span></span>

* [<span data-ttu-id="536ae-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="536ae-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="536ae-112">Compte Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="536ae-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="536ae-113">Créer un contrôleur MVC</span><span class="sxs-lookup"><span data-stu-id="536ae-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="536ae-114">Bonjour **l’Explorateur de solutions**, avec le bouton droit **contrôleurs**et, dans le menu contextuel de hello, sélectionnez **Ajouter -> contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="536ae-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Ajouter une application ASP.NET MVC de tooan contrôleur](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="536ae-116">Sur hello **ajouter une vue de structure** boîte de dialogue, sélectionnez **contrôleur MVC 5 - vide**, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="536ae-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Spécifier le type de contrôleur MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="536ae-118">Sur hello **ajouter un contrôleur** boîte de dialogue, nom hello du contrôleur *TablesController*, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="536ae-118">On hello **Add Controller** dialog, name hello controller *TablesController*, and select **Add**.</span></span>

    ![Contrôleur MVC de hello nom](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="536ae-120">Ajoutez hello suivant *à l’aide de* directives toohello `TablesController.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="536ae-120">Add hello following *using* directives toohello `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="536ae-121">Créer une classe de modèle</span><span class="sxs-lookup"><span data-stu-id="536ae-121">Create a model class</span></span>

<span data-ttu-id="536ae-122">La plupart des exemples hello dans cet article utilisent un **TableEntity**-classe appelée dérivée **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="536ae-122">Many of hello examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="536ae-123">Hello suit vous guide tout au long de déclarer cette classe comme une classe de modèle :</span><span class="sxs-lookup"><span data-stu-id="536ae-123">hello following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="536ae-124">Bonjour **l’Explorateur de solutions**, avec le bouton droit **modèles**et, dans le menu contextuel de hello, sélectionnez **Ajouter -> classe**.</span><span class="sxs-lookup"><span data-stu-id="536ae-124">In hello **Solution Explorer**, right-click **Models**, and, from hello context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="536ae-125">Sur hello **ajouter un nouvel élément** boîte de dialogue, le nom de la classe hello, **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="536ae-125">On hello **Add New Item** dialog, name hello class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="536ae-126">Ouvrez hello `CustomerEntity.cs` de fichiers et ajoutez hello suivant **à l’aide de** directive :</span><span class="sxs-lookup"><span data-stu-id="536ae-126">Open hello `CustomerEntity.cs` file, and add hello following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="536ae-127">Modifiez la classe hello, afin que, lorsque vous avez terminé, la classe hello est déclaré comme hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="536ae-127">Modify hello class so that, when finished, hello class is declared as in hello following code.</span></span> <span data-ttu-id="536ae-128">classe Hello déclare une classe d’entité appelée **CustomerEntity** qu’utilise hello prénom du client en tant que clé de ligne hello et le nom comme clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-128">hello class declares an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

    ```csharp
    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }
    }
    ```

## <a name="create-a-table"></a><span data-ttu-id="536ae-129">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="536ae-129">Create a table</span></span>

<span data-ttu-id="536ae-130">Hello étapes suivantes illustrent comment toocreate une table :</span><span class="sxs-lookup"><span data-stu-id="536ae-130">hello following steps illustrate how toocreate a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="536ae-131">Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="536ae-131">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="536ae-132">Ouvrez hello `TablesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="536ae-132">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="536ae-133">Ajoutez une méthode appelée **CreateTable** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="536ae-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="536ae-134">Au sein de hello **CreateTable** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="536ae-134">Within hello **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="536ae-135">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="536ae-135">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="536ae-136">Obtenez un objet **CloudTableClient** représentant un client du service de Table.</span><span class="sxs-lookup"><span data-stu-id="536ae-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="536ae-137">Obtenir un **CloudTable** objet qui représente un nom de référence toohello table souhaité.</span><span class="sxs-lookup"><span data-stu-id="536ae-137">Get a **CloudTable** object that represents a reference toohello desired table name.</span></span> <span data-ttu-id="536ae-138">Hello **CloudTableClient.GetTableReference** méthode ne rend pas une demande pour le stockage de table.</span><span class="sxs-lookup"><span data-stu-id="536ae-138">hello **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="536ae-139">référence de Hello est renvoyée hello table existe ou non.</span><span class="sxs-lookup"><span data-stu-id="536ae-139">hello reference is returned whether or not hello table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="536ae-140">Appelez hello **CloudTable.CreateIfNotExists** table de hello toocreate méthodes s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="536ae-140">Call hello **CloudTable.CreateIfNotExists** method toocreate hello table if it does not yet exist.</span></span> <span data-ttu-id="536ae-141">Hello **CloudTable.CreateIfNotExists** méthode retourne **true** si la table de hello n’existe pas et a été correctement créé.</span><span class="sxs-lookup"><span data-stu-id="536ae-141">hello **CloudTable.CreateIfNotExists** method returns **true** if hello table does not exist, and is successfully created.</span></span> <span data-ttu-id="536ae-142">Sinon, la valeur **false** est retournée.</span><span class="sxs-lookup"><span data-stu-id="536ae-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="536ae-143">Hello de mise à jour **ViewBag** avec nom hello de table de hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-143">Update hello **ViewBag** with hello name of hello table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="536ae-144">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="536ae-144">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="536ae-145">Sur hello **ajouter une vue** boîte de dialogue, entrez **CreateTable** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="536ae-145">On hello **Add View** dialog, enter **CreateTable** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="536ae-146">Ouvrez `CreateTable.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="536ae-146">Open `CreateTable.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="536ae-147">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="536ae-147">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="536ae-148">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="536ae-148">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="536ae-149">Exécutez l’application hello et sélectionnez **créer une table** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="536ae-149">Run hello application, and select **Create table** toosee results similar toohello following screen shot:</span></span>
  
    ![Créer une table](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="536ae-151">Comme mentionné précédemment, hello **CloudTable.CreateIfNotExists** méthode retourne **true** uniquement lorsque la table de hello n’existe pas et est créée.</span><span class="sxs-lookup"><span data-stu-id="536ae-151">As mentioned previously, hello **CloudTable.CreateIfNotExists** method returns **true** only when hello table doesn't exist and is created.</span></span> <span data-ttu-id="536ae-152">Par conséquent, si vous exécutez une application hello lors de la table de hello existe, méthode hello retourne **false**.</span><span class="sxs-lookup"><span data-stu-id="536ae-152">Therefore, if you run hello app when hello table exists, hello method returns **false**.</span></span> <span data-ttu-id="536ae-153">toorun hello application plusieurs fois, que vous devez supprimer la table de hello avant de réexécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-153">toorun hello app multiple times, you must delete hello table before running hello app again.</span></span> <span data-ttu-id="536ae-154">Suppression de table hello peut être effectuée via hello **CloudTable.Delete** (méthode).</span><span class="sxs-lookup"><span data-stu-id="536ae-154">Deleting hello table can be done via hello **CloudTable.Delete** method.</span></span> <span data-ttu-id="536ae-155">Vous pouvez également supprimer la table de hello à l’aide de hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="536ae-155">You can also delete hello table using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="536ae-156">Ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="536ae-156">Add an entity tooa table</span></span>

<span data-ttu-id="536ae-157">*Entités* mapper tooC\# objets à l’aide d’une classe personnalisée dérivée de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="536ae-157">*Entities* map tooC\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="536ae-158">tooadd une table de tooa entité, créez une classe qui définit des propriétés de votre entité hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-158">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="536ae-159">Dans cette section, vous verrez comment toodefine une classe d’entité qui utilise hello prénom du client en tant que clé de ligne hello et le nom comme clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-159">In this section, you'll see how toodefine an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="536ae-160">Ensemble, les partitions d’une entité et la clé de ligne identifient hello entité dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-160">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="536ae-161">Les requêtes d’entités dont les clés de partition sont identiques sont plus rapides que les entités dont les clés de partition sont différentes, mais le fait d’utiliser différentes clés de partition améliore l’extensibilité des opérations parallèles.</span><span class="sxs-lookup"><span data-stu-id="536ae-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="536ae-162">Pour toute propriété qui doit être stockée dans le service de table hello, propriété de hello doit être une propriété publique d’un type pris en charge qui expose la définition et de récupération des valeurs.</span><span class="sxs-lookup"><span data-stu-id="536ae-162">For any property that should be stored in hello table service, hello property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="536ae-163">classe d’entité de Hello *doit* déclarer un constructeur sans paramètre public.</span><span class="sxs-lookup"><span data-stu-id="536ae-163">hello entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="536ae-164">Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="536ae-164">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="536ae-165">Ouvrez hello `TablesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="536ae-165">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="536ae-166">Ajouter hello après la directive afin que hello code Bonjour `TablesController.cs` fichier accessible hello **CustomerEntity** classe :</span><span class="sxs-lookup"><span data-stu-id="536ae-166">Add hello following directive so that hello code in hello `TablesController.cs` file can access hello **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="536ae-167">Ajoutez une méthode appelée **AddEntity** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="536ae-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="536ae-168">Au sein de hello **AddEntity** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="536ae-168">Within hello **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="536ae-169">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="536ae-169">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="536ae-170">Obtenez un objet **CloudTableClient** représentant un client du service de Table.</span><span class="sxs-lookup"><span data-stu-id="536ae-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="536ae-171">Obtenir un **CloudTable** objet qui représente un toowhich de table toohello référence que vous vous apprêtez entité tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-171">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="536ae-172">Instancier et d’initialiser hello **CustomerEntity** classe.</span><span class="sxs-lookup"><span data-stu-id="536ae-172">Instantiate and initialize hello **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="536ae-173">Créer un **TableOperation** objet qui insère l’entité customer de hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-173">Create a **TableOperation** object that inserts hello customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="536ae-174">Exécuter l’opération d’insertion hello en appelant hello **CloudTable.Execute** (méthode).</span><span class="sxs-lookup"><span data-stu-id="536ae-174">Execute hello insert operation by calling hello **CloudTable.Execute** method.</span></span> <span data-ttu-id="536ae-175">Vous pouvez vérifier le résultat de hello d’opération de hello en inspectant hello **TableResult.HttpStatusCode** propriété.</span><span class="sxs-lookup"><span data-stu-id="536ae-175">You can verify hello result of hello operation by inspecting hello **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="536ae-176">Un code d’état de 2xx indique l’action hello demandée par hello client a été correctement traitée.</span><span class="sxs-lookup"><span data-stu-id="536ae-176">A status code of 2xx indicates hello action requested by hello client was processed successfully.</span></span> <span data-ttu-id="536ae-177">Par exemple, les insertions de nouvelles entités réussies entraîne un code d’état HTTP de 204, ce qui signifie que hello opération a été correctement traitée et le serveur de hello n’a pas retourné un contenu.</span><span class="sxs-lookup"><span data-stu-id="536ae-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that hello operation was successfully processed and hello server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="536ae-178">Hello de mise à jour **ViewBag** avec le nom de la table hello et hello les résultats de l’opération d’insertion hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-178">Update hello **ViewBag** with hello table name, and hello results of hello insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="536ae-179">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="536ae-179">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="536ae-180">Sur hello **ajouter une vue** boîte de dialogue, entrez **AddEntity** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="536ae-180">On hello **Add View** dialog, enter **AddEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="536ae-181">Ouvrez `AddEntity.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="536ae-181">Open `AddEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="536ae-182">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="536ae-182">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="536ae-183">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="536ae-183">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="536ae-184">Exécutez l’application hello et sélectionnez **ajouter une entité** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="536ae-184">Run hello application, and select **Add entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Ajouter une entité](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="536ae-186">Vous pouvez vérifier que l’entité de hello a été ajoutée en suivant les étapes de hello dans la section de hello, [obtenir une entité unique](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="536ae-186">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="536ae-187">Vous pouvez également utiliser hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tous hello entités pour vos tables.</span><span class="sxs-lookup"><span data-stu-id="536ae-187">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-tooa-table"></a><span data-ttu-id="536ae-188">Ajouter un lot de la table de tooa d’entités</span><span class="sxs-lookup"><span data-stu-id="536ae-188">Add a batch of entities tooa table</span></span>

<span data-ttu-id="536ae-189">Dans toobeing plus en mesure de trop[ajouter une table de tooa entité une à la fois](#add-an-entity-to-a-table), vous pouvez également ajouter des entités dans le lot.</span><span class="sxs-lookup"><span data-stu-id="536ae-189">In addition toobeing able too[add an entity tooa table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="536ae-190">Ajout d’entités dans un lot de réduit le nombre de hello d’allers-retours entre votre code et le service table Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-190">Adding entities in batch reduces hello number of round-trips between your code and hello Azure table service.</span></span> <span data-ttu-id="536ae-191">Hello suit illustre comment tooadd plusieurs entités tooa table avec une opération d’insertion unique :</span><span class="sxs-lookup"><span data-stu-id="536ae-191">hello following steps illustrate how tooadd multiple entities tooa table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="536ae-192">Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="536ae-192">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="536ae-193">Ouvrez hello `TablesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="536ae-193">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="536ae-194">Ajoutez une méthode appelée **AddEntities** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="536ae-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="536ae-195">Au sein de hello **AddEntities** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="536ae-195">Within hello **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="536ae-196">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="536ae-196">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="536ae-197">Obtenez un objet **CloudTableClient** représentant un client du service de Table.</span><span class="sxs-lookup"><span data-stu-id="536ae-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="536ae-198">Obtenir un **CloudTable** objet qui représente un toowhich de table toohello référence sont de nouvelles entités continu tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-198">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="536ae-199">Instancier des objets de client en fonction de hello **CustomerEntity** présentée dans la section de hello, de classe de modèle [ajouter une table de tooa entité](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="536ae-199">Instantiate some customer objects based on hello **CustomerEntity** model class presented in hello section, [Add an entity tooa table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="536ae-200">Obtenez un objet **TableBatchOperation**.</span><span class="sxs-lookup"><span data-stu-id="536ae-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="536ae-201">Ajouter un objet d’opération insert entités toohello lot.</span><span class="sxs-lookup"><span data-stu-id="536ae-201">Add entities toohello batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="536ae-202">Exécuter l’opération d’insertion de lot de hello en appelant hello **CloudTable.ExecuteBatch** (méthode).</span><span class="sxs-lookup"><span data-stu-id="536ae-202">Execute hello batch insert operation by calling hello **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="536ae-203">Hello **CloudTable.ExecuteBatch** méthode retourne une liste de **TableResult** objets où chaque **TableResult** objet peut être examiné toodetermine hello réussite ou l’échec de chaque opération.</span><span class="sxs-lookup"><span data-stu-id="536ae-203">hello **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined toodetermine hello success or failure of each individual operation.</span></span> <span data-ttu-id="536ae-204">Pour cet exemple, passer du mode de tooa liste hello et permettent d’afficher les résultats de chaque opération de hello vue de hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-204">For this example, pass hello list tooa view and let hello view display hello results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="536ae-205">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="536ae-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="536ae-206">Sur hello **ajouter une vue** boîte de dialogue, entrez **AddEntities** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="536ae-206">On hello **Add View** dialog, enter **AddEntities** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="536ae-207">Ouvrez `AddEntities.cshtml`et modifiez-le pour qu’il ressemble hello suivant.</span><span class="sxs-lookup"><span data-stu-id="536ae-207">Open `AddEntities.cshtml`, and modify it so that it looks like hello following.</span></span>

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="536ae-208">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="536ae-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="536ae-209">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="536ae-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="536ae-210">Exécutez l’application hello et sélectionnez **ajouter des entités** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="536ae-210">Run hello application, and select **Add entities** toosee results similar toohello following screen shot:</span></span>
  
    ![Ajouter des entités](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="536ae-212">Vous pouvez vérifier que l’entité de hello a été ajoutée en suivant les étapes de hello dans la section de hello, [obtenir une entité unique](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="536ae-212">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="536ae-213">Vous pouvez également utiliser hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tous hello entités pour vos tables.</span><span class="sxs-lookup"><span data-stu-id="536ae-213">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="536ae-214">Obtention d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="536ae-214">Get a single entity</span></span>

<span data-ttu-id="536ae-215">Cette section illustre comment une seule entité à partir d’une table à l’aide de tooget hello clé de ligne et la clé de partition de l’entité.</span><span class="sxs-lookup"><span data-stu-id="536ae-215">This section illustrates how tooget a single entity from a table using hello entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="536ae-216">Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment)et utilise des données de [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="536ae-216">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="536ae-217">Ouvrez hello `TablesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="536ae-217">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="536ae-218">Ajoutez une méthode appelée **GetSingle** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="536ae-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="536ae-219">Au sein de hello **GetSingle** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="536ae-219">Within hello **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="536ae-220">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="536ae-220">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="536ae-221">Obtenez un objet **CloudTableClient** représentant un client du service de Table.</span><span class="sxs-lookup"><span data-stu-id="536ae-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="536ae-222">Obtenir un **CloudTable** objet qui représente une table de toohello référence à partir duquel vous récupérez des entités de hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-222">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="536ae-223">Créez un objet d’opération de récupération qui prend un objet d’entité dérivé de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="536ae-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="536ae-224">premier paramètre de Hello est hello *partitionKey*, et hello deuxième paramètre est hello *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="536ae-224">hello first parameter is hello *partitionKey*, and hello second parameter is hello *rowKey*.</span></span> <span data-ttu-id="536ae-225">À l’aide de hello **CustomerEntity** classe et les données présentées dans la section de hello [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table), hello code extrait les requêtes hello tableau suivant pour un **CustomerEntity** entité avec une *partitionKey* valeur de « Smith » et un *rowKey* valeur de « Ben » :</span><span class="sxs-lookup"><span data-stu-id="536ae-225">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="536ae-226">Exécuter l’opération de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-226">Execute hello retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="536ae-227">Passer l’affichage du résultat de hello toohello pour l’affichage.</span><span class="sxs-lookup"><span data-stu-id="536ae-227">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="536ae-228">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="536ae-228">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="536ae-229">Sur hello **ajouter une vue** boîte de dialogue, entrez **GetSingle** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="536ae-229">On hello **Add View** dialog, enter **GetSingle** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="536ae-230">Ouvrez `GetSingle.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="536ae-230">Open `GetSingle.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. <span data-ttu-id="536ae-231">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="536ae-231">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="536ae-232">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="536ae-232">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="536ae-233">Exécutez l’application hello et sélectionnez **obtenir unique** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="536ae-233">Run hello application, and select **Get Single** toosee results similar toohello following screen shot:</span></span>
  
    ![Obtenir une entité unique](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="536ae-235">Obtenir toutes les entités d’une partition</span><span class="sxs-lookup"><span data-stu-id="536ae-235">Get all entities in a partition</span></span>

<span data-ttu-id="536ae-236">Comme indiqué dans la section de hello, [ajouter une table de tooa entité](#add-an-entity-to-a-table), combinaison de hello d’une partition et une clé de ligne identifient de manière unique une entité dans une table.</span><span class="sxs-lookup"><span data-stu-id="536ae-236">As mentioned in hello section, [Add an entity tooa table](#add-an-entity-to-a-table), hello combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="536ae-237">Les requêtes d'entités dont les clés de partition sont identiques sont plus rapides que celles d'entités dont les clés de partition sont différentes.</span><span class="sxs-lookup"><span data-stu-id="536ae-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="536ae-238">Cette section illustre comment tooquery une table pour toutes les entités hello à partir d’une partition spécifiée.</span><span class="sxs-lookup"><span data-stu-id="536ae-238">This section illustrates how tooquery a table for all hello entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="536ae-239">Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment)et utilise des données de [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="536ae-239">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="536ae-240">Ouvrez hello `TablesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="536ae-240">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="536ae-241">Ajoutez une méthode appelée **GetPartition** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="536ae-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="536ae-242">Au sein de hello **GetPartition** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="536ae-242">Within hello **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="536ae-243">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="536ae-243">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="536ae-244">Obtenez un objet **CloudTableClient** représentant un client du service de Table.</span><span class="sxs-lookup"><span data-stu-id="536ae-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="536ae-245">Obtenir un **CloudTable** objet qui représente une table de toohello référence à partir duquel vous récupérez des entités de hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-245">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="536ae-246">Instancier une **TableQuery** objet spécifiant la requête de hello Bonjour **où** clause.</span><span class="sxs-lookup"><span data-stu-id="536ae-246">Instantiate a **TableQuery** object specifying hello query in hello **Where** clause.</span></span> <span data-ttu-id="536ae-247">À l’aide de hello **CustomerEntity** classe et les données présentées dans la section de hello [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table), table de hello extrait les requêtes pour toutes les entités de code du hello suivant où hello  **PartitionKey** (nom de famille du client) a la valeur « Smith » :</span><span class="sxs-lookup"><span data-stu-id="536ae-247">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a all entities where hello **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="536ae-248">Dans une boucle, appelez hello **CloudTable.ExecuteQuerySegmented** méthode passant l’objet de requête hello vous instancié à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-248">Within a loop, call hello **CloudTable.ExecuteQuerySegmented** method passing hello query object you instantiated in hello previous step.</span></span>  <span data-ttu-id="536ae-249">Hello **CloudTable.ExecuteQuerySegmented** méthode retourne un **TableContinuationToken** objet - lorsque **null** -indique qu’il n’y a aucune entité plus tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="536ae-249">hello **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities tooretrieve.</span></span> <span data-ttu-id="536ae-250">Dans la boucle de hello, utilisez une autre boucle tooiterate sur hello entités retournée.</span><span class="sxs-lookup"><span data-stu-id="536ae-250">Within hello loop, use another loop tooiterate over hello returned entities.</span></span> <span data-ttu-id="536ae-251">Bonjour exemple de code suivant, chaque entité retournée est ajoutée tooa liste.</span><span class="sxs-lookup"><span data-stu-id="536ae-251">In hello following code example, each returned entity is added tooa list.</span></span> <span data-ttu-id="536ae-252">Une fois hello fin de la boucle, hello est passée vue tooa pour l’affichage :</span><span class="sxs-lookup"><span data-stu-id="536ae-252">Once hello loop ends, hello list is passed tooa view for display:</span></span> 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. <span data-ttu-id="536ae-253">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="536ae-253">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="536ae-254">Sur hello **ajouter une vue** boîte de dialogue, entrez **GetPartition** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="536ae-254">On hello **Add View** dialog, enter **GetPartition** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="536ae-255">Ouvrez `GetPartition.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="536ae-255">Open `GetPartition.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="536ae-256">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="536ae-256">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="536ae-257">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="536ae-257">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="536ae-258">Exécutez l’application hello et sélectionnez **obtenir une Partition** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="536ae-258">Run hello application, and select **Get Partition** toosee results similar toohello following screen shot:</span></span>
  
    ![Obtenir une partition](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="536ae-260">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="536ae-260">Delete an entity</span></span>

<span data-ttu-id="536ae-261">Cette section illustre comment toodelete d’entité à partir d’une table.</span><span class="sxs-lookup"><span data-stu-id="536ae-261">This section illustrates how toodelete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="536ae-262">Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment)et utilise des données de [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="536ae-262">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="536ae-263">Ouvrez hello `TablesController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="536ae-263">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="536ae-264">Ajoutez une méthode appelée **DeleteEntity** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="536ae-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="536ae-265">Au sein de hello **DeleteEntity** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="536ae-265">Within hello **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="536ae-266">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="536ae-266">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="536ae-267">Obtenez un objet **CloudTableClient** représentant un client du service de Table.</span><span class="sxs-lookup"><span data-stu-id="536ae-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="536ae-268">Obtenir un **CloudTable** objet qui représente une table de toohello référence à partir de laquelle vous supprimez une entité de hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-268">Get a **CloudTable** object that represents a reference toohello table from which you are deleting hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="536ae-269">Créez un objet d’opération de suppression qui prend un objet d’entité dérivé de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="536ae-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="536ae-270">Dans ce cas, nous utilisons hello **CustomerEntity** classe et les données présentées dans la section de hello [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="536ae-270">In this case, we use hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="536ae-271">l’entité de Hello **ETag** doit avoir la valeur valide de tooa.</span><span class="sxs-lookup"><span data-stu-id="536ae-271">hello entity's **ETag** must be set tooa valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="536ae-272">Exécuter l’opération de suppression hello.</span><span class="sxs-lookup"><span data-stu-id="536ae-272">Execute hello delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="536ae-273">Passer l’affichage du résultat de hello toohello pour l’affichage.</span><span class="sxs-lookup"><span data-stu-id="536ae-273">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="536ae-274">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="536ae-274">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="536ae-275">Sur hello **ajouter une vue** boîte de dialogue, entrez **DeleteEntity** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="536ae-275">On hello **Add View** dialog, enter **DeleteEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="536ae-276">Ouvrez `DeleteEntity.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="536ae-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. <span data-ttu-id="536ae-277">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="536ae-277">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="536ae-278">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="536ae-278">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="536ae-279">Exécutez l’application hello et sélectionnez **supprimer l’entité** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="536ae-279">Run hello application, and select **Delete entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Obtenir une entité unique](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="536ae-281">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="536ae-281">Next steps</span></span>
<span data-ttu-id="536ae-282">Permet d’afficher plusieurs toolearn de repères de fonctionnalité sur les options supplémentaires pour le stockage des données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="536ae-282">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="536ae-283">Prise en main du stockage d’objets blob Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="536ae-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="536ae-284">Prise en main du stockage de files d’attente Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="536ae-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-queues.md)
