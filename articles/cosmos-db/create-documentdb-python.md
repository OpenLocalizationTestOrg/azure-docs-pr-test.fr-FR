---
title: "Azure Cosmos DB : Créer une application avec Python et l’API DocumentDB | Microsoft Docs"
description: "Cet article présente un exemple de code Python que vous pouvez utiliser pour vous connecter à l’API DocumentDB d’Azure Cosmos DB et pour l’interroger."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: 08d467ea27484e7d1d07d6c21b2e04b6525fbcd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-the-azure-portal"></a><span data-ttu-id="782e5-103">Azure Cosmos DB : Développer une application API DocumentDB grâce à Python et au Portail Azure</span><span class="sxs-lookup"><span data-stu-id="782e5-103">Azure Cosmos DB: Build a DocumentDB API app with Python and the Azure portal</span></span>

<span data-ttu-id="782e5-104">Azure Cosmos DB est un service de base de données multi-modèles mondialement distribué par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="782e5-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="782e5-105">Rapidement, vous avez la possibilité de créer et d’interroger des documents, des paires clé/valeur, et des bases de données orientées graphe, profitant tous de la distribution à l’échelle mondiale et des capacités de mise à l’échelle horizontale au cœur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="782e5-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="782e5-106">Ce guide de démarrage rapide explique comment créer, à l’aide du Portail Azure, un compte Azure Cosmos DB, une base de données de documents, ainsi qu’une collection.</span><span class="sxs-lookup"><span data-stu-id="782e5-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="782e5-107">Vous allez ensuite créer et exécuter une application console basée sur [l’API Python DocumentDB](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="782e5-107">You then build and run a console app built on the [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="782e5-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="782e5-108">Prerequisites</span></span>

