---
title: aaaHow toocreate une application Web avec le Cache Redis | Documents Microsoft
description: "Découvrez comment toocreate une application Web avec le Cache Redis"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a><span data-ttu-id="101d2-103">Comment toocreate une application Web avec le Cache Redis</span><span class="sxs-lookup"><span data-stu-id="101d2-103">How toocreate a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="101d2-104">.NET</span><span class="sxs-lookup"><span data-stu-id="101d2-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="101d2-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="101d2-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="101d2-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="101d2-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="101d2-107">Java</span><span class="sxs-lookup"><span data-stu-id="101d2-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="101d2-108">Python</span><span class="sxs-lookup"><span data-stu-id="101d2-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="101d2-109">Ce didacticiel montre comment toocreate et déployer une application ASP.NET web application tooa web dans Azure App Service à l’aide de Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="101d2-109">This tutorial shows how toocreate and deploy an ASP.NET web application tooa web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="101d2-110">exemple d’application Hello affiche la liste des statistiques sur les équipes à partir d’une base de données et montre les différentes façons toouse Cache Redis Azure toostore et récupérer des données à partir du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-110">hello sample application displays a list of team statistics from a database and shows different ways toouse Azure Redis Cache toostore and retrieve data from hello cache.</span></span> <span data-ttu-id="101d2-111">Lorsque vous effectuez le didacticiel de hello vous avez une application web en cours d’exécution qui lit et écrit la base de données tooa, optimisée avec le Cache Redis Azure et hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="101d2-111">When you complete hello tutorial you'll have a running web app that reads and writes tooa database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="101d2-112">Vous apprendrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="101d2-112">You'll learn:</span></span>

* <span data-ttu-id="101d2-113">Comment toocreate un ASP.NET MVC 5 web application dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="101d2-113">How toocreate an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="101d2-114">Comment tooaccess des données à partir d’une base de données à l’aide d’Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="101d2-114">How tooaccess data from a database using Entity Framework.</span></span>
* <span data-ttu-id="101d2-115">Comment tooimprove le débit des données et réduire la charge de la base de données en stockage et la récupération des données à l’aide du Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="101d2-115">How tooimprove data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="101d2-116">Comment toouse un Redis triés ensemble tooretrieve hello top 5 les équipes.</span><span class="sxs-lookup"><span data-stu-id="101d2-116">How toouse a Redis sorted set tooretrieve hello top 5 teams.</span></span>
* <span data-ttu-id="101d2-117">Comment tooprovision hello ressources Azure pour l’application hello à l’aide d’un modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="101d2-117">How tooprovision hello Azure resources for hello application using a Resource Manager template.</span></span>
* <span data-ttu-id="101d2-118">Comment toopublish hello tooAzure d’application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="101d2-118">How toopublish hello application tooAzure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="101d2-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="101d2-119">Prerequisites</span></span>
<span data-ttu-id="101d2-120">didacticiel de hello toocomplete, vous devez avoir hello suivant des conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="101d2-120">toocomplete hello tutorial, you must have hello following prerequisites.</span></span>

