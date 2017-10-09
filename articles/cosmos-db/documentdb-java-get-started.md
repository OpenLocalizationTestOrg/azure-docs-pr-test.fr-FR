---
title: "Didacticiel NoSQL : API DocumentDB pour le kit SDK Java Azure Cosmos DB | Microsoft Docs"
description: "Didacticiel NoSQL qui crée une base de données en ligne et l’application de console Java à l’aide de hello API DocumentDB de base de données Azure Cosmos. Azure DocumentDB est une base de données NoSQL pour JSON."
keywords: "didacticiel nosql, base de données en ligne, application console java"
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="a3020-105">Didacticiel NoSQL : Générer une application console Java avec l’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="a3020-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a3020-106">.NET</span><span class="sxs-lookup"><span data-stu-id="a3020-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="a3020-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a3020-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="a3020-108">Node.js pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="a3020-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="a3020-109">Node.JS</span><span class="sxs-lookup"><span data-stu-id="a3020-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="a3020-110">Java</span><span class="sxs-lookup"><span data-stu-id="a3020-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="a3020-111">C++</span><span class="sxs-lookup"><span data-stu-id="a3020-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="a3020-112">Didacticiel de NoSQL toohello Bienvenue pour hello API DocumentDB pour le Kit de développement Java Azure Cosmos DB !</span><span class="sxs-lookup"><span data-stu-id="a3020-112">Welcome toohello NoSQL tutorial for hello DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="a3020-113">À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a3020-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="a3020-114">Le programme est le suivant :</span><span class="sxs-lookup"><span data-stu-id="a3020-114">We cover:</span></span>

* <span data-ttu-id="a3020-115">Création et connexion de compte de base de données Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="a3020-115">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="a3020-116">Configuration de votre solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3020-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="a3020-117">Création d’une base de données en ligne</span><span class="sxs-lookup"><span data-stu-id="a3020-117">Creating an online database</span></span>
* <span data-ttu-id="a3020-118">Création d’une collection</span><span class="sxs-lookup"><span data-stu-id="a3020-118">Creating a collection</span></span>
* <span data-ttu-id="a3020-119">Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="a3020-119">Creating JSON documents</span></span>
* <span data-ttu-id="a3020-120">Interrogation de collection de hello</span><span class="sxs-lookup"><span data-stu-id="a3020-120">Querying hello collection</span></span>
* <span data-ttu-id="a3020-121">Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="a3020-121">Creating JSON documents</span></span>
* <span data-ttu-id="a3020-122">Interrogation de collection de hello</span><span class="sxs-lookup"><span data-stu-id="a3020-122">Querying hello collection</span></span>
* <span data-ttu-id="a3020-123">Remplacement d'un document</span><span class="sxs-lookup"><span data-stu-id="a3020-123">Replacing a document</span></span>
* <span data-ttu-id="a3020-124">Suppression d’un document</span><span class="sxs-lookup"><span data-stu-id="a3020-124">Deleting a document</span></span>
* <span data-ttu-id="a3020-125">Suppression de la base de données hello</span><span class="sxs-lookup"><span data-stu-id="a3020-125">Deleting hello database</span></span>

<span data-ttu-id="a3020-126">Commençons dès maintenant !</span><span class="sxs-lookup"><span data-stu-id="a3020-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3020-127">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a3020-127">Prerequisites</span></span>
<span data-ttu-id="a3020-128">Vérifiez que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="a3020-128">Make sure you have hello following:</span></span>

