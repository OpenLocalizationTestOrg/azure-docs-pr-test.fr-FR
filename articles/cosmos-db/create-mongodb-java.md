---
title: "Azure Cosmos DB : Développer une application console avec Java et l’API MongoDB | Microsoft Docs"
description: "Cet article présente un exemple de code Java que vous pouvez utiliser pour vous connecter à l’API MongoDB d’Azure Cosmos DB, et pour l’interroger."
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
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: f84294d7d324f094d173f7a2ec89759266a74210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-the-azure-portal"></a><span data-ttu-id="b5e62-103">Azure Cosmos DB : Développer une application console API MongoDB avec Java et le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b5e62-103">Azure Cosmos DB: Build a MongoDB API console app with Java and the Azure portal</span></span>

<span data-ttu-id="b5e62-104">Azure Cosmos DB est un service de base de données multi-modèles mondialement distribué par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b5e62-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b5e62-105">Rapidement, vous avez la possibilité de créer et d’interroger des documents, des paires clé/valeur, et des bases de données orientées graphe, profitant tous de la distribution à l’échelle mondiale et des capacités de mise à l’échelle horizontale au cœur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b5e62-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b5e62-106">Ce guide de démarrage rapide explique comment créer, à l’aide du Portail Azure, un compte Azure Cosmos DB, une base de données de documents, ainsi qu’une collection.</span><span class="sxs-lookup"><span data-stu-id="b5e62-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="b5e62-107">Vous allez ensuite créer et déployer une application console basée sur le [pilote Java MongoDB](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="b5e62-107">You'll then build and deploy a console app built on the [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b5e62-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b5e62-108">Prerequisites</span></span>

* <span data-ttu-id="b5e62-109">Avant de pouvoir exécuter cet exemple, vous devez posséder les composants requis suivants :</span><span class="sxs-lookup"><span data-stu-id="b5e62-109">Before you can run this sample, you must have the following prerequisites:</span></span>
   * <span data-ttu-id="b5e62-110">JDK 1.7 + (exécutez `apt-get install default-jdk` si vous ne possédez pas JDK)</span><span class="sxs-lookup"><span data-stu-id="b5e62-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="b5e62-111">Maven (exécutez `apt-get install maven` si vous ne possédez pas Maven)</span><span class="sxs-lookup"><span data-stu-id="b5e62-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="b5e62-112">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="b5e62-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="b5e62-113">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="b5e62-113">Add a collection</span></span>

<span data-ttu-id="b5e62-114">Nommez votre nouvelle base de données, **db**, et votre nouvelle collection, **coll**.</span><span class="sxs-lookup"><span data-stu-id="b5e62-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="b5e62-115">Clonage de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="b5e62-115">Clone the sample application</span></span>

<span data-ttu-id="b5e62-116">À présent, nous allons cloner une application API MongoDB à partir de GitHub, configurer la chaîne de connexion, et l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="b5e62-116">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="b5e62-117">Vous verrez combien il est facile de travailler par programmation avec des données.</span><span class="sxs-lookup"><span data-stu-id="b5e62-117">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="b5e62-118">Ouvrez une fenêtre de terminal git, comme git bash, et accédez à un répertoire de travail à l’aide de la commande `cd`.</span><span class="sxs-lookup"><span data-stu-id="b5e62-118">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="b5e62-119">Exécutez la commande suivante pour cloner l’exemple de référentiel.</span><span class="sxs-lookup"><span data-stu-id="b5e62-119">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="b5e62-120">Ouvrez le fichier de solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b5e62-120">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="b5e62-121">Examiner le code</span><span class="sxs-lookup"><span data-stu-id="b5e62-121">Review the code</span></span>

