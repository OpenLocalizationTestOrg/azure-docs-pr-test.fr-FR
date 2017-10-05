---
title: "Azure Cosmos DB : Développer une application web avec .NET et l’API MongoDB | Microsoft Docs"
description: "Cet article présente un exemple de code .NET que vous pouvez utiliser pour vous connecter à l’API MongoDB d’Azure Cosmos DB, et pour l’interroger"
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
ms.openlocfilehash: 2d30bec75d701b1fd55355d1e139350b6d828c9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="a16da-103">Azure Cosmos DB : Développer une application web API MongoDB avec .NET et le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="a16da-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="a16da-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="a16da-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="a16da-105">Rapidement, vous avez la possibilité de créer et d’interroger des documents, des paires clé/valeur, et des bases de données orientées graphe, profitant tous de la distribution à l’échelle mondiale et des capacités de mise à l’échelle horizontale au cœur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a16da-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="a16da-106">Ce guide de démarrage rapide explique comment créer, à l’aide du Portail Azure, un compte Azure Cosmos DB , une base de données de documents, ainsi qu’une collection.</span><span class="sxs-lookup"><span data-stu-id="a16da-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="a16da-107">Vous allez ensuite créer et déployer une application web de liste des tâches basée sur le [pilote .NET MongoDB](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="a16da-107">You'll then build and deploy a tasks list web app built on the [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a16da-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a16da-108">Prerequisites</span></span>

<span data-ttu-id="a16da-109">Si vous n’avez pas encore installé Visual Studio 2017, vous pouvez télécharger et utiliser la version **gratuite** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a16da-109">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="a16da-110">Veillez à activer **le développement Azure** lors de l’installation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a16da-110">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="a16da-111">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="a16da-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="a16da-112">Clonage de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="a16da-112">Clone the sample application</span></span>

<span data-ttu-id="a16da-113">À présent, nous allons cloner une application API MongoDB à partir de GitHub, configurer la chaîne de connexion, et l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="a16da-113">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="a16da-114">Vous verrez combien il est facile de travailler par programmation avec des données.</span><span class="sxs-lookup"><span data-stu-id="a16da-114">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="a16da-115">Ouvrez une fenêtre de terminal git, comme git bash, et accédez à un répertoire de travail à l’aide de la commande `cd`.</span><span class="sxs-lookup"><span data-stu-id="a16da-115">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="a16da-116">Exécutez la commande suivante pour cloner l’exemple de référentiel.</span><span class="sxs-lookup"><span data-stu-id="a16da-116">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="a16da-117">Ouvrez le fichier de solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a16da-117">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="a16da-118">Examiner le code</span><span class="sxs-lookup"><span data-stu-id="a16da-118">Review the code</span></span>

<span data-ttu-id="a16da-119">Passons rapidement en revue ce qui se passe dans l’application.</span><span class="sxs-lookup"><span data-stu-id="a16da-119">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="a16da-120">Ouvrez le fichier **Dal.cs** dans le répertoire **DAL**, et vous découvrirez que ces lignes de code créent les ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a16da-120">Open the **Dal.cs** file under the **DAL** directory and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="a16da-121">Initialisez le client Mongo.</span><span class="sxs-lookup"><span data-stu-id="a16da-121">Initialize the Mongo Client.</span></span>

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* <span data-ttu-id="a16da-122">Récupérez la base de données et la collection.</span><span class="sxs-lookup"><span data-stu-id="a16da-122">Retrieve the database and the collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="a16da-123">Récupérez tous les documents.</span><span class="sxs-lookup"><span data-stu-id="a16da-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="a16da-124">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="a16da-124">Update your connection string</span></span>

<span data-ttu-id="a16da-125">Maintenant, retournez dans le portail Azure afin d’obtenir les informations de votre chaîne de connexion et de les copier dans l’application.</span><span class="sxs-lookup"><span data-stu-id="a16da-125">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="a16da-126">Dans le [portail Azure](http://portal.azure.com/), dans votre compte Azure Cosmos DB, dans le volet de navigation de gauche, cliquez sur **Chaîne de connexion**, puis sur **Clés en lecture-écriture**.</span><span class="sxs-lookup"><span data-stu-id="a16da-126">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="a16da-127">Vous utiliserez le bouton Copier sur le côté droit de l’écran pour copier le nom d’utilisateur, le mot de passe et l’hôte dans le fichier Dal.cs à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="a16da-127">You'll use the copy buttons on the right side of the screen to copy the Username, Password, and Host into the Dal.cs file in the next step.</span></span>

2. <span data-ttu-id="a16da-128">Ouvrez le fichier **Dal.cs** dans le répertoire **DAL**.</span><span class="sxs-lookup"><span data-stu-id="a16da-128">Open the **Dal.cs** file in the **DAL** directory.</span></span> 

3. <span data-ttu-id="a16da-129">Copiez votre valeur **nom d’utilisateur** à partir du portail (à l’aide du bouton Copier) et définissez-la comme valeur de **nom d’utilisateur** dans le fichier **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="a16da-129">Copy your **username** value from the portal (using the copy button) and make it the value of the **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="a16da-130">Puis, copiez votre valeur **hôte** à partir du portail et définissez-la comme valeur **hôte** dans votre fichier **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="a16da-130">Then copy your **host** value from the portal and make it the value of the **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="a16da-131">Puis, copiez votre valeur **mot de passe** à partir du portail et définissez-la comme valeur **mot de passe** dans votre fichier **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="a16da-131">Finally copy your **password** value from the portal and make it the value of the **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="a16da-132">Vous venez de mettre à jour votre application avec toutes les informations nécessaires pour communiquer avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a16da-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-web-app"></a><span data-ttu-id="a16da-133">Exécuter l’application web</span><span class="sxs-lookup"><span data-stu-id="a16da-133">Run the web app</span></span>

1. <span data-ttu-id="a16da-134">Dans Visual Studio, cliquez avec le bouton droit sur le nom du projet dans l’**Explorateur de solutions**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a16da-134">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="a16da-135">Dans la zone **Parcourir**de NuGet, tapez *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="a16da-135">In the NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="a16da-136">À partir des résultats, installez la bibliothèque **MongoDB.Driver**.</span><span class="sxs-lookup"><span data-stu-id="a16da-136">From the results, install the **MongoDB.Driver** library.</span></span> <span data-ttu-id="a16da-137">Cette opération permet d’installer le package MondoDB.Driver ainsi que toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="a16da-137">This installs the MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="a16da-138">Appuyez sur Ctrl + F5 pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="a16da-138">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="a16da-139">Votre application s’affiche dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="a16da-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="a16da-140">Cliquez sur **Créer** dans le navigateur et créez quelques tâches dans votre application de liste des tâches.</span><span class="sxs-lookup"><span data-stu-id="a16da-140">Click **Create** in the browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="a16da-141">Examen des SLA dans le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="a16da-141">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="a16da-142">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="a16da-142">Clean up resources</span></span>

<span data-ttu-id="a16da-143">Si vous ne pensez pas continuer à utiliser cette application, supprimez toutes les ressources créées durant ce guide de démarrage rapide dans le Portail Azure en procédant de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="a16da-143">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="a16da-144">Dans le menu de gauche du portail Azure, cliquez sur **Groupes de ressources**, puis sur le nom de la ressource que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="a16da-144">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="a16da-145">Dans la page de votre groupe de ressources, cliquez sur **Supprimer**, tapez le nom de la ressource à supprimer dans la zone de texte, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="a16da-145">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a16da-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a16da-146">Next steps</span></span>

<span data-ttu-id="a16da-147">Dans ce guide de démarrage rapide, vous avez appris à créer un compte Azure Cosmos DB et à exécuter une application web à l’aide de l’API de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a16da-147">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a web app using the API for MongoDB.</span></span> <span data-ttu-id="a16da-148">Vous pouvez maintenant importer des données supplémentaires dans votre compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a16da-148">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="a16da-149">Importer des données dans Azure Cosmos DB pour l’API MongoDB</span><span class="sxs-lookup"><span data-stu-id="a16da-149">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)

