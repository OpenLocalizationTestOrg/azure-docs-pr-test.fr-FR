---
title: "Azure Cosmos DB : Développer avec hello API de Table dans .NET | Documents Microsoft"
description: "Découvrez comment toodevelop avec l’API de Table Azure Cosmos DB à l’aide de .NET"
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
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a><span data-ttu-id="47723-103">Azure Cosmos DB : Développer avec hello dans .NET, les API de Table</span><span class="sxs-lookup"><span data-stu-id="47723-103">Azure Cosmos DB: Develop with hello Table API in .NET</span></span>

<span data-ttu-id="47723-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="47723-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="47723-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="47723-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="47723-106">Ce didacticiel couvre hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="47723-106">This tutorial covers hello following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="47723-107">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="47723-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="47723-108">Activer la fonctionnalité dans le fichier app.config hello</span><span class="sxs-lookup"><span data-stu-id="47723-108">Enable functionality in hello app.config file</span></span> 
> * <span data-ttu-id="47723-109">Créer une table à l’aide de hello [API Table](table-introduction.md) (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="47723-109">Create a table using hello [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="47723-110">Ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="47723-110">Add an entity tooa table</span></span> 
> * <span data-ttu-id="47723-111">Insertion d’un lot d’entités</span><span class="sxs-lookup"><span data-stu-id="47723-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="47723-112">Extraction d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="47723-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="47723-113">Interrogation d’entités à l’aide d’index secondaires automatiques</span><span class="sxs-lookup"><span data-stu-id="47723-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="47723-114">Remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="47723-114">Replace an entity</span></span> 
> * <span data-ttu-id="47723-115">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="47723-115">Delete an entity</span></span> 
> * <span data-ttu-id="47723-116">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="47723-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="47723-117">Tables dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="47723-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="47723-118">Base de données Azure Cosmos fournit hello [Table API](table-introduction.md) (aperçu) pour les applications qui ont besoin d’un magasin clé-valeur avec une conception sans schéma.</span><span class="sxs-lookup"><span data-stu-id="47723-118">Azure Cosmos DB provides hello [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="47723-119">[Stockage de Table Azure](../storage/common/storage-introduction.md) kits de développement logiciel et les API REST peuvent être toowork utilisé avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="47723-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used toowork with Azure Cosmos DB.</span></span> <span data-ttu-id="47723-120">Vous pouvez utiliser des tables de base de données Azure Cosmos toocreate aux exigences de débit élevé.</span><span class="sxs-lookup"><span data-stu-id="47723-120">You can use Azure Cosmos DB toocreate tables with high throughput requirements.</span></span> <span data-ttu-id="47723-121">Azure Cosmos DB prend en charge les tables optimisées en débit (appelées de façon informelle « tables premium »), actuellement en préversion publique.</span><span class="sxs-lookup"><span data-stu-id="47723-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="47723-122">Vous pouvez continuer toouse stockage Azure Table pour les tables de stockage et réduire les besoins de débit.</span><span class="sxs-lookup"><span data-stu-id="47723-122">You can continue toouse Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="47723-123">Base de données Azure Cosmos introduira prise en charge pour les tables de stockage optimisé dans une prochaine mise à jour et nouveaux et existants Table Azure en toute transparence les comptes de stockage sera mis à niveau tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47723-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded tooAzure Cosmos DB.</span></span>

<span data-ttu-id="47723-124">Si vous utilisez actuellement le stockage de Table Azure, vous bénéficiez hello avantages avec l’aperçu de la « table premium » hello suivants :</span><span class="sxs-lookup"><span data-stu-id="47723-124">If you currently use Azure Table storage, you gain hello following benefits with hello "premium table" preview:</span></span>

- <span data-ttu-id="47723-125">[Distribution mondiale](distribute-data-globally.md) clé en main avec multihébergement et [basculements automatiques et manuels](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="47723-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="47723-126">Prise en charge de l’indexation automatique indépendante du schéma par rapport à toutes les propriétés (« index secondaires »), et requêtes rapides</span><span class="sxs-lookup"><span data-stu-id="47723-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="47723-127">Prise en charge de la [mise à l’échelle indépendante du stockage et du débit](partition-data.md) pour autant de régions que nécessaire</span><span class="sxs-lookup"><span data-stu-id="47723-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="47723-128">Prise en charge de [débit dédié par table](request-units.md) qui peut être monté en charge des centaines toomillions de demandes par seconde</span><span class="sxs-lookup"><span data-stu-id="47723-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds toomillions of requests per second</span></span>
- <span data-ttu-id="47723-129">Prise en charge de [cinq niveaux de cohérence ajustables](consistency-levels.md) tootrade hors tension de la disponibilité, la latence et la cohérence selon les besoins de votre application</span><span class="sxs-lookup"><span data-stu-id="47723-129">Support for [five tunable consistency levels](consistency-levels.md) tootrade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="47723-130">disponibilité de 99,99 % au sein d’une seule région et capacité tooadd plusieurs régions pour augmenter la disponibilité et [SLA complète de pointe](https://azure.microsoft.com/support/legal/sla/cosmos-db/) sur la disponibilité générale</span><span class="sxs-lookup"><span data-stu-id="47723-130">99.99% availability within a single region, and ability tooadd more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="47723-131">Travailler avec le stockage Azure existant hello .NET SDK et aucune application de tooyour de modifications de code</span><span class="sxs-lookup"><span data-stu-id="47723-131">Work with hello existing Azure storage .NET SDK, and no code changes tooyour application</span></span>

<span data-ttu-id="47723-132">Version préliminaire hello, prend en charge de la base de données Azure Cosmos hello API de Table à l’aide de hello du SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="47723-132">During hello preview, Azure Cosmos DB supports hello Table API using hello .NET SDK.</span></span> <span data-ttu-id="47723-133">Vous pouvez télécharger hello [aperçu de stockage Windows Azure SDK](https://aka.ms/premiumtablenuget) de NuGet, qui a hello mêmes classes et les signatures de méthode en tant que hello [SDK Azure Storage](https://www.nuget.org/packages/WindowsAzure.Storage), mais connectez-vous également les comptes de Cosmos DB tooAzure à l’aide de hello API de table.</span><span class="sxs-lookup"><span data-stu-id="47723-133">You can download hello [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has hello same classes and method signatures as hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect tooAzure Cosmos DB accounts using hello Table API.</span></span>

<span data-ttu-id="47723-134">toolearn savoir plus sur les tâches de stockage Azure Table complexes, consultez :</span><span class="sxs-lookup"><span data-stu-id="47723-134">toolearn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="47723-135">Introduction tooAzure Cosmos DB : API de Table</span><span class="sxs-lookup"><span data-stu-id="47723-135">Introduction tooAzure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="47723-136">documentation de référence de service de Table pour plus d’informations sur les API disponibles de Hello [bibliothèque cliente de stockage pour la référence .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="47723-136">hello Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="47723-137">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="47723-137">About this tutorial</span></span>
<span data-ttu-id="47723-138">Ce didacticiel est pour les développeurs qui sont familiarisés avec hello stockage de Table Azure SDK et sont que les fonctionnalités de premium hello toouse disponibles à l’aide de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="47723-138">This tutorial is for developers who are familiar with hello Azure Table storage SDK, and would like toouse hello premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="47723-139">Il est basé sur [prise en main le stockage de Table Azure à l’aide de .NET](table-storage-how-to-use-dotnet.md) et montre comment parti tootake de fonctionnalités supplémentaires que les index secondaires, le débit approvisionné et hébergement multiple.</span><span class="sxs-lookup"><span data-stu-id="47723-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how tootake advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="47723-140">Nous abordons la toouse hello toocreate portail Azure un compte de base de données Azure Cosmos, puis créer et déployer une application de la Table.</span><span class="sxs-lookup"><span data-stu-id="47723-140">We cover how toouse hello Azure portal toocreate an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="47723-141">Nous passons également en revue des exemples .NET pour la création et la suppression d’une table, et l’insertion, la mise à jour, la suppression et l’interrogation de données de table.</span><span class="sxs-lookup"><span data-stu-id="47723-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="47723-142">Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello **libre** [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="47723-142">If you don't already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="47723-143">Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="47723-143">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="47723-144">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="47723-144">Create a database account</span></span>

<span data-ttu-id="47723-145">Commençons par la création d’un compte de base de données Azure Cosmos Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="47723-145">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="47723-146">Possédez-vous un compte Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="47723-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="47723-147">Dans ce cas, passez directement trop[configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="47723-147">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="47723-148">Possédiez-vous un compte Azure DocumentDB ?</span><span class="sxs-lookup"><span data-stu-id="47723-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="47723-149">Si votre compte est maintenant un compte de base de données Azure Cosmos, et que vous pouvez passer trop[configurer votre solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="47723-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="47723-150">Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[configurer votre Solution Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="47723-150">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a><span data-ttu-id="47723-151">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="47723-151">Clone hello sample application</span></span>

<span data-ttu-id="47723-152">Maintenant nous allons cloner une application de la Table à partir de github, définissez la chaîne de connexion hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="47723-152">Now let's clone a Table app from github, set hello connection string, and run it.</span></span>

1. <span data-ttu-id="47723-153">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="47723-153">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="47723-154">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="47723-154">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="47723-155">Ouvrez ensuite le fichier de solution de hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="47723-155">Then open hello solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="47723-156">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="47723-156">Update your connection string</span></span>

<span data-ttu-id="47723-157">Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="47723-157">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="47723-158">Bonjour [portail Azure](http://portal.azure.com/), dans votre base de données de Cosmos Azure account, Bonjour barre de navigation gauche, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**.</span><span class="sxs-lookup"><span data-stu-id="47723-158">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="47723-159">Vous allez utiliser les boutons de copier hello sur droite hello hello écran toocopy hello de chaîne de connexion dans le fichier app.config de hello dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="47723-159">You'll use hello copy buttons on hello right side of hello screen toocopy hello connection string into hello app.config file in hello next step.</span></span>

2. <span data-ttu-id="47723-160">Dans Visual Studio, ouvrez le fichier app.config de hello.</span><span class="sxs-lookup"><span data-stu-id="47723-160">In Visual Studio, open hello app.config file.</span></span> 

3. <span data-ttu-id="47723-161">Copier la valeur de l’URI à partir du portail hello (à l’aide du bouton de copie hello) et le rendre hello la valeur de clé de compte hello dans app.config. Utilisez le nom de compte de hello créé précédemment pour le nom de compte dans le fichier app.config.</span><span class="sxs-lookup"><span data-stu-id="47723-161">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello account-key in app.config. Use hello account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="47723-162">toouse cette application avec le stockage de Table Azure standard, vous devez de chaîne de connexion toochange hello dans `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="47723-162">toouse this app with standard Azure Table Storage, you need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="47723-163">Utiliser le nom de compte hello en tant que nom de compte de la Table et la clé en tant que clé primaire de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="47723-163">Use hello account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a><span data-ttu-id="47723-164">Générez et déployez l’application hello</span><span class="sxs-lookup"><span data-stu-id="47723-164">Build and deploy hello app</span></span>
1. <span data-ttu-id="47723-165">Dans Visual Studio, cliquez sur projet hello dans **l’Explorateur de solutions** puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="47723-165">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="47723-166">Bonjour NuGet **Parcourir** , tapez ***WindowsAzure.Storage-PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="47723-166">In hello NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="47723-167">Cochez la case **Inclure les préversions**.</span><span class="sxs-lookup"><span data-stu-id="47723-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="47723-168">À partir des résultats de hello, installez hello **WindowsAzure.Storage-PremiumTable** et choisissez la version préliminaire de hello `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="47723-168">From hello results, install hello **WindowsAzure.Storage-PremiumTable** and choose hello preview build `0.0.1-preview`.</span></span> <span data-ttu-id="47723-169">Cette action installe le package de stockage de Table Azure hello et toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="47723-169">This action installs hello Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="47723-170">Cliquez sur CTRL + F5 application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="47723-170">Click CTRL + F5 toorun hello application.</span></span> 

<span data-ttu-id="47723-171">Vous pouvez maintenant revenir en arrière tooData Explorer et voir la requête, modifier et travailler avec ces données de table.</span><span class="sxs-lookup"><span data-stu-id="47723-171">You can now go back tooData Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="47723-172">toouse cette application avec un émulateur de base de données Azure Cosmos, simplement vous avez besoin de chaîne de connexion toochange hello dans `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="47723-172">toouse this app with an Azure Cosmos DB Emulator, you just need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="47723-173">Utilisez hello sous la valeur de l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="47723-173">Use hello below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="47723-174">Fonctionnalités d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="47723-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="47723-175">Base de données Azure Cosmos prend en charge un certain nombre de fonctionnalités qui ne sont pas disponibles dans hello API de stockage Azure Table.</span><span class="sxs-lookup"><span data-stu-id="47723-175">Azure Cosmos DB supports a number of capabilities that are not available in hello Azure Table storage API.</span></span> <span data-ttu-id="47723-176">Hello nouvelles fonctionnalités peuvent être activées via les éléments suivants de hello `appSettings` valeurs de configuration.</span><span class="sxs-lookup"><span data-stu-id="47723-176">hello new functionality can be enabled via hello following `appSettings` configuration values.</span></span> <span data-ttu-id="47723-177">Nous n’avez pas introduit toutes les nouvelles signatures surcharges toohello aperçu ou SDK Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="47723-177">We did not introduce any new signatures or overloads toohello preview Azure Storage SDK.</span></span> <span data-ttu-id="47723-178">Cela vous permet de tooconnect tooboth standard et premium tables et le travail avec d’autres services de stockage Azure, comme les objets BLOB et files d’attente.</span><span class="sxs-lookup"><span data-stu-id="47723-178">This allows you tooconnect tooboth standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="47723-179">Clé</span><span class="sxs-lookup"><span data-stu-id="47723-179">Key</span></span> | <span data-ttu-id="47723-180">Description</span><span class="sxs-lookup"><span data-stu-id="47723-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47723-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="47723-181">TableConnectionMode</span></span>  | <span data-ttu-id="47723-182">Azure Cosmos DB prend en charge deux modes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="47723-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="47723-183">Dans `Gateway` mode, les demandes sont toujours effectuées passerelle de base de données Azure Cosmos toohello, qu’il transfère toohello des partitions de données correspondante.</span><span class="sxs-lookup"><span data-stu-id="47723-183">In `Gateway` mode, requests are always made toohello Azure Cosmos DB gateway, which forwards it toohello corresponding data partitions.</span></span> <span data-ttu-id="47723-184">Dans `Direct` mode de connectivité client de hello lit mappage hello de toopartitions de tables et les demandes sont effectuées directement sur les partitions de données.</span><span class="sxs-lookup"><span data-stu-id="47723-184">In `Direct` connectivity mode, hello client fetches hello mapping of tables toopartitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="47723-185">Nous vous recommandons de `Direct`, hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="47723-185">We recommend `Direct`, hello default.</span></span>  |
| <span data-ttu-id="47723-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="47723-186">TableConnectionProtocol</span></span> | <span data-ttu-id="47723-187">Azure Cosmos DB prend en charge deux protocoles de connexion : `Https` et `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="47723-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="47723-188">`Tcp`est la valeur par défaut hello et recommandé, car il est plus léger.</span><span class="sxs-lookup"><span data-stu-id="47723-188">`Tcp` is hello default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="47723-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="47723-189">TablePreferredLocations</span></span> | <span data-ttu-id="47723-190">Liste séparée par des virgules des emplacements (de multihébergement) préférés pour les lectures.</span><span class="sxs-lookup"><span data-stu-id="47723-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="47723-191">Chaque compte Azure Cosmos DB peut être associé à un nombre de régions compris entre un et plus de 30.</span><span class="sxs-lookup"><span data-stu-id="47723-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="47723-192">Chaque instance de client peut spécifier un sous-ensemble de ces régions dans l’ordre de hello préféré pour les lectures de faible latence.</span><span class="sxs-lookup"><span data-stu-id="47723-192">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="47723-193">les régions Hello doivent être nommées à l’aide de leurs [afficher les noms des](https://msdn.microsoft.com/library/azure/gg441293.aspx), par exemple, `West US`.</span><span class="sxs-lookup"><span data-stu-id="47723-193">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="47723-194">Voir également [API multihébergement](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="47723-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="47723-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="47723-195">TableConsistencyLevel</span></span> | <span data-ttu-id="47723-196">Vous pouvez trouver un compromis entre latence, cohérence et disponibilité en choisissant l’un des cinq niveaux de cohérence bien définis disponibles : `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` et `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="47723-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="47723-197">La valeur par défaut est `Session`.</span><span class="sxs-lookup"><span data-stu-id="47723-197">Default is `Session`.</span></span> <span data-ttu-id="47723-198">choix de Hello du niveau de cohérence rend une différence significative des performances dans les configurations de plusieurs régions.</span><span class="sxs-lookup"><span data-stu-id="47723-198">hello choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="47723-199">Pour plus d’informations, consultez [Niveaux de cohérence](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="47723-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="47723-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="47723-200">TableThroughput</span></span> | <span data-ttu-id="47723-201">Débit réservé pour la table hello exprimée en unités de demande (RU) par seconde.</span><span class="sxs-lookup"><span data-stu-id="47723-201">Reserved throughput for hello table expressed in request units (RU) per second.</span></span> <span data-ttu-id="47723-202">Les tables uniques peuvent prendre en charge plusieurs centaines de millions de RU/s.</span><span class="sxs-lookup"><span data-stu-id="47723-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="47723-203">Voir [Unités de requête](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="47723-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="47723-204">La valeur par défaut est `400`.</span><span class="sxs-lookup"><span data-stu-id="47723-204">Default is `400`</span></span> |
| <span data-ttu-id="47723-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="47723-205">TableIndexingPolicy</span></span> | <span data-ttu-id="47723-206">Indexation cohérente et automatique de toutes les colonnes que contiennent les tables.</span><span class="sxs-lookup"><span data-stu-id="47723-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="47723-207">JSON chaîne conforme toohello une spécification de la stratégie d’indexation.</span><span class="sxs-lookup"><span data-stu-id="47723-207">JSON string conforming toohello indexing policy specification.</span></span> <span data-ttu-id="47723-208">Consultez [stratégie d’indexation](indexing-policies.md) toosee comment vous pouvez modifier des colonnes spécifiques d’indexation stratégie tooinclude/exclude.</span><span class="sxs-lookup"><span data-stu-id="47723-208">See [Indexing Policy](indexing-policies.md) toosee how you can change indexing policy tooinclude/exclude specific columns.</span></span> | <span data-ttu-id="47723-209">Indexation automatique de toutes les propriétés (hachage pour les chaînes et plage pour les nombres).</span><span class="sxs-lookup"><span data-stu-id="47723-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="47723-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="47723-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="47723-211">Configurer hello le nombre maximal d’éléments renvoyés par la requête de table dans un seul aller-retour.</span><span class="sxs-lookup"><span data-stu-id="47723-211">Configure hello maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="47723-212">Valeur par défaut est `-1`, ce qui permet la base de données Azure Cosmos déterminer dynamiquement la valeur hello lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="47723-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |
| <span data-ttu-id="47723-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="47723-213">TableQueryEnableScan</span></span> | <span data-ttu-id="47723-214">Si la requête de hello ne peut pas utiliser des index de hello pour n’importe quel filtre, puis l’exécuter quand même via une analyse.</span><span class="sxs-lookup"><span data-stu-id="47723-214">If hello query cannot use hello index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="47723-215">La valeur par défaut est `false`.</span><span class="sxs-lookup"><span data-stu-id="47723-215">Default is `false`.</span></span>|
| <span data-ttu-id="47723-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="47723-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="47723-217">degré de Hello de parallélisme pour l’exécution d’une requête de partitions croisées.</span><span class="sxs-lookup"><span data-stu-id="47723-217">hello degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="47723-218">`0`est la série avec aucune pré-extraction, `1` est série avec la pré-récupération et les valeurs élevées hello accroître le taux de parallélisme.</span><span class="sxs-lookup"><span data-stu-id="47723-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase hello rate of parallelism.</span></span> <span data-ttu-id="47723-219">Valeur par défaut est `-1`, ce qui permet la base de données Azure Cosmos déterminer dynamiquement la valeur hello lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="47723-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |

<span data-ttu-id="47723-220">valeur par défaut de toochange hello, ouvrez hello `app.config` fichier à partir de l’Explorateur de solutions dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="47723-220">toochange hello default value, open hello `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="47723-221">Ajouter du contenu hello Hello `<appSettings>` élément indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="47723-221">Add hello contents of hello `<appSettings>` element shown below.</span></span> <span data-ttu-id="47723-222">Remplacez `account-name` avec nom hello de votre compte de stockage et `account-key` avec la clé d’accès de votre compte.</span><span class="sxs-lookup"><span data-stu-id="47723-222">Replace `account-name` with hello name of your storage account, and `account-key` with your account access key.</span></span> 

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

<span data-ttu-id="47723-223">Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="47723-223">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="47723-224">Ouvrez hello `Program.cs` fichier et que vous recherchez que ces lignes de code créent hello de ressources de la Table.</span><span class="sxs-lookup"><span data-stu-id="47723-224">Open hello `Program.cs` file and you find that these lines of code create hello Table resources.</span></span> 

## <a name="create-hello-table-client"></a><span data-ttu-id="47723-225">Créer le client de table hello</span><span class="sxs-lookup"><span data-stu-id="47723-225">Create hello table client</span></span>
<span data-ttu-id="47723-226">Vous initialisez un `CloudTableClient` compte de table tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="47723-226">You initialize a `CloudTableClient` tooconnect toohello table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="47723-227">Ce client est initialisé à l’aide de hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, et `TablePreferredLocations` s’il est spécifié dans les paramètres de l’application hello des valeurs de configuration.</span><span class="sxs-lookup"><span data-stu-id="47723-227">This client is initialized using hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in hello app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="47723-228">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="47723-228">Create a table</span></span>
<span data-ttu-id="47723-229">Ensuite, vous créez une table à l’aide de `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="47723-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="47723-230">Tables de base de données Azure Cosmos peuvent évoluer de manière indépendante en termes de débit et de stockage et le partitionnement est géré automatiquement par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="47723-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by hello service.</span></span> <span data-ttu-id="47723-231">Azure Cosmos DB prend à la fois en charge une taille fixe et un nombre illimité de tables.</span><span class="sxs-lookup"><span data-stu-id="47723-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="47723-232">Pour plus d’informations, consultez [Partitionnement dans Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="47723-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="47723-233">Il existe une différence importante dans la façon dont les tables sont créées.</span><span class="sxs-lookup"><span data-stu-id="47723-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="47723-234">Azure Cosmos DB réserve le débit, contrairement au modèle du stockage Azure pour les transactions, basé sur la consommation.</span><span class="sxs-lookup"><span data-stu-id="47723-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="47723-235">modèle de réservation Hello présente deux avantages principaux :</span><span class="sxs-lookup"><span data-stu-id="47723-235">hello reservation model has two key benefits:</span></span>

* <span data-ttu-id="47723-236">Le débit est dédié/réservé, ce qui fait que vous n’êtes jamais limité si le taux de requêtes est inférieur ou égal à votre débit approvisionné.</span><span class="sxs-lookup"><span data-stu-id="47723-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="47723-237">modèle de réservation Hello est plus [économique pour les charges de travail à nombre élevé de débit](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="47723-237">hello reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="47723-238">Vous pouvez configurer un débit hello par défaut en configurant le paramètre hello pour `TableThroughput` en termes de RU (unités de demande) par seconde.</span><span class="sxs-lookup"><span data-stu-id="47723-238">You can configure hello default throughput by configuring hello setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="47723-239">Une lecture d’une entité de 1 Ko est normalisée en tant que 1 ur et autres opérations sont normalisée tooa fixé valeur RU en fonction de leur consommation de processeur, mémoire et e/s.</span><span class="sxs-lookup"><span data-stu-id="47723-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized tooa fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="47723-240">En savoir plus sur les [Unités de requête dans Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="47723-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="47723-241">Alors que le SDK le stockage de Table ne prend pas en charge la modification de débit, vous pouvez modifier le débit de hello instantanément à tout moment à l’aide de hello portail Azure ou CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="47723-241">While Table storage SDK does not currently support modifying throughput, you can change hello throughput instantaneously at any time using hello Azure portal or Azure CLI.</span></span>

<span data-ttu-id="47723-242">Ensuite, nous guider lecture simple de hello et écrire des opérations à l’aide du stockage de Table Azure hello SDK.</span><span class="sxs-lookup"><span data-stu-id="47723-242">Next, we walk through hello simple read and write (CRUD) operations using hello Azure Table storage SDK.</span></span> <span data-ttu-id="47723-243">Ce didacticiel démontre les latences prévisibles faibles, de l’ordre de quelques millisecondes, et les requêtes rapides assurées par Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47723-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="47723-244">Ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="47723-244">Add an entity tooa table</span></span>
<span data-ttu-id="47723-245">Les entités dans le stockage Azure Table étendent à partir de hello `TableEntity` classe et doit avoir `PartitionKey` et `RowKey` propriétés.</span><span class="sxs-lookup"><span data-stu-id="47723-245">Entities in Azure Table storage extend from hello `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="47723-246">Voici un exemple de définition d’une entité de client.</span><span class="sxs-lookup"><span data-stu-id="47723-246">Here's a sample definition for a customer entity.</span></span>

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

<span data-ttu-id="47723-247">Hello suivant extrait de code montre comment tooinsert une entité avec hello stockage Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="47723-247">hello following snippet shows how tooinsert an entity with hello Azure storage SDK.</span></span> <span data-ttu-id="47723-248">Base de données Azure Cosmos est conçu pour être garanti de faible latence à n’importe quelle échelle, entre Bonjour.</span><span class="sxs-lookup"><span data-stu-id="47723-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across hello world.</span></span>

<span data-ttu-id="47723-249">Fin des écritures < 15 ms à p99 et ms ~ 6 à p50 pour les applications en cours d’exécution hello même région que le compte de base de données Azure Cosmos de hello.</span><span class="sxs-lookup"><span data-stu-id="47723-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in hello same region as hello Azure Cosmos DB account.</span></span> <span data-ttu-id="47723-250">Et cette durée compte fait hello qui écrit est toohello précédent client une fois qu’ils sont répliquées de manière synchrone, la validation de façon durable, et tout le contenu est indexé.</span><span class="sxs-lookup"><span data-stu-id="47723-250">And this duration accounts for hello fact that writes are acknowledged back toohello client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="47723-251">Hello API de la Table de base de données Azure Cosmos est en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="47723-251">hello Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="47723-252">Disponibilité générale, hello p99 de garanties de latence sont soutenues par SLA, comme d’autres API de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="47723-252">At general availability, hello p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="47723-253">Insertion d’un lot d’entités</span><span class="sxs-lookup"><span data-stu-id="47723-253">Insert a batch of entities</span></span>
<span data-ttu-id="47723-254">Azure Table storage prend en charge une API d’opération de traitement par lots, qui vous permet de combiner des mises à jour, suppressions et insertions dans hello même opération de lot unique.</span><span class="sxs-lookup"><span data-stu-id="47723-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in hello same single batch operation.</span></span> <span data-ttu-id="47723-255">Base de données Azure Cosmos n’a pas certaines des limitations de hello sur les API de lot hello en tant que stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="47723-255">Azure Cosmos DB does not have some of hello limitations on hello batch API as Azure Table storage.</span></span> <span data-ttu-id="47723-256">Par exemple, vous pouvez effectuer plusieurs lectures dans un lot, vous pouvez effectuer plusieurs écritures toohello même entité au sein d’un lot, et il n’existe aucune limite sur 100 opérations par lot.</span><span class="sxs-lookup"><span data-stu-id="47723-256">For example, you can perform multiple reads within a batch, you can perform multiple writes toohello same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="47723-257">Extraction d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="47723-257">Retrieve a single entity</span></span>
<span data-ttu-id="47723-258">Récupère (obtient) dans Cosmos base de données Azure complet < 10 ms à p99 et ~ 1 ms à p50 dans hello même région Azure.</span><span class="sxs-lookup"><span data-stu-id="47723-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in hello same Azure region.</span></span> <span data-ttu-id="47723-259">Vous pouvez ajouter autant compte tooyour de régions pour les lectures de faible latence et déployer tooread d’applications à partir de leur région (« multi-résidente ») en définissant `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="47723-259">You can add as many regions tooyour account for low latency reads, and deploy applications tooread from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="47723-260">Vous pouvez récupérer une entité unique à l’aide de hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="47723-260">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="47723-261">Pour plus d’informations sur les API multihébergement, consultez [Développement avec plusieurs régions](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="47723-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="47723-262">Interrogation d’entités à l’aide d’index secondaires automatiques</span><span class="sxs-lookup"><span data-stu-id="47723-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="47723-263">Tables peuvent être interrogées à l’aide de hello `TableQuery` classe.</span><span class="sxs-lookup"><span data-stu-id="47723-263">Tables can be queried using hello `TableQuery` class.</span></span> <span data-ttu-id="47723-264">Azure Cosmos DB intègre un moteur de base de données optimisé pour l’écriture qui indexe automatiquement toutes les colonnes de votre table.</span><span class="sxs-lookup"><span data-stu-id="47723-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="47723-265">L’indexation de base de données Azure Cosmos est tooschema agnostique.</span><span class="sxs-lookup"><span data-stu-id="47723-265">Indexing in Azure Cosmos DB is agnostic tooschema.</span></span> <span data-ttu-id="47723-266">Par conséquent, même si votre schéma est différent entre les lignes, ou si le schéma de hello évolue au fil du temps, il est automatiquement indexé.</span><span class="sxs-lookup"><span data-stu-id="47723-266">Therefore, even if your schema is different between rows, or if hello schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="47723-267">Étant donné que la base de données Azure Cosmos prend en charge les index secondaires automatique, les requêtes par rapport à n’importe quelle propriété peuvent utiliser les index hello et pris en charge efficacement.</span><span class="sxs-lookup"><span data-stu-id="47723-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use hello index and be served efficiently.</span></span>

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

<span data-ttu-id="47723-268">Dans l’aperçu, prend en charge la base de données Azure Cosmos hello même fonctionnalité comme stockage de Table Azure pour hello API de la Table de requête.</span><span class="sxs-lookup"><span data-stu-id="47723-268">In preview, Azure Cosmos DB supports hello same query functionality as Azure Table storage for hello Table API.</span></span> <span data-ttu-id="47723-269">Azure Cosmos DB prend également en charge le tri, les agrégats, les requêtes géospatiales, les hiérarchies et un large éventail de fonctions intégrées.</span><span class="sxs-lookup"><span data-stu-id="47723-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="47723-270">Vous trouverez des fonctionnalités supplémentaires Hello Bonjour API de Table dans une mise à jour future du service.</span><span class="sxs-lookup"><span data-stu-id="47723-270">hello additional functionality will be provided in hello Table API in a future service update.</span></span> <span data-ttu-id="47723-271">Pour une vue d’ensemble de ces fonctionnalités, consultez [Azure Cosmos DB query](documentdb-sql-query.md) (Requête dans Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="47723-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="47723-272">Remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="47723-272">Replace an entity</span></span>
<span data-ttu-id="47723-273">tooupdate une entité, récupérer à partir du service de Table hello, modifier l’objet d’entité hello, puis enregistrez les modifications hello de nouveau service de Table toohello.</span><span class="sxs-lookup"><span data-stu-id="47723-273">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="47723-274">Hello code suivant modifie un numéro de téléphone existant.</span><span class="sxs-lookup"><span data-stu-id="47723-274">hello following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="47723-275">De même, vous pouvez effectuer des opérations `InsertOrMerge` ou `Merge`.</span><span class="sxs-lookup"><span data-stu-id="47723-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="47723-276">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="47723-276">Delete an entity</span></span>
<span data-ttu-id="47723-277">Vous pouvez facilement supprimer une entité une fois que vous l’avez extrait à l’aide de hello même modèle indiqué pour la mise à jour une entité.</span><span class="sxs-lookup"><span data-stu-id="47723-277">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="47723-278">Hello suivant code récupère et supprime une entité customer.</span><span class="sxs-lookup"><span data-stu-id="47723-278">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="47723-279">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="47723-279">Delete a table</span></span>
<span data-ttu-id="47723-280">Enfin, hello, exemple de code suivant supprime une table à partir d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="47723-280">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="47723-281">Vous pouvez supprimer et recréer une table immédiatement avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47723-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="47723-282">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="47723-282">Clean up resources</span></span> 

<span data-ttu-id="47723-283">Si vous n’allez toocontinue toouse cette application, utilisez hello suivant toodelete suit toutes les ressources créées par ce didacticiel Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="47723-283">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>   

1. <span data-ttu-id="47723-284">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="47723-284">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span>  
2. <span data-ttu-id="47723-285">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="47723-285">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="47723-286">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="47723-286">Next steps</span></span>

<span data-ttu-id="47723-287">Dans ce didacticiel, nous avons abordé comment tooget démarrer à l’aide de la base de données Azure Cosmos hello API de Table, et vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="47723-287">In this tutorial, we covered how tooget started using Azure Cosmos DB with hello Table API, and you've done hello following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="47723-288">Créé un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="47723-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="47723-289">Fonctionnalité activée dans le fichier app.config hello</span><span class="sxs-lookup"><span data-stu-id="47723-289">Enabled functionality in hello app.config file</span></span> 
> * <span data-ttu-id="47723-290">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="47723-290">Created a table</span></span> 
> * <span data-ttu-id="47723-291">Ajout d’un tableau de tooa entité</span><span class="sxs-lookup"><span data-stu-id="47723-291">Added an entity tooa table</span></span> 
> * <span data-ttu-id="47723-292">Insertion d’un lot d’entités</span><span class="sxs-lookup"><span data-stu-id="47723-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="47723-293">Extraction d’une seule entité</span><span class="sxs-lookup"><span data-stu-id="47723-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="47723-294">Interrogation d’entités à l’aide d’index secondaires automatiques</span><span class="sxs-lookup"><span data-stu-id="47723-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="47723-295">Remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="47723-295">Replaced an entity</span></span> 
> * <span data-ttu-id="47723-296">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="47723-296">Deleted an entity</span></span> 
> * <span data-ttu-id="47723-297">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="47723-297">Deleted a table</span></span>  

<span data-ttu-id="47723-298">Vous pouvez maintenant continuer le didacticiel suivant de toohello et en savoir plus sur l’interrogation des données de la table.</span><span class="sxs-lookup"><span data-stu-id="47723-298">You can now proceed toohello next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="47723-299">Requête avec hello API de Table</span><span class="sxs-lookup"><span data-stu-id="47723-299">Query with hello Table API</span></span>](tutorial-query-table.md)