* [<span data-ttu-id="101d2-121">Compte Azure</span><span class="sxs-lookup"><span data-stu-id="101d2-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="101d2-122">Visual Studio 2017, avec hello Azure SDK pour .NET</span><span class="sxs-lookup"><span data-stu-id="101d2-122">Visual Studio 2017 with hello Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="101d2-123">Compte Azure</span><span class="sxs-lookup"><span data-stu-id="101d2-123">Azure account</span></span>
<span data-ttu-id="101d2-124">Vous avez besoin d’un didacticiel de hello toocomplete compte Azure.</span><span class="sxs-lookup"><span data-stu-id="101d2-124">You need an Azure account toocomplete hello tutorial.</span></span> <span data-ttu-id="101d2-125">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="101d2-125">You can:</span></span>

* <span data-ttu-id="101d2-126">[Ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="101d2-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="101d2-127">Vous obtenez des crédits qui peuvent être utilisé tootry out à payer des services Azure.</span><span class="sxs-lookup"><span data-stu-id="101d2-127">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="101d2-128">Même après que hello crédits épuisés, vous pouvez conserver le compte de hello et utiliser des fonctionnalités et des services Azure gratuits.</span><span class="sxs-lookup"><span data-stu-id="101d2-128">Even after hello credits are used up, you can keep hello account and use free Azure services and features.</span></span>
* <span data-ttu-id="101d2-129">[Activez les avantages d’abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="101d2-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="101d2-130">Votre abonnement MSDN vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.</span><span class="sxs-lookup"><span data-stu-id="101d2-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a><span data-ttu-id="101d2-131">Visual Studio 2017, avec hello Azure SDK pour .NET</span><span class="sxs-lookup"><span data-stu-id="101d2-131">Visual Studio 2017 with hello Azure SDK for .NET</span></span>
<span data-ttu-id="101d2-132">didacticiel de Hello est écrit pour Visual Studio 2017 avec hello [Azure SDK pour .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="101d2-132">hello tutorial is written for Visual Studio 2017 with hello [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="101d2-133">Bonjour Azure SDK 2.9.5 est inclus avec le programme d’installation de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-133">hello Azure SDK 2.9.5 is included with hello Visual Studio installer.</span></span>

<span data-ttu-id="101d2-134">Si vous avez Visual Studio 2015, vous pouvez suivre le didacticiel hello avec hello [Azure SDK pour .NET](../dotnet-sdk.md) point 2.8.2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="101d2-134">If you have Visual Studio 2015, you can follow hello tutorial with hello [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="101d2-135">[Téléchargement hello plus récentes de Windows Azure SDK pour Visual Studio 2015 ici](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="101d2-135">[Download hello latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="101d2-136">Visual Studio est installé automatiquement avec le Kit de développement logiciel de hello si vous n’est pas déjà installé.</span><span class="sxs-lookup"><span data-stu-id="101d2-136">Visual Studio is automatically installed with hello SDK if you don't already have it.</span></span> <span data-ttu-id="101d2-137">Certains écrans diffèrent des illustrations hello indiquées dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="101d2-137">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

<span data-ttu-id="101d2-138">Si vous avez Visual Studio 2013, vous pouvez [téléchargement hello plus récentes de Windows Azure SDK pour Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="101d2-138">If you have Visual Studio 2013, you can [download hello latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="101d2-139">Certains écrans diffèrent des illustrations hello indiquées dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="101d2-139">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

## <a name="create-hello-visual-studio-project"></a><span data-ttu-id="101d2-140">Créer le projet de Visual Studio hello</span><span class="sxs-lookup"><span data-stu-id="101d2-140">Create hello Visual Studio project</span></span>
1. <span data-ttu-id="101d2-141">Ouvrez Visual Studio et cliquez sur **Fichier**, **Nouveau**, **Projet**.</span><span class="sxs-lookup"><span data-stu-id="101d2-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="101d2-142">Développez hello **Visual C#** nœud Bonjour **modèles** liste, sélectionnez **Cloud**, puis cliquez sur **Application Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="101d2-142">Expand hello **Visual C#** node in hello **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="101d2-143">Vérifiez que l’option **.NET Framework 4.5.2** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="101d2-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="101d2-144">Type **ContosoTeamStats** dans hello **nom** zone de texte et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="101d2-144">Type **ContosoTeamStats** into hello **Name** textbox and click **OK**.</span></span>
   
    ![Créer un projet][cache-create-project]
3. <span data-ttu-id="101d2-146">Sélectionnez **MVC** en tant que type de projet hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-146">Select **MVC** as hello project type.</span></span> 

    <span data-ttu-id="101d2-147">Vérifiez que **aucune authentification** est spécifié pour hello **authentification** paramètres.</span><span class="sxs-lookup"><span data-stu-id="101d2-147">Ensure that **No Authentication** is specified for hello **Authentication** settings.</span></span> <span data-ttu-id="101d2-148">Selon votre version de Visual Studio, par défaut de hello peut être défini toosomething else.</span><span class="sxs-lookup"><span data-stu-id="101d2-148">Depending on your version of Visual Studio, hello default may be set toosomething else.</span></span> <span data-ttu-id="101d2-149">toochange, cliquez sur **modifier l’authentification** et sélectionnez **aucune authentification**.</span><span class="sxs-lookup"><span data-stu-id="101d2-149">toochange it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="101d2-150">Si vous suivez avec Visual Studio 2015, désactivez hello **hôte hello cloud** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="101d2-150">If you are following along with Visual Studio 2015, clear hello **Host in hello cloud** checkbox.</span></span> <span data-ttu-id="101d2-151">Vous allez [configurer hello ressources Azure](#provision-the-azure-resources) et [publier hello application tooAzure](#publish-the-application-to-azure) dans les étapes suivantes dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-151">You'll [provision hello Azure resources](#provision-the-azure-resources) and [publish hello application tooAzure](#publish-the-application-to-azure) in subsequent steps in hello tutorial.</span></span> <span data-ttu-id="101d2-152">Pour obtenir un exemple de configuration d’une application Service web d’application à partir de Visual Studio en laissant **hôte hello cloud** activée, consultez [prise en main Web Apps dans Azure App Service, à l’aide d’ASP.NET et Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="101d2-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in hello cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Sélectionner un modèle de projet][cache-select-template]
4. <span data-ttu-id="101d2-154">Cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="101d2-154">Click **OK** toocreate hello project.</span></span>

## <a name="create-hello-aspnet-mvc-application"></a><span data-ttu-id="101d2-155">Créer hello application ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="101d2-155">Create hello ASP.NET MVC application</span></span>
<span data-ttu-id="101d2-156">Dans cette section du didacticiel de hello, vous allez créer l’application de base hello qui lit et affiche des statistiques sur les équipes à partir d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="101d2-156">In this section of hello tutorial, you'll create hello basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="101d2-157">Ajoutez le package NuGet Entity Framework de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-157">Add hello Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="101d2-158">Ajouter un modèle de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-158">Add hello model</span></span>](#add-the-model)
* [<span data-ttu-id="101d2-159">Ajouter un contrôleur de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-159">Add hello controller</span></span>](#add-the-controller)
* [<span data-ttu-id="101d2-160">Configurer des vues de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-160">Configure hello views</span></span>](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a><span data-ttu-id="101d2-161">Ajoutez le package NuGet Entity Framework de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-161">Add hello Entity Framework NuGet package</span></span>

1. <span data-ttu-id="101d2-162">Cliquez sur **Gestionnaire de Package NuGet**, **Package Manager Console** de hello **outils** menu.</span><span class="sxs-lookup"><span data-stu-id="101d2-162">Click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="101d2-163">Exécution hello après une commande à partir de hello **Package Manager Console** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="101d2-163">Run hello following command from hello **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="101d2-164">Pour plus d’informations sur ce package, consultez hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span><span class="sxs-lookup"><span data-stu-id="101d2-164">For more information about this package, see hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-hello-model"></a><span data-ttu-id="101d2-165">Ajouter un modèle de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-165">Add hello model</span></span>
1. <span data-ttu-id="101d2-166">Cliquez avec le bouton droit sur **Modèles** dans l’**Explorateur de solutions** et sélectionnez **Ajouter**, **Classe**.</span><span class="sxs-lookup"><span data-stu-id="101d2-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Ajouter un modèle][cache-model-add-class]
2. <span data-ttu-id="101d2-168">Entrez `Team` pour le nom de la classe hello et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="101d2-168">Enter `Team` for hello class name and click **Add**.</span></span>
   
    ![Ajouter une classe de modèle][cache-model-add-class-dialog]
3. <span data-ttu-id="101d2-170">Remplacez hello `using` instructions haut hello hello `Team.cs` fichier avec les éléments suivants de hello `using` instructions.</span><span class="sxs-lookup"><span data-stu-id="101d2-170">Replace hello `using` statements at hello top of hello `Team.cs` file with hello following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="101d2-171">Remplacez la définition hello Hello `Team` classe avec hello suivant extrait de code qui contient une mise à jour `Team` classe Définition ainsi que d’autres classes d’assistance de Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="101d2-171">Replace hello definition of hello `Team` class with hello following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="101d2-172">Pour plus d’informations sur hello code première approche tooEntity Framework qui est utilisé dans ce didacticiel, consultez [Code premier tooa nouvelle base de données](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="101d2-172">For more information on hello code first approach tooEntity Framework that's used in this tutorial, see [Code first tooa new database](https://msdn.microsoft.com/data/jj193542).</span></span>

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. <span data-ttu-id="101d2-173">Dans **l’Explorateur de solutions**, double-cliquez sur **web.config** tooopen il.</span><span class="sxs-lookup"><span data-stu-id="101d2-173">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="101d2-175">Ajoutez hello suit `connectionStrings` section.</span><span class="sxs-lookup"><span data-stu-id="101d2-175">Add hello following `connectionStrings` section.</span></span> <span data-ttu-id="101d2-176">nom Hello hello de chaîne de connexion doit correspondre au nom hello Hello classe de contexte de base de données Entity Framework qui est `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="101d2-176">hello name of hello connection string must match hello name of hello Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="101d2-177">Vous pouvez ajouter hello nouvelle `connectionStrings` section afin qu’elle suive `configSections`, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="101d2-177">You can add hello new `connectionStrings` section so that it follows `configSections`, as shown in hello following example.</span></span>

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > <span data-ttu-id="101d2-178">Votre chaîne de connexion peut être différent selon la version de hello de Visual Studio et SQL Server Express edition utilisé didacticiel de hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="101d2-178">Your connection string may be different depending on hello version of Visual Studio and SQL Server Express edition used toocomplete hello tutorial.</span></span> <span data-ttu-id="101d2-179">modèle de web.config Hello doit être configuré toomatch votre installation et peut contenir `Data Source` comme des entrées `(LocalDB)\v11.0` (à partir de SQL Server Express 2012) ou `Data Source=(LocalDB)\MSSQLLocalDB` (SQL Server Express 2014 et version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="101d2-179">hello web.config template should be configured toomatch your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="101d2-180">Pour plus d’informations sur les chaînes de connexion et les versions de SQL Express, consultez [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="101d2-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-hello-controller"></a><span data-ttu-id="101d2-181">Ajouter un contrôleur de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-181">Add hello controller</span></span>
1. <span data-ttu-id="101d2-182">Appuyez sur **F6** projet hello de toobuild.</span><span class="sxs-lookup"><span data-stu-id="101d2-182">Press **F6** toobuild hello project.</span></span> 
2. <span data-ttu-id="101d2-183">Dans **l’Explorateur de solutions**, avec le bouton hello **contrôleurs** dossier et choisissez **ajouter**, **contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="101d2-183">In **Solution Explorer**, right-click hello **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Ajouter un contrôleur][cache-add-controller]
3. <span data-ttu-id="101d2-185">Sélectionnez **Contrôleur MVC 5 avec vues, en utilisant Entity Framework**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="101d2-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="101d2-186">Si vous obtenez une erreur après avoir cliqué sur **ajouter**, assurez-vous que vous avez créé un projet de hello tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="101d2-186">If you get an error after clicking **Add**, ensure that you have built hello project first.</span></span>
   
    ![Ajouter une classe de contrôleur][cache-add-controller-class]
4. <span data-ttu-id="101d2-188">Sélectionnez **Team (ContosoTeamStats.Models)** de hello **classe de modèle** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="101d2-188">Select **Team (ContosoTeamStats.Models)** from hello **Model class** drop-down list.</span></span> <span data-ttu-id="101d2-189">Sélectionnez **TeamContext (ContosoTeamStats.Models)** de hello **classe de contexte de données** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="101d2-189">Select **TeamContext (ContosoTeamStats.Models)** from hello **Data context class** drop-down list.</span></span> <span data-ttu-id="101d2-190">Type `TeamsController` Bonjour **contrôleur** zone de texte Nom (si elle n’est pas remplie automatiquement).</span><span class="sxs-lookup"><span data-stu-id="101d2-190">Type `TeamsController` in hello **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="101d2-191">Cliquez sur **ajouter** toocreate hello de classe de contrôleur et ajouter des vues par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-191">Click **Add** toocreate hello controller class and add hello default views.</span></span>
   
    ![Configurer un contrôleur][cache-configure-controller]
5. <span data-ttu-id="101d2-193">Dans **l’Explorateur de solutions**, développez **Global.asax** et double-cliquez sur **Global.asax.cs** tooopen il.</span><span class="sxs-lookup"><span data-stu-id="101d2-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** tooopen it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="101d2-195">Ajouter hello suivant deux `using` instructions haut hello du fichier hello sous hello autres `using` instructions.</span><span class="sxs-lookup"><span data-stu-id="101d2-195">Add hello following two `using` statements at hello top of hello file under hello other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="101d2-196">Ajouter hello suivant la ligne de code à fin hello Hello `Application_Start` (méthode).</span><span class="sxs-lookup"><span data-stu-id="101d2-196">Add hello following line of code at hello end of hello `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="101d2-197">Dans l’**Explorateur de solutions**, développez `App_Start` et double-cliquez sur `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="101d2-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="101d2-199">Remplacez `controller = "Home"` Bonjour suivant code Bonjour `RegisterRoutes` méthode avec `controller = "Teams"` comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="101d2-199">Replace `controller = "Home"` in hello following code in hello `RegisterRoutes` method with `controller = "Teams"` as shown in hello following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a><span data-ttu-id="101d2-200">Configurer des vues de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-200">Configure hello views</span></span>
1. <span data-ttu-id="101d2-201">Dans **l’Explorateur de solutions**, développez hello **vues** dossier puis hello **Shared** dossier, puis double-cliquez sur **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="101d2-201">In **Solution Explorer**, expand hello **Views** folder and then hello **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="101d2-203">Modifier le contenu hello Hello `title` élément et remplacer `My ASP.NET Application` avec `Contoso Team Stats` comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="101d2-203">Change hello contents of hello `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in hello following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="101d2-204">Bonjour `body` section, mise à jour de hello tout d’abord `Html.ActionLink` instruction et remplacer `Application name` avec `Contoso Team Stats` et remplacer `Home` avec `Teams`.</span><span class="sxs-lookup"><span data-stu-id="101d2-204">In hello `body` section, update hello first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="101d2-205">Avant : `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="101d2-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="101d2-206">Après : `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="101d2-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Modifications du code][cache-layout-cshtml-code]
2. <span data-ttu-id="101d2-208">Appuyez sur **Ctrl + F5** toobuild et exécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-208">Press **Ctrl+F5** toobuild and run hello application.</span></span> <span data-ttu-id="101d2-209">Cette version de l’application hello lit les résultats hello directement à partir de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-209">This version of hello application reads hello results directly from hello database.</span></span> <span data-ttu-id="101d2-210">Hello de note **créer un nouveau**, **modifier**, **détails**, et **supprimer** les actions qui ont été automatiquement ajouté toohello application par hello **Contrôleur MVC 5 avec vues, utilisant Entity Framework** structure.</span><span class="sxs-lookup"><span data-stu-id="101d2-210">Note hello **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added toohello application by hello **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="101d2-211">Dans la section suivante de hello du didacticiel de hello vous ajouterez des données de Cache Redis toooptimize hello accéder et fournissent des fonctionnalités supplémentaires toohello application.</span><span class="sxs-lookup"><span data-stu-id="101d2-211">In hello next section of hello tutorial you'll add Redis Cache toooptimize hello data access and provide additional features toohello application.</span></span>

![Application de départ][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a><span data-ttu-id="101d2-213">Configurer hello application toouse Cache Redis</span><span class="sxs-lookup"><span data-stu-id="101d2-213">Configure hello application toouse Redis Cache</span></span>
<span data-ttu-id="101d2-214">Dans cette section du didacticiel de hello, vous allez configurer toostore d’application exemple hello et extraire des statistiques sur les équipes Contoso à partir d’une instance de Cache Redis Azure à l’aide de hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) client de cache.</span><span class="sxs-lookup"><span data-stu-id="101d2-214">In this section of hello tutorial, you'll configure hello sample application toostore and retrieve Contoso team statistics from an Azure Redis Cache instance by using hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="101d2-215">Configurer l’application de hello toouse StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="101d2-215">Configure hello application toouse StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="101d2-216">Mettre à jour hello TeamsController classe tooreturn résultats à partir du cache de hello ou base de données hello</span><span class="sxs-lookup"><span data-stu-id="101d2-216">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="101d2-217">Hello, créer, modifier, de mettre à jour et supprimer des toowork méthodes avec un cache de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-217">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="101d2-218">Mettre à jour hello équipes Index vue toowork avec le cache de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-218">Update hello Teams Index view toowork with hello cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a><span data-ttu-id="101d2-219">Configurer l’application de hello toouse StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="101d2-219">Configure hello application toouse StackExchange.Redis</span></span>
1. <span data-ttu-id="101d2-220">tooconfigure une application cliente dans Visual Studio à l’aide de hello package StackExchange.Redis NuGet, cliquez sur **Gestionnaire de Package NuGet**, **Package Manager Console** de hello **outils** menu.</span><span class="sxs-lookup"><span data-stu-id="101d2-220">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="101d2-221">Exécution hello après une commande à partir de hello `Package Manager Console` fenêtre.</span><span class="sxs-lookup"><span data-stu-id="101d2-221">Run hello following command from hello `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="101d2-222">Hello NuGet package télécharge et ajoute hello obligatoire des références d’assembly pour votre tooaccess d’application client du Cache Redis Azure avec le client de cache StackExchange.Redis hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-222">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span> <span data-ttu-id="101d2-223">Si vous préférez toouse une version de nom fort de hello `StackExchange.Redis` bibliothèque cliente, installation hello `StackExchange.Redis.StrongName` package.</span><span class="sxs-lookup"><span data-stu-id="101d2-223">If you prefer toouse a strong-named version of hello `StackExchange.Redis` client library, install hello `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="101d2-224">Dans **l’Explorateur de solutions**, développez hello **contrôleurs** et double-cliquez sur **TeamsController.cs** tooopen il.</span><span class="sxs-lookup"><span data-stu-id="101d2-224">In **Solution Explorer**, expand hello **Controllers** folder and double-click **TeamsController.cs** tooopen it.</span></span>
   
    ![Contrôleur Teams][cache-teamscontroller]
4. <span data-ttu-id="101d2-226">Ajouter hello suivant deux `using` instructions trop**TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="101d2-226">Add hello following two `using` statements too**TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="101d2-227">Ajouter hello suivant deux propriétés toohello `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="101d2-227">Add hello following two properties toohello `TeamsController` class.</span></span>

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. <span data-ttu-id="101d2-228">Créer un fichier sur votre ordinateur nommé `WebAppPlusCacheAppSecrets.config` et les placer dans un emplacement qui ne sont pas vérifiées avec le code source de hello de votre application d’exemple, si vous décidez toocheck dans un emplacement.</span><span class="sxs-lookup"><span data-stu-id="101d2-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with hello source code of your sample application, should you decide toocheck it in somewhere.</span></span> <span data-ttu-id="101d2-229">Dans cette hello exemple `AppSettingsSecrets.config` fichier se trouve dans `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="101d2-229">In this example hello `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="101d2-230">Modifier hello `WebAppPlusCacheAppSecrets.config` et ajoutez hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="101d2-230">Edit hello `WebAppPlusCacheAppSecrets.config` file and add hello following contents.</span></span> <span data-ttu-id="101d2-231">Si vous exécutez des application hello localement cette information est instance de Cache Redis Azure tooyour tooconnect utilisé.</span><span class="sxs-lookup"><span data-stu-id="101d2-231">If you run hello application locally this information is used tooconnect tooyour Azure Redis Cache instance.</span></span> <span data-ttu-id="101d2-232">Plus loin dans le didacticiel de hello, vous allez configurer une instance de Cache Redis Azure et mettre à jour le mot de passe et le nom du cache hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-232">Later in hello tutorial you'll provision an Azure Redis Cache instance and update hello cache name and password.</span></span> <span data-ttu-id="101d2-233">Si vous ne prévoyez pas toorun hello exemple d’application localement, vous pouvez ignorer la création de hello de ce fichier et les étapes suivantes hello qui font référence les fichiers hello, car lorsque vous déployez tooAzure hello application récupère les informations de connexion hello du cache à partir de l’application hello paramètre de hello Web App et non à partir de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="101d2-233">If you don't plan toorun hello sample application locally you can skip hello creation of this file and hello subsequent steps that reference hello file, because when you deploy tooAzure hello application retrieves hello cache connection information from hello app setting for hello Web App and not from this file.</span></span> <span data-ttu-id="101d2-234">Depuis hello `WebAppPlusCacheAppSecrets.config` n’est pas déployée tooAzure avec votre application, vous n’en avez besoin, sauf si vous envisagez d’application de hello toorun localement.</span><span class="sxs-lookup"><span data-stu-id="101d2-234">Since hello `WebAppPlusCacheAppSecrets.config` is not deployed tooAzure with your application, you don't need it unless you are going toorun hello application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="101d2-235">Dans **l’Explorateur de solutions**, double-cliquez sur **web.config** tooopen il.</span><span class="sxs-lookup"><span data-stu-id="101d2-235">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="101d2-237">Ajoutez hello suivant `file` attribut toohello `appSettings` élément.</span><span class="sxs-lookup"><span data-stu-id="101d2-237">Add hello following `file` attribute toohello `appSettings` element.</span></span> <span data-ttu-id="101d2-238">Si vous avez utilisé un autre nom de fichier ou un emplacement, remplacez par les valeurs hello ceux indiqués dans l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-238">If you used a different file name or location, substitute those values for hello ones shown in hello example.</span></span>
   
   * <span data-ttu-id="101d2-239">Avant : `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="101d2-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="101d2-240">Après : ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="101d2-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="101d2-241">Hello ASP.NET runtime fusionne contenu hello du fichier externe de hello avec balisage hello Bonjour `<appSettings>` élément.</span><span class="sxs-lookup"><span data-stu-id="101d2-241">hello ASP.NET runtime merges hello contents of hello external file with hello markup in hello `<appSettings>` element.</span></span> <span data-ttu-id="101d2-242">Hello runtime ignore l’attribut de fichier hello si hello spécifié ne se trouve.</span><span class="sxs-lookup"><span data-stu-id="101d2-242">hello runtime ignores hello file attribute if hello specified file cannot be found.</span></span> <span data-ttu-id="101d2-243">Vos secrets (cache tooyour chaîne hello connexion) ne sont pas inclus dans le cadre du code source de hello pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-243">Your secrets (hello connection string tooyour cache) are not included as part of hello source code for hello application.</span></span> <span data-ttu-id="101d2-244">Lorsque vous déployez votre tooAzure d’application web, hello `WebAppPlusCacheAppSecrests.config` fichier ne sera pas déployé (c’est ce que vous souhaitez).</span><span class="sxs-lookup"><span data-stu-id="101d2-244">When you deploy your web app tooAzure, hello `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="101d2-245">Il existe plusieurs façons toospecify ces clés secrètes dans Azure, et dans ce didacticiel qu’ils sont configurés automatiquement pour vous lorsque vous [configurer hello ressources Azure](#provision-the-azure-resources) dans une étape ultérieure du didacticiel.</span><span class="sxs-lookup"><span data-stu-id="101d2-245">There are several ways toospecify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision hello Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="101d2-246">Pour plus d’informations sur l’utilisation des clés secrètes dans Azure, consultez [meilleures pratiques pour le déploiement de mots de passe et d’autres données sensibles tooASP.NET et Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="101d2-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data tooASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a><span data-ttu-id="101d2-247">Mettre à jour hello TeamsController classe tooreturn résultats à partir du cache de hello ou base de données hello</span><span class="sxs-lookup"><span data-stu-id="101d2-247">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>
<span data-ttu-id="101d2-248">Dans cet exemple, les statistiques sur les équipes peuvent être récupérés à partir de la base de données hello ou à partir du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-248">In this sample, team statistics can be retrieved from hello database or from hello cache.</span></span> <span data-ttu-id="101d2-249">Statistiques sur les équipes sont stockés dans le cache de hello sous la forme sérialisée `List<Team>`et également comme un ensemble trié à l’aide des types de données Redis.</span><span class="sxs-lookup"><span data-stu-id="101d2-249">Team statistics are stored in hello cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="101d2-250">Lors de la récupération des éléments d’un ensemble trié, vous pouvez récupérer certains éléments, récupérer tous les éléments ou effectuer une requête sur certains éléments.</span><span class="sxs-lookup"><span data-stu-id="101d2-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="101d2-251">Dans cet exemple, vous devez interroger ensemble hello triée pour les équipes top 5 hello classés par nombre de wins.</span><span class="sxs-lookup"><span data-stu-id="101d2-251">In this sample you'll query hello sorted set for hello top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="101d2-252">Il n’est pas requis toostore hello statistiques sur les équipes dans plusieurs formats dans le cache de hello dans l’ordre toouse Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="101d2-252">It is not required toostore hello team statistics in multiple formats in hello cache in order toouse Azure Redis Cache.</span></span> <span data-ttu-id="101d2-253">Ce didacticiel utilise plusieurs formats toodemonstrate certaines des différentes façons de hello et différents types de données, vous pouvez utiliser les données toocache.</span><span class="sxs-lookup"><span data-stu-id="101d2-253">This tutorial uses multiple formats toodemonstrate some of hello different ways and different data types you can use toocache data.</span></span>
> 
> 

1. <span data-ttu-id="101d2-254">Ajoutez hello suivant `using` instructions toohello `TeamsController.cs` fichier en haut hello avec hello autres `using` instructions.</span><span class="sxs-lookup"><span data-stu-id="101d2-254">Add hello following `using` statements toohello `TeamsController.cs` file at hello top with hello other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="101d2-255">Remplacez hello actuel `public ActionResult Index()` implémentation de méthode avec hello après mise en oeuvre.</span><span class="sxs-lookup"><span data-stu-id="101d2-255">Replace hello current `public ActionResult Index()` method implementation with hello following implementation.</span></span>

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="101d2-256">Ajouter hello suivant trois méthodes toohello `TeamsController` hello tooimplement de classe `playGames`, `clearCache`, et `rebuildDB` types d’action de hello switch, instruction ajoutée dans l’extrait de code précédent hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-256">Add hello following three methods toohello `TeamsController` class tooimplement hello `playGames`, `clearCache`, and `rebuildDB` action types from hello switch statement added in hello previous code snippet.</span></span>
   
    <span data-ttu-id="101d2-257">Hello `PlayGames` méthode met à jour les statistiques sur les équipes hello en simulant une saison des jeux et enregistre hello de base de données de résultats toohello efface hello maintenant les données à partir du cache de hello est obsolète.</span><span class="sxs-lookup"><span data-stu-id="101d2-257">hello `PlayGames` method updates hello team statistics by simulating a season of games, saves hello results toohello database, and clears hello now outdated data from hello cache.</span></span>

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="101d2-258">Hello `RebuildDB` méthode réinitialise hello base de données avec l’ensemble des équipes, par défaut de hello génère des statistiques pour les et efface hello maintenant les données à partir du cache de hello est obsolète.</span><span class="sxs-lookup"><span data-stu-id="101d2-258">hello `RebuildDB` method reinitializes hello database with hello default set of teams, generates statistics for them, and clears hello now outdated data from hello cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="101d2-259">Hello `ClearCachedTeams` méthode supprime toutes les statistiques de l’équipe de mise en cache à partir du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-259">hello `ClearCachedTeams` method removes any cached team statistics from hello cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="101d2-260">Ajouter hello suivant quatre méthodes toohello `TeamsController` hello tooimplement de classe différentes façons de récupérer des statistiques sur les équipes hello à partir du cache de hello et base de données hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-260">Add hello following four methods toohello `TeamsController` class tooimplement hello various ways of retrieving hello team statistics from hello cache and hello database.</span></span> <span data-ttu-id="101d2-261">Chacune de ces méthodes retourne une `List<Team>` qui est ensuite affiché en vue de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-261">Each of these methods returns a `List<Team>` which is then displayed by hello view.</span></span>
   
    <span data-ttu-id="101d2-262">Hello `GetFromDB` méthode lit les statistiques sur les équipes hello à partir de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-262">hello `GetFromDB` method reads hello team statistics from hello database.</span></span>
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    <span data-ttu-id="101d2-263">Hello `GetFromList` méthode lit les statistiques sur les équipes hello cache sous la forme sérialisée `List<Team>`.</span><span class="sxs-lookup"><span data-stu-id="101d2-263">hello `GetFromList` method reads hello team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="101d2-264">S’il existe une absence dans le cache, statistiques sur les équipes hello sont lus à partir de la base de données hello et ensuite stockées dans le cache de hello pour la prochaine fois.</span><span class="sxs-lookup"><span data-stu-id="101d2-264">If there is a cache miss, hello team statistics are read from hello database and then stored in hello cache for next time.</span></span> <span data-ttu-id="101d2-265">Dans cet exemple, nous utilisons JSON.NET sérialisation tooserialize hello .NET objets tooand à partir du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-265">In this sample we're using JSON.NET serialization tooserialize hello .NET objects tooand from hello cache.</span></span> <span data-ttu-id="101d2-266">Pour plus d’informations, consultez [comment les objets dans le Cache Redis Azure toowork avec .NET](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="101d2-266">For more information, see [How toowork with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="101d2-267">Hello `GetFromSortedSet` méthode lit les statistiques sur les équipes hello à partir d’un ensemble trié mis en cache.</span><span class="sxs-lookup"><span data-stu-id="101d2-267">hello `GetFromSortedSet` method reads hello team statistics from a cached sorted set.</span></span> <span data-ttu-id="101d2-268">S’il existe une absence dans le cache, statistiques sur les équipes hello sont lus à partir de la base de données hello et stockées dans le cache de hello sous la forme d’un ensemble trié.</span><span class="sxs-lookup"><span data-stu-id="101d2-268">If there is a cache miss, hello team statistics are read from hello database and stored in hello cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="101d2-269">Hello `GetFromSortedSetTop5` méthode lit l’ensemble d’équipes 5 à partir de la mise en cache de hello triées supérieur hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-269">hello `GetFromSortedSetTop5` method reads hello top 5 teams from hello cached sorted set.</span></span> <span data-ttu-id="101d2-270">Il commence par la vérification du cache de hello existence hello Hello `teamsSortedSet` clé.</span><span class="sxs-lookup"><span data-stu-id="101d2-270">It starts by checking hello cache for hello existence of hello `teamsSortedSet` key.</span></span> <span data-ttu-id="101d2-271">Si cette clé n’est pas présente, hello `GetFromSortedSet` méthode est appelée statistiques sur les équipes tooread hello et les stocker dans le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-271">If this key is not present, hello `GetFromSortedSet` method is called tooread hello team statistics and store them in hello cache.</span></span> <span data-ttu-id="101d2-272">Ensuite, hello ensemble trié mis en cache est interrogé pour hello top 5 équipes qui sont retournées.</span><span class="sxs-lookup"><span data-stu-id="101d2-272">Next, hello cached sorted set is queried for hello top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a><span data-ttu-id="101d2-273">Hello, créer, modifier, de mettre à jour et supprimer des toowork méthodes avec un cache de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-273">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>
<span data-ttu-id="101d2-274">code de génération de modèles automatique Hello qui a été généré comme partie de cet exemple inclut des méthodes tooadd, modifier et supprimer des équipes.</span><span class="sxs-lookup"><span data-stu-id="101d2-274">hello scaffolding code that was generated as part of this sample includes methods tooadd, edit, and delete teams.</span></span> <span data-ttu-id="101d2-275">Chaque fois qu’une équipe est ajoutée, modifiée ou supprimée, les données de salutation dans le cache de hello devient obsolètes.</span><span class="sxs-lookup"><span data-stu-id="101d2-275">Anytime a team is added, edited, or removed, hello data in hello cache becomes outdated.</span></span> <span data-ttu-id="101d2-276">Dans cette section, que vous allez modifier ces hello tooclear de trois méthodes mis en cache les équipes afin que le cache de hello ne sera pas synchronisé avec la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-276">In this section you'll modify these three methods tooclear hello cached teams so that hello cache won't be out of sync with hello database.</span></span>

1. <span data-ttu-id="101d2-277">Parcourir toohello `Create(Team team)` méthode Bonjour `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="101d2-277">Browse toohello `Create(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="101d2-278">Ajouter un appel toohello `ClearCachedTeams` méthode, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="101d2-278">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="101d2-279">Parcourir toohello `Edit(Team team)` méthode Bonjour `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="101d2-279">Browse toohello `Edit(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="101d2-280">Ajouter un appel toohello `ClearCachedTeams` méthode, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="101d2-280">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="101d2-281">Parcourir toohello `DeleteConfirmed(int id)` méthode Bonjour `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="101d2-281">Browse toohello `DeleteConfirmed(int id)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="101d2-282">Ajouter un appel toohello `ClearCachedTeams` méthode, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="101d2-282">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a><span data-ttu-id="101d2-283">Mettre à jour hello équipes Index vue toowork avec le cache de hello</span><span class="sxs-lookup"><span data-stu-id="101d2-283">Update hello Teams Index view toowork with hello cache</span></span>
1. <span data-ttu-id="101d2-284">Dans **l’Explorateur de solutions**, développez hello **vues** dossier, puis hello **équipes** dossier, puis double-cliquez sur **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="101d2-284">In **Solution Explorer**, expand hello **Views** folder, then hello **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="101d2-286">Haut hello du fichier de hello, recherchez hello après l’élément de paragraphe.</span><span class="sxs-lookup"><span data-stu-id="101d2-286">Near hello top of hello file, look for hello following paragraph element.</span></span>
   
    ![Table d’actions][cache-teams-index-table]
   
    <span data-ttu-id="101d2-288">Il s’agit de lien de hello toocreate une nouvelle équipe.</span><span class="sxs-lookup"><span data-stu-id="101d2-288">This is hello link toocreate a new team.</span></span> <span data-ttu-id="101d2-289">Remplacez l’élément de paragraphe hello avec hello tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="101d2-289">Replace hello paragraph element with hello following table.</span></span> <span data-ttu-id="101d2-290">Cette table comporte des liens d’action pour la création d’une nouvelle équipe, la lecture d’une nouvelle saison des jeux, l’effacement du cache de hello, récupérant les équipes de hello cache hello dans plusieurs formats, la récupération des équipes de hello à partir de la base de données hello et la reconstruction de base de données avec les données exemple nouvelle hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-290">This table has action links for creating a new team, playing a new season of games, clearing hello cache, retrieving hello teams from hello cache in several formats, retrieving hello teams from hello database, and rebuilding hello database with fresh sample data.</span></span>

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. <span data-ttu-id="101d2-291">Défiler vers le bas de hello toohello **Index.cshtml** et ajoutez les suivant hello `tr` élément afin qu’il soit hello dernière ligne hello dernière table dans le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-291">Scroll toohello bottom of hello **Index.cshtml** file and add hello following `tr` element so that it is hello last row in hello last table in hello file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="101d2-292">Cette ligne affiche la valeur hello `ViewBag.Msg` qui contient un rapport d’état sur l’opération en cours hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-292">This row displays hello value of `ViewBag.Msg` which contains a status report about hello current operation.</span></span> <span data-ttu-id="101d2-293">Hello `ViewBag.Msg` est définie lorsque vous cliquez sur un des liens d’action hello à partir de l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-293">hello `ViewBag.Msg` is set when you click any of hello action links from hello previous step.</span></span>   
   
    ![Message d’état][cache-status-message]
2. <span data-ttu-id="101d2-295">Appuyez sur **F6** projet hello de toobuild.</span><span class="sxs-lookup"><span data-stu-id="101d2-295">Press **F6** toobuild hello project.</span></span>

## <a name="provision-hello-azure-resources"></a><span data-ttu-id="101d2-296">Configurer hello ressources Azure</span><span class="sxs-lookup"><span data-stu-id="101d2-296">Provision hello Azure resources</span></span>
<span data-ttu-id="101d2-297">toohost votre application dans Azure, vous devez d’abord configurer hello des services Azure que votre application requiert.</span><span class="sxs-lookup"><span data-stu-id="101d2-297">toohost your application in Azure, you must first provision hello Azure services that your application requires.</span></span> <span data-ttu-id="101d2-298">exemple d’application Hello dans ce didacticiel utilise hello suivant des services Azure.</span><span class="sxs-lookup"><span data-stu-id="101d2-298">hello sample application in this tutorial uses hello following Azure services.</span></span>

* <span data-ttu-id="101d2-299">Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="101d2-299">Azure Redis Cache</span></span>
* <span data-ttu-id="101d2-300">Application web App Service</span><span class="sxs-lookup"><span data-stu-id="101d2-300">App Service Web App</span></span>
* <span data-ttu-id="101d2-301">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="101d2-301">SQL Database</span></span>

<span data-ttu-id="101d2-302">toodeploy ces services tooa nouvelle ou existante de la ressource de groupe de votre choix, cliquez sur hello suivant **déployer tooAzure** bouton.</span><span class="sxs-lookup"><span data-stu-id="101d2-302">toodeploy these services tooa new or existing resource group of your choice, click hello following **Deploy tooAzure** button.</span></span>

<span data-ttu-id="101d2-303">[! [Déploiement tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="101d2-303">[![Deploy tooAzure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="101d2-304">Cela **déployer tooAzure** bouton utilise hello [créer une application Web ainsi que le Cache Redis et la base de données SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) modèle tooprovision ces services et le jeu de hello chaîne de connexion pour le paramètre hello hello et de base de données SQL de l’application pour hello chaîne de connexion du Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="101d2-304">This **Deploy tooAzure** button uses hello [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template tooprovision these services and set hello connection string for hello SQL Database and hello application setting for hello Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="101d2-305">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte Azure gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="101d2-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="101d2-306">En cliquant sur hello **déployer tooAzure** bouton vous permet de toohello portail Azure et lance hello le processus de création de ressources hello décrits par le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-306">Clicking hello **Deploy tooAzure** button takes you toohello Azure portal and initiates hello process of creating hello resources described by hello template.</span></span>

![Déployer tooAzure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="101d2-308">Bonjour **notions de base** section, sélectionnez toouse d’abonnement Azure hello, sélectionnez un groupe de ressources existant ou créez-en un et spécifier l’emplacement du groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-308">In hello **Basics** section, select hello Azure subscription toouse, and select an existing resource group or create a new one, and specify hello resource group location.</span></span>
2. <span data-ttu-id="101d2-309">Bonjour **paramètres** section, spécifiez une **connexion administrateur** (n’utilisez pas **admin**), **mot de passe administrateur**et  **Nom de base de données**.</span><span class="sxs-lookup"><span data-stu-id="101d2-309">In hello **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="101d2-310">Hello autres paramètres sont configurés pour un Service d’applications libre qui héberge le plan et les options de faible coût de hello de base de données SQL et du Cache Redis Azure, qui ne sont fournis avec un niveau gratuit.</span><span class="sxs-lookup"><span data-stu-id="101d2-310">hello other parameters are configured for a free App Service hosting plan, and lower-cost options for hello SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Déployer tooAzure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="101d2-312">Après avoir configuré les paramètres de hello souhaité, faites défiler fin toohello de page de hello hello lecture et les conditions et vérifiez hello **J’accepte les termes du contrat de toohello et conditions susmentionnées** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="101d2-312">After configuring hello desired settings, scroll toohello end of hello page, read hello terms and conditions, and check hello **I agree toohello terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="101d2-313">toobegin configurer les ressources hello, cliquez sur **bon**.</span><span class="sxs-lookup"><span data-stu-id="101d2-313">toobegin provisioning hello resources, click **Purchase**.</span></span>

<span data-ttu-id="101d2-314">progression de hello tooview de votre déploiement, cliquez sur l’icône de hello et cliquez sur **déploiement démarré**.</span><span class="sxs-lookup"><span data-stu-id="101d2-314">tooview hello progress of your deployment, click hello notification icon and click **Deployment started**.</span></span>

![Le déploiement a commencé][cache-deployment-started]

<span data-ttu-id="101d2-316">Vous pouvez afficher l’état hello de votre déploiement sur hello **Microsoft.Template** panneau.</span><span class="sxs-lookup"><span data-stu-id="101d2-316">You can view hello status of your deployment on hello **Microsoft.Template** blade.</span></span>

![Déployer tooAzure][cache-deploy-to-azure-step-3]

<span data-ttu-id="101d2-318">Lors de la configuration est terminée, vous pouvez publier votre tooAzure d’application à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="101d2-318">When provisioning is complete, you can publish your application tooAzure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="101d2-319">Toutes les erreurs qui peuvent se produire pendant le processus d’approvisionnement de hello sont affichés sur hello **Microsoft.Template** panneau.</span><span class="sxs-lookup"><span data-stu-id="101d2-319">Any errors that may occur during hello provisioning process are displayed on hello **Microsoft.Template** blade.</span></span> <span data-ttu-id="101d2-320">Les erreurs courantes sont liées à un trop grand nombre de serveurs SQL ou de plans d’hébergement Free App Service par abonnement.</span><span class="sxs-lookup"><span data-stu-id="101d2-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="101d2-321">Corrigez les erreurs et redémarrer le processus de hello en cliquant sur **redéployer** sur hello **Microsoft.Template** panneau ou hello **déployer tooAzure** bouton dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="101d2-321">Resolve any errors and restart hello process by clicking **Redeploy** on hello **Microsoft.Template** blade or hello **Deploy tooAzure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-hello-application-tooazure"></a><span data-ttu-id="101d2-322">Publier hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="101d2-322">Publish hello application tooAzure</span></span>
<span data-ttu-id="101d2-323">Dans cette étape du didacticiel de hello, vous allez publier hello application tooAzure et l’exécuter dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-323">In this step of hello tutorial, you'll publish hello application tooAzure and run it in hello cloud.</span></span>

1. <span data-ttu-id="101d2-324">Avec le bouton hello **ContosoTeamStats** de projet dans Visual Studio et choisissez **publier**.</span><span class="sxs-lookup"><span data-stu-id="101d2-324">Right-click hello **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Publier][cache-publish-app]
2. <span data-ttu-id="101d2-326">Cliquez sur **Microsoft Azure App Service**, choisissez **Select Existing** (Sélectionner existant), puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="101d2-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Publier][cache-publish-to-app-service]
3. <span data-ttu-id="101d2-328">Sélectionnez l’abonnement hello utilisé lors de la création hello ressources Azure, développez groupe de ressources hello contenant des ressources hello et sélectionnez hello souhaité de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="101d2-328">Select hello subscription used when creating hello Azure resources, expand hello resource group containing hello resources, and select hello desired Web App.</span></span> <span data-ttu-id="101d2-329">Si vous avez utilisé hello **déployer tooAzure** bouton commence par le nom de votre application Web **site Web** suivi par des caractères supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="101d2-329">If you used hello **Deploy tooAzure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Sélectionner l’application web][cache-select-web-app]
4. <span data-ttu-id="101d2-331">Cliquez sur **OK** hello toobegin processus de publication.</span><span class="sxs-lookup"><span data-stu-id="101d2-331">Click **OK** toobegin hello publishing process.</span></span> <span data-ttu-id="101d2-332">Après quelques instants hello processus de publication est terminée et un navigateur est lancé par hello, exemple d’application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="101d2-332">After a few moments hello publishing process completes and a browser is launched with hello running sample application.</span></span> <span data-ttu-id="101d2-333">Si vous obtenez une erreur DNS lors de la validation ou de la publication et hello pour le processus de fourniture hello ressources Azure pour l’application hello récemment terminée, patientez quelques instants, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="101d2-333">If you get a DNS error when validating or publishing, and hello provisioning process for hello Azure resources for hello application has just recently completed, wait a moment and try again.</span></span>
   
    ![Cache ajouté][cache-added-to-application]

<span data-ttu-id="101d2-335">Hello tableau suivant décrit chaque lien d’action à partir de l’exemple d’application hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-335">hello following table describes each action link from hello sample application.</span></span>

| <span data-ttu-id="101d2-336">Action</span><span class="sxs-lookup"><span data-stu-id="101d2-336">Action</span></span> | <span data-ttu-id="101d2-337">Description</span><span class="sxs-lookup"><span data-stu-id="101d2-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="101d2-338">Création</span><span class="sxs-lookup"><span data-stu-id="101d2-338">Create New</span></span> |<span data-ttu-id="101d2-339">Crée une équipe.</span><span class="sxs-lookup"><span data-stu-id="101d2-339">Create a new Team.</span></span> |
| <span data-ttu-id="101d2-340">Play Season</span><span class="sxs-lookup"><span data-stu-id="101d2-340">Play Season</span></span> |<span data-ttu-id="101d2-341">Lire une saison des jeux, des statistiques de mise à jour hello équipe, et désactivez les obsolète des données de l’équipe à partir du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-341">Play a season of games, update hello team stats, and clear any outdated team data from hello cache.</span></span> |
| <span data-ttu-id="101d2-342">Clear Cache</span><span class="sxs-lookup"><span data-stu-id="101d2-342">Clear Cache</span></span> |<span data-ttu-id="101d2-343">Statistiques d’équipe hello clair à partir du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-343">Clear hello team stats from hello cache.</span></span> |
| <span data-ttu-id="101d2-344">List from Cache</span><span class="sxs-lookup"><span data-stu-id="101d2-344">List from Cache</span></span> |<span data-ttu-id="101d2-345">Récupérer les statistiques d’équipe hello à partir du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-345">Retrieve hello team stats from hello cache.</span></span> <span data-ttu-id="101d2-346">S’il existe une absence dans le cache, les statistiques hello de charge à partir de la base de données hello et enregistrer toohello cache pour la prochaine fois.</span><span class="sxs-lookup"><span data-stu-id="101d2-346">If there is a cache miss, load hello stats from hello database and save toohello cache for next time.</span></span> |
| <span data-ttu-id="101d2-347">Sorted Set from Cache</span><span class="sxs-lookup"><span data-stu-id="101d2-347">Sorted Set from Cache</span></span> |<span data-ttu-id="101d2-348">Extraire les statistiques équipe hello cache hello à l’aide d’un ensemble trié.</span><span class="sxs-lookup"><span data-stu-id="101d2-348">Retrieve hello team stats from hello cache using a sorted set.</span></span> <span data-ttu-id="101d2-349">S’il existe une absence dans le cache, les statistiques hello de charge à partir de la base de données hello et enregistrer cache toohello à l’aide d’un ensemble trié.</span><span class="sxs-lookup"><span data-stu-id="101d2-349">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="101d2-350">Top 5 Teams from Cache</span><span class="sxs-lookup"><span data-stu-id="101d2-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="101d2-351">Extraire les équipes de 5 premières hello cache hello à l’aide d’un ensemble trié.</span><span class="sxs-lookup"><span data-stu-id="101d2-351">Retrieve hello top 5 teams from hello cache using a sorted set.</span></span> <span data-ttu-id="101d2-352">S’il existe une absence dans le cache, les statistiques hello de charge à partir de la base de données hello et enregistrer cache toohello à l’aide d’un ensemble trié.</span><span class="sxs-lookup"><span data-stu-id="101d2-352">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="101d2-353">Load from DB</span><span class="sxs-lookup"><span data-stu-id="101d2-353">Load from DB</span></span> |<span data-ttu-id="101d2-354">Récupérer les statistiques hello équipe à partir de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-354">Retrieve hello team stats from hello database.</span></span> |
| <span data-ttu-id="101d2-355">Rebuild DB</span><span class="sxs-lookup"><span data-stu-id="101d2-355">Rebuild DB</span></span> |<span data-ttu-id="101d2-356">Reconstruire la base de données hello et recharger les exemples de données team.</span><span class="sxs-lookup"><span data-stu-id="101d2-356">Rebuild hello database and reload it with sample team data.</span></span> |
| <span data-ttu-id="101d2-357">Edit / Details / Delete</span><span class="sxs-lookup"><span data-stu-id="101d2-357">Edit / Details / Delete</span></span> |<span data-ttu-id="101d2-358">Modifie une équipe, affiche les détails d’une équipe, supprime une équipe.</span><span class="sxs-lookup"><span data-stu-id="101d2-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="101d2-359">Cliquez sur certaines des actions de hello et faire des essais avec la récupération des données de salutation à partir de sources différentes de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-359">Click some of hello actions and experiment with retrieving hello data from hello different sources.</span></span> <span data-ttu-id="101d2-360">Pas les différences de hello dans hello temps toocomplete hello différentes façons de récupérer des données de salutation à partir de la base de données hello et cache de hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-360">Not hello differences in hello time it takes toocomplete hello various ways of retrieving hello data from hello database and hello cache.</span></span>

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a><span data-ttu-id="101d2-361">Supprimer des ressources de hello lorsque vous avez terminé avec l’application hello</span><span class="sxs-lookup"><span data-stu-id="101d2-361">Delete hello resources when you are finished with hello application</span></span>
<span data-ttu-id="101d2-362">Lorsque vous avez terminé avec l’application hello du didacticiel de l’exemple, vous pouvez supprimer hello Azure utilisées dans tooconserve commande coût des ressources et des ressources.</span><span class="sxs-lookup"><span data-stu-id="101d2-362">When you are finished with hello sample tutorial application, you can delete hello Azure resources used in order tooconserve cost and resources.</span></span> <span data-ttu-id="101d2-363">Si vous utilisez hello **déployer tooAzure** bouton Bonjour [configurer hello ressources Azure](#provision-the-azure-resources) section et toutes vos ressources sont contenus dans hello même groupe de ressources, vous pouvez les supprimer ensemble dans un opération en supprimant le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-363">If you use hello **Deploy tooAzure** button in hello [Provision hello Azure resources](#provision-the-azure-resources) section and all of your resources are contained in hello same resource group, you can delete them together in one operation by deleting hello resource group.</span></span>

1. <span data-ttu-id="101d2-364">Connectez-vous à toohello [portail Azure](https://portal.azure.com) et cliquez sur **groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="101d2-364">Sign in toohello [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="101d2-365">Nom de votre groupe de ressources dans hello hello de type **filtrer les éléments...**  zone de texte.</span><span class="sxs-lookup"><span data-stu-id="101d2-365">Type hello name of your resource group into hello **Filter items...** textbox.</span></span>
3. <span data-ttu-id="101d2-366">Cliquez sur **...**  toohello à droite de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="101d2-366">Click **...** toohello right of your resource group.</span></span>
4. <span data-ttu-id="101d2-367">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="101d2-367">Click **Delete**.</span></span>
   
    ![Supprimer][cache-delete-resource-group]
5. <span data-ttu-id="101d2-369">Hello nom de type votre groupe de ressources et cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="101d2-369">Type hello name of your resource group and click **Delete**.</span></span>
   
    ![Confirmation de suppression][cache-delete-confirm]

<span data-ttu-id="101d2-371">Une fois les ressources de hello quelques instants groupe et toutes ses ressources de relation contenant-contenus sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="101d2-371">After a few moments hello resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="101d2-372">Notez que la suppression d’un groupe de ressources est irréversible et ce groupe de ressources hello et toutes les ressources hello qu’il contient sont supprimés définitivement.</span><span class="sxs-lookup"><span data-stu-id="101d2-372">Note that deleting a resource group is irreversible and that hello resource group and all hello resources in it are permanently deleted.</span></span> <span data-ttu-id="101d2-373">Assurez-vous que vous ne supprimez pas accidentellement groupe de ressource incorrect hello ou des ressources.</span><span class="sxs-lookup"><span data-stu-id="101d2-373">Make sure that you do not accidentally delete hello wrong resource group or resources.</span></span> <span data-ttu-id="101d2-374">Si vous avez créé des ressources hello pour l’hébergement de cet exemple à l’intérieur d’un groupe de ressources existant, vous pouvez supprimer individuellement chaque ressource à partir de leurs panneaux respectifs.</span><span class="sxs-lookup"><span data-stu-id="101d2-374">If you created hello resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a><span data-ttu-id="101d2-375">Exécutez l’exemple d’application hello sur votre ordinateur local</span><span class="sxs-lookup"><span data-stu-id="101d2-375">Run hello sample application on your local machine</span></span>
<span data-ttu-id="101d2-376">application de hello toorun localement sur votre ordinateur, vous avez besoin d’un cache Azure Redis Cache d’instance dans le toocache vos données.</span><span class="sxs-lookup"><span data-stu-id="101d2-376">toorun hello application locally on your machine, you need an Azure Redis Cache instance in which toocache your data.</span></span> 

* <span data-ttu-id="101d2-377">Si vous avez publié votre tooAzure application comme décrit dans la section précédente de hello, vous pouvez utiliser l’instance de Cache Redis Azure hello qui a été configuré lors de cette étape.</span><span class="sxs-lookup"><span data-stu-id="101d2-377">If you have published your application tooAzure as described in hello previous section, you can use hello Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="101d2-378">Si vous avez une autre instance de Cache Redis Azure existante, vous pouvez utiliser ce toorun cet exemple localement.</span><span class="sxs-lookup"><span data-stu-id="101d2-378">If you have another existing Azure Redis Cache instance, you can use that toorun this sample locally.</span></span>
* <span data-ttu-id="101d2-379">Si vous devez toocreate une instance de Cache Redis Azure, vous pouvez suivre les étapes de hello dans [créer un cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="101d2-379">If you need toocreate an Azure Redis Cache instance, you can follow hello steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="101d2-380">Une fois que vous avez sélectionnée ou créée hello cache toouse, parcourir le cache toohello Bonjour portail Azure et récupérer hello [nom d’hôte](cache-configure.md#properties) et [clés d’accès](cache-configure.md#access-keys) pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="101d2-380">Once you have selected or created hello cache toouse, browse toohello cache in hello Azure portal and retrieve hello [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="101d2-381">Pour obtenir des instructions, consultez la page [Configuration des paramètres de cache Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="101d2-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="101d2-382">Ouvrez hello `WebAppPlusCacheAppSecrets.config` fichier que vous avez créé au cours de hello [configurer hello application toouse Cache Redis](#configure-the-application-to-use-redis-cache) étape de ce didacticiel à l’aide de l’éditeur hello de votre choix.</span><span class="sxs-lookup"><span data-stu-id="101d2-382">Open hello `WebAppPlusCacheAppSecrets.config` file that you created during hello [Configure hello application toouse Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using hello editor of your choice.</span></span>
2. <span data-ttu-id="101d2-383">Modifier hello `value` d’attribut et remplacez `MyCache.redis.cache.windows.net` avec hello [nom d’hôte](cache-configure.md#properties) de votre cache et spécifiez soit hello [clé primaire ou secondaire](cache-configure.md#access-keys) de votre cache en tant que mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="101d2-383">Edit hello `value` attribute and replace `MyCache.redis.cache.windows.net` with hello [host name](cache-configure.md#properties) of your cache, and specify either hello [primary or secondary key](cache-configure.md#access-keys) of your cache as hello password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="101d2-384">Appuyez sur **Ctrl + F5** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="101d2-384">Press **Ctrl+F5** toorun hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="101d2-385">Notez qu’étant donné que l’application hello, y compris la base de données hello, s’exécute localement et le Cache Redis hello est hébergé dans Azure, hello cache peut apparaître toounder-réaliser hello de bases de données.</span><span class="sxs-lookup"><span data-stu-id="101d2-385">Note that because hello application, including hello database, is running locally and hello Redis Cache is hosted in Azure, hello cache may appear toounder-perform hello database.</span></span> <span data-ttu-id="101d2-386">Pour de meilleures performances, hello application cliente et l’instance de Cache Redis Azure doit être Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="101d2-386">For best performance, hello client application and Azure Redis Cache instance should be in hello same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="101d2-387">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="101d2-387">Next steps</span></span>
* <span data-ttu-id="101d2-388">En savoir plus sur [mise en route avec ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) sur hello [ASP.NET](http://asp.net/) site.</span><span class="sxs-lookup"><span data-stu-id="101d2-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on hello [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="101d2-389">Pour plus d’exemples de création d’une application Web ASP.NET dans le Service d’applications, consultez [créer et déployer une application de web ASP.NET dans Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) de hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 connexion [démonstration](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="101d2-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="101d2-390">Pour plus des Démarrages rapides à partir de la démonstration de HealthClinic.biz hello, consultez [Démarrages rapides outils de développement Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="101d2-390">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="101d2-391">En savoir plus sur hello [Code premier tooa nouvelle base de données](https://msdn.microsoft.com/data/jj193542) approche tooEntity Framework qui est utilisé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="101d2-391">Learn more about hello [Code first tooa new database](https://msdn.microsoft.com/data/jj193542) approach tooEntity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="101d2-392">Apprenez-en davantage sur les [applications web dans Azure App Service](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="101d2-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="101d2-393">Découvrez comment trop[moniteur](cache-how-to-monitor.md) votre cache Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="101d2-393">Learn how too[monitor](cache-how-to-monitor.md) your cache in hello Azure portal.</span></span>
* <span data-ttu-id="101d2-394">Explorez les fonctionnalités Premium du Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="101d2-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="101d2-395">La persistance tooconfigure Premium Azure Redis cache</span><span class="sxs-lookup"><span data-stu-id="101d2-395">How tooconfigure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="101d2-396">Comment tooconfigure clustering Premium Azure Redis cache</span><span class="sxs-lookup"><span data-stu-id="101d2-396">How tooconfigure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="101d2-397">Comment tooconfigure réseau virtuel prend en charge un Premium Azure Redis cache</span><span class="sxs-lookup"><span data-stu-id="101d2-397">How tooconfigure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="101d2-398">Consultez hello [Azure Redis Cache-FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) pour plus d’informations sur la taille, le débit et la bande passante avec des caches de niveau premium.</span><span class="sxs-lookup"><span data-stu-id="101d2-398">See hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

