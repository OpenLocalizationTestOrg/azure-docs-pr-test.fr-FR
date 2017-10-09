---
title: "aaaCreate une base de données du document de base de données Azure Cosmos avec Java | Documents Microsoft | Des documents Microsoft"
description: "Présente un exemple de code Java que vous pouvez utiliser la requête de tooand tooconnect hello Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="b2467-103">Base de données Cosmos Azure : Créer une base de données de document à l’aide de Java et hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b2467-103">Azure Cosmos DB: Create a document database using Java and hello Azure portal</span></span>

<span data-ttu-id="b2467-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="b2467-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b2467-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="b2467-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b2467-106">Ce démarrage rapide crée un document à l’aide de la base de données hello outils portails Azure pour la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b2467-106">This quickstart creates a document database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="b2467-107">Ce démarrage rapide montre comment tooquickly créer une application de console Java à l’aide de hello [DocumentDB Java API](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="b2467-107">This quickstart also shows you how tooquickly create a Java console app using hello [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="b2467-108">instructions Hello dans ce démarrage rapide peuvent être suivies sur n’importe quel système d’exploitation qui est capable d’exécuter Java.</span><span class="sxs-lookup"><span data-stu-id="b2467-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="b2467-109">En effectuant ce démarrage rapide, vous serez familiarisé avec la création et la modification des ressources de base de données de document dans soit hello l’interface utilisateur ou par programme, selon votre préférence.</span><span class="sxs-lookup"><span data-stu-id="b2467-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either hello UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2467-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b2467-110">Prerequisites</span></span>

