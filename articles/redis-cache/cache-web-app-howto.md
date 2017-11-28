---
title: "Création d’une application web avec le Cache Redis | Microsoft Docs"
description: "Découvrez comment créer une application web avec le Cache Redis"
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
ms.openlocfilehash: f23f71cc01eccf17d36885f786de9a7517606803
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-web-app-with-redis-cache"></a><span data-ttu-id="ba1cc-103">Création d’une application web avec le Cache Redis</span><span class="sxs-lookup"><span data-stu-id="ba1cc-103">How to create a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba1cc-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ba1cc-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="ba1cc-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ba1cc-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="ba1cc-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ba1cc-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="ba1cc-107">Java</span><span class="sxs-lookup"><span data-stu-id="ba1cc-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="ba1cc-108">Python</span><span class="sxs-lookup"><span data-stu-id="ba1cc-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="ba1cc-109">Ce didacticiel montre comment créer et déployer une application web ASP.NET dans une application web dans Azure App Service en utilisant Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-109">This tutorial shows how to create and deploy an ASP.NET web application to a web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="ba1cc-110">L’exemple d’application affiche une liste des statistiques d’équipe d’une base de données et montre les différentes façons d’utiliser le Cache Redis Azure pour stocker et récupérer des données à partir du cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-110">The sample application displays a list of team statistics from a database and shows different ways to use Azure Redis Cache to store and retrieve data from the cache.</span></span> <span data-ttu-id="ba1cc-111">Lorsque vous aurez terminé le didacticiel, vous disposerez d’une application web, optimisée avec le Cache Redis Azure et hébergée dans Azure, effectuant des opérations de lecture et écriture sur une base de données.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-111">When you complete the tutorial you'll have a running web app that reads and writes to a database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="ba1cc-112">Vous apprendrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ba1cc-112">You'll learn:</span></span>

* <span data-ttu-id="ba1cc-113">comment créer une application web ASP.NET MVC 5 dans Visual Studio ;</span><span class="sxs-lookup"><span data-stu-id="ba1cc-113">How to create an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="ba1cc-114">comment accéder aux données à partir d’une base de données à l’aide d’Entity Framework ;</span><span class="sxs-lookup"><span data-stu-id="ba1cc-114">How to access data from a database using Entity Framework.</span></span>
* <span data-ttu-id="ba1cc-115">comment améliorer le débit des données et réduire la charge de la base de données en stockant et en récupérant des données à l’aide du Cache Redis Azure ;</span><span class="sxs-lookup"><span data-stu-id="ba1cc-115">How to improve data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="ba1cc-116">comment utiliser un ensemble trié Redis pour récupérer les 5 meilleures équipes ;</span><span class="sxs-lookup"><span data-stu-id="ba1cc-116">How to use a Redis sorted set to retrieve the top 5 teams.</span></span>
* <span data-ttu-id="ba1cc-117">comment approvisionner des ressources Azure pour l’application à l’aide d’un modèle Resource Manager ;</span><span class="sxs-lookup"><span data-stu-id="ba1cc-117">How to provision the Azure resources for the application using a Resource Manager template.</span></span>
* <span data-ttu-id="ba1cc-118">comment publier l’application sur Azure avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-118">How to publish the application to Azure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba1cc-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ba1cc-119">Prerequisites</span></span>
<span data-ttu-id="ba1cc-120">Pour suivre ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ba1cc-120">To complete the tutorial, you must have the following prerequisites.</span></span>

