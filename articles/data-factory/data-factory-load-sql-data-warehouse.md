---
title: "aaaLoad des téraoctets de données dans l’entrepôt de données SQL | Documents Microsoft"
description: "Montre comment 1 To de données peut être chargé dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="56ff9-103">Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="56ff9-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="56ff9-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) est une base de données de mise à l’échelle basée sur le cloud qui prend en charge le traitement de grands volumes de données relationnelles et non relationnelles.</span><span class="sxs-lookup"><span data-stu-id="56ff9-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="56ff9-105">Reposant sur une architecture MPP (massively parallel processing), SQL Data Warehouse est optimisée pour les charges de travail d’entrepôt de données d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="56ff9-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="56ff9-106">Il offre cloud élasticité avec un stockage tooscale hello flexibilité et de calcul indépendamment.</span><span class="sxs-lookup"><span data-stu-id="56ff9-106">It offers cloud elasticity with hello flexibility tooscale storage and compute independently.</span></span>

<span data-ttu-id="56ff9-107">La prise en main d’Azure SQL Data Warehouse est désormais plus facile à l’aide **d’Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="56ff9-108">Azure Data Factory est un service d’intégration des données cloud entièrement géré, ce qui peut être utilisé toopopulate un entrepôt de données SQL avec des données de hello de votre système existant et l’enregistrement d’un temps précieux lors de l’évaluation SQL Data Warehouse et votre analytique solutions.</span><span class="sxs-lookup"><span data-stu-id="56ff9-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used toopopulate a SQL Data Warehouse with hello data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="56ff9-109">Voici hello principaux avantages du chargement de données dans l’entrepôt de données SQL Azure à l’aide de la fabrique de données Azure :</span><span class="sxs-lookup"><span data-stu-id="56ff9-109">Here are hello key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="56ff9-110">**Tooset facile des**: 5-étape intuitif Assistant pas de script.</span><span class="sxs-lookup"><span data-stu-id="56ff9-110">**Easy tooset up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="56ff9-111">**Prise en charge étendue du magasin de données** : prise en charge intégrée d’un ensemble complet de magasins de données locaux et sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="56ff9-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="56ff9-112">**Sécurisés et conformes**: données sont transférées sur HTTPS ou ExpressRoute et la présence du service global garantit que vos données ne quittent jamais les limites géographiques hello</span><span class="sxs-lookup"><span data-stu-id="56ff9-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves hello geographical boundary</span></span>
* <span data-ttu-id="56ff9-113">**Performances uniques à l’aide de PolyBase** – à l’aide de Polybase est hello plus efficace des toomove données dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="56ff9-113">**Unparalleled performance by using PolyBase** – Using Polybase is hello most efficient way toomove data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="56ff9-114">À l’aide de hello mise en lots de la fonctionnalité de l’objet blob, vous pouvez obtenir vitesses de charge élevée de tous les types de banques de données en plus de stockage d’objets Blob Azure, qui hello Polybase prend par défaut.</span><span class="sxs-lookup"><span data-stu-id="56ff9-114">Using hello staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which hello Polybase supports by default.</span></span>

