---
title: "Azure Cosmos DB : Didacticiel sur la prise en main de l’API DocumentDB | Microsoft Docs"
description: "Un didacticiel qui crée une base de données en ligne et une application console c# à l’aide de hello API DocumentDB."
keywords: "didacticiel nosql, base de données en ligne, application console c#"
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="89e71-104">Azure Cosmos DB : Didacticiel sur la prise en main de l’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="89e71-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89e71-105">.NET</span><span class="sxs-lookup"><span data-stu-id="89e71-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="89e71-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="89e71-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="89e71-107">Node.js pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="89e71-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="89e71-108">Node.JS</span><span class="sxs-lookup"><span data-stu-id="89e71-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="89e71-109">Java</span><span class="sxs-lookup"><span data-stu-id="89e71-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="89e71-110">C++</span><span class="sxs-lookup"><span data-stu-id="89e71-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="89e71-111">Bienvenue toohello API de DocumentDB de base de données Azure Cosmos route !</span><span class="sxs-lookup"><span data-stu-id="89e71-111">Welcome toohello Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="89e71-112">À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e71-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="89e71-113">Nous allons aborder les points suivants :</span><span class="sxs-lookup"><span data-stu-id="89e71-113">We'll cover:</span></span>

* <span data-ttu-id="89e71-114">Création et connexion de compte de base de données Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="89e71-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="89e71-115">Configuration de votre solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89e71-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="89e71-116">Création d’une base de données en ligne</span><span class="sxs-lookup"><span data-stu-id="89e71-116">Creating an online database</span></span>
* <span data-ttu-id="89e71-117">Création d’une collection</span><span class="sxs-lookup"><span data-stu-id="89e71-117">Creating a collection</span></span>
* <span data-ttu-id="89e71-118">Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="89e71-118">Creating JSON documents</span></span>
* <span data-ttu-id="89e71-119">Interrogation de collection de hello</span><span class="sxs-lookup"><span data-stu-id="89e71-119">Querying hello collection</span></span>
* <span data-ttu-id="89e71-120">Remplacement d'un document</span><span class="sxs-lookup"><span data-stu-id="89e71-120">Replacing a document</span></span>
* <span data-ttu-id="89e71-121">Suppression d’un document</span><span class="sxs-lookup"><span data-stu-id="89e71-121">Deleting a document</span></span>
* <span data-ttu-id="89e71-122">Suppression de la base de données hello</span><span class="sxs-lookup"><span data-stu-id="89e71-122">Deleting hello database</span></span>

