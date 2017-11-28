---
title: "une application Azure Cosmos DB .NET à l’aide d’aaaBuild hello API Graph | Documents Microsoft"
description: "Présente un exemple de code .NET que vous pouvez utiliser tooconnect tooand interroger la base de données Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a><span data-ttu-id="b6deb-103">Azure Cosmos DB : Générer une application .NET à l’aide de l’API Graph de hello</span><span class="sxs-lookup"><span data-stu-id="b6deb-103">Azure Cosmos DB: Build a .NET application using hello Graph API</span></span>

<span data-ttu-id="b6deb-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="b6deb-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b6deb-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="b6deb-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b6deb-106">Ce démarrage rapide montre comment toocreate un compte de base de données Azure Cosmos, base de données et à l’aide du graphique (conteneur) hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b6deb-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, database, and graph (container) using hello Azure portal.</span></span> <span data-ttu-id="b6deb-107">Vous puis créer et exécuter une application de console basée sur hello [API Graph](graph-sdk-dotnet.md) (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="b6deb-107">You then build and run a console app built on hello [Graph API](graph-sdk-dotnet.md) (preview).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="b6deb-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b6deb-108">Prerequisites</span></span>

<span data-ttu-id="b6deb-109">Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello **libre** [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b6deb-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="b6deb-110">Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="b6deb-111">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="b6deb-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="b6deb-112">Ajout d’un graphique</span><span class="sxs-lookup"><span data-stu-id="b6deb-112">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="b6deb-113">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="b6deb-113">Clone hello sample application</span></span>

<span data-ttu-id="b6deb-114">Maintenant, nous allons une API graphique le clonage d’application à partir de github, définir la chaîne de connexion hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="b6deb-114">Now let's clone a Graph API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="b6deb-115">Vous allez voir combien il est facile toowork avec des données par programme.</span><span class="sxs-lookup"><span data-stu-id="b6deb-115">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="b6deb-116">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="b6deb-116">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="b6deb-117">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-117">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. <span data-ttu-id="b6deb-118">Ouvrez Visual Studio et fichier de solution hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="b6deb-118">Then open Visual Studio and open hello solution file.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="b6deb-119">Réviser le code hello</span><span class="sxs-lookup"><span data-stu-id="b6deb-119">Review hello code</span></span>

<span data-ttu-id="b6deb-120">Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="b6deb-121">Fichier de Program.cs hello ouvert et que vous trouverez ces lignes de code créent hello des ressources de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b6deb-121">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="b6deb-122">Hello DocumentClient est initialisé.</span><span class="sxs-lookup"><span data-stu-id="b6deb-122">hello DocumentClient is initialized.</span></span> <span data-ttu-id="b6deb-123">Dans l’aperçu de hello, nous avons ajouté une API d’extension graphique sur le client de base de données Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-123">In hello preview, we added a graph extension API on hello Azure Cosmos DB client.</span></span> <span data-ttu-id="b6deb-124">Nous travaillons sur un client de graphique autonome dissocié des ressources et de client de base de données Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-124">We are working on a standalone graph client decoupled from hello Azure Cosmos DB client and resources.</span></span>

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* <span data-ttu-id="b6deb-125">Une nouvelle base de données est créée.</span><span class="sxs-lookup"><span data-stu-id="b6deb-125">A new database is created.</span></span>

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* <span data-ttu-id="b6deb-126">Un nouveau graphique est créé.</span><span class="sxs-lookup"><span data-stu-id="b6deb-126">A new graph is created.</span></span>

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* <span data-ttu-id="b6deb-127">Une série d’étapes de GREMLINE sont exécutées à l’aide de hello `CreateGremlinQuery` (méthode).</span><span class="sxs-lookup"><span data-stu-id="b6deb-127">A series of Gremlin steps are executed using hello `CreateGremlinQuery` method.</span></span>

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="b6deb-128">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="b6deb-128">Update your connection string</span></span>

<span data-ttu-id="b6deb-129">Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="b6deb-130">Dans Visual Studio 2017, ouvrez le fichier App.config de hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-130">In Visual Studio 2017, open hello App.config file.</span></span> 

2. <span data-ttu-id="b6deb-131">Bonjour portail Azure, dans votre compte de base de données Azure Cosmos, cliquez sur **clés** Bonjour barre de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="b6deb-131">In hello Azure portal, in your Azure Cosmos DB account, click **Keys** in hello left navigation.</span></span> 

    ![Afficher et copier une clé primaire dans hello portail Azure, sur la page clés de hello](./media/create-graph-dotnet/keys.png)

3. <span data-ttu-id="b6deb-133">Copiez votre **URI** à partir du portail de hello et le rendre hello la valeur de clé de point de terminaison hello dans App.config. Vous pouvez utiliser le bouton Copier de hello comme indiqué dans hello précédant la valeur de capture d’écran toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-133">Copy your **URI** value from hello portal and make it hello value of hello Endpoint key in App.config. You can use hello copy button as shown in hello preceding screenshot toocopy hello value.</span></span>

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. <span data-ttu-id="b6deb-134">Copiez votre **clé primaire** à partir du portail de hello et le rendre hello la valeur de clé de AuthKey hello dans App.config, puis enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="b6deb-134">Copy your **PRIMARY KEY** value from hello portal, and make it hello value of hello AuthKey key in App.config, then save your changes.</span></span> 

    `<add key="AuthKey" value="FILLME" />`

<span data-ttu-id="b6deb-135">Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b6deb-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-console-app"></a><span data-ttu-id="b6deb-136">Exécutez l’application de console hello</span><span class="sxs-lookup"><span data-stu-id="b6deb-136">Run hello console app</span></span>

1. <span data-ttu-id="b6deb-137">Dans Visual Studio, cliquez sur hello **GraphGetStarted** projet **l’Explorateur de solutions** puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b6deb-137">In Visual Studio, right-click on hello **GraphGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="b6deb-138">Bonjour NuGet **Parcourir** , tapez *Microsoft.Azure.Graphs* et vérifiez hello **inclut la version préliminaire** boîte.</span><span class="sxs-lookup"><span data-stu-id="b6deb-138">In hello NuGet **Browse** box, type *Microsoft.Azure.Graphs* and check hello **Includes prerelease** box.</span></span> 

3. <span data-ttu-id="b6deb-139">À partir des résultats de hello, installez hello **Microsoft.Azure.Graphs** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="b6deb-139">From hello results, install hello **Microsoft.Azure.Graphs** library.</span></span> <span data-ttu-id="b6deb-140">Cette opération installe le package de bibliothèque d’extension du graphique de base de données Azure Cosmos hello et toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="b6deb-140">This installs hello Azure Cosmos DB graph extension library package and all dependencies.</span></span>

    <span data-ttu-id="b6deb-141">Si vous obtenez un message sur la vérification des modifications toohello solution, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6deb-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="b6deb-142">Si vous obtenez un message concernant l’acceptation de la licence, cliquez sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="b6deb-142">If you get a message about license acceptance, click **I accept**.</span></span>

4. <span data-ttu-id="b6deb-143">Cliquez sur CTRL + F5 application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="b6deb-143">Click CTRL + F5 toorun hello application.</span></span>

   <span data-ttu-id="b6deb-144">fenêtre de console Hello affiche les sommets hello et bords ajoutés toohello graphique.</span><span class="sxs-lookup"><span data-stu-id="b6deb-144">hello console window displays hello vertexes and edges being added toohello graph.</span></span> <span data-ttu-id="b6deb-145">Lorsque hello script terminé, appuyez sur entrée à deux reprises les fenêtre de console hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="b6deb-145">When hello script completes, press ENTER twice tooclose hello console window.</span></span> 

## <a name="browse-using-hello-data-explorer"></a><span data-ttu-id="b6deb-146">Accédez à l’aide de hello Explorateur de données</span><span class="sxs-lookup"><span data-stu-id="b6deb-146">Browse using hello Data Explorer</span></span>

<span data-ttu-id="b6deb-147">Vous pouvez maintenant revenir en arrière tooData Explorer Bonjour portail Azure et parcourir et interroger vos nouvelles données de graphique.</span><span class="sxs-lookup"><span data-stu-id="b6deb-147">You can now go back tooData Explorer in hello Azure portal and browse and query your new graph data.</span></span>

1. <span data-ttu-id="b6deb-148">Dans l’Explorateur de données, la nouvelle base de données hello s’affiche dans le volet de graphiques hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-148">In Data Explorer, hello new database appears in hello Graphs pane.</span></span> <span data-ttu-id="b6deb-149">Développez **graphdb**, **graphcollz**, puis cliquez sur **Graphique**.</span><span class="sxs-lookup"><span data-stu-id="b6deb-149">Expand **graphdb**, **graphcollz**, and then click **Graph**.</span></span>

2. <span data-ttu-id="b6deb-150">Cliquez sur hello **appliquer le filtre** de requête par défaut de bouton toouse hello tooview tous les verticies hello dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-150">Click hello **Apply Filter** button toouse hello default query tooview all hello verticies in hello graph.</span></span> <span data-ttu-id="b6deb-151">données Hello générées par application d’exemple hello s’affiche dans le volet de graphiques hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-151">hello data generated by hello sample app is displayed in hello Graphs pane.</span></span>

    <span data-ttu-id="b6deb-152">Vous pouvez effectuer un zoom et graphique de hello, vous pouvez développer l’espace d’affichage graphique hello, ajouter verticies supplémentaires et déplacer la surface d’affichage verticies sur hello.</span><span class="sxs-lookup"><span data-stu-id="b6deb-152">You can zoom in and out of hello graph, you can expand hello graph display space, add additional verticies, and move verticies on hello display surface.</span></span>

    ![Afficher le graphique dans l’Explorateur de données hello Bonjour portail Azure](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="b6deb-154">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b6deb-154">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b6deb-155">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="b6deb-155">Clean up resources</span></span>

<span data-ttu-id="b6deb-156">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b6deb-156">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="b6deb-157">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="b6deb-157">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="b6deb-158">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b6deb-158">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6deb-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6deb-159">Next steps</span></span>

<span data-ttu-id="b6deb-160">Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer un graphique à l’aide de hello Explorateur de données et exécuter une application.</span><span class="sxs-lookup"><span data-stu-id="b6deb-160">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="b6deb-161">Vous pouvez maintenant générer des requêtes plus complexes et implémenter une logique de traversée de graphique puissante, à l’aide de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="b6deb-161">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b6deb-162">Interroger à l’aide de Gremlin</span><span class="sxs-lookup"><span data-stu-id="b6deb-162">Query using Gremlin</span></span>](tutorial-query-graph.md)