<span data-ttu-id="56ff9-115">Cet article vous montre comment toouse Assistant Copier les données fabrique tooload 1 To de données à partir du stockage d’objets Blob Azure dans Azure SQL Data Warehouse sous des 15 dernières minutes, à un débit plus 1,2 Gbits/s.</span><span class="sxs-lookup"><span data-stu-id="56ff9-115">This article shows you how toouse Data Factory Copy Wizard tooload 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="56ff9-116">Cet article fournit des instructions détaillées pour le déplacement des données dans Azure SQL Data Warehouse à l’aide de hello Assistant copie de.</span><span class="sxs-lookup"><span data-stu-id="56ff9-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using hello Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="56ff9-117">Pour des informations générales sur les fonctionnalités de la fabrique de données lors du déplacement des données vers/à partir de l’entrepôt de données SQL Azure, consultez [déplacer tooand de données à partir de l’entrepôt de données SQL Azure à l’aide d’Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="56ff9-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data tooand from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="56ff9-118">Vous pouvez également créer des pipelines à l’aide du portail Azure, de Visual Studio, de PowerShell, etc. Consultez [didacticiel : copier des données d’objets Blob Azure tooAzure base de données SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour une présentation rapide des instructions détaillées pour l’utilisation de l’activité de copie de hello dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="56ff9-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using hello Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="56ff9-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="56ff9-119">Prerequisites</span></span>
* <span data-ttu-id="56ff9-120">Stockage Blob Azure : cette expérience utilise le Stockage Blob Azure (GRS) pour stocker un jeu de données de test TPC-H.</span><span class="sxs-lookup"><span data-stu-id="56ff9-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="56ff9-121">Si vous n’avez pas de compte de stockage Azure, Découvrez [comment toocreate un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="56ff9-121">If you do not have an Azure storage account, learn [how toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="56ff9-122">[TPC-H](http://www.tpc.org/tpch/) données : nous allons toouse TPC-H comme hello du jeu de données de test.</span><span class="sxs-lookup"><span data-stu-id="56ff9-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going toouse TPC-H as hello testing dataset.</span></span>  <span data-ttu-id="56ff9-123">toodo, vous avez besoin toouse `dbgen` à partir de la boîte à outils de TPC-H, qui vous permet de générer le jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="56ff9-123">toodo that, you need toouse `dbgen` from TPC-H toolkit, which helps you generate hello dataset.</span></span>  <span data-ttu-id="56ff9-124">Vous pouvez soit télécharger le code source pour `dbgen` de [TPC outils](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) et compilez-le vous-même ou binaire hello compilé de téléchargement à partir de [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="56ff9-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download hello compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="56ff9-125">Fichier plat de toogenerate 1 To pour les commandes dbgen.exe exécution avec les éléments suivants de hello `lineitem` table réparti entre 10 fichiers :</span><span class="sxs-lookup"><span data-stu-id="56ff9-125">Run dbgen.exe with hello following commands toogenerate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="56ff9-126">…</span><span class="sxs-lookup"><span data-stu-id="56ff9-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="56ff9-127">Maintenant, hello de copie généré tooAzure de fichiers Blob.</span><span class="sxs-lookup"><span data-stu-id="56ff9-127">Now copy hello generated files tooAzure Blob.</span></span>  <span data-ttu-id="56ff9-128">Consultez trop[déplacer des données tooand à partir d’un système de fichiers local à l’aide d’Azure Data Factory](data-factory-onprem-file-system-connector.md) procédure toodo qui à l’aide de la copie de la définition d’application.</span><span class="sxs-lookup"><span data-stu-id="56ff9-128">Refer too[Move data tooand from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how toodo that using ADF Copy.</span></span>    
* <span data-ttu-id="56ff9-129">Azure SQL Data Warehouse : cette expérience charge des données dans Azure SQL Data Warehouse créé avec 6 000 DWU</span><span class="sxs-lookup"><span data-stu-id="56ff9-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="56ff9-130">Consultez trop[créer un entrepôt de données SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) pour obtenir des instructions détaillées sur la façon dont toocreate une SQL l’entrepôt de données de base de données.</span><span class="sxs-lookup"><span data-stu-id="56ff9-130">Refer too[Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how toocreate a SQL Data Warehouse database.</span></span>  <span data-ttu-id="56ff9-131">tooget hello charge possible des performances optimales dans l’entrepôt de données SQL à l’aide de Polybase, nous choisissons le nombre maximal d’unités de l’entrepôt de données (Dwu) autorisés dans le paramètre de Performance hello, qui est de 6 000 Dwu.</span><span class="sxs-lookup"><span data-stu-id="56ff9-131">tooget hello best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in hello Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="56ff9-132">Lors du chargement d’objets Blob Azure, données hello performances de chargement sont directement proportionnelle toohello différents Dwu vous configurez sur hello SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="56ff9-132">When loading from Azure Blob, hello data loading performance is directly proportional toohello number of DWUs you configure on hello SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="56ff9-133">Le chargement de 1 To dans 1 000 DWU SQL Data Warehouse prend 87 minutes (débit d’environ 200 Mo/s). Le chargement de 1 To dans 2000 DWU SQL Data Warehouse prend 46 minutes (débit d’environ 380 Mo/s). Le chargement de 1 To dans 6 000 DWU SQL Data Warehouse prend 14 minutes (débit d’environ 1,2 Go/s).</span><span class="sxs-lookup"><span data-stu-id="56ff9-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="56ff9-134">toocreate un entrepôt de données SQL avec 6 000 Dwu, déplacez hello performances curseur tous les toohello de façon hello droite :</span><span class="sxs-lookup"><span data-stu-id="56ff9-134">toocreate a SQL Data Warehouse with 6,000 DWUs, move hello Performance slider all hello way toohello right:</span></span>

    ![Curseur Performance](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="56ff9-136">Pour une base de données existante qui n’est pas configurée avec 6 000 DWU, vous pouvez la mettre à l’échelle à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="56ff9-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="56ff9-137">Accédez toohello de base de données dans le portail Azure et il est un **échelle** bouton Bonjour **vue d’ensemble** Panneau de configuration illustré hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="56ff9-137">Navigate toohello database in Azure portal, and there is a **Scale** button in hello **Overview** panel shown in hello following image:</span></span>

    ![Bouton Mise à l’échelle](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="56ff9-139">Cliquez sur hello **échelle** suivant de bouton tooopen hello du panneau, déplacez la valeur maximale de hello curseur toohello, puis cliquez sur **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="56ff9-139">Click hello **Scale** button tooopen hello following panel, move hello slider toohello maximum value, and click **Save** button.</span></span>

    ![Boîte de dialogue de mise à l’échelle](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="56ff9-141">Cette expérience charge des données dans Azure SQL Data Warehouse à l’aide de la classe de ressources `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="56ff9-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="56ff9-142">tooachieve meilleurs résultats possibles, la copie doit toobe effectuée à l’aide d’un utilisateur de l’entrepôt de données SQL appartenant trop`xlargerc` classe de ressource.</span><span class="sxs-lookup"><span data-stu-id="56ff9-142">tooachieve best possible throughput, copy needs toobe performed using a SQL Data Warehouse user belonging too`xlargerc` resource class.</span></span>  <span data-ttu-id="56ff9-143">Découvrez comment toodo qui en suivant [modifier un exemple de classe de ressource utilisateur](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="56ff9-143">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="56ff9-144">Créer le schéma de table de destination dans la base de données de l’entrepôt de données SQL Azure, en exécutant hello suivant l’instruction DDL :</span><span class="sxs-lookup"><span data-stu-id="56ff9-144">Create destination table schema in Azure SQL Data Warehouse database, by running hello following DDL statement:</span></span>

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
<span data-ttu-id="56ff9-145">Étapes hello terminées, nous sommes maintenant à l’aide de hello Assistant copie de l’activité de copie tooconfigure prêt hello.</span><span class="sxs-lookup"><span data-stu-id="56ff9-145">With hello prerequisite steps completed, we are now ready tooconfigure hello copy activity using hello Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="56ff9-146">Lancer l’Assistant Copie</span><span class="sxs-lookup"><span data-stu-id="56ff9-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="56ff9-147">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="56ff9-147">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="56ff9-148">Cliquez sur **+ nouveau** à partir de l’angle supérieur gauche de hello, cliquez sur **Intelligence + analytique**, puis cliquez sur **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-148">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="56ff9-149">Bonjour **nouvelle fabrique de données** panneau :</span><span class="sxs-lookup"><span data-stu-id="56ff9-149">In hello **New data factory** blade:</span></span>

   1. <span data-ttu-id="56ff9-150">Entrez **LoadIntoSQLDWDataFactory** pour hello **nom**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-150">Enter **LoadIntoSQLDWDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="56ff9-151">nom de Hello de fabrique de données Azure hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="56ff9-151">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="56ff9-152">Si vous recevez une erreur de hello : **nom de fabrique de données « LoadIntoSQLDWDataFactory » n’est pas disponible**, de modifier le nom hello hello fabrique de données (par exemple, yournameLoadIntoSQLDWDataFactory) et essayez à nouveau de créer.</span><span class="sxs-lookup"><span data-stu-id="56ff9-152">If you receive hello error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change hello name of hello data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="56ff9-153">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="56ff9-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="56ff9-154">Sélectionnez votre **abonnement**Azure.</span><span class="sxs-lookup"><span data-stu-id="56ff9-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="56ff9-155">Pour le groupe de ressources, effectuez l’une des hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="56ff9-155">For Resource Group, do one of hello following steps:</span></span>
      1. <span data-ttu-id="56ff9-156">Sélectionnez **utiliser l’existante** tooselect un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="56ff9-156">Select **Use existing** tooselect an existing resource group.</span></span>
      2. <span data-ttu-id="56ff9-157">Sélectionnez **nouvel** tooenter un nom pour un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="56ff9-157">Select **Create new** tooenter a name for a resource group.</span></span>
   4. <span data-ttu-id="56ff9-158">Sélectionnez un **emplacement** de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="56ff9-158">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="56ff9-159">Sélectionnez **toodashboard du code confidentiel** bas hello du Panneau de hello de case à cocher.</span><span class="sxs-lookup"><span data-stu-id="56ff9-159">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="56ff9-160">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-160">Click **Create**.</span></span>
4. <span data-ttu-id="56ff9-161">Après la création de hello est terminée, vous voyez hello **Data Factory** panneau comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="56ff9-161">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>

   ![Page d'accueil Data Factory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="56ff9-163">Sur la page d’accueil de Data Factory hello, cliquez sur hello **copier les données** vignette toolaunch **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-163">On hello Data Factory home page, click hello **Copy data** tile toolaunch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="56ff9-164">Si vous voyez ce navigateur hello est bloqué au niveau de « Autorisation... », désactiver/Décochez **bloquer les cookies tiers et les données de site** définition (ou) qu’il soit activé et créer une exception pour **login.microsoftonline.com**, puis essayez de lancer les Assistant hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="56ff9-164">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="56ff9-165">Étape 1 : Configurer la planification du chargement de données</span><span class="sxs-lookup"><span data-stu-id="56ff9-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="56ff9-166">première étape de Hello donnée tooconfigure hello du chargement de planification.</span><span class="sxs-lookup"><span data-stu-id="56ff9-166">hello first step is tooconfigure hello data loading schedule.</span></span>  

<span data-ttu-id="56ff9-167">Bonjour **propriétés** page :</span><span class="sxs-lookup"><span data-stu-id="56ff9-167">In hello **Properties** page:</span></span>

1. <span data-ttu-id="56ff9-168">Entrez **CopyFromBlobToAzureSqlDataWarehouse** comme **Nom de la tâche**</span><span class="sxs-lookup"><span data-stu-id="56ff9-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="56ff9-169">Sélectionnez l’option **Exécuter une fois**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="56ff9-170">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-170">Click **Next**.</span></span>  

    ![Assistant Copie - Page Propriétés](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="56ff9-172">Étape 2 : Configurer la source</span><span class="sxs-lookup"><span data-stu-id="56ff9-172">Step 2: Configure source</span></span>
<span data-ttu-id="56ff9-173">Cette indique la section hello de source de hello étapes tooconfigure : contenant des objets Blob Azure hello 1 to TPC-fichiers de ligne H.</span><span class="sxs-lookup"><span data-stu-id="56ff9-173">This section shows you hello steps tooconfigure hello source: Azure Blob containing hello 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="56ff9-174">Sélectionnez hello **stockage d’objets Blob Azure** comme données de salutation stocker, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-174">Select hello **Azure Blob Storage** as hello data store and click **Next**.</span></span>

    ![Assistant Copie - Page Sélectionner la source](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="56ff9-176">Renseignez les informations de connexion hello pour hello compte de stockage d’objets Blob Azure, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-176">Fill in hello connection information for hello Azure Blob storage account, and click **Next**.</span></span>

    ![Assistant Copie - Informations de connexion à la source](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="56ff9-178">Choisissez hello **dossier** contenant hello TPC-H ligne fichiers d’élément et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-178">Choose hello **folder** containing hello TPC-H line item files and click **Next**.</span></span>

    ![Assistant Copie - Sélectionner le dossier d’entrée](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="56ff9-180">Lorsque vous cliquez sur **suivant**, paramètres de format de fichier hello sont détectés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="56ff9-180">Upon clicking **Next**, hello file format settings are detected automatically.</span></span>  <span data-ttu-id="56ff9-181">Vérifiez toomake que ce séparateur de colonnes est ' | 'au lieu de virgules par défaut hello','.</span><span class="sxs-lookup"><span data-stu-id="56ff9-181">Check toomake sure that column delimiter is ‘|’ instead of hello default comma ‘,’.</span></span>  <span data-ttu-id="56ff9-182">Cliquez sur **suivant** une fois que vous avez affiché un aperçu des données de salutation.</span><span class="sxs-lookup"><span data-stu-id="56ff9-182">Click **Next** after you have previewed hello data.</span></span>

    ![Assistant Copie - Paramètres de format de fichier](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="56ff9-184">Étape 3 : Configurer la destination</span><span class="sxs-lookup"><span data-stu-id="56ff9-184">Step 3: Configure destination</span></span>
<span data-ttu-id="56ff9-185">Cette section vous montre comment tooconfigure hello destination : `lineitem` table dans la base de données Azure SQL Data Warehouse hello.</span><span class="sxs-lookup"><span data-stu-id="56ff9-185">This section shows you how tooconfigure hello destination: `lineitem` table in hello Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="56ff9-186">Choisissez **Azure SQL Data Warehouse** en tant que destination de hello stocker, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-186">Choose **Azure SQL Data Warehouse** as hello destination store and click **Next**.</span></span>

    ![Assistant Copie - Sélectionner le magasin de données de destination](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="56ff9-188">Renseignez les informations de connexion hello pour Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="56ff9-188">Fill in hello connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="56ff9-189">Assurez-vous que vous spécifiez utilisateur hello qui est membre du rôle de hello `xlargerc` (voir hello **conditions préalables** section pour obtenir des instructions détaillées), puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-189">Make sure you specify hello user that is a member of hello role `xlargerc` (see hello **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Assistant Copie - Informations de connexion à la destination](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="56ff9-191">Choisissez la table de destination hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-191">Choose hello destination table and click **Next**.</span></span>

    ![Assistant Copie - Page Mappage de table](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="56ff9-193">Dans la page Mappage de schéma, laissez l’option « Appliquer le mappage de colonnes » décochée et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="56ff9-194">Étape 4 : Paramètres de performance</span><span class="sxs-lookup"><span data-stu-id="56ff9-194">Step 4: Performance settings</span></span>

<span data-ttu-id="56ff9-195">La case **Autoriser Polybase** est cochée par défaut.</span><span class="sxs-lookup"><span data-stu-id="56ff9-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="56ff9-196">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="56ff9-196">Click **Next**.</span></span>

![Assistant Copie - Page Mappage de schéma](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="56ff9-198">Étape 5 : Déployer et surveiller les résultats du chargement</span><span class="sxs-lookup"><span data-stu-id="56ff9-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="56ff9-199">Cliquez sur **Terminer** toodeploy du bouton.</span><span class="sxs-lookup"><span data-stu-id="56ff9-199">Click **Finish** button toodeploy.</span></span>

    ![Assistant Copie - Page Résumé](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="56ff9-201">Une fois le déploiement de hello est terminé, cliquez sur `Click here toomonitor copy pipeline` copie de hello toomonitor statut d’exécution.</span><span class="sxs-lookup"><span data-stu-id="56ff9-201">After hello deployment is complete, click `Click here toomonitor copy pipeline` toomonitor hello copy run progress.</span></span> <span data-ttu-id="56ff9-202">Pipeline de copie hello sélectionnez vous avez créé dans hello **Windows de l’activité** liste.</span><span class="sxs-lookup"><span data-stu-id="56ff9-202">Select hello copy pipeline you created in hello **Activity Windows** list.</span></span>

    ![Assistant Copie - Page Résumé](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="56ff9-204">Vous pouvez consulter copie hello détails de l’exécution dans hello **activité fenêtre Explorateur** dans le panneau droit hello, y compris le volume de données hello lire à partir de la source et écrites dans la destination, la durée et le débit moyen de hello pour hello exécuter,.</span><span class="sxs-lookup"><span data-stu-id="56ff9-204">You can view hello copy run details in hello **Activity Window Explorer** in hello right panel, including hello data volume read from source and written into destination, duration, and hello average throughput for hello run.</span></span>

    <span data-ttu-id="56ff9-205">Comme vous pouvez le constater hello suivant capture d’écran, la copie de 1 To de stockage d’objets Blob Azure dans SQL Data Warehouse a duré 14 minutes, efficacement productivité 1,22 Gbits/s !</span><span class="sxs-lookup"><span data-stu-id="56ff9-205">As you can see from hello following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Assistant Copie - Boîte de dialogue Succès](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="56ff9-207">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="56ff9-207">Best practices</span></span>
<span data-ttu-id="56ff9-208">Voici quelques meilleures pratiques pour l’exécution de votre base de données Azure SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="56ff9-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="56ff9-209">Utilisez une classe de ressources supérieure lors du chargement dans un INDEX COLUMNSTORE EN CLUSTER.</span><span class="sxs-lookup"><span data-stu-id="56ff9-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="56ff9-210">Pour des jonctions plus efficaces, envisagez d’utiliser la distribution par hachage en fonction d’une colonne sélectionnée au lieu de la distribution par tourniquet (round robin) par défaut.</span><span class="sxs-lookup"><span data-stu-id="56ff9-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="56ff9-211">Pour des vitesses de chargement plus rapides, envisagez d’utiliser des tas pour les données temporaires.</span><span class="sxs-lookup"><span data-stu-id="56ff9-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="56ff9-212">Créez des statistiques une fois le chargement Azure SQL Data Warehouse terminé.</span><span class="sxs-lookup"><span data-stu-id="56ff9-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="56ff9-213">Pour plus d’informations, consultez [Meilleures pratiques pour Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="56ff9-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56ff9-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56ff9-214">Next steps</span></span>
* <span data-ttu-id="56ff9-215">[Assistant copie de fabrique de données](data-factory-copy-wizard.md) -cet article fournit des détails sur l’Assistant copie de hello.</span><span class="sxs-lookup"><span data-stu-id="56ff9-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about hello Copy Wizard.</span></span>
* <span data-ttu-id="56ff9-216">[Copier l’activité guide des performances et paramétrage](data-factory-copy-activity-performance.md) -cet article contient des mesures de performances de référence hello et guide d’optimisation.</span><span class="sxs-lookup"><span data-stu-id="56ff9-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains hello reference performance measurements and tuning guide.</span></span>
