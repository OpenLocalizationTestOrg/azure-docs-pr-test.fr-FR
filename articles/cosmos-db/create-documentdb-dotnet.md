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
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB : Génération d’une application de web API DocumentDB avec .NET et hello portail Azure

Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale. Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur. 

Ce démarrage rapide montre comment toocreate un compte de base de données Azure Cosmos, base de données du document et à l’aide de la collection hello portail Azure. Vous allez ensuite générer et déployer une application web de liste todo repose sur hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), comme indiqué dans hello suivant capture d’écran. 

![Application To-Do avec des exemples de données](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a>Composants requis

Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello **libre** [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Création d'un compte de base de données

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
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

     Vous pouvez maintenant utiliser des requêtes dans l’Explorateur de données tooretrieve vos données. Par défaut, l’Explorateur de données utilise `SELECT * FROM c` tooretrieve tous les documents dans la collection de hello, mais vous pouvez modifier ce tooa différents [requête SQL](documentdb-sql-query.md), tel que `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn tous les documents hello dans l’ordre décroissant en fonction de leur horodatage.
 
     Vous pouvez également utiliser les procédures de toocreate stockée Explorateur de données, UDF et déclencheurs tooperform ainsi la logique métier côté serveur en tant que le débit de l’échelle. Explorateur de données expose l’ensemble du hello intégrées par programmation l’accès aux données disponibles dans l’API de hello, mais il fournit des données un accès facile tooyour hello portail Azure.

## <a name="clone-hello-sample-application"></a>Exemple d’application hello de cloner

Maintenant nous allons passer tooworking avec le code. Nous allons cloner une application API DocumentDB à partir de GitHub, définissez la chaîne de connexion hello et exécutez-le. Vous allez voir combien il est facile toowork avec des données par programme. 

1. Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `CD` répertoire de travail tooa.  

2. Exécutez hello suivant le dépôt d’exemples de commande tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. Puis ouvrez le fichier de solution todo hello dans Visual Studio. 

## <a name="review-hello-code"></a>Réviser le code hello

Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello. Fichier de DocumentDBRepository.cs hello ouvert et que vous trouverez ces lignes de code créent hello des ressources de base de données Azure Cosmos. 

* Hello DocumentClient est initialisée sur la ligne 73.

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* Une nouvelle base de données est créée à la ligne 88.

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* Une nouvelle collection est créée à la ligne 107.

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a>Mise à jour de votre chaîne de connexion

Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.

1. Bonjour [portail Azure](http://portal.azure.com/), dans votre base de données de Cosmos Azure account, Bonjour barre de navigation gauche, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**. Vous allez utiliser les boutons de copier hello sur droite hello Hello de toocopy écran hello URI et la clé primaire dans le fichier web.config de hello dans l’étape suivante de hello.

    ![Afficher et copier une clé d’accès dans hello portail Azure, le panneau de clés](./media/create-documentdb-dotnet/keys.png)

2. Dans Visual Studio 2017, ouvrez le fichier web.config de hello. 

3. Copier la valeur de l’URI à partir du portail hello (à l’aide du bouton de copie hello) et le rendre hello la valeur de clé de point de terminaison hello dans le fichier web.config. 

    `<add key="endpoint" value="FILLME" />`

4. Copiez la valeur de clé primaire à partir du portail de hello, puis rendre hello valeur authKey hello dans le fichier web.config. Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos. 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a>Exécutez l’application hello web
1. Dans Visual Studio, cliquez sur projet hello dans **l’Explorateur de solutions** puis cliquez sur **gérer les Packages NuGet**. 

2. Bonjour NuGet **Parcourir** , tapez *DocumentDB*.

3. À partir des résultats de hello, installez hello **Microsoft.Azure.DocumentDB** bibliothèque. Cela installe le package de Microsoft.Azure.DocumentDB hello, ainsi que toutes les dépendances.

4. Cliquez sur CTRL + F5 application hello de toorun. Votre application s’affiche dans votre navigateur. 

5. Cliquez sur **créer un nouveau** hello navigateur et créer quelques nouvelles tâches dans votre application de l’action.

   ![Application To-Do avec des exemples de données](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

Vous pouvez maintenant revenir en arrière tooData Explorer et consultez la requête, modifier et travailler avec ces nouvelles données. 

## <a name="review-slas-in-hello-azure-portal"></a>Passez en revue les SLA dans hello portail Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :

1. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé. 
2. Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer une collection à l’aide de hello Explorateur de données et exécuter une application web. Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires. 

> [!div class="nextstepaction"]
> [Importer des données dans Azure Cosmos DB](import-data.md)


