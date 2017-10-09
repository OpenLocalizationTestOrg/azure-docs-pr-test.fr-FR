---
title: "Azure Cosmos DB : créer une application web avec authentification Xamarin et Facebook | Microsoft Docs"
description: "Présente un exemple de code .NET que vous pouvez utiliser tooconnect tooand interroger la base de données Azure Cosmos"
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
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="bce5a-103">Azure Cosmos DB : créer une application web avec authentification .NET, Xamarin et Facebook</span><span class="sxs-lookup"><span data-stu-id="bce5a-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="bce5a-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="bce5a-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="bce5a-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="bce5a-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="bce5a-106">Ce démarrage rapide montre comment toocreate un compte de base de données Azure Cosmos, base de données du document et à l’aide de la collection hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bce5a-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="bce5a-107">Vous allez ensuite générer et déployer une application web de liste todo repose sur hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)et du moteur d’autorisation de base de données Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="bce5a-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and hello Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="bce5a-108">application web de liste de tâches Hello implémente un modèle de données par l’utilisateur qui permet de toologin les utilisateurs à l’aide de Facebook Auth et gérer leurs propres éléments toodo.</span><span class="sxs-lookup"><span data-stu-id="bce5a-108">hello todo list web app implements a per-user data pattern that enables users toologin using Facebook Auth and manage their own toodo items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bce5a-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bce5a-109">Prerequisites</span></span>

