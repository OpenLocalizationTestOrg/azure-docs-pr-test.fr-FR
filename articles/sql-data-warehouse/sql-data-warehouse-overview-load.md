---
title: "Chargement de données dans Azure SQL Data Warehouse | Microsoft Docs"
description: "Découvrez les scénarios courants de chargement des données dans SQL Data Warehouse. Ceux-ci incluent l’utilisation de PolyBase, d’Azure Blob Storage et de fichiers plats ainsi que l’envoi de disques. Vous pouvez également utiliser des outils tiers."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: c4199a387f5cdbd477a5e348e48ba8e8b5900075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="1114d-105">Chargement de données dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1114d-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="1114d-106">Résumé des options de scénario et des recommandations applicables au chargement de données dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1114d-106">A summary of the scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="1114d-107">L’étape la plus difficile du chargement de données consiste généralement en la préparation des données à charger.</span><span class="sxs-lookup"><span data-stu-id="1114d-107">The hardest part of loading data is usually preparing the data for the load.</span></span> <span data-ttu-id="1114d-108">Azure simplifie le processus de chargement en utilisant Azure Blob Storage comme magasin de données commun pour la plupart des services, et en utilisant Azure Data Factory pour orchestrer la communication et le déplacement des données entre les services Azure.</span><span class="sxs-lookup"><span data-stu-id="1114d-108">Azure simplifies loading by using Azure blob storage as a common data store for many of the services, and using Azure Data Factory to orchestrate communication and data movement between the Azure services.</span></span> <span data-ttu-id="1114d-109">Ces processus sont intégrés à la technologie PolyBase qui utilise le traitement massivement parallèle (MPP) pour charger des données en parallèle dans SQL Data Warehouse à partir d’Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1114d-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) to load data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="1114d-110">Pour accéder à des didacticiels décrivant le chargement d’exemples de bases de données, consultez l’article [Charger des exemples de données dans SQL Data Warehouse][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="1114d-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="1114d-111">Chargement à partir d’Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="1114d-111">Load from Azure blob storage</span></span>
<span data-ttu-id="1114d-112">Le moyen le plus rapide d’importer des données dans SQL Data Warehouse consiste à utiliser PolyBase pour charger des données à partir d’Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1114d-112">The fastest way to import data into SQL Data Warehouse is to use PolyBase to load data from Azure blob storage.</span></span> <span data-ttu-id="1114d-113">PolyBase utilise le traitement massivement parallèle (MPP) de SQL Data Warehouse pour charger des données en parallèle à partir d’Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1114d-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design to load data in parallel from Azure blob storage.</span></span> <span data-ttu-id="1114d-114">Pour utiliser PolyBase, vous pouvez faire appel aux commandes T-SQL ou à un pipeline Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1114d-114">To use PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="1114d-115">1. Utilisation de PolyBase et de T-SQL</span><span class="sxs-lookup"><span data-stu-id="1114d-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="1114d-116">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="1114d-116">Summary of loading process:</span></span>

