---
title: "Azure Cosmos DB : créer une application web avec authentification Xamarin et Facebook | Microsoft Docs"
description: "Cet article présente un exemple de code .NET que vous pouvez utiliser pour vous connecter à Azure Cosmos DB et pour l’interroger."
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
ms.openlocfilehash: 4ea97c2aca6769843d0210ffeae6f95531a21f10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="956b5-103">Azure Cosmos DB : créer une application web avec authentification .NET, Xamarin et Facebook</span><span class="sxs-lookup"><span data-stu-id="956b5-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="956b5-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="956b5-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="956b5-105">Rapidement, vous avez la possibilité de créer et d’interroger des documents, des paires clé/valeur, et des bases de données orientées graphe, profitant tous de la distribution à l’échelle mondiale et des capacités de mise à l’échelle horizontale au cœur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="956b5-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="956b5-106">Ce guide de démarrage rapide explique comment créer, à l’aide du portail Azure, un compte Azure Cosmos DB, une base de données de documents, ainsi qu’une collection.</span><span class="sxs-lookup"><span data-stu-id="956b5-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="956b5-107">Vous allez ensuite créer et déployer une application web incluant une liste de tâches basée sur l’[API .NET DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/) et le moteur d’autorisation Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="956b5-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and the Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="956b5-108">L’application web avec liste de tâches implémente un modèle de données par utilisateur qui permet aux utilisateurs de se connecter via l’authentification Facebook et de gérer leurs propres tâches.</span><span class="sxs-lookup"><span data-stu-id="956b5-108">The todo list web app implements a per-user data pattern that enables users to login using Facebook Auth and manage their own to do items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="956b5-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="956b5-109">Prerequisites</span></span>

<span data-ttu-id="956b5-110">Si vous n’avez pas encore installé Visual Studio 2017, vous pouvez télécharger et utiliser la version **gratuite** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="956b5-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="956b5-111">Veillez à activer **le développement Azure** lors de l’installation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="956b5-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="956b5-112">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="956b5-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="956b5-113">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="956b5-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="956b5-114">Clonage de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="956b5-114">Clone the sample application</span></span>

<span data-ttu-id="956b5-115">Nous allons maintenant cloner une application API DocumentDB à partir de GitHub, configurer la chaîne de connexion et l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="956b5-115">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="956b5-116">Vous verrez combien il est facile de travailler par programmation avec des données.</span><span class="sxs-lookup"><span data-stu-id="956b5-116">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="956b5-117">Ouvrez une fenêtre de terminal git, comme git bash, et accédez à un répertoire de travail à l’aide de la commande `cd`.</span><span class="sxs-lookup"><span data-stu-id="956b5-117">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="956b5-118">Exécutez la commande suivante pour cloner l’exemple de référentiel.</span><span class="sxs-lookup"><span data-stu-id="956b5-118">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="956b5-119">Ouvrez ensuite le fichier DocumentDBTodo.sln à partir du dossier samples/xamarin/UserItems/xamarin.forms dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="956b5-119">Then open the DocumentDBTodo.sln file from the samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="956b5-120">Vérifier le code</span><span class="sxs-lookup"><span data-stu-id="956b5-120">Review the code</span></span>

<span data-ttu-id="956b5-121">Le code dans le dossier Xamarin contient :</span><span class="sxs-lookup"><span data-stu-id="956b5-121">The code in the Xamarin folder contains:</span></span>

* <span data-ttu-id="956b5-122">L’application Xamarin.</span><span class="sxs-lookup"><span data-stu-id="956b5-122">Xamarin app.</span></span> <span data-ttu-id="956b5-123">L’application stocke les tâches de l’utilisateur dans une collection partitionnée nommée UserItems.</span><span class="sxs-lookup"><span data-stu-id="956b5-123">The app stores the user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="956b5-124">L’API du répartiteur de jetons de ressource.</span><span class="sxs-lookup"><span data-stu-id="956b5-124">Resource token broker API.</span></span> <span data-ttu-id="956b5-125">Une simple API web ASP.NET permettant de répartir les jetons de ressource Azure Cosmos DB entre les utilisateurs connectés de l’application.</span><span class="sxs-lookup"><span data-stu-id="956b5-125">A simple ASP.NET Web API to broker Azure Cosmos DB resource tokens to the logged in users of the app.</span></span> <span data-ttu-id="956b5-126">Les jetons de ressource sont des jetons d’accès de courte durée qui permettent à l’application d’accéder aux données de l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="956b5-126">Resource tokens are short-lived access tokens that provide the app with the access to the logged in user's data.</span></span>