<span data-ttu-id="bce5a-110">Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello **libre** [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bce5a-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="bce5a-111">Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="bce5a-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="bce5a-112">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="bce5a-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="bce5a-113">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="bce5a-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="bce5a-114">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="bce5a-114">Clone hello sample application</span></span>

<span data-ttu-id="bce5a-115">Maintenant, nous allons une API DocumentDB le clonage d’application à partir de github, définir la chaîne de connexion hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="bce5a-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="bce5a-116">Vous allez voir combien il est facile toowork avec des données par programme.</span><span class="sxs-lookup"><span data-stu-id="bce5a-116">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="bce5a-117">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="bce5a-117">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="bce5a-118">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="bce5a-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="bce5a-119">Ouvrez ensuite le fichier de DocumentDBTodo.sln hello à partir du dossier samples/xamarin/UserItems/xamarin.forms hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bce5a-119">Then open hello DocumentDBTodo.sln file from hello samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="bce5a-120">Réviser le code hello</span><span class="sxs-lookup"><span data-stu-id="bce5a-120">Review hello code</span></span>

<span data-ttu-id="bce5a-121">code Hello dans le dossier de Xamarin hello contient :</span><span class="sxs-lookup"><span data-stu-id="bce5a-121">hello code in hello Xamarin folder contains:</span></span>

* <span data-ttu-id="bce5a-122">L’application Xamarin.</span><span class="sxs-lookup"><span data-stu-id="bce5a-122">Xamarin app.</span></span> <span data-ttu-id="bce5a-123">application Hello stocke des éléments de tâche de l’utilisateur hello dans une collection partitionnée nommée UserItems.</span><span class="sxs-lookup"><span data-stu-id="bce5a-123">hello app stores hello user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="bce5a-124">L’API du répartiteur de jetons de ressource.</span><span class="sxs-lookup"><span data-stu-id="bce5a-124">Resource token broker API.</span></span> <span data-ttu-id="bce5a-125">Une ressource de base de données Azure Cosmos toobroker API Web ASP.NET simple des jetons toohello les utilisateurs de l’application hello connecté.</span><span class="sxs-lookup"><span data-stu-id="bce5a-125">A simple ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello logged in users of hello app.</span></span> <span data-ttu-id="bce5a-126">Les jetons de ressource sont des jetons d’accès de courte durée de vie qui apportent une application hello hello accès toohello est enregistré dans les données de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bce5a-126">Resource tokens are short-lived access tokens that provide hello app with hello access toohello logged in user's data.</span></span>

<span data-ttu-id="bce5a-127">Hello d’authentification et flux de données est illustré dans le diagramme hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bce5a-127">hello authentication and data flow is illustrated in hello diagram below.</span></span>

* <span data-ttu-id="bce5a-128">Hello UserItems collection est créée avec la clé de partition hello ' / nom d’utilisateur ».</span><span class="sxs-lookup"><span data-stu-id="bce5a-128">hello UserItems collection is created with hello partition key '/userid'.</span></span> <span data-ttu-id="bce5a-129">Si vous indiquez une clé de partition pour une collection de base de données Azure Cosmos tooscale indéfiniment en tant que nombre hello des utilisateurs et des éléments augmente.</span><span class="sxs-lookup"><span data-stu-id="bce5a-129">Specifying a partition key for a collection allows Azure Cosmos DB tooscale infinitely as hello number of users and items grows.</span></span>
* <span data-ttu-id="bce5a-130">application Xamarin de Hello permet toologin utilisateurs avec les informations d’identification de Facebook.</span><span class="sxs-lookup"><span data-stu-id="bce5a-130">hello Xamarin app allows users toologin with Facebook credentials.</span></span>
* <span data-ttu-id="bce5a-131">application Xamarin de Hello utilise tooauthenticate de jeton accès Facebook avec l’API ResourceTokenBroker</span><span class="sxs-lookup"><span data-stu-id="bce5a-131">hello Xamarin app uses Facebook access token tooauthenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="bce5a-132">broker de jeton de ressource Hello API authentifie la demande de hello à l’aide de la fonctionnalité d’authentification de Service d’application et demande un jeton de ressource de base de données Azure Cosmos avec des documents de tooall d’accès en lecture/écriture partage la clé de partition de l’utilisateur authentifié hello.</span><span class="sxs-lookup"><span data-stu-id="bce5a-132">hello resource token broker API authenticates hello request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access tooall documents sharing hello authenticated user's partition key.</span></span>
* <span data-ttu-id="bce5a-133">Broker de jeton de ressource retourne hello ressource toohello jeton client application.</span><span class="sxs-lookup"><span data-stu-id="bce5a-133">Resource token broker returns hello resource token toohello client app.</span></span>
* <span data-ttu-id="bce5a-134">application Hello accède à des éléments de tâche de l’utilisateur hello à l’aide du jeton de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="bce5a-134">hello app accesses hello user's todo items using hello resource token.</span></span>

![Application To-Do avec des exemples de données](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="bce5a-136">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="bce5a-136">Update your connection string</span></span>

<span data-ttu-id="bce5a-137">Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="bce5a-137">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="bce5a-138">Bonjour [portail Azure](http://portal.azure.com/), dans votre base de données de Cosmos Azure account, Bonjour barre de navigation gauche, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**.</span><span class="sxs-lookup"><span data-stu-id="bce5a-138">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="bce5a-139">Vous allez utiliser les boutons de copier hello sur droite hello Hello de toocopy écran hello URI et la clé primaire dans le fichier Web.config de hello dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="bce5a-139">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello Web.config file in hello next step.</span></span>

    ![Afficher et copier une clé d’accès dans hello portail Azure, le panneau de clés](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="bce5a-141">Dans Visual Studio 2017, ouvrez le fichier Web.config de hello dans le dossier d’azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker hello.</span><span class="sxs-lookup"><span data-stu-id="bce5a-141">In Visual Studio 2017, open hello Web.config file in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="bce5a-142">Copier la valeur de l’URI à partir du portail hello (à l’aide du bouton de copie hello) et le rendre hello valeur accountUrl hello dans le fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="bce5a-142">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="bce5a-143">Copiez la valeur de clé primaire à partir du portail de hello, puis rendre hello valeur accountKey hello dans Web.congif.</span><span class="sxs-lookup"><span data-stu-id="bce5a-143">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="bce5a-144">Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bce5a-144">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-hello-web-app"></a><span data-ttu-id="bce5a-145">Générer et déployer l’application web de hello</span><span class="sxs-lookup"><span data-stu-id="bce5a-145">Build and deploy hello web app</span></span>

1. <span data-ttu-id="bce5a-146">Bonjour portail Azure, créer un Service d’applications du site Web toohost hello ressource jeton broker API.</span><span class="sxs-lookup"><span data-stu-id="bce5a-146">In hello Azure portal, create an App Service website toohost hello Resource token broker API.</span></span>
2. <span data-ttu-id="bce5a-147">Dans hello portail Azure, ouvrez le panneau des paramètres de l’application hello hello ressource jeton du service broker de site Web.</span><span class="sxs-lookup"><span data-stu-id="bce5a-147">In hello Azure portal, open hello App Settings blade of hello Resource token broker API website.</span></span> <span data-ttu-id="bce5a-148">Renseignez hello suivant les paramètres de l’application :</span><span class="sxs-lookup"><span data-stu-id="bce5a-148">Fill in hello following app settings:</span></span>

    * <span data-ttu-id="bce5a-149">accountUrl - URL du compte de base de données Azure Cosmos hello à partir de l’onglet de clés hello de votre compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bce5a-149">accountUrl - hello Azure Cosmos DB account URL from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="bce5a-150">accountKey - clé de principale de compte de base de données Azure Cosmos hello à partir de l’onglet de clés hello de votre compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bce5a-150">accountKey - hello Azure Cosmos DB account master key from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="bce5a-151">databaseId et collectionId de la base de données et de la collection créées</span><span class="sxs-lookup"><span data-stu-id="bce5a-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="bce5a-152">Hello tooyour de solution ResourceTokenBroker créé le site Web de publication.</span><span class="sxs-lookup"><span data-stu-id="bce5a-152">Publish hello ResourceTokenBroker solution tooyour created website.</span></span>

4. <span data-ttu-id="bce5a-153">Ouvrez le projet de Xamarin hello et accédez tooTodoItemManager.cs.</span><span class="sxs-lookup"><span data-stu-id="bce5a-153">Open hello Xamarin project, and navigate tooTodoItemManager.cs.</span></span> <span data-ttu-id="bce5a-154">Renseignez hello accountURL, collectionId, databaseId, ainsi que resourceTokenBrokerURL comme url de base https hello pour le site Web Service Broker pour les jetons de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="bce5a-154">Fill in hello values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as hello base https url for hello resource token broker website.</span></span>

5. <span data-ttu-id="bce5a-155">Hello complète [comment tooconfigure votre compte de connexion du Service d’applications application toouse Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) toosetup didacticiel l’authentification Facebook et configurer le site Web de ResourceTokenBroker hello.</span><span class="sxs-lookup"><span data-stu-id="bce5a-155">Complete hello [How tooconfigure your App Service application toouse Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial toosetup Facebook authentication and configure hello ResourceTokenBroker website.</span></span>

    <span data-ttu-id="bce5a-156">Exécutez l’application Xamarin de hello.</span><span class="sxs-lookup"><span data-stu-id="bce5a-156">Run hello Xamarin app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="bce5a-157">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="bce5a-157">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="bce5a-158">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="bce5a-158">Clean up resources</span></span>

<span data-ttu-id="bce5a-159">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bce5a-159">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="bce5a-160">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="bce5a-160">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you just created.</span></span> 
2. <span data-ttu-id="bce5a-161">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="bce5a-161">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bce5a-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bce5a-162">Next steps</span></span>

<span data-ttu-id="bce5a-163">Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer une collection à l’aide de hello Explorateur de données, générer et déployer une application Xamarin.</span><span class="sxs-lookup"><span data-stu-id="bce5a-163">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="bce5a-164">Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="bce5a-164">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="bce5a-165">Importer des données dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bce5a-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
