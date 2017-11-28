---
title: "aaaC ++ didacticiel de base de données Azure Cosmos | Documents Microsoft"
description: "Un didacticiel C++ qui crée une application de console et de base de données C++ à l’aide d’un kit de développement logiciel (SDK) approuvé par Azure Cosmos DB pour C++. Azure Cosmos DB est un service de base de données à l’échelle de la planète."
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a><span data-ttu-id="cf8dc-104">Cosmos Azure DB : Didacticiel d’application console C++ pour hello API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="cf8dc-104">Azure Cosmos DB: C++ console application tutorial for hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf8dc-105">.NET</span><span class="sxs-lookup"><span data-stu-id="cf8dc-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="cf8dc-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="cf8dc-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="cf8dc-107">Node.js pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="cf8dc-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="cf8dc-108">Node.JS</span><span class="sxs-lookup"><span data-stu-id="cf8dc-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="cf8dc-109">Java</span><span class="sxs-lookup"><span data-stu-id="cf8dc-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="cf8dc-110">C++</span><span class="sxs-lookup"><span data-stu-id="cf8dc-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="cf8dc-111">Didacticiel de C++ toohello Bienvenue pour hello Azure Cosmos DB DocumentDB API visé SDK pour C++ !</span><span class="sxs-lookup"><span data-stu-id="cf8dc-111">Welcome toohello C++ tutorial for hello Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="cf8dc-112">À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB, y compris une base de données C++.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="cf8dc-113">Nous allons aborder les points suivants :</span><span class="sxs-lookup"><span data-stu-id="cf8dc-113">We'll cover:</span></span>

