---
title: "aaaBuild une application ASP.NET dans Azure avec la base de données SQL | Documents Microsoft"
description: "Découvrez comment tooget un ASP.NET application fonctionne dans Azure, avec tooa de connexion de base de données SQL."
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
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="ae78e-103">Création d’une application ASP.NET dans Azure avec SQL Database</span><span class="sxs-lookup"><span data-stu-id="ae78e-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="ae78e-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="ae78e-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="ae78e-105">Ce didacticiel vous montre comment toodeploy un ASP.NET piloté par les données de l’application dans Azure web et le connecter trop[base de données SQL Azure](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae78e-105">This tutorial shows you how toodeploy a data-driven ASP.NET web app in Azure and connect it too[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="ae78e-106">Lorsque vous avez terminé, vous disposez d’une application ASP.NET en cours d’exécution [Azure App Service](../app-service/app-service-value-prop-what-is.md) et connecté tooSQL de base de données.</span><span class="sxs-lookup"><span data-stu-id="ae78e-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected tooSQL Database.</span></span>

![Application ASP.NET publiée dans une application web Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="ae78e-108">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ae78e-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ae78e-109">Créer une base de données SQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="ae78e-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="ae78e-110">Se connecter à un tooSQL d’application ASP.NET de base de données</span><span class="sxs-lookup"><span data-stu-id="ae78e-110">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="ae78e-111">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="ae78e-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="ae78e-112">Mettre à jour le modèle de données hello et redéployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="ae78e-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="ae78e-113">Journaux des flux de données à partir d’Azure tooyour Terminal Server</span><span class="sxs-lookup"><span data-stu-id="ae78e-113">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="ae78e-114">Gérer l’application hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="ae78e-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae78e-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ae78e-115">Prerequisites</span></span>

<span data-ttu-id="ae78e-116">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="ae78e-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="ae78e-117">Installer [Visual Studio 2017](https://www.visualstudio.com/downloads/) avec hello suivant les charges de travail :</span><span class="sxs-lookup"><span data-stu-id="ae78e-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
  - <span data-ttu-id="ae78e-118">**Développement web et ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="ae78e-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="ae78e-119">**Développement Azure**</span><span class="sxs-lookup"><span data-stu-id="ae78e-119">**Azure development**</span></span>

  ![Développement web et ASP.NET et Développement Azure (sous Web et cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="ae78e-121">Télécharger l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="ae78e-121">Download hello sample</span></span>

<span data-ttu-id="ae78e-122">[Télécharger l’exemple de projet hello](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="ae78e-122">[Download hello sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="ae78e-123">Extraire (décompresser) hello *dotnet-sqldb-didacticiel-master.zip* fichier.</span><span class="sxs-lookup"><span data-stu-id="ae78e-123">Extract (unzip) hello  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="ae78e-124">exemple de projet Hello contient une basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-lecture-mise à jour-suppression) à l’aide d’application [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="ae78e-124">hello sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-hello-app"></a><span data-ttu-id="ae78e-125">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="ae78e-125">Run hello app</span></span>

<span data-ttu-id="ae78e-126">Ouvrez hello *dotnet-sqldb-didacticiel-master/DotNetAppSqlDb.sln* fichier dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae78e-126">Open hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="ae78e-127">Type `Ctrl+F5` application hello de toorun sans débogage.</span><span class="sxs-lookup"><span data-stu-id="ae78e-127">Type `Ctrl+F5` toorun hello app without debugging.</span></span> <span data-ttu-id="ae78e-128">application Hello s’affiche dans votre navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="ae78e-128">hello app is displayed in your default browser.</span></span> <span data-ttu-id="ae78e-129">Sélectionnez hello **créer un nouveau** lier et créer quelques *action* éléments.</span><span class="sxs-lookup"><span data-stu-id="ae78e-129">Select hello **Create New** link and create a couple *to-do* items.</span></span> 

![Boîte de dialogue New ASP.NET Project](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="ae78e-131">Hello de test **modifier**, **détails**, et **supprimer** des liens.</span><span class="sxs-lookup"><span data-stu-id="ae78e-131">Test hello **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="ae78e-132">application Hello utilise un tooconnect de contexte de base de données avec la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="ae78e-132">hello app uses a database context tooconnect with hello database.</span></span> <span data-ttu-id="ae78e-133">Dans cet exemple, le contexte de base de données hello utilise une chaîne de connexion nommée `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="ae78e-133">In this sample, hello database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="ae78e-134">chaîne de connexion Hello est définie dans hello *Web.config* de fichiers et référencé dans hello *Models/MyDatabaseContext.cs* fichier.</span><span class="sxs-lookup"><span data-stu-id="ae78e-134">hello connection string is set in hello *Web.config* file and referenced in hello *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="ae78e-135">nom de chaîne de connexion Hello est utilisé ultérieurement dans Azure web application tooan base de données SQL Azure hello tooconnect didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="ae78e-135">hello connection string name is used later in hello tutorial tooconnect hello Azure web app tooan Azure SQL Database.</span></span> 

## <a name="publish-tooazure-with-sql-database"></a><span data-ttu-id="ae78e-136">Publier tooAzure avec la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="ae78e-136">Publish tooAzure with SQL Database</span></span>

<span data-ttu-id="ae78e-137">Bonjour **l’Explorateur de solutions**, cliquez sur votre **DotNetAppSqlDb** de projet et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-137">In hello **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publier à partir de l’Explorateur de solutions](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="ae78e-139">Assurez-vous que **Microsoft Azure App Service** est sélectionné et cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publier à partir de la page de présentation du projet](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="ae78e-141">Publication ouvre hello **créer un Service application** boîte de dialogue, qui vous permet de créer tous les hello ressources Azure, vous devez toorun votre application de web ASP.NET dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ae78e-141">Publishing opens hello **Create App Service** dialog, which helps you create all hello Azure resources you need toorun your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="ae78e-142">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="ae78e-142">Sign in tooAzure</span></span>

<span data-ttu-id="ae78e-143">Bonjour **créer un Service application** boîte de dialogue, cliquez sur **ajouter un compte**, puis connectez-vous à tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ae78e-143">In hello **Create App Service** dialog, click **Add an account**, and then sign in tooyour Azure subscription.</span></span> <span data-ttu-id="ae78e-144">Si vous êtes déjà connecté à un compte Microsoft, assurez-vous que le compte conserve votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ae78e-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="ae78e-145">Si votre abonnement Azure n’a pas hello signé Microsoft compte, cliquez dessus compte tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="ae78e-145">If hello signed-in Microsoft account doesn't have your Azure subscription, click it tooadd hello correct account.</span></span>
   
![Connectez-vous à tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="ae78e-147">Une fois connecté, vous êtes prêt toocreate que tous hello ressources dont vous avez besoin pour votre application web Azure dans cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ae78e-147">Once signed in, you're ready toocreate all hello resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-hello-web-app-name"></a><span data-ttu-id="ae78e-148">Configurer le nom de l’application hello web</span><span class="sxs-lookup"><span data-stu-id="ae78e-148">Configure hello web app name</span></span>

<span data-ttu-id="ae78e-149">Vous pouvez conserver le nom de l’application web hello généré, ou modifier le nom unique de tooanother (les caractères valides sont `a-z`, `0-9`, et `-`).</span><span class="sxs-lookup"><span data-stu-id="ae78e-149">You can keep hello generated web app name, or change it tooanother unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="ae78e-150">nom de l’application web Hello est utilisé dans le cadre de l’URL par défaut de hello pour votre application (`<app_name>.azurewebsites.net`, où `<app_name>` est le nom de votre application web).</span><span class="sxs-lookup"><span data-stu-id="ae78e-150">hello web app name is used as part of hello default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="ae78e-151">nom de l’application web Hello doit toobe unique entre toutes les applications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ae78e-151">hello web app name needs toobe unique across all apps in Azure.</span></span> 

![Boîte de dialogue Créer App Service](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="ae78e-153">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="ae78e-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="ae78e-154">Suivant trop**groupe de ressources**, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-154">Next too**Resource Group**, click **New**.</span></span>

![TooResource suivant groupe, cliquez sur Nouveau.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="ae78e-156">Groupe de ressources de nom hello **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-156">Name hello resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="ae78e-157">Ne cliquez pas sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-157">Do not click **Create**.</span></span> <span data-ttu-id="ae78e-158">Vous devez tout d’abord tooset une base de données SQL dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ae78e-158">You first need tooset up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="ae78e-159">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="ae78e-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="ae78e-160">Suivant trop**du Plan App Service**, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-160">Next too**App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="ae78e-161">Bonjour **configurer un Plan App Service** boîte de dialogue Configurer le nouveau plan de Service de l’application hello avec hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="ae78e-161">In hello **Configure App Service Plan** dialog, configure hello new App Service plan with hello following settings:</span></span>

![Créer un plan App Service](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="ae78e-163">Paramètre</span><span class="sxs-lookup"><span data-stu-id="ae78e-163">Setting</span></span>  | <span data-ttu-id="ae78e-164">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="ae78e-164">Suggested value</span></span> | <span data-ttu-id="ae78e-165">Pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="ae78e-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="ae78e-166">**Plan App Service**</span><span class="sxs-lookup"><span data-stu-id="ae78e-166">**App Service Plan**</span></span>| <span data-ttu-id="ae78e-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="ae78e-167">myAppServicePlan</span></span> | [<span data-ttu-id="ae78e-168">Plans App Service</span><span class="sxs-lookup"><span data-stu-id="ae78e-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="ae78e-169">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="ae78e-169">**Location**</span></span>| <span data-ttu-id="ae78e-170">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="ae78e-170">West Europe</span></span> | [<span data-ttu-id="ae78e-171">Régions Azure</span><span class="sxs-lookup"><span data-stu-id="ae78e-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="ae78e-172">**Taille**</span><span class="sxs-lookup"><span data-stu-id="ae78e-172">**Size**</span></span>| <span data-ttu-id="ae78e-173">Gratuit</span><span class="sxs-lookup"><span data-stu-id="ae78e-173">Free</span></span> | [<span data-ttu-id="ae78e-174">Niveaux de tarification</span><span class="sxs-lookup"><span data-stu-id="ae78e-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="ae78e-175">Créer une instance SQL Server</span><span class="sxs-lookup"><span data-stu-id="ae78e-175">Create a SQL Server instance</span></span>

<span data-ttu-id="ae78e-176">Pour créer une base de données, il vous faut un [serveur logique Azure SQL Database](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="ae78e-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="ae78e-177">Un serveur logique contient un groupe de bases de données gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="ae78e-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="ae78e-178">Sélectionnez **Explorer des services Azure supplémentaires**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-178">Select **Explore additional Azure services**.</span></span>

![Configurer le nom de l’application web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="ae78e-180">Bonjour **Services** , cliquez sur hello  **+**  icône suivant trop**base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-180">In hello **Services** tab, click hello **+** icon next too**SQL Database**.</span></span> 

![Dans l’onglet Services de hello, cliquez sur l’icône + hello tooSQL suivant de base de données.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="ae78e-182">Bonjour **configurer la base de données SQL** boîte de dialogue, cliquez sur **nouveau** suivant trop**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-182">In hello **Configure SQL Database** dialog, click **New** next too**SQL Server**.</span></span> 

<span data-ttu-id="ae78e-183">Un nom de serveur unique est généré.</span><span class="sxs-lookup"><span data-stu-id="ae78e-183">A unique server name is generated.</span></span> <span data-ttu-id="ae78e-184">Ce nom est utilisé dans le cadre de l’URL par défaut de hello pour votre serveur logique, `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="ae78e-184">This name is used as part of hello default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="ae78e-185">Il doit être unique parmi toutes les instances de serveur logique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ae78e-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="ae78e-186">Vous pouvez modifier le nom du serveur hello, mais pour ce didacticiel, conservez la valeur de l’hello généré.</span><span class="sxs-lookup"><span data-stu-id="ae78e-186">You can change hello server name, but for this tutorial, keep hello generated value.</span></span>

<span data-ttu-id="ae78e-187">Ajoutez un nom d’utilisateur administrateur et un mot de passe, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="ae78e-188">Pour plus d’informations sur la complexité requise des mots de passe, consultez [Stratégie de mot de passe](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="ae78e-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="ae78e-189">Gardez en tête ce nom d'utilisateur et ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ae78e-189">Remember this username and password.</span></span> <span data-ttu-id="ae78e-190">Vous avez besoin serveur logique de hello toomanage instance ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="ae78e-190">You need them toomanage hello logical server instance later.</span></span>

![Créer une instance SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="ae78e-192">Création d’une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="ae78e-192">Create a SQL Database</span></span>

<span data-ttu-id="ae78e-193">Bonjour **configurer la base de données SQL** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="ae78e-193">In hello **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="ae78e-194">Conservez généré de la valeur par défaut hello **nom de la base de données**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-194">Keep hello default generated **Database Name**.</span></span>
* <span data-ttu-id="ae78e-195">Dans **Nom de la chaîne de connexion**, saisissez *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="ae78e-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="ae78e-196">Ce nom doit correspondre la chaîne de connexion hello qui est référencé dans *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="ae78e-196">This name must match hello connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="ae78e-197">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-197">Select **OK**.</span></span>

![Configurer SQL Database](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="ae78e-199">Hello **créer un Service application** boîte de dialogue affiche les ressources hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="ae78e-199">hello **Create App Service** dialog shows hello resources you've created.</span></span> <span data-ttu-id="ae78e-200">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-200">Click **Create**.</span></span> 

![ressources Hello que vous avez créé](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="ae78e-202">Une fois l’Assistant de hello ait fini de créer des ressources Azure hello, elle publie votre tooAzure d’application ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ae78e-202">Once hello wizard finishes creating hello Azure resources, it  publishes your ASP.NET app tooAzure.</span></span> <span data-ttu-id="ae78e-203">Votre navigateur par défaut est lancé avec application de hello URL toohello déployé.</span><span class="sxs-lookup"><span data-stu-id="ae78e-203">Your default browser is launched with hello URL toohello deployed app.</span></span> 

<span data-ttu-id="ae78e-204">Ajoutez quelques tâches.</span><span class="sxs-lookup"><span data-stu-id="ae78e-204">Add a few to-do items.</span></span>

![Application ASP.NET publiée dans une application web Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="ae78e-206">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="ae78e-206">Congratulations!</span></span> <span data-ttu-id="ae78e-207">Votre application ASP.NET orientée données s’exécute dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ae78e-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-hello-sql-database-locally"></a><span data-ttu-id="ae78e-208">Accéder localement hello de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="ae78e-208">Access hello SQL Database locally</span></span>

<span data-ttu-id="ae78e-209">Visual Studio vous permet d’Explorer et gérer votre nouvelle base de données SQL facilement dans hello **l’Explorateur d’objets SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-209">Visual Studio lets you explore and manage your new SQL Database easily in hello **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="ae78e-210">Créer une connexion à la base de données</span><span class="sxs-lookup"><span data-stu-id="ae78e-210">Create a database connection</span></span>

<span data-ttu-id="ae78e-211">À partir de hello **vue** menu, sélectionnez **l’Explorateur d’objets SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-211">From hello **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="ae78e-212">Haut hello **l’Explorateur d’objets SQL Server**, cliquez sur hello **ajouter SQL Server** bouton.</span><span class="sxs-lookup"><span data-stu-id="ae78e-212">At hello top of **SQL Server Object Explorer**, click hello **Add SQL Server** button.</span></span>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="ae78e-213">Configurer la connexion de base de données hello</span><span class="sxs-lookup"><span data-stu-id="ae78e-213">Configure hello database connection</span></span>

<span data-ttu-id="ae78e-214">Bonjour **Connect** boîte de dialogue, développez hello **Azure** nœud.</span><span class="sxs-lookup"><span data-stu-id="ae78e-214">In hello **Connect** dialog, expand hello **Azure** node.</span></span> <span data-ttu-id="ae78e-215">Toutes vos instances SQL Database dans Azure sont répertoriées ici.</span><span class="sxs-lookup"><span data-stu-id="ae78e-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="ae78e-216">Sélectionnez hello `DotNetAppSqlDb` base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="ae78e-216">Select hello `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="ae78e-217">connexion Hello que vous avez créé précédemment est renseignée automatiquement en bas de hello.</span><span class="sxs-lookup"><span data-stu-id="ae78e-217">hello connection you created earlier is automatically filled at hello bottom.</span></span>

<span data-ttu-id="ae78e-218">Tapez le mot de passe administrateur de base de données hello vous avez créé précédemment et cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-218">Type hello database administrator password you created earlier and click **Connect**.</span></span>

![Configurer la connexion à la base de données à partir de Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="ae78e-220">Autoriser une connexion client à partir de votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="ae78e-220">Allow client connection from your computer</span></span>

<span data-ttu-id="ae78e-221">Hello **créer une nouvelle règle de pare-feu** boîte de dialogue est ouverte.</span><span class="sxs-lookup"><span data-stu-id="ae78e-221">hello **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="ae78e-222">Par défaut, votre instance SQL Database n’autorise que les connexions provenant de services Azure, comme votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="ae78e-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="ae78e-223">tooconnect tooyour de base de données, créer une règle de pare-feu dans l’instance de base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="ae78e-223">tooconnect tooyour database, create a firewall rule in hello SQL Database instance.</span></span> <span data-ttu-id="ae78e-224">règle de pare-feu Hello permet hello adresse IP publique de votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ae78e-224">hello firewall rule allows hello public IP address of your local computer.</span></span>

<span data-ttu-id="ae78e-225">boîte de dialogue Hello est déjà remplie avec l’adresse IP de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ae78e-225">hello dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="ae78e-226">Assurez-vous que la case **Ajouter mon adresse IP cliente** est cochée, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Configuration du pare-feu pour l’instance SQL Database](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="ae78e-228">Une fois que Visual Studio a terminé la création du paramètre de pare-feu hello pour votre instance de base de données SQL, votre connexion s’affiche dans **l’Explorateur d’objets SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-228">Once Visual Studio finishes creating hello firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="ae78e-229">Ici, vous pouvez effectuer hello de base de données opérations les plus courantes, telles que les requêtes de l’exécution, créent des vues et procédures stockées et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="ae78e-229">Here, you can perform hello most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="ae78e-230">Avec le bouton droit sur hello `Todoes` de table et sélectionnez **des données d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-230">Right-click on hello `Todoes` table and select **View Data**.</span></span> 

![Explorer les objets SQL Database](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="ae78e-232">Mettre à jour l’application avec les Code First Migrations</span><span class="sxs-lookup"><span data-stu-id="ae78e-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="ae78e-233">Vous pouvez utiliser des outils familiers de hello dans Visual Studio tooupdate votre base de données et l’application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ae78e-233">You can use hello familiar tools in Visual Studio tooupdate your database and web app in Azure.</span></span> <span data-ttu-id="ae78e-234">Dans cette étape, vous utilisez Migrations Code First dans Entity Framework toomake un schéma de base de données modifiées tooyour et publiez tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ae78e-234">In this step, you use Code First Migrations in Entity Framework toomake a change tooyour database schema and publish it tooAzure.</span></span>

<span data-ttu-id="ae78e-235">Pour plus d’informations sur l’utilisation de Migrations Entity Framework Code First, consultez [Getting Started with Entity Framework 6 Code First using MVC 5 (Mise en route avec Entity Framework 6 Code First à l’aide de MVC 5)](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="ae78e-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="ae78e-236">Mettre à jour votre modèle de données</span><span class="sxs-lookup"><span data-stu-id="ae78e-236">Update your data model</span></span>

<span data-ttu-id="ae78e-237">Ouvrez _Models\Todo.cs_ dans l’éditeur de code hello.</span><span class="sxs-lookup"><span data-stu-id="ae78e-237">Open _Models\Todo.cs_ in hello code editor.</span></span> <span data-ttu-id="ae78e-238">Ajouter hello suivant propriété toohello `ToDo` classe :</span><span class="sxs-lookup"><span data-stu-id="ae78e-238">Add hello following property toohello `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="ae78e-239">Exécuter la fonction Code First Migrations en local</span><span class="sxs-lookup"><span data-stu-id="ae78e-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="ae78e-240">Exécuter quelques commandes toomake mises à jour tooyour base de données locale.</span><span class="sxs-lookup"><span data-stu-id="ae78e-240">Run a few commands toomake updates tooyour local database.</span></span> 

<span data-ttu-id="ae78e-241">À partir de hello **outils** menu, cliquez sur **Gestionnaire de Package NuGet** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-241">From hello **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="ae78e-242">Dans la fenêtre de Console du Gestionnaire de Package de hello, activer les Migrations Code First :</span><span class="sxs-lookup"><span data-stu-id="ae78e-242">In hello Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="ae78e-243">Ajoutez une migration :</span><span class="sxs-lookup"><span data-stu-id="ae78e-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="ae78e-244">Mise à jour de la base de données locale hello :</span><span class="sxs-lookup"><span data-stu-id="ae78e-244">Update hello local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="ae78e-245">Type `Ctrl+F5` toorun hello application.</span><span class="sxs-lookup"><span data-stu-id="ae78e-245">Type `Ctrl+F5` toorun hello app.</span></span> <span data-ttu-id="ae78e-246">Hello de test, modifier les détails et créer des liens.</span><span class="sxs-lookup"><span data-stu-id="ae78e-246">Test hello edit, details, and create links.</span></span>

<span data-ttu-id="ae78e-247">Si l’application hello se charge sans erreur, les Migrations Code First a réussi.</span><span class="sxs-lookup"><span data-stu-id="ae78e-247">If hello application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="ae78e-248">Toutefois, votre recherche toujours page hello identiques car votre logique d’application n’utilise pas encore cette nouvelle propriété.</span><span class="sxs-lookup"><span data-stu-id="ae78e-248">However, your page still looks hello same because your application logic is not using this new property yet.</span></span> 

### <a name="use-hello-new-property"></a><span data-ttu-id="ae78e-249">Utiliser la nouvelle propriété de hello</span><span class="sxs-lookup"><span data-stu-id="ae78e-249">Use hello new property</span></span>

<span data-ttu-id="ae78e-250">Apportez des modifications à votre hello toouse de code `Done` propriété.</span><span class="sxs-lookup"><span data-stu-id="ae78e-250">Make some changes in your code toouse hello `Done` property.</span></span> <span data-ttu-id="ae78e-251">Par souci de simplicité dans ce didacticiel, vous allez uniquement toochange hello `Index` et `Create` affiche la propriété de hello toosee en action.</span><span class="sxs-lookup"><span data-stu-id="ae78e-251">For simplicity in this tutorial, you're only going toochange hello `Index` and `Create` views toosee hello property in action.</span></span>

<span data-ttu-id="ae78e-252">Ouvrez _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="ae78e-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="ae78e-253">Recherche hello `Create()` (méthode) et ajoutez `Done` toohello la liste des propriétés Bonjour `Bind` attribut.</span><span class="sxs-lookup"><span data-stu-id="ae78e-253">Find hello `Create()` method and add `Done` toohello list of properties in hello `Bind` attribute.</span></span> <span data-ttu-id="ae78e-254">Lorsque vous avez terminé, votre `Create()` signature de méthode ressemble à hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="ae78e-254">When you're done, your `Create()` method signature looks like hello following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="ae78e-255">Ouvrez _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="ae78e-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="ae78e-256">Bonjour code Razor, vous devez voir un `<div class="form-group">` élément utilise `model.Description`et un autre `<div class="form-group">` élément utilise `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="ae78e-256">In hello Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="ae78e-257">Juste après ces deux éléments, ajoutez un autre élément `<div class="form-group">` qui utilise `model.Done` :</span><span class="sxs-lookup"><span data-stu-id="ae78e-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

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

<span data-ttu-id="ae78e-258">Ouvrez _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="ae78e-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="ae78e-259">Recherchez hello vide `<th></th>` élément.</span><span class="sxs-lookup"><span data-stu-id="ae78e-259">Search for hello empty `<th></th>` element.</span></span> <span data-ttu-id="ae78e-260">Juste au-dessus de cet élément, ajoutez hello suivant de code Razor :</span><span class="sxs-lookup"><span data-stu-id="ae78e-260">Just above this element, add hello following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="ae78e-261">Recherche hello `<td>` élément contenant hello `Html.ActionLink()` méthodes d’assistance.</span><span class="sxs-lookup"><span data-stu-id="ae78e-261">Find hello `<td>` element that contains hello `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="ae78e-262">Juste au-dessus de cet élément, ajoutez hello suivant de code Razor :</span><span class="sxs-lookup"><span data-stu-id="ae78e-262">Just above this element, add hello following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="ae78e-263">Que vous n’avez rien toosee des modifications de hello Bonjour `Index` et `Create` vues.</span><span class="sxs-lookup"><span data-stu-id="ae78e-263">That's all you need toosee hello changes in hello `Index` and `Create` views.</span></span> 

<span data-ttu-id="ae78e-264">Type `Ctrl+F5` toorun hello application.</span><span class="sxs-lookup"><span data-stu-id="ae78e-264">Type `Ctrl+F5` toorun hello app.</span></span>

<span data-ttu-id="ae78e-265">Vous pouvez maintenant ajouter un élément de tâche et cocher **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="ae78e-266">Cette tâche devrait ensuite apparaître dans votre page d’accueil comme un élément terminé.</span><span class="sxs-lookup"><span data-stu-id="ae78e-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="ae78e-267">N’oubliez pas que hello `Edit` vue n’affiche pas hello `Done` champ, car vous n’avez pas modifier hello `Edit` vue.</span><span class="sxs-lookup"><span data-stu-id="ae78e-267">Remember that hello `Edit` view doesn't show hello `Done` field, because you didn't change hello `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="ae78e-268">Activer Code First Migrations dans Azure</span><span class="sxs-lookup"><span data-stu-id="ae78e-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="ae78e-269">Maintenant que votre code modifier fonctionne, dont la migration de la base de données, vous publiez tooyour Azure web app et mettre à jour trop de votre base de données SQL avec les Migrations Code First.</span><span class="sxs-lookup"><span data-stu-id="ae78e-269">Now that your code change works, including database migration, you publish it tooyour Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="ae78e-270">Comme précédemment, cliquez avec le bouton droit sur votre projet et sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="ae78e-271">Cliquez sur **paramètres** tooopen hello Assistant de publication.</span><span class="sxs-lookup"><span data-stu-id="ae78e-271">Click **Settings** tooopen hello publish wizard.</span></span>

![Ouvrir les paramètres de publication](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="ae78e-273">Dans l’Assistant de hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-273">In hello wizard, click **Next**.</span></span>

<span data-ttu-id="ae78e-274">Assurez-vous que cette chaîne de connexion hello pour votre base de données SQL est remplie dans **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-274">Make sure that hello connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="ae78e-275">Vous devrez peut-être tooselect hello **myToDoAppDb** base de données à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="ae78e-275">You may need tooselect hello **myToDoAppDb** database from hello dropdown.</span></span> 

<span data-ttu-id="ae78e-276">Sélectionnez **Exécuter les migrations Code First (s’exécute au démarrage de l’application)**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Activer Code First Migrations dans l’application web Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="ae78e-278">Publier vos modifications</span><span class="sxs-lookup"><span data-stu-id="ae78e-278">Publish your changes</span></span>

<span data-ttu-id="ae78e-279">Maintenant que vous avez activé les Migrations Code First dans votre application web Azure, publiez vos modifications du code.</span><span class="sxs-lookup"><span data-stu-id="ae78e-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="ae78e-280">Bonjour, page Publier, cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-280">In hello publish page, click **Publish**.</span></span>

<span data-ttu-id="ae78e-281">Essayez d’ajouter à nouveau des tâches et de sélectionner **Terminé** : elles doivent apparaître dans votre page d’accueil comme éléments terminés.</span><span class="sxs-lookup"><span data-stu-id="ae78e-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Application web Azure après l’activation de Code First Migration](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="ae78e-283">Toutes les tâches existantes sont toujours affichées.</span><span class="sxs-lookup"><span data-stu-id="ae78e-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="ae78e-284">Lorsque vous republiez votre application ASP.NET, les données existantes dans votre instance SQL Database ne sont pas perdues.</span><span class="sxs-lookup"><span data-stu-id="ae78e-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="ae78e-285">En outre, les Migrations Code First modifie uniquement schéma de données hello et conserve vos données existantes intact.</span><span class="sxs-lookup"><span data-stu-id="ae78e-285">Also, Code First Migrations only changes hello data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="ae78e-286">Diffuser les journaux d’applications</span><span class="sxs-lookup"><span data-stu-id="ae78e-286">Stream application logs</span></span>

<span data-ttu-id="ae78e-287">Vous pouvez diffuser des messages de suivi directement à partir de votre tooVisual d’application web Azure Studio.</span><span class="sxs-lookup"><span data-stu-id="ae78e-287">You can stream tracing messages directly from your Azure web app tooVisual Studio.</span></span>

<span data-ttu-id="ae78e-288">Ouvrez _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="ae78e-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="ae78e-289">Chaque action commence par une méthode `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="ae78e-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="ae78e-290">Ce code est ajouté tooshow vous comment les messages de trace de tooadd tooyour Azure web app.</span><span class="sxs-lookup"><span data-stu-id="ae78e-290">This code is added tooshow you how tooadd trace messages tooyour Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="ae78e-291">Ouvrir l’Explorateur de serveurs</span><span class="sxs-lookup"><span data-stu-id="ae78e-291">Open Server Explorer</span></span>

<span data-ttu-id="ae78e-292">À partir de hello **vue** menu, sélectionnez **l’Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-292">From hello **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="ae78e-293">Vous pouvez configurer la journalisation pour votre application web Azure dans **l’Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="ae78e-294">Activer la diffusion de journaux</span><span class="sxs-lookup"><span data-stu-id="ae78e-294">Enable log streaming</span></span>

<span data-ttu-id="ae78e-295">Dans **l’Explorateur de serveurs**, développez **Azure** > **App Service**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="ae78e-296">Développez hello **myResourceGroup** groupe de ressources, vous avez créé lors de la création d’application web Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="ae78e-296">Expand hello **myResourceGroup** resource group, you created when you first created hello Azure web app.</span></span>

<span data-ttu-id="ae78e-297">Cliquez avec le bouton droit sur votre application web Azure et sélectionnez **Afficher les journaux de streaming**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Activer la diffusion de journaux](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="ae78e-299">Hello journaux sont maintenant transmis en hello **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="ae78e-299">hello logs are now streamed into hello **Output** window.</span></span> 

![Diffusion des journaux dans la fenêtre Sortie](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="ae78e-301">Toutefois, vous ne voyez pas un des messages de trace hello encore.</span><span class="sxs-lookup"><span data-stu-id="ae78e-301">However, you don't see any of hello trace messages yet.</span></span> <span data-ttu-id="ae78e-302">C’est la parce que, lorsque vous sélectionnez **afficher les journaux de diffusion en continu**, votre application web Azure définit le niveau de trace hello trop`Error`, qui enregistre uniquement les événements d’erreur (avec hello `Trace.TraceError()` méthode).</span><span class="sxs-lookup"><span data-stu-id="ae78e-302">That's because when you first select **View Streaming Logs**, your Azure web app sets hello trace level too`Error`, which only logs error events (with hello `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="ae78e-303">Modifier les niveaux de suivi</span><span class="sxs-lookup"><span data-stu-id="ae78e-303">Change trace levels</span></span>

<span data-ttu-id="ae78e-304">trace de hello toochange niveaux toooutput autres messages de trace, accédez précédent trop**l’Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-304">toochange hello trace levels toooutput other trace messages, go back too**Server Explorer**.</span></span>

<span data-ttu-id="ae78e-305">Cliquez de nouveau avec le bouton droit sur votre application web Azure et sélectionnez **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="ae78e-306">Bonjour **journalisation des applications (système de fichiers)** liste déroulante, sélectionnez **Verbose**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-306">In hello **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="ae78e-307">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ae78e-307">Click **Save**.</span></span>

![Modifier tooVerbose au niveau de trace](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="ae78e-309">Vous pouvez expérimenter trace différents niveaux toosee quels types de messages sont affichés pour chaque niveau.</span><span class="sxs-lookup"><span data-stu-id="ae78e-309">You can experiment with different trace levels toosee what types of messages are displayed for each level.</span></span> <span data-ttu-id="ae78e-310">Par exemple, hello **informations** niveau inclut tous les journaux créés par `Trace.TraceInformation()`, `Trace.TraceWarning()`, et `Trace.TraceError()`, mais pas les journaux créés par `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="ae78e-310">For example, hello **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="ae78e-311">Dans votre navigateur, essayez de cliquer sur l’application de liste de tâches hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ae78e-311">In your browser, try clicking around hello to-do list application in Azure.</span></span> <span data-ttu-id="ae78e-312">les messages de trace Hello sont transmises maintenant toohello **sortie** fenêtre dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae78e-312">hello trace messages are now streamed toohello **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="ae78e-313">Arrêter la diffusion de journaux</span><span class="sxs-lookup"><span data-stu-id="ae78e-313">Stop log streaming</span></span>

<span data-ttu-id="ae78e-314">toostop hello service de diffusion en continu de journal, cliquez sur hello **arrêter l’analyse** bouton Bonjour **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="ae78e-314">toostop hello log-streaming service, click hello **Stop monitoring** button in hello **Output** window.</span></span>

![Arrêter la diffusion de journaux](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="ae78e-316">Gérer votre application web Azure</span><span class="sxs-lookup"><span data-stu-id="ae78e-316">Manage your Azure web app</span></span>

<span data-ttu-id="ae78e-317">Accédez toohello [portail Azure](https://portal.azure.com) toosee vous avez créé l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="ae78e-317">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span> 



<span data-ttu-id="ae78e-318">Dans le menu de gauche hello, cliquez sur **du Service d’applications**, puis cliquez sur nom hello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="ae78e-318">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Application de navigation du portail tooAzure web](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="ae78e-320">Vous accédez à la page de votre application web.</span><span class="sxs-lookup"><span data-stu-id="ae78e-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="ae78e-321">Par défaut, le portail de hello affiche hello **vue d’ensemble** page.</span><span class="sxs-lookup"><span data-stu-id="ae78e-321">By default, hello portal shows hello **Overview** page.</span></span> <span data-ttu-id="ae78e-322">Cette page propose un aperçu de votre application.</span><span class="sxs-lookup"><span data-stu-id="ae78e-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="ae78e-323">Ici, vous pouvez également effectuer des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="ae78e-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="ae78e-324">onglets Hello sur le côté gauche de hello de page de hello affichent les pages de configuration différents hello que vous pouvez l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="ae78e-324">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span> 

![Page App Service du Portail Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="ae78e-326">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae78e-326">Next steps</span></span>

<span data-ttu-id="ae78e-327">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="ae78e-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ae78e-328">Créer une base de données SQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="ae78e-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="ae78e-329">Se connecter à un tooSQL d’application ASP.NET de base de données</span><span class="sxs-lookup"><span data-stu-id="ae78e-329">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="ae78e-330">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="ae78e-330">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="ae78e-331">Mettre à jour le modèle de données hello et redéployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="ae78e-331">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="ae78e-332">Journaux des flux de données à partir d’Azure tooyour Terminal Server</span><span class="sxs-lookup"><span data-stu-id="ae78e-332">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="ae78e-333">Gérer l’application hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="ae78e-333">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="ae78e-334">Avancer toolearn de didacticiel suivant toohello toohello l’application web de noms toomap DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="ae78e-334">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae78e-335">Mapper une tooAzure de nom DNS personnalisé existant Web Apps</span><span class="sxs-lookup"><span data-stu-id="ae78e-335">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
