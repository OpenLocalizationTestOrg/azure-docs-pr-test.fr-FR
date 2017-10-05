---
title: "Azure Cosmos DB : Développer une application web avec .NET et l’API DocumentDB | Microsoft Docs"
description: "Cet article présente un exemple de code .NET que vous pouvez utiliser pour vous connecter à l’API Azure Cosmos DB DocumentDB, et pour l’interroger."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 9bb863261da64c97f99757d4a0cb3474a7755591
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="2d379-103">Azure Cosmos DB : Développer une application web API DocumentDB avec .NET et le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2d379-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="2d379-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="2d379-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="2d379-105">Rapidement, vous avez la possibilité de créer et d’interroger des documents, des paires clé/valeur, et des bases de données orientées graphe, profitant tous de la distribution à l’échelle mondiale et des capacités de mise à l’échelle horizontale au cœur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2d379-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="2d379-106">Ce guide de démarrage rapide explique comment créer, à l’aide du portail Azure, un compte Azure Cosmos DB, une base de données de documents, ainsi qu’une collection.</span><span class="sxs-lookup"><span data-stu-id="2d379-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="2d379-107">Vous allez ensuite créer et déployer une application web de liste de tâches, basée sur [l’API .NET DocumentDB](documentdb-sdk-dotnet.md), comme illustré par la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="2d379-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in the following screenshot.</span></span> 