* <span data-ttu-id="cf8dc-114">Création et connexion de compte de base de données Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="cf8dc-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="cf8dc-115">Configuration de votre application</span><span class="sxs-lookup"><span data-stu-id="cf8dc-115">Setting up your application</span></span>
* <span data-ttu-id="cf8dc-116">Création d’une base de données Azure Cosmos DB C++</span><span class="sxs-lookup"><span data-stu-id="cf8dc-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="cf8dc-117">Création d’une collection</span><span class="sxs-lookup"><span data-stu-id="cf8dc-117">Creating a collection</span></span>
* <span data-ttu-id="cf8dc-118">Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="cf8dc-118">Creating JSON documents</span></span>
* <span data-ttu-id="cf8dc-119">Interrogation de collection de hello</span><span class="sxs-lookup"><span data-stu-id="cf8dc-119">Querying hello collection</span></span>
* <span data-ttu-id="cf8dc-120">Remplacement d'un document</span><span class="sxs-lookup"><span data-stu-id="cf8dc-120">Replacing a document</span></span>
* <span data-ttu-id="cf8dc-121">Suppression d’un document</span><span class="sxs-lookup"><span data-stu-id="cf8dc-121">Deleting a document</span></span>
* <span data-ttu-id="cf8dc-122">Suppression de base de données de la base de données C++ Azure Cosmos hello</span><span class="sxs-lookup"><span data-stu-id="cf8dc-122">Deleting hello C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="cf8dc-123">Vous n’avez pas le temps ?</span><span class="sxs-lookup"><span data-stu-id="cf8dc-123">Don't have time?</span></span> <span data-ttu-id="cf8dc-124">Ne vous inquiétez pas !</span><span class="sxs-lookup"><span data-stu-id="cf8dc-124">Don't worry!</span></span> <span data-ttu-id="cf8dc-125">solution complète de Hello est disponible sur [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="cf8dc-125">hello complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="cf8dc-126">Consultez [obtenir la solution complète de hello](#GetSolution) pour obtenir des instructions rapides.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="cf8dc-127">Une fois que vous avez terminé le didacticiel de C++ hello, veuillez utiliser hello des boutons de vote bas hello toogive de cette page nous vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-127">After you've completed hello C++ tutorial, please use hello voting buttons at hello bottom of this page toogive us feedback.</span></span> 

<span data-ttu-id="cf8dc-128">Si vous souhaitez que nous toocontact vous directement, vous pouvez tooinclude libre votre adresse de messagerie dans vos commentaires ou [atteindre ici toous](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="cf8dc-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments or [reach out toous here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="cf8dc-129">Commençons dès maintenant !</span><span class="sxs-lookup"><span data-stu-id="cf8dc-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-c-tutorial"></a><span data-ttu-id="cf8dc-130">Configuration requise pour le didacticiel de hello C++</span><span class="sxs-lookup"><span data-stu-id="cf8dc-130">Prerequisites for hello C++ tutorial</span></span>
<span data-ttu-id="cf8dc-131">Vérifiez que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="cf8dc-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="cf8dc-132">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-132">An active Azure account.</span></span> <span data-ttu-id="cf8dc-133">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit des services Azure](https://azure.microsoft.com/pricing/free-trial/)dès aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cf8dc-134">[Visual Studio](https://www.visualstudio.com/downloads/), avec les composants de langage hello C++ installés.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-134">[Visual Studio](https://www.visualstudio.com/downloads/), with hello C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="cf8dc-135">Étape 1 : créer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cf8dc-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="cf8dc-136">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="cf8dc-137">Si vous avez déjà un compte que vous souhaitez toouse, vous pouvez passer trop[le programme d’installation de votre application C++](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="cf8dc-137">If you already have an account you want toouse, you can skip ahead too[Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="cf8dc-138"><a id="SetupC++"></a>Étape 2 : configurer votre application C++</span><span class="sxs-lookup"><span data-stu-id="cf8dc-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="cf8dc-139">Ouvrez Visual Studio, puis sous hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-139">Open Visual Studio, and then on hello **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="cf8dc-140">Bonjour **nouveau projet** fenêtre hello **installé** volet, développez **Visual C++**, cliquez sur **Win32**, puis cliquez sur  **Application Console Win32**.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-140">In hello **New Project** window, in hello **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="cf8dc-141">Nom hello projet hellodocumentdb, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-141">Name hello project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Capture d’écran de l’Assistant Nouveau projet d’hello](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="cf8dc-143">Démarrage de l’Assistant Application Win32 de hello, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-143">When hello Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="cf8dc-144">Une fois le projet de hello a été créé, ouvrez le Gestionnaire de package NuGet hello en double-cliquant sur hello **hellodocumentdb** projet **l’Explorateur de solutions** et en cliquant sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-144">Once hello project has been created, open hello NuGet package manager by right-clicking hello **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Capture d’écran de gérer le NuGet Package dans le menu de projet hello](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="cf8dc-146">Bonjour **NuGet : hellodocumentdb** , cliquez sur **Parcourir**, puis recherchez *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-146">In hello **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="cf8dc-147">Dans les résultats de hello, sélectionnez DocumentDbCPP, comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-147">In hello results, select DocumentDbCPP, as shown in hello following screenshot.</span></span> <span data-ttu-id="cf8dc-148">Ce package installe les références tooC ++ reste SDK, qui est une dépendance pour hello DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-148">This package installs references tooC++ REST SDK, which is a dependency for hello DocumentDbCPP.</span></span>  
   
    ![Package de DocumentDbCpp capture d’écran hello mis en surbrillance](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="cf8dc-150">Après ont ajouté les packages hello tooyour projet, nous sommes tous ensemble toostart écrire du code.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-150">Once hello packages have been added tooyour project, we are all set toostart writing some code.</span></span>   

## <span data-ttu-id="cf8dc-151"><a id="Config"></a>Étape 3 : copier les détails de la connexion à partir du portail Azure pour votre base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cf8dc-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="cf8dc-152">Afficher [portail Azure](https://portal.azure.com) et parcourir le compte de base de données de base de données Azure Cosmos toohello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-152">Bring up [Azure portal](https://portal.azure.com) and traverse toohello Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="cf8dc-153">Nous devons hello URI et la clé primaire de hello à partir du portail Azure dans hello prochaine étape tooestablish une connexion à partir de notre extrait de code C++.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-153">We will need hello URI and hello primary key from Azure portal in hello next step tooestablish a connection from our C++ code snippet.</span></span> 

![Azure Cosmos DB URI et les clés dans hello portail Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="cf8dc-155"><a id="Connect"></a>Étape 4 : Connexion de compte de base de données Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="cf8dc-155"><a id="Connect"></a>Step 4: Connect tooan Azure Cosmos DB account</span></span>
1. <span data-ttu-id="cf8dc-156">Ajouter hello après les en-têtes et les espaces de noms de code source tooyour, après `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-156">Add hello following headers and namespaces tooyour source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="cf8dc-157">Ajoutez ensuite hello code suivant tooyour main (fonction) et configuration de compte hello et toomatch de clé primaire vos paramètres de base de données Azure Cosmos à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-157">Next add hello following code tooyour main function and replace hello account configuration and primary key toomatch your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="cf8dc-158">Maintenant que vous possédez hello code tooinitialize hello documentdb client, examinons une utilisation des ressources de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-158">Now that you have hello code tooinitialize hello documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="cf8dc-159"><a id="CreateDBColl"></a>Étape 5 : créer une base de données C++ et une collection</span><span class="sxs-lookup"><span data-stu-id="cf8dc-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="cf8dc-160">Avant cette étape, nous allons interagissent entre une base de données, de collection et de documents pour ceux qui sont nouveaux tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new tooAzure Cosmos DB.</span></span> <span data-ttu-id="cf8dc-161">Une [base de données](documentdb-resources.md#databases) est un conteneur logique de stockage de documents réparti entre des collections.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="cf8dc-162">A [collection](documentdb-resources.md#collections) est un conteneur de documents JSON et hello logique d’application JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and hello associated JavaScript application logic.</span></span> <span data-ttu-id="cf8dc-163">Vous pouvez en savoir plus sur les concepts et le modèle de ressource hiérarchique de base de données Azure Cosmos hello [concepts et modèle de ressource hiérarchiques de base de données Azure Cosmos](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="cf8dc-163">You can learn more about hello Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="cf8dc-164">toocreate une base de données et la collection correspondante ajoutent hello suivant fin toohello de code de votre fonction principale.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-164">toocreate a database and a corresponding collection add hello following code toohello end of your main function.</span></span> <span data-ttu-id="cf8dc-165">Cette opération crée une base de données appelé « FamilyRegistry » et une collection appelée « FamilyCollection » à l’aide de la configuration du client hello déclarée à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using hello client configuration you declared in hello previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="cf8dc-166"><a id="CreateDoc"></a>Étape 6 : créer un document</span><span class="sxs-lookup"><span data-stu-id="cf8dc-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="cf8dc-167">Les [documents](documentdb-resources.md#documents) correspondent à du contenu JSON (arbitraire) défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="cf8dc-168">Vous pouvez maintenant insérer un document dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="cf8dc-169">Vous pouvez créer un document en copiant hello après le code en fin de Bonjour de main (fonction) hello.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-169">You can create a document by copying hello following code into hello end of hello main function.</span></span> 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

<span data-ttu-id="cf8dc-170">toosummarize, ce code crée une base de données de la base de données Azure Cosmos, la collection et les documents, vous pouvez rechercher dans l’Explorateur de documents dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-170">toosummarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Didacticiel C++ - diagramme illustrant la relation hiérarchique de hello entre le compte de hello, la base de données hello, collection de hello et documents de hello](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="cf8dc-172"><a id="QueryDB"></a>Étape 7 : interroger les ressources Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cf8dc-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="cf8dc-173">Azure Cosmos DB prend en charge les [requêtes enrichies](documentdb-sql-query.md) sur les documents JSON stockés dans chaque collection.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="cf8dc-174">Hello exemple de code suivant montre une requête effectuée à l’aide de la syntaxe SQL que vous pouvez exécuter par rapport aux documents de hello que nous créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-174">hello following sample code shows a query made using SQL syntax that you can run against hello documents we created in hello previous step.</span></span>

<span data-ttu-id="cf8dc-175">fonction de Hello utilise comme arguments hello identificateur unique ou l’id de ressource pour la base de données hello et collection hello en même temps que le client du document hello.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-175">hello function takes in as arguments hello unique identifier or resource id for hello database and hello collection along with hello document client.</span></span> <span data-ttu-id="cf8dc-176">Ajoutez ce code avant la fonction main.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-176">Add this code before main function.</span></span>

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="cf8dc-177"><a id="Replace"></a>Étape 8 : remplacer un document</span><span class="sxs-lookup"><span data-stu-id="cf8dc-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="cf8dc-178">Azure Cosmos DB prend en charge en remplaçant les documents JSON, comme illustré dans hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in hello following code.</span></span> <span data-ttu-id="cf8dc-179">Ajoutez ce code après la fonction d’executesimplequery hello.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-179">Add this code after hello executesimplequery function.</span></span>

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <span data-ttu-id="cf8dc-180"><a id="Delete"></a>Étape 9 : supprimer un document</span><span class="sxs-lookup"><span data-stu-id="cf8dc-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="cf8dc-181">Azure Cosmos DB prend en charge la suppression de documents JSON, vous pouvez le faire par copie et collage de hello après le code après la fonction de replacedocument hello.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting hello following code after hello replacedocument function.</span></span> 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="cf8dc-182"><a id="DeleteDB"></a>Étape 10 : supprimer une base de données</span><span class="sxs-lookup"><span data-stu-id="cf8dc-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="cf8dc-183">Base de données de suppression hello créé supprime de la base de données hello et toutes les ressources enfants (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="cf8dc-183">Deleting hello created database removes hello database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="cf8dc-184">Copiez et collez hello suivant extrait de code (nettoyage de la fonction) après la base de données hello deletedocument fonction tooremove hello et toutes les ressources enfants de hello.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-184">Copy and paste hello following code snippet (function cleanup) after hello deletedocument function tooremove hello database and all hello child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="cf8dc-185"><a id="Run"></a>Étape 11 : exécuter l’ensemble votre application C++ !</span><span class="sxs-lookup"><span data-stu-id="cf8dc-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="cf8dc-186">Nous avez maintenant ajouté le code toocreate, interroger, modifier et supprimer des ressources de base de données Azure Cosmos différents.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-186">We have now added code toocreate, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="cf8dc-187">Nous maintenant associer ce en ajoutant des appels des fonctions différentes toothese de notre fonction principale dans hellodocumentdb.cpp, ainsi que certains messages de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-187">Let us now wire this up by adding calls toothese different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="cf8dc-188">Vous pouvez le faire en remplaçant hello principale fonction de votre application avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-188">You can do so by replacing hello main function of your application with hello following code.</span></span> <span data-ttu-id="cf8dc-189">Cette écritures hello account_configuration_uri et primary_key que vous avez copié dans le code hello à l’étape 3, par conséquent, réenregistrez qui ligne ou la copie des valeurs hello dans à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-189">This writes over hello account_configuration_uri and primary_key you copied into hello code in Step 3, so save that line or copy hello values in again from hello portal.</span></span> 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

<span data-ttu-id="cf8dc-190">Vous devez maintenant être en mesure de toobuild et exécuter votre code dans Visual Studio en appuyant sur F5 ou également dans la fenêtre de terminal hello en recherchant des application hello et en cours d’exécution hello exécutable.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-190">You should now be able toobuild and run your code in Visual Studio by pressing F5 or alternatively in hello terminal window by locating hello application and running hello executable.</span></span> 

<span data-ttu-id="cf8dc-191">Vous devez voir la sortie hello de votre application démarrée get.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-191">You should see hello output of your get started app.</span></span> <span data-ttu-id="cf8dc-192">sortie de Hello doit correspondre au hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-192">hello output should match hello following screenshot.</span></span>

![Sortie de l’application Azure Cosmos DB C++](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="cf8dc-194">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="cf8dc-194">Congratulations!</span></span> <span data-ttu-id="cf8dc-195">Vous avez terminé hello C++ didacticiel et que vous avez votre première application de console de base de données Azure Cosmos !</span><span class="sxs-lookup"><span data-stu-id="cf8dc-195">You've completed hello C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="cf8dc-196"><a id="GetSolution"></a>Obtenir la solution didacticiel hello complète C++</span><span class="sxs-lookup"><span data-stu-id="cf8dc-196"><a id="GetSolution"></a>Get hello complete C++ tutorial solution</span></span>
<span data-ttu-id="cf8dc-197">toobuild hello GetStarted solution qui contient tous les exemples hello dans cet article hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="cf8dc-197">toobuild hello GetStarted solution that contains all hello samples in this article, you need hello following:</span></span>

* <span data-ttu-id="cf8dc-198">[Un compte Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="cf8dc-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="cf8dc-199">Hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="cf8dc-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf8dc-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cf8dc-200">Next steps</span></span>
* <span data-ttu-id="cf8dc-201">Découvrez comment trop[surveiller un compte de base de données Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="cf8dc-201">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="cf8dc-202">Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="cf8dc-202">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="cf8dc-203">En savoir plus sur le modèle de programmation hello Bonjour section développer Hello [page de documentation de base de données Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="cf8dc-203">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


