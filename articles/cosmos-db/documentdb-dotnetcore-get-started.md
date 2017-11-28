---
title: "Azure Cosmos DB : Didacticiel sur la prise en main de l’API DocumentDB avec .NET Core | Microsoft Docs"
description: "Un didacticiel qui crée une application de base de données en ligne et de console C# à l’aide du kit de développement logiciel (SDK) .NET Core de l’API Document DB d’Azure Cosmos DB."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 7536978bbb1e41b6484b66fd1b51c900fc3e545d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-getting-started-with-the-documentdb-api-and-net-core"></a><span data-ttu-id="7a2a0-103">Azure Cosmos DB : Prise en main de l’API DocumentDB et de .NET Core</span><span class="sxs-lookup"><span data-stu-id="7a2a0-103">Azure Cosmos DB: Getting started with the DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a2a0-104">.NET</span><span class="sxs-lookup"><span data-stu-id="7a2a0-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="7a2a0-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="7a2a0-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="7a2a0-106">Node.js pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="7a2a0-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="7a2a0-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="7a2a0-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="7a2a0-108">Java</span><span class="sxs-lookup"><span data-stu-id="7a2a0-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="7a2a0-109">C++</span><span class="sxs-lookup"><span data-stu-id="7a2a0-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="7a2a0-110">Bienvenue dans le didacticiel Prise en main de l’API DocumentDB pour Azure Cosmos DB avec .NET Core</span><span class="sxs-lookup"><span data-stu-id="7a2a0-110">Welcome to the DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="7a2a0-111">À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="7a2a0-112">Nous allons aborder les points suivants :</span><span class="sxs-lookup"><span data-stu-id="7a2a0-112">We'll cover:</span></span>

* <span data-ttu-id="7a2a0-113">Création et connexion à un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7a2a0-113">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="7a2a0-114">Configuration de votre solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a2a0-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="7a2a0-115">Création d’une base de données en ligne</span><span class="sxs-lookup"><span data-stu-id="7a2a0-115">Creating an online database</span></span>
* <span data-ttu-id="7a2a0-116">Création d’une collection</span><span class="sxs-lookup"><span data-stu-id="7a2a0-116">Creating a collection</span></span>
* <span data-ttu-id="7a2a0-117">Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="7a2a0-117">Creating JSON documents</span></span>
* <span data-ttu-id="7a2a0-118">Interrogation de la collection</span><span class="sxs-lookup"><span data-stu-id="7a2a0-118">Querying the collection</span></span>
* <span data-ttu-id="7a2a0-119">Remplacement d'un document</span><span class="sxs-lookup"><span data-stu-id="7a2a0-119">Replacing a document</span></span>
* <span data-ttu-id="7a2a0-120">Suppression d’un document</span><span class="sxs-lookup"><span data-stu-id="7a2a0-120">Deleting a document</span></span>
* <span data-ttu-id="7a2a0-121">Suppression de la base de données</span><span class="sxs-lookup"><span data-stu-id="7a2a0-121">Deleting the database</span></span>

