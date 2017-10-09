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
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a><span data-ttu-id="80f6f-103">Azure Cosmos DB : Générer une application .NET à l’aide de hello API de Table</span><span class="sxs-lookup"><span data-stu-id="80f6f-103">Azure Cosmos DB: Build a .NET application using hello Table API</span></span>

<span data-ttu-id="80f6f-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="80f6f-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="80f6f-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="80f6f-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="80f6f-106">Ce démarrage rapide montre comment toocreate une base de données Azure Cosmos compte et créer une table dans ce compte à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="80f6f-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, and create a table within that account using hello Azure portal.</span></span> <span data-ttu-id="80f6f-107">Vous allez ensuite écrire le code tooinsert, mise à jour et supprimer des entités et exécuter des requêtes à l’aide de nouveau hello [Table Premium de Windows Azure Storage](https://aka.ms/premiumtablenuget) package (version préliminaire) de NuGet.</span><span class="sxs-lookup"><span data-stu-id="80f6f-107">You'll then write code tooinsert, update, and delete entities, and run some queries using hello new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="80f6f-108">Cette bibliothèque a hello mêmes classes et les signatures de méthode hello public [le stockage Windows Azure SDK](https://www.nuget.org/packages/WindowsAzure.Storage), mais a également les comptes hello capacité tooconnect tooAzure Cosmos DB à l’aide de hello [API Table](table-introduction.md) (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="80f6f-108">This library has hello same classes and method signatures as hello public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has hello ability tooconnect tooAzure Cosmos DB accounts using hello [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="80f6f-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="80f6f-109">Prerequisites</span></span>

