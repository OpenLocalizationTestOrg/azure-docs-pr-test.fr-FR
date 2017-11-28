---
title: "Azure Cosmos DB : Développer avec hello API DocumentDB dans .NET | Documents Microsoft"
description: "Découvrez comment toodevelop avec l’API DocumentDB Azure Cosmos DB à l’aide de .NET"
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
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a><span data-ttu-id="15b90-103">Azure CosmosDB : Développer avec hello API DocumentDB dans .NET</span><span class="sxs-lookup"><span data-stu-id="15b90-103">Azure CosmosDB: Develop with hello DocumentDB API in .NET</span></span>

<span data-ttu-id="15b90-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="15b90-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="15b90-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="15b90-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="15b90-106">Ce didacticiel montre comment toocreate un compte de base de données Azure Cosmos à l’aide de hello portail Azure et ensuite créer une base de données du document et de la collection avec une [clé de partition](documentdb-partition-data.md#partition-keys) à l’aide de hello [DocumentDB .NET API](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="15b90-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using hello [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="15b90-107">En définissant une clé de partition lorsque vous créez une collection, votre application est prête tooscale aptitude à mesure que vos données augmentent.</span><span class="sxs-lookup"><span data-stu-id="15b90-107">By defining a partition key when you create a collection, your application is prepared tooscale effortlessly as your data grows.</span></span> 

<span data-ttu-id="15b90-108">Les tâches suivantes hello didacticiel couvre à l’aide de hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="15b90-108">This tutorial covers hello following tasks by using hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="15b90-109">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="15b90-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="15b90-110">Créer une base de données et une collection avec une clé de partition</span><span class="sxs-lookup"><span data-stu-id="15b90-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="15b90-111">Créer des documents JSON</span><span class="sxs-lookup"><span data-stu-id="15b90-111">Create JSON documents</span></span>
> * <span data-ttu-id="15b90-112">Mettre à jour un document</span><span class="sxs-lookup"><span data-stu-id="15b90-112">Update a document</span></span>
> * <span data-ttu-id="15b90-113">Interroger des collections partitionnées</span><span class="sxs-lookup"><span data-stu-id="15b90-113">Query partitioned collections</span></span>
> * <span data-ttu-id="15b90-114">Exécuter des procédures stockées</span><span class="sxs-lookup"><span data-stu-id="15b90-114">Run stored procedures</span></span>
> * <span data-ttu-id="15b90-115">Supprimer un document</span><span class="sxs-lookup"><span data-stu-id="15b90-115">Delete a document</span></span>
> * <span data-ttu-id="15b90-116">Supprimer une base de données</span><span class="sxs-lookup"><span data-stu-id="15b90-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15b90-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="15b90-117">Prerequisites</span></span>
<span data-ttu-id="15b90-118">Vérifiez que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="15b90-118">Please make sure you have hello following:</span></span>

* <span data-ttu-id="15b90-119">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="15b90-119">An active Azure account.</span></span> <span data-ttu-id="15b90-120">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="15b90-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="15b90-121">Vous pouvez également utiliser hello [Azure Cosmos DB émulateur](local-emulator.md) pour ce didacticiel, si vous souhaitez que toouse un environnement local qui émule les services d’Azure DocumentDB hello à des fins de développement.</span><span class="sxs-lookup"><span data-stu-id="15b90-121">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like toouse a local environment that emulates hello Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="15b90-122">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="15b90-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="15b90-123">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="15b90-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="15b90-124">Commençons par la création d’un compte de base de données Azure Cosmos Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="15b90-124">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="15b90-125">Possédez-vous un compte Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="15b90-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="15b90-126">Dans ce cas, passez directement trop[configurer votre solution Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="15b90-126">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="15b90-127">Possédiez-vous un compte Azure DocumentDB ?</span><span class="sxs-lookup"><span data-stu-id="15b90-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="15b90-128">Si votre compte est maintenant un compte de base de données Azure Cosmos, et que vous pouvez passer trop[configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="15b90-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="15b90-129">Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[configurer votre Solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="15b90-129">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="15b90-130"><a id="SetupVS"></a>Configurer votre solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15b90-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="15b90-131">Ouvrez **Visual Studio** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="15b90-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="15b90-132">Sur hello **fichier** menu, sélectionnez **nouveau**, puis choisissez **projet**.</span><span class="sxs-lookup"><span data-stu-id="15b90-132">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="15b90-133">Bonjour **nouveau projet** boîte de dialogue, sélectionnez **modèles** / **Visual C#** / **l’application Console (.NET Framework)**, nommez votre projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="15b90-133">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="15b90-134">![Capture d’écran de la fenêtre de nouveau projet hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="15b90-134">![Screen shot of hello New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="15b90-135">Bonjour **l’Explorateur de solutions**, cliquez avec le bouton droit sur votre nouvelle application console qui se trouve sous votre solution Visual Studio, et puis cliquez sur **gérer les Packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="15b90-135">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Capture d’écran de hello droite Menu Clicked hello projet](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="15b90-137">Bonjour **NuGet** , cliquez sur **Parcourir**et le type **documentdb** dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="15b90-137">In hello **NuGet** tab, click **Browse**, and type **documentdb** in hello search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="15b90-138">Dans les résultats de hello, recherchez **Microsoft.Azure.DocumentDB** et cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="15b90-138">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="15b90-139">ID de package Hello pour hello Azure Cosmos DB Client Library est [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="15b90-139">hello package ID for hello Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="15b90-140">![Capture d’écran de hello Menu de NuGet pour la recherche de base de données Client SDK Azure Cosmos](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="15b90-140">![Screen shot of hello NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="15b90-141">Si vous obtenez un message sur la vérification des modifications toohello solution, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="15b90-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="15b90-142">Si vous obtenez un message concernant l’acceptation de la licence, cliquez sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="15b90-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="15b90-143"><a id="Connect"></a>Ajoutez les références tooyour projet</span><span class="sxs-lookup"><span data-stu-id="15b90-143"><a id="Connect"></a>Add references tooyour project</span></span>
<span data-ttu-id="15b90-144">les étapes restantes de Hello dans ce didacticiel fournir hello API DocumentDB code des extraits de code requis toocreate et mise à jour de base de données Azure Cosmos ressources dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="15b90-144">hello remaining steps in this tutorial provide hello DocumentDB API code snippets required toocreate and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="15b90-145">Ajoutez d’abord ces applications tooyour de références.</span><span class="sxs-lookup"><span data-stu-id="15b90-145">First, add these references tooyour application.</span></span>
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="15b90-146"><a id="add-references"></a>Connecter votre application</span><span class="sxs-lookup"><span data-stu-id="15b90-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="15b90-147">Ajoutez ces deux constantes et votre variable *client* à votre application.</span><span class="sxs-lookup"><span data-stu-id="15b90-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="15b90-148">Ensuite, head sauvegarde toohello [portail Azure](https://portal.azure.com) tooretrieve votre URL de point de terminaison et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="15b90-148">Then, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="15b90-149">URL de point de terminaison Hello et la clé primaire sont nécessaires pour votre application toounderstand où tooconnect et de base de données Azure Cosmos tootrust connexion de votre application.</span><span class="sxs-lookup"><span data-stu-id="15b90-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="15b90-150">Dans hello portail Azure, accédez de compte de base de données Azure Cosmos tooyour, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**.</span><span class="sxs-lookup"><span data-stu-id="15b90-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="15b90-151">Copiez hello URI à partir du portail de hello et collez-la sur `<your endpoint URL>` dans le fichier program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="15b90-151">Copy hello URI from hello portal and paste it over `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="15b90-152">Copie hello clé primaire à partir du portail de hello et collez-la sur `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="15b90-152">Then copy hello PRIMARY KEY from hello portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="15b90-153">Être vraiment tooremove hello `<` et `>` à partir de vos valeurs.</span><span class="sxs-lookup"><span data-stu-id="15b90-153">Be sure tooremove hello `<` and `>` from your values.</span></span>

![Capture d’écran de hello portail Azure utilisée par toocreate de didacticiel hello NoSQL une application console c#.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="15b90-156"><a id="instantiate"></a>Instancier hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="15b90-156"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span>

<span data-ttu-id="15b90-157">À présent, créez une nouvelle instance de hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="15b90-157">Now, create a new instance of hello **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="15b90-158"><a id="create-database"></a>Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="15b90-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="15b90-159">Ensuite, créez une base de données Azure Cosmos [base de données](documentdb-resources.md#databases) à l’aide de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) méthode ou [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) méthode Hello  **DocumentClient** classe à partir de hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="15b90-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="15b90-160">Une base de données est un conteneur logique de hello JSON de stockage de documents partitionné entre des collections.</span><span class="sxs-lookup"><span data-stu-id="15b90-160">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="15b90-161">Choisir une clé de partition</span><span class="sxs-lookup"><span data-stu-id="15b90-161">Decide on a partition key</span></span> 

<span data-ttu-id="15b90-162">Les collections sont des conteneurs servant au stockage des documents.</span><span class="sxs-lookup"><span data-stu-id="15b90-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="15b90-163">Ce sont des ressources logiques. [Elles peuvent s’étendre sur une ou plusieurs partitions physiques](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="15b90-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="15b90-164">A [clé de partition](documentdb-partition-data.md) est une propriété (ou le chemin d’accès) dans vos documents est utilisée toodistribute vos données entre les serveurs de hello ou les partitions.</span><span class="sxs-lookup"><span data-stu-id="15b90-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used toodistribute your data among hello servers or partitions.</span></span> <span data-ttu-id="15b90-165">Tous les documents dont la même clé de partition sont stockées dans des hello hello même partition.</span><span class="sxs-lookup"><span data-stu-id="15b90-165">All documents with hello same partition key are stored in hello same partition.</span></span> 

<span data-ttu-id="15b90-166">Détermination d’une clé de partition d’est une décision importante de toomake avant de créer une collection.</span><span class="sxs-lookup"><span data-stu-id="15b90-166">Determining a partition key is an important decision toomake before you create a collection.</span></span> <span data-ttu-id="15b90-167">Les clés de partition sont une propriété (ou le chemin d’accès) dans vos documents qui peuvent être utilisées par la base de données Azure Cosmos toodistribute vos données entre plusieurs serveurs ou des partitions.</span><span class="sxs-lookup"><span data-stu-id="15b90-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB toodistribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="15b90-168">COSMOS DB hache la valeur de clé de partition hello et utilise la partition de hello toodetermine hello haché résultat dans le document de hello toostore.</span><span class="sxs-lookup"><span data-stu-id="15b90-168">Cosmos DB hashes hello partition key value and uses hello hashed result toodetermine hello partition in which toostore hello document.</span></span> <span data-ttu-id="15b90-169">Tous les documents dont la même clé de partition sont stockées dans des hello hello même partition, et les clés de partition ne peut pas être modifiés après la création d’une collection.</span><span class="sxs-lookup"><span data-stu-id="15b90-169">All documents with hello same partition key are stored in hello same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="15b90-170">Pour ce didacticiel, nous allons clé de partition tooset hello trop`/deviceId` ainsi que hello toutes les données hello pour un seul périphérique est stocké dans une partition unique.</span><span class="sxs-lookup"><span data-stu-id="15b90-170">For this tutorial, we're going tooset hello partition key too`/deviceId` so that hello all hello data for a single device is stored in a single partition.</span></span> <span data-ttu-id="15b90-171">Vous souhaitez toochoose une clé de partition qui a un grand nombre de valeurs, chacune d’elles servent à hello sur la même fréquence tooensure Cosmos DB peut équilibrer la charge que vos données augmente et obtenir un débit complet de la collection de hello hello.</span><span class="sxs-lookup"><span data-stu-id="15b90-171">You want toochoose a partition key that has a large number of values, each of which are used at about hello same frequency tooensure Cosmos DB can load balance as your data grows and achieve hello full throughput of hello collection.</span></span> 

<span data-ttu-id="15b90-172">Pour plus d’informations sur le partitionnement, consultez [comment toopartition et l’échelle dans la base de données Azure Cosmos ?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="15b90-172">For more information about partitioning, see [How toopartition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="15b90-173"><a id="CreateColl"></a>Créer une collection</span><span class="sxs-lookup"><span data-stu-id="15b90-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="15b90-174">Maintenant que nous savons notre clé de partition, `/deviceId`, permet de créer un [collection](documentdb-resources.md#collections) à l’aide de hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) méthode ou [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) méthode Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="15b90-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="15b90-175">Une collection est un conteneur de documents JSON. Elle est associée à une logique d’application JavaScript.</span><span class="sxs-lookup"><span data-stu-id="15b90-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="15b90-176">Création d’une collection a tarification implications, que vous réservez un débit de toocommunicate d’application hello avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="15b90-176">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="15b90-177">Pour plus d'informations, visitez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="15b90-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
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

<span data-ttu-id="15b90-178">Méthode donc une API REST appeler tooAzure Cosmos DB et hello dispositions de service à un nombre de partitions basé sur le débit hello demandée.</span><span class="sxs-lookup"><span data-stu-id="15b90-178">This method makes a REST API call tooAzure Cosmos DB, and hello service provisions a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="15b90-179">Vous pouvez modifier le débit d’une collection hello besoins évoluent à l’aide de hello SDK ou hello [portail Azure](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="15b90-179">You can change hello throughput of a collection as your performance needs evolve using hello SDK or hello [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="15b90-180"><a id="CreateDoc"></a>Créer des documents JSON</span><span class="sxs-lookup"><span data-stu-id="15b90-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="15b90-181">Insérons maintenant des documents JSON dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="15b90-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="15b90-182">A [document](documentdb-resources.md#documents) peuvent être créés à l’aide de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) méthode Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="15b90-182">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="15b90-183">Les documents sont du contenu JSON (arbitraire) défini par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="15b90-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="15b90-184">Cet exemple de classe contient une lecture de l’appareil et un tooinsert de tooCreateDocumentAsync appel un nouveau périphérique de lecture dans une collection.</span><span class="sxs-lookup"><span data-stu-id="15b90-184">This sample class contains a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a collection.</span></span>

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

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
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
## <a name="read-data"></a><span data-ttu-id="15b90-185">Lire les données</span><span class="sxs-lookup"><span data-stu-id="15b90-185">Read data</span></span>

<span data-ttu-id="15b90-186">Nous allons lire document hello par sa clé de partition et un Id à l’aide de la méthode de ReadDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="15b90-186">Let's read hello document by its partition key and Id using hello ReadDocumentAsync method.</span></span> <span data-ttu-id="15b90-187">Notez que les lectures hello incluent une valeur de PartitionKey (correspondante toohello `x-ms-documentdb-partitionkey` en-tête de demande dans l’API REST de hello).</span><span class="sxs-lookup"><span data-stu-id="15b90-187">Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="15b90-188">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="15b90-188">Update data</span></span>

<span data-ttu-id="15b90-189">Maintenant nous allons mettre à jour des données à l’aide de la méthode de ReplaceDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="15b90-189">Now let's update some data using hello ReplaceDocumentAsync method.</span></span>

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="15b90-190">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="15b90-190">Delete data</span></span>

<span data-ttu-id="15b90-191">Vous permet de supprimer un document par clé de partition et l’id en utilisant la méthode de DeleteDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="15b90-191">Now lets delete a document by partition key and id by using hello DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="15b90-192">Interroger des collections partitionnées</span><span class="sxs-lookup"><span data-stu-id="15b90-192">Query partitioned collections</span></span>

<span data-ttu-id="15b90-193">Lorsque vous interrogez des données dans des collections partitionnées, la base de données Azure Cosmos automatiquement les itinéraires hello partitions toohello de requête correspondant des valeurs de clé de partition toohello spécifiées dans le filtre de hello (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="15b90-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="15b90-194">Par exemple, cette requête est routé toojust hello partition contenant hello clé de partition « XMS-0001 ».</span><span class="sxs-lookup"><span data-stu-id="15b90-194">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="15b90-195">Bonjour requête suivante n’a pas de filtre sur la clé de partition hello (DeviceId) et les partitions tooall où elle est exécutée sur les index de la partition hello est déployée.</span><span class="sxs-lookup"><span data-stu-id="15b90-195">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="15b90-196">Notez que vous avez toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` Bonjour API REST) toohave hello SDK tooexecute une requête sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="15b90-196">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="15b90-197">Exécution de requêtes parallèles</span><span class="sxs-lookup"><span data-stu-id="15b90-197">Parallel query execution</span></span>
<span data-ttu-id="15b90-198">Hello kits de développement Azure Cosmos DB DocumentDB à 1.9.0 et supérieur prennent en charge les options d’exécution de requête parallèle, qui vous permettront d’une latence faible tooperform de requêtes sur les collections partitionnées, même lorsqu’ils ont besoin tootouch un grand nombre de partitions.</span><span class="sxs-lookup"><span data-stu-id="15b90-198">hello Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="15b90-199">Par exemple, hello suivant la requête est configuré toorun en parallèle sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="15b90-199">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="15b90-200">Vous pouvez gérer l’exécution des requêtes parallèles en réglant hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="15b90-200">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="15b90-201">En définissant `MaxDegreeOfParallelism`, vous pouvez contrôler le degré de hello de parallélisme c'est-à-dire hello nombre maximal de partitions de la collection de toohello connexions réseau simultanées.</span><span class="sxs-lookup"><span data-stu-id="15b90-201">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello collection's partitions.</span></span> <span data-ttu-id="15b90-202">Si vous affectez ce trop-1, degré hello de parallélisme est géré par hello SDK.</span><span class="sxs-lookup"><span data-stu-id="15b90-202">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="15b90-203">Si hello `MaxDegreeOfParallelism` n’est pas spécifié ou la valeur de too0, qui est la valeur par défaut de hello, il y aura des partitions d’un réseau unique connexion toohello la collection.</span><span class="sxs-lookup"><span data-stu-id="15b90-203">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello collection's partitions.</span></span>
* <span data-ttu-id="15b90-204">En définissant `MaxBufferedItemCount`, vous pouvez compenser l’utilisation de la mémoire côté client et la latence de la requête.</span><span class="sxs-lookup"><span data-stu-id="15b90-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="15b90-205">Si vous omettez ce paramètre ou cette trop-1, nombre de hello d’éléments mis en mémoire tampon lors de l’exécution de requête parallèle est géré par hello SDK.</span><span class="sxs-lookup"><span data-stu-id="15b90-205">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="15b90-206">Fonction hello même d’état de la collection de hello, une requête parallèle renvoie des résultats dans le même ordre que dans l’exécution séquentielle de hello.</span><span class="sxs-lookup"><span data-stu-id="15b90-206">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="15b90-207">Lorsque vous effectuez une requête de partitions croisées qui inclut le tri (ORDER BY et/ou haut), hello DocumentDB SDK émet des requêtes hello en parallèle sur plusieurs partitions et fusionne les résultats partiellement triés dans hello client côté tooproduce globalement les résultats classés.</span><span class="sxs-lookup"><span data-stu-id="15b90-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello DocumentDB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="15b90-208">Exécuter des procédures stockées</span><span class="sxs-lookup"><span data-stu-id="15b90-208">Execute stored procedures</span></span>
<span data-ttu-id="15b90-209">Enfin, vous pouvez exécuter des transactions atomiques par rapport à des documents avec hello même ID de périphérique, par exemple, si vous gérez des agrégats ou hello du dernier état d’un périphérique dans un document unique en ajoutant hello suivant du projet de code tooyour.</span><span class="sxs-lookup"><span data-stu-id="15b90-209">Lastly, you can execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single document by adding hello following code tooyour project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="15b90-210">Et le tour est joué !</span><span class="sxs-lookup"><span data-stu-id="15b90-210">And that's it!</span></span> <span data-ttu-id="15b90-211">Il s’hello principaux composants d’une application de base de données Azure Cosmos qui utilise une distribution de données de l’échelle de clé tooefficiently partition sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="15b90-211">those are hello main components of an Azure Cosmos DB application that uses a partition key tooefficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="15b90-212">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="15b90-212">Clean up resources</span></span>

<span data-ttu-id="15b90-213">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce didacticiel dans hello portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="15b90-213">If you're not going toocontinue toouse this app, delete all resources created by this tutorial in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="15b90-214">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur le nom unique de hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="15b90-214">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello unique name of hello resource you created.</span></span> 
2. <span data-ttu-id="15b90-215">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="15b90-215">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15b90-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="15b90-216">Next steps</span></span>

<span data-ttu-id="15b90-217">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="15b90-217">In this tutorial, you've done hello following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="15b90-218">Créé un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="15b90-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="15b90-219">Créé une base de données et une collection avec une clé de partition</span><span class="sxs-lookup"><span data-stu-id="15b90-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="15b90-220">Créé des documents JSON</span><span class="sxs-lookup"><span data-stu-id="15b90-220">Created JSON documents</span></span>
> * <span data-ttu-id="15b90-221">Mis à jour un document</span><span class="sxs-lookup"><span data-stu-id="15b90-221">Updated a document</span></span>
> * <span data-ttu-id="15b90-222">Interrogé des collections partitionnées</span><span class="sxs-lookup"><span data-stu-id="15b90-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="15b90-223">Exécuté une procédure stockée</span><span class="sxs-lookup"><span data-stu-id="15b90-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="15b90-224">Supprimé un document</span><span class="sxs-lookup"><span data-stu-id="15b90-224">Deleted a document</span></span>
> * <span data-ttu-id="15b90-225">Supprimé une base de données</span><span class="sxs-lookup"><span data-stu-id="15b90-225">Deleted a database</span></span>

<span data-ttu-id="15b90-226">Vous pouvez maintenant continuer le didacticiel suivant de toohello et importer des données supplémentaires tooyour Cosmos DB compte.</span><span class="sxs-lookup"><span data-stu-id="15b90-226">You can now proceed toohello next tutorial and import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="15b90-227">Importer des données dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="15b90-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