<span data-ttu-id="7a2a0-122">Vous n’avez pas le temps ?</span><span class="sxs-lookup"><span data-stu-id="7a2a0-122">Don't have time?</span></span> <span data-ttu-id="7a2a0-123">Ne vous inquiétez pas !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-123">Don't worry!</span></span> <span data-ttu-id="7a2a0-124">La solution complète est disponible sur [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-124">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="7a2a0-125">Pour obtenir des instructions rapides, allez à la section [Obtenir la solution complète](#GetSolution) .</span><span class="sxs-lookup"><span data-stu-id="7a2a0-125">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="7a2a0-126">Vous voulez créer une application Xamarin iOS, Android ou Forms à l’aide de l’API DocumentDB et du SDK .NET Core ?</span><span class="sxs-lookup"><span data-stu-id="7a2a0-126">Want to build a Xamarin iOS, Android, or Forms application using the DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="7a2a0-127">Consultez la page [Créer des applications mobiles avec Xamarin et Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7a2a0-128">Le SDK .NET Core Azure Cosmos DB utilisé dans ce didacticiel n’est pas encore compatible avec les applications UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-128">The Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="7a2a0-129">Pour obtenir une version préliminaire du Kit de développement logiciel (SDK) .NET Core qui prenne en charge les applications UWP, envoyez un e-mail à l’adresse [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-129">For a preview version of the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="7a2a0-130">Commençons dès maintenant !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a2a0-131">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7a2a0-131">Prerequisites</span></span>
<span data-ttu-id="7a2a0-132">Vérifiez que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7a2a0-132">Please make sure you have the following:</span></span>

* <span data-ttu-id="7a2a0-133">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-133">An active Azure account.</span></span> <span data-ttu-id="7a2a0-134">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="7a2a0-135">Vous pouvez également utiliser [l’émulateur Azure Cosmos DB](local-emulator.md) pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-135">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="7a2a0-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7a2a0-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="7a2a0-137">Si vous travaillez sous Mac OS ou Linux, vous pouvez développer des applications .NET Core à partir de la ligne de commande en installant le [kit de développement logiciel (SDK) .NET Core](https://www.microsoft.com/net/core#macos) pour la plateforme de votre choix.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-137">If you're working on MacOS or Linux, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span></span> 
    * <span data-ttu-id="7a2a0-138">Si vous travaillez sous Windows, vous pouvez développer des applications .NET Core à partir de la ligne de commande en installant le [kit de développement logiciel (SDK) .NET Core](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-138">If you're working on Windows, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="7a2a0-139">Vous pouvez utiliser votre propre éditeur, ou télécharger [Visual Studio Code](https://code.visualstudio.com/) qui est disponible gratuitement et fonctionne sous Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="7a2a0-140">Étape 1 : créer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7a2a0-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="7a2a0-141">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="7a2a0-142">Si vous avez déjà un compte que vous souhaitez utiliser, vous pouvez passer directement à l’étape [Configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-142">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="7a2a0-143">Si vous utilisez l’émulateur Azure Cosmos DB, suivez les étapes de la section [Émulateur Azure Cosmos DB](local-emulator.md) pour le configurer, puis passez directement à l’étape [Configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-143">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="7a2a0-144"><a id="SetupVS"></a>Étape 2 : configurer votre solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a2a0-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="7a2a0-145">Ouvrez **Visual Studio 2017** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="7a2a0-146">Dans le menu **Fichier**, sélectionnez **Nouveau**, puis choisissez **Projet**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-146">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="7a2a0-147">Dans la boîte de dialogue **Nouveau projet**, sélectionnez **Modèles** / **Visual C#** / **.NET Core**/**Application console (.NET Core)**, nommez votre projet **DocumentDBGettingStarted**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-147">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Capture d’écran de la fenêtre Nouveau projet](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="7a2a0-149">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-149">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="7a2a0-150">Ensuite, sans quitter le menu, cliquez sur **Gérer les packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="7a2a0-150">Then without leaving the menu, click on **Manage NuGet Packages...**.</span></span>

   ![Capture d'écran du menu du clic droit pour le projet](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="7a2a0-152">Dans l’onglet **NuGet**, cliquez sur **Parcourir** en haut de la fenêtre, puis tapez **azure documentdb** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-152">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span></span>
7. <span data-ttu-id="7a2a0-153">Dans les résultats, recherchez **Microsoft.Azure.DocumentDB.Core** et cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-153">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="7a2a0-154">L’ID de package de la bibliothèque cliente DocumentDB pour .NET Core est [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-154">The package ID for the DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="7a2a0-155">Si vous ciblez une version de .NET Framework (net461, par exemple) qui n’est pas prise en charge par ce package NuGet .NET Core, utilisez [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) qui prend en charge toutes les versions de .NET Framework à partir de la version 4.5.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="7a2a0-156">Aux invites, acceptez les installations de packages NuGet et le contrat de licence.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-156">At the prompts, accept the NuGet package installations and the license agreement.</span></span>

<span data-ttu-id="7a2a0-157">Parfait !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-157">Great!</span></span> <span data-ttu-id="7a2a0-158">L’installation étant terminée, nous pouvons passer à l’écriture du code.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-158">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="7a2a0-159">Vous trouverez le projet de code complet de ce didacticiel dans [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="7a2a0-160"><a id="Connect"></a>Étape 3 : se connecter à un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7a2a0-160"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="7a2a0-161">Tout d’abord, ajoutez ces références au début de votre application C#, dans le fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="7a2a0-161">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART TO YOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="7a2a0-162">Pour pouvoir exécuter ce didacticiel, veillez à ajouter les dépendances ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-162">In order to complete this tutorial, make sure you add the dependencies above.</span></span>

<span data-ttu-id="7a2a0-163">Maintenant, ajoutez ces deux constantes et votre variable *client* dans votre classe publique *Program*.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="7a2a0-164">Ensuite, accédez au [portail Azure](https://portal.azure.com) pour récupérer votre URI et votre clé primaire.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-164">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span></span> <span data-ttu-id="7a2a0-165">L’URI et la clé primaire Azure Cosmos DB sont nécessaires pour que votre application sache où se connecter et qu’Azure Cosmos DB approuve la connexion de votre application.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-165">The Azure Cosmos DB URI and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="7a2a0-166">Dans le portail Azure, accédez à votre compte Azure Cosmos DB, puis cliquez sur **Clés**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-166">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="7a2a0-167">Copiez l’URI à partir du portail et collez-le dans `<your endpoint URI>` dans le fichier program.cs.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-167">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span></span> <span data-ttu-id="7a2a0-168">Ensuite, copiez la clé primaire à partir du portail, puis collez-la dans `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-168">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span> <span data-ttu-id="7a2a0-169">Si vous utilisez l’émulateur Azure Cosmos DB, utilisez `https://localhost:8081` comme point de terminaison et la clé d’autorisation bien définie dans [How to develop using the Azure Cosmos DB Emulator](local-emulator.md) (Comment développer à l’aide de l’émulateur Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-169">If you are using the Azure Cosmos DB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="7a2a0-170">Assurez-vous de supprimer le < et > , mais laissez les guillemets doubles autour de votre point de terminaison et de la clé.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-170">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span></span>

![Capture d’écran du portail Azure utilisée par le didacticiel NoSQL pour créer une application de console C#.][keys]

<span data-ttu-id="7a2a0-173">Nous allons démarrer l’application de prise en main en créant une instance de **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-173">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="7a2a0-174">Sous la méthode **Main**, ajoutez la nouvelle tâche asynchrone appelée **GetStartedDemo** qui va instancier notre nouveau **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-174">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART TO YOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="7a2a0-175">Ajoutez le code suivant pour exécuter votre tâche asynchrone à partir de la méthode **Main** .</span><span class="sxs-lookup"><span data-stu-id="7a2a0-175">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="7a2a0-176">La méthode **Main** va intercepter les exceptions et les consigner dans la console.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-176">The **Main** method will catch exceptions and write them to the console.</span></span>

```csharp
static void Main(string[] args)
{
        // ADD THIS PART TO YOUR CODE
        try
        {
                Program p = new Program();
                p.GetStartedDemo().Wait();
        }
        catch (DocumentClientException de)
        {
                Exception baseException = de.GetBaseException();
                Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
        }
        catch (Exception e)
        {
                Exception baseException = e.GetBaseException();
                Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
        }
        finally
        {
                Console.WriteLine("End of demo, press any key to exit.");
                Console.ReadKey();
        }
```

<span data-ttu-id="7a2a0-177">Appuyez sur le bouton **DocumentDBGettingStarted** pour générer et exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-177">Press the **DocumentDBGettingStarted** button to build and run the application.</span></span>

<span data-ttu-id="7a2a0-178">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-178">Congratulations!</span></span> <span data-ttu-id="7a2a0-179">Vous êtes connecté à un compte Azure Cosmos DB. Jetons maintenant un œil à l’utilisation des ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-179">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="7a2a0-180">Étape 4 : créer une base de données</span><span class="sxs-lookup"><span data-stu-id="7a2a0-180">Step 4: Create a database</span></span>
<span data-ttu-id="7a2a0-181">Avant d'ajouter le code permettant de créer une base de données, ajoutez une méthode d'assistance pour l'écriture sur la console.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-181">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="7a2a0-182">Copiez et collez la méthode **WriteToConsoleAndPromptToContinue** sous la méthode **GetStartedDemo**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-182">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="7a2a0-183">Pour créer votre [base de données](documentdb-resources.md#databases) Azure Cosmos DB, utilisez la méthode [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) de la classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="7a2a0-184">Une base de données est le conteneur logique de stockage de documents JSON partitionné entre les collections.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-184">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="7a2a0-185">Copiez et collez le code suivant dans votre méthode **GetStartedDemo** en dessous de la création du client.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-185">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span></span> <span data-ttu-id="7a2a0-186">Ce faisant, vous créez la base de données *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="7a2a0-187">Appuyez sur le bouton **DocumentDBGettingStarted** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-187">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a2a0-188">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-188">Congratulations!</span></span> <span data-ttu-id="7a2a0-189">Vous avez créé une base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="7a2a0-190"><a id="CreateColl"></a>Étape 5 : créer une collection</span><span class="sxs-lookup"><span data-stu-id="7a2a0-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="7a2a0-191">**CreateDocumentCollectionAsync** crée une collection avec un débit réservé, ce qui a des conséquences sur la tarification.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="7a2a0-192">Pour plus d'informations, visitez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="7a2a0-193">Vous pouvez créer une [collection](documentdb-resources.md#collections) à l’aide de la méthode [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) de la classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-193">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="7a2a0-194">Une collection est un conteneur de documents JSON. Elle est associée à une logique d'application JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="7a2a0-195">Copiez et collez le code suivant dans votre méthode **GetStartedDemo** en dessous de la création de la base de données.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-195">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span></span> <span data-ttu-id="7a2a0-196">Ce faisant, vous créez la collection de documents *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="7a2a0-197">Appuyez sur le bouton **DocumentDBGettingStarted** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-197">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a2a0-198">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-198">Congratulations!</span></span> <span data-ttu-id="7a2a0-199">Vous avez créé une collection de documents Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="7a2a0-200"><a id="CreateDoc"></a>Étape 6 : Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="7a2a0-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="7a2a0-201">Vous pouvez créer un [document](documentdb-resources.md#documents) à l’aide de la méthode [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) de la classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-201">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="7a2a0-202">Les documents correspondent à du contenu JSON (arbitraire) défini par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="7a2a0-203">Nous pouvons maintenant insérer un ou plusieurs documents.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-203">We can now insert one or more documents.</span></span> <span data-ttu-id="7a2a0-204">Si vous disposez déjà de données que vous souhaitez stocker dans votre base de données, vous pouvez utiliser [l’outil de migration de données](import-data.md) d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-204">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="7a2a0-205">Nous devons tout d’abord créer une classe **Family** représentant les objets stockés dans Azure Cosmos DB dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-205">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="7a2a0-206">Nous allons également créer les sous-classes **Parent**, **Child**, **Pet** et **Address** qui seront utilisées dans **Family**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="7a2a0-207">Notez que les documents doivent avoir une propriété **Id** sérialisée comme **id** dans JSON.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="7a2a0-208">Créez ces classes en ajoutant les sous-classes internes suivantes après la méthode **GetStartedDemo** .</span><span class="sxs-lookup"><span data-stu-id="7a2a0-208">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="7a2a0-209">Copiez et collez les classes **Family**, **Parent**, **Child**, **Pet** et **Address** sous la méthode **WriteToConsoleAndPromptToContinue**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-209">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
    Console.WriteLine(format, args);
    Console.WriteLine("Press any key to continue ...");
    Console.ReadKey();
}

// ADD THIS PART TO YOUR CODE
public class Family
{
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }
    public string LastName { get; set; }
    public Parent[] Parents { get; set; }
    public Child[] Children { get; set; }
    public Address Address { get; set; }
    public bool IsRegistered { get; set; }
    public override string ToString()
    {
            return JsonConvert.SerializeObject(this);
    }
}

public class Parent
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
}

public class Child
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
    public string Gender { get; set; }
    public int Grade { get; set; }
    public Pet[] Pets { get; set; }
}

public class Pet
{
    public string GivenName { get; set; }
}

public class Address
{
    public string State { get; set; }
    public string County { get; set; }
    public string City { get; set; }
}
```

<span data-ttu-id="7a2a0-210">Copiez et collez la méthode **CreateFamilyDocumentIfNotExists** sous votre méthode **CreateDocumentCollectionIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-210">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
{
    try
    {
        await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
        this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
    }
    catch (DocumentClientException de)
    {
        if (de.StatusCode == HttpStatusCode.NotFound)
        {
            await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
            this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
        }
        else
        {
            throw;
        }
    }
}
```

<span data-ttu-id="7a2a0-211">Insérez ensuite deux documents, un pour la famille Andersen, l’autre pour la famille Wakefield.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-211">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="7a2a0-212">Copiez et collez le code suivant `// ADD THIS PART TO YOUR CODE` dans votre méthode **GetStartedDemo** en dessous de la création de la collection de documents.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-212">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
Family andersenFamily = new Family
{
        Id = "Andersen.1",
        LastName = "Andersen",
        Parents = new Parent[]
        {
                new Parent { FirstName = "Thomas" },
                new Parent { FirstName = "Mary Kay" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FirstName = "Henriette Thaulow",
                        Gender = "female",
                        Grade = 5,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Fluffy" }
                        }
                }
        },
        Address = new Address { State = "WA", County = "King", City = "Seattle" },
        IsRegistered = true
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

Family wakefieldFamily = new Family
{
        Id = "Wakefield.7",
        LastName = "Wakefield",
        Parents = new Parent[]
        {
                new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                new Parent { FamilyName = "Miller", FirstName = "Ben" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FamilyName = "Merriam",
                        FirstName = "Jesse",
                        Gender = "female",
                        Grade = 8,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Goofy" },
                                new Pet { GivenName = "Shadow" }
                        }
                },
                new Child
                {
                        FamilyName = "Miller",
                        FirstName = "Lisa",
                        Gender = "female",
                        Grade = 1
                }
        },
        Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
        IsRegistered = false
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

<span data-ttu-id="7a2a0-213">Appuyez sur le bouton **DocumentDBGettingStarted** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-213">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a2a0-214">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-214">Congratulations!</span></span> <span data-ttu-id="7a2a0-215">Vous avez créé deux documents Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagramme illustrant la relation hiérarchique existant entre le compte, la base de données en ligne, la collection et les documents utilisés par le didacticiel NoSQL pour créer une application de console C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="7a2a0-217"><a id="Query"></a>Étape 7 : interroger les ressources Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7a2a0-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="7a2a0-218">Azure Cosmos DB prend en charge les [requêtes](documentdb-sql-query.md) enrichies sur les documents JSON stockés dans chaque collection.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="7a2a0-219">L’exemple de code suivant affiche différentes requêtes (à l’aide de la syntaxe SQL d’Azure Cosmos DB et de LINQ) que nous pouvons exécuter sur les documents insérés à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-219">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="7a2a0-220">Copiez et collez la méthode **ExecuteSimpleQuery** sous votre méthode **CreateFamilyDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-220">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void ExecuteSimpleQuery(string databaseName, string collectionName)
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

        // Here we find the Andersen family via its LastName
        IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(f => f.LastName == "Andersen");

        // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (Family family in familyQuery)
        {
            Console.WriteLine("\tRead {0}", family);
        }

        // Now execute the same query via direct SQL
        IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                queryOptions);

        Console.WriteLine("Running direct SQL query...");
        foreach (Family family in familyQueryInSql)
        {
                Console.WriteLine("\tRead {0}", family);
        }

        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="7a2a0-221">Copiez et collez le code suivant dans votre méthode **GetStartedDemo** en dessous de la création du deuxième document.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-221">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="7a2a0-222">Appuyez sur le bouton **DocumentDBGettingStarted** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-222">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a2a0-223">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-223">Congratulations!</span></span> <span data-ttu-id="7a2a0-224">Vous avez interrogé une collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="7a2a0-225">Le schéma suivant montre comment la syntaxe de requête SQL d’Azure Cosmos DB est appelée sur la collection que vous avez créée. C’est par ailleurs cette même logique qui s’applique à la requête LINQ.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-225">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagramme illustrant l’étendue et la signification de la requête utilisée par le didacticiel NoSQL pour créer une application de console C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="7a2a0-227">Le mot clé [FROM](documentdb-sql-query.md#FromClause) est facultatif dans la requête, car les requêtes Azure Cosmos DB sont déjà étendues à une collection unique.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-227">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="7a2a0-228">Par conséquent, « FROM Families f » peut être remplacé par «FROM root r » ou par tout autre nom de variable que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="7a2a0-229">DocumentDB déduira que Families, root ou le nom de variable choisi fait par défaut référence à la collection actuelle.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-229">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="7a2a0-230"><a id="ReplaceDocument"></a>Étape 8 : remplacer le document JSON</span><span class="sxs-lookup"><span data-stu-id="7a2a0-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="7a2a0-231">Azure Cosmos DB prend en charge le remplacement des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="7a2a0-232">Copiez et collez la méthode **ReplaceFamilyDocument** sous votre méthode **ExecuteSimpleQuery**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-232">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="7a2a0-233">Copiez et collez le code suivant dans votre méthode **GetStartedDemo** en dessous de l’exécution de la requête.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-233">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span></span> <span data-ttu-id="7a2a0-234">Après avoir remplacé le document, cela exécutera à nouveau la même requête pour afficher le document modifié.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-234">After replacing the document, this will run the same query again to view the changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="7a2a0-235">Appuyez sur le bouton **DocumentDBGettingStarted** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-235">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a2a0-236">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-236">Congratulations!</span></span> <span data-ttu-id="7a2a0-237">Vous avez remplacé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="7a2a0-238"><a id="DeleteDocument"></a>Étape 9 : supprimer le document JSON</span><span class="sxs-lookup"><span data-stu-id="7a2a0-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="7a2a0-239">Azure Cosmos DB prend en charge la suppression des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="7a2a0-240">Copiez et collez la méthode **DeleteFamilyDocument** sous votre méthode **ReplaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-240">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="7a2a0-241">Copiez et collez le code suivant dans votre méthode **GetStartedDemo** en dessous de l’exécution de la deuxième requête.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-241">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="7a2a0-242">Appuyez sur le bouton **DocumentDBGettingStarted** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-242">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a2a0-243">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-243">Congratulations!</span></span> <span data-ttu-id="7a2a0-244">Vous avez supprimé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="7a2a0-245"><a id="DeleteDatabase"></a>Étape 10 : supprimer la base de données</span><span class="sxs-lookup"><span data-stu-id="7a2a0-245"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="7a2a0-246">Supprimer la base de données créée revient à supprimer la base de données et toutes les ressources enfants (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-246">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="7a2a0-247">Copiez et collez le code suivant dans votre méthode **GetStartedDemo** sous la suppression du document, pour supprimer la base de données et toutes ses ressources enfants.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-247">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="7a2a0-248">Appuyez sur le bouton **DocumentDBGettingStarted** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-248">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a2a0-249">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-249">Congratulations!</span></span> <span data-ttu-id="7a2a0-250">Vous avez supprimé une base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="7a2a0-251"><a id="Run"></a>Étape 11 : exécuter votre application de console C#</span><span class="sxs-lookup"><span data-stu-id="7a2a0-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="7a2a0-252">Appuyez sur le bouton **DocumentDBGettingStarted** dans Visual Studio pour générer l’application en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-252">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="7a2a0-253">La sortie de votre application de prise en main doit s’afficher dans la fenêtre de la console.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-253">You should see the output of your get started app in the console window.</span></span> <span data-ttu-id="7a2a0-254">Celle-ci doit présenter les résultats des requêtes que nous avons ajoutées, qui doivent correspondre au texte d'exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-254">The output will show the results of the queries we added and should match the example text below.</span></span>

```
Created FamilyDB_oa
Press any key to continue ...
Created FamilyCollection_oa
Press any key to continue ...
Created Family Andersen.1
Press any key to continue ...
Created Family Wakefield.7
Press any key to continue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Replaced Family Andersen.1
Press any key to continue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Deleted Family Andersen.1
End of demo, press any key to exit.
```

<span data-ttu-id="7a2a0-255">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-255">Congratulations!</span></span> <span data-ttu-id="7a2a0-256">Vous avez terminé le didacticiel et vous disposez d’une application de console C# qui fonctionne !</span><span class="sxs-lookup"><span data-stu-id="7a2a0-256">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="7a2a0-257"><a id="GetSolution"></a> Obtenir la solution complète du didacticiel</span><span class="sxs-lookup"><span data-stu-id="7a2a0-257"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="7a2a0-258">Pour générer la solution GetStarted qui contient tous les exemples de cet article, vous devez avoir les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7a2a0-258">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="7a2a0-259">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-259">An active Azure account.</span></span> <span data-ttu-id="7a2a0-260">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="7a2a0-261">Un [compte Azure Cosmos DB][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="7a2a0-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="7a2a0-262">La solution [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-262">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="7a2a0-263">Pour restaurer les références à l’API DocumentDB pour le SDK .NET Core Azure Cosmos DB dans Visual Studio, cliquez avec le bouton droit sur la solution **GetStarted** dans l’Explorateur de solutions, puis cliquez sur **Activer la restauration des packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7a2a0-263">To restore the references to the DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="7a2a0-264">Ensuite, dans le fichier Program.cs, mettez à jour les valeurs pour EndpointUrl et AuthorizationKey comme décrit dans [Se connecter à un compte Azure Cosmos DB](#Connect).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-264">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a2a0-265">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7a2a0-265">Next steps</span></span>
* <span data-ttu-id="7a2a0-266">Vous voulez un didacticiel ASP.NET MVC plus complexe ?</span><span class="sxs-lookup"><span data-stu-id="7a2a0-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="7a2a0-267">Reportez-vous à la page [Didacticiel ASP.NET MVC : développement d’applications web avec Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="7a2a0-268">Vous voulez développer une application Xamarin iOS, Android ou Forms à l’aide de l’API DocumentDB pour le SDK .NET Core Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="7a2a0-268">Want to develop a Xamarin iOS, Android, or Forms application using the DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="7a2a0-269">Consultez la page [Créer des applications mobiles avec Xamarin et Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="7a2a0-270">Vous voulez effectuer un test des performances et de la mise à l’échelle avec Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="7a2a0-270">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="7a2a0-271">Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="7a2a0-272">Découvrez comment [Surveiller le stockage, l’utilisation et les demandes Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-272">Learn how to [Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="7a2a0-273">Exécutez des requêtes sur notre exemple de dataset dans le [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-273">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="7a2a0-274">Pour en savoir plus sur le modèle de programmation, consultez la page [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="7a2a0-274">To learn more about the programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
