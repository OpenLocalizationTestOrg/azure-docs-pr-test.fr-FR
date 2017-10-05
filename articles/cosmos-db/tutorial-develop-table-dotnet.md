---
title: "Azure Cosmos DB : développer avec l’API Table dans .NET | Microsoft Docs"
description: "Découvrez comment développer avec l’API Table d’Azure Cosmos DB en utilisant .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 52cb5f2569b6c3a5301752b1e8bfb6cea13ff7f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-develop-with-the-table-api-in-net"></a><span data-ttu-id="de946-103">Azure Cosmos DB : développer avec l’API Table dans .NET</span><span class="sxs-lookup"><span data-stu-id="de946-103">Azure Cosmos DB: Develop with the Table API in .NET</span></span>

<span data-ttu-id="de946-104">Azure Cosmos DB est le service de base de données multi-modèle mondialement distribué de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="de946-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="de946-105">Vous pouvez rapidement créer et interroger des bases de données de documents, de paires clé-valeur et de graphiques, qui bénéficient toutes des fonctionnalités de distribution mondiale et de mise à l’échelle horizontale au cœur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de946-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="de946-106">Ce didacticiel décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="de946-106">This tutorial covers the following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="de946-107">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de946-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="de946-108">Activation des fonctionnalités dans le fichier app.config</span><span class="sxs-lookup"><span data-stu-id="de946-108">Enable functionality in the app.config file</span></span> 
> * <span data-ttu-id="de946-109">Création une table à l’aide de l’[API Table](table-introduction.md) (préversion)</span><span class="sxs-lookup"><span data-stu-id="de946-109">Create a table using the [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="de946-110">Ajout d'une entité à une table</span><span class="sxs-lookup"><span data-stu-id="de946-110">Add an entity to a table</span></span> 
> * <span data-ttu-id="de946-111">Insertion d'un lot d'entités</span><span class="sxs-lookup"><span data-stu-id="de946-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="de946-112">Extraction d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="de946-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="de946-113">Interrogation d’entités à l’aide d’index secondaires automatiques</span><span class="sxs-lookup"><span data-stu-id="de946-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="de946-114">Remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="de946-114">Replace an entity</span></span> 
> * <span data-ttu-id="de946-115">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="de946-115">Delete an entity</span></span> 
> * <span data-ttu-id="de946-116">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="de946-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="de946-117">Tables dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de946-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="de946-118">Azure Cosmos DB fournit l’[API Table](table-introduction.md) (préversion) pour les applications nécessitant un magasin de paires clé-valeur avec une conception sans schéma.</span><span class="sxs-lookup"><span data-stu-id="de946-118">Azure Cosmos DB provides the [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="de946-119">Les Kits de développement logiciel (SDK) et les API REST [Stockage Table Azure](../storage/common/storage-introduction.md) peuvent être utilisés pour travailler avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de946-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used to work with Azure Cosmos DB.</span></span> <span data-ttu-id="de946-120">Vous pouvez faire appel à Azure Cosmos DB pour créer des tables avec des exigences de débit élevées.</span><span class="sxs-lookup"><span data-stu-id="de946-120">You can use Azure Cosmos DB to create tables with high throughput requirements.</span></span> <span data-ttu-id="de946-121">Azure Cosmos DB prend en charge les tables optimisées en débit (appelées de façon informelle « tables premium »), actuellement en préversion publique.</span><span class="sxs-lookup"><span data-stu-id="de946-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="de946-122">Vous pouvez continuer à utiliser le stockage Table Azure pour les tables présentant des exigences de débit et de stockage inférieures.</span><span class="sxs-lookup"><span data-stu-id="de946-122">You can continue to use Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="de946-123">Azure Cosmos DB introduira la prise en charge des tables optimisées pour le stockage dans une prochaine mise à jour, et les comptes de stockage Table Azure nouveaux ou existants seront mis à niveau en toute transparence vers Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de946-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded to Azure Cosmos DB.</span></span>

<span data-ttu-id="de946-124">Si vous utilisez actuellement le stockage Table Azure, vous bénéficiez des avantages suivants avec la préversion des « tables premium » :</span><span class="sxs-lookup"><span data-stu-id="de946-124">If you currently use Azure Table storage, you gain the following benefits with the "premium table" preview:</span></span>

- <span data-ttu-id="de946-125">[Distribution mondiale](distribute-data-globally.md) clé en main avec multihébergement et [basculements automatiques et manuels](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="de946-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="de946-126">Prise en charge de l’indexation automatique indépendante du schéma par rapport à toutes les propriétés (« index secondaires »), et requêtes rapides</span><span class="sxs-lookup"><span data-stu-id="de946-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="de946-127">Prise en charge de la [mise à l’échelle indépendante du stockage et du débit](partition-data.md) pour autant de régions que nécessaire</span><span class="sxs-lookup"><span data-stu-id="de946-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="de946-128">Prise en charge du [débit dédié par table](request-units.md), qui peut être mis à l’échelle de quelques centaines à plusieurs millions de requêtes par seconde</span><span class="sxs-lookup"><span data-stu-id="de946-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds to millions of requests per second</span></span>
- <span data-ttu-id="de946-129">Prise en charge de [cinq niveaux de cohérence ajustables](consistency-levels.md) pour trouver le bon compromis entre disponibilité, latence et cohérence en fonction des besoins de votre application</span><span class="sxs-lookup"><span data-stu-id="de946-129">Support for [five tunable consistency levels](consistency-levels.md) to trade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="de946-130">Disponibilité de 99,99 % dans une région unique, possibilité d’ajouter d’autres régions pour augmenter la disponibilité et [contrats SLA complets à la pointe du secteur](https://azure.microsoft.com/support/legal/sla/cosmos-db/) sur la disponibilité générale</span><span class="sxs-lookup"><span data-stu-id="de946-130">99.99% availability within a single region, and ability to add more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="de946-131">Possibilité de travailler avec le Kit de développement logiciel (SDK) .NET Stockage Azure existant et aucune modification du code de votre application requise</span><span class="sxs-lookup"><span data-stu-id="de946-131">Work with the existing Azure storage .NET SDK, and no code changes to your application</span></span>

<span data-ttu-id="de946-132">Dans la préversion, Azure Cosmos DB prend en charge l’API Table à l’aide du Kit de développement logiciel (SDK) .NET.</span><span class="sxs-lookup"><span data-stu-id="de946-132">During the preview, Azure Cosmos DB supports the Table API using the .NET SDK.</span></span> <span data-ttu-id="de946-133">Vous pouvez télécharger le [Kit de développement logiciel (SDK) de la préversion de Stockage Azure](https://aka.ms/premiumtablenuget) à partir de NuGet. Il présente les mêmes classes et signatures de méthode que le [Kit de développement logiciel (SDK) Stockage Azure](https://www.nuget.org/packages/WindowsAzure.Storage), mais il peut également se connecter à des comptes Azure Cosmos DB à l’aide de l’API Table.</span><span class="sxs-lookup"><span data-stu-id="de946-133">You can download the [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has the same classes and method signatures as the [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect to Azure Cosmos DB accounts using the Table API.</span></span>

<span data-ttu-id="de946-134">Pour en savoir plus sur les tâches de stockage Table Azure complexes, consultez :</span><span class="sxs-lookup"><span data-stu-id="de946-134">To learn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="de946-135">Présentation d’Azure Cosmos DB : API Table</span><span class="sxs-lookup"><span data-stu-id="de946-135">Introduction to Azure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="de946-136">La documentation de référence du service de Table pour des informations complètes sur les API disponibles : [Référence de la bibliothèque cliente de stockage pour .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="de946-136">The Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="de946-137">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="de946-137">About this tutorial</span></span>
<span data-ttu-id="de946-138">Ce didacticiel est destiné aux développeurs familiarisés avec le Kit de développement logiciel (SDK) Stockage Table Azure qui souhaitent utiliser les fonctionnalités premium offertes par Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de946-138">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="de946-139">Basé sur le didacticiel [Prise en main du stockage de tables Azure à l’aide de .NET](table-storage-how-to-use-dotnet.md), il montre comment tirer parti des fonctionnalités supplémentaires telles que les index secondaires, le débit approvisionné et le multihébergement.</span><span class="sxs-lookup"><span data-stu-id="de946-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="de946-140">Nous expliquons comment utiliser le portail Azure pour créer un compte Azure Cosmos DB, puis créer et déployer une application Table.</span><span class="sxs-lookup"><span data-stu-id="de946-140">We cover how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="de946-141">Nous passons également en revue des exemples .NET pour la création et la suppression d’une table, et l’insertion, la mise à jour, la suppression et l’interrogation de données de table.</span><span class="sxs-lookup"><span data-stu-id="de946-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="de946-142">Si vous n’avez pas encore installé Visual Studio 2017, vous pouvez télécharger et utiliser la version **gratuite** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="de946-142">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="de946-143">Veillez à activer **le développement Azure** lors de l’installation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de946-143">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="de946-144">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="de946-144">Create a database account</span></span>

<span data-ttu-id="de946-145">Commençons par créer un compte Azure Cosmos DB dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="de946-145">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="de946-146">Vous possédez déjà un compte Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="de946-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="de946-147">Si c’est le cas, passez directement à l’étape [Configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="de946-147">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="de946-148">Vous possédiez un compte Azure DocumentDB ?</span><span class="sxs-lookup"><span data-stu-id="de946-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="de946-149">Si c’est le cas, votre compte a été converti en compte Azure Cosmos DB et vous pouvez passer directement à l’étape [Configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="de946-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="de946-150">Si vous utilisez l’émulateur Azure Cosmos DB, suivez les étapes de la section [Émulateur Azure Cosmos DB](local-emulator.md) pour le configurer, puis passez directement à l’étape [Configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="de946-150">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting to any location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-the-sample-application"></a><span data-ttu-id="de946-151">Clonage de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="de946-151">Clone the sample application</span></span>

<span data-ttu-id="de946-152">À présent, nous allons cloner une application Table à partir de GitHub, configurer la chaîne de connexion et l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="de946-152">Now let's clone a Table app from github, set the connection string, and run it.</span></span>

1. <span data-ttu-id="de946-153">Ouvrez une fenêtre de terminal git, comme git bash, et accédez à un répertoire de travail à l’aide de la commande `cd`.</span><span class="sxs-lookup"><span data-stu-id="de946-153">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="de946-154">Exécutez la commande suivante pour cloner l’exemple de référentiel.</span><span class="sxs-lookup"><span data-stu-id="de946-154">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="de946-155">Ouvrez le fichier de solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de946-155">Then open the solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="de946-156">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="de946-156">Update your connection string</span></span>

<span data-ttu-id="de946-157">Maintenant, retournez dans le portail Azure afin d’obtenir les informations de votre chaîne de connexion et de les copier dans l’application.</span><span class="sxs-lookup"><span data-stu-id="de946-157">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="de946-158">Dans le [portail Azure](http://portal.azure.com/), dans votre compte Azure Cosmos DB, dans le volet de navigation de gauche, cliquez sur **Clés**, puis sur **Clés en lecture-écriture**.</span><span class="sxs-lookup"><span data-stu-id="de946-158">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="de946-159">Vous utiliserez le bouton Copier sur le côté droit de l’écran pour copier la chaîne de connexion dans le fichier app.config à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="de946-159">You'll use the copy buttons on the right side of the screen to copy the connection string into the app.config file in the next step.</span></span>

2. <span data-ttu-id="de946-160">Dans Visual Studio, ouvrez le fichier app.config.</span><span class="sxs-lookup"><span data-stu-id="de946-160">In Visual Studio, open the app.config file.</span></span> 

3. <span data-ttu-id="de946-161">Copiez la valeur de votre URI dans le portail (à l’aide du bouton Copier) et définissez-la comme valeur de la clé du compte dans le fichier app.config. Utilisez le nom du compte créé précédemment pour le nom du compte dans app.config.</span><span class="sxs-lookup"><span data-stu-id="de946-161">Copy your URI value from the portal (using the copy button) and make it the value of the account-key in app.config. Use the account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="de946-162">Pour utiliser cette application avec le service Stockage Table Azure standard, vous devez modifier la chaîne de connexion dans `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="de946-162">To use this app with standard Azure Table Storage, you need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="de946-163">Utilisez le nom du compte en tant que nom du compte Table et la clé en tant que clé primaire de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="de946-163">Use the account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-the-app"></a><span data-ttu-id="de946-164">Génération et déploiement de l’application</span><span class="sxs-lookup"><span data-stu-id="de946-164">Build and deploy the app</span></span>
1. <span data-ttu-id="de946-165">Dans Visual Studio, cliquez avec le bouton droit sur le nom du projet dans l’**Explorateur de solutions**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="de946-165">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="de946-166">Dans la zone **Parcourir** de NuGet, tapez ***WindowsAzure.Storage-PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="de946-166">In the NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="de946-167">Cochez la case **Inclure les préversions**.</span><span class="sxs-lookup"><span data-stu-id="de946-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="de946-168">À partir des résultats, installez **WindowsAzure.Storage-PremiumTable** et choisissez la version d’évaluation `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="de946-168">From the results, install the **WindowsAzure.Storage-PremiumTable** and choose the preview build `0.0.1-preview`.</span></span> <span data-ttu-id="de946-169">Cette action installe le package de stockage Table Azure et toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="de946-169">This action installs the Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="de946-170">Appuyez sur Ctrl + F5 pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="de946-170">Click CTRL + F5 to run the application.</span></span> 

<span data-ttu-id="de946-171">Vous pouvez maintenant revenir à l’Explorateur de données et voir la requête, effectuer des modifications et travailler avec ces données de table.</span><span class="sxs-lookup"><span data-stu-id="de946-171">You can now go back to Data Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="de946-172">Pour utiliser cette application avec un émulateur Azure Cosmos DB, il vous suffit de modifier la chaîne de connexion dans `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="de946-172">To use this app with an Azure Cosmos DB Emulator, you just need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="de946-173">Utilisez la valeur ci-dessous pour l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="de946-173">Use the below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="de946-174">Fonctionnalités d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de946-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="de946-175">Azure Cosmos DB prend en charge un certain nombre de fonctionnalités qui ne sont pas disponibles dans l’API de stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="de946-175">Azure Cosmos DB supports a number of capabilities that are not available in the Azure Table storage API.</span></span> <span data-ttu-id="de946-176">Les nouvelles fonctionnalités peuvent être activées à l’aide des valeurs de configuration `appSettings` suivantes.</span><span class="sxs-lookup"><span data-stu-id="de946-176">The new functionality can be enabled via the following `appSettings` configuration values.</span></span> <span data-ttu-id="de946-177">Nous n’avons pas introduit de nouvelles signatures ou surcharges dans la préversion du Kit de développement logiciel (SDK) Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="de946-177">We did not introduce any new signatures or overloads to the preview Azure Storage SDK.</span></span> <span data-ttu-id="de946-178">Vous pouvez ainsi vous connecter aussi bien à des tables standard que premium, et travailler avec d’autres services de stockage Azure, tels que les objets blob et les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="de946-178">This allows you to connect to both standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="de946-179">Clé</span><span class="sxs-lookup"><span data-stu-id="de946-179">Key</span></span> | <span data-ttu-id="de946-180">Description</span><span class="sxs-lookup"><span data-stu-id="de946-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de946-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="de946-181">TableConnectionMode</span></span>  | <span data-ttu-id="de946-182">Azure Cosmos DB prend en charge deux modes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="de946-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="de946-183">Dans le mode `Gateway`, les requêtes sont toujours effectuées auprès de la passerelle Azure Cosmos DB, qui les transmet aux partitions de données correspondantes.</span><span class="sxs-lookup"><span data-stu-id="de946-183">In `Gateway` mode, requests are always made to the Azure Cosmos DB gateway, which forwards it to the corresponding data partitions.</span></span> <span data-ttu-id="de946-184">Dans le mode de connectivité `Direct`, le client lit le mappage des tables aux partitions, et les requêtes sont effectuées directement dans les partitions de données.</span><span class="sxs-lookup"><span data-stu-id="de946-184">In `Direct` connectivity mode, the client fetches the mapping of tables to partitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="de946-185">Nous recommandons d’utiliser le mode `Direct` (il s’agit du mode par défaut).</span><span class="sxs-lookup"><span data-stu-id="de946-185">We recommend `Direct`, the default.</span></span>  |
| <span data-ttu-id="de946-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="de946-186">TableConnectionProtocol</span></span> | <span data-ttu-id="de946-187">Azure Cosmos DB prend en charge deux protocoles de connexion : `Https` et `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="de946-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="de946-188">`Tcp` est la valeur par défaut. C’est le protocole recommandé, car il est plus léger.</span><span class="sxs-lookup"><span data-stu-id="de946-188">`Tcp` is the default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="de946-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="de946-189">TablePreferredLocations</span></span> | <span data-ttu-id="de946-190">Liste séparée par des virgules des emplacements (de multihébergement) préférés pour les lectures.</span><span class="sxs-lookup"><span data-stu-id="de946-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="de946-191">Chaque compte Azure Cosmos DB peut être associé à un nombre de régions compris entre un et plus de 30.</span><span class="sxs-lookup"><span data-stu-id="de946-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="de946-192">Chaque instance de client peut spécifier un sous-ensemble de ces régions dans l’ordre de préférence pour des lectures à faible latence.</span><span class="sxs-lookup"><span data-stu-id="de946-192">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="de946-193">Les régions doivent être nommées à l’aide de leurs [noms d’affichage](https://msdn.microsoft.com/library/azure/gg441293.aspx), par exemple, `West US`.</span><span class="sxs-lookup"><span data-stu-id="de946-193">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="de946-194">Voir également [API multihébergement](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="de946-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="de946-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="de946-195">TableConsistencyLevel</span></span> | <span data-ttu-id="de946-196">Vous pouvez trouver un compromis entre latence, cohérence et disponibilité en choisissant l’un des cinq niveaux de cohérence bien définis disponibles : `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` et `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="de946-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="de946-197">La valeur par défaut est `Session`.</span><span class="sxs-lookup"><span data-stu-id="de946-197">Default is `Session`.</span></span> <span data-ttu-id="de946-198">Le choix du niveau de cohérence a une influence considérable sur les performances dans les configurations multirégions.</span><span class="sxs-lookup"><span data-stu-id="de946-198">The choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="de946-199">Pour plus d’informations, consultez [Niveaux de cohérence](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="de946-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="de946-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="de946-200">TableThroughput</span></span> | <span data-ttu-id="de946-201">Débit réservé pour la table, exprimé en unités de requête (RU) par seconde.</span><span class="sxs-lookup"><span data-stu-id="de946-201">Reserved throughput for the table expressed in request units (RU) per second.</span></span> <span data-ttu-id="de946-202">Les tables uniques peuvent prendre en charge plusieurs centaines de millions de RU/s.</span><span class="sxs-lookup"><span data-stu-id="de946-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="de946-203">Voir [Unités de requête](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="de946-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="de946-204">La valeur par défaut est `400`.</span><span class="sxs-lookup"><span data-stu-id="de946-204">Default is `400`</span></span> |
| <span data-ttu-id="de946-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="de946-205">TableIndexingPolicy</span></span> | <span data-ttu-id="de946-206">Indexation cohérente et automatique de toutes les colonnes que contiennent les tables.</span><span class="sxs-lookup"><span data-stu-id="de946-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="de946-207">Chaîne JSON conforme à la spécification de la stratégie d’indexation.</span><span class="sxs-lookup"><span data-stu-id="de946-207">JSON string conforming to the indexing policy specification.</span></span> <span data-ttu-id="de946-208">Pour savoir comment modifier la stratégie d’indexation de manière à inclure/exclure des colonnes spécifiques, consultez [Stratégie d’indexation](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="de946-208">See [Indexing Policy](indexing-policies.md) to see how you can change indexing policy to include/exclude specific columns.</span></span> | <span data-ttu-id="de946-209">Indexation automatique de toutes les propriétés (hachage pour les chaînes et plage pour les nombres).</span><span class="sxs-lookup"><span data-stu-id="de946-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="de946-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="de946-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="de946-211">Configurez le nombre maximal d’éléments renvoyés par requête de table en un seul aller-retour.</span><span class="sxs-lookup"><span data-stu-id="de946-211">Configure the maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="de946-212">La valeur par défaut, `-1`, laisse Azure Cosmos DB déterminer dynamiquement la valeur lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="de946-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |
| <span data-ttu-id="de946-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="de946-213">TableQueryEnableScan</span></span> | <span data-ttu-id="de946-214">Si la requête ne peut pas utiliser l’index pour des filtres, vous pouvez l’exécuter malgré tout via une analyse.</span><span class="sxs-lookup"><span data-stu-id="de946-214">If the query cannot use the index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="de946-215">La valeur par défaut est `false`.</span><span class="sxs-lookup"><span data-stu-id="de946-215">Default is `false`.</span></span>|
| <span data-ttu-id="de946-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="de946-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="de946-217">Degré de parallélisme pour l’exécution d’une requête sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="de946-217">The degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="de946-218">`0` correspond à une exécution en série sans pré-extraction, `1` à une exécution en série avec pré-extraction et les valeurs plus élevées augmentent le taux de parallélisme.</span><span class="sxs-lookup"><span data-stu-id="de946-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase the rate of parallelism.</span></span> <span data-ttu-id="de946-219">La valeur par défaut, `-1`, laisse Azure Cosmos DB déterminer dynamiquement la valeur lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="de946-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |

<span data-ttu-id="de946-220">Pour modifier la valeur par défaut, ouvrez le fichier `app.config` à partir de l’Explorateur de solutions dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de946-220">To change the default value, open the `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="de946-221">Ajoutez le contenu de l’élément `<appSettings>` indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="de946-221">Add the contents of the `<appSettings>` element shown below.</span></span> <span data-ttu-id="de946-222">Remplacez `account-name` par le nom de votre compte de stockage et `account-key` par votre clé d’accès au compte.</span><span class="sxs-lookup"><span data-stu-id="de946-222">Replace `account-name` with the name of your storage account, and `account-key` with your account access key.</span></span> 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

<span data-ttu-id="de946-223">Passons rapidement en revue ce qui se passe dans l’application.</span><span class="sxs-lookup"><span data-stu-id="de946-223">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="de946-224">Ouvrez le fichier `Program.cs` ; vous pouvez constater que ces lignes de code créent les ressources de table.</span><span class="sxs-lookup"><span data-stu-id="de946-224">Open the `Program.cs` file and you find that these lines of code create the Table resources.</span></span> 

## <a name="create-the-table-client"></a><span data-ttu-id="de946-225">Création du client de tables</span><span class="sxs-lookup"><span data-stu-id="de946-225">Create the table client</span></span>
<span data-ttu-id="de946-226">Vous initialisez un `CloudTableClient` pour vous connecter au compte de tables.</span><span class="sxs-lookup"><span data-stu-id="de946-226">You initialize a `CloudTableClient` to connect to the table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="de946-227">Ce client est initialisé à l’aide des valeurs de configuration `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel` et `TablePreferredLocations` si elles sont spécifiées dans les paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="de946-227">This client is initialized using the `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in the app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="de946-228">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="de946-228">Create a table</span></span>
<span data-ttu-id="de946-229">Ensuite, vous créez une table à l’aide de `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="de946-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="de946-230">Dans Azure Cosmos DB, le stockage et le débit peuvent être mis à l’échelle indépendamment pour chaque table, et le partitionnement est géré automatiquement par le service.</span><span class="sxs-lookup"><span data-stu-id="de946-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by the service.</span></span> <span data-ttu-id="de946-231">Azure Cosmos DB prend à la fois en charge une taille fixe et un nombre illimité de tables.</span><span class="sxs-lookup"><span data-stu-id="de946-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="de946-232">Pour plus d’informations, consultez [Partitionnement dans Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="de946-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="de946-233">Il existe une différence importante dans la façon dont les tables sont créées.</span><span class="sxs-lookup"><span data-stu-id="de946-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="de946-234">Azure Cosmos DB réserve le débit, contrairement au modèle du stockage Azure pour les transactions, basé sur la consommation.</span><span class="sxs-lookup"><span data-stu-id="de946-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="de946-235">Le modèle de réservation présente deux avantages principaux :</span><span class="sxs-lookup"><span data-stu-id="de946-235">The reservation model has two key benefits:</span></span>

* <span data-ttu-id="de946-236">Le débit est dédié/réservé, ce qui fait que vous n’êtes jamais limité si le taux de requêtes est inférieur ou égal à votre débit approvisionné.</span><span class="sxs-lookup"><span data-stu-id="de946-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="de946-237">Le modèle de réservation est plus [économique pour les charges de travail nécessitant beaucoup de débit](key-value-store-cost.md).</span><span class="sxs-lookup"><span data-stu-id="de946-237">The reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="de946-238">Vous pouvez configurer le débit par défaut en configurant le nombre de RU (unités de requête) par seconde pour le paramètre de `TableThroughput`.</span><span class="sxs-lookup"><span data-stu-id="de946-238">You can configure the default throughput by configuring the setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="de946-239">Une lecture d’une entité de 1 Ko est normalisée à 1 RU, et les autres opérations sont normalisées à une valeur de RU fixe en fonction de leur consommation de ressources processeur, de mémoire et d’E/S par seconde.</span><span class="sxs-lookup"><span data-stu-id="de946-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized to a fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="de946-240">En savoir plus sur les [Unités de requête dans Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="de946-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="de946-241">Bien que le Kit de développement logiciel (SDK) Stockage Table ne prenne pas en charge la modification du débit pour le moment, vous pouvez modifier le débit instantanément à tout moment via le portail Azure ou l’interface CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="de946-241">While Table storage SDK does not currently support modifying throughput, you can change the throughput instantaneously at any time using the Azure portal or Azure CLI.</span></span>

<span data-ttu-id="de946-242">Maintenant, nous allons passer en revue les opérations de lecture et d’écriture (CRUD) simples avec le Kit de développement logiciel (SDK) Stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="de946-242">Next, we walk through the simple read and write (CRUD) operations using the Azure Table storage SDK.</span></span> <span data-ttu-id="de946-243">Ce didacticiel démontre les latences prévisibles faibles, de l’ordre de quelques millisecondes, et les requêtes rapides assurées par Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de946-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="de946-244">Ajout d'une entité à une table</span><span class="sxs-lookup"><span data-stu-id="de946-244">Add an entity to a table</span></span>
<span data-ttu-id="de946-245">Les entités du stockage Table Azure partent de la classe `TableEntity` et doivent présenter des propriétés `PartitionKey` et `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="de946-245">Entities in Azure Table storage extend from the `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="de946-246">Voici un exemple de définition d’une entité de client.</span><span class="sxs-lookup"><span data-stu-id="de946-246">Here's a sample definition for a customer entity.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="de946-247">L’extrait de code suivant montre comment insérer une entité avec le Kit de développement logiciel (SDK) Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="de946-247">The following snippet shows how to insert an entity with the Azure storage SDK.</span></span> <span data-ttu-id="de946-248">Azure Cosmos DB est conçu pour garantir une latence faible à n’importe quelle échelle, partout dans le monde.</span><span class="sxs-lookup"><span data-stu-id="de946-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across the world.</span></span>

<span data-ttu-id="de946-249">Pour les applications exécutées dans la même région que le compte Azure Cosmos DB, 99 % des écritures prennent moins de 15 ms, 50 % d’entre elles prenant moins de 6 ms environ.</span><span class="sxs-lookup"><span data-stu-id="de946-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in the same region as the Azure Cosmos DB account.</span></span> <span data-ttu-id="de946-250">Cette durée tient compte du fait que les écritures sont confirmées au client seulement une fois qu’elles ont été répliquées de manière synchrone, validées durablement, et que tout le contenu a été indexé.</span><span class="sxs-lookup"><span data-stu-id="de946-250">And this duration accounts for the fact that writes are acknowledged back to the client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="de946-251">L’API Table pour Azure Cosmos DB est en préversion.</span><span class="sxs-lookup"><span data-stu-id="de946-251">The Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="de946-252">Dès la mise à la disposition générale, les garanties de latence pour 99 % des opérations seront soutenues par des contrats SLA, comme les autres API Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de946-252">At general availability, the p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="de946-253">Insertion d'un lot d'entités</span><span class="sxs-lookup"><span data-stu-id="de946-253">Insert a batch of entities</span></span>
<span data-ttu-id="de946-254">Le stockage Table Azure prend en charge une API d’opération par lot qui permet de combiner des mises à jour, des suppressions et des insertions dans la même opération par lot.</span><span class="sxs-lookup"><span data-stu-id="de946-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in the same single batch operation.</span></span> <span data-ttu-id="de946-255">Azure Cosmos DB ne présente pas certaines des restrictions du stockage Table Azure pour cette API.</span><span class="sxs-lookup"><span data-stu-id="de946-255">Azure Cosmos DB does not have some of the limitations on the batch API as Azure Table storage.</span></span> <span data-ttu-id="de946-256">Par exemple, vous pouvez effectuer plusieurs lectures dans un lot, effectuer plusieurs écritures sur la même entité d’un lot, et il n’existe pas de limite de 100 opérations par lot.</span><span class="sxs-lookup"><span data-stu-id="de946-256">For example, you can perform multiple reads within a batch, you can perform multiple writes to the same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="de946-257">Extraction d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="de946-257">Retrieve a single entity</span></span>
<span data-ttu-id="de946-258">Dans la même région Azure, 99 % des extractions dans Azure Cosmos DB prennent moins de 10 ms, 50 % d’entre elles prenant moins de 1 ms environ.</span><span class="sxs-lookup"><span data-stu-id="de946-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in the same Azure region.</span></span> <span data-ttu-id="de946-259">Vous pouvez ajouter autant de régions à votre compte pour bénéficier de lectures à faible latence, et déployer les applications de sorte qu’elles effectuent les lectures à partir de leur région locale (applications dites « multihébergées ») en définissant `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="de946-259">You can add as many regions to your account for low latency reads, and deploy applications to read from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="de946-260">Vous pouvez récupérer une entité unique à l’aide de l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="de946-260">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="de946-261">Pour plus d’informations sur les API multihébergement, consultez [Développement avec plusieurs régions](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="de946-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="de946-262">Interrogation d’entités à l’aide d’index secondaires automatiques</span><span class="sxs-lookup"><span data-stu-id="de946-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="de946-263">Les tables peuvent être interrogées à l’aide de la classe `TableQuery`.</span><span class="sxs-lookup"><span data-stu-id="de946-263">Tables can be queried using the `TableQuery` class.</span></span> <span data-ttu-id="de946-264">Azure Cosmos DB intègre un moteur de base de données optimisé pour l’écriture qui indexe automatiquement toutes les colonnes de votre table.</span><span class="sxs-lookup"><span data-stu-id="de946-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="de946-265">L’indexation dans Azure Cosmos DB est indépendante du schéma.</span><span class="sxs-lookup"><span data-stu-id="de946-265">Indexing in Azure Cosmos DB is agnostic to schema.</span></span> <span data-ttu-id="de946-266">Par conséquent, même si votre schéma est différent entre les lignes, ou s’il évolue au fil du temps, il est automatiquement indexé.</span><span class="sxs-lookup"><span data-stu-id="de946-266">Therefore, even if your schema is different between rows, or if the schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="de946-267">Comme Azure Cosmos DB prend en charge les index secondaires automatiques, les requêtes sur n’importe quelle propriété peuvent utiliser l’index et être traitées efficacement.</span><span class="sxs-lookup"><span data-stu-id="de946-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use the index and be served efficiently.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

<span data-ttu-id="de946-268">En préversion, Azure Cosmos DB prend en charge les mêmes fonctionnalités de requête que le stockage Table Azure pour l’API Table.</span><span class="sxs-lookup"><span data-stu-id="de946-268">In preview, Azure Cosmos DB supports the same query functionality as Azure Table storage for the Table API.</span></span> <span data-ttu-id="de946-269">Azure Cosmos DB prend également en charge le tri, les agrégats, les requêtes géospatiales, les hiérarchies et un large éventail de fonctions intégrées.</span><span class="sxs-lookup"><span data-stu-id="de946-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="de946-270">Les fonctionnalités supplémentaires seront ajoutées à l’API Table dans une prochaine mise à jour de service.</span><span class="sxs-lookup"><span data-stu-id="de946-270">The additional functionality will be provided in the Table API in a future service update.</span></span> <span data-ttu-id="de946-271">Pour une vue d’ensemble de ces fonctionnalités, consultez [Azure Cosmos DB query](documentdb-sql-query.md) (Requête dans Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="de946-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="de946-272">Remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="de946-272">Replace an entity</span></span>
<span data-ttu-id="de946-273">Pour mettre à jour une entité, récupérez-la du service de Table, modifiez l’objet d’entité, puis enregistrez les modifications dans le service de Table.</span><span class="sxs-lookup"><span data-stu-id="de946-273">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="de946-274">Le code suivant modifie le numéro de téléphone d'un client existant.</span><span class="sxs-lookup"><span data-stu-id="de946-274">The following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="de946-275">De même, vous pouvez effectuer des opérations `InsertOrMerge` ou `Merge`.</span><span class="sxs-lookup"><span data-stu-id="de946-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="de946-276">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="de946-276">Delete an entity</span></span>
<span data-ttu-id="de946-277">Il est facile de supprimer une entité après l’avoir récupérée. Il suffit pour cela d’utiliser la procédure suivie pour la mise à jour d’une entité.</span><span class="sxs-lookup"><span data-stu-id="de946-277">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="de946-278">Le code suivant extrait et supprime une entité de client.</span><span class="sxs-lookup"><span data-stu-id="de946-278">The following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="de946-279">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="de946-279">Delete a table</span></span>
<span data-ttu-id="de946-280">Pour finir, l’exemple de code suivant supprime une table d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="de946-280">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="de946-281">Vous pouvez supprimer et recréer une table immédiatement avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de946-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="de946-282">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="de946-282">Clean up resources</span></span> 

<span data-ttu-id="de946-283">Si vous ne prévoyez pas de continuer à utiliser cette application, utilisez les étapes suivantes pour supprimer toutes les ressources créées par ce didacticiel dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="de946-283">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>   

1. <span data-ttu-id="de946-284">Dans le menu de gauche du portail Azure, cliquez sur **Groupes de ressources**, puis sur le nom de la ressource que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="de946-284">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span>  
2. <span data-ttu-id="de946-285">Dans la page de votre groupe de ressources, cliquez sur **Supprimer**, tapez le nom de la ressource à supprimer dans la zone de texte, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="de946-285">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="de946-286">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="de946-286">Next steps</span></span>

<span data-ttu-id="de946-287">Dans ce didacticiel, nous avons vu comment prendre en main Azure Cosmos DB avec l’API Table, et vous avez effectué les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="de946-287">In this tutorial, we covered how to get started using Azure Cosmos DB with the Table API, and you've done the following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="de946-288">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de946-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="de946-289">Activation des fonctionnalités dans le fichier app.config</span><span class="sxs-lookup"><span data-stu-id="de946-289">Enabled functionality in the app.config file</span></span> 
> * <span data-ttu-id="de946-290">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="de946-290">Created a table</span></span> 
> * <span data-ttu-id="de946-291">Ajout d’une entité à une table</span><span class="sxs-lookup"><span data-stu-id="de946-291">Added an entity to a table</span></span> 
> * <span data-ttu-id="de946-292">Insertion d’un lot d’entités</span><span class="sxs-lookup"><span data-stu-id="de946-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="de946-293">Extraction d’une seule entité</span><span class="sxs-lookup"><span data-stu-id="de946-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="de946-294">Interrogation d’entités à l’aide d’index secondaires automatiques</span><span class="sxs-lookup"><span data-stu-id="de946-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="de946-295">Remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="de946-295">Replaced an entity</span></span> 
> * <span data-ttu-id="de946-296">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="de946-296">Deleted an entity</span></span> 
> * <span data-ttu-id="de946-297">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="de946-297">Deleted a table</span></span>  

<span data-ttu-id="de946-298">Vous pouvez maintenant passer au didacticiel suivant pour en savoir plus sur l’interrogation de données de table.</span><span class="sxs-lookup"><span data-stu-id="de946-298">You can now proceed to the next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="de946-299">Exécution de requêtes avec l’API Table</span><span class="sxs-lookup"><span data-stu-id="de946-299">Query with the Table API</span></span>](tutorial-query-table.md)