* <span data-ttu-id="a3020-129">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="a3020-129">An active Azure account.</span></span> <span data-ttu-id="a3020-130">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a3020-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="a3020-131">Vous pouvez également utiliser hello [Azure Cosmos DB émulateur](local-emulator.md) pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a3020-131">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="a3020-132">Git</span><span class="sxs-lookup"><span data-stu-id="a3020-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="a3020-133">[Kit de développement logiciel Java (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)</span><span class="sxs-lookup"><span data-stu-id="a3020-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="a3020-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="a3020-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="a3020-135">Étape 1 : créer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a3020-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="a3020-136">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a3020-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="a3020-137">Si vous avez déjà un compte que vous souhaitez toouse, vous pouvez passer trop[projet de Clone hello GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="a3020-137">If you already have an account you want toouse, you can skip ahead too[Clone hello GitHub project](#GitClone).</span></span> <span data-ttu-id="a3020-138">Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) tooset jusqu'à l’émulateur de hello et passer trop[projet de Clone hello GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="a3020-138">If you are using hello Azure Cosmos DB Emulator, follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) tooset up hello emulator and skip ahead too[Clone hello GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="a3020-139"><a id="GitClone"></a>Étape 2 : Cloner des projets de GitHub hello</span><span class="sxs-lookup"><span data-stu-id="a3020-139"><a id="GitClone"></a>Step 2: Clone hello GitHub project</span></span>
<span data-ttu-id="a3020-140">Vous pouvez commencer par le clonage du référentiel GitHub de hello pour [prise en main Azure Cosmos DB et Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="a3020-140">You can get started by cloning hello GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="a3020-141">Par exemple, à partir d’un répertoire local exécuter hello suivant tooretrieve hello exemple de projet localement.</span><span class="sxs-lookup"><span data-stu-id="a3020-141">For example, from a local directory run hello following tooretrieve hello sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="a3020-142">Hello répertoire contient un `pom.xml` pour le projet de hello et un `src` dossier qui contient, y compris le code Java source `Program.java` qui indique comment effectuer des opérations simples avec la base de données Azure Cosmos telles que la création de documents et l’interrogation des données dans un collection.</span><span class="sxs-lookup"><span data-stu-id="a3020-142">hello directory contains a `pom.xml` for hello project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="a3020-143">Hello `pom.xml` inclut une dépendance sur hello [DocumentDB Java SDK sur Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="a3020-143">hello `pom.xml` includes a dependency on hello [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="a3020-144"><a id="Connect"></a>Étape 3 : Relier le compte de base de données Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="a3020-144"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="a3020-145">Ensuite, head sauvegarde toohello [Azure Portal](https://portal.azure.com) tooretrieve votre point de terminaison et la clé principale du principale.</span><span class="sxs-lookup"><span data-stu-id="a3020-145">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint and primary master key.</span></span> <span data-ttu-id="a3020-146">Hello point de terminaison de base de données Azure Cosmos et la clé primaire sont nécessaires pour votre application toounderstand où tooconnect et de base de données Azure Cosmos tootrust connexion de votre application.</span><span class="sxs-lookup"><span data-stu-id="a3020-146">hello Azure Cosmos DB endpoint and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="a3020-147">Dans hello portail Azure, accédez de compte de base de données Azure Cosmos tooyour, puis cliquez sur **clés**.</span><span class="sxs-lookup"><span data-stu-id="a3020-147">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="a3020-148">Copiez hello URI à partir du portail de hello, puis collez-la dans `https://FILLME.documents.azure.com` dans le fichier de Program.java hello.</span><span class="sxs-lookup"><span data-stu-id="a3020-148">Copy hello URI from hello portal and paste it into `https://FILLME.documents.azure.com` in hello Program.java file.</span></span> <span data-ttu-id="a3020-149">Copie hello clé primaire à partir du portail de hello et collez-la dans `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="a3020-149">Then copy hello PRIMARY KEY from hello portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Capture d’écran de hello portail Azure utilisée par hello toocreate de didacticiel NoSQL une application de console Java.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="a3020-152">Étape 4 : créer une base de données</span><span class="sxs-lookup"><span data-stu-id="a3020-152">Step 4: Create a database</span></span>
<span data-ttu-id="a3020-153">Votre base de données Azure Cosmos [base de données](documentdb-resources.md#databases) peuvent être créés à l’aide de hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) méthode Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="a3020-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="a3020-154">Une base de données est un conteneur logique de hello JSON de stockage de documents partitionné entre des collections.</span><span class="sxs-lookup"><span data-stu-id="a3020-154">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="a3020-155"><a id="CreateColl"></a>Étape 5 : créer une collection</span><span class="sxs-lookup"><span data-stu-id="a3020-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="a3020-156">**createCollection** crée une collection avec un débit réservé, ce qui a des conséquences sur la tarification.</span><span class="sxs-lookup"><span data-stu-id="a3020-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="a3020-157">Pour plus d’informations, consultez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="a3020-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="a3020-158">A [collection](documentdb-resources.md#collections) peuvent être créés à l’aide de hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) méthode Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="a3020-158">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="a3020-159">Une collection est un conteneur de documents JSON. Elle est associée à une logique d'application JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a3020-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="a3020-160"><a id="CreateDoc"></a>Étape 6 : Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="a3020-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="a3020-161">A [document](documentdb-resources.md#documents) peuvent être créés à l’aide de hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) méthode Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="a3020-161">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="a3020-162">Les documents sont du contenu JSON (arbitraire) défini par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a3020-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="a3020-163">Nous pouvons maintenant insérer un ou plusieurs documents.</span><span class="sxs-lookup"><span data-stu-id="a3020-163">We can now insert one or more documents.</span></span> <span data-ttu-id="a3020-164">Si vous avez déjà des données que vous souhaitez toostore dans votre base de données, vous pouvez utiliser Azure Cosmos DB [l’outil de Migration de données](import-data.md) tooimport les données de salutation dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="a3020-164">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![Diagramme illustrant relation hiérarchique hello entre le compte de hello, la base de données en ligne hello, collection de hello et documents hello utilisés par hello toocreate de didacticiel NoSQL une application de console Java](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="a3020-166"><a id="Query"></a>Étape 7 : interroger les ressources Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a3020-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="a3020-167">Azure Cosmos DB prend en charge les [requêtes](documentdb-sql-query.md) enrichies sur les documents JSON stockés dans chaque collection.</span><span class="sxs-lookup"><span data-stu-id="a3020-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="a3020-168">Hello suivant l’exemple de code montre comment tooquery décrit dans la base de données Azure Cosmos à l’aide de la syntaxe SQL hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) (méthode).</span><span class="sxs-lookup"><span data-stu-id="a3020-168">hello following sample code shows how tooquery documents in Azure Cosmos DB using SQL syntax with hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="a3020-169"><a id="ReplaceDocument"></a>Étape 8 : remplacer le document JSON</span><span class="sxs-lookup"><span data-stu-id="a3020-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="a3020-170">Base de données Azure Cosmos prend en charge la mise à jour des documents JSON à l’aide de hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) (méthode).</span><span class="sxs-lookup"><span data-stu-id="a3020-170">Azure Cosmos DB supports updating JSON documents using hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="a3020-171"><a id="DeleteDocument"></a>Étape 9 : supprimer le document JSON</span><span class="sxs-lookup"><span data-stu-id="a3020-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="a3020-172">De même, base de données Azure Cosmos prend en charge la suppression de documents JSON à l’aide de hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) (méthode).</span><span class="sxs-lookup"><span data-stu-id="a3020-172">Similarly, Azure Cosmos DB supports deleting JSON documents using hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="a3020-173"><a id="DeleteDatabase"></a>Étape 10 : Supprimer la base de données hello</span><span class="sxs-lookup"><span data-stu-id="a3020-173"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="a3020-174">Base de données de suppression hello créé supprime de la base de données hello et toutes les ressources enfants (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="a3020-174">Deleting hello created database removes hello database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="a3020-175"><a id="Run"></a>Étape 11 : exécuter votre application console C#</span><span class="sxs-lookup"><span data-stu-id="a3020-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="a3020-176">application de hello toorun à partir de la console hello, accédez à toohello le dossier de projet et de la compilation à l’aide de Maven :</span><span class="sxs-lookup"><span data-stu-id="a3020-176">toorun hello application from hello console, navigate toohello project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="a3020-177">En cours d’exécution `mvn package` télécharge la bibliothèque de base de données Azure Cosmos hello plus récente à partir de Maven et produit `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="a3020-177">Running `mvn package` downloads hello latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="a3020-178">Puis exécutez l’application hello en exécutant :</span><span class="sxs-lookup"><span data-stu-id="a3020-178">Then run hello app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="a3020-179">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="a3020-179">Congratulations!</span></span> <span data-ttu-id="a3020-180">Vous avez terminé ce didacticiel NoSQL et vous disposez d’une application console Java opérationnelle !</span><span class="sxs-lookup"><span data-stu-id="a3020-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3020-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a3020-181">Next steps</span></span>
* <span data-ttu-id="a3020-182">Vous recherchez un didacticiel sur les applications web Java ?</span><span class="sxs-lookup"><span data-stu-id="a3020-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="a3020-183">Consultez [Créer une application web Java avec Azure Cosmos DB](documentdb-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="a3020-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="a3020-184">Découvrez comment trop[surveiller un compte de base de données Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="a3020-184">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="a3020-185">Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="a3020-185">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="a3020-186">En savoir plus sur le modèle de programmation hello Bonjour section développer Hello [page de documentation de base de données Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="a3020-186">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
