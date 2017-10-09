---
title: "Azure Cosmos DB : Didacticiel sur la prise en main de l’API DocumentDB avec .NET Core | Microsoft Docs"
description: "Un didacticiel qui crée une base de données en ligne et une application console c# à l’aide de hello Azure Cosmos API DB DocumentDB .NET Core SDK."
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
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a><span data-ttu-id="9b46e-103">Azure Cosmos DB : Prise en main de hello API DocumentDB et .NET Core</span><span class="sxs-lookup"><span data-stu-id="9b46e-103">Azure Cosmos DB: Getting started with hello DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b46e-104">.NET</span><span class="sxs-lookup"><span data-stu-id="9b46e-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="9b46e-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="9b46e-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="9b46e-106">Node.js pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="9b46e-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="9b46e-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="9b46e-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="9b46e-108">Java</span><span class="sxs-lookup"><span data-stu-id="9b46e-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="9b46e-109">C++</span><span class="sxs-lookup"><span data-stu-id="9b46e-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="9b46e-110">Bienvenue toohello API DocumentDB de base de données Azure Cosmos mise en route du didacticiel de .NET Core !</span><span class="sxs-lookup"><span data-stu-id="9b46e-110">Welcome toohello DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="9b46e-111">À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9b46e-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="9b46e-112">Nous allons aborder les points suivants :</span><span class="sxs-lookup"><span data-stu-id="9b46e-112">We'll cover:</span></span>

* <span data-ttu-id="9b46e-113">Création et connexion de compte de base de données Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="9b46e-113">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="9b46e-114">Configuration de votre solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9b46e-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="9b46e-115">Création d’une base de données en ligne</span><span class="sxs-lookup"><span data-stu-id="9b46e-115">Creating an online database</span></span>
* <span data-ttu-id="9b46e-116">Création d’une collection</span><span class="sxs-lookup"><span data-stu-id="9b46e-116">Creating a collection</span></span>
* <span data-ttu-id="9b46e-117">Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="9b46e-117">Creating JSON documents</span></span>
* <span data-ttu-id="9b46e-118">Interrogation de collection de hello</span><span class="sxs-lookup"><span data-stu-id="9b46e-118">Querying hello collection</span></span>
* <span data-ttu-id="9b46e-119">Remplacement d'un document</span><span class="sxs-lookup"><span data-stu-id="9b46e-119">Replacing a document</span></span>
* <span data-ttu-id="9b46e-120">Suppression d’un document</span><span class="sxs-lookup"><span data-stu-id="9b46e-120">Deleting a document</span></span>
* <span data-ttu-id="9b46e-121">Suppression de la base de données hello</span><span class="sxs-lookup"><span data-stu-id="9b46e-121">Deleting hello database</span></span>

