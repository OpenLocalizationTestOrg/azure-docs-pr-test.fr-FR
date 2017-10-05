---
title: "Création d’une application ASP.NET dans Azure avec SQL Database | Microsoft Docs"
description: "Découvrez comment faire fonctionner une application ASP.NET dans Azure en établissant une connexion à une instance SQL Database."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c22b8ef4866fe2f1ae32c7cb9158fc7866788b26
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="a3f4c-103">Création d’une application ASP.NET dans Azure avec SQL Database</span><span class="sxs-lookup"><span data-stu-id="a3f4c-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="a3f4c-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="a3f4c-105">Ce didacticiel vous montre comment déployer dans Azure une application web ASP.NET axée sur les données et comment la connecter à [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3f4c-105">This tutorial shows you how to deploy a data-driven ASP.NET web app in Azure and connect it to [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="a3f4c-106">Lorsque vous avez terminé, vous disposez d’une application ASP.NET exécutée dans [Azure App Service](../app-service/app-service-value-prop-what-is.md) et connectée à SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected to SQL Database.</span></span>

![Application ASP.NET publiée dans une application web Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="a3f4c-108">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3f4c-109">Créer une base de données SQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="a3f4c-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="a3f4c-110">Connecter une application ASP.NET à SQL Database</span><span class="sxs-lookup"><span data-stu-id="a3f4c-110">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="a3f4c-111">Déploiement de l’application dans Azure</span><span class="sxs-lookup"><span data-stu-id="a3f4c-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="a3f4c-112">Mettre à jour le modèle de données et redéployer l’application</span><span class="sxs-lookup"><span data-stu-id="a3f4c-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="a3f4c-113">Diffuser des journaux à partir d’Azure vers votre terminal</span><span class="sxs-lookup"><span data-stu-id="a3f4c-113">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="a3f4c-114">Gérer l’application dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a3f4c-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3f4c-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a3f4c-115">Prerequisites</span></span>

<span data-ttu-id="a3f4c-116">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-116">To complete this tutorial:</span></span>

* <span data-ttu-id="a3f4c-117">Installez [Visual Studio 2017](https://www.visualstudio.com/downloads/) avec les charges de travail suivantes :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
  - <span data-ttu-id="a3f4c-118">**Développement web et ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="a3f4c-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="a3f4c-119">**Développement Azure**</span><span class="sxs-lookup"><span data-stu-id="a3f4c-119">**Azure development**</span></span>

  ![Développement web et ASP.NET et Développement Azure (sous Web et cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="a3f4c-121">Téléchargez l’exemple</span><span class="sxs-lookup"><span data-stu-id="a3f4c-121">Download the sample</span></span>

<span data-ttu-id="a3f4c-122">[Téléchargez l’exemple de projet](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="a3f4c-122">[Download the sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="a3f4c-123">Extrayez (décompressez) le fichier *dotnet-sqldb-tutorial-master.zip*.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-123">Extract (unzip) the  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="a3f4c-124">Cet exemple de projet contient une simple application CRUD (Create-Read-Update-Delete) [ASP.NET MVC](https://www.asp.net/mvc) basée sur [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="a3f4c-124">The sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-the-app"></a><span data-ttu-id="a3f4c-125">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="a3f4c-125">Run the app</span></span>

<span data-ttu-id="a3f4c-126">Ouvrez le fichier *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-126">Open the *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="a3f4c-127">Entrez `Ctrl+F5` pour exécuter l’application sans débogage.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-127">Type `Ctrl+F5` to run the app without debugging.</span></span> <span data-ttu-id="a3f4c-128">L’application s’affiche dans votre navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-128">The app is displayed in your default browser.</span></span> <span data-ttu-id="a3f4c-129">Sélectionnez le lien **Create New** et créez quelques éléments *to-do*.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-129">Select the **Create New** link and create a couple *to-do* items.</span></span> 

![Boîte de dialogue New ASP.NET Project](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="a3f4c-131">Testez les liens **Edit**, **Details** et **Delete**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-131">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="a3f4c-132">L’application utilise un contexte de base de données pour se connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-132">The app uses a database context to connect with the database.</span></span> <span data-ttu-id="a3f4c-133">Dans cet exemple, le contexte de base de données utilise une chaîne de connexion appelée `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-133">In this sample, the database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="a3f4c-134">Cette chaîne de connexion est définie dans le fichier *Web.config* et référencée dans le fichier *Models\MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-134">The connection string is set in the *Web.config* file and referenced in the *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="a3f4c-135">Utilisé plus loin dans ce didacticiel, le nom de chaîne de connexion permet de connecter l’application web Azure à une base de données SQL Azure Database.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-135">The connection string name is used later in the tutorial to connect the Azure web app to an Azure SQL Database.</span></span> 

## <a name="publish-to-azure-with-sql-database"></a><span data-ttu-id="a3f4c-136">Publier dans Azure avec SQL Database</span><span class="sxs-lookup"><span data-stu-id="a3f4c-136">Publish to Azure with SQL Database</span></span>

<span data-ttu-id="a3f4c-137">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet **DotNetAppSqlDb**, puis sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-137">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publier à partir de l’Explorateur de solutions](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="a3f4c-139">Assurez-vous que **Microsoft Azure App Service** est sélectionné et cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publier à partir de la page de présentation du projet](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="a3f4c-141">La publication ouvre la boîte de dialogue **Créer App Service** qui vous permet de créer toutes les ressources Azure dont vous avez besoin pour exécuter votre application web ASP.NET dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-141">Publishing opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="a3f4c-142">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="a3f4c-142">Sign in to Azure</span></span>

<span data-ttu-id="a3f4c-143">Dans la boîte de dialogue **Créer App Service**, cliquez sur **Ajouter un compte** puis connectez-vous à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-143">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span></span> <span data-ttu-id="a3f4c-144">Si vous êtes déjà connecté à un compte Microsoft, assurez-vous que le compte conserve votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="a3f4c-145">Si le compte Microsoft auquel vous êtes connecté ne comporte pas votre abonnement Azure, cliquez dessus pour ajouter le compte approprié.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-145">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span></span>
   
![Connexion à Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="a3f4c-147">Une fois connecté, vous êtes prêt à créer toutes les ressources dont vous avez besoin pour votre application web Azure dans cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-147">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-the-web-app-name"></a><span data-ttu-id="a3f4c-148">Configurer le nom de l’application web</span><span class="sxs-lookup"><span data-stu-id="a3f4c-148">Configure the web app name</span></span>

<span data-ttu-id="a3f4c-149">Vous pouvez conserver le nom de l’application web généré ou le remplacer par un autre nom unique (les caractères valides sont `a-z`, `0-9` et `-`).</span><span class="sxs-lookup"><span data-stu-id="a3f4c-149">You can keep the generated web app name, or change it to another unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="a3f4c-150">Le nom de l’application web est utilisé dans l’URL par défaut de votre application (`<app_name>.azurewebsites.net`, où `<app_name>` est le nom de votre application web).</span><span class="sxs-lookup"><span data-stu-id="a3f4c-150">The web app name is used as part of the default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="a3f4c-151">Le nom de l’application web doit être unique parmi toutes les applications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-151">The web app name needs to be unique across all apps in Azure.</span></span> 

![Boîte de dialogue Créer App Service](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="a3f4c-153">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="a3f4c-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="a3f4c-154">À côté de **Groupe de ressources**, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-154">Next to **Resource Group**, click **New**.</span></span>

![À côté de Groupe de ressources, cliquez sur Nouveau.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="a3f4c-156">Attribuez au groupe de ressources le nom **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-156">Name the resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="a3f4c-157">Ne cliquez pas sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-157">Do not click **Create**.</span></span> <span data-ttu-id="a3f4c-158">Vous devez d’abord configurer une base de données SQL Database dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-158">You first need to set up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="a3f4c-159">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="a3f4c-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="a3f4c-160">À côté de **Plan App Service**, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-160">Next to **App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="a3f4c-161">Dans la boîte de dialogue **Configurer plan App Service** configurez le nouveau plan App Service avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-161">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span></span>

![Créer un plan App Service](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="a3f4c-163">Paramètre</span><span class="sxs-lookup"><span data-stu-id="a3f4c-163">Setting</span></span>  | <span data-ttu-id="a3f4c-164">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="a3f4c-164">Suggested value</span></span> | <span data-ttu-id="a3f4c-165">Pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="a3f4c-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="a3f4c-166">**Plan App Service**</span><span class="sxs-lookup"><span data-stu-id="a3f4c-166">**App Service Plan**</span></span>| <span data-ttu-id="a3f4c-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a3f4c-167">myAppServicePlan</span></span> | [<span data-ttu-id="a3f4c-168">Plans App Service</span><span class="sxs-lookup"><span data-stu-id="a3f4c-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="a3f4c-169">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="a3f4c-169">**Location**</span></span>| <span data-ttu-id="a3f4c-170">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="a3f4c-170">West Europe</span></span> | [<span data-ttu-id="a3f4c-171">Régions Azure</span><span class="sxs-lookup"><span data-stu-id="a3f4c-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="a3f4c-172">**Taille**</span><span class="sxs-lookup"><span data-stu-id="a3f4c-172">**Size**</span></span>| <span data-ttu-id="a3f4c-173">Gratuit</span><span class="sxs-lookup"><span data-stu-id="a3f4c-173">Free</span></span> | [<span data-ttu-id="a3f4c-174">Niveaux de tarification</span><span class="sxs-lookup"><span data-stu-id="a3f4c-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="a3f4c-175">Créer une instance SQL Server</span><span class="sxs-lookup"><span data-stu-id="a3f4c-175">Create a SQL Server instance</span></span>

<span data-ttu-id="a3f4c-176">Pour créer une base de données, il vous faut un [serveur logique Azure SQL Database](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="a3f4c-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="a3f4c-177">Un serveur logique contient un groupe de bases de données gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="a3f4c-178">Sélectionnez **Explorer des services Azure supplémentaires**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-178">Select **Explore additional Azure services**.</span></span>

![Configurer le nom de l’application web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="a3f4c-180">Dans l’onglet **Services**, cliquez sur l’icône **+** en regard de **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-180">In the **Services** tab, click the **+** icon next to **SQL Database**.</span></span> 

![Dans l’onglet Services, cliquez sur l’icône + en regard de SQL Database.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="a3f4c-182">Dans la boîte de dialogue **Configurer la base de données SQL**, cliquez sur **Nouveau** en regard de **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-182">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span></span> 

<span data-ttu-id="a3f4c-183">Un nom de serveur unique est généré.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-183">A unique server name is generated.</span></span> <span data-ttu-id="a3f4c-184">Ce nom est utilisé dans l’URL par défaut de votre serveur logique, `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-184">This name is used as part of the default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="a3f4c-185">Il doit être unique parmi toutes les instances de serveur logique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="a3f4c-186">Vous pouvez modifier le nom du serveur, mais pour ce didacticiel, conservez la valeur générée.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-186">You can change the server name, but for this tutorial, keep the generated value.</span></span>

<span data-ttu-id="a3f4c-187">Ajoutez un nom d’utilisateur administrateur et un mot de passe, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="a3f4c-188">Pour plus d’informations sur la complexité requise des mots de passe, consultez [Stratégie de mot de passe](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="a3f4c-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="a3f4c-189">Gardez en tête ce nom d'utilisateur et ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-189">Remember this username and password.</span></span> <span data-ttu-id="a3f4c-190">Vous en aurez besoin pour gérer l’instance de serveur logique ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-190">You need them to manage the logical server instance later.</span></span>

![Créer une instance SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="a3f4c-192">Création d’une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="a3f4c-192">Create a SQL Database</span></span>

<span data-ttu-id="a3f4c-193">Dans la boîte de dialogue **Configurer la base de données SQL** :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-193">In the **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="a3f4c-194">Conservez le **Nom de base de données** généré par défaut.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-194">Keep the default generated **Database Name**.</span></span>
* <span data-ttu-id="a3f4c-195">Dans **Nom de la chaîne de connexion**, saisissez *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="a3f4c-196">Ce nom doit correspondre à la chaîne de connexion référencée dans *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-196">This name must match the connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="a3f4c-197">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-197">Select **OK**.</span></span>

![Configurer SQL Database](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="a3f4c-199">La boîte de dialogue **Créer App Service** affiche les ressources que vous avez créées.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-199">The **Create App Service** dialog shows the resources you've created.</span></span> <span data-ttu-id="a3f4c-200">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-200">Click **Create**.</span></span> 

![les ressources que vous avez créées](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="a3f4c-202">Une fois que l’Assistant a créé les ressources Azure, il publie votre application ASP.NET sur Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-202">Once the wizard finishes creating the Azure resources, it  publishes your ASP.NET app to Azure.</span></span> <span data-ttu-id="a3f4c-203">Votre navigateur par défaut démarre et se connecte à l’URL de l’application déployée.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-203">Your default browser is launched with the URL to the deployed app.</span></span> 

<span data-ttu-id="a3f4c-204">Ajoutez quelques tâches.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-204">Add a few to-do items.</span></span>

![Application ASP.NET publiée dans une application web Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="a3f4c-206">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="a3f4c-206">Congratulations!</span></span> <span data-ttu-id="a3f4c-207">Votre application ASP.NET orientée données s’exécute dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-the-sql-database-locally"></a><span data-ttu-id="a3f4c-208">Accéder à SQL Database en local</span><span class="sxs-lookup"><span data-stu-id="a3f4c-208">Access the SQL Database locally</span></span>

<span data-ttu-id="a3f4c-209">Visual Studio vous permet d’explorer et de gérer facilement votre nouvelle instance SQL Database dans **l’Explorateur d’objets SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-209">Visual Studio lets you explore and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="a3f4c-210">Créer une connexion à la base de données</span><span class="sxs-lookup"><span data-stu-id="a3f4c-210">Create a database connection</span></span>

<span data-ttu-id="a3f4c-211">Dans le menu **Vue**, sélectionnez **Explorateur d’objets SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-211">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="a3f4c-212">En haut de **l’Explorateur d’objets SQL Server**, cliquez sur le bouton **Ajouter SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-212">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span></span>

### <a name="configure-the-database-connection"></a><span data-ttu-id="a3f4c-213">Configurer la connexion à la base de données</span><span class="sxs-lookup"><span data-stu-id="a3f4c-213">Configure the database connection</span></span>

<span data-ttu-id="a3f4c-214">Dans la boîte de dialogue **Se connecter**, développez le nœud **Azure**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-214">In the **Connect** dialog, expand the **Azure** node.</span></span> <span data-ttu-id="a3f4c-215">Toutes vos instances SQL Database dans Azure sont répertoriées ici.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="a3f4c-216">Sélectionnez la base de données SQL `DotNetAppSqlDb`.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-216">Select the `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="a3f4c-217">La connexion que vous avez créée apparaît automatiquement en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-217">The connection you created earlier is automatically filled at the bottom.</span></span>

<span data-ttu-id="a3f4c-218">Entrez le mot de passe de l’administrateur de base de données que vous avez créé, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-218">Type the database administrator password you created earlier and click **Connect**.</span></span>

![Configurer la connexion à la base de données à partir de Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="a3f4c-220">Autoriser une connexion client à partir de votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="a3f4c-220">Allow client connection from your computer</span></span>

<span data-ttu-id="a3f4c-221">La boîte de dialogue **Créer une nouvelle règle de pare-feu** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-221">The **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="a3f4c-222">Par défaut, votre instance SQL Database n’autorise que les connexions provenant de services Azure, comme votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="a3f4c-223">Pour vous connecter à votre base de données, créez une règle de pare-feu dans l’instance SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-223">To connect to your database, create a firewall rule in the SQL Database instance.</span></span> <span data-ttu-id="a3f4c-224">Cette règle de pare-feu autorise l’adresse IP publique de votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-224">The firewall rule allows the public IP address of your local computer.</span></span>

<span data-ttu-id="a3f4c-225">La boîte de dialogue contient déjà l’adresse IP de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-225">The dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="a3f4c-226">Assurez-vous que la case **Ajouter mon adresse IP cliente** est cochée, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Configuration du pare-feu pour l’instance SQL Database](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="a3f4c-228">Lorsque Visual Studio a créé le paramètre de pare-feu pour votre instance SQL Database, votre connexion s’affiche dans l’**Explorateur d’objets SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-228">Once Visual Studio finishes creating the firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="a3f4c-229">Ici, vous pouvez effectuer les opérations de base de données les plus courantes, par exemple exécuter des requêtes, créer des vues et des procédures stockées, etc.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-229">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="a3f4c-230">Cliquez avec le bouton droit sur la table `Todoes`, puis sélectionnez **Afficher les données**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-230">Right-click on the `Todoes` table and select **View Data**.</span></span> 

![Explorer les objets SQL Database](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="a3f4c-232">Mettre à jour l’application avec les Code First Migrations</span><span class="sxs-lookup"><span data-stu-id="a3f4c-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="a3f4c-233">Vous pouvez utiliser les outils que vous connaissez dans Visual Studio pour mettre à jour votre base de données et votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-233">You can use the familiar tools in Visual Studio to update your database and web app in Azure.</span></span> <span data-ttu-id="a3f4c-234">Dans cette étape, vous allez utiliser des Code First Migrations dans Entity Framework pour apporter une modification à votre schéma de base de données et la publier sur Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-234">In this step, you use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span></span>

<span data-ttu-id="a3f4c-235">Pour plus d’informations sur l’utilisation de Migrations Entity Framework Code First, consultez [Getting Started with Entity Framework 6 Code First using MVC 5 (Mise en route avec Entity Framework 6 Code First à l’aide de MVC 5)](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="a3f4c-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="a3f4c-236">Mettre à jour votre modèle de données</span><span class="sxs-lookup"><span data-stu-id="a3f4c-236">Update your data model</span></span>

<span data-ttu-id="a3f4c-237">Ouvrez _Models\Todo.cs_ dans l’éditeur de code.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-237">Open _Models\Todo.cs_ in the code editor.</span></span> <span data-ttu-id="a3f4c-238">Ajoutez la propriété suivante à la classe `ToDo` :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-238">Add the following property to the `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="a3f4c-239">Exécuter la fonction Code First Migrations en local</span><span class="sxs-lookup"><span data-stu-id="a3f4c-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="a3f4c-240">Exécutez quelques commandes pour mettre à jour votre base de données locale.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-240">Run a few commands to make updates to your local database.</span></span> 

<span data-ttu-id="a3f4c-241">Dans le menu **Outils**, cliquez sur **Gestionnaire de package NuGet** > **Console du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-241">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="a3f4c-242">Dans la fenêtre de Console du Gestionnaire de package, activez les Migrations Code First :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-242">In the Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="a3f4c-243">Ajoutez une migration :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="a3f4c-244">Mettez à jour la base de données locale :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-244">Update the local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="a3f4c-245">Entrez `Ctrl+F5` pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-245">Type `Ctrl+F5` to run the app.</span></span> <span data-ttu-id="a3f4c-246">Testez les liens de modification, de détails et de création.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-246">Test the edit, details, and create links.</span></span>

<span data-ttu-id="a3f4c-247">Si l’application se charge sans erreur, cela signifie que la fonction Code First Migrations a réussi.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-247">If the application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="a3f4c-248">Votre page garde cependant le même aspect car votre logique d’application n’utilise pas encore cette nouvelle propriété.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-248">However, your page still looks the same because your application logic is not using this new property yet.</span></span> 

### <a name="use-the-new-property"></a><span data-ttu-id="a3f4c-249">Utiliser la nouvelle propriété</span><span class="sxs-lookup"><span data-stu-id="a3f4c-249">Use the new property</span></span>

<span data-ttu-id="a3f4c-250">Apportez quelques modifications à votre code pour utiliser la propriété `Done`.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-250">Make some changes in your code to use the `Done` property.</span></span> <span data-ttu-id="a3f4c-251">Pour plus de simplicité dans ce didacticiel, vous allez uniquement modifier les vues `Index` et `Create` pour voir la propriété en action.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-251">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span></span>

<span data-ttu-id="a3f4c-252">Ouvrez _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="a3f4c-253">Recherchez la méthode `Create()` et ajoutez `Done` à la liste des propriétés dans l’attribut `Bind`.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-253">Find the `Create()` method and add `Done` to the list of properties in the `Bind` attribute.</span></span> <span data-ttu-id="a3f4c-254">Lorsque vous avez terminé, la signature de votre méthode `Create()` doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-254">When you're done, your `Create()` method signature looks like the following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="a3f4c-255">Ouvrez _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="a3f4c-256">Dans le code Razor, vous devriez voir un élément `<div class="form-group">` qui utilise `model.Description` et un autre élément `<div class="form-group">` qui utilise `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-256">In the Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="a3f4c-257">Juste après ces deux éléments, ajoutez un autre élément `<div class="form-group">` qui utilise `model.Done` :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

<span data-ttu-id="a3f4c-258">Ouvrez _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="a3f4c-259">Recherchez l’élément `<th></th>` vide.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-259">Search for the empty `<th></th>` element.</span></span> <span data-ttu-id="a3f4c-260">Juste au-dessus de cet élément, ajoutez le code Razor suivant :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-260">Just above this element, add the following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="a3f4c-261">Recherchez l’élément `<td>` contenant les méthodes d’assistance `Html.ActionLink()`.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-261">Find the `<td>` element that contains the `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="a3f4c-262">Juste au-dessus de cet élément, ajoutez le code Razor suivant :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-262">Just above this element, add the following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="a3f4c-263">Voilà tout ce que vous avez à faire pour voir les modifications dans les vues `Index` et `Create`.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-263">That's all you need to see the changes in the `Index` and `Create` views.</span></span> 

<span data-ttu-id="a3f4c-264">Entrez `Ctrl+F5` pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-264">Type `Ctrl+F5` to run the app.</span></span>

<span data-ttu-id="a3f4c-265">Vous pouvez maintenant ajouter un élément de tâche et cocher **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="a3f4c-266">Cette tâche devrait ensuite apparaître dans votre page d’accueil comme un élément terminé.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="a3f4c-267">N’oubliez pas que la vue `Edit` n’affiche pas le champ `Done`, car vous n’avez pas modifié la vue `Edit`.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-267">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="a3f4c-268">Activer Code First Migrations dans Azure</span><span class="sxs-lookup"><span data-stu-id="a3f4c-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="a3f4c-269">Maintenant que votre changement de code fonctionne, y compris la migration de la base de données, vous allez le publiez dans votre application web Azure et mettre également à jour votre instance SQL Database avec Code First Migrations.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-269">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="a3f4c-270">Comme précédemment, cliquez avec le bouton droit sur votre projet et sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="a3f4c-271">Cliquez sur **Paramètres** pour ouvrir l’Assistant Publication.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-271">Click **Settings** to open the publish wizard.</span></span>

![Ouvrir les paramètres de publication](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="a3f4c-273">Dans l’assistant, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-273">In the wizard, click **Next**.</span></span>

<span data-ttu-id="a3f4c-274">Assurez-vous que la chaîne de connexion pour votre instance SQL Database est renseignée dans **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-274">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="a3f4c-275">Vous devrez peut-être sélectionner la base de données **myToDoAppDb** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-275">You may need to select the **myToDoAppDb** database from the dropdown.</span></span> 

<span data-ttu-id="a3f4c-276">Sélectionnez **Exécuter les migrations Code First (s’exécute au démarrage de l’application)**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Activer Code First Migrations dans l’application web Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="a3f4c-278">Publier vos modifications</span><span class="sxs-lookup"><span data-stu-id="a3f4c-278">Publish your changes</span></span>

<span data-ttu-id="a3f4c-279">Maintenant que vous avez activé les Migrations Code First dans votre application web Azure, publiez vos modifications du code.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="a3f4c-280">Dans la page de publication, cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-280">In the publish page, click **Publish**.</span></span>

<span data-ttu-id="a3f4c-281">Essayez d’ajouter à nouveau des tâches et de sélectionner **Terminé** : elles doivent apparaître dans votre page d’accueil comme éléments terminés.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Application web Azure après l’activation de Code First Migration](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="a3f4c-283">Toutes les tâches existantes sont toujours affichées.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="a3f4c-284">Lorsque vous republiez votre application ASP.NET, les données existantes dans votre instance SQL Database ne sont pas perdues.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="a3f4c-285">En outre, Code First Migrations modifie uniquement le schéma de données, sans toucher à vos données existantes.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-285">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="a3f4c-286">Diffuser les journaux d’applications</span><span class="sxs-lookup"><span data-stu-id="a3f4c-286">Stream application logs</span></span>

<span data-ttu-id="a3f4c-287">Vous pouvez diffuser des messages de suivi directement entre votre application web Azure et Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-287">You can stream tracing messages directly from your Azure web app to Visual Studio.</span></span>

<span data-ttu-id="a3f4c-288">Ouvrez _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="a3f4c-289">Chaque action commence par une méthode `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="a3f4c-290">Ce code est ajouté pour vous montrer comment ajouter des messages de trace à votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-290">This code is added to show you how to add trace messages to your Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="a3f4c-291">Ouvrir l’Explorateur de serveurs</span><span class="sxs-lookup"><span data-stu-id="a3f4c-291">Open Server Explorer</span></span>

<span data-ttu-id="a3f4c-292">Dans le menu **Vue**, sélectionnez **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-292">From the **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="a3f4c-293">Vous pouvez configurer la journalisation pour votre application web Azure dans **l’Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="a3f4c-294">Activer la diffusion de journaux</span><span class="sxs-lookup"><span data-stu-id="a3f4c-294">Enable log streaming</span></span>

<span data-ttu-id="a3f4c-295">Dans **l’Explorateur de serveurs**, développez **Azure** > **App Service**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="a3f4c-296">Développez le groupe de ressources **myResourceGroup** que vous avez créé lorsque vous avez créé l’application web Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-296">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span></span>

<span data-ttu-id="a3f4c-297">Cliquez avec le bouton droit sur votre application web Azure et sélectionnez **Afficher les journaux de streaming**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Activer la diffusion de journaux](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="a3f4c-299">Les journaux sont maintenant transmis à la fenêtre **Sortie**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-299">The logs are now streamed into the **Output** window.</span></span> 

![Diffusion des journaux dans la fenêtre Sortie](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="a3f4c-301">Vous ne pourrez cependant pas visualiser les messages de suivi à ce stade.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-301">However, you don't see any of the trace messages yet.</span></span> <span data-ttu-id="a3f4c-302">La raison est simple : lorsque vous sélectionnez **Afficher les journaux de streaming**, votre application web Azure définit le niveau de suivi sur `Error`, ce qui enregistre uniquement les événements d’erreur (avec la méthode `Trace.TraceError()`).</span><span class="sxs-lookup"><span data-stu-id="a3f4c-302">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="a3f4c-303">Modifier les niveaux de suivi</span><span class="sxs-lookup"><span data-stu-id="a3f4c-303">Change trace levels</span></span>

<span data-ttu-id="a3f4c-304">Pour modifier les niveaux de suivi pour générer d’autres messages de suivi, revenez à **l’Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-304">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span></span>

<span data-ttu-id="a3f4c-305">Cliquez de nouveau avec le bouton droit sur votre application web Azure et sélectionnez **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="a3f4c-306">Dans la liste déroulante **Journal des applications (Système de fichiers)**, sélectionnez **Détaillé**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-306">In the **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="a3f4c-307">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-307">Click **Save**.</span></span>

![Définir le niveau de suivi sur Détaillé](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="a3f4c-309">Vous pouvez expérimenter différents niveaux de suivi pour connaître les types de messages qui s’affichent pour chaque niveau.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-309">You can experiment with different trace levels to see what types of messages are displayed for each level.</span></span> <span data-ttu-id="a3f4c-310">Par exemple, le niveau **Informations** inclut tous les journaux créés par `Trace.TraceInformation()`, `Trace.TraceWarning()`, et `Trace.TraceError()`, mais pas les journaux créés par `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-310">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="a3f4c-311">Dans votre navigateur, essayez de cliquer autour de l’application de la liste des tâches dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-311">In your browser, try clicking around the to-do list application in Azure.</span></span> <span data-ttu-id="a3f4c-312">Les messages de suivi sont maintenant diffusés vers la fenêtre **Sortie** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-312">The trace messages are now streamed to the **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="a3f4c-313">Arrêter la diffusion de journaux</span><span class="sxs-lookup"><span data-stu-id="a3f4c-313">Stop log streaming</span></span>

<span data-ttu-id="a3f4c-314">Pour arrêter le service de diffusion de journaux, cliquez sur le bouton **Arrêter l’analyse** situé dans la fenêtre **Sortie**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-314">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span></span>

![Arrêter la diffusion de journaux](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="a3f4c-316">Gérer votre application web Azure</span><span class="sxs-lookup"><span data-stu-id="a3f4c-316">Manage your Azure web app</span></span>

<span data-ttu-id="a3f4c-317">Accédez au [portail Azure](https://portal.azure.com) pour voir l’application web que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-317">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span> 



<span data-ttu-id="a3f4c-318">Dans le menu de gauche, cliquez sur **App Service**, puis cliquez sur le nom de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-318">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Navigation au sein du portail pour accéder à l’application web Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="a3f4c-320">Vous accédez à la page de votre application web.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="a3f4c-321">Par défaut, le portail affiche la page **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-321">By default, the portal shows the **Overview** page.</span></span> <span data-ttu-id="a3f4c-322">Cette page propose un aperçu de votre application.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="a3f4c-323">Ici, vous pouvez également effectuer des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="a3f4c-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="a3f4c-324">Les onglets sur le côté gauche de la page affichent les différentes pages de configuration que vous pouvez ouvrir.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-324">The tabs on the left side of the page show the different configuration pages you can open.</span></span> 

![Page App Service du Portail Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="a3f4c-326">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a3f4c-326">Next steps</span></span>

<span data-ttu-id="a3f4c-327">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="a3f4c-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3f4c-328">Créer une base de données SQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="a3f4c-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="a3f4c-329">Connecter une application ASP.NET à SQL Database</span><span class="sxs-lookup"><span data-stu-id="a3f4c-329">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="a3f4c-330">Déploiement de l’application dans Azure</span><span class="sxs-lookup"><span data-stu-id="a3f4c-330">Deploy the app to Azure</span></span>
> * <span data-ttu-id="a3f4c-331">Mettre à jour le modèle de données et redéployer l’application</span><span class="sxs-lookup"><span data-stu-id="a3f4c-331">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="a3f4c-332">Diffuser des journaux à partir d’Azure vers votre terminal</span><span class="sxs-lookup"><span data-stu-id="a3f4c-332">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="a3f4c-333">Gérer l’application dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a3f4c-333">Manage the app in the Azure portal</span></span>

<span data-ttu-id="a3f4c-334">Passez au didacticiel suivant pour découvrir comment mapper un nom DNS personnalisé à l’application web.</span><span class="sxs-lookup"><span data-stu-id="a3f4c-334">Advance to the next tutorial to learn how to map a custom DNS name to the web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a3f4c-335">Mapper un nom DNS personnalisé existant à des applications web Azure</span><span class="sxs-lookup"><span data-stu-id="a3f4c-335">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
