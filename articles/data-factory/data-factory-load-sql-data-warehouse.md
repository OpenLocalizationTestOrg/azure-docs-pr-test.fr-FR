---
title: "Charger des téraoctets de données dans SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: c29f1f01b660c4eb780e178a68036327fafa9ba6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="33f81-103">Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="33f81-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="33f81-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) est une base de données de mise à l’échelle basée sur le cloud qui prend en charge le traitement de grands volumes de données relationnelles et non relationnelles.</span><span class="sxs-lookup"><span data-stu-id="33f81-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="33f81-105">Reposant sur une architecture MPP (massively parallel processing), SQL Data Warehouse est optimisée pour les charges de travail d’entrepôt de données d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="33f81-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="33f81-106">Elle offre l’élasticité du cloud avec la flexibilité de mettre à l’échelle le stockage et d’exécuter le calcul indépendamment.</span><span class="sxs-lookup"><span data-stu-id="33f81-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span></span>

<span data-ttu-id="33f81-107">La prise en main d’Azure SQL Data Warehouse est désormais plus facile à l’aide **d’Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="33f81-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="33f81-108">Azure Data Factory est un service d’intégration de données cloud entièrement géré, qui peut être utilisé pour remplir une base de données SQL Data Warehouse avec les données de votre système existant. Cela vous permet de gagner un temps précieux lors de l’évaluation de SQL Data Warehouse et de la création de vos solutions d’analyse.</span><span class="sxs-lookup"><span data-stu-id="33f81-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="33f81-109">Voici les principaux avantages liés au chargement de données dans Azure SQL Data Warehouse à l’aide d’Azure Data Factory :</span><span class="sxs-lookup"><span data-stu-id="33f81-109">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="33f81-110">**Facilité de configuration** : assistant intuitif en 5 étapes sans script nécessaire.</span><span class="sxs-lookup"><span data-stu-id="33f81-110">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="33f81-111">**Prise en charge étendue du magasin de données** : prise en charge intégrée d’un ensemble complet de magasins de données locaux et sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="33f81-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="33f81-112">**Sécurité et conformité** : les données sont transférées via HTTPS ou ExpressRoute et la présence globale du service garantit que vos données ne quittent jamais les limites géographiques</span><span class="sxs-lookup"><span data-stu-id="33f81-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span></span>
* <span data-ttu-id="33f81-113">**Performances sans précédent à l’aide de PolyBase** : l’utilisation de Polybase est le moyen le plus efficace pour déplacer des données dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="33f81-113">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="33f81-114">À l’aide de la fonction blob intermédiaire, vous pouvez obtenir des vitesses de charge élevées pour tous les types de magasins de données en plus du Stockage Blob Azure, pris en charge par Polybase par défaut.</span><span class="sxs-lookup"><span data-stu-id="33f81-114">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span></span>