![Application To-Do avec des exemples de données](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="2d379-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2d379-109">Prerequisites</span></span>

<span data-ttu-id="2d379-110">Si vous n’avez pas encore installé Visual Studio 2017, vous pouvez télécharger et utiliser la version **gratuite** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2d379-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="2d379-111">Veillez à activer **le développement Azure** lors de l’installation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d379-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="2d379-112">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="2d379-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="2d379-113">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="2d379-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="2d379-114">Ajouter un exemple de données</span><span class="sxs-lookup"><span data-stu-id="2d379-114">Add sample data</span></span>

<span data-ttu-id="2d379-115">Vous pouvez maintenant ajouter des données à votre nouvelle collection grâce à l’Explorateur de données.</span><span class="sxs-lookup"><span data-stu-id="2d379-115">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="2d379-116">Dans l’Explorateur de données, la nouvelle base de données apparaît dans le volet Collections.</span><span class="sxs-lookup"><span data-stu-id="2d379-116">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="2d379-117">Développez la base de données **Tâches**, développez la collection **Éléments**, cliquez sur **Documents**, puis cliquez sur **Nouveaux documents**.</span><span class="sxs-lookup"><span data-stu-id="2d379-117">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Créer des documents dans l’Explorateur de données, dans le Portail Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="2d379-119">À présent, ajoutez un document à la collection avec la structure suivante.</span><span class="sxs-lookup"><span data-stu-id="2d379-119">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="2d379-120">Une fois le fichier json ajouté à l’onglet **Documents**, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2d379-120">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Copiez dans les données json, puis cliquez sur Enregistrer dans l’Explorateur de données du portail Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="2d379-122">Créez et enregistrez un document supplémentaire dans lequel vous insérez une valeur unique pour la propriété `id` et modifiez les autres propriétés selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="2d379-122">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="2d379-123">Vos nouveaux documents peuvent avoir la structure de votre choix car Azure Cosmos DB n’impose aucun schéma pour vos données.</span><span class="sxs-lookup"><span data-stu-id="2d379-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="2d379-124">Vous pouvez désormais utiliser des requêtes dans l’Explorateur de données pour récupérer vos données.</span><span class="sxs-lookup"><span data-stu-id="2d379-124">You can now use queries in Data Explorer to retrieve your data.</span></span> <span data-ttu-id="2d379-125">Par défaut, l’Explorateur de données utilise `SELECT * FROM c` pour récupérer tous les documents dans la collection, mais vous pouvez remplacer cette requête par une autre [requête SQL](documentdb-sql-query.md), telle que `SELECT * FROM c ORDER BY c._ts DESC`, pour obtenir tous les documents dans l’ordre décroissant en fonction de leur horodateur.</span><span class="sxs-lookup"><span data-stu-id="2d379-125">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="2d379-126">Vous pouvez également utiliser l’Explorateur de données pour créer des procédures stockées, des fonctions définies par l'utilisateur et des déclencheurs afin d’exécuter la logique métier côté serveur ainsi que la mise à l’échelle du débit.</span><span class="sxs-lookup"><span data-stu-id="2d379-126">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="2d379-127">L’Explorateur de données affiche tous les accès aux données par programmation intégrés disponibles dans l’API, mais permet d’accéder facilement à vos données dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2d379-127">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="2d379-128">Clonage de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="2d379-128">Clone the sample application</span></span>

<span data-ttu-id="2d379-129">À présent, travaillons sur le code.</span><span class="sxs-lookup"><span data-stu-id="2d379-129">Now let's switch to working with code.</span></span> <span data-ttu-id="2d379-130">Nous allons cloner une application API DocumentDB à partir de GitHub, définir la chaîne de connexion et l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="2d379-130">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="2d379-131">Vous verrez combien il est facile de travailler par programmation avec des données.</span><span class="sxs-lookup"><span data-stu-id="2d379-131">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="2d379-132">Ouvrez une fenêtre de terminal git, comme git bash, et accédez à un répertoire de travail à l’aide de la commande `CD`.</span><span class="sxs-lookup"><span data-stu-id="2d379-132">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="2d379-133">Exécutez la commande suivante pour cloner l’exemple de référentiel.</span><span class="sxs-lookup"><span data-stu-id="2d379-133">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="2d379-134">Ouvrez le fichier de solution todo dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d379-134">Then open the todo solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="2d379-135">Examiner le code</span><span class="sxs-lookup"><span data-stu-id="2d379-135">Review the code</span></span>

<span data-ttu-id="2d379-136">Passons rapidement en revue ce qui se passe dans l’application.</span><span class="sxs-lookup"><span data-stu-id="2d379-136">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="2d379-137">Ouvrez le fichier DocumentDBRepository.cs, et vous découvrirez que ces lignes de code créent les ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2d379-137">Open the DocumentDBRepository.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="2d379-138">Le DocumentClient est initialisé à la ligne 73.</span><span class="sxs-lookup"><span data-stu-id="2d379-138">The DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="2d379-139">Une nouvelle base de données est créée à la ligne 88.</span><span class="sxs-lookup"><span data-stu-id="2d379-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="2d379-140">Une nouvelle collection est créée à la ligne 107.</span><span class="sxs-lookup"><span data-stu-id="2d379-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="2d379-141">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="2d379-141">Update your connection string</span></span>

<span data-ttu-id="2d379-142">Maintenant, retournez dans le portail Azure afin d’obtenir les informations de votre chaîne de connexion et de les copier dans l’application.</span><span class="sxs-lookup"><span data-stu-id="2d379-142">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="2d379-143">Dans le [portail Azure](http://portal.azure.com/), dans votre compte Azure Cosmos DB, dans le volet de navigation de gauche, cliquez sur **Clés**, puis sur **Clés en lecture-écriture**.</span><span class="sxs-lookup"><span data-stu-id="2d379-143">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="2d379-144">Vous utiliserez les boutons Copier sur le côté droit de l’écran pour copier l’URI et la clé primaire dans le fichier web.config à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="2d379-144">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the web.config file in the next step.</span></span>

    ![Affichage et copie d’une clé d’accès rapide dans le portail Azure, panneau Clés](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="2d379-146">Dans Visual Studio 2017, ouvrez le fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="2d379-146">In Visual Studio 2017, open the web.config file.</span></span> 

3. <span data-ttu-id="2d379-147">Copiez votre valeur URI à partir du portail (à l’aide du bouton Copier) et définissez-la comme la valeur de la clé du point de terminaison dans le fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="2d379-147">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="2d379-148">Puis, copiez votre valeur de clé primaire à partir du portail et définissez-la comme la valeur de la authKey dans web.config. Vous venez de mettre à jour votre application avec toutes les informations nécessaires pour communiquer avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2d379-148">Then copy your PRIMARY KEY value from the portal and make it the value of the authKey in web.config. You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-the-web-app"></a><span data-ttu-id="2d379-149">Exécuter l’application web</span><span class="sxs-lookup"><span data-stu-id="2d379-149">Run the web app</span></span>
1. <span data-ttu-id="2d379-150">Dans Visual Studio, cliquez avec le bouton droit sur le nom du projet dans l’**Explorateur de solutions**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2d379-150">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="2d379-151">Dans la zone **Parcourir**de NuGet, tapez *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="2d379-151">In the NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="2d379-152">À partir des résultats, installez la bibliothèque **Microsoft.Azure.DocumentDB**.</span><span class="sxs-lookup"><span data-stu-id="2d379-152">From the results, install the **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="2d379-153">Cette opération permet d’installer le package Microsoft.Azure.DocumentDB ainsi que toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="2d379-153">This installs the Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="2d379-154">Appuyez sur Ctrl + F5 pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="2d379-154">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="2d379-155">Votre application s’affiche dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="2d379-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="2d379-156">Cliquez sur **Créer** dans le navigateur et créer quelques tâches dans votre application To-Do.</span><span class="sxs-lookup"><span data-stu-id="2d379-156">Click **Create New** in the browser and create a few new tasks in your to-do app.</span></span>

   ![Application To-Do avec des exemples de données](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="2d379-158">Vous pouvez dès à présent revenir à l’Explorateur de données et voir la requête, modifier et travailler avec ces nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="2d379-158">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="2d379-159">Examiner les SLA dans le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="2d379-159">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="2d379-160">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="2d379-160">Clean up resources</span></span>

<span data-ttu-id="2d379-161">Si vous ne pensez pas continuer à utiliser cette application, supprimez toutes les ressources créées durant ce guide de démarrage rapide dans le Portail Azure en procédant de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="2d379-161">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="2d379-162">Dans le menu de gauche du portail Azure, cliquez sur **Groupes de ressources**, puis sur le nom de la ressource que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="2d379-162">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="2d379-163">Dans la page de votre groupe de ressources, cliquez sur **Supprimer**, tapez le nom de la ressource à supprimer dans la zone de texte, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="2d379-163">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d379-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d379-164">Next steps</span></span>

<span data-ttu-id="2d379-165">Dans ce guide de démarrage rapide, vous avez appris à créer un compte Azure Cosmos DB, à créer une collection à l’aide de l’Explorateur de données et à exécuter une application web.</span><span class="sxs-lookup"><span data-stu-id="2d379-165">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a web app.</span></span> <span data-ttu-id="2d379-166">Vous pouvez maintenant importer des données supplémentaires à votre compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2d379-166">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d379-167">Importer des données dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2d379-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


