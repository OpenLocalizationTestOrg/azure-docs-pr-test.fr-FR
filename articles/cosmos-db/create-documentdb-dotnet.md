---
title: "Azure Cosmos DB : Génération d’une application web avec .NET et hello API DocumentDB | Documents Microsoft"
description: "Présente un exemple de code .NET que vous pouvez utiliser la requête de tooand tooconnect hello Azure Cosmos DB DocumentDB API"
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
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="d7b3c-103">Azure Cosmos DB : Génération d’une application de web API DocumentDB avec .NET et hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d7b3c-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="d7b3c-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="d7b3c-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="d7b3c-106">Ce démarrage rapide montre comment toocreate un compte de base de données Azure Cosmos, base de données du document et à l’aide de la collection hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="d7b3c-107">Vous allez ensuite générer et déployer une application web de liste todo repose sur hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in hello following screenshot.</span></span> 

![Application To-Do avec des exemples de données](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="d7b3c-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d7b3c-109">Prerequisites</span></span>

<span data-ttu-id="d7b3c-110">Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello **libre** [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d7b3c-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="d7b3c-111">Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="d7b3c-112">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="d7b3c-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="d7b3c-113">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="d7b3c-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="d7b3c-114">Ajouter un exemple de données</span><span class="sxs-lookup"><span data-stu-id="d7b3c-114">Add sample data</span></span>

<span data-ttu-id="d7b3c-115">Vous pouvez maintenant ajouter la nouvelle collection données tooyour à l’aide de l’Explorateur de données.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-115">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="d7b3c-116">Dans l’Explorateur de données, la nouvelle base de données hello s’affiche dans le volet de Collections hello.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-116">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="d7b3c-117">Développez hello **tâches** de base de données, développez hello **éléments** collection, cliquez sur **Documents**, puis cliquez sur **nouveaux Documents**.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-117">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Créer des documents dans l’Explorateur de données Bonjour portail Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="d7b3c-119">Maintenant ajouter une collection de toohello document avec hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-119">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="d7b3c-120">Une fois que vous avez ajouté hello json toohello **Documents** , cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-120">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Copier des données json et cliquez sur Enregistrer dans l’Explorateur de données Bonjour portail Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="d7b3c-122">Créer et enregistrer un document plus où vous insérez une valeur unique pour hello `id` propriété et la modification hello autres propriétés comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-122">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="d7b3c-123">Vos nouveaux documents peuvent avoir la structure de votre choix car Azure Cosmos DB n’impose aucun schéma pour vos données.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="d7b3c-124">Vous pouvez maintenant utiliser des requêtes dans l’Explorateur de données tooretrieve vos données.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-124">You can now use queries in Data Explorer tooretrieve your data.</span></span> <span data-ttu-id="d7b3c-125">Par défaut, l’Explorateur de données utilise `SELECT * FROM c` tooretrieve tous les documents dans la collection de hello, mais vous pouvez modifier ce tooa différents [requête SQL](documentdb-sql-query.md), tel que `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn tous les documents hello dans l’ordre décroissant en fonction de leur horodatage.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-125">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="d7b3c-126">Vous pouvez également utiliser les procédures de toocreate stockée Explorateur de données, UDF et déclencheurs tooperform ainsi la logique métier côté serveur en tant que le débit de l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-126">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="d7b3c-127">Explorateur de données expose l’ensemble du hello intégrées par programmation l’accès aux données disponibles dans l’API de hello, mais il fournit des données un accès facile tooyour hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-127">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="d7b3c-128">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="d7b3c-128">Clone hello sample application</span></span>

<span data-ttu-id="d7b3c-129">Maintenant nous allons passer tooworking avec le code.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-129">Now let's switch tooworking with code.</span></span> <span data-ttu-id="d7b3c-130">Nous allons cloner une application API DocumentDB à partir de GitHub, définissez la chaîne de connexion hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-130">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="d7b3c-131">Vous allez voir combien il est facile toowork avec des données par programme.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-131">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="d7b3c-132">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `CD` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-132">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="d7b3c-133">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-133">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="d7b3c-134">Puis ouvrez le fichier de solution todo hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-134">Then open hello todo solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="d7b3c-135">Réviser le code hello</span><span class="sxs-lookup"><span data-stu-id="d7b3c-135">Review hello code</span></span>

<span data-ttu-id="d7b3c-136">Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-136">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="d7b3c-137">Fichier de DocumentDBRepository.cs hello ouvert et que vous trouverez ces lignes de code créent hello des ressources de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-137">Open hello DocumentDBRepository.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="d7b3c-138">Hello DocumentClient est initialisée sur la ligne 73.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-138">hello DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="d7b3c-139">Une nouvelle base de données est créée à la ligne 88.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="d7b3c-140">Une nouvelle collection est créée à la ligne 107.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="d7b3c-141">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="d7b3c-141">Update your connection string</span></span>

<span data-ttu-id="d7b3c-142">Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-142">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="d7b3c-143">Bonjour [portail Azure](http://portal.azure.com/), dans votre base de données de Cosmos Azure account, Bonjour barre de navigation gauche, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-143">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="d7b3c-144">Vous allez utiliser les boutons de copier hello sur droite hello Hello de toocopy écran hello URI et la clé primaire dans le fichier web.config de hello dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-144">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello web.config file in hello next step.</span></span>

    ![Afficher et copier une clé d’accès dans hello portail Azure, le panneau de clés](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="d7b3c-146">Dans Visual Studio 2017, ouvrez le fichier web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-146">In Visual Studio 2017, open hello web.config file.</span></span> 

3. <span data-ttu-id="d7b3c-147">Copier la valeur de l’URI à partir du portail hello (à l’aide du bouton de copie hello) et le rendre hello la valeur de clé de point de terminaison hello dans le fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-147">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="d7b3c-148">Copiez la valeur de clé primaire à partir du portail de hello, puis rendre hello valeur authKey hello dans le fichier web.config. Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-148">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello authKey in web.config. You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a><span data-ttu-id="d7b3c-149">Exécutez l’application hello web</span><span class="sxs-lookup"><span data-stu-id="d7b3c-149">Run hello web app</span></span>
1. <span data-ttu-id="d7b3c-150">Dans Visual Studio, cliquez sur projet hello dans **l’Explorateur de solutions** puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-150">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="d7b3c-151">Bonjour NuGet **Parcourir** , tapez *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-151">In hello NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="d7b3c-152">À partir des résultats de hello, installez hello **Microsoft.Azure.DocumentDB** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-152">From hello results, install hello **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="d7b3c-153">Cela installe le package de Microsoft.Azure.DocumentDB hello, ainsi que toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-153">This installs hello Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="d7b3c-154">Cliquez sur CTRL + F5 application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-154">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="d7b3c-155">Votre application s’affiche dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="d7b3c-156">Cliquez sur **créer un nouveau** hello navigateur et créer quelques nouvelles tâches dans votre application de l’action.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-156">Click **Create New** in hello browser and create a few new tasks in your to-do app.</span></span>

   ![Application To-Do avec des exemples de données](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="d7b3c-158">Vous pouvez maintenant revenir en arrière tooData Explorer et consultez la requête, modifier et travailler avec ces nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-158">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="d7b3c-159">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d7b3c-159">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="d7b3c-160">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="d7b3c-160">Clean up resources</span></span>

<span data-ttu-id="d7b3c-161">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7b3c-161">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="d7b3c-162">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-162">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="d7b3c-163">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-163">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7b3c-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7b3c-164">Next steps</span></span>

<span data-ttu-id="d7b3c-165">Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer une collection à l’aide de hello Explorateur de données et exécuter une application web.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-165">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a web app.</span></span> <span data-ttu-id="d7b3c-166">Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="d7b3c-166">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7b3c-167">Importer des données dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d7b3c-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


