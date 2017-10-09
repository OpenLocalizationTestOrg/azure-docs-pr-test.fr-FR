---
title: "Azure Cosmos DB : Générer une application avec Node.js et hello API DocumentDB | Documents Microsoft"
description: "Présente un exemple de code Node.js que vous pouvez utiliser la requête de tooand tooconnect hello Azure Cosmos DB DocumentDB API"
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
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a><span data-ttu-id="f8f33-103">Base de données Cosmos Azure : Générer une application de l’API DocumentDB avec Node.js et hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f8f33-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and hello Azure portal</span></span>

<span data-ttu-id="f8f33-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="f8f33-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="f8f33-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="f8f33-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="f8f33-106">Ce démarrage rapide montre comment toocreate un compte de base de données Azure Cosmos, base de données du document et à l’aide de la collection hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f8f33-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="f8f33-107">Vous puis créer et exécuter une application de console basée sur hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="f8f33-107">You then build and run a console app built on hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8f33-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f8f33-108">Prerequisites</span></span>

* <span data-ttu-id="f8f33-109">Avant de pouvoir exécuter cet exemple, vous devez disposer de hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="f8f33-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="f8f33-110">[Node.js](https://nodejs.org/en/) version v0.10.29 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="f8f33-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="f8f33-111">Git</span><span class="sxs-lookup"><span data-stu-id="f8f33-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="f8f33-112">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="f8f33-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="f8f33-113">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="f8f33-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="f8f33-114">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="f8f33-114">Clone hello sample application</span></span>

<span data-ttu-id="f8f33-115">Maintenant, nous allons une API DocumentDB le clonage d’application à partir de github, définir la chaîne de connexion hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="f8f33-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="f8f33-116">Vous voyez combien il est facile toowork avec des données par programme.</span><span class="sxs-lookup"><span data-stu-id="f8f33-116">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="f8f33-117">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `CD` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="f8f33-117">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="f8f33-118">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="f8f33-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="f8f33-119">Réviser le code hello</span><span class="sxs-lookup"><span data-stu-id="f8f33-119">Review hello code</span></span>

<span data-ttu-id="f8f33-120">Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="f8f33-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="f8f33-121">Ouvrez hello `app.js` fichier et que vous recherchez que ces lignes de code créent les ressources de base de données Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="f8f33-121">Open hello `app.js` file and you find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="f8f33-122">Hello `documentClient` est initialisé.</span><span class="sxs-lookup"><span data-stu-id="f8f33-122">hello `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="f8f33-123">Une nouvelle base de données est créée.</span><span class="sxs-lookup"><span data-stu-id="f8f33-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="f8f33-124">Une nouvelle collection est créée.</span><span class="sxs-lookup"><span data-stu-id="f8f33-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="f8f33-125">Certains documents sont créés.</span><span class="sxs-lookup"><span data-stu-id="f8f33-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="f8f33-126">Une requête SQL sur JSON est effectuée.</span><span class="sxs-lookup"><span data-stu-id="f8f33-126">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="f8f33-127">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="f8f33-127">Update your connection string</span></span>

<span data-ttu-id="f8f33-128">Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="f8f33-128">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="f8f33-129">Bonjour [portail Azure](http://portal.azure.com/), dans votre base de données de Cosmos Azure account, Bonjour barre de navigation gauche, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**.</span><span class="sxs-lookup"><span data-stu-id="f8f33-129">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="f8f33-130">Vous allez utiliser les boutons de copier hello sur droite hello Hello de toocopy écran hello URI et la clé primaire dans hello `config.js` fichier à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="f8f33-130">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `config.js` file in hello next step.</span></span>

    ![Afficher et copier une clé d’accès dans hello portail Azure, le panneau de clés](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="f8f33-132">Ouvrez Bonjour `config.js` fichier.</span><span class="sxs-lookup"><span data-stu-id="f8f33-132">In Open hello `config.js` file.</span></span> 

3. <span data-ttu-id="f8f33-133">Copier la valeur de l’URI à partir du portail hello (à l’aide du bouton de copie hello) et le rendre hello la valeur de clé de point de terminaison hello dans `config.js`.</span><span class="sxs-lookup"><span data-stu-id="f8f33-133">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="f8f33-134">Copiez la valeur de clé primaire à partir du portail de hello, puis rendre hello valeur Hello `config.primaryKey` dans `config.js`.</span><span class="sxs-lookup"><span data-stu-id="f8f33-134">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="f8f33-135">Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f8f33-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="f8f33-136">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="f8f33-136">Run hello app</span></span>
1. <span data-ttu-id="f8f33-137">Exécutez `npm install` dans un terminal tooinstall requis des modules npm</span><span class="sxs-lookup"><span data-stu-id="f8f33-137">Run `npm install` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="f8f33-138">Exécutez `node app.js` dans un terminal toostart votre application de nœud.</span><span class="sxs-lookup"><span data-stu-id="f8f33-138">Run `node app.js` in a terminal toostart your node application.</span></span>

<span data-ttu-id="f8f33-139">Vous pouvez maintenant revenir en arrière tooData Explorer et consultez la requête, modifier et travailler avec ces nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="f8f33-139">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="f8f33-140">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f8f33-140">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="f8f33-141">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="f8f33-141">Clean up resources</span></span>

<span data-ttu-id="f8f33-142">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f8f33-142">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="f8f33-143">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="f8f33-143">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="f8f33-144">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="f8f33-144">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8f33-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f8f33-145">Next steps</span></span>

<span data-ttu-id="f8f33-146">Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer une collection à l’aide de hello Explorateur de données et exécuter une application.</span><span class="sxs-lookup"><span data-stu-id="f8f33-146">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="f8f33-147">Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f8f33-147">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="f8f33-148">Importer des données dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f8f33-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


