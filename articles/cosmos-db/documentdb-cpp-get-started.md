---
title: Didacticiel C++ pour Azure Cosmos DB | Microsoft Docs
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
ms.openlocfilehash: 7d8de973765830ccd7983182bc1bb19b1e01e505
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-the-documentdb-api"></a><span data-ttu-id="fff95-104">Azure Cosmos DB : Didacticiel d’application de console C++ pour l’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="fff95-104">Azure Cosmos DB: C++ console application tutorial for the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fff95-105">.NET</span><span class="sxs-lookup"><span data-stu-id="fff95-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="fff95-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="fff95-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="fff95-107">Node.js pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="fff95-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="fff95-108">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fff95-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="fff95-109">Java</span><span class="sxs-lookup"><span data-stu-id="fff95-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="fff95-110">C++</span><span class="sxs-lookup"><span data-stu-id="fff95-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="fff95-111">Bienvenue dans le didacticiel C++ pour le kit de développement logiciel (SDK) approuvé par l’API DocumentDB d’Azure Cosmos DB pour C++ !</span><span class="sxs-lookup"><span data-stu-id="fff95-111">Welcome to the C++ tutorial for the Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="fff95-112">À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB, y compris une base de données C++.</span><span class="sxs-lookup"><span data-stu-id="fff95-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="fff95-113">Nous allons aborder les points suivants :</span><span class="sxs-lookup"><span data-stu-id="fff95-113">We'll cover:</span></span>

