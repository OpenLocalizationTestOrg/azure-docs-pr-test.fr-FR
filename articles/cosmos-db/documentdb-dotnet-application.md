---
title: "Didacticiel ASP.NET MVC pour Azure Cosmos DB : développement d’applications Web | Microsoft Docs"
description: "Une application web MVC à l’aide de la base de données Azure Cosmos de toocreate didacticiel ASP.NET MVC. Vous allez stocker JSON et accéder aux données à partir d’une application todo hébergée sur des sites web Azure - Didacticiel étape par étape ASP NET MVC."
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
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="79c5b-105"><a name="_Toc395809351"></a>Didacticiel ASP.NET MVC : développement d’applications web avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="79c5b-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79c5b-106">.NET</span><span class="sxs-lookup"><span data-stu-id="79c5b-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="79c5b-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="79c5b-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="79c5b-108">Java</span><span class="sxs-lookup"><span data-stu-id="79c5b-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="79c5b-109">Python</span><span class="sxs-lookup"><span data-stu-id="79c5b-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="79c5b-110">toohighlight comment vous pouvez efficacement tirer parti de base de données Azure Cosmos toostore et interroger des documents JSON, cet article fournit une procédure de bout en bout vous montrant comment toobuild une application de tâches à l’aide de la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="79c5b-110">toohighlight how you can efficiently leverage Azure Cosmos DB toostore and query JSON documents, this article provides an end-to-end walk-through showing you how toobuild a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="79c5b-111">tâches de Hello sont stockés sous forme de documents JSON dans la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="79c5b-111">hello tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Capture d’écran de liste de tâches hello application de web MVC créée par ce didacticiel - Didacticiel de ASP NET MVC étape par étape](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="79c5b-113">Cette procédure pas à pas vous montre comment toouse hello Azure Cosmos DB service toostore et accéder aux données à partir d’une application de web ASP.NET MVC hébergée sur Azure.</span><span class="sxs-lookup"><span data-stu-id="79c5b-113">This walk-through shows you how toouse hello Azure Cosmos DB service toostore and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="79c5b-114">Si vous recherchez un didacticiel qui porte uniquement sur la base de données Azure Cosmos, et pas hello composants d’ASP.NET MVC, consultez [générer une application de console Azure Cosmos DB c#](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="79c5b-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not hello ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="79c5b-115">Ce didacticiel suppose que vous disposez d'une expérience préalable de l'utilisation d'ASP.NET MVC et d'Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="79c5b-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="79c5b-116">Si vous êtes tooASP.NET nouveau ou hello [outils requis](#_Toc395637760), nous vous recommandons de télécharger le projet exemple complet de hello à partir de [GitHub] [ GitHub] et en suivant les instructions de hello dans Cet exemple.</span><span class="sxs-lookup"><span data-stu-id="79c5b-116">If you are new tooASP.NET or hello [prerequisite tools](#_Toc395637760), we recommend downloading hello complete sample project from [GitHub][GitHub] and following hello instructions in this sample.</span></span> <span data-ttu-id="79c5b-117">Une fois que vous avez créé, vous pouvez consulter ces informations toogain de l’article sur le code hello dans le contexte de hello du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-117">Once you have it built, you can review this article toogain insight on hello code in hello context of hello project.</span></span>
> 
> 