<span data-ttu-id="89e71-123">Vous n’avez pas le temps ?</span><span class="sxs-lookup"><span data-stu-id="89e71-123">Don't have time?</span></span> <span data-ttu-id="89e71-124">Ne vous inquiétez pas !</span><span class="sxs-lookup"><span data-stu-id="89e71-124">Don't worry!</span></span> <span data-ttu-id="89e71-125">solution complète de Hello est disponible sur [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="89e71-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="89e71-126">Raccourcis toohello [obtenir la section de solution du didacticiel hello complète NoSQL](#GetSolution) pour obtenir des instructions rapides.</span><span class="sxs-lookup"><span data-stu-id="89e71-126">Jump toohello [Get hello complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="89e71-127">Par la suite, veuillez utiliser hello des boutons de vote haut de hello ou du bas de cette page de toogive nous vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="89e71-127">Afterwards, please use hello voting buttons at hello top or bottom of this page toogive us feedback.</span></span> <span data-ttu-id="89e71-128">Si vous souhaitez que nous toocontact vous directement, vous pouvez tooinclude libre votre adresse de messagerie dans vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="89e71-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="89e71-129">Commençons dès maintenant !</span><span class="sxs-lookup"><span data-stu-id="89e71-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89e71-130">Composants requis</span><span class="sxs-lookup"><span data-stu-id="89e71-130">Prerequisites</span></span>
<span data-ttu-id="89e71-131">Vérifiez que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="89e71-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="89e71-132">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="89e71-132">An active Azure account.</span></span> <span data-ttu-id="89e71-133">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="89e71-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="89e71-134">Vous pouvez également utiliser hello [Azure Cosmos DB émulateur](local-emulator.md) pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="89e71-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="89e71-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="89e71-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="89e71-136">Étape 1 : créer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="89e71-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="89e71-137">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e71-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="89e71-138">Si vous avez déjà un compte que vous souhaitez toouse, vous pouvez passer trop[le programme d’installation de votre Solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="89e71-138">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="89e71-139">Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[le programme d’installation de votre Solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="89e71-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="89e71-140"><a id="SetupVS"></a>Étape 2 : configurer votre solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89e71-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="89e71-141">Ouvrez **Visual Studio 2017** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="89e71-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="89e71-142">Sur hello **fichier** menu, sélectionnez **nouveau**, puis choisissez **projet**.</span><span class="sxs-lookup"><span data-stu-id="89e71-142">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="89e71-143">Bonjour **nouveau projet** boîte de dialogue, sélectionnez **modèles** / **Visual C#** / **Application Console**, nom votre projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89e71-143">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="89e71-144">![Capture d’écran de la fenêtre de nouveau projet hello](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="89e71-144">![Screen shot of hello New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="89e71-145">Bonjour **l’Explorateur de solutions**, cliquez avec le bouton droit sur votre nouvelle application console qui se trouve sous votre solution Visual Studio, et puis cliquez sur **gérer les Packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="89e71-145">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Capture d’écran de hello droite Menu Clicked hello projet](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="89e71-147">Bonjour **Nuget** , cliquez sur **Parcourir**et le type **azure documentdb** dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="89e71-147">In hello **Nuget** tab, click **Browse**, and type **azure documentdb** in hello search box.</span></span>
6. <span data-ttu-id="89e71-148">Dans les résultats de hello, recherchez **Microsoft.Azure.DocumentDB** et cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="89e71-148">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="89e71-149">ID de package Hello pour hello Azure Cosmos DB DocumentDB API Client Library est [bibliothèque cliente de Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="89e71-149">hello package ID for hello Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="89e71-150">![Capture d’écran de hello Menu de Nuget pour la recherche de base de données Client SDK Azure Cosmos](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="89e71-150">![Screen shot of hello Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="89e71-151">Si vous obtenez un message sur la vérification des modifications toohello solution, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89e71-151">If you get a messages about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="89e71-152">Si vous obtenez un message concernant l’acceptation de la licence, cliquez sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="89e71-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="89e71-153">Parfait !</span><span class="sxs-lookup"><span data-stu-id="89e71-153">Great!</span></span> <span data-ttu-id="89e71-154">Maintenant que nous avons terminé le programme d’installation Bonjour, nous pouvons commencer l’écriture du code.</span><span class="sxs-lookup"><span data-stu-id="89e71-154">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="89e71-155">Vous trouverez le projet de code complet de ce didacticiel dans [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="89e71-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="89e71-156"><a id="Connect"></a>Étape 3 : Relier le compte de base de données Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="89e71-156"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="89e71-157">Tout d’abord, ajoutez ces références début toohello de votre application c#, dans le fichier Program.cs de hello :</span><span class="sxs-lookup"><span data-stu-id="89e71-157">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="89e71-158">Dans le didacticiel de commande toocomplete hello, assurez-vous que vous ajoutez des dépendances hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="89e71-158">In order toocomplete hello tutorial, make sure you add hello dependencies above.</span></span>
> 
> 

<span data-ttu-id="89e71-159">Maintenant, ajoutez ces deux constantes et votre variable *client* dans votre classe publique *Program*.</span><span class="sxs-lookup"><span data-stu-id="89e71-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="89e71-160">Ensuite, head sauvegarde toohello [Azure Portal](https://portal.azure.com) tooretrieve votre URL de point de terminaison et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="89e71-160">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="89e71-161">URL de point de terminaison Hello et la clé primaire sont nécessaires pour votre application toounderstand où tooconnect et de base de données Azure Cosmos tootrust connexion de votre application.</span><span class="sxs-lookup"><span data-stu-id="89e71-161">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="89e71-162">Dans hello portail Azure, accédez de compte de base de données Azure Cosmos tooyour, puis cliquez sur **clés**.</span><span class="sxs-lookup"><span data-stu-id="89e71-162">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="89e71-163">Copiez hello URI à partir du portail de hello, puis collez-la dans `<your endpoint URL>` dans le fichier program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="89e71-163">Copy hello URI from hello portal and paste it into `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="89e71-164">Copie hello clé primaire à partir du portail de hello et collez-la dans `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="89e71-164">Then copy hello PRIMARY KEY from hello portal and paste it into `<your primary key>`.</span></span>

![Capture d’écran de hello portail Azure utilisée par hello toocreate de didacticiel NoSQL une application console c#.][keys]

<span data-ttu-id="89e71-167">Ensuite, nous allons commencer application hello en créant une nouvelle instance de hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="89e71-167">Next, we'll start hello application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="89e71-168">Ci-dessous hello **principal** méthode, ajoutez cette nouvelle tâche asynchrone appelée **GetStartedDemo**, qui instancie notre nouveau **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="89e71-168">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="89e71-169">Ajouter le code suivant de hello toorun votre tâche asynchrone à partir de votre **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="89e71-169">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="89e71-170">Hello **Main** méthode intercepter les exceptions et les écrire toohello console.</span><span class="sxs-lookup"><span data-stu-id="89e71-170">hello **Main** method will catch exceptions and write them toohello console.</span></span>

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

<span data-ttu-id="89e71-171">Appuyez sur **F5** toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="89e71-171">Press **F5** toorun your application.</span></span> <span data-ttu-id="89e71-172">sortie de la fenêtre console Hello affiche le message de type hello `End of demo, press any key tooexit.` confirmant que la connexion de hello a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="89e71-172">hello console window output displays hello message `End of demo, press any key tooexit.` confirming that hello connection was made.</span></span>  <span data-ttu-id="89e71-173">Vous pouvez ensuite fermer la fenêtre de console hello.</span><span class="sxs-lookup"><span data-stu-id="89e71-173">You can then close hello console window.</span></span> 

<span data-ttu-id="89e71-174">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="89e71-174">Congratulations!</span></span> <span data-ttu-id="89e71-175">Vous avez correctement connecté le compte de base de données Azure Cosmos tooan, maintenant examinons une utilisation des ressources de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="89e71-175">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="89e71-176">Étape 4 : créer une base de données</span><span class="sxs-lookup"><span data-stu-id="89e71-176">Step 4: Create a database</span></span>
<span data-ttu-id="89e71-177">Avant d’ajouter de code hello pour la création d’une base de données, ajoutez une méthode d’assistance pour l’écriture de toohello console.</span><span class="sxs-lookup"><span data-stu-id="89e71-177">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="89e71-178">Copiez et collez hello **WriteToConsoleAndPromptToContinue** méthode après hello **GetStartedDemo** (méthode).</span><span class="sxs-lookup"><span data-stu-id="89e71-178">Copy and paste hello **WriteToConsoleAndPromptToContinue** method after hello **GetStartedDemo** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="89e71-179">Votre base de données Azure Cosmos [base de données](documentdb-resources.md#databases) peuvent être créés à l’aide de hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) méthode Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="89e71-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="89e71-180">Une base de données est un conteneur logique de hello JSON de stockage de documents partitionné entre des collections.</span><span class="sxs-lookup"><span data-stu-id="89e71-180">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="89e71-181">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après la création du client hello.</span><span class="sxs-lookup"><span data-stu-id="89e71-181">Copy and paste hello following code tooyour **GetStartedDemo** method after hello client creation.</span></span> <span data-ttu-id="89e71-182">Ce faisant, vous créez la base de données *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="89e71-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="89e71-183">Appuyez sur **F5** toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="89e71-183">Press **F5** toorun your application.</span></span>

<span data-ttu-id="89e71-184">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="89e71-184">Congratulations!</span></span> <span data-ttu-id="89e71-185">Vous avez créé une base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e71-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="89e71-186"><a id="CreateColl"></a>Étape 5 : créer une collection</span><span class="sxs-lookup"><span data-stu-id="89e71-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="89e71-187">**CreateDocumentCollectionIfNotExistsAsync** crée une collection avec un débit réservé, ce qui a des conséquences sur la tarification.</span><span class="sxs-lookup"><span data-stu-id="89e71-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="89e71-188">Pour plus d'informations, visitez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="89e71-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="89e71-189">A [collection](documentdb-resources.md#collections) peuvent être créés à l’aide de hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) méthode Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="89e71-189">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="89e71-190">Une collection est un conteneur de documents JSON. Elle est associée à une logique d'application JavaScript.</span><span class="sxs-lookup"><span data-stu-id="89e71-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="89e71-191">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après la création de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="89e71-191">Copy and paste hello following code tooyour **GetStartedDemo** method after hello database creation.</span></span> <span data-ttu-id="89e71-192">Ce faisant, vous créez la collection de documents *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="89e71-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="89e71-193">Appuyez sur **F5** toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="89e71-193">Press **F5** toorun your application.</span></span>

<span data-ttu-id="89e71-194">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="89e71-194">Congratulations!</span></span> <span data-ttu-id="89e71-195">Vous avez créé une collection de documents Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e71-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="89e71-196"><a id="CreateDoc"></a>Étape 6 : Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="89e71-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="89e71-197">A [document](documentdb-resources.md#documents) peuvent être créés à l’aide de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) méthode Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="89e71-197">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="89e71-198">Les documents correspondent à du contenu JSON (arbitraire) défini par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="89e71-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="89e71-199">Nous pouvons maintenant insérer un ou plusieurs documents.</span><span class="sxs-lookup"><span data-stu-id="89e71-199">We can now insert one or more documents.</span></span> <span data-ttu-id="89e71-200">Si vous avez déjà des données que vous souhaitez toostore dans votre base de données, vous pouvez utiliser hello Azure Cosmos DB [l’outil de Migration de données](import-data.md) tooimport les données de salutation dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="89e71-200">If you already have data you'd like toostore in your database, you can use hello Azure Cosmos DB [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

<span data-ttu-id="89e71-201">Tout d’abord, nous devons toocreate un **famille** classe représentant des objets stockés dans la base de données Azure Cosmos dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="89e71-201">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="89e71-202">Nous allons également créer les sous-classes **Parent**, **Child**, **Pet** et **Address** qui seront utilisées dans **Family**.</span><span class="sxs-lookup"><span data-stu-id="89e71-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="89e71-203">Notez que les documents doivent avoir une propriété **Id** sérialisée comme **id** dans JSON.</span><span class="sxs-lookup"><span data-stu-id="89e71-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="89e71-204">Créer ces classes en ajoutant hello suivant sous-classes internes après hello **GetStartedDemo** (méthode).</span><span class="sxs-lookup"><span data-stu-id="89e71-204">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="89e71-205">Copiez et collez hello **famille**, **Parent**, **enfant**, **animal de compagnie**, et **adresse** classes après hello **WriteToConsoleAndPromptToContinue** (méthode).</span><span class="sxs-lookup"><span data-stu-id="89e71-205">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after hello **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="89e71-206">Copiez et collez hello **CreateFamilyDocumentIfNotExists** méthode sous votre **adresse** classe.</span><span class="sxs-lookup"><span data-stu-id="89e71-206">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

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

<span data-ttu-id="89e71-207">Et insérez les deux documents, un pour chacun des hello Andersen famille et hello Wakefield famille.</span><span class="sxs-lookup"><span data-stu-id="89e71-207">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="89e71-208">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après la création de la collection de document hello.</span><span class="sxs-lookup"><span data-stu-id="89e71-208">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

<span data-ttu-id="89e71-209">Appuyez sur **F5** toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="89e71-209">Press **F5** toorun your application.</span></span>

<span data-ttu-id="89e71-210">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="89e71-210">Congratulations!</span></span> <span data-ttu-id="89e71-211">Vous avez créé deux documents Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e71-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagramme illustrant relation hiérarchique hello entre le compte de hello, base de données en ligne hello, la collection de hello et documents hello utilisés par hello toocreate de didacticiel NoSQL une application console c#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="89e71-213"><a id="Query"></a>Étape 7 : interroger les ressources Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="89e71-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="89e71-214">Azure Cosmos DB prend en charge les [requêtes](documentdb-sql-query.md) enrichies sur les documents JSON stockés dans chaque collection.</span><span class="sxs-lookup"><span data-stu-id="89e71-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="89e71-215">Hello exemple de code suivant montre différentes requêtes - à l’aide de la base de données SQL Azure Cosmos syntaxe ainsi que LINQ - ce que nous pouvons exécuter par rapport aux documents que nous insérés à l’étape précédente de hello hello.</span><span class="sxs-lookup"><span data-stu-id="89e71-215">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="89e71-216">Copiez et collez hello **ExecuteSimpleQuery** méthode après votre **CreateFamilyDocumentIfNotExists** (méthode).</span><span class="sxs-lookup"><span data-stu-id="89e71-216">Copy and paste hello **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="89e71-217">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après la création d’un deuxième document hello.</span><span class="sxs-lookup"><span data-stu-id="89e71-217">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="89e71-218">Appuyez sur **F5** toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="89e71-218">Press **F5** toorun your application.</span></span>

<span data-ttu-id="89e71-219">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="89e71-219">Congratulations!</span></span> <span data-ttu-id="89e71-220">Vous avez interrogé une collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e71-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="89e71-221">Hello diagramme suivant illustre la requête SQL de base de données Azure Cosmos de hello syntaxe est appelée sur la collection de hello créée et hello même logique s’applique également les requêtes LINQ toohello.</span><span class="sxs-lookup"><span data-stu-id="89e71-221">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagramme illustrant la portée de hello et la signification de la requête de hello utilisé par toocreate de didacticiel hello NoSQL, une application console c#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="89e71-223">Hello [FROM](documentdb-sql-query.md#FromClause) mot clé est facultatif dans la requête de hello, car les requêtes de base de données Azure Cosmos sont déjà incluses dans l’étendue tooa unique collection.</span><span class="sxs-lookup"><span data-stu-id="89e71-223">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="89e71-224">Par conséquent, « FROM Families f » peut être remplacé par «FROM root r » ou par tout autre nom de variable que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="89e71-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="89e71-225">Base de données Azure Cosmos déduira familles, racine ou le nom de la variable hello choisie, référence hello de collection actuel par défaut.</span><span class="sxs-lookup"><span data-stu-id="89e71-225">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="89e71-226"><a id="ReplaceDocument"></a>Étape 8 : remplacer le document JSON</span><span class="sxs-lookup"><span data-stu-id="89e71-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="89e71-227">Azure Cosmos DB prend en charge le remplacement des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="89e71-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="89e71-228">Copiez et collez hello **ReplaceFamilyDocument** méthode après votre **ExecuteSimpleQuery** (méthode).</span><span class="sxs-lookup"><span data-stu-id="89e71-228">Copy and paste hello **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="89e71-229">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après l’exécution de requête hello, à fin hello de méthode hello.</span><span class="sxs-lookup"><span data-stu-id="89e71-229">Copy and paste hello following code tooyour **GetStartedDemo** method after hello query execution, at hello end of hello method.</span></span> <span data-ttu-id="89e71-230">Après le remplacement de document de hello, hello s’exécute même interroger à nouveau tooview hello modifié document.</span><span class="sxs-lookup"><span data-stu-id="89e71-230">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="89e71-231">Appuyez sur **F5** toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="89e71-231">Press **F5** toorun your application.</span></span>

<span data-ttu-id="89e71-232">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="89e71-232">Congratulations!</span></span> <span data-ttu-id="89e71-233">Vous avez remplacé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e71-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="89e71-234"><a id="DeleteDocument"></a>Étape 9 : supprimer le document JSON</span><span class="sxs-lookup"><span data-stu-id="89e71-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="89e71-235">Azure Cosmos DB prend en charge la suppression des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="89e71-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="89e71-236">Copiez et collez hello **DeleteFamilyDocument** méthode après votre **ReplaceFamilyDocument** (méthode).</span><span class="sxs-lookup"><span data-stu-id="89e71-236">Copy and paste hello **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="89e71-237">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après hello deuxième exécution de la requête à fin hello de méthode hello.</span><span class="sxs-lookup"><span data-stu-id="89e71-237">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second query execution, at hello end of hello method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="89e71-238">Appuyez sur **F5** toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="89e71-238">Press **F5** toorun your application.</span></span>

<span data-ttu-id="89e71-239">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="89e71-239">Congratulations!</span></span> <span data-ttu-id="89e71-240">Vous avez supprimé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e71-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="89e71-241"><a id="DeleteDatabase"></a>Étape 10 : Supprimer la base de données hello</span><span class="sxs-lookup"><span data-stu-id="89e71-241"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="89e71-242">Suppression hello créé la base de données supprime de la base de données hello et toutes les ressources enfants (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="89e71-242">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="89e71-243">Copie et suit hello de coller du code tooyour **GetStartedDemo** méthode après le document de hello supprimer la base de données entière toodelete hello et toutes les ressources enfants.</span><span class="sxs-lookup"><span data-stu-id="89e71-243">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document delete toodelete hello entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="89e71-244">Appuyez sur **F5** toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="89e71-244">Press **F5** toorun your application.</span></span>

<span data-ttu-id="89e71-245">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="89e71-245">Congratulations!</span></span> <span data-ttu-id="89e71-246">Vous avez supprimé une base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e71-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="89e71-247"><a id="Run"></a>Étape 11 : exécuter votre application de console C#</span><span class="sxs-lookup"><span data-stu-id="89e71-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="89e71-248">Dans l’application de hello toobuild Visual Studio en mode débogage, appuyez sur F5.</span><span class="sxs-lookup"><span data-stu-id="89e71-248">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="89e71-249">Vous devez voir la sortie hello de votre application démarrée get dans une fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="89e71-249">You should see hello output of your get started app in a console window.</span></span> <span data-ttu-id="89e71-250">sortie de Hello affiche les résultats de hello Hello requêtes, nous avons ajouté et doit correspondre au texte d’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="89e71-250">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
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

<span data-ttu-id="89e71-251">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="89e71-251">Congratulations!</span></span> <span data-ttu-id="89e71-252">Vous avez terminé le didacticiel de hello et que vous avez une application de console c# de travail !</span><span class="sxs-lookup"><span data-stu-id="89e71-252">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="89e71-253"><a id="GetSolution"></a>Obtenir la solution du didacticiel complet hello</span><span class="sxs-lookup"><span data-stu-id="89e71-253"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="89e71-254">Si vous n’avez pas ont toocomplete hello dans ce didacticiel, ou simplement que vous souhaitez toodownload hello exemples de code pour les étapes, vous pouvez l’obtenir à partir de [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="89e71-254">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="89e71-255">solution de GetStarted toobuild hello, vous devrez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="89e71-255">toobuild hello GetStarted solution, you will need hello following:</span></span>

* <span data-ttu-id="89e71-256">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="89e71-256">An active Azure account.</span></span> <span data-ttu-id="89e71-257">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="89e71-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="89e71-258">Un [compte Azure Cosmos DB][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="89e71-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="89e71-259">Hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="89e71-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="89e71-260">toorestore hello références toohello Azure Cosmos DB .NET SDK dans Visual Studio, avec le bouton droit hello **GetStarted** solution dans l’Explorateur de solutions, puis cliquez sur **activer la restauration des packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="89e71-260">toorestore hello references toohello Azure Cosmos DB .NET SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="89e71-261">Ensuite, dans le fichier App.config hello, mettre à jour les valeurs EndpointUrl et AuthorizationKey hello comme décrit dans [connecter compte de base de données Azure Cosmos tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="89e71-261">Next, in hello App.config file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="89e71-262">Voilà, vous n’avez plus qu’à générer l’élément pour être sur la bonne voie !</span><span class="sxs-lookup"><span data-stu-id="89e71-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="89e71-263">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89e71-263">Next steps</span></span>
* <span data-ttu-id="89e71-264">Vous voulez un didacticiel ASP.NET MVC plus complexe ?</span><span class="sxs-lookup"><span data-stu-id="89e71-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="89e71-265">Reportez-vous à la page [Didacticiel ASP.NET MVC : développement d’applications web avec Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="89e71-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="89e71-266">Vous souhaitez tooperform mise à l’échelle et des tests de performances avec la base de données Azure Cosmos ?</span><span class="sxs-lookup"><span data-stu-id="89e71-266">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="89e71-267">Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="89e71-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="89e71-268">Découvrez comment trop[surveiller les demandes, l’utilisation et le stockage Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="89e71-268">Learn how too[monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="89e71-269">Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="89e71-269">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="89e71-270">toolearn savoir plus sur la base de données Azure Cosmos, consultez [Bienvenue tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="89e71-270">toolearn more about Azure Cosmos DB, see [Welcome tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