<span data-ttu-id="33f81-115">Cet article vous montre comment utiliser l’Assistant Copie de Data Factory pour charger 1 To de données depuis le Stockage Blob Azure dans Azure SQL Data Warehouse en moins de 15 minutes, à un débit de 1,2 Go/s minimum.</span><span class="sxs-lookup"><span data-stu-id="33f81-115">This article shows you how to use Data Factory Copy Wizard to load 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="33f81-116">Cet article fournit des instructions détaillées pour déplacer les données dans Azure SQL Data Warehouse à l’aide de l’Assistant Copie.</span><span class="sxs-lookup"><span data-stu-id="33f81-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="33f81-117">Pour des informations générales sur les fonctionnalités de Data Factory permettant de déplacer des données vers et depuis Azure SQL Data Warehouse, consultez [Déplacer des données vers et depuis Azure SQL Data Warehouse à l’aide d’Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md).</span><span class="sxs-lookup"><span data-stu-id="33f81-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="33f81-118">Vous pouvez également créer des pipelines à l’aide du portail Azure, de Visual Studio, de PowerShell, etc. Consultez le [Didacticiel : copie de données d’Azure Blob Storage vers une base de données SQL Azure](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir une brève procédure pas à pas de l’utilisation de l’activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="33f81-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="33f81-119">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="33f81-119">Prerequisites</span></span>
* <span data-ttu-id="33f81-120">Stockage Blob Azure : cette expérience utilise le Stockage Blob Azure (GRS) pour stocker un jeu de données de test TPC-H.</span><span class="sxs-lookup"><span data-stu-id="33f81-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="33f81-121">Si vous ne possédez pas de compte de stockage Azure, découvrez [comment créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="33f81-121">If you do not have an Azure storage account, learn [how to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="33f81-122">Données [TPC-H](http://www.tpc.org/tpch/) : nous allons utiliser TPC-H comme jeu de données de test.</span><span class="sxs-lookup"><span data-stu-id="33f81-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span></span>  <span data-ttu-id="33f81-123">Pour ce faire, vous devez utiliser `dbgen` dans le kit d’outils TPC-H, qui vous permet de générer le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="33f81-123">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span></span>  <span data-ttu-id="33f81-124">Vous pouvez télécharger le code source pour `dbgen` depuis [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) et le compiler vous-même, ou vous pouvez télécharger le fichier binaire compilé à partir de [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="33f81-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="33f81-125">Exécutez dbgen.exe avec les commandes suivantes pour générer le fichier plat de 1 To pour la table `lineitem` répartie entre 10 fichiers :</span><span class="sxs-lookup"><span data-stu-id="33f81-125">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="33f81-126">…</span><span class="sxs-lookup"><span data-stu-id="33f81-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="33f81-127">À présent, copiez les fichiers générés vers Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="33f81-127">Now copy the generated files to Azure Blob.</span></span>  <span data-ttu-id="33f81-128">Consultez [Déplacer des données vers et depuis un système de fichiers local à l’aide d’Azure Data Factory](data-factory-onprem-file-system-connector.md) pour savoir comment procéder à l’aide d’ADF Copy.</span><span class="sxs-lookup"><span data-stu-id="33f81-128">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span></span>    
* <span data-ttu-id="33f81-129">Azure SQL Data Warehouse : cette expérience charge des données dans Azure SQL Data Warehouse créé avec 6 000 DWU</span><span class="sxs-lookup"><span data-stu-id="33f81-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="33f81-130">Consultez [Créer un Azure SQL Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) pour obtenir des instructions détaillées sur la création d’une base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="33f81-130">Refer to [Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span></span>  <span data-ttu-id="33f81-131">Pour obtenir les meilleures performances possibles de charge dans SQL Data Warehouse à l’aide de Polybase, nous choisissons le nombre maximal d’unités de DWU (Data Warehouse Units) autorisé dans le paramètre Performance, qui est de 6 000 DWU.</span><span class="sxs-lookup"><span data-stu-id="33f81-131">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="33f81-132">Lors du chargement à partir d’Azure Blob, les performances de chargement des données sont directement proportionnelles au nombre de DWU configuré dans le SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="33f81-132">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="33f81-133">Le chargement de 1 To dans 1 000 DWU SQL Data Warehouse prend 87 minutes (débit d’environ 200 Mo/s). Le chargement de 1 To dans 2000 DWU SQL Data Warehouse prend 46 minutes (débit d’environ 380 Mo/s). Le chargement de 1 To dans 6 000 DWU SQL Data Warehouse prend 14 minutes (débit d’environ 1,2 Go/s).</span><span class="sxs-lookup"><span data-stu-id="33f81-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="33f81-134">Pour créer un SQL Data Warehouse avec 6 000 DWU, déplacez le curseur Performance complètement à droite :</span><span class="sxs-lookup"><span data-stu-id="33f81-134">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span></span>

    ![Curseur Performance](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="33f81-136">Pour une base de données existante qui n’est pas configurée avec 6 000 DWU, vous pouvez la mettre à l’échelle à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="33f81-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="33f81-137">Accédez à la base de données dans le portail Azure. Il existe un bouton **Mise à l’échelle** situé dans le panneau **Présentation** illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33f81-137">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span></span>

    ![Bouton Mise à l’échelle](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="33f81-139">Cliquez sur le bouton **Mise à l’échelle** pour ouvrir le panneau suivant, déplacez le curseur sur la valeur maximale, puis cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="33f81-139">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span></span>

    ![Boîte de dialogue de mise à l’échelle](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="33f81-141">Cette expérience charge des données dans Azure SQL Data Warehouse à l’aide de la classe de ressources `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="33f81-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="33f81-142">Pour obtenir le meilleur débit possible, la copie doit être effectuée à l’aide d’un utilisateur SQL Data Warehouse appartenant à la classe de ressources `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="33f81-142">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span></span>  <span data-ttu-id="33f81-143">Découvrez comment procéder en consultant [Exemple de modification d’une classe de ressources utilisateur](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="33f81-143">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="33f81-144">Créez le schéma de la table de destination dans la base de données Azure SQL Data Warehouse en exécutant l’instruction DDL suivante :</span><span class="sxs-lookup"><span data-stu-id="33f81-144">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span></span>

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
<span data-ttu-id="33f81-145">Une fois les étapes requises terminées, nous sommes désormais prêts à configurer l’activité de copie à l’aide de l’Assistant Copie.</span><span class="sxs-lookup"><span data-stu-id="33f81-145">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="33f81-146">Lancer l’Assistant Copie</span><span class="sxs-lookup"><span data-stu-id="33f81-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="33f81-147">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="33f81-147">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="33f81-148">Cliquez sur **+ NOUVEAU** en haut à gauche, sur **Intelligence et analyse**, puis sur **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="33f81-148">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="33f81-149">Dans le panneau **Nouvelle fabrique de données** :</span><span class="sxs-lookup"><span data-stu-id="33f81-149">In the **New data factory** blade:</span></span>

   1. <span data-ttu-id="33f81-150">Entrez **LoadIntoSQLDWDataFactory** pour le **nom**.</span><span class="sxs-lookup"><span data-stu-id="33f81-150">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span></span>
       <span data-ttu-id="33f81-151">Le nom de la fabrique de données Azure doit être un nom global unique.</span><span class="sxs-lookup"><span data-stu-id="33f81-151">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="33f81-152">Si l’erreur suivante s’affiche, changez le nom de la fabrique de données (par exemple, votrenomLoadIntoSQLDWDataFactory), puis tentez de la recréer : **Le nom de la fabrique de données « LoadIntoSQLDWDataFactory » n'est pas disponible**.</span><span class="sxs-lookup"><span data-stu-id="33f81-152">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="33f81-153">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="33f81-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="33f81-154">Sélectionnez votre **abonnement**Azure.</span><span class="sxs-lookup"><span data-stu-id="33f81-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="33f81-155">Pour Groupe de ressources, effectuez l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="33f81-155">For Resource Group, do one of the following steps:</span></span>
      1. <span data-ttu-id="33f81-156">Sélectionnez **Utiliser l’existant** pour sélectionner un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="33f81-156">Select **Use existing** to select an existing resource group.</span></span>
      2. <span data-ttu-id="33f81-157">Sélectionnez **Créer un nouveau** pour entrer un nom pour un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="33f81-157">Select **Create new** to enter a name for a resource group.</span></span>
   4. <span data-ttu-id="33f81-158">Sélectionnez un **emplacement** pour la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="33f81-158">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="33f81-159">Sélectionnez la case à cocher **Épingler au tableau de bord** en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="33f81-159">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="33f81-160">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="33f81-160">Click **Create**.</span></span>
4. <span data-ttu-id="33f81-161">Une fois la création terminée, le panneau **Data Factory** s’affiche comme sur l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="33f81-161">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>

   ![Page d'accueil Data Factory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="33f81-163">Dans la page d’accueil Fabrique de données, cliquez sur la vignette **Copier les données** pour lancer l’**Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="33f81-163">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="33f81-164">Si vous voyez que le navigateur web est bloqué au niveau « Autorisation... », désactivez/décochez l’option **Block third party cookies and site data** (Bloquer les cookies et les données de site tiers) (ou) laissez cette option activée et créez une exception pour **login.microsoftonline.com**, puis essayez de relancer l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="33f81-164">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="33f81-165">Étape 1 : Configurer la planification du chargement de données</span><span class="sxs-lookup"><span data-stu-id="33f81-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="33f81-166">La première étape consiste à configurer la planification du chargement de données.</span><span class="sxs-lookup"><span data-stu-id="33f81-166">The first step is to configure the data loading schedule.</span></span>  

<span data-ttu-id="33f81-167">Dans la page **Propriétés** :</span><span class="sxs-lookup"><span data-stu-id="33f81-167">In the **Properties** page:</span></span>

1. <span data-ttu-id="33f81-168">Entrez **CopyFromBlobToAzureSqlDataWarehouse** comme **Nom de la tâche**</span><span class="sxs-lookup"><span data-stu-id="33f81-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="33f81-169">Sélectionnez l’option **Exécuter une fois**.</span><span class="sxs-lookup"><span data-stu-id="33f81-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="33f81-170">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="33f81-170">Click **Next**.</span></span>  

    ![Assistant Copie - Page Propriétés](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="33f81-172">Étape 2 : Configurer la source</span><span class="sxs-lookup"><span data-stu-id="33f81-172">Step 2: Configure source</span></span>
<span data-ttu-id="33f81-173">Cette section décrit les étapes pour configurer la source : Azure Blob contenant les fichiers d’éléments de ligne TPC-H 1 To.</span><span class="sxs-lookup"><span data-stu-id="33f81-173">This section shows you the steps to configure the source: Azure Blob containing the 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="33f81-174">Sélectionnez **Stockage Blob Azure** comme magasin de données et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="33f81-174">Select the **Azure Blob Storage** as the data store and click **Next**.</span></span>

    ![Assistant Copie - Page Sélectionner la source](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="33f81-176">Renseignez les informations de connexion pour le compte Stockage Blob Azure, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="33f81-176">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span></span>

    ![Assistant Copie - Informations de connexion à la source](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="33f81-178">Choisissez le **dossier** contenant les fichiers d’éléments de ligne TPC-H et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="33f81-178">Choose the **folder** containing the TPC-H line item files and click **Next**.</span></span>

    ![Assistant Copie - Sélectionner le dossier d’entrée](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="33f81-180">Lorsque vous cliquez sur **Suivant**, les paramètres de format de fichier sont détectés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="33f81-180">Upon clicking **Next**, the file format settings are detected automatically.</span></span>  <span data-ttu-id="33f81-181">Vérifiez que le délimiteur de colonne est « | » au lieu de la virgule par défaut « , ».</span><span class="sxs-lookup"><span data-stu-id="33f81-181">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span></span>  <span data-ttu-id="33f81-182">Cliquez sur **Suivant** une fois que vous avez affiché un aperçu des données.</span><span class="sxs-lookup"><span data-stu-id="33f81-182">Click **Next** after you have previewed the data.</span></span>

    ![Assistant Copie - Paramètres de format de fichier](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="33f81-184">Étape 3 : Configurer la destination</span><span class="sxs-lookup"><span data-stu-id="33f81-184">Step 3: Configure destination</span></span>
<span data-ttu-id="33f81-185">Cette section vous montre comment configurer la destination : la table `lineitem` dans la base de données Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="33f81-185">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="33f81-186">Choisissez **Azure SQL Data Warehouse** comme magasin de destination et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="33f81-186">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span></span>

    ![Assistant Copie - Sélectionner le magasin de données de destination](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="33f81-188">Renseignez les informations de connexion pour Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="33f81-188">Fill in the connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="33f81-189">Veillez à spécifier l’utilisateur qui est membre du rôle `xlargerc` (voir les **conditions préalables** pour obtenir des instructions détaillées), puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="33f81-189">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Assistant Copie - Informations de connexion à la destination](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="33f81-191">Choisissez la table de destination et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="33f81-191">Choose the destination table and click **Next**.</span></span>

    ![Assistant Copie - Page Mappage de table](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="33f81-193">Dans la page Mappage de schéma, laissez l’option « Appliquer le mappage de colonnes » décochée et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="33f81-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="33f81-194">Étape 4 : Paramètres de performance</span><span class="sxs-lookup"><span data-stu-id="33f81-194">Step 4: Performance settings</span></span>

<span data-ttu-id="33f81-195">La case **Autoriser Polybase** est cochée par défaut.</span><span class="sxs-lookup"><span data-stu-id="33f81-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="33f81-196">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="33f81-196">Click **Next**.</span></span>

![Assistant Copie - Page Mappage de schéma](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="33f81-198">Étape 5 : Déployer et surveiller les résultats du chargement</span><span class="sxs-lookup"><span data-stu-id="33f81-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="33f81-199">Cliquez sur le bouton **Terminer** pour déployer.</span><span class="sxs-lookup"><span data-stu-id="33f81-199">Click **Finish** button to deploy.</span></span>

    ![Assistant Copie - Page Résumé](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="33f81-201">Une fois le déploiement terminé, cliquez sur `Click here to monitor copy pipeline` pour surveiller la progression de l’exécution de la copie.</span><span class="sxs-lookup"><span data-stu-id="33f81-201">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span></span> <span data-ttu-id="33f81-202">Sélectionner le pipeline de copie que vous avez créé dans la liste **Fenêtres d’activité**.</span><span class="sxs-lookup"><span data-stu-id="33f81-202">Select the copy pipeline you created in the **Activity Windows** list.</span></span>

    ![Assistant Copie - Page Résumé](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="33f81-204">Vous pouvez afficher les détails de l’exécution de la copie dans **l’Explorateur de fenêtres d’activité** dans le panneau de droite, notamment le volume de données lu à partir de la source et écrit dans la destination, la durée et le débit moyen de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="33f81-204">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span></span>

    <span data-ttu-id="33f81-205">Comme vous pouvez le voir dans la capture d’écran suivante, la copie de 1 To à partir du Stockage Blob Azure vers SQL Data Warehouse a pris 14 minutes, avec un débit de 1,22 Gbits/s !</span><span class="sxs-lookup"><span data-stu-id="33f81-205">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Assistant Copie - Boîte de dialogue Succès](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="33f81-207">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="33f81-207">Best practices</span></span>
<span data-ttu-id="33f81-208">Voici quelques meilleures pratiques pour l’exécution de votre base de données Azure SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="33f81-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="33f81-209">Utilisez une classe de ressources supérieure lors du chargement dans un INDEX COLUMNSTORE EN CLUSTER.</span><span class="sxs-lookup"><span data-stu-id="33f81-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="33f81-210">Pour des jonctions plus efficaces, envisagez d’utiliser la distribution par hachage en fonction d’une colonne sélectionnée au lieu de la distribution par tourniquet (round robin) par défaut.</span><span class="sxs-lookup"><span data-stu-id="33f81-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="33f81-211">Pour des vitesses de chargement plus rapides, envisagez d’utiliser des tas pour les données temporaires.</span><span class="sxs-lookup"><span data-stu-id="33f81-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="33f81-212">Créez des statistiques une fois le chargement Azure SQL Data Warehouse terminé.</span><span class="sxs-lookup"><span data-stu-id="33f81-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="33f81-213">Pour plus d’informations, consultez [Meilleures pratiques pour Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="33f81-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33f81-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="33f81-214">Next steps</span></span>
* <span data-ttu-id="33f81-215">[Assistant Copie de Data Factory](data-factory-copy-wizard.md) : cet article fournit des détails sur l’Assistant Copie.</span><span class="sxs-lookup"><span data-stu-id="33f81-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span></span>
* <span data-ttu-id="33f81-216">[Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) : cet article contient le guide sur le réglage et les mesures de performances de référence.</span><span class="sxs-lookup"><span data-stu-id="33f81-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span></span>
