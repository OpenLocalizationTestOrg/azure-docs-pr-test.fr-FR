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
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a>Base de données Cosmos Azure : Créer une base de données de document à l’aide de Java et hello portail Azure

Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale. Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur. 

Ce démarrage rapide crée un document à l’aide de la base de données hello outils portails Azure pour la base de données Azure Cosmos. Ce démarrage rapide montre comment tooquickly créer une application de console Java à l’aide de hello [DocumentDB Java API](documentdb-sdk-java.md). instructions Hello dans ce démarrage rapide peuvent être suivies sur n’importe quel système d’exploitation qui est capable d’exécuter Java. En effectuant ce démarrage rapide, vous serez familiarisé avec la création et la modification des ressources de base de données de document dans soit hello l’interface utilisateur ou par programme, selon votre préférence.

## <a name="prerequisites"></a>Composants requis

* [Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * Sur Ubuntu, exécutez `apt-get install default-jdk` tooinstall hello JDK.
    * Être tooset vraiment hello JAVA_HOME variable toopoint toohello dossier d’environnement sur lequel hello JDK est installé.
* [Téléchargement](http://maven.apache.org/download.cgi) et [installation](http://maven.apache.org/install.html) d’une archive binaire [Maven](http://maven.apache.org/)
    * Sur Ubuntu, vous pouvez exécuter `apt-get install maven` tooinstall Maven.
* [Git](https://www.git-scm.com/)
    * Sur Ubuntu, vous pouvez exécuter `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Création d'un compte de base de données

Avant de pouvoir créer une base de données de document, vous devez toocreate un compte de base de données SQL (DocumentDB) avec la base de données Azure Cosmos.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Ajouter une collection

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Ajouter un exemple de données

Vous pouvez maintenant ajouter la nouvelle collection données tooyour à l’aide de l’Explorateur de données.

1. Dans l’Explorateur de données, la nouvelle base de données hello s’affiche dans le volet de Collections hello. Développez hello **tâches** de base de données, développez hello **éléments** collection, cliquez sur **Documents**, puis cliquez sur **nouveaux Documents**. 

   ![Créer des documents dans l’Explorateur de données Bonjour portail Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Maintenant ajouter une collection de toohello document avec hello suivant la structure.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. Une fois que vous avez ajouté hello json toohello **Documents** , cliquez sur **enregistrer**.

    ![Copier des données json et cliquez sur Enregistrer dans l’Explorateur de données Bonjour portail Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Créer et enregistrer un document plus où vous insérez une valeur unique pour hello `id` propriété et la modification hello autres propriétés comme vous le souhaitez. Vos nouveaux documents peuvent avoir la structure de votre choix car Azure Cosmos DB n’impose aucun schéma pour vos données.

     Vous pouvez maintenant utiliser des requêtes dans l’Explorateur de données tooretrieve vos données en cliquant sur hello **modifier le filtre** et **appliquer le filtre** boutons. Par défaut, l’Explorateur de données utilise `SELECT * FROM c` tooretrieve tous les documents dans la collection de hello, mais vous pouvez modifier ce tooa différents [requête SQL](documentdb-sql-query.md), tel que `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn tous les documents hello dans l’ordre décroissant en fonction de leur horodatage. 
 
     Vous pouvez également utiliser les procédures de toocreate stockée Explorateur de données, UDF et déclencheurs tooperform ainsi la logique métier côté serveur en tant que le débit de l’échelle. Explorateur de données expose l’ensemble du hello intégrées par programmation l’accès aux données disponibles dans l’API de hello, mais il fournit des données un accès facile tooyour hello portail Azure.

## <a name="clone-hello-sample-application"></a>Exemple d’application hello de cloner

Maintenant nous allons passer tooworking avec le code. Nous allons cloner une application API DocumentDB à partir de GitHub, définissez la chaîne de connexion hello et exécutez-le. Vous voyez combien il est facile toowork avec des données par programme. 

1. Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `CD` répertoire de travail tooa.  

2. Exécutez hello suivant le dépôt d’exemples de commande tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Réviser le code hello

Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello. Ouvrez hello `Program.java` de fichiers à partir du dossier \src\GetStarted hello et recherchez ces lignes de code qui créent des ressources de base de données Azure Cosmos hello. 

* Hello `DocumentClient` est initialisé.

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* Une nouvelle base de données est créée.

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* Une nouvelle collection est créée.

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* Certains documents sont créés.

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* Une requête SQL sur JSON est effectuée.

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

## <a name="update-your-connection-string"></a>Mise à jour de votre chaîne de connexion

Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello. Cette opération activera toocommunicate de votre application avec votre base de données hébergée.

1. Bonjour [portail Azure](http://portal.azure.com/), dans votre base de données de Cosmos Azure account, Bonjour barre de navigation gauche, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**. Vous allez utiliser les boutons de copier hello sur droite hello Hello de toocopy écran hello URI et la clé primaire dans hello `Program.java` fichier à l’étape suivante de hello.

    ![Afficher et copier une clé d’accès dans hello portail Azure, le panneau de clés](./media/create-documentdb-dotnet/keys.png)

2. Bonjour ouvrir `Program.java` de fichiers, copiez votre valeur d’URI à partir du portail hello (à l’aide du bouton de copie hello) et le rendre hello valeur de hello point de terminaison toohello DocumentClient constructeur dans `Program.java`. 

    `"https://FILLME.documents.azure.com"`

4. Copiez la valeur de clé primaire à partir du portail de hello, puis collez-la sur « FILLME », ce qui hello second paramètre de constructeur de DocumentClient hello. Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos. 
    
## <a name="run-hello-app"></a>Exécutez l’application hello

1. Dans la fenêtre de terminal git hello, `cd` dossier azure-cosmos-db-documentdb-java-getting-started de toohello.

2. Dans la fenêtre de terminal git hello, tapez `mvn package` tooinstall hello requis packages Java.

3. Dans la fenêtre de terminal git hello, exécutez `mvn exec:java -D exec.mainClass=GetStarted.Program` dans hello toostart de la fenêtre de terminal de votre application Java.

    Dans la fenêtre de terminal hello, vous recevrez une notification qui hello FamilyDB base de données a été créée et toopress une clé toocontinue. Appuyez sur une base de données de clé toocreate hello, puis basculez toohello Explorateur de données, et vous verrez qu’il contient maintenant une base de données FamilyDB. Continuer toopress clés toocreate hello hello et la collection documents, puis effectuez une requête. Lorsque le projet de hello est terminée, les ressources hello sont supprimés de votre compte. 

    ![Afficher et copier une clé d’accès dans hello portail Azure, le panneau de clés](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a>Passez en revue les SLA dans hello portail Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :

1. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé. 
2. Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Dans ce démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, base de données du document et la collection à l’aide de hello Explorateur de données et exécuter une application toodo hello même chose par programme. Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires. 

> [!div class="nextstepaction"]
> [Importer des données dans Azure Cosmos DB](import-data.md)