* [<span data-ttu-id="b2467-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="b2467-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="b2467-112">Sur Ubuntu, exécutez `apt-get install default-jdk` tooinstall hello JDK.</span><span class="sxs-lookup"><span data-stu-id="b2467-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="b2467-113">Être tooset vraiment hello JAVA_HOME variable toopoint toohello dossier d’environnement sur lequel hello JDK est installé.</span><span class="sxs-lookup"><span data-stu-id="b2467-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="b2467-114">[Téléchargement](http://maven.apache.org/download.cgi) et [installation](http://maven.apache.org/install.html) d’une archive binaire [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="b2467-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="b2467-115">Sur Ubuntu, vous pouvez exécuter `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="b2467-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="b2467-116">Git</span><span class="sxs-lookup"><span data-stu-id="b2467-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="b2467-117">Sur Ubuntu, vous pouvez exécuter `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="b2467-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="b2467-118">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="b2467-118">Create a database account</span></span>

<span data-ttu-id="b2467-119">Avant de pouvoir créer une base de données de document, vous devez toocreate un compte de base de données SQL (DocumentDB) avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b2467-119">Before you can create a document database, you need toocreate a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="b2467-120">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="b2467-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="b2467-121">Ajouter un exemple de données</span><span class="sxs-lookup"><span data-stu-id="b2467-121">Add sample data</span></span>

<span data-ttu-id="b2467-122">Vous pouvez maintenant ajouter la nouvelle collection données tooyour à l’aide de l’Explorateur de données.</span><span class="sxs-lookup"><span data-stu-id="b2467-122">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="b2467-123">Dans l’Explorateur de données, la nouvelle base de données hello s’affiche dans le volet de Collections hello.</span><span class="sxs-lookup"><span data-stu-id="b2467-123">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="b2467-124">Développez hello **tâches** de base de données, développez hello **éléments** collection, cliquez sur **Documents**, puis cliquez sur **nouveaux Documents**.</span><span class="sxs-lookup"><span data-stu-id="b2467-124">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Créer des documents dans l’Explorateur de données Bonjour portail Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="b2467-126">Maintenant ajouter une collection de toohello document avec hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="b2467-126">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="b2467-127">Une fois que vous avez ajouté hello json toohello **Documents** , cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b2467-127">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Copier des données json et cliquez sur Enregistrer dans l’Explorateur de données Bonjour portail Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="b2467-129">Créer et enregistrer un document plus où vous insérez une valeur unique pour hello `id` propriété et la modification hello autres propriétés comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="b2467-129">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="b2467-130">Vos nouveaux documents peuvent avoir la structure de votre choix car Azure Cosmos DB n’impose aucun schéma pour vos données.</span><span class="sxs-lookup"><span data-stu-id="b2467-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="b2467-131">Vous pouvez maintenant utiliser des requêtes dans l’Explorateur de données tooretrieve vos données en cliquant sur hello **modifier le filtre** et **appliquer le filtre** boutons.</span><span class="sxs-lookup"><span data-stu-id="b2467-131">You can now use queries in Data Explorer tooretrieve your data by clicking hello **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="b2467-132">Par défaut, l’Explorateur de données utilise `SELECT * FROM c` tooretrieve tous les documents dans la collection de hello, mais vous pouvez modifier ce tooa différents [requête SQL](documentdb-sql-query.md), tel que `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn tous les documents hello dans l’ordre décroissant en fonction de leur horodatage.</span><span class="sxs-lookup"><span data-stu-id="b2467-132">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="b2467-133">Vous pouvez également utiliser les procédures de toocreate stockée Explorateur de données, UDF et déclencheurs tooperform ainsi la logique métier côté serveur en tant que le débit de l’échelle.</span><span class="sxs-lookup"><span data-stu-id="b2467-133">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="b2467-134">Explorateur de données expose l’ensemble du hello intégrées par programmation l’accès aux données disponibles dans l’API de hello, mais il fournit des données un accès facile tooyour hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b2467-134">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="b2467-135">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="b2467-135">Clone hello sample application</span></span>

<span data-ttu-id="b2467-136">Maintenant nous allons passer tooworking avec le code.</span><span class="sxs-lookup"><span data-stu-id="b2467-136">Now let's switch tooworking with code.</span></span> <span data-ttu-id="b2467-137">Nous allons cloner une application API DocumentDB à partir de GitHub, définissez la chaîne de connexion hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="b2467-137">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="b2467-138">Vous voyez combien il est facile toowork avec des données par programme.</span><span class="sxs-lookup"><span data-stu-id="b2467-138">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="b2467-139">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `CD` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="b2467-139">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="b2467-140">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="b2467-140">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="b2467-141">Réviser le code hello</span><span class="sxs-lookup"><span data-stu-id="b2467-141">Review hello code</span></span>

<span data-ttu-id="b2467-142">Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b2467-142">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="b2467-143">Ouvrez hello `Program.java` de fichiers à partir du dossier \src\GetStarted hello et recherchez ces lignes de code qui créent des ressources de base de données Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="b2467-143">Open hello `Program.java` file from hello \src\GetStarted folder, and find these lines of code that create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="b2467-144">Hello `DocumentClient` est initialisé.</span><span class="sxs-lookup"><span data-stu-id="b2467-144">hello `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="b2467-145">Une nouvelle base de données est créée.</span><span class="sxs-lookup"><span data-stu-id="b2467-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="b2467-146">Une nouvelle collection est créée.</span><span class="sxs-lookup"><span data-stu-id="b2467-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="b2467-147">Certains documents sont créés.</span><span class="sxs-lookup"><span data-stu-id="b2467-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="b2467-148">Une requête SQL sur JSON est effectuée.</span><span class="sxs-lookup"><span data-stu-id="b2467-148">A SQL query over JSON is performed.</span></span>

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="b2467-149">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="b2467-149">Update your connection string</span></span>

<span data-ttu-id="b2467-150">Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="b2467-150">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span> <span data-ttu-id="b2467-151">Cette opération activera toocommunicate de votre application avec votre base de données hébergée.</span><span class="sxs-lookup"><span data-stu-id="b2467-151">This will enable your app toocommunicate with your hosted database.</span></span>

1. <span data-ttu-id="b2467-152">Bonjour [portail Azure](http://portal.azure.com/), dans votre base de données de Cosmos Azure account, Bonjour barre de navigation gauche, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**.</span><span class="sxs-lookup"><span data-stu-id="b2467-152">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="b2467-153">Vous allez utiliser les boutons de copier hello sur droite hello Hello de toocopy écran hello URI et la clé primaire dans hello `Program.java` fichier à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="b2467-153">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and PRIMARY KEY into hello `Program.java` file in hello next step.</span></span>

    ![Afficher et copier une clé d’accès dans hello portail Azure, le panneau de clés](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="b2467-155">Bonjour ouvrir `Program.java` de fichiers, copiez votre valeur d’URI à partir du portail hello (à l’aide du bouton de copie hello) et le rendre hello valeur de hello point de terminaison toohello DocumentClient constructeur dans `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="b2467-155">In hello open `Program.java` file, copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint toohello DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="b2467-156">Copiez la valeur de clé primaire à partir du portail de hello, puis collez-la sur « FILLME », ce qui hello second paramètre de constructeur de DocumentClient hello.</span><span class="sxs-lookup"><span data-stu-id="b2467-156">Then copy your PRIMARY KEY value from hello portal and paste it over “FILLME”, making it hello second parameter in hello DocumentClient constructor.</span></span> <span data-ttu-id="b2467-157">Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b2467-157">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-app"></a><span data-ttu-id="b2467-158">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="b2467-158">Run hello app</span></span>

1. <span data-ttu-id="b2467-159">Dans la fenêtre de terminal git hello, `cd` dossier azure-cosmos-db-documentdb-java-getting-started de toohello.</span><span class="sxs-lookup"><span data-stu-id="b2467-159">In hello git terminal window, `cd` toohello azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="b2467-160">Dans la fenêtre de terminal git hello, tapez `mvn package` tooinstall hello requis packages Java.</span><span class="sxs-lookup"><span data-stu-id="b2467-160">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="b2467-161">Dans la fenêtre de terminal git hello, exécutez `mvn exec:java -D exec.mainClass=GetStarted.Program` dans hello toostart de la fenêtre de terminal de votre application Java.</span><span class="sxs-lookup"><span data-stu-id="b2467-161">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

    <span data-ttu-id="b2467-162">Dans la fenêtre de terminal hello, vous recevrez une notification qui hello FamilyDB base de données a été créée et toopress une clé toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b2467-162">In hello terminal window, you'll receive notification that hello FamilyDB database was created, and toopress a key toocontinue.</span></span> <span data-ttu-id="b2467-163">Appuyez sur une base de données de clé toocreate hello, puis basculez toohello Explorateur de données, et vous verrez qu’il contient maintenant une base de données FamilyDB.</span><span class="sxs-lookup"><span data-stu-id="b2467-163">Press a key toocreate hello database, then switch toohello Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="b2467-164">Continuer toopress clés toocreate hello hello et la collection documents, puis effectuez une requête.</span><span class="sxs-lookup"><span data-stu-id="b2467-164">Continue toopress keys toocreate hello collection and hello documents and then perform a query.</span></span> <span data-ttu-id="b2467-165">Lorsque le projet de hello est terminée, les ressources hello sont supprimés de votre compte.</span><span class="sxs-lookup"><span data-stu-id="b2467-165">When hello project completes, hello resources are deleted from your account.</span></span> 

    ![Afficher et copier une clé d’accès dans hello portail Azure, le panneau de clés](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="b2467-167">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b2467-167">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b2467-168">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="b2467-168">Clean up resources</span></span>

<span data-ttu-id="b2467-169">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b2467-169">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="b2467-170">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="b2467-170">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="b2467-171">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b2467-171">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2467-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b2467-172">Next steps</span></span>

<span data-ttu-id="b2467-173">Dans ce démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, base de données du document et la collection à l’aide de hello Explorateur de données et exécuter une application toodo hello même chose par programme.</span><span class="sxs-lookup"><span data-stu-id="b2467-173">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, document database, and collection using hello Data Explorer, and run an app toodo hello same thing programmatically.</span></span> <span data-ttu-id="b2467-174">Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b2467-174">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b2467-175">Importer des données dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b2467-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