<span data-ttu-id="9b46e-122">Vous n’avez pas le temps ?</span><span class="sxs-lookup"><span data-stu-id="9b46e-122">Don't have time?</span></span> <span data-ttu-id="9b46e-123">Ne vous inquiétez pas !</span><span class="sxs-lookup"><span data-stu-id="9b46e-123">Don't worry!</span></span> <span data-ttu-id="9b46e-124">solution complète de Hello est disponible sur [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9b46e-124">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="9b46e-125">Raccourcis toohello [obtenir la section de solution complète hello](#GetSolution) pour obtenir des instructions rapides.</span><span class="sxs-lookup"><span data-stu-id="9b46e-125">Jump toohello [Get hello complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="9b46e-126">Voulez toobuild un Xamarin iOS, Android ou des formulaires à l’aide de l’application hello API DocumentDB et Kit de développement .NET Core ?</span><span class="sxs-lookup"><span data-stu-id="9b46e-126">Want toobuild a Xamarin iOS, Android, or Forms application using hello DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="9b46e-127">Consultez la page [Créer des applications mobiles avec Xamarin et Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="9b46e-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9b46e-128">Bonjour Azure Cosmos DB .NET Core SDK est utilisé dans ce didacticiel n’est pas encore compatible avec les applications de plateforme Windows universelle (UWP).</span><span class="sxs-lookup"><span data-stu-id="9b46e-128">hello Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="9b46e-129">Pour une version préliminaire du Kit de développement .NET Core qui ne prend pas en charge les applications UWP de hello, envoyer un courrier électronique trop[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="9b46e-129">For a preview version of hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="9b46e-130">Commençons dès maintenant !</span><span class="sxs-lookup"><span data-stu-id="9b46e-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b46e-131">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9b46e-131">Prerequisites</span></span>
<span data-ttu-id="9b46e-132">Vérifiez que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="9b46e-132">Please make sure you have hello following:</span></span>

* <span data-ttu-id="9b46e-133">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="9b46e-133">An active Azure account.</span></span> <span data-ttu-id="9b46e-134">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9b46e-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="9b46e-135">Vous pouvez également utiliser hello [Azure Cosmos DB émulateur](local-emulator.md) pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9b46e-135">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="9b46e-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9b46e-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="9b46e-137">Si vous travaillez sur MacOS ou Linux, vous pouvez développer des applications .NET Core à partir de ligne de commande de hello en installant hello [le Kit de développement .NET Core](https://www.microsoft.com/net/core#macos) pour la plateforme hello de votre choix.</span><span class="sxs-lookup"><span data-stu-id="9b46e-137">If you're working on MacOS or Linux, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) for hello platform of your choice.</span></span> 
    * <span data-ttu-id="9b46e-138">Si vous travaillez sur Windows, vous pouvez développer des applications .NET Core à partir de ligne de commande de hello en installant hello [le Kit de développement .NET Core](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="9b46e-138">If you're working on Windows, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="9b46e-139">Vous pouvez utiliser votre propre éditeur, ou télécharger [Visual Studio Code](https://code.visualstudio.com/) qui est disponible gratuitement et fonctionne sous Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="9b46e-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="9b46e-140">Étape 1 : créer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9b46e-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="9b46e-141">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9b46e-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="9b46e-142">Si vous avez déjà un compte que vous souhaitez toouse, vous pouvez passer trop[le programme d’installation de votre Solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="9b46e-142">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="9b46e-143">Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[le programme d’installation de votre Solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="9b46e-143">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="9b46e-144"><a id="SetupVS"></a>Étape 2 : configurer votre solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9b46e-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="9b46e-145">Ouvrez **Visual Studio 2017** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9b46e-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="9b46e-146">Sur hello **fichier** menu, sélectionnez **nouveau**, puis choisissez **projet**.</span><span class="sxs-lookup"><span data-stu-id="9b46e-146">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="9b46e-147">Bonjour **nouveau projet** boîte de dialogue, sélectionnez **modèles** / **Visual C#** / **.NET Core** / **L’Application console (.NET Core)**, nommez votre projet **DocumentDBGettingStarted**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b46e-147">In hello **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Capture d’écran de la fenêtre de nouveau projet hello](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="9b46e-149">Bonjour **l’Explorateur de solutions**, cliquez avec le bouton droit sur **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="9b46e-149">In hello **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="9b46e-150">Sans quitter le menu de hello, cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="9b46e-150">Then without leaving hello menu, click on **Manage NuGet Packages...**.</span></span>

   ![Capture d’écran de hello droite Menu Clicked hello projet](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="9b46e-152">Bonjour **NuGet** , cliquez sur **Parcourir** haut hello fenêtre hello et type **azure documentdb** dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-152">In hello **NuGet** tab, click **Browse** at hello top of hello window, and type **azure documentdb** in hello search box.</span></span>
7. <span data-ttu-id="9b46e-153">Dans les résultats de hello, recherchez **Microsoft.Azure.DocumentDB.Core** et cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="9b46e-153">Within hello results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="9b46e-154">ID de package Hello pour hello bibliothèque cliente de DocumentDB pour .NET Core est [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="9b46e-154">hello package ID for hello DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="9b46e-155">Si vous ciblez une version de .NET Framework (net461, par exemple) qui n’est pas prise en charge par ce package NuGet .NET Core, utilisez [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) qui prend en charge toutes les versions de .NET Framework à partir de la version 4.5.</span><span class="sxs-lookup"><span data-stu-id="9b46e-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="9b46e-156">Aux invites de hello, acceptez les installations des packages NuGet hello et contrat de licence hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-156">At hello prompts, accept hello NuGet package installations and hello license agreement.</span></span>

<span data-ttu-id="9b46e-157">Parfait !</span><span class="sxs-lookup"><span data-stu-id="9b46e-157">Great!</span></span> <span data-ttu-id="9b46e-158">Maintenant que nous avons terminé le programme d’installation Bonjour, nous pouvons commencer l’écriture du code.</span><span class="sxs-lookup"><span data-stu-id="9b46e-158">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="9b46e-159">Vous trouverez le projet de code complet de ce didacticiel dans [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9b46e-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="9b46e-160"><a id="Connect"></a>Étape 3 : Relier le compte de base de données Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="9b46e-160"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="9b46e-161">Tout d’abord, ajoutez ces références début toohello de votre application c#, dans le fichier Program.cs de hello :</span><span class="sxs-lookup"><span data-stu-id="9b46e-161">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="9b46e-162">Dans l’ordre toocomplete ce didacticiel, veillez à qu'ajouter des dépendances de hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9b46e-162">In order toocomplete this tutorial, make sure you add hello dependencies above.</span></span>

<span data-ttu-id="9b46e-163">Maintenant, ajoutez ces deux constantes et votre variable *client* dans votre classe publique *Program*.</span><span class="sxs-lookup"><span data-stu-id="9b46e-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="9b46e-164">Ensuite, head toohello [Azure Portal](https://portal.azure.com) tooretrieve votre URI et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="9b46e-164">Next, head toohello [Azure Portal](https://portal.azure.com) tooretrieve your URI and primary key.</span></span> <span data-ttu-id="9b46e-165">Hello URI de base de données Azure Cosmos et la clé primaire sont nécessaires pour votre application toounderstand où tooconnect et de base de données Azure Cosmos tootrust connexion de votre application.</span><span class="sxs-lookup"><span data-stu-id="9b46e-165">hello Azure Cosmos DB URI and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="9b46e-166">Dans hello portail Azure, accédez de compte de base de données Azure Cosmos tooyour, puis cliquez sur **clés**.</span><span class="sxs-lookup"><span data-stu-id="9b46e-166">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="9b46e-167">Copiez hello URI à partir du portail de hello, puis collez-la dans `<your endpoint URI>` dans le fichier program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-167">Copy hello URI from hello portal and paste it into `<your endpoint URI>` in hello program.cs file.</span></span> <span data-ttu-id="9b46e-168">Copie hello clé primaire à partir du portail de hello et collez-la dans `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="9b46e-168">Then copy hello PRIMARY KEY from hello portal and paste it into `<your key>`.</span></span> <span data-ttu-id="9b46e-169">Si vous utilisez hello Azure Cosmos DB émulateur, utilisez `https://localhost:8081` en tant que point de terminaison hello et clé d’autorisation bien défini hello [comment l’à l’aide de toodevelop hello Azure Cosmos DB émulateur](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="9b46e-169">If you are using hello Azure Cosmos DB Emulator, use `https://localhost:8081` as hello endpoint, and hello well-defined authorization key from [How toodevelop using hello Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="9b46e-170">Assurez-vous que tooremove hello < et >, mais laissez hello des guillemets doubles autour de votre point de terminaison et la clé.</span><span class="sxs-lookup"><span data-stu-id="9b46e-170">Make sure tooremove hello < and > but leave hello double quotes around your endpoint and key.</span></span>

![Capture d’écran de hello portail Azure utilisée par hello toocreate de didacticiel NoSQL une application console c#.][keys]

<span data-ttu-id="9b46e-173">Nous allons commencer l’application démarrée lors de l’obtention de hello en créant une nouvelle instance de hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="9b46e-173">We'll start hello getting started application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="9b46e-174">Ci-dessous hello **principal** méthode, ajoutez cette nouvelle tâche asynchrone appelée **GetStartedDemo**, qui instancie notre nouveau **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="9b46e-174">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="9b46e-175">Ajouter le code suivant de hello toorun votre tâche asynchrone à partir de votre **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9b46e-175">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="9b46e-176">Hello **Main** méthode intercepter les exceptions et les écrire toohello console.</span><span class="sxs-lookup"><span data-stu-id="9b46e-176">hello **Main** method will catch exceptions and write them toohello console.</span></span>

```csharp
static void Main(string[] args)
{
        // ADD THIS PART tooYOUR CODE
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
                Console.WriteLine("End of demo, press any key tooexit.");
                Console.ReadKey();
        }
```

<span data-ttu-id="9b46e-177">Hello de presse **DocumentDBGettingStarted** bouton toobuild et exécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-177">Press hello **DocumentDBGettingStarted** button toobuild and run hello application.</span></span>

<span data-ttu-id="9b46e-178">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9b46e-178">Congratulations!</span></span> <span data-ttu-id="9b46e-179">Vous avez correctement connecté le compte de base de données Azure Cosmos tooan, maintenant examinons une utilisation des ressources de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9b46e-179">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="9b46e-180">Étape 4 : créer une base de données</span><span class="sxs-lookup"><span data-stu-id="9b46e-180">Step 4: Create a database</span></span>
<span data-ttu-id="9b46e-181">Avant d’ajouter de code hello pour la création d’une base de données, ajoutez une méthode d’assistance pour l’écriture de toohello console.</span><span class="sxs-lookup"><span data-stu-id="9b46e-181">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="9b46e-182">Copiez et collez hello **WriteToConsoleAndPromptToContinue** méthode sous hello **GetStartedDemo** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9b46e-182">Copy and paste hello **WriteToConsoleAndPromptToContinue** method underneath hello **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="9b46e-183">Votre base de données Azure Cosmos [base de données](documentdb-resources.md#databases) peuvent être créés à l’aide de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) méthode Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="9b46e-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="9b46e-184">Une base de données est un conteneur logique de hello JSON de stockage de documents partitionné entre des collections.</span><span class="sxs-lookup"><span data-stu-id="9b46e-184">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="9b46e-185">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode en dessous de la création du client hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-185">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello client creation.</span></span> <span data-ttu-id="9b46e-186">Ce faisant, vous créez la base de données *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="9b46e-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="9b46e-187">Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="9b46e-187">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="9b46e-188">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9b46e-188">Congratulations!</span></span> <span data-ttu-id="9b46e-189">Vous avez créé une base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9b46e-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="9b46e-190"><a id="CreateColl"></a>Étape 5 : créer une collection</span><span class="sxs-lookup"><span data-stu-id="9b46e-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="9b46e-191">**CreateDocumentCollectionAsync** crée une collection avec un débit réservé, ce qui a des conséquences sur la tarification.</span><span class="sxs-lookup"><span data-stu-id="9b46e-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="9b46e-192">Pour plus d'informations, visitez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="9b46e-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="9b46e-193">A [collection](documentdb-resources.md#collections) peuvent être créés à l’aide de hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) méthode Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="9b46e-193">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="9b46e-194">Une collection est un conteneur de documents JSON. Elle est associée à une logique d'application JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9b46e-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="9b46e-195">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode en dessous de la création de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-195">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello database creation.</span></span> <span data-ttu-id="9b46e-196">Ce faisant, vous créez la collection de documents *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="9b46e-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="9b46e-197">Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="9b46e-197">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="9b46e-198">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9b46e-198">Congratulations!</span></span> <span data-ttu-id="9b46e-199">Vous avez créé une collection de documents Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9b46e-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="9b46e-200"><a id="CreateDoc"></a>Étape 6 : Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="9b46e-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="9b46e-201">A [document](documentdb-resources.md#documents) peuvent être créés à l’aide de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) méthode Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="9b46e-201">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="9b46e-202">Les documents correspondent à du contenu JSON (arbitraire) défini par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9b46e-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="9b46e-203">Nous pouvons maintenant insérer un ou plusieurs documents.</span><span class="sxs-lookup"><span data-stu-id="9b46e-203">We can now insert one or more documents.</span></span> <span data-ttu-id="9b46e-204">Si vous avez déjà des données que vous souhaitez toostore dans votre base de données, vous pouvez utiliser Azure Cosmos DB [l’outil de Migration de données](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="9b46e-204">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="9b46e-205">Tout d’abord, nous devons toocreate un **famille** classe représentant des objets stockés dans la base de données Azure Cosmos dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="9b46e-205">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="9b46e-206">Nous allons également créer les sous-classes **Parent**, **Child**, **Pet** et **Address** qui seront utilisées dans **Family**.</span><span class="sxs-lookup"><span data-stu-id="9b46e-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="9b46e-207">Notez que les documents doivent avoir une propriété **Id** sérialisée comme **id** dans JSON.</span><span class="sxs-lookup"><span data-stu-id="9b46e-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="9b46e-208">Créer ces classes en ajoutant hello suivant sous-classes internes après hello **GetStartedDemo** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9b46e-208">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="9b46e-209">Copiez et collez hello **famille**, **Parent**, **enfant**, **animal de compagnie**, et **adresse** classes sous Hello **WriteToConsoleAndPromptToContinue** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9b46e-209">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath hello **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
    Console.WriteLine(format, args);
    Console.WriteLine("Press any key toocontinue ...");
    Console.ReadKey();
}

// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="9b46e-210">Copiez et collez hello **CreateFamilyDocumentIfNotExists** méthode sous votre **CreateDocumentCollectionIfNotExists** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9b46e-210">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="9b46e-211">Et insérez les deux documents, un pour chacun des hello Andersen famille et hello Wakefield famille.</span><span class="sxs-lookup"><span data-stu-id="9b46e-211">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="9b46e-212">Copiez et collez le code hello qui suit `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** méthode en dessous de la création de la collection de document hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-212">Copy and paste hello code that follows `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** method underneath hello document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="9b46e-213">Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="9b46e-213">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="9b46e-214">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9b46e-214">Congratulations!</span></span> <span data-ttu-id="9b46e-215">Vous avez créé deux documents Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9b46e-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagramme illustrant relation hiérarchique hello entre le compte de hello, base de données en ligne hello, la collection de hello et documents hello utilisés par hello toocreate de didacticiel NoSQL une application console c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="9b46e-217"><a id="Query"></a>Étape 7 : interroger les ressources Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9b46e-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="9b46e-218">Azure Cosmos DB prend en charge les [requêtes](documentdb-sql-query.md) enrichies sur les documents JSON stockés dans chaque collection.</span><span class="sxs-lookup"><span data-stu-id="9b46e-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="9b46e-219">Hello exemple de code suivant montre différentes requêtes - à l’aide de la base de données SQL Azure Cosmos syntaxe ainsi que LINQ - ce que nous pouvons exécuter par rapport aux documents que nous insérés à l’étape précédente de hello hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-219">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="9b46e-220">Copiez et collez hello **ExecuteSimpleQuery** méthode sous votre **CreateFamilyDocumentIfNotExists** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9b46e-220">Copy and paste hello **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void ExecuteSimpleQuery(string databaseName, string collectionName)
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

        // Here we find hello Andersen family via its LastName
        IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(f => f.LastName == "Andersen");

        // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (Family family in familyQuery)
        {
            Console.WriteLine("\tRead {0}", family);
        }

        // Now execute hello same query via direct SQL
        IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                queryOptions);

        Console.WriteLine("Running direct SQL query...");
        foreach (Family family in familyQueryInSql)
        {
                Console.WriteLine("\tRead {0}", family);
        }

        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="9b46e-221">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode en dessous de la création d’un deuxième document hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-221">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="9b46e-222">Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="9b46e-222">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="9b46e-223">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9b46e-223">Congratulations!</span></span> <span data-ttu-id="9b46e-224">Vous avez interrogé une collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9b46e-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="9b46e-225">Hello diagramme suivant illustre la requête SQL de base de données Azure Cosmos de hello syntaxe est appelée sur la collection de hello créée et hello même logique s’applique également les requêtes LINQ toohello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-225">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagramme illustrant la portée de hello et la signification de la requête de hello utilisé par toocreate de didacticiel hello NoSQL, une application console c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="9b46e-227">Hello [FROM](documentdb-sql-query.md#FromClause) mot clé est facultatif dans la requête de hello, car les requêtes de base de données Azure Cosmos sont déjà incluses dans l’étendue tooa unique collection.</span><span class="sxs-lookup"><span data-stu-id="9b46e-227">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="9b46e-228">Par conséquent, « FROM Families f » peut être remplacé par «FROM root r » ou par tout autre nom de variable que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="9b46e-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="9b46e-229">DocumentDB déduira familles, racine ou le nom de la variable hello choisie, référence hello de collection actuel par défaut.</span><span class="sxs-lookup"><span data-stu-id="9b46e-229">DocumentDB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="9b46e-230"><a id="ReplaceDocument"></a>Étape 8 : remplacer le document JSON</span><span class="sxs-lookup"><span data-stu-id="9b46e-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="9b46e-231">Azure Cosmos DB prend en charge le remplacement des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="9b46e-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="9b46e-232">Copiez et collez hello **ReplaceFamilyDocument** méthode sous votre **ExecuteSimpleQuery** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9b46e-232">Copy and paste hello **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="9b46e-233">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode en dessous de l’exécution des requêtes hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-233">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello query execution.</span></span> <span data-ttu-id="9b46e-234">Après le remplacement de document de hello, hello s’exécute même interroger à nouveau tooview hello modifié document.</span><span class="sxs-lookup"><span data-stu-id="9b46e-234">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="9b46e-235">Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="9b46e-235">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="9b46e-236">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9b46e-236">Congratulations!</span></span> <span data-ttu-id="9b46e-237">Vous avez remplacé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9b46e-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="9b46e-238"><a id="DeleteDocument"></a>Étape 9 : supprimer le document JSON</span><span class="sxs-lookup"><span data-stu-id="9b46e-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="9b46e-239">Azure Cosmos DB prend en charge la suppression des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="9b46e-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="9b46e-240">Copiez et collez hello **DeleteFamilyDocument** méthode sous votre **ReplaceFamilyDocument** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9b46e-240">Copy and paste hello **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="9b46e-241">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode en dessous de l’exécution de la deuxième requête hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-241">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="9b46e-242">Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="9b46e-242">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="9b46e-243">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9b46e-243">Congratulations!</span></span> <span data-ttu-id="9b46e-244">Vous avez supprimé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9b46e-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="9b46e-245"><a id="DeleteDatabase"></a>Étape 10 : Supprimer la base de données hello</span><span class="sxs-lookup"><span data-stu-id="9b46e-245"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="9b46e-246">Suppression hello créé la base de données supprime de la base de données hello et toutes les ressources enfants (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="9b46e-246">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="9b46e-247">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode sous le document de hello supprimer toute base de données toodelete hello et toutes les ressources enfants.</span><span class="sxs-lookup"><span data-stu-id="9b46e-247">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello document delete toodelete hello entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="9b46e-248">Hello de presse **DocumentDBGettingStarted** bouton toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="9b46e-248">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="9b46e-249">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9b46e-249">Congratulations!</span></span> <span data-ttu-id="9b46e-250">Vous avez supprimé une base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9b46e-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="9b46e-251"><a id="Run"></a>Étape 11 : exécuter votre application de console C#</span><span class="sxs-lookup"><span data-stu-id="9b46e-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="9b46e-252">Hello de presse **DocumentDBGettingStarted** bouton dans Visual Studio toobuild hello application en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="9b46e-252">Press hello **DocumentDBGettingStarted** button in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="9b46e-253">Vous devez voir la sortie hello de votre application démarrée get dans la fenêtre de console hello.</span><span class="sxs-lookup"><span data-stu-id="9b46e-253">You should see hello output of your get started app in hello console window.</span></span> <span data-ttu-id="9b46e-254">sortie de Hello affiche les résultats de hello Hello requêtes, nous avons ajouté et doit correspondre au texte d’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9b46e-254">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
Press any key toocontinue ...
Created Family Andersen.1
Press any key toocontinue ...
Created Family Wakefield.7
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Replaced Family Andersen.1
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Deleted Family Andersen.1
End of demo, press any key tooexit.
```

<span data-ttu-id="9b46e-255">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9b46e-255">Congratulations!</span></span> <span data-ttu-id="9b46e-256">Vous avez terminé le didacticiel de hello et que vous avez une application de console c# de travail !</span><span class="sxs-lookup"><span data-stu-id="9b46e-256">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="9b46e-257"><a id="GetSolution"></a>Obtenir la solution du didacticiel complet hello</span><span class="sxs-lookup"><span data-stu-id="9b46e-257"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="9b46e-258">toobuild hello GetStarted solution qui contient tous les exemples hello dans cet article vous serez hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="9b46e-258">toobuild hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="9b46e-259">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="9b46e-259">An active Azure account.</span></span> <span data-ttu-id="9b46e-260">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9b46e-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="9b46e-261">Un [compte Azure Cosmos DB][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="9b46e-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="9b46e-262">Hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="9b46e-262">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="9b46e-263">toorestore hello références toohello API DocumentDB Azure Cosmos DB Core du SDK pour .NET dans Visual Studio, avec le bouton droit hello **GetStarted** solution dans l’Explorateur de solutions, puis cliquez sur **activer la restauration des packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9b46e-263">toorestore hello references toohello DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="9b46e-264">Ensuite, dans le fichier Program.cs de hello, mettre à jour les valeurs EndpointUrl et AuthorizationKey hello comme décrit dans [connecter compte de base de données Azure Cosmos tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="9b46e-264">Next, in hello Program.cs file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b46e-265">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b46e-265">Next steps</span></span>
* <span data-ttu-id="9b46e-266">Vous voulez un didacticiel ASP.NET MVC plus complexe ?</span><span class="sxs-lookup"><span data-stu-id="9b46e-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="9b46e-267">Reportez-vous à la page [Didacticiel ASP.NET MVC : développement d’applications web avec Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="9b46e-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="9b46e-268">Voulez toodevelop un Xamarin iOS, Android ou des formulaires à l’aide de l’application hello API DocumentDB pour le Kit de développement logiciel Azure Cosmos DB .NET Core ?</span><span class="sxs-lookup"><span data-stu-id="9b46e-268">Want toodevelop a Xamarin iOS, Android, or Forms application using hello DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="9b46e-269">Consultez la page [Créer des applications mobiles avec Xamarin et Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="9b46e-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="9b46e-270">Vous souhaitez tooperform mise à l’échelle et des tests de performances avec la base de données Azure Cosmos ?</span><span class="sxs-lookup"><span data-stu-id="9b46e-270">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="9b46e-271">Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="9b46e-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="9b46e-272">Découvrez comment trop[demandes analyse Azure Cosmos DB, l’utilisation et stockage](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="9b46e-272">Learn how too[Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="9b46e-273">Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="9b46e-273">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="9b46e-274">toolearn en savoir plus sur le modèle de programmation hello, consultez [base de données Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="9b46e-274">toolearn more about hello programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
