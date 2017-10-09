---
title: "Azure Cosmos DB : Générer une application avec Python et hello API DocumentDB | Documents Microsoft"
description: "Présente un exemple de code Python que vous pouvez utiliser la requête de tooand tooconnect hello Azure Cosmos DB DocumentDB API"
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
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a><span data-ttu-id="73dc2-103">Base de données Cosmos Azure : Générer une application de l’API DocumentDB avec Python et hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="73dc2-103">Azure Cosmos DB: Build a DocumentDB API app with Python and hello Azure portal</span></span>

<span data-ttu-id="73dc2-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="73dc2-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="73dc2-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="73dc2-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="73dc2-106">Ce démarrage rapide montre comment toocreate un compte de base de données Azure Cosmos, base de données du document et à l’aide de la collection hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="73dc2-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="73dc2-107">Vous puis créer et exécuter une application de console basée sur hello [DocumentDB Python API](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="73dc2-107">You then build and run a console app built on hello [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73dc2-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="73dc2-108">Prerequisites</span></span>

* <span data-ttu-id="73dc2-109">Avant de pouvoir exécuter cet exemple, vous devez disposer de hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="73dc2-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="73dc2-110">Version [Visual Studio 2015](http://www.visualstudio.com/) ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="73dc2-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="73dc2-111">Outils Python pour Visual Studio disponibles dans [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="73dc2-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="73dc2-112">Ce didacticiel utilise Python Tools for Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="73dc2-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="73dc2-113">Python 2.7 disponible auprès de [python.org](https://www.python.org/downloads/release/python-2712/)</span><span class="sxs-lookup"><span data-stu-id="73dc2-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="73dc2-114">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="73dc2-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="73dc2-115">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="73dc2-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="73dc2-116">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="73dc2-116">Clone hello sample application</span></span>

<span data-ttu-id="73dc2-117">Maintenant, nous allons une API DocumentDB le clonage d’application à partir de github, définir la chaîne de connexion hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="73dc2-117">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="73dc2-118">Vous voyez combien il est facile toowork avec des données par programme.</span><span class="sxs-lookup"><span data-stu-id="73dc2-118">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="73dc2-119">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="73dc2-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="73dc2-120">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="73dc2-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a><span data-ttu-id="73dc2-121">Réviser le code hello</span><span class="sxs-lookup"><span data-stu-id="73dc2-121">Review hello code</span></span>

<span data-ttu-id="73dc2-122">Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="73dc2-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="73dc2-123">Fichier de DocumentDBGetStarted.py hello ouvert et que vous trouverez ces lignes de code créent hello des ressources de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="73dc2-123">Open hello DocumentDBGetStarted.py file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="73dc2-124">Hello DocumentClient est initialisé.</span><span class="sxs-lookup"><span data-stu-id="73dc2-124">hello DocumentClient is initialized.</span></span>

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="73dc2-125">Une nouvelle base de données est créée.</span><span class="sxs-lookup"><span data-stu-id="73dc2-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="73dc2-126">Une nouvelle collection est créée.</span><span class="sxs-lookup"><span data-stu-id="73dc2-126">A new collection is created.</span></span>

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

* <span data-ttu-id="73dc2-127">Certains documents sont créés.</span><span class="sxs-lookup"><span data-stu-id="73dc2-127">Some documents are created.</span></span>

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

* <span data-ttu-id="73dc2-128">Une requête est effectuée grâce à SQL</span><span class="sxs-lookup"><span data-stu-id="73dc2-128">A query is performed using SQL</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="73dc2-129">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="73dc2-129">Update your connection string</span></span>

<span data-ttu-id="73dc2-130">Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="73dc2-130">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="73dc2-131">Bonjour [portail Azure](http://portal.azure.com/), dans votre base de données de Cosmos Azure account, Bonjour barre de navigation gauche, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**.</span><span class="sxs-lookup"><span data-stu-id="73dc2-131">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="73dc2-132">Vous allez utiliser les boutons de copier hello sur droite hello Hello de toocopy écran hello URI et la clé primaire dans hello `DocumentDBGetStarted.py` fichier à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="73dc2-132">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `DocumentDBGetStarted.py` file in hello next step.</span></span>

    ![Afficher et copier une clé d’accès dans hello portail Azure, le panneau de clés](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="73dc2-134">Ouvrez Bonjour `DocumentDBGetStarted.py` fichier.</span><span class="sxs-lookup"><span data-stu-id="73dc2-134">In Open hello `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="73dc2-135">Copier la valeur de l’URI à partir du portail hello (à l’aide du bouton de copie hello) et le rendre hello la valeur de clé de point de terminaison hello dans `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="73dc2-135">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="73dc2-136">Copiez la valeur de clé primaire à partir du portail de hello, puis rendre hello valeur Hello `config.MASTERKEY` dans `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="73dc2-136">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="73dc2-137">Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="73dc2-137">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="73dc2-138">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="73dc2-138">Run hello app</span></span>
1. <span data-ttu-id="73dc2-139">Dans Visual Studio, cliquez sur projet hello dans **l’Explorateur de solutions**, sélectionnez l’environnement Python hello, puis avec le bouton droit.</span><span class="sxs-lookup"><span data-stu-id="73dc2-139">In Visual Studio, right-click on hello project in **Solution Explorer**, select hello current Python environment, then right click.</span></span>

2. <span data-ttu-id="73dc2-140">Sélectionnez Installer le package Python, puis tapez dans **pydocumentdb**</span><span class="sxs-lookup"><span data-stu-id="73dc2-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="73dc2-141">Exécutez l’application de hello toorun F5.</span><span class="sxs-lookup"><span data-stu-id="73dc2-141">Run F5 toorun hello application.</span></span> <span data-ttu-id="73dc2-142">Votre application s’affiche dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="73dc2-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="73dc2-143">Vous pouvez maintenant revenir en arrière tooData Explorer et consultez la requête, modifier et travailler avec ces nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="73dc2-143">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="73dc2-144">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="73dc2-144">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="73dc2-145">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="73dc2-145">Clean up resources</span></span>

<span data-ttu-id="73dc2-146">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="73dc2-146">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="73dc2-147">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="73dc2-147">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="73dc2-148">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="73dc2-148">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73dc2-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="73dc2-149">Next steps</span></span>

<span data-ttu-id="73dc2-150">Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer une collection à l’aide de hello Explorateur de données et exécuter une application.</span><span class="sxs-lookup"><span data-stu-id="73dc2-150">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="73dc2-151">Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="73dc2-151">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="73dc2-152">Importer des données dans la base de données Azure Cosmos pour hello API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="73dc2-152">Import data into Azure Cosmos DB for hello DocumentDB API</span></span>](import-data.md)