<span data-ttu-id="b5e62-122">Passons rapidement en revue ce qu’il se passe dans l’application.</span><span class="sxs-lookup"><span data-stu-id="b5e62-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="b5e62-123">Ouvrez le fichier `Program.cs` et vous découvrirez que ces lignes de code créent les ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b5e62-123">Open the `Program.cs` file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="b5e62-124">Le DocumentClient est initialisé.</span><span class="sxs-lookup"><span data-stu-id="b5e62-124">The DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="b5e62-125">Une base de données et une collection ont été créées.</span><span class="sxs-lookup"><span data-stu-id="b5e62-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="b5e62-126">Certains documents sont intégrés à l’aide de `MongoCollection.insertOne`</span><span class="sxs-lookup"><span data-stu-id="b5e62-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="b5e62-127">Certaines requêtes sont effectuées à l’aide de `MongoCollection.find`</span><span class="sxs-lookup"><span data-stu-id="b5e62-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="b5e62-128">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="b5e62-128">Update your connection string</span></span>

<span data-ttu-id="b5e62-129">Maintenant, retournez sur le Portail Azure afin d’obtenir vos informations de chaîne de connexion, et copiez-les dans l’application.</span><span class="sxs-lookup"><span data-stu-id="b5e62-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="b5e62-130">À partir du compte, sélectionnez **Démarrage rapide**et Java, puis copiez la chaîne de connexion dans votre presse-papiers</span><span class="sxs-lookup"><span data-stu-id="b5e62-130">From the Account, select **Quick Start**, select Java, then copy the connection string to your clipboard</span></span>

2. <span data-ttu-id="b5e62-131">Ouvrez le fichier `Program.java`, remplacez l’argument au constructeur MongoClientURI par la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="b5e62-131">Open the `Program.java` file, replace the argument to the MongoClientURI constructor with the connection string.</span></span> <span data-ttu-id="b5e62-132">Vous venez de mettre à jour votre application avec toutes les informations nécessaires pour communiquer avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b5e62-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-console-app"></a><span data-ttu-id="b5e62-133">Exécuter l’application console</span><span class="sxs-lookup"><span data-stu-id="b5e62-133">Run the console app</span></span>

1. <span data-ttu-id="b5e62-134">Exécutez `mvn package` sur un terminal pour installer les modules npm requis.</span><span class="sxs-lookup"><span data-stu-id="b5e62-134">Run `mvn package` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="b5e62-135">Exécutez `mvn exec:java -D exec.mainClass=GetStarted.Program` sur un terminal pour démarrer votre application Java.</span><span class="sxs-lookup"><span data-stu-id="b5e62-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal to start your Java application.</span></span>

<span data-ttu-id="b5e62-136">Vous pouvez maintenant utiliser [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) pour interroger ces nouvelles données, pour les modifier, et pour travailler avec elles.</span><span class="sxs-lookup"><span data-stu-id="b5e62-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) to query, modify, and work with this new data.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="b5e62-137">Examiner les SLA dans le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b5e62-137">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b5e62-138">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="b5e62-138">Clean up resources</span></span>

<span data-ttu-id="b5e62-139">Si vous ne pensez pas continuer à utiliser cette application, supprimez toutes les ressources créées durant ce guide de démarrage rapide dans le Portail Azure en procédant de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="b5e62-139">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="b5e62-140">Dans le menu de gauche du portail Azure, cliquez sur **Groupes de ressources**, puis sur le nom de la ressource que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="b5e62-140">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="b5e62-141">Dans la page de votre groupe de ressources, cliquez sur **Supprimer**, tapez le nom de la ressource à supprimer dans la zone de texte, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b5e62-141">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5e62-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b5e62-142">Next steps</span></span>

<span data-ttu-id="b5e62-143">Dans ce guide de démarrage rapide, vous avez appris à créer un compte Azure Cosmos DB, à créer une collection à l’aide de l’Explorateur de données, et à exécuter une application console.</span><span class="sxs-lookup"><span data-stu-id="b5e62-143">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a console app.</span></span> <span data-ttu-id="b5e62-144">Vous pouvez maintenant importer des données supplémentaires à votre compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b5e62-144">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5e62-145">Importer des données MongoDB dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b5e62-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


