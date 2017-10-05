---
title: "Azure Cosmos DB : développer avec l’API DocumentDB dans .NET | Microsoft Docs"
description: "Apprendre à développer avec l’API DocumentDB d’Azure Cosmos DB à l’aide de .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 2eed74ae9bd173b0944ec190dfe5d9a4bdc54c37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmosdb-develop-with-the-documentdb-api-in-net"></a><span data-ttu-id="6052f-103">Azure Cosmos DB : développer avec l’API DocumentDB dans .NET</span><span class="sxs-lookup"><span data-stu-id="6052f-103">Azure CosmosDB: Develop with the DocumentDB API in .NET</span></span>

<span data-ttu-id="6052f-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="6052f-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="6052f-105">Vous pouvez rapidement créer et interroger des documents, des paires clé/valeur et des bases de données de graphiques, tous profitant de la distribution à l’échelle mondiale et des capacités de mise à l’échelle horizontale au cœur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6052f-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="6052f-106">Ce didacticiel montre comment créer un compte Azure Cosmos DB à l’aide du portail Azure, puis une base de données de documents et une collection avec une [clé de partition](documentdb-partition-data.md#partition-keys) à l’aide de [l’API .NET de DocumentDB](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6052f-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using the [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="6052f-107">En définissant une clé de partition au moment de créer une collection, vous préparez votre application et lui permettez d’être mise à l’échelle sans effort, à mesure que le volume de vos données augmente.</span><span class="sxs-lookup"><span data-stu-id="6052f-107">By defining a partition key when you create a collection, your application is prepared to scale effortlessly as your data grows.</span></span> 

<span data-ttu-id="6052f-108">Ce didacticiel décrit les tâches suivantes à l’aide de [l’API .NET de DocumentDB](documentdb-sdk-dotnet.md) :</span><span class="sxs-lookup"><span data-stu-id="6052f-108">This tutorial covers the following tasks by using the [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6052f-109">Créer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6052f-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="6052f-110">Créer une base de données et une collection avec une clé de partition</span><span class="sxs-lookup"><span data-stu-id="6052f-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="6052f-111">Créer des documents JSON</span><span class="sxs-lookup"><span data-stu-id="6052f-111">Create JSON documents</span></span>
> * <span data-ttu-id="6052f-112">Mettre à jour un document</span><span class="sxs-lookup"><span data-stu-id="6052f-112">Update a document</span></span>
> * <span data-ttu-id="6052f-113">Interroger des collections partitionnées</span><span class="sxs-lookup"><span data-stu-id="6052f-113">Query partitioned collections</span></span>
> * <span data-ttu-id="6052f-114">Exécuter des procédures stockées</span><span class="sxs-lookup"><span data-stu-id="6052f-114">Run stored procedures</span></span>
> * <span data-ttu-id="6052f-115">Supprimer un document</span><span class="sxs-lookup"><span data-stu-id="6052f-115">Delete a document</span></span>
> * <span data-ttu-id="6052f-116">Supprimer une base de données</span><span class="sxs-lookup"><span data-stu-id="6052f-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6052f-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6052f-117">Prerequisites</span></span>
<span data-ttu-id="6052f-118">Vérifiez que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6052f-118">Please make sure you have the following:</span></span>

* <span data-ttu-id="6052f-119">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="6052f-119">An active Azure account.</span></span> <span data-ttu-id="6052f-120">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="6052f-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="6052f-121">Si vous préférez utiliser un environnement local qui émule le service Azure DocumentDB à des fins de développement, vous pouvez utiliser [l’émulateur Azure Cosmos DB](local-emulator.md) dans le cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6052f-121">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like to use a local environment that emulates the Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="6052f-122">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="6052f-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="6052f-123">Créer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6052f-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="6052f-124">Commençons par créer un compte Azure Cosmos DB dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6052f-124">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="6052f-125">Possédez-vous un compte Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="6052f-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="6052f-126">Si tel est le cas, passez directement à l’étape [Configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="6052f-126">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="6052f-127">Possédiez-vous un compte Azure DocumentDB ?</span><span class="sxs-lookup"><span data-stu-id="6052f-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="6052f-128">Si c’est le cas, votre compte a été converti en compte Azure Cosmos DB et vous pouvez passer directement à l’étape [Configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="6052f-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="6052f-129">Si vous utilisez l’émulateur Azure Cosmos DB, suivez les étapes de la section [Émulateur Azure Cosmos DB](local-emulator.md) pour le configurer, puis passez directement à l’étape [Configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="6052f-129">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="6052f-130"><a id="SetupVS"></a>Configurer votre solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6052f-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="6052f-131">Ouvrez **Visual Studio** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6052f-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="6052f-132">Dans le menu **Fichier**, sélectionnez **Nouveau**, puis choisissez **Projet**.</span><span class="sxs-lookup"><span data-stu-id="6052f-132">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="6052f-133">Dans la boîte de dialogue **Nouveau projet**, sélectionnez **Modèles** / **Visual C#** / **Application console (.NET Framework)**, donnez un nom à votre projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6052f-133">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="6052f-134">![Capture d’écran de la fenêtre Nouveau projet](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="6052f-134">![Screen shot of the New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="6052f-135">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur votre nouvelle application console, qui se trouve sous votre solution Visual Studio, puis cliquez sur **Gérer les packages NuGet…**</span><span class="sxs-lookup"><span data-stu-id="6052f-135">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Capture d'écran du menu du clic droit pour le projet](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="6052f-137">Dans l’onglet **NuGet**, cliquez sur **Parcourir**, puis tapez **documentdb** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="6052f-137">In the **NuGet** tab, click **Browse**, and type **documentdb** in the search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="6052f-138">Dans les résultats, recherchez **Microsoft.Azure.DocumentDB** et cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="6052f-138">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="6052f-139">L’ID de package de la bibliothèque cliente Azure Cosmos DB est [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="6052f-139">The package ID for the Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="6052f-140">![Capture d’écran du menu NuGet pour la recherche du Kit de développement logiciel (SDK) client Azure Cosmos DB](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="6052f-140">![Screen shot of the NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="6052f-141">Si vous obtenez un message concernant la vérification des modifications apportées à la solution, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6052f-141">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="6052f-142">Si vous obtenez un message concernant l’acceptation de la licence, cliquez sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="6052f-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="6052f-143"><a id="Connect"></a>Ajouter des références à votre projet</span><span class="sxs-lookup"><span data-stu-id="6052f-143"><a id="Connect"></a>Add references to your project</span></span>
<span data-ttu-id="6052f-144">Les étapes restantes de ce didacticiel fournissent les extraits de code API DocumentDB requis pour créer et mettre à jour des ressources Azure Cosmos DB dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="6052f-144">The remaining steps in this tutorial provide the DocumentDB API code snippets required to create and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="6052f-145">Tout d’abord, ajoutez ces références à votre application.</span><span class="sxs-lookup"><span data-stu-id="6052f-145">First, add these references to your application.</span></span>
<!---These aren't added by default when you install the pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="6052f-146"><a id="add-references"></a>Connecter votre application</span><span class="sxs-lookup"><span data-stu-id="6052f-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="6052f-147">Ajoutez ces deux constantes et votre variable *client* à votre application.</span><span class="sxs-lookup"><span data-stu-id="6052f-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="6052f-148">Ensuite, revenez dans le [portail Azure](https://portal.azure.com) pour récupérer l’URL du point de terminaison et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="6052f-148">Then, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="6052f-149">L’URL du point de terminaison et la clé primaire sont nécessaires pour que votre application sache où se connecter et qu’Azure Cosmos DB approuve la connexion de votre application.</span><span class="sxs-lookup"><span data-stu-id="6052f-149">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="6052f-150">Dans le portail Azure, accédez à votre compte Azure Cosmos DB, cliquez sur **Clés**, puis sur **Clés en lecture-écriture**.</span><span class="sxs-lookup"><span data-stu-id="6052f-150">In the Azure portal, navigate to your Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="6052f-151">Copiez l’URI à partir du portail et collez-le dans `<your endpoint URL>`, dans le fichier program.cs.</span><span class="sxs-lookup"><span data-stu-id="6052f-151">Copy the URI from the portal and paste it over `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="6052f-152">Copiez ensuite la CLÉ PRIMAIRE à partir du portail et collez-la dans `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="6052f-152">Then copy the PRIMARY KEY from the portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="6052f-153">Veillez à supprimer `<` et `>` des valeurs.</span><span class="sxs-lookup"><span data-stu-id="6052f-153">Be sure to remove the `<` and `>` from your values.</span></span>

![Capture d’écran du portail Azure utilisée par le didacticiel NoSQL pour créer une application de console C#.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="6052f-156"><a id="instantiate"></a>Instancier le DocumentClient</span><span class="sxs-lookup"><span data-stu-id="6052f-156"><a id="instantiate"></a>Instantiate the DocumentClient</span></span>

<span data-ttu-id="6052f-157">Maintenant, créez une instance de **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="6052f-157">Now, create a new instance of the **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="6052f-158"><a id="create-database"></a>Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="6052f-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="6052f-159">Ensuite, créez une [base de données](documentdb-resources.md#databases) Azure Cosmos DB à l’aide de la méthode [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) ou de la méthode [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) de la classe **DocumentClient** à partir du [SDK DocumentDB .NET](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6052f-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class from the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="6052f-160">Une base de données est le conteneur logique de stockage de documents JSON partitionné entre les collections.</span><span class="sxs-lookup"><span data-stu-id="6052f-160">A database is the logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="6052f-161">Choisir une clé de partition</span><span class="sxs-lookup"><span data-stu-id="6052f-161">Decide on a partition key</span></span> 

<span data-ttu-id="6052f-162">Les collections sont des conteneurs servant au stockage des documents.</span><span class="sxs-lookup"><span data-stu-id="6052f-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="6052f-163">Ce sont des ressources logiques. [Elles peuvent s’étendre sur une ou plusieurs partitions physiques](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="6052f-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="6052f-164">Une [clé de partition](documentdb-partition-data.md) est une propriété (ou chemin d’accès) dans vos documents qui sert à distribuer vos données entre plusieurs serveurs ou partitions.</span><span class="sxs-lookup"><span data-stu-id="6052f-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used to distribute your data among the servers or partitions.</span></span> <span data-ttu-id="6052f-165">Tous les documents présentant la même clé de partition sont stockés au sein de la même partition.</span><span class="sxs-lookup"><span data-stu-id="6052f-165">All documents with the same partition key are stored in the same partition.</span></span> 

<span data-ttu-id="6052f-166">Il est important de choisir une clé de partition avant de créer une collection.</span><span class="sxs-lookup"><span data-stu-id="6052f-166">Determining a partition key is an important decision to make before you create a collection.</span></span> <span data-ttu-id="6052f-167">Les clés de partition sont une propriété (ou chemin d’accès) dans vos documents dont Azure Cosmos DB se sert pour distribuer vos données entre plusieurs serveurs ou partitions.</span><span class="sxs-lookup"><span data-stu-id="6052f-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB to distribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="6052f-168">Cosmos DB hache la valeur de clé de partition et utilise le résultat haché pour déterminer dans quelle partition stocker le document.</span><span class="sxs-lookup"><span data-stu-id="6052f-168">Cosmos DB hashes the partition key value and uses the hashed result to determine the partition in which to store the document.</span></span> <span data-ttu-id="6052f-169">Tous les documents ayant la même clé de partition sont stockés dans la même partition, et il est impossible de modifier les clés de partition après la création d’une collection.</span><span class="sxs-lookup"><span data-stu-id="6052f-169">All documents with the same partition key are stored in the same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="6052f-170">Dans le cadre de ce didacticiel, nous allons définir la clé de partition sur `/deviceId` afin que toutes les données d’un seul appareil soient stockées dans une partition unique.</span><span class="sxs-lookup"><span data-stu-id="6052f-170">For this tutorial, we're going to set the partition key to `/deviceId` so that the all the data for a single device is stored in a single partition.</span></span> <span data-ttu-id="6052f-171">Vous souhaitez une clé de partition qui comporte un grand nombre de valeurs, chacune d’elles étant utilisées sur la même fréquence. Votre objectif ? Garantir que Cosmos DB puisse équilibrer la charge à mesure que le volume de vos données augmente et atteindre le débit maximal de la collection.</span><span class="sxs-lookup"><span data-stu-id="6052f-171">You want to choose a partition key that has a large number of values, each of which are used at about the same frequency to ensure Cosmos DB can load balance as your data grows and achieve the full throughput of the collection.</span></span> 

<span data-ttu-id="6052f-172">Pour plus d’informations sur le partitionnement, voir [Comment partitionner et mettre à l’échelle dans Azure Cosmos DB ?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="6052f-172">For more information about partitioning, see [How to partition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="6052f-173"><a id="CreateColl"></a>Créer une collection</span><span class="sxs-lookup"><span data-stu-id="6052f-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="6052f-174">Maintenant que nous connaissons notre clé de partition, `/deviceId`, créons une [collection](documentdb-resources.md#collections) à l’aide de la méthode [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) ou de la méthode [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) de la classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="6052f-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="6052f-175">Une collection est un conteneur de documents JSON. Elle est associée à une logique d’application JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6052f-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="6052f-176">La création d’une collection a des conséquences d’un point de vue tarifaire. En effet, vous réservez une part du débit pour que l’application puisse communiquer avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6052f-176">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="6052f-177">Pour plus d'informations, visitez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="6052f-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here the JSON property deviceId is used  
// as the partition key to spread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

<span data-ttu-id="6052f-178">Cette méthode passe un appel d’API REST à Azure Cosmos DB et le service approvisionne un certain nombre de partitions en fonction du débit demandé.</span><span class="sxs-lookup"><span data-stu-id="6052f-178">This method makes a REST API call to Azure Cosmos DB, and the service provisions a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="6052f-179">Vous pouvez modifier le débit d’une collection à mesure que vos besoins en performances évoluent. Pour cela, vous utilisez le SDK ou le [portail Azure](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="6052f-179">You can change the throughput of a collection as your performance needs evolve using the SDK or the [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="6052f-180"><a id="CreateDoc"></a>Créer des documents JSON</span><span class="sxs-lookup"><span data-stu-id="6052f-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="6052f-181">Insérons maintenant des documents JSON dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6052f-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="6052f-182">Vous pouvez créer un [document](documentdb-resources.md#documents) à l’aide de la méthode [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) de la classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="6052f-182">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="6052f-183">Les documents sont du contenu JSON (arbitraire) défini par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6052f-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="6052f-184">Cette classe utilisée à titre d’exemple contient la lecture d’un appareil et un appel à la méthode CreateDocumentAsync pour insérer une nouvelle lecture d’appareil dans une collection.</span><span class="sxs-lookup"><span data-stu-id="6052f-184">This sample class contains a device reading, and a call to CreateDocumentAsync to insert a new device reading into a collection.</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here the partition key is extracted 
// as "XMS-0001" based on the collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a><span data-ttu-id="6052f-185">Lire les données</span><span class="sxs-lookup"><span data-stu-id="6052f-185">Read data</span></span>

<span data-ttu-id="6052f-186">Lisons le document par sa clé de partition et son identifiant à l’aide de la méthode ReadDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="6052f-186">Let's read the document by its partition key and Id using the ReadDocumentAsync method.</span></span> <span data-ttu-id="6052f-187">Notez que les lectures incluent une valeur PartitionKey (correspondant à l’en-tête de demande `x-ms-documentdb-partitionkey` dans l’API REST).</span><span class="sxs-lookup"><span data-stu-id="6052f-187">Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the Id to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="6052f-188">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="6052f-188">Update data</span></span>

<span data-ttu-id="6052f-189">Maintenant, nous allons mettre à jour les données à l’aide de la méthode ReplaceDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="6052f-189">Now let's update some data using the ReplaceDocumentAsync method.</span></span>

```csharp
// Update the document. Partition key is not required, again extracted from the document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="6052f-190">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="6052f-190">Delete data</span></span>

<span data-ttu-id="6052f-191">Supprimons un document par sa clé de partition et son identifiant à l’aide de la méthode DeleteDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="6052f-191">Now lets delete a document by partition key and id by using the DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. The partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="6052f-192">Interroger des collections partitionnées</span><span class="sxs-lookup"><span data-stu-id="6052f-192">Query partitioned collections</span></span>

<span data-ttu-id="6052f-193">Lorsque vous interrogez des données dans des collections partitionnées, Azure Cosmos DB achemine automatiquement la requête vers les partitions correspondant aux valeurs de clé de partition spécifiées dans le filtre (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="6052f-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="6052f-194">Par exemple, cette requête est acheminée uniquement vers la partition contenant la clé de partition « XMS-0001 ».</span><span class="sxs-lookup"><span data-stu-id="6052f-194">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="6052f-195">Pour la requête suivante, la clé de partition (DeviceId) n’a pas de filtre. La requête est donc distribuée à toutes les partitions où elle est exécutée sur l’index de la partition.</span><span class="sxs-lookup"><span data-stu-id="6052f-195">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="6052f-196">Notez que vous devez spécifier la valeur EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` dans l’API REST) pour que le Kit de développement logiciel (SDK) exécute une requête sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="6052f-196">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="6052f-197">Exécution de requêtes parallèles</span><span class="sxs-lookup"><span data-stu-id="6052f-197">Parallel query execution</span></span>
<span data-ttu-id="6052f-198">Les kits de développement logiciel (SDK) d’Azure Cosmos DB version 1.9.0 et versions ultérieures prennent en charge des options d’exécution de requêtes parallèles. Ils vous permettent d’effectuer des requêtes à faible latence sur les collections partitionnées, même lorsque ces requêtes concernent un grand nombre de partitions.</span><span class="sxs-lookup"><span data-stu-id="6052f-198">The Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="6052f-199">Par exemple, la requête suivante est configurée pour s’exécuter en parallèle sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="6052f-199">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="6052f-200">Vous pouvez gérer l’exécution de requêtes parallèles en réglant les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="6052f-200">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="6052f-201">En définissant `MaxDegreeOfParallelism`, vous pouvez contrôler le degré de parallélisme, c’est-à-dire le nombre maximal de connexions réseau simultanées aux partitions de la collection.</span><span class="sxs-lookup"><span data-stu-id="6052f-201">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the collection's partitions.</span></span> <span data-ttu-id="6052f-202">Si vous définissez cette valeur sur -1, le degré de parallélisme est géré par le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="6052f-202">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="6052f-203">Si la valeur `MaxDegreeOfParallelism` n’est pas spécifiée ou définie sur 0, qui est la valeur par défaut, il n’y aura qu’une seule connexion réseau aux partitions de la collection.</span><span class="sxs-lookup"><span data-stu-id="6052f-203">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the collection's partitions.</span></span>
* <span data-ttu-id="6052f-204">En définissant `MaxBufferedItemCount`, vous pouvez compenser l’utilisation de la mémoire côté client et la latence de la requête.</span><span class="sxs-lookup"><span data-stu-id="6052f-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="6052f-205">Si vous omettez ce paramètre ou que vous lui affectez la valeur -1, le nombre d’éléments mis en mémoire tampon pendant l’exécution de requêtes parallèles est géré par le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="6052f-205">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="6052f-206">Avec un même état de collection, une requête parallèle retourne les résultats dans l’ordre d’exécution en série.</span><span class="sxs-lookup"><span data-stu-id="6052f-206">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="6052f-207">Lorsque vous effectuez une requête entre plusieurs partitions qui comporte le tri (ORDER BY et/ou TOP), le Kit de développement logiciel (SDK) de DocumentDB émet la requête en parallèle sur plusieurs partitions et fusionne les résultats partiellement triés côté client pour produire des résultats globalement classés.</span><span class="sxs-lookup"><span data-stu-id="6052f-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the DocumentDB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="6052f-208">Exécuter des procédures stockées</span><span class="sxs-lookup"><span data-stu-id="6052f-208">Execute stored procedures</span></span>
<span data-ttu-id="6052f-209">Enfin, vous pouvez également exécuter des transactions atomiques sur des documents avec le même ID d’appareil. C’est par exemple le cas lorsque vous réalisez la maintenance des agrégats ou que vous souhaitez obtenir le dernier état d’un appareil dans un document unique. Il vous suffit alors d’ajouter le code suivant à votre projet.</span><span class="sxs-lookup"><span data-stu-id="6052f-209">Lastly, you can execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single document by adding the following code to your project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="6052f-210">Et le tour est joué !</span><span class="sxs-lookup"><span data-stu-id="6052f-210">And that's it!</span></span> <span data-ttu-id="6052f-211">Il s’agit des principaux composants d’une application Azure Cosmos DB qui utilise une clé de partition pour mettre efficacement à l’échelle la distribution des données sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="6052f-211">those are the main components of an Azure Cosmos DB application that uses a partition key to efficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="6052f-212">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="6052f-212">Clean up resources</span></span>

<span data-ttu-id="6052f-213">Si vous ne prévoyez pas de continuer à utiliser cette application, supprimez toutes les ressources créées par ce didacticiel dans le portail Azure. Pour cela, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6052f-213">If you're not going to continue to use this app, delete all resources created by this tutorial in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="6052f-214">Dans le menu de gauche du portail Azure, cliquez sur **Groupes de ressources**, puis sur le nom de la ressource que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="6052f-214">From the left-hand menu in the Azure portal, click **Resource groups** and then click the unique name of the resource you created.</span></span> 
2. <span data-ttu-id="6052f-215">Sur la page de votre groupe de ressources, cliquez sur **Supprimer**, tapez le nom de la ressource à supprimer dans la zone de texte, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="6052f-215">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6052f-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6052f-216">Next steps</span></span>

<span data-ttu-id="6052f-217">Dans ce didacticiel, vous avez :</span><span class="sxs-lookup"><span data-stu-id="6052f-217">In this tutorial, you've done the following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6052f-218">Créé un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6052f-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="6052f-219">Créé une base de données et une collection avec une clé de partition</span><span class="sxs-lookup"><span data-stu-id="6052f-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="6052f-220">Créé des documents JSON</span><span class="sxs-lookup"><span data-stu-id="6052f-220">Created JSON documents</span></span>
> * <span data-ttu-id="6052f-221">Mis à jour un document</span><span class="sxs-lookup"><span data-stu-id="6052f-221">Updated a document</span></span>
> * <span data-ttu-id="6052f-222">Interrogé des collections partitionnées</span><span class="sxs-lookup"><span data-stu-id="6052f-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="6052f-223">Exécuté une procédure stockée</span><span class="sxs-lookup"><span data-stu-id="6052f-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="6052f-224">Supprimé un document</span><span class="sxs-lookup"><span data-stu-id="6052f-224">Deleted a document</span></span>
> * <span data-ttu-id="6052f-225">Supprimé une base de données</span><span class="sxs-lookup"><span data-stu-id="6052f-225">Deleted a database</span></span>

<span data-ttu-id="6052f-226">Vous pouvez maintenant passer à l’étape suivante du didacticiel et importer des données supplémentaires dans votre compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6052f-226">You can now proceed to the next tutorial and import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="6052f-227">Importer des données dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6052f-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