1. <span data-ttu-id="1114d-117">Déplacez vos données vers Azure Blob Storage ou Azure Data Lake Store et enregistrez-les dans des fichiers texte.</span><span class="sxs-lookup"><span data-stu-id="1114d-117">Move your data to Azure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="1114d-118">Configurez les objets externes dans SQL Data Warehouse pour définir l’emplacement et le format des données.</span><span class="sxs-lookup"><span data-stu-id="1114d-118">Configure external objects in SQL Data Warehouse to define the location and format of the data</span></span>
3. <span data-ttu-id="1114d-119">Exécutez une commande T-SQL pour charger les données en parallèle dans une nouvelle table de base de données.</span><span class="sxs-lookup"><span data-stu-id="1114d-119">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="1114d-120">Pour accéder à un didacticiel, consultez [Charger les données de stockage d’objets blob Azure dans SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="1114d-120">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="1114d-121">2. Utilisation d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1114d-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="1114d-122">Pour utiliser PolyBase plus simplement, vous pouvez créer un pipeline Azure Data Factory qui utilise PolyBase pour charger des données dans SQL Data Warehouse à partir d’Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1114d-122">For a simpler way to use PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase to load data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="1114d-123">Cette approche permet une configuration plus rapide, car vous n’avez pas à définir les objets T-SQL.</span><span class="sxs-lookup"><span data-stu-id="1114d-123">This is fast to configure since you don't need to define the T-SQL objects.</span></span> <span data-ttu-id="1114d-124">Si vous avez besoin d’interroger les données externes sans les importer, utilisez T-SQL.</span><span class="sxs-lookup"><span data-stu-id="1114d-124">If you need to query the external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="1114d-125">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="1114d-125">Summary of loading process:</span></span>

1. <span data-ttu-id="1114d-126">Déplacez vos données vers Azure Blob Storage et enregistrez-les dans des fichiers texte.</span><span class="sxs-lookup"><span data-stu-id="1114d-126">Move your data to Azure blob storage and store it in text files.</span></span> <span data-ttu-id="1114d-127">(Azure Data Factory ne prend pas en charge la connectivité ADLS avec PolyBase pour le moment.)</span><span class="sxs-lookup"><span data-stu-id="1114d-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="1114d-128">Créez un pipeline Azure Data Factory pour recevoir les données.</span><span class="sxs-lookup"><span data-stu-id="1114d-128">Create an Azure Data Factory pipeline to ingest the data.</span></span> <span data-ttu-id="1114d-129">Utilisez l’option PolyBase.</span><span class="sxs-lookup"><span data-stu-id="1114d-129">Use the PolyBase option.</span></span>
4. <span data-ttu-id="1114d-130">Planifiez et exécutez le pipeline.</span><span class="sxs-lookup"><span data-stu-id="1114d-130">Schedule and run the pipeline.</span></span>

<span data-ttu-id="1114d-131">Pour accéder à un didacticiel, consultez [Charger les données conservées dans un stockage d’objets blob Azure dans Azure SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="1114d-131">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="1114d-132">Chargement à partir de SQL Server</span><span class="sxs-lookup"><span data-stu-id="1114d-132">Load from SQL Server</span></span>
<span data-ttu-id="1114d-133">Pour charger des données dans SQL Data Warehouse à partir de SQL Server, vous pouvez utiliser Integration Services (SSIS), transférer des fichiers plats ou envoyer des disques à Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1114d-133">To load data from SQL Server to SQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks to Microsoft.</span></span> <span data-ttu-id="1114d-134">Poursuivez la lecture de ce document pour obtenir un résumé des différents processus de chargement et accéder à des liens vers des didacticiels.</span><span class="sxs-lookup"><span data-stu-id="1114d-134">Read on to see a summary of the different loading processes and links to tutorials.</span></span>

<span data-ttu-id="1114d-135">Pour planifier une migration complète des données dans SQL Data Warehouse à partir de SQL Server, consultez la [vue d’ensemble de la migration][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="1114d-135">To plan a full data migration from SQL Server to SQL Data Warehouse, see the [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="1114d-136">Utilisation d’Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="1114d-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="1114d-137">Si vous utilisez déjà les packages Integration Services (SSIS) pour le chargement de données dans SQL Server, vous pouvez mettre à jour vos packages afin d’utiliser SQL Server comme source et SQL Data Warehouse comme destination.</span><span class="sxs-lookup"><span data-stu-id="1114d-137">If you are already using Integration Services (SSIS) packages to load into SQL Server, you can update your packages to use SQL Server as the source and SQL Data Warehouse as the destination.</span></span> <span data-ttu-id="1114d-138">Facile et rapide, cette approche est idéale si vous ne voulez pas migrer votre processus de chargement pour utiliser des données déjà stockées dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="1114d-138">This is quick and easy to do, and is a good choice if you are not trying to migrate your loading process to use data already in the cloud.</span></span> <span data-ttu-id="1114d-139">La charge sera toutefois plus lente que lorsque vous utilisez PolyBase, car SSIS n’effectue pas de chargement en parallèle.</span><span class="sxs-lookup"><span data-stu-id="1114d-139">The tradeoff is the load will be slower than using PolyBase because this SSIS does not perform the load in parallel.</span></span>

<span data-ttu-id="1114d-140">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="1114d-140">Summary of loading process:</span></span>

1. <span data-ttu-id="1114d-141">Modifiez votre package Integration Services de sorte qu’il pointe vers l’instance SQL Server pour la source et vers la base de données SQL Data Warehouse pour la destination.</span><span class="sxs-lookup"><span data-stu-id="1114d-141">Revise your Integration Services package to point to the SQL Server instance for the source and the SQL Data Warehouse database for the destination.</span></span>
2. <span data-ttu-id="1114d-142">Migrez votre schéma vers SQL Data Warehouse si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="1114d-142">Migrate your schema to SQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="1114d-143">Modifiez le mappage dans vos packages et utilisez uniquement les types de données pris en charge par SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1114d-143">Change the mapping in your packages use only the data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="1114d-144">Planifiez et exécutez le package.</span><span class="sxs-lookup"><span data-stu-id="1114d-144">Schedule and run the package.</span></span>

<span data-ttu-id="1114d-145">Pour accéder à un didacticiel, consultez [Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="1114d-145">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="1114d-146">Utilisation d’AZCopy (recommandé pour des données de moins de 10 To)</span><span class="sxs-lookup"><span data-stu-id="1114d-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="1114d-147">Si la taille de vos données est inférieure à 10 To, vous pouvez exporter les données à partir de SQL Server dans des fichiers plats, copier les fichiers vers Azure Blob Storage, puis utiliser PolyBase pour charger les données dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1114d-147">If your data size is < 10 TB, you can export the data from SQL Server to flat files, copy the files to Azure blob storage, and then use PolyBase to load the data into SQL Data Warehouse</span></span>

<span data-ttu-id="1114d-148">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="1114d-148">Summary of loading process:</span></span>

1. <span data-ttu-id="1114d-149">Utilisez l’utilitaire de ligne de commande bcp pour exporter des données de SQL Server vers des fichiers plats.</span><span class="sxs-lookup"><span data-stu-id="1114d-149">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="1114d-150">Utilisez l’utilitaire de ligne de commande AZCopy pour copier les données de fichiers plats vers Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1114d-150">Use the AZCopy command-line utility to copy data from flat files to Azure blob storage.</span></span>
3. <span data-ttu-id="1114d-151">Utilisez PolyBase pour charger des données dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1114d-151">Use PolyBase to load into SQL Data Warehouse.</span></span>

<span data-ttu-id="1114d-152">Pour accéder à un didacticiel, consultez [Charger les données de stockage d’objets blob Azure dans SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="1114d-152">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="1114d-153">Utilisation de bcp</span><span class="sxs-lookup"><span data-stu-id="1114d-153">Use bcp</span></span>
<span data-ttu-id="1114d-154">Si vous disposez d’une petite quantité de données, vous pouvez utiliser l’utilitaire bcp pour charger des données directement dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1114d-154">If you have a small amount of data you can use bcp to load directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="1114d-155">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="1114d-155">Summary of loading process:</span></span>

1. <span data-ttu-id="1114d-156">Utilisez l’utilitaire de ligne de commande bcp pour exporter des données de SQL Server vers des fichiers plats.</span><span class="sxs-lookup"><span data-stu-id="1114d-156">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="1114d-157">Utilisez bcp pour charger des données de fichiers plats directement vers SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1114d-157">Use bcp to load data from flat files directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="1114d-158">Pour accéder à un didacticiel, consultez [Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (fichiers plats)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="1114d-158">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="1114d-159">Utilisation des fonctions d’importation/exportation (recommandé pour les données supérieures à 10 To)</span><span class="sxs-lookup"><span data-stu-id="1114d-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="1114d-160">Si la taille de vos données est supérieure à 10 To et que vous souhaitez les déplacer vers Azure, nous vous recommandons d’utiliser notre service d’expédition de disque [Import/Export][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="1114d-160">If your data size is > 10 TB and you want to move it to Azure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="1114d-161">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="1114d-161">Summary of loading process</span></span>

1. <span data-ttu-id="1114d-162">Utilisez l’utilitaire de ligne de commande bcp pour exporter des données de SQL Server vers des fichiers plats sur des disques transférables.</span><span class="sxs-lookup"><span data-stu-id="1114d-162">Use the bcp command-line utility to export data from SQL Server to flat files on transferrable disks.</span></span>
2. <span data-ttu-id="1114d-163">Expédiez les disques à Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1114d-163">Ship the disks to Microsoft.</span></span>
3. <span data-ttu-id="1114d-164">Microsoft charge les données dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1114d-164">Microsoft loads the data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="1114d-165">Charger à partir de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1114d-165">Load from HDInsight</span></span>
<span data-ttu-id="1114d-166">SQL Data Warehouse prend en charge le chargement des données à partir de HDInsight par le biais de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="1114d-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="1114d-167">Le processus est le même que pour le chargement des données à partir du stockage d’objets Blob Azure : utilisation de PolyBase pour se connecter à HDInsight pour charger des données.</span><span class="sxs-lookup"><span data-stu-id="1114d-167">The process is the same as loading data from Azure Blob Storage - using PolyBase to connect to HDInsight to load data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="1114d-168">1. Utilisation de PolyBase et de T-SQL</span><span class="sxs-lookup"><span data-stu-id="1114d-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="1114d-169">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="1114d-169">Summary of loading process:</span></span>

1. <span data-ttu-id="1114d-170">Déplacer vos données vers HDInsight et les stocker dans des fichiers texte, au format ORC ou Parquet.</span><span class="sxs-lookup"><span data-stu-id="1114d-170">Move your data to HDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="1114d-171">Configurez les objets externes dans SQL Data Warehouse pour définir l’emplacement et le format des données.</span><span class="sxs-lookup"><span data-stu-id="1114d-171">Configure external objects in SQL Data Warehouse to define the location and format of the data.</span></span>
3. <span data-ttu-id="1114d-172">Exécutez une commande T-SQL pour charger les données en parallèle dans une nouvelle table de base de données.</span><span class="sxs-lookup"><span data-stu-id="1114d-172">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<span data-ttu-id="1114d-173">Pour accéder à un didacticiel, consultez [Charger les données de stockage d’objets blob Azure dans SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="1114d-173">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="1114d-174">Recommandations</span><span class="sxs-lookup"><span data-stu-id="1114d-174">Recommendations</span></span>
<span data-ttu-id="1114d-175">La plupart de nos partenaires proposent des solutions de chargement.</span><span class="sxs-lookup"><span data-stu-id="1114d-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="1114d-176">Pour en savoir plus, consultez la liste de nos [partenaires de solutions][solution partners].</span><span class="sxs-lookup"><span data-stu-id="1114d-176">To find out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="1114d-177">Si vos données proviennent d’une source non relationnelle et que vous souhaitez les charger dans SQL Data Warehouse, vous devez transformer ces données en lignes et en colonnes avant de les charger.</span><span class="sxs-lookup"><span data-stu-id="1114d-177">If your data is coming from a non-relational source and you want to load it into SQL Data Warehouse you will need to transform it into rows and columns before you load it.</span></span> <span data-ttu-id="1114d-178">Il n’est pas nécessaire de stocker les données transformées dans une base de données ; de simples fichiers texte suffisent.</span><span class="sxs-lookup"><span data-stu-id="1114d-178">The transformed data doesn't need to be stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="1114d-179">Créer des statistiques sur des données nouvellement chargées.</span><span class="sxs-lookup"><span data-stu-id="1114d-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="1114d-180">Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="1114d-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="1114d-181">Pour optimiser les performances de vos requêtes, il est important de créer des statistiques sur toutes les colonnes de toutes les tables après le premier chargement ou après toute modification substantielle dans les données.</span><span class="sxs-lookup"><span data-stu-id="1114d-181">In order to get the best performance from your queries, it's important to create statistics on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="1114d-182">Pour plus d’informations, consultez [Statistiques][Statistics].</span><span class="sxs-lookup"><span data-stu-id="1114d-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="1114d-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1114d-183">Next steps</span></span>
<span data-ttu-id="1114d-184">Pour obtenir des conseils supplémentaires sur le développement, consultez la [vue d’ensemble sur le développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="1114d-184">For more development tips, see the [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server to Azure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server to Azure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
