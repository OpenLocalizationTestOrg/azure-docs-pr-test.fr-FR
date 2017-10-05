---
title: "Azure Cosmos DB : Créer une application avec Node.js et l’API DocumentDB | Microsoft Docs"
description: "Cet article présente un exemple de code Node.js que vous pouvez utiliser pour vous connecter à l’API DocumentDB d’Azure Cosmos DB et pour l’interroger."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 26e3548bf6aacbc60c4c46a5cc88749ca14cec01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-the-azure-portal"></a><span data-ttu-id="3f582-103">Azure Cosmos DB : Développer une application API DocumentDB grâce à Node.js et au Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3f582-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and the Azure portal</span></span>

<span data-ttu-id="3f582-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="3f582-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="3f582-105">Rapidement, vous avez la possibilité de créer et d’interroger des documents, des paires clé/valeur, et des bases de données orientées graphe, profitant tous de la distribution à l’échelle mondiale et des capacités de mise à l’échelle horizontale au cœur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f582-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="3f582-106">Ce guide de démarrage rapide explique comment créer, à l’aide du Portail Azure, un compte Azure Cosmos DB , une base de données de documents, ainsi qu’une collection.</span><span class="sxs-lookup"><span data-stu-id="3f582-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="3f582-107">Vous allez ensuite créer et exécuter une application console basée sur [l’API Node.js DocumentDB](documentdb-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="3f582-107">You then build and run a console app built on the [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f582-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3f582-108">Prerequisites</span></span>

* <span data-ttu-id="3f582-109">Avant de pouvoir exécuter cet exemple, vous devez posséder les composants requis suivants :</span><span class="sxs-lookup"><span data-stu-id="3f582-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="3f582-110">[Node.js](https://nodejs.org/en/) version v0.10.29 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="3f582-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="3f582-111">Git</span><span class="sxs-lookup"><span data-stu-id="3f582-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="3f582-112">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="3f582-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="3f582-113">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="3f582-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="3f582-114">Clonage de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="3f582-114">Clone the sample application</span></span>

<span data-ttu-id="3f582-115">Nous allons maintenant cloner une application API DocumentDB à partir de GitHub, configurer la chaîne de connexion et l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="3f582-115">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="3f582-116">Vous pouvez constater à quel point il est facile de travailler par programmation avec des données.</span><span class="sxs-lookup"><span data-stu-id="3f582-116">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="3f582-117">Ouvrez une fenêtre de terminal git, comme git bash, et accédez à un répertoire de travail à l’aide de la commande `CD`.</span><span class="sxs-lookup"><span data-stu-id="3f582-117">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="3f582-118">Exécutez la commande suivante pour cloner l’exemple de référentiel :</span><span class="sxs-lookup"><span data-stu-id="3f582-118">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="3f582-119">Examiner le code</span><span class="sxs-lookup"><span data-stu-id="3f582-119">Review the code</span></span>

<span data-ttu-id="3f582-120">Passons rapidement en revue ce qui se passe dans l’application.</span><span class="sxs-lookup"><span data-stu-id="3f582-120">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="3f582-121">Ouvrez le fichier `app.js` ; vous constatez que ces lignes de code créent les ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f582-121">Open the `app.js` file and you find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="3f582-122">Le `documentClient` est initialisé.</span><span class="sxs-lookup"><span data-stu-id="3f582-122">The `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="3f582-123">Une nouvelle base de données est créée.</span><span class="sxs-lookup"><span data-stu-id="3f582-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="3f582-124">Une nouvelle collection est créée.</span><span class="sxs-lookup"><span data-stu-id="3f582-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="3f582-125">Certains documents sont créés.</span><span class="sxs-lookup"><span data-stu-id="3f582-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="3f582-126">Une requête SQL sur JSON est effectuée.</span><span class="sxs-lookup"><span data-stu-id="3f582-126">A SQL query over JSON is performed.</span></span>

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="3f582-127">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="3f582-127">Update your connection string</span></span>

<span data-ttu-id="3f582-128">Maintenant, retournez dans le portail Azure afin d’obtenir les informations de votre chaîne de connexion et de les copier dans l’application.</span><span class="sxs-lookup"><span data-stu-id="3f582-128">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="3f582-129">Dans le [portail Azure](http://portal.azure.com/), dans votre compte Azure Cosmos DB, dans le volet de navigation de gauche, cliquez sur **Clés**, puis sur **Clés en lecture-écriture**.</span><span class="sxs-lookup"><span data-stu-id="3f582-129">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="3f582-130">Vous utiliserez les boutons Copier sur le côté droit de l’écran pour copier l’URI et la clé primaire dans le fichier `config.js` à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="3f582-130">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `config.js` file in the next step.</span></span>

    ![Affichage et copie d’une clé d’accès dans le portail Azure, panneau Clés](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="3f582-132">Ouvrez le fichier `config.js`.</span><span class="sxs-lookup"><span data-stu-id="3f582-132">In Open the `config.js` file.</span></span> 

3. <span data-ttu-id="3f582-133">Copiez votre valeur URI à partir du portail (à l’aide du bouton Copier) et définissez-la comme la valeur de la clé du point de terminaison dans `config.js`.</span><span class="sxs-lookup"><span data-stu-id="3f582-133">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="3f582-134">Puis, copiez votre valeur de clé primaire à partir du portail et définissez-la comme la valeur de `config.primaryKey` dans `config.js`.</span><span class="sxs-lookup"><span data-stu-id="3f582-134">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="3f582-135">Vous venez de mettre à jour votre application avec toutes les informations nécessaires pour communiquer avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f582-135">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="3f582-136">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="3f582-136">Run the app</span></span>
1. <span data-ttu-id="3f582-137">Exécutez `npm install` dans un terminal afin d’installer les modules npm requis.</span><span class="sxs-lookup"><span data-stu-id="3f582-137">Run `npm install` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="3f582-138">Exécutez `node app.js` sur un terminal pour démarrer votre application Node.</span><span class="sxs-lookup"><span data-stu-id="3f582-138">Run `node app.js` in a terminal to start your node application.</span></span>

<span data-ttu-id="3f582-139">Vous pouvez dès à présent revenir à l’Explorateur de données et voir la requête, modifier et travailler avec ces nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="3f582-139">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="3f582-140">Examiner les SLA dans le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3f582-140">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="3f582-141">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="3f582-141">Clean up resources</span></span>

<span data-ttu-id="3f582-142">Si vous ne pensez pas continuer à utiliser cette application, supprimez toutes les ressources créées durant ce guide de démarrage rapide dans le Portail Azure en procédant de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="3f582-142">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="3f582-143">Dans le menu de gauche du portail Azure, cliquez sur **Groupes de ressources**, puis sur le nom de la ressource que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="3f582-143">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="3f582-144">Dans la page de votre groupe de ressources, cliquez sur **Supprimer**, tapez le nom de la ressource à supprimer dans la zone de texte, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="3f582-144">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f582-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f582-145">Next steps</span></span>

<span data-ttu-id="3f582-146">Dans ce guide de démarrage rapide, vous avez appris à créer un compte Azure Cosmos DB, à créer une collection à l’aide de l’Explorateur de données, et à exécuter une application.</span><span class="sxs-lookup"><span data-stu-id="3f582-146">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="3f582-147">Vous pouvez maintenant importer des données supplémentaires dans votre compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f582-147">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="3f582-148">Importer des données dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3f582-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