* <span data-ttu-id="fff95-114">Création et connexion à un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fff95-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="fff95-115">Configuration de votre application</span><span class="sxs-lookup"><span data-stu-id="fff95-115">Setting up your application</span></span>
* <span data-ttu-id="fff95-116">Création d’une base de données Azure Cosmos DB C++</span><span class="sxs-lookup"><span data-stu-id="fff95-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="fff95-117">Création d’une collection</span><span class="sxs-lookup"><span data-stu-id="fff95-117">Creating a collection</span></span>
* <span data-ttu-id="fff95-118">Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="fff95-118">Creating JSON documents</span></span>
* <span data-ttu-id="fff95-119">Interrogation de la collection</span><span class="sxs-lookup"><span data-stu-id="fff95-119">Querying the collection</span></span>
* <span data-ttu-id="fff95-120">Remplacement d'un document</span><span class="sxs-lookup"><span data-stu-id="fff95-120">Replacing a document</span></span>
* <span data-ttu-id="fff95-121">Suppression d’un document</span><span class="sxs-lookup"><span data-stu-id="fff95-121">Deleting a document</span></span>
* <span data-ttu-id="fff95-122">Suppression d’une base de données Azure Cosmos DB C++</span><span class="sxs-lookup"><span data-stu-id="fff95-122">Deleting the C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="fff95-123">Vous n’avez pas le temps ?</span><span class="sxs-lookup"><span data-stu-id="fff95-123">Don't have time?</span></span> <span data-ttu-id="fff95-124">Ne vous inquiétez pas !</span><span class="sxs-lookup"><span data-stu-id="fff95-124">Don't worry!</span></span> <span data-ttu-id="fff95-125">La solution complète est disponible sur [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="fff95-125">The complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="fff95-126">Pour obtenir des instructions rapides, consultez [Obtenir la solution complète](#GetSolution) .</span><span class="sxs-lookup"><span data-stu-id="fff95-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="fff95-127">Une fois que vous avez terminé le didacticiel C++, utilisez les boutons de vote en bas de cette page pour nous faire part de vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="fff95-127">After you've completed the C++ tutorial, please use the voting buttons at the bottom of this page to give us feedback.</span></span> 

<span data-ttu-id="fff95-128">Si vous souhaitez que nous vous contactions directement, n’hésitez pas à inclure votre adresse de messagerie dans vos commentaires ou à [nous contacter](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="fff95-128">If you'd like us to contact you directly, feel free to include your email address in your comments or [reach out to us here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="fff95-129">Commençons dès maintenant !</span><span class="sxs-lookup"><span data-stu-id="fff95-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-c-tutorial"></a><span data-ttu-id="fff95-130">Configuration requise pour le didacticiel C++</span><span class="sxs-lookup"><span data-stu-id="fff95-130">Prerequisites for the C++ tutorial</span></span>
<span data-ttu-id="fff95-131">Vérifiez que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fff95-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="fff95-132">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="fff95-132">An active Azure account.</span></span> <span data-ttu-id="fff95-133">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit des services Azure](https://azure.microsoft.com/pricing/free-trial/)dès aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="fff95-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="fff95-134">[Visual Studio](https://www.visualstudio.com/downloads/), avec les composants du langage C++ installés.</span><span class="sxs-lookup"><span data-stu-id="fff95-134">[Visual Studio](https://www.visualstudio.com/downloads/), with the C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="fff95-135">Étape 1 : créer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fff95-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="fff95-136">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fff95-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="fff95-137">Si vous avez déjà un compte que vous souhaitez utiliser, vous pouvez passer directement à l’étape [Configurer votre application C++](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="fff95-137">If you already have an account you want to use, you can skip ahead to [Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="fff95-138"><a id="SetupC++"></a>Étape 2 : configurer votre application C++</span><span class="sxs-lookup"><span data-stu-id="fff95-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="fff95-139">Après avoir ouvert Visual Studio, dans le menu **Fichier**, cliquez sur **Nouveau**, puis sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="fff95-139">Open Visual Studio, and then on the **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="fff95-140">Dans le volet **Installé** de la fenêtre **Nouveau projet**, développez **Visual C++**, cliquez sur **Win32** et cliquez sur **Application console Win32**.</span><span class="sxs-lookup"><span data-stu-id="fff95-140">In the **New Project** window, in the **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="fff95-141">Nommez le projet hellodocumentdb, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="fff95-141">Name the project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Capture d’écran de l’Assistant Nouveau projet](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="fff95-143">Au démarrage de l’Assistant Application Win32, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="fff95-143">When the Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="fff95-144">Une fois le projet créé, ouvrez le Gestionnaire de package NuGet en cliquant avec le bouton droit sur le projet **hellodocumentdb** dans **l’Explorateur de solutions** et en cliquant sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fff95-144">Once the project has been created, open the NuGet package manager by right-clicking the **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Capture d’écran montrant Gérer le package NuGet dans le menu du projet](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="fff95-146">Dans l’onglet **NuGet : hellodocumentdb** cliquez sur **Parcourir**, puis recherchez *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="fff95-146">In the **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="fff95-147">Dans les résultats, sélectionnez DocumentDbCpp, comme l’illustre la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="fff95-147">In the results, select DocumentDbCPP, as shown in the following screenshot.</span></span> <span data-ttu-id="fff95-148">Ce package installe les références au Kit de développement logiciel (SDK) C++ REST, une dépendance de DocumentDbCpp.</span><span class="sxs-lookup"><span data-stu-id="fff95-148">This package installs references to C++ REST SDK, which is a dependency for the DocumentDbCPP.</span></span>  
   
    ![Capture d’écran du package DocumentDbCpp en surbrillance](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="fff95-150">Une fois les packages ajoutés à votre projet, nous sommes prêts à commencer à écrire du code.</span><span class="sxs-lookup"><span data-stu-id="fff95-150">Once the packages have been added to your project, we are all set to start writing some code.</span></span>   

## <span data-ttu-id="fff95-151"><a id="Config"></a>Étape 3 : copier les détails de la connexion à partir du portail Azure pour votre base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fff95-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="fff95-152">Affichez le [portail Azure](https://portal.azure.com) et accédez au compte de base de données Azure Cosmos DB créé.</span><span class="sxs-lookup"><span data-stu-id="fff95-152">Bring up [Azure portal](https://portal.azure.com) and traverse to the Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="fff95-153">Nous aurons besoin de l’URI et de la clé primaire du Portail Azure à l’étape suivante pour établir une connexion à partir de notre extrait de code C++.</span><span class="sxs-lookup"><span data-stu-id="fff95-153">We will need the URI and the primary key from Azure portal in the next step to establish a connection from our C++ code snippet.</span></span> 

![URI et clés Azure Cosmos DB dans le portail Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="fff95-155"><a id="Connect"></a>Étape 4 : se connecter à un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fff95-155"><a id="Connect"></a>Step 4: Connect to an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="fff95-156">Ajoutez les en-têtes et espaces de noms suivants à votre code source, après `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="fff95-156">Add the following headers and namespaces to your source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="fff95-157">Ensuite, ajoutez le code suivant à votre fonction principale et remplacez la configuration du compte et la clé primaire de façon à ce qu’elles correspondent à vos paramètres Azure Cosmos DB de l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="fff95-157">Next add the following code to your main function and replace the account configuration and primary key to match your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="fff95-158">Maintenant que vous avez le code permettant d’initialiser le client DocumentDB, voyons comment utiliser les ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fff95-158">Now that you have the code to initialize the documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="fff95-159"><a id="CreateDBColl"></a>Étape 5 : créer une base de données C++ et une collection</span><span class="sxs-lookup"><span data-stu-id="fff95-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="fff95-160">Avant d’effectuer cette étape, expliquons comment fonctionnent les interactions entre une base de données, une collection et des documents à ceux d’entre vous qui débutent avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fff95-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new to Azure Cosmos DB.</span></span> <span data-ttu-id="fff95-161">Une [base de données](documentdb-resources.md#databases) est un conteneur logique de stockage de documents réparti entre des collections.</span><span class="sxs-lookup"><span data-stu-id="fff95-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="fff95-162">Une [collection](documentdb-resources.md#collections) est un conteneur de documents JSON. Elle est associée à une logique d’application JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fff95-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="fff95-163">Pour en savoir plus sur les concepts et le modèle de ressources hiérarchique d’Azure Cosmos DB, consultez [Modèle de ressource hiérarchique et principaux concepts Azure Cosmos DB](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="fff95-163">You can learn more about the Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="fff95-164">Pour créer une base de données et la collection correspondante, ajoutez le code suivant à la fin de votre fonction main.</span><span class="sxs-lookup"><span data-stu-id="fff95-164">To create a database and a corresponding collection add the following code to the end of your main function.</span></span> <span data-ttu-id="fff95-165">Cela crée une base de données appelée « FamilyRegistry » et une collection appelée « FamilyCollection » selon la configuration du client déclarée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="fff95-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using the client configuration you declared in the previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="fff95-166"><a id="CreateDoc"></a>Étape 6 : créer un document</span><span class="sxs-lookup"><span data-stu-id="fff95-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="fff95-167">Les [documents](documentdb-resources.md#documents) correspondent à du contenu JSON (arbitraire) défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fff95-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="fff95-168">Vous pouvez maintenant insérer un document dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fff95-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="fff95-169">Vous pouvez créer un document en copiant le code suivant à la fin de la fonction main.</span><span class="sxs-lookup"><span data-stu-id="fff95-169">You can create a document by copying the following code into the end of the main function.</span></span> 

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

<span data-ttu-id="fff95-170">En bref, ce code crée une base de données Azure Cosmos DB, une collection et des documents, que vous pouvez interroger dans l’Explorateur de documents dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fff95-170">To summarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Tutoriel C++ : diagramme illustrant la relation hiérarchique entre le compte, la base de données, la collection et les documents](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="fff95-172"><a id="QueryDB"></a>Étape 7 : interroger les ressources Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fff95-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="fff95-173">Azure Cosmos DB prend en charge les [requêtes enrichies](documentdb-sql-query.md) sur les documents JSON stockés dans chaque collection.</span><span class="sxs-lookup"><span data-stu-id="fff95-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="fff95-174">L’exemple de code suivant affiche une requête utilisant la syntaxe SQL que vous pouvez exécuter sur les documents créés à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="fff95-174">The following sample code shows a query made using SQL syntax that you can run against the documents we created in the previous step.</span></span>

<span data-ttu-id="fff95-175">La fonction prend comme arguments l’ID de ressource ou l’identificateur unique de la base de données et de la collection, ainsi que le client du document.</span><span class="sxs-lookup"><span data-stu-id="fff95-175">The function takes in as arguments the unique identifier or resource id for the database and the collection along with the document client.</span></span> <span data-ttu-id="fff95-176">Ajoutez ce code avant la fonction main.</span><span class="sxs-lookup"><span data-stu-id="fff95-176">Add this code before main function.</span></span>

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

## <span data-ttu-id="fff95-177"><a id="Replace"></a>Étape 8 : remplacer un document</span><span class="sxs-lookup"><span data-stu-id="fff95-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="fff95-178">Azure Cosmos DB prend en charge le remplacement de documents JSON, comme l’illustre le code suivant.</span><span class="sxs-lookup"><span data-stu-id="fff95-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in the following code.</span></span> <span data-ttu-id="fff95-179">Ajoutez ce code après la fonction executesimplequery.</span><span class="sxs-lookup"><span data-stu-id="fff95-179">Add this code after the executesimplequery function.</span></span>

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

## <span data-ttu-id="fff95-180"><a id="Delete"></a>Étape 9 : supprimer un document</span><span class="sxs-lookup"><span data-stu-id="fff95-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="fff95-181">Azure Cosmos DB prend en charge la suppression de documents JSON. Pour ce faire, copiez et collez le code suivant après la fonction replacedocument.</span><span class="sxs-lookup"><span data-stu-id="fff95-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting the following code after the replacedocument function.</span></span> 

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

## <span data-ttu-id="fff95-182"><a id="DeleteDB"></a>Étape 10 : supprimer une base de données</span><span class="sxs-lookup"><span data-stu-id="fff95-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="fff95-183">Supprimer la base de données créée revient à supprimer la base de données et toutes les ressources enfants (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="fff95-183">Deleting the created database removes the database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="fff95-184">Copiez et collez l’extrait de code suivant (fonction cleanup) après la fonction deletedocument pour supprimer la base de données et toutes ses ressources enfants.</span><span class="sxs-lookup"><span data-stu-id="fff95-184">Copy and paste the following code snippet (function cleanup) after the deletedocument function to remove the database and all the child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="fff95-185"><a id="Run"></a>Étape 11 : exécuter l’ensemble votre application C++ !</span><span class="sxs-lookup"><span data-stu-id="fff95-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="fff95-186">Nous avons maintenant ajouté le code permettant de créer, d’interroger, de modifier et de supprimer différentes ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fff95-186">We have now added code to create, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="fff95-187">Nous allons maintenant lier ces éléments en ajoutant des appels à ces différentes fonctions à notre fonction main dans hellodocumentdb.cpp, ainsi que des messages de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="fff95-187">Let us now wire this up by adding calls to these different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="fff95-188">Pour cela, remplacez la fonction main de votre application par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="fff95-188">You can do so by replacing the main function of your application with the following code.</span></span> <span data-ttu-id="fff95-189">Cela remplace account_configuration_uri et primary_key que vous avez copiés dans le code à l’étape 3 : par conséquent, enregistrez cette ligne ou copiez à nouveau les valeurs sur le portail.</span><span class="sxs-lookup"><span data-stu-id="fff95-189">This writes over the account_configuration_uri and primary_key you copied into the code in Step 3, so save that line or copy the values in again from the portal.</span></span> 

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

<span data-ttu-id="fff95-190">Vous pouvez maintenant générer et exécuter votre code dans Visual Studio en appuyant sur F5 ou dans la fenêtre du terminal en localisant l’application et en exécutant le fichier exécutable.</span><span class="sxs-lookup"><span data-stu-id="fff95-190">You should now be able to build and run your code in Visual Studio by pressing F5 or alternatively in the terminal window by locating the application and running the executable.</span></span> 

<span data-ttu-id="fff95-191">La sortie de votre application de prise en main doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="fff95-191">You should see the output of your get started app.</span></span> <span data-ttu-id="fff95-192">La sortie devrait ressembler à la capture d’écran qui suit.</span><span class="sxs-lookup"><span data-stu-id="fff95-192">The output should match the following screenshot.</span></span>

![Sortie de l’application Azure Cosmos DB C++](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="fff95-194">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="fff95-194">Congratulations!</span></span> <span data-ttu-id="fff95-195">Vous avez terminé le didacticiel C++ et disposez à présent de votre première application de console Azure Cosmos DB !</span><span class="sxs-lookup"><span data-stu-id="fff95-195">You've completed the C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="fff95-196"><a id="GetSolution"></a>Obtenir la solution complète du didacticiel C++</span><span class="sxs-lookup"><span data-stu-id="fff95-196"><a id="GetSolution"></a>Get the complete C++ tutorial solution</span></span>
<span data-ttu-id="fff95-197">Pour générer la solution GetStarted qui contient tous les exemples de cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fff95-197">To build the GetStarted solution that contains all the samples in this article, you need the following:</span></span>

* <span data-ttu-id="fff95-198">[Un compte Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="fff95-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="fff95-199">La solution [GetStarted](https://github.com/stalker314314/DocumentDBCpp) disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="fff95-199">The [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fff95-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fff95-200">Next steps</span></span>
* <span data-ttu-id="fff95-201">Découvrez comment [surveiller un compte Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="fff95-201">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="fff95-202">Exécutez des requêtes sur notre exemple de dataset dans le [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="fff95-202">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="fff95-203">Consultez la section Developer (Développeur) de la [page de documentation Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/) pour découvrir plus en détail le modèle de programmation.</span><span class="sxs-lookup"><span data-stu-id="fff95-203">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


