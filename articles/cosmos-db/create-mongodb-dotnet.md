---
title: "Azure Cosmos DB : Génération d’une application web avec .NET et hello MongoDB API | Documents Microsoft"
description: "Présente un exemple de code .NET que vous pouvez utiliser la requête de tooand tooconnect hello Azure Cosmos DB MongoDB API"
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
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="48923-103">Azure Cosmos DB : Génération d’une application web de MongoDB API avec .NET et hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="48923-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="48923-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="48923-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="48923-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="48923-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="48923-106">Ce démarrage rapide montre comment toocreate un compte de base de données Azure Cosmos, base de données du document et à l’aide de la collection hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="48923-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="48923-107">Vous allez ensuite créer et déployer une application web de liste de tâches basée sur hello [pilote MongoDB .NET](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="48923-107">You'll then build and deploy a tasks list web app built on hello [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="48923-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="48923-108">Prerequisites</span></span>

<span data-ttu-id="48923-109">Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello **libre** [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="48923-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="48923-110">Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="48923-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="48923-111">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="48923-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="48923-112">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="48923-112">Clone hello sample application</span></span>

<span data-ttu-id="48923-113">Maintenant, nous allons une API MongoDB le clonage d’application à partir de github, définir la chaîne de connexion hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="48923-113">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="48923-114">Vous allez voir combien il est facile toowork avec des données par programme.</span><span class="sxs-lookup"><span data-stu-id="48923-114">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="48923-115">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="48923-115">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="48923-116">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="48923-116">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="48923-117">Ouvrez ensuite le fichier de solution de hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="48923-117">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="48923-118">Réviser le code hello</span><span class="sxs-lookup"><span data-stu-id="48923-118">Review hello code</span></span>

<span data-ttu-id="48923-119">Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="48923-119">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="48923-120">Ouvrez hello **Dal.cs** fichier sous hello **DAL** active et que vous trouverez ces lignes de code créent hello des ressources de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="48923-120">Open hello **Dal.cs** file under hello **DAL** directory and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="48923-121">Initialiser hello Mongo Client.</span><span class="sxs-lookup"><span data-stu-id="48923-121">Initialize hello Mongo Client.</span></span>

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

* <span data-ttu-id="48923-122">Récupérer la base de données hello et collection de hello.</span><span class="sxs-lookup"><span data-stu-id="48923-122">Retrieve hello database and hello collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="48923-123">Récupérez tous les documents.</span><span class="sxs-lookup"><span data-stu-id="48923-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="48923-124">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="48923-124">Update your connection string</span></span>

<span data-ttu-id="48923-125">Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="48923-125">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="48923-126">Bonjour [portail Azure](http://portal.azure.com/), dans votre base de données de Cosmos Azure account, Bonjour barre de navigation gauche, cliquez sur **chaîne de connexion**, puis cliquez sur **en lecture-écriture clés**.</span><span class="sxs-lookup"><span data-stu-id="48923-126">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="48923-127">Vous allez utiliser l’hôte hello copie sur boutons hello côté droit de hello de toocopy écran hello nom d’utilisateur et mot de passe dans fichier de Dal.cs hello dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="48923-127">You'll use hello copy buttons on hello right side of hello screen toocopy hello Username, Password, and Host into hello Dal.cs file in hello next step.</span></span>

2. <span data-ttu-id="48923-128">Ouvrez hello **Dal.cs** fichier Bonjour **DAL** active.</span><span class="sxs-lookup"><span data-stu-id="48923-128">Open hello **Dal.cs** file in hello **DAL** directory.</span></span> 

3. <span data-ttu-id="48923-129">Copiez votre **nom d’utilisateur** à partir du portail hello (à l’aide du bouton de copie hello) et le rendre hello valeur Hello **nom d’utilisateur** dans votre **Dal.cs** fichier.</span><span class="sxs-lookup"><span data-stu-id="48923-129">Copy your **username** value from hello portal (using hello copy button) and make it hello value of hello **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="48923-130">Copiez votre **hôte** à partir du portail de hello et le rendre hello valeur Hello **hôte** dans votre **Dal.cs** fichier.</span><span class="sxs-lookup"><span data-stu-id="48923-130">Then copy your **host** value from hello portal and make it hello value of hello **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="48923-131">Pour finir copiez votre **mot de passe** à partir du portail de hello et le rendre hello valeur Hello **mot de passe** dans votre **Dal.cs** fichier.</span><span class="sxs-lookup"><span data-stu-id="48923-131">Finally copy your **password** value from hello portal and make it hello value of hello **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="48923-132">Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="48923-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-web-app"></a><span data-ttu-id="48923-133">Exécutez l’application hello web</span><span class="sxs-lookup"><span data-stu-id="48923-133">Run hello web app</span></span>

1. <span data-ttu-id="48923-134">Dans Visual Studio, cliquez sur projet hello dans **l’Explorateur de solutions** puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="48923-134">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="48923-135">Bonjour NuGet **Parcourir** , tapez *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="48923-135">In hello NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="48923-136">À partir des résultats de hello, installez hello **MongoDB.Driver** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="48923-136">From hello results, install hello **MongoDB.Driver** library.</span></span> <span data-ttu-id="48923-137">Cela installe le package de MongoDB.Driver hello, ainsi que toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="48923-137">This installs hello MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="48923-138">Cliquez sur CTRL + F5 application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="48923-138">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="48923-139">Votre application s’affiche dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="48923-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="48923-140">Cliquez sur **créer** hello navigateur et créer quelques nouvelles tâches dans votre application de liste de tâches.</span><span class="sxs-lookup"><span data-stu-id="48923-140">Click **Create** in hello browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="48923-141">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="48923-141">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="48923-142">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="48923-142">Clean up resources</span></span>

<span data-ttu-id="48923-143">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="48923-143">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="48923-144">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="48923-144">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="48923-145">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="48923-145">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48923-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48923-146">Next steps</span></span>

<span data-ttu-id="48923-147">Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos et exécuter une application web à l’aide hello API pour MongoDB.</span><span class="sxs-lookup"><span data-stu-id="48923-147">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a web app using hello API for MongoDB.</span></span> <span data-ttu-id="48923-148">Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="48923-148">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="48923-149">Importer des données dans la base de données Azure Cosmos pour hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="48923-149">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