<span data-ttu-id="80f6f-110">Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello **libre** [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="80f6f-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="80f6f-111">Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="80f6f-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="80f6f-112">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="80f6f-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="80f6f-113">Ajouter une table</span><span class="sxs-lookup"><span data-stu-id="80f6f-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="80f6f-114">Ajouter un exemple de données</span><span class="sxs-lookup"><span data-stu-id="80f6f-114">Add sample data</span></span>

<span data-ttu-id="80f6f-115">Vous pouvez maintenant ajouter la nouvelle table données tooyour à l’aide de l’Explorateur de données (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="80f6f-115">You can now add data tooyour new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="80f6f-116">Dans l’Explorateur de données, développez **exemple de table**, cliquez sur **Entités**, puis cliquez sur **Ajouter une entité**.</span><span class="sxs-lookup"><span data-stu-id="80f6f-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Créez de nouvelles entités dans l’Explorateur de données Bonjour portail Azure](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="80f6f-118">Maintenant ajouter une zone de valeur de données toohello PartitionKey et de la zone de valeur de RowKey, puis cliquez sur **ajouter une entité**.</span><span class="sxs-lookup"><span data-stu-id="80f6f-118">Now add data toohello PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![Définir hello clé de Partition et clé de ligne pour une nouvelle entité](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="80f6f-120">Vous pouvez maintenant ajouter une table de tooyour plusieurs entités, modifier vos entités ou interroger vos données dans l’Explorateur de données.</span><span class="sxs-lookup"><span data-stu-id="80f6f-120">You can now add more entities tooyour table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="80f6f-121">Explorateur de données est également où vous pouvez faire évoluer votre débit et d’ajouter des procédures stockées, les fonctions définies par l’utilisateur et déclencheurs tooyour table.</span><span class="sxs-lookup"><span data-stu-id="80f6f-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers tooyour table.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="80f6f-122">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="80f6f-122">Clone hello sample application</span></span>

<span data-ttu-id="80f6f-123">Maintenant nous allons cloner une application de la Table à partir de github, définissez la chaîne de connexion hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="80f6f-123">Now let's clone a Table app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="80f6f-124">Vous allez voir combien il est facile toowork avec des données par programme.</span><span class="sxs-lookup"><span data-stu-id="80f6f-124">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="80f6f-125">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="80f6f-125">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="80f6f-126">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="80f6f-126">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="80f6f-127">Ouvrez ensuite le fichier de solution de hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80f6f-127">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="80f6f-128">Réviser le code hello</span><span class="sxs-lookup"><span data-stu-id="80f6f-128">Review hello code</span></span>

<span data-ttu-id="80f6f-129">Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="80f6f-129">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="80f6f-130">Fichier de Program.cs hello ouvert et que vous trouverez ces lignes de code créent hello des ressources de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="80f6f-130">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="80f6f-131">Hello CloudTableClient est initialisé.</span><span class="sxs-lookup"><span data-stu-id="80f6f-131">hello CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="80f6f-132">Une nouvelle table est créée si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="80f6f-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="80f6f-133">Un nouveau conteneur de table est créé.</span><span class="sxs-lookup"><span data-stu-id="80f6f-133">A new Table container is created.</span></span> <span data-ttu-id="80f6f-134">Vous remarquerez ce stockage de Table Azure SDK du code très similaire tooregular.</span><span class="sxs-lookup"><span data-stu-id="80f6f-134">You will notice this code very similar tooregular Azure Table storage SDK.</span></span> 

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

## <a name="update-your-connection-string"></a><span data-ttu-id="80f6f-135">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="80f6f-135">Update your connection string</span></span>

<span data-ttu-id="80f6f-136">Maintenant nous allons mettre à jour les informations de chaîne de connexion hello pour votre application peut communiquer avec tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80f6f-136">Now we'll update hello connection string information so your app can talk tooAzure Cosmos DB.</span></span> 

1. <span data-ttu-id="80f6f-137">Dans Visual Studio, ouvrez le fichier app.config de hello.</span><span class="sxs-lookup"><span data-stu-id="80f6f-137">In Visual Studio, open hello app.config file.</span></span> 

2. <span data-ttu-id="80f6f-138">Bonjour [portail Azure](http://portal.azure.com/), Bonjour Azure Cosmos DB laissé le menu de navigation, cliquez sur **chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="80f6f-138">In hello [Azure portal](http://portal.azure.com/), in hello Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="80f6f-139">Puis cliquez sur bouton hello pour la chaîne de connexion hello dans le nouveau volet de hello.</span><span class="sxs-lookup"><span data-stu-id="80f6f-139">Then in hello new pane click hello copy button for hello connection string.</span></span> 

    ![Afficher et copier hello point de terminaison et la clé de compte dans le volet de chaîne de connexion hello](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="80f6f-141">Collez les valeur hello dans le fichier app.config de hello en tant que valeur hello Hello PremiumStorageConnectionString.</span><span class="sxs-lookup"><span data-stu-id="80f6f-141">Paste hello value into hello app.config file as hello value of hello PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="80f6f-142">Vous pouvez laisser hello StandardStorageConnectionString en l’état.</span><span class="sxs-lookup"><span data-stu-id="80f6f-142">You can leave hello StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="80f6f-143">Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="80f6f-143">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-web-app"></a><span data-ttu-id="80f6f-144">Exécutez l’application hello web</span><span class="sxs-lookup"><span data-stu-id="80f6f-144">Run hello web app</span></span>

1. <span data-ttu-id="80f6f-145">Dans Visual Studio, cliquez sur hello **PremiumTableGetStarted** projet **l’Explorateur de solutions** puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="80f6f-145">In Visual Studio, right-click on hello **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="80f6f-146">Bonjour NuGet **Parcourir** , tapez *WindowsAzure.Storage-PremiumTable*.</span><span class="sxs-lookup"><span data-stu-id="80f6f-146">In hello NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="80f6f-147">Vérifiez hello **inclure la version préliminaire** boîte.</span><span class="sxs-lookup"><span data-stu-id="80f6f-147">Check hello **Include prerelease** box.</span></span> 

4. <span data-ttu-id="80f6f-148">À partir des résultats de hello, installez hello **WindowsAzure.Storage-PremiumTable** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="80f6f-148">From hello results, install hello **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="80f6f-149">Cette commande installe l’aperçu hello package de l’API de Table de base de données Azure Cosmos ainsi que toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="80f6f-149">This installs hello preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="80f6f-150">Notez qu’il s’agit d’un package NuGet différent que le package de stockage Windows Azure hello utilisée par le stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="80f6f-150">Note that this is a different NuGet package than hello Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="80f6f-151">Cliquez sur CTRL + F5 application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="80f6f-151">Click CTRL + F5 toorun hello application.</span></span>

    <span data-ttu-id="80f6f-152">fenêtre de console Hello affiche hello données ajouté, récupérés, interrogé, remplacés et supprimés à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="80f6f-152">hello console window displays hello data being added, retrieved, queried, replaced and deleted from hello table.</span></span> <span data-ttu-id="80f6f-153">Hello script terminé, appuyez sur n’importe quelle fenêtre de console hello tooclose clé.</span><span class="sxs-lookup"><span data-stu-id="80f6f-153">When hello script completes, press any key tooclose hello console window.</span></span> 
    
    ![Sortie de la console de démarrage rapide de hello](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="80f6f-155">Si vous souhaitez toosee hello nouvelles entités dans l’Explorateur de données, seulement commentez les lignes 188-208 dans le fichier program.cs afin qu’ils ne sont pas supprimés, puis réexécutez exemple hello.</span><span class="sxs-lookup"><span data-stu-id="80f6f-155">If you want toosee hello new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run hello sample again.</span></span> 

    <span data-ttu-id="80f6f-156">Vous pouvez maintenant revenir tooData Explorateur de solutions, cliquez sur **Actualiser**, développez hello **personnes** de table et cliquez sur **entités**, puis travailler avec ces nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="80f6f-156">You can now go back tooData Explorer, click **Refresh**, expand hello **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![Nouvelles entités dans l’Explorateur de données](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="80f6f-158">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="80f6f-158">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="80f6f-159">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="80f6f-159">Clean up resources</span></span>

<span data-ttu-id="80f6f-160">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="80f6f-160">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="80f6f-161">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="80f6f-161">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="80f6f-162">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="80f6f-162">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80f6f-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80f6f-163">Next steps</span></span>

<span data-ttu-id="80f6f-164">Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer une table à l’aide de hello Explorateur de données et exécuter une application.</span><span class="sxs-lookup"><span data-stu-id="80f6f-164">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a table using hello Data Explorer, and run an app.</span></span>  <span data-ttu-id="80f6f-165">Maintenant, vous pouvez interroger vos données à l’aide de hello API de Table.</span><span class="sxs-lookup"><span data-stu-id="80f6f-165">Now you can query your data using hello Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="80f6f-166">Requête à l’aide de hello API de Table</span><span class="sxs-lookup"><span data-stu-id="80f6f-166">Query using hello Table API</span></span>](tutorial-query-table.md)