<span data-ttu-id="956b5-127">Le flux de données et d’authentification est illustré dans le diagramme ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="956b5-127">The authentication and data flow is illustrated in the diagram below.</span></span>

* <span data-ttu-id="956b5-128">La collection UserItems est créée avec la clé de partition « /userid ».</span><span class="sxs-lookup"><span data-stu-id="956b5-128">The UserItems collection is created with the partition key '/userid'.</span></span> <span data-ttu-id="956b5-129">Si vous spécifiez une clé de partition pour une collection, Azure Cosmos DB peut se mettre à l’échelle à l’infini au fur et à mesure que le nombre d’utilisateurs et d’éléments augmente.</span><span class="sxs-lookup"><span data-stu-id="956b5-129">Specifying a partition key for a collection allows Azure Cosmos DB to scale infinitely as the number of users and items grows.</span></span>
* <span data-ttu-id="956b5-130">L’application Xamarin permet aux utilisateurs de se connecter avec leurs identifiants Facebook.</span><span class="sxs-lookup"><span data-stu-id="956b5-130">The Xamarin app allows users to login with Facebook credentials.</span></span>
* <span data-ttu-id="956b5-131">L’application Xamarin utilise le jeton d’accès Facebook pour s’authentifier avec l’API ResourceTokenBroker.</span><span class="sxs-lookup"><span data-stu-id="956b5-131">The Xamarin app uses Facebook access token to authenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="956b5-132">L’API de répartition de jetons de ressource authentifie la demande à l’aide de la fonctionnalité d’authentification d’App Service et demande un jeton de ressource Azure Cosmos DB avec accès en lecture/écriture à tous les documents partageant la clé de partition de l’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="956b5-132">The resource token broker API authenticates the request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access to all documents sharing the authenticated user's partition key.</span></span>
* <span data-ttu-id="956b5-133">Le répartiteur de jetons de ressource renvoie le jeton de ressource à l’application cliente.</span><span class="sxs-lookup"><span data-stu-id="956b5-133">Resource token broker returns the resource token to the client app.</span></span>
* <span data-ttu-id="956b5-134">L’application accède aux tâches de l’utilisateur à l’aide du jeton de ressource.</span><span class="sxs-lookup"><span data-stu-id="956b5-134">The app accesses the user's todo items using the resource token.</span></span>

