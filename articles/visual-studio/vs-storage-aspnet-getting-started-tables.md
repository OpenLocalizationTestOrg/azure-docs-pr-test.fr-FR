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
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a>Prise en main du Stockage Table Azure et des services connectés de Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Vue d'ensemble

Stockage de Table Azure vous permet de toostore de grandes quantités de données structurées. service de Hello est une banque de données NoSQL qui accepte des appels authentifiés provenant à l’intérieur et extérieur hello cloud Azure. Les tables Azure sont idéales pour le stockage des données structurées non relationnelles.

Ce didacticiel montre comment toowrite ASP.NET de code pour les scénarios courants à l’aide des entités de stockage de table Windows Azure. Ces scénarios incluent la création d’une table ainsi que l'ajout, l'interrogation et la suppression d’entités de table. 

##<a name="prerequisites"></a>Composants requis

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Créer un contrôleur MVC 

1. Bonjour **l’Explorateur de solutions**, avec le bouton droit **contrôleurs**et, dans le menu contextuel de hello, sélectionnez **Ajouter -> contrôleur**.

    ![Ajouter une application ASP.NET MVC de tooan contrôleur](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. Sur hello **ajouter une vue de structure** boîte de dialogue, sélectionnez **contrôleur MVC 5 - vide**, puis sélectionnez **ajouter**.

    ![Spécifier le type de contrôleur MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. Sur hello **ajouter un contrôleur** boîte de dialogue, nom hello du contrôleur *TablesController*, puis sélectionnez **ajouter**.

    ![Contrôleur MVC de hello nom](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. Ajoutez hello suivant *à l’aide de* directives toohello `TablesController.cs` fichier :

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a>Créer une classe de modèle

La plupart des exemples hello dans cet article utilisent un **TableEntity**-classe appelée dérivée **CustomerEntity**. Hello suit vous guide tout au long de déclarer cette classe comme une classe de modèle :

1. Bonjour **l’Explorateur de solutions**, avec le bouton droit **modèles**et, dans le menu contextuel de hello, sélectionnez **Ajouter -> classe**.

1. Sur hello **ajouter un nouvel élément** boîte de dialogue, le nom de la classe hello, **CustomerEntity**.

1. Ouvrez hello `CustomerEntity.cs` de fichiers et ajoutez hello suivant **à l’aide de** directive :

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. Modifiez la classe hello, afin que, lorsque vous avez terminé, la classe hello est déclaré comme hello suivant de code. classe Hello déclare une classe d’entité appelée **CustomerEntity** qu’utilise hello prénom du client en tant que clé de ligne hello et le nom comme clé de partition hello.

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

## <a name="create-a-table"></a>Création d’une table

Hello étapes suivantes illustrent comment toocreate une table :

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment). 

1. Ouvrez hello `TablesController.cs` fichier.

1. Ajoutez une méthode appelée **CreateTable** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Au sein de hello **CreateTable** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenez un objet **CloudTableClient** représentant un client du service de Table.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtenir un **CloudTable** objet qui représente un nom de référence toohello table souhaité. Hello **CloudTableClient.GetTableReference** méthode ne rend pas une demande pour le stockage de table. référence de Hello est renvoyée hello table existe ou non. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Appelez hello **CloudTable.CreateIfNotExists** table de hello toocreate méthodes s’il n’existe pas encore. Hello **CloudTable.CreateIfNotExists** méthode retourne **true** si la table de hello n’existe pas et a été correctement créé. Sinon, la valeur **false** est retournée.    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. Hello de mise à jour **ViewBag** avec nom hello de table de hello.

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **CreateTable** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `CreateTable.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. Exécutez l’application hello et sélectionnez **créer une table** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Créer une table](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    Comme mentionné précédemment, hello **CloudTable.CreateIfNotExists** méthode retourne **true** uniquement lorsque la table de hello n’existe pas et est créée. Par conséquent, si vous exécutez une application hello lors de la table de hello existe, méthode hello retourne **false**. toorun hello application plusieurs fois, que vous devez supprimer la table de hello avant de réexécuter l’application hello. Suppression de table hello peut être effectuée via hello **CloudTable.Delete** (méthode). Vous pouvez également supprimer la table de hello à l’aide de hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-an-entity-tooa-table"></a>Ajouter une table de tooa d’entité

*Entités* mapper tooC\# objets à l’aide d’une classe personnalisée dérivée de **TableEntity**. tooadd une table de tooa entité, créez une classe qui définit des propriétés de votre entité hello. Dans cette section, vous verrez comment toodefine une classe d’entité qui utilise hello prénom du client en tant que clé de ligne hello et le nom comme clé de partition hello. Ensemble, les partitions d’une entité et la clé de ligne identifient hello entité dans la table de hello. Les requêtes d’entités dont les clés de partition sont identiques sont plus rapides que les entités dont les clés de partition sont différentes, mais le fait d’utiliser différentes clés de partition améliore l’extensibilité des opérations parallèles. Pour toute propriété qui doit être stockée dans le service de table hello, propriété de hello doit être une propriété publique d’un type pris en charge qui expose la définition et de récupération des valeurs.
classe d’entité de Hello *doit* déclarer un constructeur sans paramètre public.

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment).

1. Ouvrez hello `TablesController.cs` fichier.

1. Ajouter hello après la directive afin que hello code Bonjour `TablesController.cs` fichier accessible hello **CustomerEntity** classe :

    ```csharp
    using StorageAspnet.Models;
    ```

1. Ajoutez une méthode appelée **AddEntity** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Au sein de hello **AddEntity** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenez un objet **CloudTableClient** représentant un client du service de Table.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtenir un **CloudTable** objet qui représente un toowhich de table toohello référence que vous vous apprêtez entité tooadd hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Instancier et d’initialiser hello **CustomerEntity** classe.

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. Créer un **TableOperation** objet qui insère l’entité customer de hello.

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. Exécuter l’opération d’insertion hello en appelant hello **CloudTable.Execute** (méthode). Vous pouvez vérifier le résultat de hello d’opération de hello en inspectant hello **TableResult.HttpStatusCode** propriété. Un code d’état de 2xx indique l’action hello demandée par hello client a été correctement traitée. Par exemple, les insertions de nouvelles entités réussies entraîne un code d’état HTTP de 204, ce qui signifie que hello opération a été correctement traitée et le serveur de hello n’a pas retourné un contenu.

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. Hello de mise à jour **ViewBag** avec le nom de la table hello et hello les résultats de l’opération d’insertion hello.

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **AddEntity** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `AddEntity.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. Exécutez l’application hello et sélectionnez **ajouter une entité** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Ajouter une entité](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    Vous pouvez vérifier que l’entité de hello a été ajoutée en suivant les étapes de hello dans la section de hello, [obtenir une entité unique](#get-a-single-entity). Vous pouvez également utiliser hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tous hello entités pour vos tables.

## <a name="add-a-batch-of-entities-tooa-table"></a>Ajouter un lot de la table de tooa d’entités

Dans toobeing plus en mesure de trop[ajouter une table de tooa entité une à la fois](#add-an-entity-to-a-table), vous pouvez également ajouter des entités dans le lot. Ajout d’entités dans un lot de réduit le nombre de hello d’allers-retours entre votre code et le service table Azure de hello. Hello suit illustre comment tooadd plusieurs entités tooa table avec une opération d’insertion unique :

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment).

1. Ouvrez hello `TablesController.cs` fichier.

1. Ajoutez une méthode appelée **AddEntities** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Au sein de hello **AddEntities** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenez un objet **CloudTableClient** représentant un client du service de Table.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtenir un **CloudTable** objet qui représente un toowhich de table toohello référence sont de nouvelles entités continu tooadd hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Instancier des objets de client en fonction de hello **CustomerEntity** présentée dans la section de hello, de classe de modèle [ajouter une table de tooa entité](#add-an-entity-to-a-table).

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. Obtenez un objet **TableBatchOperation**.

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. Ajouter un objet d’opération insert entités toohello lot.

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. Exécuter l’opération d’insertion de lot de hello en appelant hello **CloudTable.ExecuteBatch** (méthode).   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. Hello **CloudTable.ExecuteBatch** méthode retourne une liste de **TableResult** objets où chaque **TableResult** objet peut être examiné toodetermine hello réussite ou l’échec de chaque opération. Pour cet exemple, passer du mode de tooa liste hello et permettent d’afficher les résultats de chaque opération de hello vue de hello. 
 
    ```csharp
    return View(results);
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **AddEntities** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `AddEntities.cshtml`et modifiez-le pour qu’il ressemble hello suivant.

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

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. Exécutez l’application hello et sélectionnez **ajouter des entités** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Ajouter des entités](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    Vous pouvez vérifier que l’entité de hello a été ajoutée en suivant les étapes de hello dans la section de hello, [obtenir une entité unique](#get-a-single-entity). Vous pouvez également utiliser hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tous hello entités pour vos tables.

## <a name="get-a-single-entity"></a>Obtention d'une seule entité

Cette section illustre comment une seule entité à partir d’une table à l’aide de tooget hello clé de ligne et la clé de partition de l’entité. 

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment)et utilise des données de [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table). 

1. Ouvrez hello `TablesController.cs` fichier.

1. Ajoutez une méthode appelée **GetSingle** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Au sein de hello **GetSingle** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenez un objet **CloudTableClient** représentant un client du service de Table.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtenir un **CloudTable** objet qui représente une table de toohello référence à partir duquel vous récupérez des entités de hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Créez un objet d’opération de récupération qui prend un objet d’entité dérivé de **TableEntity**. premier paramètre de Hello est hello *partitionKey*, et hello deuxième paramètre est hello *rowKey*. À l’aide de hello **CustomerEntity** classe et les données présentées dans la section de hello [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table), hello code extrait les requêtes hello tableau suivant pour un **CustomerEntity** entité avec une *partitionKey* valeur de « Smith » et un *rowKey* valeur de « Ben » :

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. Exécuter l’opération de récupération hello.   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. Passer l’affichage du résultat de hello toohello pour l’affichage.

    ```csharp
    return View(result);
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **GetSingle** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `GetSingle.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

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

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. Exécutez l’application hello et sélectionnez **obtenir unique** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Obtenir une entité unique](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a>Obtenir toutes les entités d’une partition

Comme indiqué dans la section de hello, [ajouter une table de tooa entité](#add-an-entity-to-a-table), combinaison de hello d’une partition et une clé de ligne identifient de manière unique une entité dans une table. Les requêtes d'entités dont les clés de partition sont identiques sont plus rapides que celles d'entités dont les clés de partition sont différentes. Cette section illustre comment tooquery une table pour toutes les entités hello à partir d’une partition spécifiée.  

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment)et utilise des données de [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table). 

1. Ouvrez hello `TablesController.cs` fichier.

1. Ajoutez une méthode appelée **GetPartition** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Au sein de hello **GetPartition** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenez un objet **CloudTableClient** représentant un client du service de Table.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtenir un **CloudTable** objet qui représente une table de toohello référence à partir duquel vous récupérez des entités de hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Instancier une **TableQuery** objet spécifiant la requête de hello Bonjour **où** clause. À l’aide de hello **CustomerEntity** classe et les données présentées dans la section de hello [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table), table de hello extrait les requêtes pour toutes les entités de code du hello suivant où hello  **PartitionKey** (nom de famille du client) a la valeur « Smith » :

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. Dans une boucle, appelez hello **CloudTable.ExecuteQuerySegmented** méthode passant l’objet de requête hello vous instancié à l’étape précédente de hello.  Hello **CloudTable.ExecuteQuerySegmented** méthode retourne un **TableContinuationToken** objet - lorsque **null** -indique qu’il n’y a aucune entité plus tooretrieve. Dans la boucle de hello, utilisez une autre boucle tooiterate sur hello entités retournée. Bonjour exemple de code suivant, chaque entité retournée est ajoutée tooa liste. Une fois hello fin de la boucle, hello est passée vue tooa pour l’affichage : 

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

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **GetPartition** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `GetPartition.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

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

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. Exécutez l’application hello et sélectionnez **obtenir une Partition** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Obtenir une partition](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a>Suppression d’une entité

Cette section illustre comment toodelete d’entité à partir d’une table.

> [!NOTE]
> 
> Cette section suppose que vous avez effectué les étapes hello dans [configuration d’environnement de développement hello](#set-up-the-development-environment)et utilise des données de [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table). 

1. Ouvrez hello `TablesController.cs` fichier.

1. Ajoutez une méthode appelée **DeleteEntity** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Au sein de hello **DeleteEntity** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenez un objet **CloudTableClient** représentant un client du service de Table.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtenir un **CloudTable** objet qui représente une table de toohello référence à partir de laquelle vous supprimez une entité de hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Créez un objet d’opération de suppression qui prend un objet d’entité dérivé de **TableEntity**. Dans ce cas, nous utilisons hello **CustomerEntity** classe et les données présentées dans la section de hello [ajouter un lot de la table de tooa d’entités](#add-a-batch-of-entities-to-a-table). l’entité de Hello **ETag** doit avoir la valeur valide de tooa.  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. Exécuter l’opération de suppression hello.   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. Passer l’affichage du résultat de hello toohello pour l’affichage.

    ```csharp
    return View(result);
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **Tables**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **DeleteEntity** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `DeleteEntity.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

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

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. Exécutez l’application hello et sélectionnez **supprimer l’entité** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Obtenir une entité unique](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a>Étapes suivantes
Permet d’afficher plusieurs toolearn de repères de fonctionnalité sur les options supplémentaires pour le stockage des données dans Azure.

  * [Prise en main du stockage d’objets blob Azure et des services connectés de Visual Studio (ASP.NET)](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [Prise en main du stockage de files d’attente Azure et des services connectés de Visual Studio (ASP.NET)](../storage/vs-storage-aspnet-getting-started-queues.md)
