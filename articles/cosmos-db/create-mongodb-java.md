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
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a>Azure Cosmos DB : Génération d’une application de console MongoDB API avec Java et hello portail Azure

Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale. Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur. 

Ce démarrage rapide montre comment toocreate un compte de base de données Azure Cosmos, base de données du document et à l’aide de la collection hello portail Azure. Vous allez ensuite générer et déployer une application de console basée sur hello [pilote MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/). 

## <a name="prerequisites"></a>Composants requis

* Avant de pouvoir exécuter cet exemple, vous devez disposer de hello suivant des conditions préalables :
   * JDK 1.7 + (exécutez `apt-get install default-jdk` si vous ne possédez pas JDK)
   * Maven (exécutez `apt-get install maven` si vous ne possédez pas Maven)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Création d'un compte de base de données

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a>Ajouter une collection

Nommez votre nouvelle base de données, **db**, et votre nouvelle collection, **coll**.

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Exemple d’application hello de cloner

Maintenant, nous allons une API MongoDB le clonage d’application à partir de github, définir la chaîne de connexion hello et exécutez-le. Vous allez voir combien il est facile toowork avec des données par programme. 

1. Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.  

2. Exécutez hello suivant le dépôt d’exemples de commande tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. Ouvrez ensuite le fichier de solution de hello dans Visual Studio. 

## <a name="review-hello-code"></a>Réviser le code hello

Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello. Ouvrez hello `Program.cs` fichier et que vous trouverez ces lignes de code créent hello des ressources de base de données Azure Cosmos. 

* Hello DocumentClient est initialisé.

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* Une base de données et une collection ont été créées.

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* Certains documents sont intégrés à l’aide de `MongoCollection.insertOne`

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* Certaines requêtes sont effectuées à l’aide de `MongoCollection.find`

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a>Mise à jour de votre chaîne de connexion

Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.

1. À partir de hello compte, sélectionnez **Quick Start**, sélectionnez Java, puis copiez le Presse-papiers de tooyour de chaîne de connexion hello

2. Ouvrez hello `Program.java` fichier, remplacer le constructeur de hello argument toohello MongoClientURI avec la chaîne de connexion hello. Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos. 
    
## <a name="run-hello-console-app"></a>Exécutez l’application de console hello

1. Exécutez `mvn package` dans un terminal tooinstall requis des modules npm

2. Exécutez `mvn exec:java -D exec.mainClass=GetStarted.Program` dans un terminal toostart votre application Java.

Vous pouvez maintenant utiliser [Robomongo](mongodb-robomongo.md) / [Studio 3P](mongodb-mongochef.md) tooquery, modifier et travailler avec ces nouvelles données.

## <a name="review-slas-in-hello-azure-portal"></a>Passez en revue les SLA dans hello portail Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :

1. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé. 
2. Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer une collection à l’aide de hello Explorateur de données et exécuter une application console. Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires. 

> [!div class="nextstepaction"]
> [Importer des données MongoDB dans Azure Cosmos DB](mongodb-migrate.md)