* <span data-ttu-id="782e5-109">Avant de pouvoir exécuter cet exemple, vous devez posséder les composants requis suivant :</span><span class="sxs-lookup"><span data-stu-id="782e5-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="782e5-110">Version [Visual Studio 2015](http://www.visualstudio.com/) ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="782e5-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="782e5-111">Outils Python pour Visual Studio disponibles dans [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="782e5-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="782e5-112">Ce didacticiel utilise Python Tools for Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="782e5-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="782e5-113">Python 2.7 disponible auprès de [python.org](https://www.python.org/downloads/release/python-2712/)</span><span class="sxs-lookup"><span data-stu-id="782e5-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="782e5-114">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="782e5-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="782e5-115">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="782e5-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="782e5-116">Clonage de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="782e5-116">Clone the sample application</span></span>

<span data-ttu-id="782e5-117">Nous allons maintenant cloner une application API DocumentDB à partir de GitHub, configurer la chaîne de connexion et l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="782e5-117">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="782e5-118">Vous pouvez constater à quel point il est facile de travailler par programmation avec des données.</span><span class="sxs-lookup"><span data-stu-id="782e5-118">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="782e5-119">Ouvrez une fenêtre de terminal git, comme git bash, et accédez à un répertoire de travail à l’aide de la commande `cd`.</span><span class="sxs-lookup"><span data-stu-id="782e5-119">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="782e5-120">Exécutez la commande suivante pour cloner l’exemple de référentiel :</span><span class="sxs-lookup"><span data-stu-id="782e5-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-the-code"></a><span data-ttu-id="782e5-121">Examiner le code</span><span class="sxs-lookup"><span data-stu-id="782e5-121">Review the code</span></span>

<span data-ttu-id="782e5-122">Passons rapidement en revue ce qu’il se passe dans l’application.</span><span class="sxs-lookup"><span data-stu-id="782e5-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="782e5-123">Ouvrez le fichier DocumentDBGetStarted.py, et vous découvrirez que ces lignes de code créent les ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="782e5-123">Open the DocumentDBGetStarted.py file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="782e5-124">Le DocumentClient est initialisé.</span><span class="sxs-lookup"><span data-stu-id="782e5-124">The DocumentClient is initialized.</span></span>

    ```python
    # Initialize the Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="782e5-125">Une nouvelle base de données est créée.</span><span class="sxs-lookup"><span data-stu-id="782e5-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="782e5-126">Une nouvelle collection est créée.</span><span class="sxs-lookup"><span data-stu-id="782e5-126">A new collection is created.</span></span>

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* <span data-ttu-id="782e5-127">Certains documents sont créés.</span><span class="sxs-lookup"><span data-stu-id="782e5-127">Some documents are created.</span></span>

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* <span data-ttu-id="782e5-128">Une requête est effectuée grâce à SQL</span><span class="sxs-lookup"><span data-stu-id="782e5-128">A query is performed using SQL</span></span>

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="782e5-129">Mettre à jour votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="782e5-129">Update your connection string</span></span>

<span data-ttu-id="782e5-130">Maintenant, retournez dans le portail Azure afin d’obtenir les informations de votre chaîne de connexion et de les copier dans l’application.</span><span class="sxs-lookup"><span data-stu-id="782e5-130">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="782e5-131">Dans le [portail Azure](http://portal.azure.com/), dans votre compte Azure Cosmos DB, dans le volet de navigation de gauche, cliquez sur **Clés**, puis sur **Clés en lecture-écriture**.</span><span class="sxs-lookup"><span data-stu-id="782e5-131">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="782e5-132">Vous utiliserez les boutons Copier sur le côté droit de l’écran pour copier l’URI et la clé primaire dans le fichier `DocumentDBGetStarted.py` à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="782e5-132">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `DocumentDBGetStarted.py` file in the next step.</span></span>

    ![Affichage et copie d’une clé d’accès dans le portail Azure, panneau Clés](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="782e5-134">Ouvrez le fichier `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="782e5-134">In Open the `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="782e5-135">Copiez votre valeur URI à partir du portail (à l’aide du bouton Copier) et définissez-la comme la valeur de la clé du point de terminaison dans `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="782e5-135">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="782e5-136">Puis, copiez votre valeur de clé primaire à partir du portail et définissez-la comme la valeur de `config.MASTERKEY` dans `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="782e5-136">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="782e5-137">Vous venez de mettre à jour votre application avec toutes les informations nécessaires pour communiquer avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="782e5-137">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="782e5-138">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="782e5-138">Run the app</span></span>
1. <span data-ttu-id="782e5-139">Dans Visual Studio, cliquez avec le bouton droit sur le projet dans **l’Explorateur de solutions**, sélectionnez l’environnement Python actuel, puis cliquez avec le bouton droit.</span><span class="sxs-lookup"><span data-stu-id="782e5-139">In Visual Studio, right-click on the project in **Solution Explorer**, select the current Python environment, then right click.</span></span>

2. <span data-ttu-id="782e5-140">Sélectionnez Installer le package Python, puis tapez dans **pydocumentdb**</span><span class="sxs-lookup"><span data-stu-id="782e5-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="782e5-141">Lancez F5 pour exécuter l'application.</span><span class="sxs-lookup"><span data-stu-id="782e5-141">Run F5 to run the application.</span></span> <span data-ttu-id="782e5-142">Votre application s’affiche dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="782e5-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="782e5-143">Vous pouvez dès à présent revenir à l’Explorateur de données et voir la requête, modifier et travailler avec ces nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="782e5-143">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="782e5-144">Examiner les SLA dans le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="782e5-144">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="782e5-145">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="782e5-145">Clean up resources</span></span>

<span data-ttu-id="782e5-146">Si vous ne pensez pas continuer à utiliser cette application, supprimez toutes les ressources créées durant ce guide de démarrage rapide dans le Portail Azure en procédant de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="782e5-146">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="782e5-147">Dans le menu de gauche du portail Azure, cliquez sur **Groupes de ressources**, puis sur le nom de la ressource que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="782e5-147">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="782e5-148">Dans la page de votre groupe de ressources, cliquez sur **Supprimer**, tapez le nom de la ressource à supprimer dans la zone de texte, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="782e5-148">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="782e5-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="782e5-149">Next steps</span></span>

<span data-ttu-id="782e5-150">Dans ce guide de démarrage rapide, vous avez appris à créer un compte Azure Cosmos DB, à créer une collection à l’aide de l’Explorateur de données, et à exécuter une application.</span><span class="sxs-lookup"><span data-stu-id="782e5-150">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="782e5-151">Vous pouvez maintenant importer des données supplémentaires à votre compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="782e5-151">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="782e5-152">Importer des données dans Azure Cosmos DB pour l’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="782e5-152">Import data into Azure Cosmos DB for the DocumentDB API</span></span>](import-data.md)


