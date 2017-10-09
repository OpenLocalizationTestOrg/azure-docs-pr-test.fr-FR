---
title: "Azure Cosmos DB : Développer avec hello API Graph dans .NET | Documents Microsoft"
description: "Découvrez comment toodevelop avec l’API DocumentDB Azure Cosmos DB à l’aide de .NET"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a><span data-ttu-id="6eb68-103">Azure Cosmos DB : Développer avec hello API Graph dans .NET</span><span class="sxs-lookup"><span data-stu-id="6eb68-103">Azure Cosmos DB: Develop with hello Graph API in .NET</span></span>
<span data-ttu-id="6eb68-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="6eb68-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="6eb68-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="6eb68-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="6eb68-106">Ce didacticiel montre comment un compte de base de données Azure Cosmos à l’aide de toocreate hello portail Azure et toocreate une base de données du graphique et un conteneur.</span><span class="sxs-lookup"><span data-stu-id="6eb68-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal and how toocreate a graph database and container.</span></span> <span data-ttu-id="6eb68-107">application Hello puis crée un réseau social simple avec quatre personnes à l’aide de hello [API Graph](graph-sdk-dotnet.md) (version préliminaire), puis parcourt et interroge le graphique de hello à l’aide de GREMLINE.</span><span class="sxs-lookup"><span data-stu-id="6eb68-107">hello application then creates a simple social network with four people using hello [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries hello graph using Gremlin.</span></span>

<span data-ttu-id="6eb68-108">Ce didacticiel couvre hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="6eb68-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6eb68-109">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6eb68-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="6eb68-110">Créer une base de données des graphiques et un conteneur</span><span class="sxs-lookup"><span data-stu-id="6eb68-110">Create a graph database and container</span></span>
> * <span data-ttu-id="6eb68-111">Sérialiser des objets de too.NET de sommets et de bords</span><span class="sxs-lookup"><span data-stu-id="6eb68-111">Serialize vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="6eb68-112">Ajouter des vertex et des bords</span><span class="sxs-lookup"><span data-stu-id="6eb68-112">Add vertices and edges</span></span>
> * <span data-ttu-id="6eb68-113">Graphique de hello la requête à l’aide de GREMLINE</span><span class="sxs-lookup"><span data-stu-id="6eb68-113">Query hello graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="6eb68-114">Graphiques dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6eb68-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="6eb68-115">Vous pouvez utiliser la base de données Azure Cosmos toocreate, mise à jour et graphiques de requête à l’aide de hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="6eb68-115">You can use Azure Cosmos DB toocreate, update, and query graphs using hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="6eb68-116">bibliothèque de Microsoft.Azure.Graph Hello fournit une méthode d’extension unique `CreateGremlinQuery<T>` par-dessus hello `DocumentClient` classe les requêtes GREMLINE tooexecute.</span><span class="sxs-lookup"><span data-stu-id="6eb68-116">hello Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of hello `DocumentClient` class tooexecute Gremlin queries.</span></span>

<span data-ttu-id="6eb68-117">Gremlin est un langage de programmation fonctionnel qui prend en charge les opérations d’écriture (DML) et les opérations de requête et de traversée.</span><span class="sxs-lookup"><span data-stu-id="6eb68-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="6eb68-118">Nous aborderons quelques exemples dans cet article de tooget votre prise en main avec GREMLINE.</span><span class="sxs-lookup"><span data-stu-id="6eb68-118">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="6eb68-119">Consultez [Requêtes Gremlin](gremlin-support.md) pour une description détaillée des fonctionnalités de Gremlin disponibles dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6eb68-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6eb68-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6eb68-120">Prerequisites</span></span>
<span data-ttu-id="6eb68-121">Vérifiez que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="6eb68-121">Please make sure you have hello following:</span></span>