## <span data-ttu-id="79c5b-118"><a name="_Toc395637760"></a>Conditions préalables à l’exécution de ce didacticiel de base de données</span><span class="sxs-lookup"><span data-stu-id="79c5b-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="79c5b-119">Avant de suivre les instructions de hello dans cet article, vous devez vous assurer que vous disposez des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="79c5b-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="79c5b-120">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="79c5b-120">An active Azure account.</span></span> <span data-ttu-id="79c5b-121">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="79c5b-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="79c5b-122">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79c5b-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="79c5b-123">OU</span><span class="sxs-lookup"><span data-stu-id="79c5b-123">OR</span></span>

    <span data-ttu-id="79c5b-124">Une installation locale de hello [Azure Cosmos DB émulateur](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="79c5b-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="79c5b-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="79c5b-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="79c5b-126">Microsoft Azure SDK pour .NET de Visual Studio 2017, disponible via le programme d’installation de Visual Studio de hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through hello Visual Studio Installer.</span></span>

<span data-ttu-id="79c5b-127">Toutes les captures d’écran hello dans cet article ont été effectuées à l’aide de Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="79c5b-127">All hello screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="79c5b-128">Si votre système est configuré avec une version différente, il est possible que vos écrans et les options ne correspondront pas entièrement, mais si vous répondez à hello au-dessus de conditions préalables cette solution doit fonctionner.</span><span class="sxs-lookup"><span data-stu-id="79c5b-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet hello above prerequisites this solution should work.</span></span>

## <span data-ttu-id="79c5b-129"><a name="_Toc395637761"></a>Étape 1 : création d’un compte de base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="79c5b-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="79c5b-130">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79c5b-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="79c5b-131">Si vous déjà disposez d’un compte SQL (DocumentDB) pour la base de données Azure Cosmos ou si vous utilisez hello Azure Cosmos DB émulateur pour ce didacticiel, vous pouvez ignorer trop[créer une application ASP.NET MVC](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="79c5b-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="79c5b-132">Nous étudierons maintenant comment toocreate une application ASP.NET MVC à partir de hello sol à distance.</span><span class="sxs-lookup"><span data-stu-id="79c5b-132">We will now walk through how toocreate a new ASP.NET MVC application from hello ground-up.</span></span> 

## <span data-ttu-id="79c5b-133"><a name="_Toc395637762"></a>Étape 2 : création d'une application ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="79c5b-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="79c5b-134">Dans Visual Studio, sur hello **fichier** menu, pointez trop**nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-134">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span> <span data-ttu-id="79c5b-135">Hello **nouveau projet** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="79c5b-135">hello **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="79c5b-136">Bonjour **types de projet** volet, développez **modèles**, **Visual C#**, **Web**, puis sélectionnez **Application Web ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="79c5b-136">In hello **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Capture d’écran de boîte de dialogue Nouveau projet hello avec le type de projet d’Application Web ASP.NET hello mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="79c5b-138">Bonjour **nom** zone, entrez un nom hello du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-138">In hello **Name** box, type hello name of hello project.</span></span> <span data-ttu-id="79c5b-139">Ce didacticiel utilise le nom hello « todo ».</span><span class="sxs-lookup"><span data-stu-id="79c5b-139">This tutorial uses hello name "todo".</span></span> <span data-ttu-id="79c5b-140">Si vous choisissez autre chose qu’il toouse, partout où ce didacticiel s’adresse à propos de l’espace de noms hello todo, vous devez tooadjust hello fourni code exemples toouse tout ce que vous avez nommé votre application.</span><span class="sxs-lookup"><span data-stu-id="79c5b-140">If you choose toouse something other than this, then wherever this tutorial talks about hello todo namespace, you need tooadjust hello provided code samples toouse whatever you named your application.</span></span> 
4. <span data-ttu-id="79c5b-141">Cliquez sur **Parcourir** toonavigate toohello dossier où vous serez comme projet de hello toocreate, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-141">Click **Browse** toonavigate toohello folder where you would like toocreate hello project, and then click **OK**.</span></span>
   
      <span data-ttu-id="79c5b-142">Hello **nouvelle Application Web ASP.NET** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="79c5b-142">hello **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Capture d’écran de la boîte de dialogue nouvelle Application Web ASP.NET hello avec le modèle d’application MVC hello mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="79c5b-144">Dans le volet des modèles hello, sélectionnez **MVC**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-144">In hello templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="79c5b-145">Cliquez sur **OK** et permettent d’effectuer son travail autour de modèle ASP.NET MVC vide de la structure hello Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79c5b-145">Click **OK** and let Visual Studio do its thing around scaffolding hello empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="79c5b-146">Une fois que Visual Studio a terminé la création d’application de MVC hello réutilisable, vous avez une application ASP.NET vide que vous pouvez exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="79c5b-146">Once Visual Studio has finished creating hello boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="79c5b-147">Nous ignorons le projet de hello en cours d’exécution localement, car je suis sûr que nous avons hello vu tous les « Hello World » d’ASP.NET application.</span><span class="sxs-lookup"><span data-stu-id="79c5b-147">We'll skip running hello project locally because I'm sure we've all seen hello ASP.NET "Hello World" application.</span></span> <span data-ttu-id="79c5b-148">Attardons-nous droites tooadding base de données Azure Cosmos toothis projet et la création de notre application.</span><span class="sxs-lookup"><span data-stu-id="79c5b-148">Let's go straight tooadding Azure Cosmos DB toothis project and building our application.</span></span>

## <span data-ttu-id="79c5b-149"><a name="_Toc395637767"></a>Étape 3 : Ajouter le projet d’application web MVC Azure Cosmos DB tooyour</span><span class="sxs-lookup"><span data-stu-id="79c5b-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB tooyour MVC web application project</span></span>
<span data-ttu-id="79c5b-150">Maintenant que nous avons la plupart des mécanismes d’ASP.NET MVC hello dont nous avons besoin pour cette solution, nous allons obtenir toohello véritable but de ce didacticiel, l’ajout d’une application web de base de données Azure Cosmos tooour MVC.</span><span class="sxs-lookup"><span data-stu-id="79c5b-150">Now that we have most of hello ASP.NET MVC plumbing that we need for this solution, let's get toohello real purpose of this tutorial, adding Azure Cosmos DB tooour MVC web application.</span></span>

1. <span data-ttu-id="79c5b-151">Bonjour Azure Cosmos DB .NET SDK est packagée et distribuée comme package NuGet.</span><span class="sxs-lookup"><span data-stu-id="79c5b-151">hello Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="79c5b-152">tooget hello package NuGet dans Visual Studio, utilisez le Gestionnaire de package NuGet hello dans Visual Studio en cliquant sur le projet hello dans **l’Explorateur de solutions** , puis en cliquant sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-152">tooget hello NuGet package in Visual Studio, use hello NuGet package manager in Visual Studio by right-clicking on hello project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Capture d’écran de hello cliquez sur options pour le projet d’application web hello dans l’Explorateur de solutions, gérer les Packages NuGet mis en surbrillance.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="79c5b-154">Hello **gérer les Packages NuGet** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="79c5b-154">hello **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="79c5b-155">Bonjour NuGet **Parcourir** , tapez ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-155">In hello NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="79c5b-156">(nom du package hello n’a été mis à jour tooAzure Cosmos DB.)</span><span class="sxs-lookup"><span data-stu-id="79c5b-156">(hello package name has not been updated tooAzure Cosmos DB.)</span></span>
   
    <span data-ttu-id="79c5b-157">À partir des résultats de hello, installez hello **Microsoft.Azure.DocumentDB par Microsoft** package.</span><span class="sxs-lookup"><span data-stu-id="79c5b-157">From hello results, install hello **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="79c5b-158">Il télécharge et installe le package de base de données Azure Cosmos hello, ainsi que toutes les dépendances, telles que Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="79c5b-158">This will download and install hello Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="79c5b-159">Cliquez sur **OK** Bonjour **aperçu** fenêtre, et **J’accepte** Bonjour **acceptation de licence** fenêtre toocomplete hello installation.</span><span class="sxs-lookup"><span data-stu-id="79c5b-159">Click **OK** in hello **Preview** window, and **I Accept** in hello **License Acceptance** window toocomplete hello install.</span></span>
   
    ![Capture de l ' écran de la fenêtre Gérer les Packages NuGet hello, avec hello bibliothèque cliente Microsoft Azure DocumentDB mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="79c5b-161">Vous pouvez également utiliser hello package de Console du Gestionnaire de Package tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-161">Alternatively you can use hello Package Manager Console tooinstall hello package.</span></span> <span data-ttu-id="79c5b-162">toodo sur hello **outils** menu, cliquez sur **Gestionnaire de Package NuGet**, puis cliquez sur **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-162">toodo so, on hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="79c5b-163">À l’invite de hello, tapez hello qui suit.</span><span class="sxs-lookup"><span data-stu-id="79c5b-163">At hello prompt, type hello following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="79c5b-164">Une fois le package de hello est installé, votre solution Visual Studio doit ressembler à suivant hello avec deux nouvelles références ajoutées, Microsoft.Azure.Documents.Client et Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="79c5b-164">Once hello package is installed, your Visual Studio solution should resemble hello following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Capture de l ' écran de deux références de hello ajouté toohello projet des données JSON dans l’Explorateur de solutions](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="79c5b-166"><a name="_Toc395637763"></a>Étape 4 : Configurer hello application ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="79c5b-166"><a name="_Toc395637763"></a>Step 4: Set up hello ASP.NET MVC application</span></span>
<span data-ttu-id="79c5b-167">Maintenant nous allons ajouter application de MVC toothis modèles, vues et contrôleurs des hello :</span><span class="sxs-lookup"><span data-stu-id="79c5b-167">Now let's add hello models, views, and controllers toothis MVC application:</span></span>

* <span data-ttu-id="79c5b-168">[Ajout d'un modèle](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="79c5b-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="79c5b-169">[Ajout d'un contrôleur](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="79c5b-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="79c5b-170">[Ajout de vues](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="79c5b-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="79c5b-171"><a name="_Toc395637764"></a>Ajout d’un modèle de données JSON</span><span class="sxs-lookup"><span data-stu-id="79c5b-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="79c5b-172">Commençons par créer hello **M** dans MVC, hello modèle.</span><span class="sxs-lookup"><span data-stu-id="79c5b-172">Let's begin by creating hello **M** in MVC, hello model.</span></span> 

1. <span data-ttu-id="79c5b-173">Dans **l’Explorateur de solutions**, avec le bouton hello **modèles** dossier, cliquez sur **ajouter**, puis cliquez sur **classe**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-173">In **Solution Explorer**, right-click hello **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="79c5b-174">Hello **ajouter un nouvel élément** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="79c5b-174">hello **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="79c5b-175">Nommez votre nouvelle classe **Item.cs**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="79c5b-176">Dans cette nouvelle **Item.cs** , ajoutez suivant hello après hello dernière *à l’aide d’instruction*.</span><span class="sxs-lookup"><span data-stu-id="79c5b-176">In this new **Item.cs** file, add hello following after hello last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="79c5b-177">Remplacez maintenant ce code</span><span class="sxs-lookup"><span data-stu-id="79c5b-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="79c5b-178">avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="79c5b-178">with hello following code.</span></span>
   
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
   
    <span data-ttu-id="79c5b-179">Toutes les données dans la base de données Azure Cosmos est transmise sur le câble de hello et stockés au format JSON.</span><span class="sxs-lookup"><span data-stu-id="79c5b-179">All data in Azure Cosmos DB is passed over hello wire and stored as JSON.</span></span> <span data-ttu-id="79c5b-180">moyen de hello toocontrol vos objets sont sérialisés/désérialisé par JSON.NET, vous pouvez utiliser hello **JsonProperty** attribut comme Bonjour **élément** classe que nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="79c5b-180">toocontrol hello way your objects are serialized/deserialized by JSON.NET you can use hello **JsonProperty** attribute as demonstrated in hello **Item** class we just created.</span></span> <span data-ttu-id="79c5b-181">Vous n’avez pas **ont** toodo cela mais souhaitez tooensure que mes propriétés suivent camelCase JSON hello conventions d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="79c5b-181">You don't **have** toodo this but I want tooensure that my properties follow hello JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="79c5b-182">Non seulement pourrez vous contrôler hello format du nom de la propriété hello lorsqu’il passe en JSON, mais vous pouvez entièrement renommer vos propriétés .NET comme je l’ai fait avec hello **Description** propriété.</span><span class="sxs-lookup"><span data-stu-id="79c5b-182">Not only can you control hello format of hello property name when it goes into JSON, but you can entirely rename your .NET properties like I did with hello **Description** property.</span></span> 

### <span data-ttu-id="79c5b-183"><a name="_Toc395637765"></a>Ajout d'un contrôleur</span><span class="sxs-lookup"><span data-stu-id="79c5b-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="79c5b-184">Qui prend en charge hello **M**, maintenant nous allons créer hello **C** dans MVC, une classe de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="79c5b-184">That takes care of hello **M**, now let's create hello **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="79c5b-185">Dans **l’Explorateur de solutions**, avec le bouton hello **contrôleurs** dossier, cliquez sur **ajouter**, puis cliquez sur **contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-185">In **Solution Explorer**, right-click hello **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="79c5b-186">Hello **ajouter une vue de structure** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="79c5b-186">hello **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="79c5b-187">Sélectionnez **Classe de contrôleur MVC 5 - Vide** puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Capture d’écran de la boîte de dialogue Ajouter une vue de structure hello hello contrôleur MVC 5 - option vide mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="79c5b-189">Nommez votre contrôleur **ItemController**</span><span class="sxs-lookup"><span data-stu-id="79c5b-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Capture d’écran de la boîte de dialogue Ajouter un contrôleur hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="79c5b-191">Une fois que le fichier de hello est créé, votre solution Visual Studio doit se présenter comme suit de hello avec le nouveau fichier de ItemController.cs hello dans **l’Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-191">Once hello file is created, your Visual Studio solution should resemble hello following with hello new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="79c5b-192">nouveau fichier Item.cs Hello, créé précédemment est également affiché.</span><span class="sxs-lookup"><span data-stu-id="79c5b-192">hello new Item.cs file created earlier is also shown.</span></span>
   
    ![Capture d’écran de hello solution Visual Studio - Explorateur de solutions avec le nouveau fichier de ItemController.cs hello et fichier Item.cs mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="79c5b-194">Vous pouvez fermer ItemController.cs, nous y reviendrons tooit plus tard.</span><span class="sxs-lookup"><span data-stu-id="79c5b-194">You can close ItemController.cs, we'll come back tooit later.</span></span> 

### <span data-ttu-id="79c5b-195"><a name="_Toc395637766"></a>Ajout de vues</span><span class="sxs-lookup"><span data-stu-id="79c5b-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="79c5b-196">Maintenant, nous allons créer hello **V** dans MVC, hello vues :</span><span class="sxs-lookup"><span data-stu-id="79c5b-196">Now, let's create hello **V** in MVC, hello views:</span></span>

* <span data-ttu-id="79c5b-197">[Ajout d'une vue Index de l'élément](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="79c5b-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="79c5b-198">[Ajout d'une vue Nouvel élément](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="79c5b-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="79c5b-199">[Ajout d'une vue Modifier l'élément](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="79c5b-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="79c5b-200"><a name="AddItemIndexView"></a>Ajout d'une vue Index de l'élément</span><span class="sxs-lookup"><span data-stu-id="79c5b-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="79c5b-201">Dans **l’Explorateur de solutions**, développez hello **vues** dossier, hello avec le bouton vide **élément** dossier créé par Visual Studio pour vous lorsque vous avez ajouté hello  **ItemController** précédemment, cliquez sur **ajouter**, puis cliquez sur **vue**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-201">In **Solution Explorer**, expand hello **Views**  folder, right-click hello empty **Item** folder that Visual Studio created for you when you added hello **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Capture d’écran de l’Explorateur de solutions affichant le dossier d’éléments de hello créé par Visual Studio avec des commandes d’ajouter une vue hello mis en surbrillance](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="79c5b-203">Bonjour **ajouter une vue** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="79c5b-203">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="79c5b-204">Bonjour **nom de la vue** , tapez ***Index***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-204">In hello **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="79c5b-205">Bonjour **modèle** boîte, sélectionnez ***liste***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-205">In hello **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="79c5b-206">Bonjour **classe de modèle** boîte, sélectionnez ***élément (todo. Modèles)***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-206">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="79c5b-207">Dans la zone de page de disposition hello, tapez ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-207">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Boîte de dialogue Ajouter une vue de capture d’écran montrant hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="79c5b-209">Une fois que vous avez défini toutes ces valeurs, cliquez sur **Ajouter** et laissez Visual Studio créer une vue de modèle.</span><span class="sxs-lookup"><span data-stu-id="79c5b-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="79c5b-210">Une fois ceci effectué, il ouvre le fichier cshtml hello qui a été créé.</span><span class="sxs-lookup"><span data-stu-id="79c5b-210">Once it is done, it will open hello cshtml file  that was created.</span></span> <span data-ttu-id="79c5b-211">Nous pouvons fermer ce fichier dans Visual Studio comme nous reviendra tooit plus tard.</span><span class="sxs-lookup"><span data-stu-id="79c5b-211">We can close that file in Visual Studio as we will come back tooit later.</span></span>

#### <span data-ttu-id="79c5b-212"><a name="AddNewIndexView"></a>Ajout d'une vue Nouvel élément</span><span class="sxs-lookup"><span data-stu-id="79c5b-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="79c5b-213">Toohow semblables, nous avons créé un **Index de l’élément** affichage, nous allons maintenant créer une nouvelle vue pour la création de nouveaux **éléments**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-213">Similar toohow we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="79c5b-214">Dans **l’Explorateur de solutions**, avec le bouton hello **élément** dossier, cliquez sur **ajouter**, puis cliquez sur **vue**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-214">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="79c5b-215">Bonjour **ajouter une vue** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="79c5b-215">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="79c5b-216">Bonjour **nom de la vue** , tapez ***créer***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-216">In hello **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="79c5b-217">Bonjour **modèle** boîte, sélectionnez ***créer***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-217">In hello **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="79c5b-218">Bonjour **classe de modèle** boîte, sélectionnez ***élément (todo. Modèles)***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-218">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="79c5b-219">Dans la zone de page de disposition hello, tapez ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-219">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="79c5b-220">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="79c5b-221"><a name="_Toc395888515"></a>Ajout d'une vue Modifier l'élément</span><span class="sxs-lookup"><span data-stu-id="79c5b-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="79c5b-222">Enfin, ajoutez une dernière vue pour modifier un **élément** Bonjour même façon qu’avant.</span><span class="sxs-lookup"><span data-stu-id="79c5b-222">And finally, add one last view for editing an **Item** in hello same way as before.</span></span>

1. <span data-ttu-id="79c5b-223">Dans **l’Explorateur de solutions**, avec le bouton hello **élément** dossier, cliquez sur **ajouter**, puis cliquez sur **vue**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-223">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="79c5b-224">Bonjour **ajouter une vue** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="79c5b-224">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="79c5b-225">Bonjour **nom de la vue** , tapez ***modifier***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-225">In hello **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="79c5b-226">Bonjour **modèle** boîte, sélectionnez ***modifier***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-226">In hello **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="79c5b-227">Bonjour **classe de modèle** boîte, sélectionnez ***élément (todo. Modèles)***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-227">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="79c5b-228">Dans la zone de page de disposition hello, tapez ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="79c5b-228">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="79c5b-229">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-229">Click **Add**.</span></span>

<span data-ttu-id="79c5b-230">Une fois cette opération est effectuée, fermez tous les documents de cshtml de hello dans Visual Studio comme nous retourneront les vues toothese plus tard.</span><span class="sxs-lookup"><span data-stu-id="79c5b-230">Once this is done, close all hello cshtml documents in Visual Studio as we will return toothese views later.</span></span>

## <span data-ttu-id="79c5b-231"><a name="_Toc395637769"></a>Étape 5 : liaison d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="79c5b-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="79c5b-232">Maintenant que les sélections MVC standard hello sont pris en charge, nous allons activer le code de hello tooadding pour la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="79c5b-232">Now that hello standard MVC stuff is taken care of, let's turn tooadding hello code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="79c5b-233">Dans cette section, nous allons ajouter suivante de code toohandle hello :</span><span class="sxs-lookup"><span data-stu-id="79c5b-233">In this section, we'll add code toohandle hello following:</span></span>

* <span data-ttu-id="79c5b-234">[Recensement des éléments non terminés.](#_Toc395637770)</span><span class="sxs-lookup"><span data-stu-id="79c5b-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="79c5b-235">[Ajout d'éléments](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="79c5b-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="79c5b-236">[Modification d'éléments](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="79c5b-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="79c5b-237"><a name="_Toc395637770"></a>Établissement de la liste des éléments incomplets dans votre application web MVC</span><span class="sxs-lookup"><span data-stu-id="79c5b-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="79c5b-238">Hello premier toodo chose ici est d’ajouter une classe qui contient tous les hello logique tooconnect tooand utiliser Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="79c5b-238">hello first thing toodo here is add a class that contains all hello logic tooconnect tooand use Azure Cosmos DB.</span></span> <span data-ttu-id="79c5b-239">Pour ce didacticiel nous allons encapsulent toute cette logique dans la classe de référentiel tooa appelé DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="79c5b-239">For this tutorial we'll encapsulate all this logic in tooa repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="79c5b-240">Dans **l’Explorateur de solutions**, avec le bouton droit sur le projet de hello, cliquez sur **ajouter**, puis cliquez sur **classe**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-240">In **Solution Explorer**, right-click on hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="79c5b-241">Nommez la nouvelle classe de hello **DocumentDBRepository** et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-241">Name hello new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="79c5b-242">Bonjour nouvellement créé **DocumentDBRepository** et ajouter des éléments suivants de hello *à l’aide d’instructions* ci-dessus hello *espace de noms* déclaration</span><span class="sxs-lookup"><span data-stu-id="79c5b-242">In hello newly created **DocumentDBRepository** class and add hello following *using statements* above hello *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="79c5b-243">Remplacez maintenant ce code</span><span class="sxs-lookup"><span data-stu-id="79c5b-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="79c5b-244">avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="79c5b-244">with hello following code.</span></span>
   
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
   
    
3. <span data-ttu-id="79c5b-245">Nous mettons lors de la lecture des valeurs de configuration, ouvrez hello **Web.config** fichier de votre application et ajoutez hello lignes sous hello suivantes `<AppSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="79c5b-245">We're reading some values from configuration, so open hello **Web.config** file of your application and add hello following lines under hello `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="79c5b-246">À présent, mettez à jour de valeurs hello *point de terminaison* et *authKey* à l’aide du Panneau de clés hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="79c5b-246">Now, update hello values for *endpoint* and *authKey* using hello Keys blade of hello Azure Portal.</span></span> <span data-ttu-id="79c5b-247">Utilisez hello **URI** à partir du Panneau de clés hello en tant que valeur hello du paramètre de point de terminaison hello et utilisez hello **clé primaire**, ou **clé secondaire** à partir du Panneau de clés hello en tant que valeur hello Hello paramètre d’authKey.</span><span class="sxs-lookup"><span data-stu-id="79c5b-247">Use hello **URI** from hello Keys blade as hello value of hello endpoint setting, and use hello **PRIMARY KEY**, or **SECONDARY KEY** from hello Keys blade as hello value of hello authKey setting.</span></span>

    <span data-ttu-id="79c5b-248">Que se charge de mettre en place des référentiels de base de données Azure Cosmos hello, maintenant nous allons ajouter notre logique d’application.</span><span class="sxs-lookup"><span data-stu-id="79c5b-248">That takes care of wiring up hello Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="79c5b-249">Hello première chose que nous souhaitons toodo en mesure de toobe avec une application de liste todo est toodisplay des éléments incomplets hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-249">hello first thing we want toobe able toodo with a todo list application is toodisplay hello incomplete items.</span></span>  <span data-ttu-id="79c5b-250">Copiez et collez hello suivant extrait de code n’importe où dans hello **DocumentDBRepository** classe.</span><span class="sxs-lookup"><span data-stu-id="79c5b-250">Copy and paste hello following code snippet anywhere within hello **DocumentDBRepository** class.</span></span>
   
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
2. <span data-ttu-id="79c5b-251">Ouvrez hello **ItemController** nous avons ajouté précédemment et ajoutez hello suivant *à l’aide d’instructions* au-dessus de déclaration d’espace de noms hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-251">Open hello **ItemController** we added earlier and add hello following *using statements* above hello namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="79c5b-252">Si votre projet n’est pas nommé « todo », vous devez tooupdate à l’aide de « todo. Modèles » ; nom de hello tooreflect de votre projet.</span><span class="sxs-lookup"><span data-stu-id="79c5b-252">If your project is not named "todo", then you need tooupdate using "todo.Models"; tooreflect hello name of your project.</span></span>
   
    <span data-ttu-id="79c5b-253">Remplacez maintenant ce code</span><span class="sxs-lookup"><span data-stu-id="79c5b-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="79c5b-254">avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="79c5b-254">with hello following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="79c5b-255">Ouvrez **Global.asax.cs** et ajoutez hello suivant ligne toohello **Application_Start** (méthode)</span><span class="sxs-lookup"><span data-stu-id="79c5b-255">Open **Global.asax.cs** and add hello following line toohello **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="79c5b-256">À ce stade, votre solution doit être en mesure de toobuild sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="79c5b-256">At this point your solution should be able toobuild without any errors.</span></span>

<span data-ttu-id="79c5b-257">Si vous avez exécuté application hello maintenant, vous indiquerez toohello **HomeController** et hello **Index** vue de ce contrôleur.</span><span class="sxs-lookup"><span data-stu-id="79c5b-257">If you ran hello application now, you would go toohello **HomeController** and hello **Index** view of that controller.</span></span> <span data-ttu-id="79c5b-258">Il s’agit par défaut hello pour le projet de modèle MVC hello que nous avons choisi au démarrage de hello, mais nous ne voulons pas qui !</span><span class="sxs-lookup"><span data-stu-id="79c5b-258">This is hello default behavior for hello MVC template project we chose at hello start but we don't want that!</span></span> <span data-ttu-id="79c5b-259">Nous allons modifier hello routage sur cette tooalter d’application MVC ce comportement.</span><span class="sxs-lookup"><span data-stu-id="79c5b-259">Let's change hello routing on this MVC application tooalter this behavior.</span></span>

<span data-ttu-id="79c5b-260">Ouvrez ***application\_Start\RouteConfig.cs*** et recherchez la ligne hello commençant par « valeurs par défaut : » et modifiez-le hello tooresemble suivant.</span><span class="sxs-lookup"><span data-stu-id="79c5b-260">Open ***App\_Start\RouteConfig.cs*** and locate hello line starting with "defaults:" and change it tooresemble hello following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="79c5b-261">Cela maintenant indique à ASP.NET MVC que si vous n’avez pas spécifié une valeur dans hello URL toocontrol hello le comportement de routage que, au lieu de **accueil**, utilisez **élément** en tant que contrôleur de hello et utilisateur **Index** comme vue de hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-261">This now tells ASP.NET MVC that if you have not specified a value in hello URL toocontrol hello routing behavior that instead of **Home**, use **Item** as hello controller and user **Index** as hello view.</span></span>

<span data-ttu-id="79c5b-262">À présent si vous exécutez application hello, il appelle votre **ItemController** qui appeler dans la classe de référentiel toohello et utiliser hello GetItems méthode tooreturn tous les toohello d’éléments incomplet hello **vues** \\ **Élément**\\**Index** vue.</span><span class="sxs-lookup"><span data-stu-id="79c5b-262">Now if you run hello application, it will call into your **ItemController** which will call in toohello repository class and use hello GetItems method tooreturn all hello incomplete items toohello **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="79c5b-263">Si vous créez et exécutez ce projet maintenant, vous devriez voir ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="79c5b-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Capture d’écran de l’application web hello todo liste sont créée par ce didacticiel de base de données](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="79c5b-265"><a name="_Toc395637771"></a>Ajout d'éléments</span><span class="sxs-lookup"><span data-stu-id="79c5b-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="79c5b-266">Nous allons insérer des éléments dans notre base de données afin que nous quelque chose de plus qu’un toolook de grille vide à.</span><span class="sxs-lookup"><span data-stu-id="79c5b-266">Let's put some items into our database so we have something more than an empty grid toolook at.</span></span>

<span data-ttu-id="79c5b-267">Vous allez ajouter du code trop Azure Cosmos DBRepository ItemController toopersist hello enregistrement de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="79c5b-267">Let's add some code too Azure Cosmos DBRepository and ItemController toopersist hello record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="79c5b-268">Ajouter hello suivant de méthode tooyour **DocumentDBRepository** classe.</span><span class="sxs-lookup"><span data-stu-id="79c5b-268">Add hello following method tooyour **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="79c5b-269">Cette méthode prend un objet passé tooit simplement et l’enregistre dans la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="79c5b-269">This method simply takes an object passed tooit and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="79c5b-270">Ouvrir le fichier de ItemController.cs hello et ajouter hello suivant extrait de code au sein de la classe hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-270">Open hello ItemController.cs file and add hello following code snippet within hello class.</span></span> <span data-ttu-id="79c5b-271">Voici comment ASP.NET MVC sait quel toodo pour hello **créer** action.</span><span class="sxs-lookup"><span data-stu-id="79c5b-271">This is how ASP.NET MVC knows what toodo for hello **Create** action.</span></span> <span data-ttu-id="79c5b-272">Dans ce cas rendu simplement hello associés vue Create.cshtml créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="79c5b-272">In this case just render hello associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="79c5b-273">Nous devons maintenant du code plus dans ce contrôleur qui acceptera soumission hello de hello **créer** vue.</span><span class="sxs-lookup"><span data-stu-id="79c5b-273">We now need some more code in this controller that will accept hello submission from hello **Create** view.</span></span>
3. <span data-ttu-id="79c5b-274">Ajoutez hello bloc suivant de code toohello classe ItemController.cs qui indique à ASP.NET MVC quel toodo avec une publication de formulaire pour ce contrôleur.</span><span class="sxs-lookup"><span data-stu-id="79c5b-274">Add hello next block of code toohello ItemController.cs class that tells ASP.NET MVC what toodo with a form POST for this controller.</span></span>
   
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
   
    <span data-ttu-id="79c5b-275">Ce code appelle dans toohello DocumentDBRepository et utilise hello CreateItemAsync méthode toopersist hello todo élément toohello base de données.</span><span class="sxs-lookup"><span data-stu-id="79c5b-275">This code calls in toohello DocumentDBRepository and uses hello CreateItemAsync method toopersist hello new todo item toohello database.</span></span> 
   
    <span data-ttu-id="79c5b-276">**Note de sécurité**: hello **ValidateAntiForgeryToken** attribut est utilisé ici toohelp protéger cette application contre les attaques de falsification de requête.</span><span class="sxs-lookup"><span data-stu-id="79c5b-276">**Security Note**: hello **ValidateAntiForgeryToken** attribute is used here toohelp protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="79c5b-277">Il est tooit plus que simplement en ajoutant cet attribut, vos vues doivent toowork par ce jeton anti-contrefaçon ainsi.</span><span class="sxs-lookup"><span data-stu-id="79c5b-277">There is more tooit than just adding this attribute, your views need toowork with this anti-forgery token as well.</span></span> <span data-ttu-id="79c5b-278">Pour plus d’informations sur le sujet de hello et des exemples de procédure tooimplement cela correctement, consultez [empêcher Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="79c5b-278">For more on hello subject, and examples of how tooimplement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="79c5b-279">Hello de code source fourni sur [GitHub] [ GitHub] comporte une implémentation complète de hello en place.</span><span class="sxs-lookup"><span data-stu-id="79c5b-279">hello source code provided on [GitHub][GitHub] has hello full implementation in place.</span></span>
   
    <span data-ttu-id="79c5b-280">**Note de sécurité**: nous utilisons également hello **lier** attribut sur toohelp de paramètre de méthode hello protéger contre les attaques de validation excessive.</span><span class="sxs-lookup"><span data-stu-id="79c5b-280">**Security Note**: We also use hello **Bind** attribute on hello method parameter toohelp protect against over-posting attacks.</span></span> <span data-ttu-id="79c5b-281">Pour plus d’informations, consultez la rubrique [Opérations CRUD de base dans ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="79c5b-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="79c5b-282">Ceci conclut hello code nécessaire tooadd éléments tooour base de données.</span><span class="sxs-lookup"><span data-stu-id="79c5b-282">This concludes hello code required tooadd new Items tooour database.</span></span>

### <span data-ttu-id="79c5b-283"><a name="_Toc395637772"></a>Modification d'éléments</span><span class="sxs-lookup"><span data-stu-id="79c5b-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="79c5b-284">Il existe une dernière chose pour nous toodo, et qui est tooadd hello capacité tooedit **éléments** dans la base de données hello et toomark en tant que terminer.</span><span class="sxs-lookup"><span data-stu-id="79c5b-284">There is one last thing for us toodo, and that is tooadd hello ability tooedit **Items** in hello database and toomark them as complete.</span></span> <span data-ttu-id="79c5b-285">Hello vue pour la modification a déjà été ajoutée toohello projet, donc vous devez simplement tooadd certains de code tooour contrôleur toohello **DocumentDBRepository** classe à nouveau.</span><span class="sxs-lookup"><span data-stu-id="79c5b-285">hello view for editing was already added toohello project, so we just need tooadd some code tooour controller and toohello **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="79c5b-286">Ajouter hello suivant toohello **DocumentDBRepository** classe.</span><span class="sxs-lookup"><span data-stu-id="79c5b-286">Add hello following toohello **DocumentDBRepository** class.</span></span>
   
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
   
    <span data-ttu-id="79c5b-287">Hello première de ces méthodes, **GetItem** extrait un élément à partir de la base de données Azure Cosmos passée arrière toohello **ItemController** et ensuite sur toohello **modifier** vue.</span><span class="sxs-lookup"><span data-stu-id="79c5b-287">hello first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back toohello **ItemController** and then on toohello **Edit** view.</span></span>
   
    <span data-ttu-id="79c5b-288">Hello seconde des méthodes de hello nous venons d’ajouter remplace hello **Document** dans la base de données Azure Cosmos avec version hello Hello **Document** transmis depuis hello **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-288">hello second of hello methods we just added replaces hello **Document** in Azure Cosmos DB with hello version of hello **Document** passed in from hello **ItemController**.</span></span>
2. <span data-ttu-id="79c5b-289">Ajouter hello suivant toohello **ItemController** classe.</span><span class="sxs-lookup"><span data-stu-id="79c5b-289">Add hello following toohello **ItemController** class.</span></span>
   
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
   
    <span data-ttu-id="79c5b-290">Hello première méthode gère hello Http GET qui se produit lorsque hello utilisateur clique sur hello **modifier** lien à partir de hello **Index** vue.</span><span class="sxs-lookup"><span data-stu-id="79c5b-290">hello first method handles hello Http GET that happens when hello user clicks on hello **Edit** link from hello **Index** view.</span></span> <span data-ttu-id="79c5b-291">Cette méthode extrait un [ **Document** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) à partir de la base de données Azure Cosmos et lui passe toohello **modifier** vue.</span><span class="sxs-lookup"><span data-stu-id="79c5b-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it toohello **Edit** view.</span></span>
   
    <span data-ttu-id="79c5b-292">Hello **modifier** vue effectuez un toohello Http POST **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-292">hello **Edit** view will then do an Http POST toohello **IndexController**.</span></span> 
   
    <span data-ttu-id="79c5b-293">Hello seconde méthode nous avons ajouté des handles en passant hello mis à jour objet tooAzure Cosmos DB toobe rendues persistantes dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-293">hello second method we added handles passing hello updated object tooAzure Cosmos DB toobe persisted in hello database.</span></span>

<span data-ttu-id="79c5b-294">C’est tout, ce qui est tout ce dont nous avons besoin toorun notre application, la liste incomplète **éléments**, ajouter de nouveaux **éléments**et modifier **éléments**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-294">That's it, that is everything we need toorun our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="79c5b-295"><a name="_Toc395637773"></a>Étape 6 : Exécuter localement l’application hello</span><span class="sxs-lookup"><span data-stu-id="79c5b-295"><a name="_Toc395637773"></a>Step 6: Run hello application locally</span></span>
<span data-ttu-id="79c5b-296">application de hello tootest sur votre ordinateur local, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="79c5b-296">tootest hello application on your local machine, do hello following:</span></span>

1. <span data-ttu-id="79c5b-297">Dans l’application de hello toobuild Visual Studio en mode débogage, appuyez sur F5.</span><span class="sxs-lookup"><span data-stu-id="79c5b-297">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span> <span data-ttu-id="79c5b-298">Il doit générer l’application hello et lancer un navigateur avec la page de grille vide hello que nous avons vu avant :</span><span class="sxs-lookup"><span data-stu-id="79c5b-298">It should build hello application and launch a browser with hello empty grid page we saw before:</span></span>
   
    ![Capture d’écran de l’application web hello todo liste sont créée par ce didacticiel de base de données](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="79c5b-300">Cliquez sur hello **créer un nouveau** lier et ajouter des valeurs toohello **nom** et **Description** champs.</span><span class="sxs-lookup"><span data-stu-id="79c5b-300">Click hello **Create New** link and add values toohello **Name** and **Description** fields.</span></span> <span data-ttu-id="79c5b-301">Laissez hello **terminé** case à cocher désactivée sinon hello nouvelle **élément** sera ajoutée dans un état terminé et n’apparaissent pas dans la liste initiale de hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-301">Leave hello **Completed** check box unselected otherwise hello new **Item** will be added in a completed state and will not appear on hello initial list.</span></span>
   
    ![Capture d’écran de hello créer une vue](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="79c5b-303">Cliquez sur **créer** et que vous êtes redirigé toohello arrière **Index** vue et votre **élément** s’affiche dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-303">Click **Create** and you are redirected back toohello **Index** view and your **Item** appears in hello list.</span></span>
   
    ![Capture d’écran de hello vue d’Index](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="79c5b-305">Pensez tooadd libre plus quelques **éléments** tooyour liste des tâches.</span><span class="sxs-lookup"><span data-stu-id="79c5b-305">Feel free tooadd a few more **Items** tooyour todo list.</span></span>
    
4. <span data-ttu-id="79c5b-306">Cliquez sur **modifier** tooan suivant **élément** proviennent de la liste de hello et que vous toohello **modifier** vue dans laquelle vous pouvez mettre à jour n’importe quelle propriété de votre objet, y compris hello  **Terminé** indicateur.</span><span class="sxs-lookup"><span data-stu-id="79c5b-306">Click **Edit** next tooan **Item** on hello list and you are taken toohello **Edit** view where you can update any property of your object, including hello **Completed** flag.</span></span> <span data-ttu-id="79c5b-307">Si vous marquez hello **Complete** indicateur et cliquez sur **enregistrer**, hello **élément** est supprimé de la liste de hello des tâches incomplètes.</span><span class="sxs-lookup"><span data-stu-id="79c5b-307">If you mark hello **Complete** flag and click **Save**, hello **Item** is removed from hello list of incomplete tasks.</span></span>
   
    ![Capture d’écran de hello vue Index avec case hello terminé à](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="79c5b-309">Une fois que vous avez testé l’application hello, appuyez sur toostop Ctrl + F5 débogage application hello.</span><span class="sxs-lookup"><span data-stu-id="79c5b-309">Once you've tested hello app, press Ctrl+F5 toostop debugging hello app.</span></span> <span data-ttu-id="79c5b-310">Vous êtes prêt toodeploy !</span><span class="sxs-lookup"><span data-stu-id="79c5b-310">You're ready toodeploy!</span></span>

## <span data-ttu-id="79c5b-311"><a name="_Toc395637774"></a>Étape 7 : Déployer hello application tooAzure du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="79c5b-311"><a name="_Toc395637774"></a>Step 7: Deploy hello application tooAzure App Service</span></span> 
<span data-ttu-id="79c5b-312">Maintenant que vous avez application complète hello fonctionne correctement avec la base de données Azure Cosmos nous allons toodeploy cette tooAzure d’application web du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="79c5b-312">Now that you have hello complete application working correctly with Azure Cosmos DB we're going toodeploy this web app tooAzure App Service.</span></span>  

1. <span data-ttu-id="79c5b-313">est de cette application tous les, vous devez toodo toopublish avec le bouton droit sur le projet hello dans **l’Explorateur de solutions** et cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-313">toopublish this application all you need toodo is right-click on hello project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Capture d’écran de hello option Publier dans l’Explorateur de solutions](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="79c5b-315">Bonjour **publier** boîte de dialogue, cliquez sur **Microsoft Azure App Service**, puis sélectionnez **créer un nouveau** toocreate un Service d’application de profil, ou cliquez sur **sélectionner Existant** toouse un profil existant.</span><span class="sxs-lookup"><span data-stu-id="79c5b-315">In hello **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** toocreate an App Service profile, or click **Select Existing** toouse an existing profile.</span></span>

    ![Publier une boîte de dialogue dans Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="79c5b-317">Si vous possédez un profil Azure App Service existant, entrez votre nom d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="79c5b-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="79c5b-318">Hello d’utilisation **vue** filtrer toosort par type de ressource ou le groupe de ressources, puis sélectionnez votre Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="79c5b-318">Use hello **View** filter toosort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Boîte de dialogue App Service dans Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="79c5b-320">toocreate un nouveau profil de Service d’applications Azure, cliquez sur **créer un nouveau** Bonjour **publier** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="79c5b-320">toocreate a new Azure App Service profile, click **Create New** in hello **Publish** dialog box.</span></span> <span data-ttu-id="79c5b-321">Bonjour **créer un Service application** boîte de dialogue, entrez votre nom de l’application Web et un abonnement approprié, un groupe de ressources et un plan App Service, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="79c5b-321">In hello **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Créer une boîte de dialogue App Service dans Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="79c5b-323">Dans quelques secondes, Visual Studio achèvera la publication de votre application web et lancera un navigateur dans lequel vous pourrez voir votre réalisation exécutée dans Azure !</span><span class="sxs-lookup"><span data-stu-id="79c5b-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="79c5b-324"><a name="_Toc395637775"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79c5b-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="79c5b-325">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="79c5b-325">Congratulations!</span></span> <span data-ttu-id="79c5b-326">Vous venez de créé votre premier ASP.NET MVC application web à l’aide de la base de données Azure Cosmos et publié tooAzure.</span><span class="sxs-lookup"><span data-stu-id="79c5b-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it tooAzure.</span></span> <span data-ttu-id="79c5b-327">Hello de code source pour l’application hello complète, y compris les détails de hello et supprimer des fonctionnalités qui n’étaient pas incluses dans ce didacticiel peut être téléchargé ou cloné à partir de [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="79c5b-327">hello source code for hello complete application, including hello detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="79c5b-328">Par conséquent, si vous souhaitez ajouter à cette application tooyour, saisissez le code de hello et l’ajouter toothis application.</span><span class="sxs-lookup"><span data-stu-id="79c5b-328">So if you're interested in adding that tooyour app, grab hello code and add it toothis app.</span></span>

<span data-ttu-id="79c5b-329">application de tooyour tooadd des fonctionnalités supplémentaires, consultez hello API disponibles dans hello [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) apparence toocontribute libre toohello Azure Cosmos DB .NET Library sur [GitHub] [GitHub].</span><span class="sxs-lookup"><span data-stu-id="79c5b-329">tooadd additional functionality tooyour application, review hello APIs available in hello [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free toocontribute toohello Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
