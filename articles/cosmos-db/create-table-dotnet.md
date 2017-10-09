---
title: "une application Azure Cosmos DB .NET à l’aide d’aaaBuild hello API Table | Documents Microsoft"
description: "Débutez avec les API Tables d’Azure Cosmos DB à l’aide de .NET"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: bdd4f8ec45407962b3d2cb26aa814a20cfc62173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a>Azure Cosmos DB : Générer une application .NET à l’aide de hello API de Table

Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale. Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur. 

Ce démarrage rapide montre comment toocreate une base de données Azure Cosmos compte et créer une table dans ce compte à l’aide de hello portail Azure. Vous allez ensuite écrire le code tooinsert, mise à jour et supprimer des entités et exécuter des requêtes à l’aide de nouveau hello [Table Premium de Windows Azure Storage](https://aka.ms/premiumtablenuget) package (version préliminaire) de NuGet. Cette bibliothèque a hello mêmes classes et les signatures de méthode hello public [le stockage Windows Azure SDK](https://www.nuget.org/packages/WindowsAzure.Storage), mais a également les comptes hello capacité tooconnect tooAzure Cosmos DB à l’aide de hello [API Table](table-introduction.md) (version préliminaire). 

## <a name="prerequisites"></a>Composants requis

Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello **libre** [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Création d'un compte de base de données

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a>Ajouter une table

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a>Ajouter un exemple de données

Vous pouvez maintenant ajouter la nouvelle table données tooyour à l’aide de l’Explorateur de données (version préliminaire).

1. Dans l’Explorateur de données, développez **exemple de table**, cliquez sur **Entités**, puis cliquez sur **Ajouter une entité**.

   ![Créez de nouvelles entités dans l’Explorateur de données Bonjour portail Azure](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. Maintenant ajouter une zone de valeur de données toohello PartitionKey et de la zone de valeur de RowKey, puis cliquez sur **ajouter une entité**.

   ![Définir hello clé de Partition et clé de ligne pour une nouvelle entité](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    Vous pouvez maintenant ajouter une table de tooyour plusieurs entités, modifier vos entités ou interroger vos données dans l’Explorateur de données. Explorateur de données est également où vous pouvez faire évoluer votre débit et d’ajouter des procédures stockées, les fonctions définies par l’utilisateur et déclencheurs tooyour table.

## <a name="clone-hello-sample-application"></a>Exemple d’application hello de cloner

Maintenant nous allons cloner une application de la Table à partir de github, définissez la chaîne de connexion hello et exécutez-le. Vous allez voir combien il est facile toowork avec des données par programme. 

1. Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.  

2. Exécutez hello suivant le dépôt d’exemples de commande tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. Ouvrez ensuite le fichier de solution de hello dans Visual Studio. 

## <a name="review-hello-code"></a>Réviser le code hello

Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello. Fichier de Program.cs hello ouvert et que vous trouverez ces lignes de code créent hello des ressources de base de données Azure Cosmos. 

* Hello CloudTableClient est initialisé.

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* Une nouvelle table est créée si elle n’existe pas.

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* Un nouveau conteneur de table est créé. Vous remarquerez ce stockage de Table Azure SDK du code très similaire tooregular. 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a>Mise à jour de votre chaîne de connexion

Maintenant nous allons mettre à jour les informations de chaîne de connexion hello pour votre application peut communiquer avec tooAzure Cosmos DB. 

1. Dans Visual Studio, ouvrez le fichier app.config de hello. 

2. Bonjour [portail Azure](http://portal.azure.com/), Bonjour Azure Cosmos DB laissé le menu de navigation, cliquez sur **chaîne de connexion**. Puis cliquez sur bouton hello pour la chaîne de connexion hello dans le nouveau volet de hello. 

    ![Afficher et copier hello point de terminaison et la clé de compte dans le volet de chaîne de connexion hello](./media/create-table-dotnet/keys.png)

3. Collez les valeur hello dans le fichier app.config de hello en tant que valeur hello Hello PremiumStorageConnectionString. 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    Vous pouvez laisser hello StandardStorageConnectionString en l’état.

Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos. 

## <a name="run-hello-web-app"></a>Exécutez l’application hello web

1. Dans Visual Studio, cliquez sur hello **PremiumTableGetStarted** projet **l’Explorateur de solutions** puis cliquez sur **gérer les Packages NuGet**. 

2. Bonjour NuGet **Parcourir** , tapez *WindowsAzure.Storage-PremiumTable*.

3. Vérifiez hello **inclure la version préliminaire** boîte. 

4. À partir des résultats de hello, installez hello **WindowsAzure.Storage-PremiumTable** bibliothèque. Cette commande installe l’aperçu hello package de l’API de Table de base de données Azure Cosmos ainsi que toutes les dépendances. Notez qu’il s’agit d’un package NuGet différent que le package de stockage Windows Azure hello utilisée par le stockage de Table Azure. 

5. Cliquez sur CTRL + F5 application hello de toorun.

    fenêtre de console Hello affiche hello données ajouté, récupérés, interrogé, remplacés et supprimés à partir de la table de hello. Hello script terminé, appuyez sur n’importe quelle fenêtre de console hello tooclose clé. 
    
    ![Sortie de la console de démarrage rapide de hello](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. Si vous souhaitez toosee hello nouvelles entités dans l’Explorateur de données, seulement commentez les lignes 188-208 dans le fichier program.cs afin qu’ils ne sont pas supprimés, puis réexécutez exemple hello. 

    Vous pouvez maintenant revenir tooData Explorateur de solutions, cliquez sur **Actualiser**, développez hello **personnes** de table et cliquez sur **entités**, puis travailler avec ces nouvelles données. 

    ![Nouvelles entités dans l’Explorateur de données](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Passez en revue les SLA dans hello portail Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit : 

1. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé. 
2. Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer une table à l’aide de hello Explorateur de données et exécuter une application.  Maintenant, vous pouvez interroger vos données à l’aide de hello API de Table.  

> [!div class="nextstepaction"]
> [Requête à l’aide de hello API de Table](tutorial-query-table.md)