* <span data-ttu-id="6eb68-122">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="6eb68-122">An active Azure account.</span></span> <span data-ttu-id="6eb68-123">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="6eb68-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="6eb68-124">Vous pouvez également utiliser hello [Azure DocumentDB émulateur](local-emulator.md) pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6eb68-124">Alternatively, you can use hello [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="6eb68-125">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="6eb68-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="6eb68-126">Créer un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="6eb68-126">Create database account</span></span>

<span data-ttu-id="6eb68-127">Commençons par la création d’un compte de base de données Azure Cosmos Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6eb68-127">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="6eb68-128">Possédez-vous un compte Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="6eb68-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="6eb68-129">Dans ce cas, passez directement trop[configurer votre solution Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="6eb68-129">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="6eb68-130">Possédiez-vous un compte Azure DocumentDB ?</span><span class="sxs-lookup"><span data-stu-id="6eb68-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="6eb68-131">Si votre compte est maintenant un compte de base de données Azure Cosmos, et que vous pouvez passer trop[configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="6eb68-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="6eb68-132">Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[configurer votre Solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="6eb68-132">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="6eb68-133"><a id="SetupVS"></a>Configurer votre solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6eb68-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="6eb68-134">Ouvrez **Visual Studio** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6eb68-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="6eb68-135">Sur hello **fichier** menu, sélectionnez **nouveau**, puis choisissez **projet**.</span><span class="sxs-lookup"><span data-stu-id="6eb68-135">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="6eb68-136">Bonjour **nouveau projet** boîte de dialogue, sélectionnez **modèles** / **Visual C#** / **l’application Console (.NET Framework)**, nommez votre projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6eb68-136">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="6eb68-137">Bonjour **l’Explorateur de solutions**, cliquez avec le bouton droit sur votre nouvelle application console qui se trouve sous votre solution Visual Studio, et puis cliquez sur **gérer les Packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="6eb68-137">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="6eb68-138">Bonjour **NuGet** , cliquez sur **Parcourir**et le type **Microsoft.Azure.Graphs** dans la zone de recherche hello et vérification hello **incluent les versions préliminaires**.</span><span class="sxs-lookup"><span data-stu-id="6eb68-138">In hello **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in hello search box, and check hello **Include prerelease versions**.</span></span>
6. <span data-ttu-id="6eb68-139">Dans les résultats de hello, recherchez **Microsoft.Azure.Graphs** et cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="6eb68-139">Within hello results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="6eb68-140">Si vous obtenez un message sur la vérification des modifications toohello solution, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6eb68-140">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="6eb68-141">Si vous obtenez un message concernant l’acceptation de la licence, cliquez sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="6eb68-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="6eb68-142">Hello `Microsoft.Azure.Graphs` bibliothèque fournit une méthode d’extension unique `CreateGremlinQuery<T>` pour l’exécution d’opérations de GREMLINE.</span><span class="sxs-lookup"><span data-stu-id="6eb68-142">hello `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="6eb68-143">Gremlin est un langage de programmation fonctionnel qui prend en charge les opérations d’écriture (DML) et les opérations de requête et de traversée.</span><span class="sxs-lookup"><span data-stu-id="6eb68-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="6eb68-144">Nous aborderons quelques exemples dans cet article de tooget votre prise en main avec GREMLINE.</span><span class="sxs-lookup"><span data-stu-id="6eb68-144">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="6eb68-145">[Requêtes Gremlin](gremlin-support.md) comporte une description détaillée des fonctionnalités de Gremlin disponibles dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6eb68-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="6eb68-146"><a id="add-references"></a>Connecter votre application</span><span class="sxs-lookup"><span data-stu-id="6eb68-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="6eb68-147">Ajoutez ces deux constantes et votre variable *client* à votre application.</span><span class="sxs-lookup"><span data-stu-id="6eb68-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="6eb68-148">Ensuite, head sauvegarde toohello [portail Azure](https://portal.azure.com) tooretrieve votre URL de point de terminaison et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="6eb68-148">Next, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="6eb68-149">URL de point de terminaison Hello et la clé primaire sont nécessaires pour votre application toounderstand où tooconnect et de base de données Azure Cosmos tootrust connexion de votre application.</span><span class="sxs-lookup"><span data-stu-id="6eb68-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span> 

<span data-ttu-id="6eb68-150">Dans hello portail Azure, accédez de compte de base de données Azure Cosmos tooyour, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**.</span><span class="sxs-lookup"><span data-stu-id="6eb68-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="6eb68-151">Copiez hello URI à partir du portail de hello et collez-la sur `Endpoint` dans la propriété de point de terminaison hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="6eb68-151">Copy hello URI from hello portal and paste it over `Endpoint` in hello endpoint property above.</span></span> <span data-ttu-id="6eb68-152">Puis copie hello clé primaire à partir du portail de hello et collez-le dans hello `AuthKey` propriété ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="6eb68-152">Then copy hello PRIMARY KEY from hello portal and paste it into hello `AuthKey` property above.</span></span> 

<span data-ttu-id="6eb68-153">! [Capture d’écran de hello portail Azure utilisée par toocreate de didacticiel hello une application c#.</span><span class="sxs-lookup"><span data-stu-id="6eb68-153">![Screen shot of hello Azure portal used by hello tutorial toocreate a C# application.</span></span> <span data-ttu-id="6eb68-154">Affiche un hello de compte de base de données Azure Cosmos bouton clés en surbrillance sur hello navigation de base de données Azure Cosmos et valeurs d’URI et la clé primaire hello mis en surbrillance sur hello Panneau de clés] [clés]</span><span class="sxs-lookup"><span data-stu-id="6eb68-154">Shows an Azure Cosmos DB account hello KEYS button highlighted on hello Azure Cosmos DB navigation , and hello URI and PRIMARY KEY values highlighted on hello Keys blade][keys]</span></span> 
 
## <span data-ttu-id="6eb68-155"><a id="instantiate"></a>Instancier hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="6eb68-155"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span> 
<span data-ttu-id="6eb68-156">Ensuite, créez une nouvelle instance de hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="6eb68-156">Next, create a new instance of hello **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="6eb68-157"><a id="create-database"></a>Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="6eb68-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="6eb68-158">À présent, créez une base de données Azure Cosmos [base de données](documentdb-resources.md#databases) à l’aide de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) méthode ou [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) méthode Hello  **DocumentClient** classe à partir de hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6eb68-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="6eb68-159">Créer un graphique</span><span class="sxs-lookup"><span data-stu-id="6eb68-159">Create a graph</span></span> 

<span data-ttu-id="6eb68-160">Ensuite, créez un conteneur graphique à l’aide de hello à l’aide de hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) méthode ou [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) méthode Hello **DocumentClient**  classe.</span><span class="sxs-lookup"><span data-stu-id="6eb68-160">Next, create a graph container by using hello using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="6eb68-161">Une collection est un conteneur d’entités graphiques.</span><span class="sxs-lookup"><span data-stu-id="6eb68-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="6eb68-162"><a id="serializing"></a>Sérialiser des objets de too.NET de sommets et de bords</span><span class="sxs-lookup"><span data-stu-id="6eb68-162"><a id="serializing"></a>Serialize vertices and edges too.NET objects</span></span>
<span data-ttu-id="6eb68-163">Base de données Azure Cosmos utilise hello [GraphSON au format câble](gremlin-support.md), qui définit un schéma JSON pour les propriétés, les bords et les sommets.</span><span class="sxs-lookup"><span data-stu-id="6eb68-163">Azure Cosmos DB uses hello [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="6eb68-164">Bonjour Azure Cosmos DB .NET SDK inclut JSON.NET en tant que dépendance, et cela nous permet de désérialiser GraphSON/tooserialize en objets .NET que nous pouvons utiliser dans le code.</span><span class="sxs-lookup"><span data-stu-id="6eb68-164">hello Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us tooserialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="6eb68-165">Par exemple, nous allons travailler avec un réseau social simple composé de quatre personnes.</span><span class="sxs-lookup"><span data-stu-id="6eb68-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="6eb68-166">Nous abordons la façon dont toocreate `Person` sommets, ajouter `Knows` des relations entre eux, puis interroger et parcourir des relations de hello graphique toofind « friend de friend ».</span><span class="sxs-lookup"><span data-stu-id="6eb68-166">We look at how toocreate `Person` vertices, add `Knows` relationships between them, then query and traverse hello graph toofind "friend of friend" relationships.</span></span> 

<span data-ttu-id="6eb68-167">Hello `Microsoft.Azure.Graphs.Elements` fournit de l’espace de noms `Vertex`, `Edge`, `Property` et `VertexProperty` des classes pour la désérialisation des objets de .NET définis par le toowell GraphSON réponses.</span><span class="sxs-lookup"><span data-stu-id="6eb68-167">hello `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses toowell-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="6eb68-168">Exécuter Gremlin à l’aide de CreateGremlinQuery</span><span class="sxs-lookup"><span data-stu-id="6eb68-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="6eb68-169">Gremlin, tout comme SQL, prend en charge les opérations de lecture, d’écriture et d’interrogation.</span><span class="sxs-lookup"><span data-stu-id="6eb68-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="6eb68-170">Par exemple, hello extrait de code suivant montre comment toocreate sommets, contours, effectuer quelques exemples de requêtes à l’aide de `CreateGremlinQuery<T>`et de façon asynchrone une itération au sein ces résultats à l’aide `ExecuteNextAsync` et ' HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="6eb68-170">For example, hello following snippet shows how toocreate vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a><span data-ttu-id="6eb68-171">Ajouter des vertex et des bords</span><span class="sxs-lookup"><span data-stu-id="6eb68-171">Add vertices and edges</span></span>

<span data-ttu-id="6eb68-172">Examinons les instructions de GREMLINE hello illustrées hello précédant la section plus en détail.</span><span class="sxs-lookup"><span data-stu-id="6eb68-172">Let's look at hello Gremlin statements shown in hello preceding section more detail.</span></span> <span data-ttu-id="6eb68-173">Nous commençons par créer des vertex à l’aide de la méthode `addV` de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="6eb68-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="6eb68-174">Par exemple, hello extrait de code suivant crée un sommet « Thomas Andersen » de type « Person », avec des propriétés pour le prénom, nom et âge.</span><span class="sxs-lookup"><span data-stu-id="6eb68-174">For example, hello following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

<span data-ttu-id="6eb68-175">Nous créons ensuite des bords entre ces vertex à l’aide de la méthode `addE` de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="6eb68-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

<span data-ttu-id="6eb68-176">Nous pouvons mettre à jour un vertex existant à l’aide de l’étape `properties` dans Gremlin.</span><span class="sxs-lookup"><span data-stu-id="6eb68-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="6eb68-177">Nous ignorer la requête de hello hello appel tooexecute via `HasMoreResults` et `ExecuteNextAsync` pour obtenir des exemples hello autres hello.</span><span class="sxs-lookup"><span data-stu-id="6eb68-177">We skip hello call tooexecute hello query via `HasMoreResults` and `ExecuteNextAsync` for hello rest of hello examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="6eb68-178">Vous pouvez supprimer des bords et des vertex en suivant l’étape `drop` de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="6eb68-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="6eb68-179">Voici un extrait de code qui montre comment toodelete un sommet et qu’un bord.</span><span class="sxs-lookup"><span data-stu-id="6eb68-179">Here's a snippet that shows how toodelete a vertex and an edge.</span></span> <span data-ttu-id="6eb68-180">Notez que la suppression d’un sommet effectue une suppression en cascade de hello associés bords.</span><span class="sxs-lookup"><span data-stu-id="6eb68-180">Note that dropping a vertex performs a cascading delete of hello associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a><span data-ttu-id="6eb68-181">Graphique de requête hello</span><span class="sxs-lookup"><span data-stu-id="6eb68-181">Query hello graph</span></span>

<span data-ttu-id="6eb68-182">Gremlin permet également d’effectuer des requêtes et des traversées.</span><span class="sxs-lookup"><span data-stu-id="6eb68-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="6eb68-183">Par exemple, hello suivant extrait de code montre comment toocount hello nombre de sommets dans le graphique de hello :</span><span class="sxs-lookup"><span data-stu-id="6eb68-183">For example, hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="6eb68-184">Vous pouvez effectuer des filtres à l’aide de GREMLINE `has` et `hasLabel` les étapes et les associer à l’aide de `and`, `or`, et `not` toobuild les filtres plus complexe :</span><span class="sxs-lookup"><span data-stu-id="6eb68-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="6eb68-185">Vous pouvez projeter certaines propriétés dans les résultats de la requête hello à l’aide de hello `values` étape :</span><span class="sxs-lookup"><span data-stu-id="6eb68-185">You can project certain properties in hello query results using hello `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="6eb68-186">Jusqu’ici, nous avons seulement abordé les opérateurs de requête fonctionnant dans n’importe quelle base de données.</span><span class="sxs-lookup"><span data-stu-id="6eb68-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="6eb68-187">Graphiques sont rapides et efficaces pour les opérations de parcours lorsque vous avez besoin toonavigate toorelated arêtes et les sommets.</span><span class="sxs-lookup"><span data-stu-id="6eb68-187">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="6eb68-188">Recherchons à présent tous les amis de Thomas.</span><span class="sxs-lookup"><span data-stu-id="6eb68-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="6eb68-189">Pour ce faire, nous à l’aide de GREMLINE `outE` toofind hello tous les out-bords Thomas à partir de l’étape, puis parcourir les sommets dans toohello entre les bords à l’aide de GREMLINE `inV` étape :</span><span class="sxs-lookup"><span data-stu-id="6eb68-189">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="6eb68-190">éditeur de requête suivant de Hello effectue deux sauts toofind tous « Amis de vos amis » de Thomas, en appelant `outE` et `inV` deux fois.</span><span class="sxs-lookup"><span data-stu-id="6eb68-190">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="6eb68-191">Vous pouvez générer des requêtes plus complexes et implémenter la logique de parcours puissant de graphique à l’aide de GREMLINE, y compris filtre mélange des expressions, exécution à l’aide de bouclage hello `loop` étape et la navigation conditionnelle implémentation à l’aide de hello `choose` étape.</span><span class="sxs-lookup"><span data-stu-id="6eb68-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="6eb68-192">En savoir plus sur ce que la [prise en charge de Gremlin](gremlin-support.md) vous permet de faire !</span><span class="sxs-lookup"><span data-stu-id="6eb68-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="6eb68-193">Ce didacticiel Azure Cosmos DB est maintenant terminé !</span><span class="sxs-lookup"><span data-stu-id="6eb68-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="6eb68-194">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="6eb68-194">Clean up resources</span></span>

<span data-ttu-id="6eb68-195">Si vous n’allez toocontinue toouse cette application, utilisez hello suivant toodelete suit toutes les ressources créées par ce didacticiel Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6eb68-195">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>  

1. <span data-ttu-id="6eb68-196">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="6eb68-196">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="6eb68-197">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="6eb68-197">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6eb68-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6eb68-198">Next Steps</span></span>

<span data-ttu-id="6eb68-199">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="6eb68-199">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6eb68-200">Créé un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6eb68-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="6eb68-201">Créer une base de données des graphiques et un conteneur</span><span class="sxs-lookup"><span data-stu-id="6eb68-201">Created a graph database and container</span></span>
> * <span data-ttu-id="6eb68-202">Objets sérialisés too.NET de sommets et de bords</span><span class="sxs-lookup"><span data-stu-id="6eb68-202">Serialized vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="6eb68-203">Ajouter des vertex et des bords</span><span class="sxs-lookup"><span data-stu-id="6eb68-203">Added vertices and edges</span></span>
> * <span data-ttu-id="6eb68-204">Graphique de hello interrogé à l’aide de GREMLINE</span><span class="sxs-lookup"><span data-stu-id="6eb68-204">Queried hello graph using Gremlin</span></span>

<span data-ttu-id="6eb68-205">Vous pouvez maintenant générer des requêtes plus complexes et implémenter une logique de traversée de graphique puissante, à l’aide de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="6eb68-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="6eb68-206">Interroger à l’aide de Gremlin</span><span class="sxs-lookup"><span data-stu-id="6eb68-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