![Application Todo avec des exemples de données](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="956b5-136">Mettre à jour votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="956b5-136">Update your connection string</span></span>

<span data-ttu-id="956b5-137">Maintenant, retournez dans le portail Azure afin d’obtenir les informations de votre chaîne de connexion et de les copier dans l’application.</span><span class="sxs-lookup"><span data-stu-id="956b5-137">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="956b5-138">Dans le [portail Azure](http://portal.azure.com/), dans votre compte Azure Cosmos DB, dans le volet de navigation de gauche, cliquez sur **Clés**, puis sur **Clés en lecture-écriture**.</span><span class="sxs-lookup"><span data-stu-id="956b5-138">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="956b5-139">Vous utiliserez les boutons Copier sur le côté droit de l’écran pour copier l’URI et la clé primaire dans le fichier Web.config à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="956b5-139">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the Web.config file in the next step.</span></span>

    ![Afficher et copier une touche d’accès rapide dans le portail Azure, panneau Clés](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="956b5-141">Dans Visual Studio 2017, ouvrez le fichier Web.config dans le dossier azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker.</span><span class="sxs-lookup"><span data-stu-id="956b5-141">In Visual Studio 2017, open the Web.config file in the azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="956b5-142">Copiez votre valeur URI à partir du portail (à l’aide du bouton Copier) et définissez-la comme la valeur de la propriété accountUrl dans le fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="956b5-142">Copy your URI value from the portal (using the copy button) and make it the value of the accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="956b5-143">Puis, copiez votre valeur de clé primaire à partir du portail et définissez-la comme la valeur de la clé accountKey dans Web.config.</span><span class="sxs-lookup"><span data-stu-id="956b5-143">Then copy your PRIMARY KEY value from the portal and make it the value of the accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="956b5-144">Vous venez de mettre à jour votre application avec toutes les informations nécessaires pour communiquer avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="956b5-144">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-the-web-app"></a><span data-ttu-id="956b5-145">Générer et déployer l’application web</span><span class="sxs-lookup"><span data-stu-id="956b5-145">Build and deploy the web app</span></span>

1. <span data-ttu-id="956b5-146">Dans le portail Azure, créez un site web App Service pour héberger l’API de répartition des jetons de ressource.</span><span class="sxs-lookup"><span data-stu-id="956b5-146">In the Azure portal, create an App Service website to host the Resource token broker API.</span></span>
2. <span data-ttu-id="956b5-147">Dans le portail Azure, ouvrez le panneau Paramètres de l’application du site web de l’API de répartition des jetons de ressource.</span><span class="sxs-lookup"><span data-stu-id="956b5-147">In the Azure portal, open the App Settings blade of the Resource token broker API website.</span></span> <span data-ttu-id="956b5-148">Renseignez les paramètres d’application suivants :</span><span class="sxs-lookup"><span data-stu-id="956b5-148">Fill in the following app settings:</span></span>

    * <span data-ttu-id="956b5-149">accountUrl : URL du compte Azure Cosmos DB à partir de l’onglet Clés de votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="956b5-149">accountUrl - The Azure Cosmos DB account URL from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="956b5-150">accountKey : clé principale du compte Azure Cosmos DB à partir de l’onglet Clés de votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="956b5-150">accountKey - The Azure Cosmos DB account master key from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="956b5-151">databaseId et collectionId de la base de données et de la collection créées</span><span class="sxs-lookup"><span data-stu-id="956b5-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="956b5-152">Publiez la solution ResourceTokenBroker sur le site web que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="956b5-152">Publish the ResourceTokenBroker solution to your created website.</span></span>

4. <span data-ttu-id="956b5-153">Ouvrez le projet Xamarin et accédez à TodoItemManager.cs.</span><span class="sxs-lookup"><span data-stu-id="956b5-153">Open the Xamarin project, and navigate to TodoItemManager.cs.</span></span> <span data-ttu-id="956b5-154">Renseignez les valeurs accountURL, collectionId, databaseId, ainsi que resourceTokenBrokerURL comme URL https de base pour le site web de répartition des jetons de ressource.</span><span class="sxs-lookup"><span data-stu-id="956b5-154">Fill in the values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as the base https url for the resource token broker website.</span></span>

5. <span data-ttu-id="956b5-155">Terminez le didacticiel [Comment configurer votre application App Service de manière à utiliser la connexion Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) pour configurer l’authentification Facebook et le site web ResourceTokenBroker.</span><span class="sxs-lookup"><span data-stu-id="956b5-155">Complete the [How to configure your App Service application to use Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial to setup Facebook authentication and configure the ResourceTokenBroker website.</span></span>

    <span data-ttu-id="956b5-156">Exécutez l'application Xamarin.</span><span class="sxs-lookup"><span data-stu-id="956b5-156">Run the Xamarin app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="956b5-157">Consulter les contrats SLA dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="956b5-157">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="956b5-158">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="956b5-158">Clean up resources</span></span>

<span data-ttu-id="956b5-159">Si vous ne pensez pas utiliser à nouveau cette application, supprimez toutes les ressources créées par ce démarrage rapide dans le portail Azure en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="956b5-159">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="956b5-160">À partir du menu de gauche dans le portail Azure, cliquez sur **Groupes de ressources**, puis sur le nom de la ressource que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="956b5-160">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you just created.</span></span> 
2. <span data-ttu-id="956b5-161">Dans la page de votre groupe de ressources, cliquez sur **Supprimer**, tapez le nom de la ressource à supprimer dans la zone de texte, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="956b5-161">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="956b5-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="956b5-162">Next steps</span></span>

<span data-ttu-id="956b5-163">Dans ce démarrage rapide, vous avez appris à créer un compte Azure Cosmos DB, à créer une collection à l’aide de l’Explorateur de données, et à concevoir et déployer une application Xamarin.</span><span class="sxs-lookup"><span data-stu-id="956b5-163">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="956b5-164">Vous pouvez maintenant importer des données supplémentaires dans votre compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="956b5-164">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="956b5-165">Importer des données dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="956b5-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