* [<span data-ttu-id="ba1cc-121">Compte Azure</span><span class="sxs-lookup"><span data-stu-id="ba1cc-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="ba1cc-122">Visual Studio 2017 avec le Kit de développement logiciel (SDK) Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="ba1cc-122">Visual Studio 2017 with the Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="ba1cc-123">Compte Azure</span><span class="sxs-lookup"><span data-stu-id="ba1cc-123">Azure account</span></span>
<span data-ttu-id="ba1cc-124">Pour suivre ce didacticiel, vous avez besoin d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-124">You need an Azure account to complete the tutorial.</span></span> <span data-ttu-id="ba1cc-125">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="ba1cc-125">You can:</span></span>

* <span data-ttu-id="ba1cc-126">[Ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="ba1cc-127">Vous obtenez des crédits que vous pouvez utiliser pour essayer des services Azure payants.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-127">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="ba1cc-128">Même après que les crédits sont épuisés, vous pouvez conserver le compte et utiliser les services et fonctionnalités Azure gratuits.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-128">Even after the credits are used up, you can keep the account and use free Azure services and features.</span></span>
* <span data-ttu-id="ba1cc-129">[Activez les avantages d’abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="ba1cc-130">Votre abonnement MSDN vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-the-azure-sdk-for-net"></a><span data-ttu-id="ba1cc-131">Visual Studio 2017 avec le Kit de développement logiciel (SDK) Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="ba1cc-131">Visual Studio 2017 with the Azure SDK for .NET</span></span>
<span data-ttu-id="ba1cc-132">Ce didacticiel a été rédigé pour Visual Studio 2017 avec le [Kit de développement logiciel (SDK) Azure pour .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-132">The tutorial is written for Visual Studio 2017 with the [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="ba1cc-133">Le Kit de développement logiciel (SDK) version 2.9.5 est inclus dans le programme d’installation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-133">The Azure SDK 2.9.5 is included with the Visual Studio installer.</span></span>

<span data-ttu-id="ba1cc-134">Si vous utilisez Visual Studio 2015, vous pouvez suivre le didacticiel avec le [Kit de développement logiciel (SDK) Azure pour .NET](../dotnet-sdk.md) version 2.8.2 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-134">If you have Visual Studio 2015, you can follow the tutorial with the [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="ba1cc-135">[Cliquez ici pour télécharger la dernière version du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-135">[Download the latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="ba1cc-136">Visual Studio est automatiquement installé avec le SDK si vous n’en disposez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-136">Visual Studio is automatically installed with the SDK if you don't already have it.</span></span> <span data-ttu-id="ba1cc-137">Certains écrans diffèrent des illustrations présentées dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-137">Some screens may look different from the illustrations shown in this tutorial.</span></span>

<span data-ttu-id="ba1cc-138">Si vous utilisez Visual Studio 2013, vous pouvez [télécharger la dernière version du Kit de développement logiciel (SDK) Azure pour Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-138">If you have Visual Studio 2013, you can [download the latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="ba1cc-139">Certains écrans diffèrent des illustrations présentées dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-139">Some screens may look different from the illustrations shown in this tutorial.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="ba1cc-140">Créer le projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba1cc-140">Create the Visual Studio project</span></span>
1. <span data-ttu-id="ba1cc-141">Ouvrez Visual Studio et cliquez sur **Fichier**, **Nouveau**, **Projet**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="ba1cc-142">Développez le nœud **Visual C#** dans la liste **Modèles**, sélectionnez **Cloud**, puis cliquez sur **Application web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-142">Expand the **Visual C#** node in the **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="ba1cc-143">Vérifiez que l’option **.NET Framework 4.5.2** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="ba1cc-144">Tapez **ContosoTeamStats** dans la zone de texte **Nom** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-144">Type **ContosoTeamStats** into the **Name** textbox and click **OK**.</span></span>
   
    ![Créer un projet][cache-create-project]
3. <span data-ttu-id="ba1cc-146">Sélectionnez le type de projet **MVC** .</span><span class="sxs-lookup"><span data-stu-id="ba1cc-146">Select **MVC** as the project type.</span></span> 

    <span data-ttu-id="ba1cc-147">Vérifiez que la valeur **Aucune authentification** est spécifiée dans les paramètres **Authentification**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-147">Ensure that **No Authentication** is specified for the **Authentication** settings.</span></span> <span data-ttu-id="ba1cc-148">Selon votre version de Visual Studio, la valeur par défaut peut être différente.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-148">Depending on your version of Visual Studio, the default may be set to something else.</span></span> <span data-ttu-id="ba1cc-149">Pour la modifier, cliquez sur **Modifier l’authentification** et sélectionnez **Aucune authentification**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-149">To change it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="ba1cc-150">Si vous poursuivez la procédure avec Visual Studio 2015, décochez la case **Héberger dans le cloud**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-150">If you are following along with Visual Studio 2015, clear the **Host in the cloud** checkbox.</span></span> <span data-ttu-id="ba1cc-151">Vous [approvisionnerez les ressources Azure](#provision-the-azure-resources) et [publierez l’application sur Azure](#publish-the-application-to-azure) au cours des étapes suivantes du didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-151">You'll [provision the Azure resources](#provision-the-azure-resources) and [publish the application to Azure](#publish-the-application-to-azure) in subsequent steps in the tutorial.</span></span> <span data-ttu-id="ba1cc-152">Pour obtenir un exemple d’approvisionnement d’application web App Service à partir de Visual Studio en laissant la case à cocher **Héberger sur le cloud** activée, consultez [Prise en main de Web Apps dans Azure App Service à l’aide d’ASP.NET et Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in the cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Sélectionner un modèle de projet][cache-select-template]
4. <span data-ttu-id="ba1cc-154">Cliquez sur **OK** pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-154">Click **OK** to create the project.</span></span>

## <a name="create-the-aspnet-mvc-application"></a><span data-ttu-id="ba1cc-155">Créer l’application ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="ba1cc-155">Create the ASP.NET MVC application</span></span>
<span data-ttu-id="ba1cc-156">Dans cette section du didacticiel, vous allez créer l’application de base qui lit et affiche les statistiques d’équipe à partir d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-156">In this section of the tutorial, you'll create the basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="ba1cc-157">Ajouter le package NuGet Entity Framework</span><span class="sxs-lookup"><span data-stu-id="ba1cc-157">Add the Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="ba1cc-158">Ajouter le modèle</span><span class="sxs-lookup"><span data-stu-id="ba1cc-158">Add the model</span></span>](#add-the-model)
* [<span data-ttu-id="ba1cc-159">Ajouter le contrôleur</span><span class="sxs-lookup"><span data-stu-id="ba1cc-159">Add the controller</span></span>](#add-the-controller)
* [<span data-ttu-id="ba1cc-160">Configurer les vues</span><span class="sxs-lookup"><span data-stu-id="ba1cc-160">Configure the views</span></span>](#configure-the-views)

### <a name="add-the-entity-framework-nuget-package"></a><span data-ttu-id="ba1cc-161">Ajouter le package NuGet Entity Framework</span><span class="sxs-lookup"><span data-stu-id="ba1cc-161">Add the Entity Framework NuGet package</span></span>

1. <span data-ttu-id="ba1cc-162">Dans le menu **Outils**, cliquez sur **Gestionnaire de package NuGet**, puis **Console du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-162">Click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="ba1cc-163">Exécutez la commande suivante dans la fenêtre **Console du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-163">Run the following command from the **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="ba1cc-164">Pour plus d’informations sur ce package, consultez la page NuGet [EntityFramework](https://www.nuget.org/packages/EntityFramework/).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-164">For more information about this package, see the [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-the-model"></a><span data-ttu-id="ba1cc-165">Ajouter le modèle</span><span class="sxs-lookup"><span data-stu-id="ba1cc-165">Add the model</span></span>
1. <span data-ttu-id="ba1cc-166">Cliquez avec le bouton droit sur **Modèles** dans l’**Explorateur de solutions** et sélectionnez **Ajouter**, **Classe**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Ajouter un modèle][cache-model-add-class]
2. <span data-ttu-id="ba1cc-168">Entrez le nom de classe `Team` et cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-168">Enter `Team` for the class name and click **Add**.</span></span>
   
    ![Ajouter une classe de modèle][cache-model-add-class-dialog]
3. <span data-ttu-id="ba1cc-170">Remplacez les instructions `using` au début du fichier `Team.cs` par les instructions `using` suivantes.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-170">Replace the `using` statements at the top of the `Team.cs` file with the following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="ba1cc-171">Remplacez la définition de la classe `Team` par l’extrait de code suivant, qui contient une définition de classe `Team` mise à jour, ainsi que d’autres classes d’assistance Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-171">Replace the definition of the `Team` class with the following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="ba1cc-172">Pour plus d’informations sur l’approche Code First d’Entity Framework utilisée dans ce didacticiel, consultez [Code First pour une nouvelle base de données](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-172">For more information on the code first approach to Entity Framework that's used in this tutorial, see [Code first to a new database](https://msdn.microsoft.com/data/jj193542).</span></span>

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


1. <span data-ttu-id="ba1cc-173">Dans l’**Explorateur de solutions**, double-cliquez sur le fichier **web.config** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-173">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="ba1cc-175">Ajoutez la section `connectionStrings` suivante.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-175">Add the following `connectionStrings` section.</span></span> <span data-ttu-id="ba1cc-176">Le nom de la chaîne de connexion doit correspondre au nom de la classe de contexte de base de données Entity Framework, qui est `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-176">The name of the connection string must match the name of the Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="ba1cc-177">Vous pouvez ajouter la nouvelle section `connectionStrings` afin qu’elle suive `configSections`, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-177">You can add the new `connectionStrings` section so that it follows `configSections`, as shown in the following example.</span></span>

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
    > <span data-ttu-id="ba1cc-178">Votre chaîne de connexion peut être différente selon les versions de Visual Studio et de SQL Server Express utilisées pour suivre le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-178">Your connection string may be different depending on the version of Visual Studio and SQL Server Express edition used to complete the tutorial.</span></span> <span data-ttu-id="ba1cc-179">Le modèle web.config doit être configuré pour correspondre à votre installation et peut contenir des entrées `Data Source` telles que `(LocalDB)\v11.0` (à partir de SQL Server Express 2012) ou `Data Source=(LocalDB)\MSSQLLocalDB` (à partir de SQL Server Express 2014 et versions ultérieures).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-179">The web.config template should be configured to match your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="ba1cc-180">Pour plus d’informations sur les chaînes de connexion et les versions de SQL Express, consultez [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-the-controller"></a><span data-ttu-id="ba1cc-181">Ajouter le contrôleur</span><span class="sxs-lookup"><span data-stu-id="ba1cc-181">Add the controller</span></span>
1. <span data-ttu-id="ba1cc-182">Appuyez sur **F6** pour générer le projet.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-182">Press **F6** to build the project.</span></span> 
2. <span data-ttu-id="ba1cc-183">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le dossier **Contrôleurs**. Cliquez ensuite sur **Ajouter** puis sur **Contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-183">In **Solution Explorer**, right-click the **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Ajouter un contrôleur][cache-add-controller]
3. <span data-ttu-id="ba1cc-185">Sélectionnez **Contrôleur MVC 5 avec vues, en utilisant Entity Framework**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="ba1cc-186">Si vous obtenez une erreur après avoir cliqué sur **Ajouter**, assurez-vous que vous avez déjà généré le projet.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-186">If you get an error after clicking **Add**, ensure that you have built the project first.</span></span>
   
    ![Ajouter une classe de contrôleur][cache-add-controller-class]
4. <span data-ttu-id="ba1cc-188">Sélectionnez **Team (ContosoTeamStats.Models)** dans la liste déroulante **Classe de modèle**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-188">Select **Team (ContosoTeamStats.Models)** from the **Model class** drop-down list.</span></span> <span data-ttu-id="ba1cc-189">Sélectionnez **TeamContext (ContosoTeamStats.Models)** dans la liste déroulante **Classe du contexte de données**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-189">Select **TeamContext (ContosoTeamStats.Models)** from the **Data context class** drop-down list.</span></span> <span data-ttu-id="ba1cc-190">Tapez `TeamsController` dans la zone de texte **Nom du contrôleur** (si elle n’est pas remplie automatiquement).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-190">Type `TeamsController` in the **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="ba1cc-191">Cliquez sur **Ajouter** pour créer la classe de contrôleur et ajouter les vues par défaut.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-191">Click **Add** to create the controller class and add the default views.</span></span>
   
    ![Configurer un contrôleur][cache-configure-controller]
5. <span data-ttu-id="ba1cc-193">Dans l’**Explorateur de solutions**, développez **Global.asax**, puis double-cliquez sur **Global.asax.cs** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** to open it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="ba1cc-195">Ajoutez les deux instructions `using` suivantes au début du fichier, sous les autres instructions `using`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-195">Add the following two `using` statements at the top of the file under the other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="ba1cc-196">Ajoutez la ligne de code ci-après à la fin de la méthode `Application_Start` .</span><span class="sxs-lookup"><span data-stu-id="ba1cc-196">Add the following line of code at the end of the `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="ba1cc-197">Dans l’**Explorateur de solutions**, développez `App_Start` et double-cliquez sur `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="ba1cc-199">Dans le code suivant, dans la méthode `RegisterRoutes`, remplacez `controller = "Home"` par `controller = "Teams"`, comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-199">Replace `controller = "Home"` in the following code in the `RegisterRoutes` method with `controller = "Teams"` as shown in the following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-the-views"></a><span data-ttu-id="ba1cc-200">Configurer les vues</span><span class="sxs-lookup"><span data-stu-id="ba1cc-200">Configure the views</span></span>
1. <span data-ttu-id="ba1cc-201">Dans l’**Explorateur de solutions**, développez le dossier **Vues** puis le dossier **Partagé** et double-cliquez sur **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-201">In **Solution Explorer**, expand the **Views** folder and then the **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="ba1cc-203">Modifiez le contenu de l’élément `title` et remplacez `My ASP.NET Application` par `Contoso Team Stats`, comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-203">Change the contents of the `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in the following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="ba1cc-204">Dans la section `body`, mettez à jour la première instruction `Html.ActionLink`, remplacez `Application name` par `Contoso Team Stats` et remplacez `Home` par `Teams`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-204">In the `body` section, update the first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="ba1cc-205">Avant : `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="ba1cc-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="ba1cc-206">Après : `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="ba1cc-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Modifications du code][cache-layout-cshtml-code]
2. <span data-ttu-id="ba1cc-208">Appuyez sur **Ctrl+F5** pour générer et exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-208">Press **Ctrl+F5** to build and run the application.</span></span> <span data-ttu-id="ba1cc-209">Cette version de l’application lit les résultats directement à partir de la base de données.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-209">This version of the application reads the results directly from the database.</span></span> <span data-ttu-id="ba1cc-210">Notez les actions **Créer**, **Modifier**, **Détails** et **Supprimer** qui ont été automatiquement ajoutées à l’application par le modèle automatique **Contrôleur MVC 5 avec vues, en utilisant Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-210">Note the **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added to the application by the **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="ba1cc-211">Dans la section suivante du didacticiel, vous allez ajouter le Cache Redis pour optimiser l’accès aux données et fournir des fonctionnalités supplémentaires à l’application.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-211">In the next section of the tutorial you'll add Redis Cache to optimize the data access and provide additional features to the application.</span></span>

![Application de départ][cache-starter-application]

## <a name="configure-the-application-to-use-redis-cache"></a><span data-ttu-id="ba1cc-213">Configurer l’application pour utiliser le Cache Redis</span><span class="sxs-lookup"><span data-stu-id="ba1cc-213">Configure the application to use Redis Cache</span></span>
<span data-ttu-id="ba1cc-214">Dans cette section du didacticiel, vous allez configurer l’exemple d’application pour stocker et récupérer des statistiques d’équipe Contoso à partir d’une instance de Cache Redis Azure à l’aide du client de cache [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .</span><span class="sxs-lookup"><span data-stu-id="ba1cc-214">In this section of the tutorial, you'll configure the sample application to store and retrieve Contoso team statistics from an Azure Redis Cache instance by using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="ba1cc-215">Configurer l’application pour utiliser StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="ba1cc-215">Configure the application to use StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="ba1cc-216">Mettre à jour la classe TeamsController pour retourner des résultats à partir du cache ou de la base de données</span><span class="sxs-lookup"><span data-stu-id="ba1cc-216">Update the TeamsController class to return results from the cache or the database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="ba1cc-217">Mettre à jour les méthodes Create, Edit et Delete pour utiliser le cache</span><span class="sxs-lookup"><span data-stu-id="ba1cc-217">Update the Create, Edit, and Delete methods to work with the cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="ba1cc-218">Mettre à jour la vue Teams Index pour utiliser le cache</span><span class="sxs-lookup"><span data-stu-id="ba1cc-218">Update the Teams Index view to work with the cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-the-application-to-use-stackexchangeredis"></a><span data-ttu-id="ba1cc-219">Configurer l’application pour utiliser StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="ba1cc-219">Configure the application to use StackExchange.Redis</span></span>
1. <span data-ttu-id="ba1cc-220">Pour configurer une application cliente dans Visual Studio avec le package NuGet StackExchange.Redis, cliquez sur **Gestionnaire de package NuGet**, **Console du Gestionnaire de package** dans le menu **Outils**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-220">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="ba1cc-221">Exécutez la commande suivante depuis la fenêtre `Package Manager Console`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-221">Run the following command from the `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="ba1cc-222">Le package NuGet télécharge et ajoute les références d'assembly nécessaires pour que votre application cliente puisse accéder à Cache Redis Azure avec le client du cache StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-222">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span> <span data-ttu-id="ba1cc-223">Si vous préférez utiliser une version avec nom fort de la bibliothèque du client `StackExchange.Redis`, installez le package `StackExchange.Redis.StrongName`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-223">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="ba1cc-224">Dans l’**Explorateur de solutions**, développez le dossier **Contrôleurs** et double-cliquez sur **TeamsController.cs** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-224">In **Solution Explorer**, expand the **Controllers** folder and double-click **TeamsController.cs** to open it.</span></span>
   
    ![Contrôleur Teams][cache-teamscontroller]
4. <span data-ttu-id="ba1cc-226">Ajoutez les deux instructions `using` suivantes à **TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-226">Add the following two `using` statements to **TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="ba1cc-227">Ajoutez les deux propriétés suivantes à la classe `TeamsController` .</span><span class="sxs-lookup"><span data-stu-id="ba1cc-227">Add the following two properties to the `TeamsController` class.</span></span>

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

6. <span data-ttu-id="ba1cc-228">Créez un fichier nommé `WebAppPlusCacheAppSecrets.config` sur votre ordinateur et placez-le dans un emplacement qui ne sera pas archivé avec le code source de votre exemple d’application au cas où vous décideriez de l’archiver à un emplacement quelconque.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with the source code of your sample application, should you decide to check it in somewhere.</span></span> <span data-ttu-id="ba1cc-229">Dans cet exemple, le fichier `AppSettingsSecrets.config` se trouve sous `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-229">In this example the `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="ba1cc-230">Modifiez le fichier `WebAppPlusCacheAppSecrets.config` et ajoutez le contenu suivant.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-230">Edit the `WebAppPlusCacheAppSecrets.config` file and add the following contents.</span></span> <span data-ttu-id="ba1cc-231">Si vous exécutez l’application localement, ces informations sont utilisées pour vous connecter à votre instance de Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-231">If you run the application locally this information is used to connect to your Azure Redis Cache instance.</span></span> <span data-ttu-id="ba1cc-232">Plus loin dans ce didacticiel, vous allez approvisionner une instance de Cache Redis Azure et mettre à jour le nom et le mot de passe du cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-232">Later in the tutorial you'll provision an Azure Redis Cache instance and update the cache name and password.</span></span> <span data-ttu-id="ba1cc-233">Si vous ne souhaitez pas exécuter l’exemple d’application localement, vous pouvez ignorer la création de ce fichier et les étapes suivantes qui référencent le fichier. En effet, lorsque vous déployez sur Azure, l’application récupère les informations de connexion de cache à partir du paramètre d’application de l’application web et non à partir de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-233">If you don't plan to run the sample application locally you can skip the creation of this file and the subsequent steps that reference the file, because when you deploy to Azure the application retrieves the cache connection information from the app setting for the Web App and not from this file.</span></span> <span data-ttu-id="ba1cc-234">Étant donné que `WebAppPlusCacheAppSecrets.config` n’est pas déployé sur Azure avec votre application, vous n’en avez pas besoin, sauf si vous souhaitez exécuter l’application localement.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-234">Since the `WebAppPlusCacheAppSecrets.config` is not deployed to Azure with your application, you don't need it unless you are going to run the application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="ba1cc-235">Dans l’**Explorateur de solutions**, double-cliquez sur le fichier **web.config** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-235">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="ba1cc-237">Ajoutez l’attribut `file` suivant à l’élément `appSettings`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-237">Add the following `file` attribute to the `appSettings` element.</span></span> <span data-ttu-id="ba1cc-238">Si vous avez utilisé un autre nom de fichier ou un autre emplacement, remplacez ces valeurs pour celles indiquées dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-238">If you used a different file name or location, substitute those values for the ones shown in the example.</span></span>
   
   * <span data-ttu-id="ba1cc-239">Avant : `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="ba1cc-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="ba1cc-240">Après : ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="ba1cc-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="ba1cc-241">Le runtime ASP.NET fusionne le contenu du fichier externe avec le balisage dans l’élément `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-241">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span></span> <span data-ttu-id="ba1cc-242">Le runtime ignore l’attribut de fichier si le fichier spécifié est introuvable.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-242">The runtime ignores the file attribute if the specified file cannot be found.</span></span> <span data-ttu-id="ba1cc-243">Vos secrets (la chaîne de connexion à votre cache) ne sont pas inclus dans le code source de l’application.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-243">Your secrets (the connection string to your cache) are not included as part of the source code for the application.</span></span> <span data-ttu-id="ba1cc-244">Lorsque vous déployez votre application web sur Azure, le fichier `WebAppPlusCacheAppSecrests.config` n’est pas déployé (c’est ce que vous souhaitez).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-244">When you deploy your web app to Azure, the `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="ba1cc-245">Il existe plusieurs façons de spécifier ces secrets dans Azure. Ils seront configurés automatiquement pour vous lorsque vous [approvisionnerez les ressources Azure](#provision-the-azure-resources) plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-245">There are several ways to specify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision the Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="ba1cc-246">Pour en savoir plus sur l’utilisation des secrets dans Azure, voir [Meilleures pratiques portant sur le déploiement de mots de passe et autres données sensibles dans ASP.NET et Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database"></a><span data-ttu-id="ba1cc-247">Mettre à jour la classe TeamsController pour retourner des résultats à partir du cache ou de la base de données</span><span class="sxs-lookup"><span data-stu-id="ba1cc-247">Update the TeamsController class to return results from the cache or the database</span></span>
<span data-ttu-id="ba1cc-248">Dans cet exemple, les statistiques d’équipe peuvent être récupérées à partir de la base de données ou à partir du cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-248">In this sample, team statistics can be retrieved from the database or from the cache.</span></span> <span data-ttu-id="ba1cc-249">Les statistiques d’équipe sont stockées dans le cache comme `List<Team>`sérialisé et comme ensemble trié à l’aide des types de données Redis.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-249">Team statistics are stored in the cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="ba1cc-250">Lors de la récupération des éléments d’un ensemble trié, vous pouvez récupérer certains éléments, récupérer tous les éléments ou effectuer une requête sur certains éléments.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="ba1cc-251">Dans cet exemple, vous allez interroger l’ensemble trié pour trouver les 5 meilleures équipes, classées par nombre de victoires.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-251">In this sample you'll query the sorted set for the top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="ba1cc-252">Il n’est pas nécessaire de stocker les statistiques d’équipe dans plusieurs formats dans le cache pour utiliser le Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-252">It is not required to store the team statistics in multiple formats in the cache in order to use Azure Redis Cache.</span></span> <span data-ttu-id="ba1cc-253">Ce didacticiel utilise plusieurs formats pour illustrer certaines façons de mettre des données en cache et les différents types de données que vous pouvez utiliser à cette fin.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-253">This tutorial uses multiple formats to demonstrate some of the different ways and different data types you can use to cache data.</span></span>
> 
> 

1. <span data-ttu-id="ba1cc-254">Ajoutez les instructions `using` suivantes au début du fichier `TeamsController.cs`, avec les autres instructions `using`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-254">Add the following `using` statements to the `TeamsController.cs` file at the top with the other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="ba1cc-255">Remplacez la méthode d’implémentation `public ActionResult Index()` actuelle par l’implémentation suivante.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-255">Replace the current `public ActionResult Index()` method implementation with the following implementation.</span></span>

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

            case "clearCache": // Clear the results from the cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild the database with sample data.
                RebuildDB();
                break;
        }

        // Measure the time it takes to retrieve the results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve the top 5 teams from the sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from the cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from the database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add the elapsed time of the operation to the ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="ba1cc-256">Ajoutez les trois méthodes suivantes à la classe `TeamsController` pour implémenter les types d’action `playGames`, `clearCache` et `rebuildDB` de l’instruction switch ajoutée dans l’extrait de code précédent.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-256">Add the following three methods to the `TeamsController` class to implement the `playGames`, `clearCache`, and `rebuildDB` action types from the switch statement added in the previous code snippet.</span></span>
   
    <span data-ttu-id="ba1cc-257">La méthode `PlayGames` met à jour les statistiques d’équipe en simulant une saison de jeux, enregistre les résultats dans la base de données et efface les données désormais obsolètes à partir du cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-257">The `PlayGames` method updates the team statistics by simulating a season of games, saves the results to the database, and clears the now outdated data from the cache.</span></span>

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

    <span data-ttu-id="ba1cc-258">La méthode `RebuildDB` réinitialise la base de données avec l’ensemble d’équipes par défaut, génère des statistiques pour ces équipes et efface les données désormais obsolètes à partir du cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-258">The `RebuildDB` method reinitializes the database with the default set of teams, generates statistics for them, and clears the now outdated data from the cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize the database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="ba1cc-259">La méthode `ClearCachedTeams` supprime du cache toutes les statistiques d’équipe mises en cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-259">The `ClearCachedTeams` method removes any cached team statistics from the cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="ba1cc-260">Ajoutez les quatre méthodes suivantes à la classe `TeamsController` pour implémenter les différentes façons de récupérer les statistiques d’équipe à partir du cache et de la base de données.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-260">Add the following four methods to the `TeamsController` class to implement the various ways of retrieving the team statistics from the cache and the database.</span></span> <span data-ttu-id="ba1cc-261">Chacune de ces méthodes retourne un `List<Team>` qui est ensuite affiché par la vue.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-261">Each of these methods returns a `List<Team>` which is then displayed by the view.</span></span>
   
    <span data-ttu-id="ba1cc-262">La méthode `GetFromDB` lit les statistiques d’équipe à partir de la base de données.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-262">The `GetFromDB` method reads the team statistics from the database.</span></span>
   
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

    <span data-ttu-id="ba1cc-263">La méthode `GetFromList` lit les statistiques d’équipe à partir du cache en tant que `List<Team>` sérialisé.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-263">The `GetFromList` method reads the team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="ba1cc-264">En cas d’absence dans le cache, les statistiques d’équipe sont lues à partir de la base de données, puis stockées dans le cache pour la prochaine fois.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-264">If there is a cache miss, the team statistics are read from the database and then stored in the cache for next time.</span></span> <span data-ttu-id="ba1cc-265">Dans cet exemple, nous utilisons la sérialisation JSON.NET pour sérialiser les objets .NET vers et depuis le cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-265">In this sample we're using JSON.NET serialization to serialize the .NET objects to and from the cache.</span></span> <span data-ttu-id="ba1cc-266">Pour plus d’informations, consultez la rubrique [Utilisation des objets .NET dans le cache Redis Azure](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-266">For more information, see [How to work with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

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

            ViewBag.msg += "Storing results to cache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="ba1cc-267">La méthode `GetFromSortedSet` lit les statistiques d’équipe à partir d’un ensemble trié en cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-267">The `GetFromSortedSet` method reads the team statistics from a cached sorted set.</span></span> <span data-ttu-id="ba1cc-268">En cas d’absence dans le cache, les statistiques d’équipe sont lues à partir de la base de données, puis stockées dans le cache en tant qu’ensemble trié.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-268">If there is a cache miss, the team statistics are read from the database and stored in the cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
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

            ViewBag.msg += "Storing results to cache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding to sorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="ba1cc-269">La méthode `GetFromSortedSetTop5` lit les 5 meilleures équipes à partir de l’ensemble trié en cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-269">The `GetFromSortedSetTop5` method reads the top 5 teams from the cached sorted set.</span></span> <span data-ttu-id="ba1cc-270">Elle commence par vérifier l’existence de la clé `teamsSortedSet` dans le cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-270">It starts by checking the cache for the existence of the `teamsSortedSet` key.</span></span> <span data-ttu-id="ba1cc-271">Si cette clé n’est pas présente, la méthode `GetFromSortedSet` est appelée pour lire les statistiques d’équipe et les stocker dans le cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-271">If this key is not present, the `GetFromSortedSet` method is called to read the team statistics and store them in the cache.</span></span> <span data-ttu-id="ba1cc-272">Ensuite, l’ensemble trié mis en cache est interrogé de façon à trouver les 5 meilleures équipes, qui sont retournées.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-272">Next, the cached sorted set is queried for the top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load the entire sorted set into the cache.
            GetFromSortedSet();

            // Retrieve the top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get the top 5 teams from the sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-the-create-edit-and-delete-methods-to-work-with-the-cache"></a><span data-ttu-id="ba1cc-273">Mettre à jour les méthodes Create, Edit et Delete pour utiliser le cache</span><span class="sxs-lookup"><span data-stu-id="ba1cc-273">Update the Create, Edit, and Delete methods to work with the cache</span></span>
<span data-ttu-id="ba1cc-274">Le code de génération de modèles automatique qui a été généré dans le cadre de cet exemple inclut des méthodes permettant d’ajouter, modifier et supprimer des équipes.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-274">The scaffolding code that was generated as part of this sample includes methods to add, edit, and delete teams.</span></span> <span data-ttu-id="ba1cc-275">Chaque fois qu’une équipe est ajoutée, modifiée ou supprimée, les données dans le cache deviennent obsolètes.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-275">Anytime a team is added, edited, or removed, the data in the cache becomes outdated.</span></span> <span data-ttu-id="ba1cc-276">Dans cette section, vous allez modifier ces trois méthodes pour effacer les équipes en cache, de sorte que le cache ne soit pas désynchronisé avec la base de données.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-276">In this section you'll modify these three methods to clear the cached teams so that the cache won't be out of sync with the database.</span></span>

1. <span data-ttu-id="ba1cc-277">Accédez à la méthode `Create(Team team)` dans la classe `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-277">Browse to the `Create(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="ba1cc-278">Ajoutez un appel à la méthode `ClearCachedTeams` , comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-278">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Create
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="ba1cc-279">Accédez à la méthode `Edit(Team team)` dans la classe `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-279">Browse to the `Edit(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="ba1cc-280">Ajoutez un appel à la méthode `ClearCachedTeams` , comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-280">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="ba1cc-281">Accédez à la méthode `DeleteConfirmed(int id)` dans la classe `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-281">Browse to the `DeleteConfirmed(int id)` method in the `TeamsController` class.</span></span> <span data-ttu-id="ba1cc-282">Ajoutez un appel à la méthode `ClearCachedTeams` , comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-282">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, the cache is out of date.
        // Clear the cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-the-teams-index-view-to-work-with-the-cache"></a><span data-ttu-id="ba1cc-283">Mettre à jour la vue Teams Index pour utiliser le cache</span><span class="sxs-lookup"><span data-stu-id="ba1cc-283">Update the Teams Index view to work with the cache</span></span>
1. <span data-ttu-id="ba1cc-284">Dans l’**Explorateur de solutions**, développez le dossier **Vues** puis le dossier **Équipes**, et double-cliquez sur **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-284">In **Solution Explorer**, expand the **Views** folder, then the **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="ba1cc-286">Au début du fichier, recherchez l’élément de paragraphe suivant.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-286">Near the top of the file, look for the following paragraph element.</span></span>
   
    ![Table d’actions][cache-teams-index-table]
   
    <span data-ttu-id="ba1cc-288">Il s’agit du lien permettant de créer une équipe.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-288">This is the link to create a new team.</span></span> <span data-ttu-id="ba1cc-289">Remplacez l’élément de paragraphe par la table suivante.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-289">Replace the paragraph element with the following table.</span></span> <span data-ttu-id="ba1cc-290">Cette table contient des liens d’action pour créer une nouvelle équipe, jouer une nouvelle saison de jeux, effacer le cache, récupérer les équipes à partir du cache dans plusieurs formats, récupérer les équipes à partir de la base de données et reconstruire la base de données avec de nouvelles données d’exemple.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-290">This table has action links for creating a new team, playing a new season of games, clearing the cache, retrieving the teams from the cache in several formats, retrieving the teams from the database, and rebuilding the database with fresh sample data.</span></span>

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


1. <span data-ttu-id="ba1cc-291">Faites défiler le fichier **Index.cshtml`tr` vers le bas pour visualiser la fin du fichier, puis ajoutez l’élément**  suivant, de sorte qu’il représente la dernière ligne de la dernière table du fichier.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-291">Scroll to the bottom of the **Index.cshtml** file and add the following `tr` element so that it is the last row in the last table in the file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="ba1cc-292">Cette ligne affiche la valeur `ViewBag.Msg` qui contient un rapport d’état sur l’opération en cours.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-292">This row displays the value of `ViewBag.Msg` which contains a status report about the current operation.</span></span> <span data-ttu-id="ba1cc-293">La valeur `ViewBag.Msg` est définie lorsque vous cliquez sur l’un des liens d’action à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-293">The `ViewBag.Msg` is set when you click any of the action links from the previous step.</span></span>   
   
    ![Message d’état][cache-status-message]
2. <span data-ttu-id="ba1cc-295">Appuyez sur **F6** pour générer le projet.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-295">Press **F6** to build the project.</span></span>

## <a name="provision-the-azure-resources"></a><span data-ttu-id="ba1cc-296">Approvisionner les ressources Azure</span><span class="sxs-lookup"><span data-stu-id="ba1cc-296">Provision the Azure resources</span></span>
<span data-ttu-id="ba1cc-297">Pour héberger votre application dans Azure, vous devez d’abord approvisionner les services Azure requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-297">To host your application in Azure, you must first provision the Azure services that your application requires.</span></span> <span data-ttu-id="ba1cc-298">L’exemple d’application de ce didacticiel utilise les services Azure suivants.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-298">The sample application in this tutorial uses the following Azure services.</span></span>

* <span data-ttu-id="ba1cc-299">Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="ba1cc-299">Azure Redis Cache</span></span>
* <span data-ttu-id="ba1cc-300">Application web App Service</span><span class="sxs-lookup"><span data-stu-id="ba1cc-300">App Service Web App</span></span>
* <span data-ttu-id="ba1cc-301">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="ba1cc-301">SQL Database</span></span>

<span data-ttu-id="ba1cc-302">Pour déployer ces services vers un groupe de ressources de votre choix, nouveau ou existant, cliquez sur le bouton **Déployer dans Azure** ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-302">To deploy these services to a new or existing resource group of your choice, click the following **Deploy to Azure** button.</span></span>

<span data-ttu-id="ba1cc-303">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="ba1cc-303">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="ba1cc-304">Le bouton **Déployer dans Azure** utilise le modèle de [démarrage rapide Microsoft Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Création d’une application web, du Cache Redis et d’une base de données SQL](https://github.com/Azure/azure-quickstart-templates) pour approvisionner ces services et définir la chaîne de connexion pour la base de données SQL et le paramètre d’application de la chaîne de connexion du Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-304">This **Deploy to Azure** button uses the [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template to provision these services and set the connection string for the SQL Database and the application setting for the Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="ba1cc-305">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte Azure gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="ba1cc-306">Le bouton **Déployer dans Azure** vous permet d’accéder au Portail Azure et lance le processus de création des ressources décrit par le modèle.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-306">Clicking the **Deploy to Azure** button takes you to the Azure portal and initiates the process of creating the resources described by the template.</span></span>

![Déployer dans Azure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="ba1cc-308">Dans la section des **paramètres de base**, sélectionnez l’abonnement Azure à utiliser et un groupe de ressources existant ou créez-en un nouveau et spécifiez l’emplacement du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-308">In the **Basics** section, select the Azure subscription to use, and select an existing resource group or create a new one, and specify the resource group location.</span></span>
2. <span data-ttu-id="ba1cc-309">Dans la section **Paramètres**, spécifiez un **nom de connexion administrateur** (n’utilisez pas **admin**), un **mot de passe de connexion administrateur** et un **nom de base de données**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-309">In the **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="ba1cc-310">Les autres paramètres sont configurés pour un plan d’hébergement Free App Service et des options moins coûteuses pour la base de données SQL et le Cache Redis Azure, qui ne sont pas fournis avec un niveau Gratuit.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-310">The other parameters are configured for a free App Service hosting plan, and lower-cost options for the SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Déployer dans Azure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="ba1cc-312">Après avoir configuré les paramètres souhaités, faites défiler jusqu’à la fin de la page, lisez les termes et conditions et cochez la case **J’accepte les termes et conditions mentionnés ci-dessus**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-312">After configuring the desired settings, scroll to the end of the page, read the terms and conditions, and check the **I agree to the terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="ba1cc-313">Pour commencer l’approvisionnement des ressources, cliquez sur **Purchase** (Acheter).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-313">To begin provisioning the resources, click **Purchase**.</span></span>

<span data-ttu-id="ba1cc-314">Pour afficher la progression de votre déploiement, cliquez sur l’icône de notification, puis cliquez sur **Le déploiement a commencé**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-314">To view the progress of your deployment, click the notification icon and click **Deployment started**.</span></span>

![Le déploiement a commencé][cache-deployment-started]

<span data-ttu-id="ba1cc-316">Vous pouvez visualiser l’état de votre déploiement dans le panneau **Microsoft.Template** .</span><span class="sxs-lookup"><span data-stu-id="ba1cc-316">You can view the status of your deployment on the **Microsoft.Template** blade.</span></span>

![Déployer dans Azure][cache-deploy-to-azure-step-3]

<span data-ttu-id="ba1cc-318">Une fois l’approvisionnement terminé, vous pouvez publier votre application sur Azure à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-318">When provisioning is complete, you can publish your application to Azure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="ba1cc-319">Les erreurs susceptibles de se produire pendant le processus d’approvisionnement sont affichées dans le panneau **Microsoft.Template** .</span><span class="sxs-lookup"><span data-stu-id="ba1cc-319">Any errors that may occur during the provisioning process are displayed on the **Microsoft.Template** blade.</span></span> <span data-ttu-id="ba1cc-320">Les erreurs courantes sont liées à un trop grand nombre de serveurs SQL ou de plans d’hébergement Free App Service par abonnement.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="ba1cc-321">Corrigez les erreurs et redémarrez le processus en cliquant sur **Redéployer** dans le panneau **Microsoft.Template** ou sur le bouton **Déployer dans Azure** de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-321">Resolve any errors and restart the process by clicking **Redeploy** on the **Microsoft.Template** blade or the **Deploy to Azure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-the-application-to-azure"></a><span data-ttu-id="ba1cc-322">Publier l’application sur Azure</span><span class="sxs-lookup"><span data-stu-id="ba1cc-322">Publish the application to Azure</span></span>
<span data-ttu-id="ba1cc-323">Dans cette étape du didacticiel, vous allez publier l’application sur Azure et l’exécuter dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-323">In this step of the tutorial, you'll publish the application to Azure and run it in the cloud.</span></span>

1. <span data-ttu-id="ba1cc-324">Cliquez avec le bouton droit sur le projet **ContosoTeamStats** dans Visual Studio, puis choisissez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-324">Right-click the **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Publier][cache-publish-app]
2. <span data-ttu-id="ba1cc-326">Cliquez sur **Microsoft Azure App Service**, choisissez **Select Existing** (Sélectionner existant), puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Publier][cache-publish-to-app-service]
3. <span data-ttu-id="ba1cc-328">Sélectionnez l’abonnement utilisé lors de la création des ressources Azure, développez le groupe de ressources contenant les ressources et sélectionnez l’application web souhaitée.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-328">Select the subscription used when creating the Azure resources, expand the resource group containing the resources, and select the desired Web App.</span></span> <span data-ttu-id="ba1cc-329">Si vous avez utilisé le bouton **Déployer dans Azure**, le nom de votre application web commence par **webSite** et contient des caractères supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-329">If you used the **Deploy to Azure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Sélectionner l’application web][cache-select-web-app]
4. <span data-ttu-id="ba1cc-331">Cliquez sur **OK** pour démarrer le processus de publication.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-331">Click **OK** to begin the publishing process.</span></span> <span data-ttu-id="ba1cc-332">Après quelques instants, le processus de publication se termine et un navigateur s’ouvre. L’exemple d’application y est exécuté.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-332">After a few moments the publishing process completes and a browser is launched with the running sample application.</span></span> <span data-ttu-id="ba1cc-333">Si vous obtenez une erreur DNS lors de la validation ou de la publication et que le processus d’approvisionnement des ressources Azure pour l’application vient de se terminer, attendez un instant et réessayez.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-333">If you get a DNS error when validating or publishing, and the provisioning process for the Azure resources for the application has just recently completed, wait a moment and try again.</span></span>
   
    ![Cache ajouté][cache-added-to-application]

<span data-ttu-id="ba1cc-335">Le tableau suivant décrit chaque lien d’action de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-335">The following table describes each action link from the sample application.</span></span>

| <span data-ttu-id="ba1cc-336">Action</span><span class="sxs-lookup"><span data-stu-id="ba1cc-336">Action</span></span> | <span data-ttu-id="ba1cc-337">Description</span><span class="sxs-lookup"><span data-stu-id="ba1cc-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ba1cc-338">Création</span><span class="sxs-lookup"><span data-stu-id="ba1cc-338">Create New</span></span> |<span data-ttu-id="ba1cc-339">Crée une équipe.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-339">Create a new Team.</span></span> |
| <span data-ttu-id="ba1cc-340">Play Season</span><span class="sxs-lookup"><span data-stu-id="ba1cc-340">Play Season</span></span> |<span data-ttu-id="ba1cc-341">Joue une saison de jeux, met à jour les statistiques d’équipe et efface les données d’équipe obsolètes du cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-341">Play a season of games, update the team stats, and clear any outdated team data from the cache.</span></span> |
| <span data-ttu-id="ba1cc-342">Clear Cache</span><span class="sxs-lookup"><span data-stu-id="ba1cc-342">Clear Cache</span></span> |<span data-ttu-id="ba1cc-343">Efface les statistiques d’équipe du cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-343">Clear the team stats from the cache.</span></span> |
| <span data-ttu-id="ba1cc-344">List from Cache</span><span class="sxs-lookup"><span data-stu-id="ba1cc-344">List from Cache</span></span> |<span data-ttu-id="ba1cc-345">Récupère les statistiques d’équipe à partir cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-345">Retrieve the team stats from the cache.</span></span> <span data-ttu-id="ba1cc-346">En cas d’absence dans le cache, charge les statistiques à partir de la base de données et les enregistre dans le cache pour la prochaine fois.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-346">If there is a cache miss, load the stats from the database and save to the cache for next time.</span></span> |
| <span data-ttu-id="ba1cc-347">Sorted Set from Cache</span><span class="sxs-lookup"><span data-stu-id="ba1cc-347">Sorted Set from Cache</span></span> |<span data-ttu-id="ba1cc-348">Récupère les statistiques d’équipe du cache à l’aide d’un ensemble trié.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-348">Retrieve the team stats from the cache using a sorted set.</span></span> <span data-ttu-id="ba1cc-349">En cas d’absence dans le cache, charge les statistiques à partir de la base de données et les enregistre dans le cache à l’aide d’un ensemble trié.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-349">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="ba1cc-350">Top 5 Teams from Cache</span><span class="sxs-lookup"><span data-stu-id="ba1cc-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="ba1cc-351">Récupère les 5 meilleures équipes à partir du cache à l’aide d’un ensemble trié.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-351">Retrieve the top 5 teams from the cache using a sorted set.</span></span> <span data-ttu-id="ba1cc-352">En cas d’absence dans le cache, charge les statistiques à partir de la base de données et les enregistre dans le cache à l’aide d’un ensemble trié.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-352">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="ba1cc-353">Load from DB</span><span class="sxs-lookup"><span data-stu-id="ba1cc-353">Load from DB</span></span> |<span data-ttu-id="ba1cc-354">Récupère les statistiques d’équipe à partir de la base de données.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-354">Retrieve the team stats from the database.</span></span> |
| <span data-ttu-id="ba1cc-355">Rebuild DB</span><span class="sxs-lookup"><span data-stu-id="ba1cc-355">Rebuild DB</span></span> |<span data-ttu-id="ba1cc-356">Reconstruit la base de données et la recharge avec les exemples de données d’équipe.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-356">Rebuild the database and reload it with sample team data.</span></span> |
| <span data-ttu-id="ba1cc-357">Edit / Details / Delete</span><span class="sxs-lookup"><span data-stu-id="ba1cc-357">Edit / Details / Delete</span></span> |<span data-ttu-id="ba1cc-358">Modifie une équipe, affiche les détails d’une équipe, supprime une équipe.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="ba1cc-359">Cliquez sur certaines actions et essayez de récupérer les données de différentes sources.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-359">Click some of the actions and experiment with retrieving the data from the different sources.</span></span> <span data-ttu-id="ba1cc-360">Notez que le temps nécessaire pour récupérer les données à partir de la base de données et du cache varie selon la méthode utilisée.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-360">Not the differences in the time it takes to complete the various ways of retrieving the data from the database and the cache.</span></span>

## <a name="delete-the-resources-when-you-are-finished-with-the-application"></a><span data-ttu-id="ba1cc-361">Supprimer les ressources une fois la procédure liée à l’application terminée</span><span class="sxs-lookup"><span data-stu-id="ba1cc-361">Delete the resources when you are finished with the application</span></span>
<span data-ttu-id="ba1cc-362">Lorsque vous avez terminé avec l’exemple d’application du didacticiel, vous pouvez supprimer les ressources Azure utilisées afin de réduire les coûts et de préserver les ressources.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-362">When you are finished with the sample tutorial application, you can delete the Azure resources used in order to conserve cost and resources.</span></span> <span data-ttu-id="ba1cc-363">Si vous utilisez le bouton **Déployer dans Azure** dans la section [Approvisionner les ressources Azure](#provision-the-azure-resources) et que toutes vos ressources se trouvent dans le même groupe de ressources, vous pouvez les supprimer en une seule opération en supprimant le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-363">If you use the **Deploy to Azure** button in the [Provision the Azure resources](#provision-the-azure-resources) section and all of your resources are contained in the same resource group, you can delete them together in one operation by deleting the resource group.</span></span>

1. <span data-ttu-id="ba1cc-364">Connectez-vous au [Portail Azure](https://portal.azure.com) et cliquez sur **Groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-364">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="ba1cc-365">Tapez le nom de votre groupe de ressources dans la zone de texte **Filtrer des éléments...** .</span><span class="sxs-lookup"><span data-stu-id="ba1cc-365">Type the name of your resource group into the **Filter items...** textbox.</span></span>
3. <span data-ttu-id="ba1cc-366">Cliquez sur **…** à droite de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-366">Click **...** to the right of your resource group.</span></span>
4. <span data-ttu-id="ba1cc-367">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-367">Click **Delete**.</span></span>
   
    ![Supprimer][cache-delete-resource-group]
5. <span data-ttu-id="ba1cc-369">Tapez le nom de votre groupe de ressources et cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-369">Type the name of your resource group and click **Delete**.</span></span>
   
    ![Confirmation de suppression][cache-delete-confirm]

<span data-ttu-id="ba1cc-371">Après quelques instants, le groupe de ressources et toutes les ressources qu’il contient sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-371">After a few moments the resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba1cc-372">Notez que la suppression d’un groupe de ressources est irréversible et que le groupe de ressources, ainsi que toutes les ressources qu’il contient, sont supprimés définitivement.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-372">Note that deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="ba1cc-373">Veillez à ne pas supprimer accidentellement des ressources ou un groupe de ressources incorrects.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-373">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="ba1cc-374">Si vous avez créé les ressources pour l’hébergement de cet exemple à l’intérieur d’un groupe de ressources existant, vous pouvez supprimer individuellement chaque ressource à partir de leurs panneaux respectifs.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-374">If you created the resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-the-sample-application-on-your-local-machine"></a><span data-ttu-id="ba1cc-375">Exécuter l’exemple d’application sur votre ordinateur local</span><span class="sxs-lookup"><span data-stu-id="ba1cc-375">Run the sample application on your local machine</span></span>
<span data-ttu-id="ba1cc-376">Pour exécuter l’application localement sur votre ordinateur, vous avez besoin d’une instance de Cache Redis Azure dans laquelle mettre en cache vos données.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-376">To run the application locally on your machine, you need an Azure Redis Cache instance in which to cache your data.</span></span> 

* <span data-ttu-id="ba1cc-377">Si vous avez publié votre application sur Azure comme décrit dans la section précédente, vous pouvez utiliser l’instance de Cache Redis Azure approvisionnée lors de cette étape.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-377">If you have published your application to Azure as described in the previous section, you can use the Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="ba1cc-378">Si vous avez une autre instance de Cache Redis Azure, vous pouvez l’utiliser pour exécuter cet exemple localement.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-378">If you have another existing Azure Redis Cache instance, you can use that to run this sample locally.</span></span>
* <span data-ttu-id="ba1cc-379">Si vous avez besoin de créer une instance de Cache Redis Azure, vous pouvez suivre les étapes de la section [Création d’un cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-379">If you need to create an Azure Redis Cache instance, you can follow the steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="ba1cc-380">Une fois que vous avez sélectionné ou créé le cache à utiliser, accédez au cache dans le Portail Azure et récupérez le [nom d’hôte](cache-configure.md#properties) et les [clés d’accès](cache-configure.md#access-keys) pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-380">Once you have selected or created the cache to use, browse to the cache in the Azure portal and retrieve the [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="ba1cc-381">Pour obtenir des instructions, consultez la page [Configuration des paramètres de cache Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="ba1cc-382">Ouvrez le fichier `WebAppPlusCacheAppSecrets.config` que vous avez créé au cours de l’étape [Configurer l’application pour utiliser le Cache Redis](#configure-the-application-to-use-redis-cache) de ce didacticiel à l’aide de l’éditeur de votre choix.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-382">Open the `WebAppPlusCacheAppSecrets.config` file that you created during the [Configure the application to use Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using the editor of your choice.</span></span>
2. <span data-ttu-id="ba1cc-383">Modifiez l’attribut `value` et remplacez `MyCache.redis.cache.windows.net` par le [nom d’hôte](cache-configure.md#properties) de votre cache, puis spécifiez la [clé primaire ou secondaire](cache-configure.md#access-keys) de votre cache en tant que mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-383">Edit the `value` attribute and replace `MyCache.redis.cache.windows.net` with the [host name](cache-configure.md#properties) of your cache, and specify either the [primary or secondary key](cache-configure.md#access-keys) of your cache as the password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="ba1cc-384">Appuyez sur **Ctrl+F5** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-384">Press **Ctrl+F5** to run the application.</span></span>

> [!NOTE]
> <span data-ttu-id="ba1cc-385">Notez que, dans la mesure où l’application (y compris la base de données) s’exécute localement et où le Cache Redis est hébergé dans Azure, il est possible que le cache réduise les performances de la base de données.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-385">Note that because the application, including the database, is running locally and the Redis Cache is hosted in Azure, the cache may appear to under-perform the database.</span></span> <span data-ttu-id="ba1cc-386">Pour de meilleures performances, l’application cliente et l’instance de Cache Redis Azure doivent se trouver au même emplacement.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-386">For best performance, the client application and Azure Redis Cache instance should be in the same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ba1cc-387">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba1cc-387">Next steps</span></span>
* <span data-ttu-id="ba1cc-388">Consultez [Prise en main d’ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) sur le site [ASP.NET](http://asp.net/) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on the [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="ba1cc-389">Pour plus d’exemples de création d’une application web ASP.NET dans App Service, voir [Création d’une application web ASP.NET dans Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) dans la [démonstration](https://github.com/Microsoft/HealthClinic.biz) de 2015 Connect pour [HealthClinic.biz](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="ba1cc-390">Pour d’autres démarrages rapides à partir de la démonstration pour HealthClinic.biz, consultez [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)(Démarrages rapides avec les outils de développement Azure).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-390">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="ba1cc-391">Apprenez-en plus sur l’approche d’Entity Framework [Code First pour une nouvelle base de données](https://msdn.microsoft.com/data/jj193542) utilisée dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-391">Learn more about the [Code first to a new database](https://msdn.microsoft.com/data/jj193542) approach to Entity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="ba1cc-392">Apprenez-en davantage sur les [applications web dans Azure App Service](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba1cc-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="ba1cc-393">Découvrez comment [surveiller](cache-how-to-monitor.md) votre cache dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ba1cc-393">Learn how to [monitor](cache-how-to-monitor.md) your cache in the Azure portal.</span></span>
* <span data-ttu-id="ba1cc-394">Explorez les fonctionnalités Premium du Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="ba1cc-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="ba1cc-395">Comment configurer la persistance pour un Cache Redis Azure Premium</span><span class="sxs-lookup"><span data-stu-id="ba1cc-395">How to configure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="ba1cc-396">Comment configurer le clustering pour un Cache Redis Azure Premium</span><span class="sxs-lookup"><span data-stu-id="ba1cc-396">How to configure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="ba1cc-397">Comment configurer la prise en charge de réseau virtuel pour un Cache Redis Azure Premium</span><span class="sxs-lookup"><span data-stu-id="ba1cc-397">How to configure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="ba1cc-398">Pour plus d’informations sur la taille, le débit et la bande passante des caches Premium, voir le [Forum aux questions sur le Cache Redis Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) .</span><span class="sxs-lookup"><span data-stu-id="ba1cc-398">See the [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

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

