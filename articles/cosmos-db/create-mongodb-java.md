---
title: "Azure Cosmos DB : Générer une application de console avec Java et hello MongoDB API | Documents Microsoft"
description: "Présente un exemple de code Java que vous pouvez utiliser la requête de tooand tooconnect hello Azure Cosmos DB MongoDB API"
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
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a><span data-ttu-id="1099b-103">Azure Cosmos DB : Génération d’une application de console MongoDB API avec Java et hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1099b-103">Azure Cosmos DB: Build a MongoDB API console app with Java and hello Azure portal</span></span>

<span data-ttu-id="1099b-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="1099b-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="1099b-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="1099b-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="1099b-106">Ce démarrage rapide montre comment toocreate un compte de base de données Azure Cosmos, base de données du document et à l’aide de la collection hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1099b-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="1099b-107">Vous allez ensuite générer et déployer une application de console basée sur hello [pilote MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="1099b-107">You'll then build and deploy a console app built on hello [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1099b-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1099b-108">Prerequisites</span></span>

* <span data-ttu-id="1099b-109">Avant de pouvoir exécuter cet exemple, vous devez disposer de hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="1099b-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
   * <span data-ttu-id="1099b-110">JDK 1.7 + (exécutez `apt-get install default-jdk` si vous ne possédez pas JDK)</span><span class="sxs-lookup"><span data-stu-id="1099b-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="1099b-111">Maven (exécutez `apt-get install maven` si vous ne possédez pas Maven)</span><span class="sxs-lookup"><span data-stu-id="1099b-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="1099b-112">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="1099b-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="1099b-113">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="1099b-113">Add a collection</span></span>

<span data-ttu-id="1099b-114">Nommez votre nouvelle base de données, **db**, et votre nouvelle collection, **coll**.</span><span class="sxs-lookup"><span data-stu-id="1099b-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="1099b-115">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="1099b-115">Clone hello sample application</span></span>

<span data-ttu-id="1099b-116">Maintenant, nous allons une API MongoDB le clonage d’application à partir de github, définir la chaîne de connexion hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="1099b-116">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="1099b-117">Vous allez voir combien il est facile toowork avec des données par programme.</span><span class="sxs-lookup"><span data-stu-id="1099b-117">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="1099b-118">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="1099b-118">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="1099b-119">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="1099b-119">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="1099b-120">Ouvrez ensuite le fichier de solution de hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1099b-120">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="1099b-121">Réviser le code hello</span><span class="sxs-lookup"><span data-stu-id="1099b-121">Review hello code</span></span>

<span data-ttu-id="1099b-122">Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1099b-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="1099b-123">Ouvrez hello `Program.cs` fichier et que vous trouverez ces lignes de code créent hello des ressources de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="1099b-123">Open hello `Program.cs` file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="1099b-124">Hello DocumentClient est initialisé.</span><span class="sxs-lookup"><span data-stu-id="1099b-124">hello DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="1099b-125">Une base de données et une collection ont été créées.</span><span class="sxs-lookup"><span data-stu-id="1099b-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="1099b-126">Certains documents sont intégrés à l’aide de `MongoCollection.insertOne`</span><span class="sxs-lookup"><span data-stu-id="1099b-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="1099b-127">Certaines requêtes sont effectuées à l’aide de `MongoCollection.find`</span><span class="sxs-lookup"><span data-stu-id="1099b-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="1099b-128">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="1099b-128">Update your connection string</span></span>

<span data-ttu-id="1099b-129">Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="1099b-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="1099b-130">À partir de hello compte, sélectionnez **Quick Start**, sélectionnez Java, puis copiez le Presse-papiers de tooyour de chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="1099b-130">From hello Account, select **Quick Start**, select Java, then copy hello connection string tooyour clipboard</span></span>

2. <span data-ttu-id="1099b-131">Ouvrez hello `Program.java` fichier, remplacer le constructeur de hello argument toohello MongoClientURI avec la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="1099b-131">Open hello `Program.java` file, replace hello argument toohello MongoClientURI constructor with hello connection string.</span></span> <span data-ttu-id="1099b-132">Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="1099b-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-console-app"></a><span data-ttu-id="1099b-133">Exécutez l’application de console hello</span><span class="sxs-lookup"><span data-stu-id="1099b-133">Run hello console app</span></span>

1. <span data-ttu-id="1099b-134">Exécutez `mvn package` dans un terminal tooinstall requis des modules npm</span><span class="sxs-lookup"><span data-stu-id="1099b-134">Run `mvn package` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="1099b-135">Exécutez `mvn exec:java -D exec.mainClass=GetStarted.Program` dans un terminal toostart votre application Java.</span><span class="sxs-lookup"><span data-stu-id="1099b-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal toostart your Java application.</span></span>

<span data-ttu-id="1099b-136">Vous pouvez maintenant utiliser [Robomongo](mongodb-robomongo.md) / [Studio 3P](mongodb-mongochef.md) tooquery, modifier et travailler avec ces nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="1099b-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modify, and work with this new data.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="1099b-137">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1099b-137">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="1099b-138">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="1099b-138">Clean up resources</span></span>

<span data-ttu-id="1099b-139">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1099b-139">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="1099b-140">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="1099b-140">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="1099b-141">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="1099b-141">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1099b-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1099b-142">Next steps</span></span>

<span data-ttu-id="1099b-143">Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer une collection à l’aide de hello Explorateur de données et exécuter une application console.</span><span class="sxs-lookup"><span data-stu-id="1099b-143">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a console app.</span></span> <span data-ttu-id="1099b-144">Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="1099b-144">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1099b-145">Importer des données MongoDB dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1099b-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


