---
title: "Didacticiel ASP.NET MVC pour Azure Cosmos DB : développement d’applications Web | Microsoft Docs"
description: "Didacticiel ASP.NET MVC pour créer une application web MVC à l’aide d’Azure Cosmos DB. Vous allez stocker JSON et accéder aux données à partir d’une application todo hébergée sur des sites web Azure - Didacticiel étape par étape ASP NET MVC."
keywords: "didacticiel asp.net mvc, développement d’application web, application web mvc, didacticiel mvc asp net étape par étape"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: 3f2950fe25feb8f3ee81cc0a79bf624f0ee33bd5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="0c7be-105"><a name="_Toc395809351"></a>Didacticiel ASP.NET MVC : développement d’applications web avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0c7be-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c7be-106">.NET</span><span class="sxs-lookup"><span data-stu-id="0c7be-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="0c7be-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0c7be-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="0c7be-108">Java</span><span class="sxs-lookup"><span data-stu-id="0c7be-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="0c7be-109">Python</span><span class="sxs-lookup"><span data-stu-id="0c7be-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="0c7be-110">Pour mettre en évidence la façon dont vous pouvez exploiter efficacement Azure Cosmos DB pour stocker et interroger les documents JSON, cet article fournit une procédure de bout en bout vous montrant comment créer une application todo à l’aide d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0c7be-110">To highlight how you can efficiently leverage Azure Cosmos DB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="0c7be-111">Les tâches sont stockées en tant que documents JSON dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0c7be-111">The tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Capture d’écran de l’application web todo list MVC créée dans ce didacticiel - Didacticiel étape par étape ASP.NET MVC](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="0c7be-113">Cette procédure pas à pas montre comment utiliser le service Azure Cosmos DB pour stocker des données et y accéder à partir d’une application web ASP.NET MVC hébergée sur Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7be-113">This walk-through shows you how to use the Azure Cosmos DB service to store and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="0c7be-114">Si vous recherchez un didacticiel portant uniquement sur Azure Cosmos DB et non sur les composants ASP.NET MVC, consultez [Azure Cosmos DB : Didacticiel sur la prise en main de l’API DocumentDB](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0c7be-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not the ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="0c7be-115">Ce didacticiel suppose que vous disposez d'une expérience préalable de l'utilisation d'ASP.NET MVC et d'Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="0c7be-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="0c7be-116">Si vous débutez avec ASP.NET ou les [outils requis](#_Toc395637760), nous vous recommandons de télécharger le projet exemple complet à partir de [GitHub][GitHub] et de suivre les instructions fournies dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="0c7be-116">If you are new to ASP.NET or the [prerequisite tools](#_Toc395637760), we recommend downloading the complete sample project from [GitHub][GitHub] and following the instructions in this sample.</span></span> <span data-ttu-id="0c7be-117">Une fois que vous l'avez créé, vous pouvez consulter cet article pour obtenir des informations sur le code dans le contexte du projet.</span><span class="sxs-lookup"><span data-stu-id="0c7be-117">Once you have it built, you can review this article to gain insight on the code in the context of the project.</span></span>
> 
> 

## <span data-ttu-id="0c7be-118"><a name="_Toc395637760"></a>Conditions préalables à l’exécution de ce didacticiel de base de données</span><span class="sxs-lookup"><span data-stu-id="0c7be-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="0c7be-119">Avant de suivre les instructions de cet article, vérifiez que les éléments suivants sont installés :</span><span class="sxs-lookup"><span data-stu-id="0c7be-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="0c7be-120">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="0c7be-120">An active Azure account.</span></span> <span data-ttu-id="0c7be-121">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="0c7be-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0c7be-122">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c7be-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="0c7be-123">OU</span><span class="sxs-lookup"><span data-stu-id="0c7be-123">OR</span></span>

    <span data-ttu-id="0c7be-124">Une installation locale de [l’émulateur Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="0c7be-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="0c7be-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="0c7be-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="0c7be-126">Kit de développement logiciel Microsoft Azure SDK pour .NET de Visual Studio 2017, disponible via Visual Studio Installer.</span><span class="sxs-lookup"><span data-stu-id="0c7be-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through the Visual Studio Installer.</span></span>

<span data-ttu-id="0c7be-127">Toutes les captures d’écran dans cet article ont été effectuées à l’aide de Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="0c7be-127">All the screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="0c7be-128">Si votre système est configuré avec une version différente, il est possible que vos écrans et options ne correspondent pas totalement. Toutefois, si vous respectez les conditions préalables ci-dessus, cette solution devrait fonctionner.</span><span class="sxs-lookup"><span data-stu-id="0c7be-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span></span>

## <span data-ttu-id="0c7be-129"><a name="_Toc395637761"></a>Étape 1 : création d’un compte de base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0c7be-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="0c7be-130">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0c7be-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="0c7be-131">Si vous avez déjà un compte SQL (DocumentDB) pour Azure Cosmos DB ou si vous utilisez l’émulateur Azure Cosmos DB pour ce didacticiel, vous pouvez passer à [Créer une nouvelle application web ASP.NET MVC](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="0c7be-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="0c7be-132">Voyons à présent comment créer une application ASP.NET MVC de A à Z.</span><span class="sxs-lookup"><span data-stu-id="0c7be-132">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span></span> 

## <span data-ttu-id="0c7be-133"><a name="_Toc395637762"></a>Étape 2 : création d'une application ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="0c7be-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="0c7be-134">Dans Visual Studio, dans le menu **Fichier**, pointez sur **Nouveau**, puis cliquez sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-134">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="0c7be-135">La boîte de dialogue **Nouveau projet** apparaît.</span><span class="sxs-lookup"><span data-stu-id="0c7be-135">The **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="0c7be-136">Dans le volet **Types de projets**, développez **Modèles**, **Visual C#**, **Web**, puis sélectionnez **Application web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-136">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Capture d'écran de la boîte de dialogue Nouveau projet avec le type de projet d'application web ASP.NET mis en évidence](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="0c7be-138">Dans la zone **Nom** , tapez le nom du projet.</span><span class="sxs-lookup"><span data-stu-id="0c7be-138">In the **Name** box, type the name of the project.</span></span> <span data-ttu-id="0c7be-139">Ce didacticiel utilise le nom « todo ».</span><span class="sxs-lookup"><span data-stu-id="0c7be-139">This tutorial uses the name "todo".</span></span> <span data-ttu-id="0c7be-140">Si vous choisissez d'utiliser un autre nom, chaque fois que ce didacticiel fera référence à l'espace de noms todo, veillez à corriger les exemples de code fournis de façon à utiliser le nom que vous avez attribué à votre application.</span><span class="sxs-lookup"><span data-stu-id="0c7be-140">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span></span> 
4. <span data-ttu-id="0c7be-141">Cliquez sur **Parcourir** pour accéder au dossier où vous souhaitez créer le projet, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-141">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span></span>
   
      <span data-ttu-id="0c7be-142">La boîte de dialogue **Nouvelle application web ASP.NET** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0c7be-142">The **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Capture d’écran de la boîte de dialogue Nouvelle application web ASP.NET avec le modèle d’application MVC mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="0c7be-144">Dans le volet Modèles, sélectionnez **MVC**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-144">In the templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="0c7be-145">Cliquez sur **OK** et laissez Visual Studio structurer le modèle ASP.NET MVC vide.</span><span class="sxs-lookup"><span data-stu-id="0c7be-145">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="0c7be-146">Une fois que Visual Studio a fini de créer l'application MVC réutilisable, vous disposez d'une application ASP.NET vide que vous pouvez exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="0c7be-146">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="0c7be-147">Nous allons sauter l'exécution du projet localement, car je suis sûr que nous avons tous vu l'application « Hello World » ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0c7be-147">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span></span> <span data-ttu-id="0c7be-148">Nous allons maintenant ajouter Azure Cosmos DB à ce projet et créer notre application.</span><span class="sxs-lookup"><span data-stu-id="0c7be-148">Let's go straight to adding Azure Cosmos DB to this project and building our application.</span></span>

## <span data-ttu-id="0c7be-149"><a name="_Toc395637767"></a>Étape 3 : ajout d’Azure Cosmos DB à votre projet d’application web MVC</span><span class="sxs-lookup"><span data-stu-id="0c7be-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB to your MVC web application project</span></span>
<span data-ttu-id="0c7be-150">Maintenant que nous avons la plupart des éléments ASP.NET MVC nécessaires à cette solution, passons au véritable objectif de ce didacticiel, à savoir, ajouter Azure Cosmos DB à notre application web MVC.</span><span class="sxs-lookup"><span data-stu-id="0c7be-150">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure Cosmos DB to our MVC web application.</span></span>

1. <span data-ttu-id="0c7be-151">Le Kit de développement logiciel (SDK) .NET Azure Cosmos DB est empaqueté et distribué en tant que package NuGet.</span><span class="sxs-lookup"><span data-stu-id="0c7be-151">The Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="0c7be-152">Pour obtenir le package NuGet dans Visual Studio, utilisez le gestionnaire de package NuGet dans Visual Studio en cliquant avec le bouton droit sur le projet dans **l’Explorateur de solutions**, puis en cliquant sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-152">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Capture d’écran des options contextuelles pour le projet d’application web dans l’Explorateur de solutions, avec Gérer les packages NuGet mis en surbrillance.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="0c7be-154">La boîte de dialogue **Gérer les packages NuGet** apparaît.</span><span class="sxs-lookup"><span data-stu-id="0c7be-154">The **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="0c7be-155">Dans la zone NuGet **Parcourir**, tapez ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-155">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="0c7be-156">(Le nom du package n’a pas été mis à jour pour Azure Cosmos DB.)</span><span class="sxs-lookup"><span data-stu-id="0c7be-156">(The package name has not been updated to Azure Cosmos DB.)</span></span>
   
    <span data-ttu-id="0c7be-157">À partir des résultats, installez le package **Microsoft.Azure.DocumentDB par Microsoft** .</span><span class="sxs-lookup"><span data-stu-id="0c7be-157">From the results, install the **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="0c7be-158">Cela va vous permettra de télécharger et d’installer le package Azure Cosmos DB, ainsi que toutes les dépendances (telles que Newtonsoft.Json).</span><span class="sxs-lookup"><span data-stu-id="0c7be-158">This will download and install the Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="0c7be-159">Cliquez sur **OK** dans la fenêtre **Aperçu**, puis sur **J’accepte** dans la fenêtre **Acceptation de la licence** pour terminer l’installation.</span><span class="sxs-lookup"><span data-stu-id="0c7be-159">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span></span>
   
    ![Capture d'écran de la fenêtre Gérer les packages NuGet, avec la bibliothèque cliente Microsoft Azure DocumentDB mise en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="0c7be-161">Vous pouvez aussi utiliser la console du Gestionnaire de package pour installer le package.</span><span class="sxs-lookup"><span data-stu-id="0c7be-161">Alternatively you can use the Package Manager Console to install the package.</span></span> <span data-ttu-id="0c7be-162">Pour cela, dans le menu **Outils**, cliquez sur **Gestionnaire de package NuGet**, puis cliquez sur **Console du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-162">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="0c7be-163">À l'invite de commandes, tapez ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="0c7be-163">At the prompt, type the following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="0c7be-164">Une fois que le package est installé, votre solution Visual Studio doit ressembler à ce qui suit avec deux nouvelles références ajoutées, Microsoft.Azure.Documents.Client et Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="0c7be-164">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Capture d’écran de deux références ajoutées au projet de données JSON dans l’Explorateur de solutions](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="0c7be-166"><a name="_Toc395637763"></a>Étape 4 : configuration de l'application ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="0c7be-166"><a name="_Toc395637763"></a>Step 4: Set up the ASP.NET MVC application</span></span>
<span data-ttu-id="0c7be-167">Maintenant nous allons ajouter les modèles, les vues et les contrôleurs à cette application MVC :</span><span class="sxs-lookup"><span data-stu-id="0c7be-167">Now let's add the models, views, and controllers to this MVC application:</span></span>

* <span data-ttu-id="0c7be-168">[Ajout d'un modèle](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="0c7be-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="0c7be-169">[Ajout d'un contrôleur](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="0c7be-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="0c7be-170">[Ajout de vues](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="0c7be-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="0c7be-171"><a name="_Toc395637764"></a>Ajout d’un modèle de données JSON</span><span class="sxs-lookup"><span data-stu-id="0c7be-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="0c7be-172">Commençons par créer le modèle (qui correspond au **M** dans MVC).</span><span class="sxs-lookup"><span data-stu-id="0c7be-172">Let's begin by creating the **M** in MVC, the model.</span></span> 

1. <span data-ttu-id="0c7be-173">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le dossier **Modèles**, cliquez sur **Ajouter**, puis sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-173">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="0c7be-174">La boîte de dialogue **Ajouter un nouvel élément** s'affiche.</span><span class="sxs-lookup"><span data-stu-id="0c7be-174">The **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="0c7be-175">Nommez votre nouvelle classe **Item.cs**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="0c7be-176">Dans ce nouveau fichier **Item.cs** , ajoutez ce qui suit après la dernière *instruction using*.</span><span class="sxs-lookup"><span data-stu-id="0c7be-176">In this new **Item.cs** file, add the following after the last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="0c7be-177">Remplacez maintenant ce code</span><span class="sxs-lookup"><span data-stu-id="0c7be-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="0c7be-178">par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="0c7be-178">with the following code.</span></span>
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    <span data-ttu-id="0c7be-179">Toutes les données d’Azure Cosmos DB sont transmises puis stockées au format JSON.</span><span class="sxs-lookup"><span data-stu-id="0c7be-179">All data in Azure Cosmos DB is passed over the wire and stored as JSON.</span></span> <span data-ttu-id="0c7be-180">Pour contrôler la méthode JSON.NET de sérialisation/désérialisation de vos objets, vous pouvez utiliser l’attribut **JsonProperty**, comme indiqué dans la classe **Item** que nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="0c7be-180">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span></span> <span data-ttu-id="0c7be-181">Vous n'êtes **pas obligé** de procéder ainsi, mais cela permet de s'assurer que les propriétés respectent les conventions d'attribution de noms JSON camelCase.</span><span class="sxs-lookup"><span data-stu-id="0c7be-181">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="0c7be-182">En plus de contrôler le format du nom de propriété au moment d'être transmis à JSON, vous pouvez entièrement renommer vos propriétés .NET, comme ici avec la propriété **Description** .</span><span class="sxs-lookup"><span data-stu-id="0c7be-182">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span></span> 

### <span data-ttu-id="0c7be-183"><a name="_Toc395637765"></a>Ajout d'un contrôleur</span><span class="sxs-lookup"><span data-stu-id="0c7be-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="0c7be-184">Maintenant que nous en avons terminé avec le **M** de MVC, intéressons-nous au **C**, qui correspond à la classe de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="0c7be-184">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="0c7be-185">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le dossier **Contrôleurs**, cliquez sur **Ajouter**, puis sur **Contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-185">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="0c7be-186">La boîte de dialogue **Ajouter une structure** s'affiche.</span><span class="sxs-lookup"><span data-stu-id="0c7be-186">The **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="0c7be-187">Sélectionnez **Classe de contrôleur MVC 5 - Vide** puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Capture d'écran de la boîte de dialogue Ajouter une structure avec l'option Contrôleur MVC 5 - Vide mise en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="0c7be-189">Nommez votre contrôleur **ItemController**</span><span class="sxs-lookup"><span data-stu-id="0c7be-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Capture d'écran de la boîte de dialogue Ajouter un contrôleur](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="0c7be-191">Une fois le fichier créé, votre solution Visual Studio doit ressembler à ce qui suit avec le nouveau fichier ItemController.cs dans l' **Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-191">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="0c7be-192">Le nouveau fichier Item.cs créé précédemment est aussi affiché.</span><span class="sxs-lookup"><span data-stu-id="0c7be-192">The new Item.cs file created earlier is also shown.</span></span>
   
    ![Capture d’écran de la solution Visual Studio - Explorateur de solutions avec le nouveau fichier ItemController.cs et le fichier Item.cs mis en évidence](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="0c7be-194">Vous pouvez fermer ItemController.cs, nous y reviendrons par la suite.</span><span class="sxs-lookup"><span data-stu-id="0c7be-194">You can close ItemController.cs, we'll come back to it later.</span></span> 

### <span data-ttu-id="0c7be-195"><a name="_Toc395637766"></a>Ajout de vues</span><span class="sxs-lookup"><span data-stu-id="0c7be-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="0c7be-196">À présent, créons le **V** de MVC, les vues :</span><span class="sxs-lookup"><span data-stu-id="0c7be-196">Now, let's create the **V** in MVC, the views:</span></span>

* <span data-ttu-id="0c7be-197">[Ajout d'une vue Index de l'élément](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="0c7be-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="0c7be-198">[Ajout d'une vue Nouvel élément](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="0c7be-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="0c7be-199">[Ajout d'une vue Modifier l'élément](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="0c7be-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="0c7be-200"><a name="AddItemIndexView"></a>Ajout d'une vue Index de l'élément</span><span class="sxs-lookup"><span data-stu-id="0c7be-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="0c7be-201">Dans **l’Explorateur de solutions**, développez le dossier **Vues**, cliquez avec le bouton droit sur le dossier vide **Élément** créé automatiquement par Visual Studio quand vous avez ajouté **ItemController** précédemment, cliquez sur **Ajouter**, puis sur **Affichage**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-201">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Capture d’écran de l’Explorateur de solutions présentant le dossier créé par Visual Studio avec les commandes Ajouter/Vue mises en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="0c7be-203">Dans la boîte de dialogue **Ajouter une vue** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0c7be-203">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="0c7be-204">Dans la zone **Nom de la vue**, tapez ***Index***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-204">In the **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="0c7be-205">Dans la zone **Modèle**, sélectionnez ***Liste***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-205">In the **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="0c7be-206">Dans la zone **Classe de modèle**, sélectionnez ***Élément (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-206">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="0c7be-207">Dans la zone de la page de disposition, tapez ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-207">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Capture d'écran présentant la boîte de dialogue Ajouter une vue](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="0c7be-209">Une fois que vous avez défini toutes ces valeurs, cliquez sur **Ajouter** et laissez Visual Studio créer une vue de modèle.</span><span class="sxs-lookup"><span data-stu-id="0c7be-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="0c7be-210">Le fichier .cshtml créé est ensuite ouvert.</span><span class="sxs-lookup"><span data-stu-id="0c7be-210">Once it is done, it will open the cshtml file  that was created.</span></span> <span data-ttu-id="0c7be-211">Nous pouvons fermer ce fichier dans Visual Studio. Nous y reviendrons ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="0c7be-211">We can close that file in Visual Studio as we will come back to it later.</span></span>

#### <span data-ttu-id="0c7be-212"><a name="AddNewIndexView"></a>Ajout d'une vue Nouvel élément</span><span class="sxs-lookup"><span data-stu-id="0c7be-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="0c7be-213">De la même façon que nous avons créé une vue **Index de l’élément**, nous allons maintenant créer une vue permettant de créer des **Éléments**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-213">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="0c7be-214">Dans **l’Explorateur de solutions**, à nouveau, cliquez avec le bouton droit sur le dossier **Élément**, cliquez sur **Ajouter**, puis sur **Affichage**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-214">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="0c7be-215">Dans la boîte de dialogue **Ajouter une vue** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0c7be-215">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="0c7be-216">Dans la zone **Nom de la vue**, tapez ***Create***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-216">In the **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="0c7be-217">Dans la zone **Modèle**, sélectionnez ***Create***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-217">In the **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="0c7be-218">Dans la zone **Classe de modèle**, sélectionnez ***Élément (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-218">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="0c7be-219">Dans la zone de la page de disposition, tapez ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-219">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="0c7be-220">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="0c7be-221"><a name="_Toc395888515"></a>Ajout d'une vue Modifier l'élément</span><span class="sxs-lookup"><span data-stu-id="0c7be-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="0c7be-222">Pour terminer, ajoutons une dernière vue permettant de modifier un **Élément** en suivant la même procédure que précédemment.</span><span class="sxs-lookup"><span data-stu-id="0c7be-222">And finally, add one last view for editing an **Item** in the same way as before.</span></span>

1. <span data-ttu-id="0c7be-223">Dans **l’Explorateur de solutions**, à nouveau, cliquez avec le bouton droit sur le dossier **Élément**, cliquez sur **Ajouter**, puis sur **Affichage**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-223">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="0c7be-224">Dans la boîte de dialogue **Ajouter une vue** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0c7be-224">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="0c7be-225">Dans la zone **Nom de la vue**, tapez ***Edit***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-225">In the **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="0c7be-226">Dans la zone **Modèle**, sélectionnez ***Edit***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-226">In the **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="0c7be-227">Dans la zone **Classe de modèle**, sélectionnez ***Élément (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-227">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="0c7be-228">Dans la zone de la page de disposition, tapez ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="0c7be-228">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="0c7be-229">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-229">Click **Add**.</span></span>

<span data-ttu-id="0c7be-230">Une fois cette opération effectuée, fermez tous les documents .cshtml dans Visual Studio. Nous reviendrons à ces vues un peu plus tard.</span><span class="sxs-lookup"><span data-stu-id="0c7be-230">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span></span>

## <span data-ttu-id="0c7be-231"><a name="_Toc395637769"></a>Étape 5 : liaison d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0c7be-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="0c7be-232">Maintenant que nous nous sommes occupés des éléments de base de MVC, ajoutons le code pour Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0c7be-232">Now that the standard MVC stuff is taken care of, let's turn to adding the code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="0c7be-233">Dans cette section, nous allons ajouter du code pour gérer les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0c7be-233">In this section, we'll add code to handle the following:</span></span>

* <span data-ttu-id="0c7be-234">[Recensement des éléments non terminés.](#_Toc395637770)</span><span class="sxs-lookup"><span data-stu-id="0c7be-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="0c7be-235">[Ajout d'éléments](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="0c7be-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="0c7be-236">[Modification d'éléments](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="0c7be-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="0c7be-237"><a name="_Toc395637770"></a>Établissement de la liste des éléments incomplets dans votre application web MVC</span><span class="sxs-lookup"><span data-stu-id="0c7be-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="0c7be-238">La première chose à faire ici est d’ajouter une classe qui contient toute la logique permettant de se connecter à Azure Cosmos DB et de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="0c7be-238">The first thing to do here is add a class that contains all the logic to connect to and use Azure Cosmos DB.</span></span> <span data-ttu-id="0c7be-239">Pour ce didacticiel, nous allons encapsuler toute cette logique dans une classe de référentiel appelée DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="0c7be-239">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="0c7be-240">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet, cliquez sur **Ajouter**, puis sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-240">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="0c7be-241">Nommez la nouvelle classe **DocumentDBRepository**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-241">Name the new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="0c7be-242">Dans la classe **DocumentDBRepository** nouvellement créée, ajoutez les *instructions using* suivantes au-dessus de la déclaration *namespace*</span><span class="sxs-lookup"><span data-stu-id="0c7be-242">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="0c7be-243">Remplacez maintenant ce code</span><span class="sxs-lookup"><span data-stu-id="0c7be-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="0c7be-244">par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="0c7be-244">with the following code.</span></span>
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. <span data-ttu-id="0c7be-245">Nous allons lire certaines valeurs de la configuration. Pour cela, ouvrez le fichier **Web.config** de votre application et ajoutez les lignes suivantes sous la section `<AppSettings>`.</span><span class="sxs-lookup"><span data-stu-id="0c7be-245">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="0c7be-246">À présent, mettez à jour les valeurs de *endpoint* et *authKey* avec le panneau Clés du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7be-246">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span></span> <span data-ttu-id="0c7be-247">Utilisez **l’URI** du panneau Clés comme valeur du paramètre endpoint et utilisez la valeur de **CLÉ PRIMAIRE** ou de **CLÉ SECONDAIRE** du panneau Clés comme valeur du paramètre authKey.</span><span class="sxs-lookup"><span data-stu-id="0c7be-247">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span></span>

    <span data-ttu-id="0c7be-248">Cette opération assure la connexion du référentiel Azure Cosmos DB. Ajoutons à présent notre logique d’application.</span><span class="sxs-lookup"><span data-stu-id="0c7be-248">That takes care of wiring up the Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="0c7be-249">La première chose que nous souhaitons pouvoir faire avec une application de liste todo est d'afficher les éléments non terminés.</span><span class="sxs-lookup"><span data-stu-id="0c7be-249">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span></span>  <span data-ttu-id="0c7be-250">Copiez et collez l'extrait de code suivant n'importe où dans la classe **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="0c7be-250">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span></span>
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. <span data-ttu-id="0c7be-251">Ouvrez le **ItemController** que nous avons ajouté précédemment et ajoutez les *instructions using* suivantes au-dessus de la déclaration namespace.</span><span class="sxs-lookup"><span data-stu-id="0c7be-251">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="0c7be-252">Si votre projet n'est pas nommé « todo », vous devez mettre à jour « todo.Models; » en fonction du nom de votre projet.</span><span class="sxs-lookup"><span data-stu-id="0c7be-252">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span></span>
   
    <span data-ttu-id="0c7be-253">Remplacez maintenant ce code</span><span class="sxs-lookup"><span data-stu-id="0c7be-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="0c7be-254">par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="0c7be-254">with the following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="0c7be-255">Ouvrez **Global.asax.cs**, puis ajoutez la ligne suivante à la méthode **Application_Start**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-255">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="0c7be-256">À ce stade, votre solution doit pouvoir être générée sans erreur.</span><span class="sxs-lookup"><span data-stu-id="0c7be-256">At this point your solution should be able to build without any errors.</span></span>

<span data-ttu-id="0c7be-257">Si vous exécutiez l’application maintenant, vous pourriez accéder au **HomeController** et à la vue **Index** de ce contrôleur.</span><span class="sxs-lookup"><span data-stu-id="0c7be-257">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span></span> <span data-ttu-id="0c7be-258">Bien qu'il s'agisse du comportement par défaut pour le projet de modèle MVC choisi au début, nous n'en voulons pas.</span><span class="sxs-lookup"><span data-stu-id="0c7be-258">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span></span> <span data-ttu-id="0c7be-259">Modifions le routage de cette application MVC pour changer ce comportement.</span><span class="sxs-lookup"><span data-stu-id="0c7be-259">Let's change the routing on this MVC application to alter this behavior.</span></span>

<span data-ttu-id="0c7be-260">Ouvrez ***App\_Start\RouteConfig.cs***. Recherchez la ligne commençant par « defaults: », puis modifiez-la à l’image de celle qui suit.</span><span class="sxs-lookup"><span data-stu-id="0c7be-260">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="0c7be-261">Ce code indique maintenant à ASP.NET MVC que vous n’avez pas spécifié de valeur dans l’URL pour contrôler le comportement de routage qui, au lieu de **Home**, utilise **Item** comme contrôleur et **Index** comme vue.</span><span class="sxs-lookup"><span data-stu-id="0c7be-261">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span></span>

<span data-ttu-id="0c7be-262">Maintenant, si vous exécutez l’application, elle appellera votre **ItemController**, qui appellera la classe de référentiel et utilisera la méthode GetItems pour retourner tous les éléments non terminés à la vue **Views**\\**Item**\\**Index**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-262">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="0c7be-263">Si vous créez et exécutez ce projet maintenant, vous devriez voir ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="0c7be-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Capture d’écran de l’application web todo list créée dans ce didacticiel de base de données](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="0c7be-265"><a name="_Toc395637771"></a>Ajout d'éléments</span><span class="sxs-lookup"><span data-stu-id="0c7be-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="0c7be-266">Plaçons à présent quelques éléments dans notre base de données afin d'ajouter du contenu à la grille vide.</span><span class="sxs-lookup"><span data-stu-id="0c7be-266">Let's put some items into our database so we have something more than an empty grid to look at.</span></span>

<span data-ttu-id="0c7be-267">Ajoutons du code à AzureCosmosDBRepository et ItemController pour rendre l’enregistrement persistant dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0c7be-267">Let's add some code to  Azure Cosmos DBRepository and ItemController to persist the record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="0c7be-268">Ajoutez la méthode suivante à la classe **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="0c7be-268">Add the following method to your **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="0c7be-269">Cette méthode prend simplement un des objets qui lui est transmis et le rend persistant dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0c7be-269">This method simply takes an object passed to it and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="0c7be-270">Ouvrez le fichier ItemController.cs et ajoutez l'extrait de code suivant dans la classe.</span><span class="sxs-lookup"><span data-stu-id="0c7be-270">Open the ItemController.cs file and add the following code snippet within the class.</span></span> <span data-ttu-id="0c7be-271">C'est ce qui indique à ASP.NET MVC quelles opérations effectuer par rapport à l'action **Create** .</span><span class="sxs-lookup"><span data-stu-id="0c7be-271">This is how ASP.NET MVC knows what to do for the **Create** action.</span></span> <span data-ttu-id="0c7be-272">Dans ce cas, restituez simplement la vue Create.cshtml associée créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="0c7be-272">In this case just render the associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="0c7be-273">Nous devons à présent ajouter du code à ce contrôleur qui acceptera la soumission à partir de la vue **Create** .</span><span class="sxs-lookup"><span data-stu-id="0c7be-273">We now need some more code in this controller that will accept the submission from the **Create** view.</span></span>
3. <span data-ttu-id="0c7be-274">Ajoutez le bloc de code suivant à la classe ItemController.cs qui indique à ASP.NET MVC quoi faire d'une opération POST de formulaire pour ce contrôleur.</span><span class="sxs-lookup"><span data-stu-id="0c7be-274">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span></span>
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    <span data-ttu-id="0c7be-275">Ce code invoque le référentiel DocumentDB et utilise la méthode CreateItemAsync pour conserver la nouvelle tâche dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="0c7be-275">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span></span> 
   
    <span data-ttu-id="0c7be-276">**Note de sécurité** : L’attribut **ValidateAntiForgeryToken** est utilisé ici pour protéger cette application contre les attaques de type falsification de requête intersites.</span><span class="sxs-lookup"><span data-stu-id="0c7be-276">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="0c7be-277">En plus d'ajouter cet attribut, vous devez vérifier que vos vues fonctionnent avec ce jeton anti-falsification.</span><span class="sxs-lookup"><span data-stu-id="0c7be-277">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span></span> <span data-ttu-id="0c7be-278">Pour plus d’informations sur le sujet et pour obtenir des exemples illustrant une implémentation adéquate, consultez la rubrique [Prévention des falsifications de requête intersites][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="0c7be-278">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="0c7be-279">Le code source fourni sur [GitHub][GitHub] comporte l’implémentation complète.</span><span class="sxs-lookup"><span data-stu-id="0c7be-279">The source code provided on [GitHub][GitHub] has the full implementation in place.</span></span>
   
    <span data-ttu-id="0c7be-280">**Note de sécurité** : Nous utilisons également l’attribut **Bind** sur le paramètre de la méthode pour établir une protection contre les attaques par surcharge.</span><span class="sxs-lookup"><span data-stu-id="0c7be-280">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span></span> <span data-ttu-id="0c7be-281">Pour plus d’informations, consultez la rubrique [Opérations CRUD de base dans ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="0c7be-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="0c7be-282">Le code qui permet d'ajouter de nouveaux éléments à la base de données est à présent complet.</span><span class="sxs-lookup"><span data-stu-id="0c7be-282">This concludes the code required to add new Items to our database.</span></span>

### <span data-ttu-id="0c7be-283"><a name="_Toc395637772"></a>Modification d'éléments</span><span class="sxs-lookup"><span data-stu-id="0c7be-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="0c7be-284">La dernière chose à faire est d'ajouter la possibilité de modifier des **éléments** de la base de données et de les marquer comme terminés.</span><span class="sxs-lookup"><span data-stu-id="0c7be-284">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span></span> <span data-ttu-id="0c7be-285">La vue de modification ayant déjà été ajoutée au projet, il convient simplement d'ajouter à nouveau du code au contrôleur et à la classe **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="0c7be-285">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="0c7be-286">Ajoutez le code suivant à la classe **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="0c7be-286">Add the following to the **DocumentDBRepository** class.</span></span>
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    <span data-ttu-id="0c7be-287">La première de ces méthodes, **GetItem**, récupère un élément auprès d’Azure Cosmos DB et le transmet à nouveau à **ItemController**, puis à la vue **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-287">The first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back to the **ItemController** and then on to the **Edit** view.</span></span>
   
    <span data-ttu-id="0c7be-288">La deuxième méthode que nous venons d’ajouter remplace le **document** dans Azure Cosmos DB par la version du **document** transmise par **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-288">The second of the methods we just added replaces the **Document** in Azure Cosmos DB with the version of the **Document** passed in from the **ItemController**.</span></span>
2. <span data-ttu-id="0c7be-289">Ajoutez le code suivant à la classe **ItemController** .</span><span class="sxs-lookup"><span data-stu-id="0c7be-289">Add the following to the **ItemController** class.</span></span>
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    <span data-ttu-id="0c7be-290">La première méthode traite l’opération HTTP GET qui se produit lorsque l’utilisateur clique sur le lien **Edit** de la vue **Index**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-290">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span></span> <span data-ttu-id="0c7be-291">Elle extrait un [**document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) à partir d’Azure Cosmos DB et le transmet à la vue **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it to the **Edit** view.</span></span>
   
    <span data-ttu-id="0c7be-292">La vue **Edit** renvoie ensuite une opération HTTP POST au **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-292">The **Edit** view will then do an Http POST to the **IndexController**.</span></span> 
   
    <span data-ttu-id="0c7be-293">La deuxième méthode que nous avons ajoutée gère la transmission de l’objet mis à jour à Azure Cosmos DB pour le rendre persistant dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="0c7be-293">The second method we added handles passing the updated object to Azure Cosmos DB to be persisted in the database.</span></span>

<span data-ttu-id="0c7be-294">Maintenant que nous avons répertorié les **éléments** non terminés, ajouté des **éléments**, puis modifié des **éléments**, nous sommes en mesure d’exécuter notre application.</span><span class="sxs-lookup"><span data-stu-id="0c7be-294">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="0c7be-295"><a name="_Toc395637773"></a>Étape 6 : exécution de l'application en local</span><span class="sxs-lookup"><span data-stu-id="0c7be-295"><a name="_Toc395637773"></a>Step 6: Run the application locally</span></span>
<span data-ttu-id="0c7be-296">Pour tester l'application sur votre machine locale, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0c7be-296">To test the application on your local machine, do the following:</span></span>

1. <span data-ttu-id="0c7be-297">Appuyez sur F5 dans Visual Studio pour générer l'application en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="0c7be-297">Hit F5 in Visual Studio to build the application in debug mode.</span></span> <span data-ttu-id="0c7be-298">Cette opération doit générer l'application et lancer un navigateur avec la page de grille vide que nous avons vue auparavant :</span><span class="sxs-lookup"><span data-stu-id="0c7be-298">It should build the application and launch a browser with the empty grid page we saw before:</span></span>
   
    ![Capture d’écran de l’application web todo list créée dans ce didacticiel de base de données](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="0c7be-300">Cliquez sur le lien **Créer nouveau** et ajoutez des valeurs aux champs **Nom** et **Description**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-300">Click the **Create New** link and add values to the **Name** and **Description** fields.</span></span> <span data-ttu-id="0c7be-301">Ne cochez pas la case **Terminé**, sinon le nouvel **élément** serait ajouté avec l’état terminé et n’apparaîtrait pas dans la liste initiale.</span><span class="sxs-lookup"><span data-stu-id="0c7be-301">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span></span>
   
    ![Capture d'écran de la vue Create](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="0c7be-303">Cliquez sur **Créer**. Vous êtes alors redirigé vers la vue **Index** et votre **élément** apparaît dans la liste.</span><span class="sxs-lookup"><span data-stu-id="0c7be-303">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span></span>
   
    ![Capture d'écran de la vue Index](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="0c7be-305">Vous êtes libre d'ajouter quelques **éléments** supplémentaires à votre liste.</span><span class="sxs-lookup"><span data-stu-id="0c7be-305">Feel free to add a few more **Items** to your todo list.</span></span>
    
4. <span data-ttu-id="0c7be-306">Cliquez sur **Modifier** en regard d’un **élément** de la liste. Vous êtes alors dirigé vers la vue **Edit** où vous pouvez mettre à jour les propriétés de votre objet, notamment l’indicateur **Completed**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-306">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span></span> <span data-ttu-id="0c7be-307">Si vous marquez l’indicateur **Completed** et cliquez sur **Enregistrer**, **l’élément** est supprimé de la liste des tâches non terminées.</span><span class="sxs-lookup"><span data-stu-id="0c7be-307">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span></span>
   
    ![Capture d'écran de la vue Index avec la case Terminé cochée](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="0c7be-309">Une fois que vous avez testé l'application, appuyez sur Ctrl+F5 pour arrêter le débogage de l'application.</span><span class="sxs-lookup"><span data-stu-id="0c7be-309">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span></span> <span data-ttu-id="0c7be-310">Vous êtes prêt à déployer.</span><span class="sxs-lookup"><span data-stu-id="0c7be-310">You're ready to deploy!</span></span>

## <span data-ttu-id="0c7be-311"><a name="_Toc395637774"></a>Étape 7 : Déployer l'application sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0c7be-311"><a name="_Toc395637774"></a>Step 7: Deploy the application to Azure App Service</span></span> 
<span data-ttu-id="0c7be-312">Maintenant que l’application complète fonctionne correctement avec Azure Cosmos DB, nous allons déployer cette application web vers Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0c7be-312">Now that you have the complete application working correctly with Azure Cosmos DB we're going to deploy this web app to Azure App Service.</span></span>  

1. <span data-ttu-id="0c7be-313">Pour publier cette application, il vous suffit de cliquer avec le bouton droit sur le projet dans **l’Explorateur de solutions**, puis de cliquer sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-313">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Capture d'écran de l'option Publier dans l'Explorateur de solutions](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="0c7be-315">Dans la boîte de dialogue **Publier** , cliquez sur **Microsoft Azure App Service**, puis sélectionnez **Créer** pour créer un profil App Service, ou cliquez sur **Sélectionner Existant** pour utiliser un profil existant.</span><span class="sxs-lookup"><span data-stu-id="0c7be-315">In the **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** to create an App Service profile, or click **Select Existing** to use an existing profile.</span></span>

    ![Publier une boîte de dialogue dans Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="0c7be-317">Si vous possédez un profil Azure App Service existant, entrez votre nom d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="0c7be-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="0c7be-318">Utilisez le filtre **de vue** filtrer pour trier par groupe de ressource ou type de ressource, puis sélectionnez votre Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0c7be-318">Use the **View** filter to sort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Boîte de dialogue App Service dans Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="0c7be-320">Pour créer un nouveau profil Azure App Service, cliquez sur **Créer** dans la boîte de dialogue **Publier** .</span><span class="sxs-lookup"><span data-stu-id="0c7be-320">To create a new Azure App Service profile, click **Create New** in the **Publish** dialog box.</span></span> <span data-ttu-id="0c7be-321">Dans le dialogue **Créer un App Service** , entrez le nom de votre application web et un abonnement approprié, un groupe de ressources et un plan App Service, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0c7be-321">In the **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Créer une boîte de dialogue App Service dans Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="0c7be-323">Dans quelques secondes, Visual Studio achèvera la publication de votre application web et lancera un navigateur dans lequel vous pourrez voir votre réalisation exécutée dans Azure !</span><span class="sxs-lookup"><span data-stu-id="0c7be-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="0c7be-324"><a name="_Toc395637775"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0c7be-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="0c7be-325">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="0c7be-325">Congratulations!</span></span> <span data-ttu-id="0c7be-326">Vous venez de créer votre première application web ASP.NET MVC à l’aide d’Azure Cosmos DB et de la publier sur Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7be-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it to Azure.</span></span> <span data-ttu-id="0c7be-327">Le code source de l'application complète, y compris les fonctionnalités de détail et de suppression qui n'étaient pas incluses dans ce didacticiel, peuvent être téléchargés ou clonés à partir de [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="0c7be-327">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="0c7be-328">Si vous êtes intéressé par l'ajout de ce code à votre application, copiez-le et ajoutez-le à cette dernière.</span><span class="sxs-lookup"><span data-stu-id="0c7be-328">So if you're interested in adding that to your app, grab the code and add it to this app.</span></span>

<span data-ttu-id="0c7be-329">Pour ajouter des fonctionnalités supplémentaires à votre application, passez en revue les API disponibles dans la [bibliothèque Azure Cosmos DB .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) et n’hésitez pas à contribuer à la bibliothèque Azure Cosmos DB .NET sur [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="0c7be-329">To add additional functionality to your application, review the APIs available in the [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free to contribute to the Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
