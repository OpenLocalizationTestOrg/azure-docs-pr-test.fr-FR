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
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a>Didacticiel NoSQL : Générer une application console Java avec l’API DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js pour MongoDB](mongodb-samples.md)
> * [Node.JS](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Didacticiel de NoSQL toohello Bienvenue pour hello API DocumentDB pour le Kit de développement Java Azure Cosmos DB ! À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB.

Le programme est le suivant :

* Création et connexion de compte de base de données Azure Cosmos tooan
* Configuration de votre solution Visual Studio
* Création d’une base de données en ligne
* Création d’une collection
* Création de documents JSON
* Interrogation de collection de hello
* Création de documents JSON
* Interrogation de collection de hello
* Remplacement d'un document
* Suppression d’un document
* Suppression de la base de données hello

Commençons dès maintenant !

## <a name="prerequisites"></a>Composants requis
Vérifiez que vous avez hello suivantes :

* Un compte Azure actif. Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/). Vous pouvez également utiliser hello [Azure Cosmos DB émulateur](local-emulator.md) pour ce didacticiel.
* [Git](https://git-scm.com/downloads)
* [Kit de développement logiciel Java (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Étape 1 : créer un compte Azure Cosmos DB
Commençons par créer un compte Azure Cosmos DB. Si vous avez déjà un compte que vous souhaitez toouse, vous pouvez passer trop[projet de Clone hello GitHub](#GitClone). Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) tooset jusqu'à l’émulateur de hello et passer trop[projet de Clone hello GitHub](#GitClone).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>Étape 2 : Cloner des projets de GitHub hello
Vous pouvez commencer par le clonage du référentiel GitHub de hello pour [prise en main Azure Cosmos DB et Java](https://github.com/Azure-Samples/documentdb-java-getting-started). Par exemple, à partir d’un répertoire local exécuter hello suivant tooretrieve hello exemple de projet localement.

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

Hello répertoire contient un `pom.xml` pour le projet de hello et un `src` dossier qui contient, y compris le code Java source `Program.java` qui indique comment effectuer des opérations simples avec la base de données Azure Cosmos telles que la création de documents et l’interrogation des données dans un collection. Hello `pom.xml` inclut une dépendance sur hello [DocumentDB Java SDK sur Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>Étape 3 : Relier le compte de base de données Azure Cosmos tooan
Ensuite, head sauvegarde toohello [Azure Portal](https://portal.azure.com) tooretrieve votre point de terminaison et la clé principale du principale. Hello point de terminaison de base de données Azure Cosmos et la clé primaire sont nécessaires pour votre application toounderstand où tooconnect et de base de données Azure Cosmos tootrust connexion de votre application.

Dans hello portail Azure, accédez de compte de base de données Azure Cosmos tooyour, puis cliquez sur **clés**. Copiez hello URI à partir du portail de hello, puis collez-la dans `https://FILLME.documents.azure.com` dans le fichier de Program.java hello. Copie hello clé primaire à partir du portail de hello et collez-la dans `FILLME`.

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Capture d’écran de hello portail Azure utilisée par hello toocreate de didacticiel NoSQL une application de console Java. Indique une base de données Azure Cosmos compte, avec un concentrateur actif de hello mis en surbrillance, hello bouton les clés de mise en surbrillance dans le panneau de compte de base de données Azure Cosmos hello et valeurs d’URI, clés primaires et secondaires hello mis en surbrillance sur hello Panneau de clés][keys]

## <a name="step-4-create-a-database"></a>Étape 4 : créer une base de données
Votre base de données Azure Cosmos [base de données](documentdb-resources.md#databases) peuvent être créés à l’aide de hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) méthode Hello **DocumentClient** classe. Une base de données est un conteneur logique de hello JSON de stockage de documents partitionné entre des collections.

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>Étape 5 : créer une collection
> [!WARNING]
> **createCollection** crée une collection avec un débit réservé, ce qui a des conséquences sur la tarification. Pour plus d’informations, consultez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

A [collection](documentdb-resources.md#collections) peuvent être créés à l’aide de hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) méthode Hello **DocumentClient** classe. Une collection est un conteneur de documents JSON. Elle est associée à une logique d'application JavaScript.


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>Étape 6 : Création de documents JSON
A [document](documentdb-resources.md#documents) peuvent être créés à l’aide de hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) méthode Hello **DocumentClient** classe. Les documents sont du contenu JSON (arbitraire) défini par l'utilisateur. Nous pouvons maintenant insérer un ou plusieurs documents. Si vous avez déjà des données que vous souhaitez toostore dans votre base de données, vous pouvez utiliser Azure Cosmos DB [l’outil de Migration de données](import-data.md) tooimport les données de salutation dans une base de données.

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

## <a id="Query"></a>Étape 7 : interroger les ressources Azure Cosmos DB
Azure Cosmos DB prend en charge les [requêtes](documentdb-sql-query.md) enrichies sur les documents JSON stockés dans chaque collection.  Hello suivant l’exemple de code montre comment tooquery décrit dans la base de données Azure Cosmos à l’aide de la syntaxe SQL hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) (méthode).

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>Étape 8 : remplacer le document JSON
Base de données Azure Cosmos prend en charge la mise à jour des documents JSON à l’aide de hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) (méthode).

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>Étape 9 : supprimer le document JSON
De même, base de données Azure Cosmos prend en charge la suppression de documents JSON à l’aide de hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) (méthode).  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>Étape 10 : Supprimer la base de données hello
Base de données de suppression hello créé supprime de la base de données hello et toutes les ressources enfants (collections, documents, etc.).

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>Étape 11 : exécuter votre application console C#
application de hello toorun à partir de la console hello, accédez à toohello le dossier de projet et de la compilation à l’aide de Maven :
    
    mvn package

En cours d’exécution `mvn package` télécharge la bibliothèque de base de données Azure Cosmos hello plus récente à partir de Maven et produit `GetStarted-0.0.1-SNAPSHOT.jar`. Puis exécutez l’application hello en exécutant :

    mvn exec:java -D exec.mainClass=GetStarted.Program

Félicitations ! Vous avez terminé ce didacticiel NoSQL et vous disposez d’une application console Java opérationnelle !

## <a name="next-steps"></a>Étapes suivantes
* Vous recherchez un didacticiel sur les applications web Java ? Consultez [Créer une application web Java avec Azure Cosmos DB](documentdb-java-application.md).
* Découvrez comment trop[surveiller un compte de base de données Azure Cosmos](monitor-accounts.md).
* Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).
* En savoir plus sur le modèle de programmation hello Bonjour section développer Hello [page de documentation de base de données Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
