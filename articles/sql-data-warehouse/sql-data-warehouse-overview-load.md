---
title: "données aaaLoad dans Azure SQL Data Warehouse | Documents Microsoft"
description: "Découvrez les scénarios courants de hello pour les données à charger dans l’entrepôt de données SQL. Ceux-ci incluent l’utilisation de PolyBase, d’Azure Blob Storage et de fichiers plats ainsi que l’envoi de disques. Vous pouvez également utiliser des outils tiers."
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
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="9ffc4-105">Chargement de données dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9ffc4-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="9ffc4-106">Résumé des options de scénario hello et des recommandations pour le chargement des données dans l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-106">A summary of hello scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="9ffc4-107">Hello plus difficiles le chargement des données est généralement préparation des données de hello pour la charge hello.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-107">hello hardest part of loading data is usually preparing hello data for hello load.</span></span> <span data-ttu-id="9ffc4-108">Azure simplifie le chargement à l’aide du stockage d’objets blob Azure comme une banque de données commune pour un grand nombre de services de hello et à l’aide d’Azure Data Factory le hello tooorchestrate communication et déplacement des données entre des services Azure.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-108">Azure simplifies loading by using Azure blob storage as a common data store for many of hello services, and using Azure Data Factory tooorchestrate communication and data movement between hello Azure services.</span></span> <span data-ttu-id="9ffc4-109">Ces processus sont intégrés à la technologie PolyBase qui utilise massivement parallèle du traitement des données de tooload de (MPP) en parallèle à partir du stockage d’objets blob Azure dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) tooload data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="9ffc4-110">Pour accéder à des didacticiels décrivant le chargement d’exemples de bases de données, consultez l’article [Charger des exemples de données dans SQL Data Warehouse][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="9ffc4-111">Chargement à partir d’Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="9ffc4-111">Load from Azure blob storage</span></span>
<span data-ttu-id="9ffc4-112">Hello plus rapide des tooimport données dans l’entrepôt de données SQL sont toouse PolyBase les données de tooload depuis le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-112">hello fastest way tooimport data into SQL Data Warehouse is toouse PolyBase tooload data from Azure blob storage.</span></span> <span data-ttu-id="9ffc4-113">PolyBase utilise SQL Data Warehouse traitement hautement parallèle des données de tooload de conception (MPP) en parallèle à partir du stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design tooload data in parallel from Azure blob storage.</span></span> <span data-ttu-id="9ffc4-114">toouse PolyBase, vous pouvez utiliser les commandes T-SQL ou un pipeline Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-114">toouse PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="9ffc4-115">1. Utilisation de PolyBase et de T-SQL</span><span class="sxs-lookup"><span data-stu-id="9ffc4-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="9ffc4-116">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="9ffc4-116">Summary of loading process:</span></span>

1. <span data-ttu-id="9ffc4-117">Déplacez la Azure Data Lake Store ou le stockage d’objets blob de données tooAzure et stockez-le dans des fichiers texte.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-117">Move your data tooAzure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="9ffc4-118">Configurer des objets externes dans l’emplacement de l’entrepôt de données SQL toodefine hello et un format de données de hello</span><span class="sxs-lookup"><span data-stu-id="9ffc4-118">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data</span></span>
3. <span data-ttu-id="9ffc4-119">Exécuter les données de salutation tooload une commande T-SQL en parallèle dans une nouvelle table de base de données.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-119">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="9ffc4-120">Pour obtenir un didacticiel, consultez [charger des données à partir de tooSQL de stockage d’objets blob Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-120">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="9ffc4-121">2. Utilisation d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9ffc4-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="9ffc4-122">Pour un moyen plus simple toouse PolyBase, vous pouvez créer un pipeline Azure Data Factory qui utilise des données de tooload PolyBase à partir du stockage d’objets blob Azure dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-122">For a simpler way toouse PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase tooload data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="9ffc4-123">Il s’agit de tooconfigure rapide, car vous n’avez pas besoin d’objets de toodefine hello T-SQL.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-123">This is fast tooconfigure since you don't need toodefine hello T-SQL objects.</span></span> <span data-ttu-id="9ffc4-124">Si vous avez besoin des données externes tooquery hello sans les importer, utilisez T-SQL.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-124">If you need tooquery hello external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="9ffc4-125">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="9ffc4-125">Summary of loading process:</span></span>

1. <span data-ttu-id="9ffc4-126">Déplacez votre stockage d’objets blob de données tooAzure et stockez-le dans des fichiers texte.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-126">Move your data tooAzure blob storage and store it in text files.</span></span> <span data-ttu-id="9ffc4-127">(Azure Data Factory ne prend pas en charge la connectivité ADLS avec PolyBase pour le moment.)</span><span class="sxs-lookup"><span data-stu-id="9ffc4-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="9ffc4-128">Créer une pipeline Azure Data Factory tooingest des données hello.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-128">Create an Azure Data Factory pipeline tooingest hello data.</span></span> <span data-ttu-id="9ffc4-129">Utilisez l’option de PolyBase hello.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-129">Use hello PolyBase option.</span></span>
4. <span data-ttu-id="9ffc4-130">Planifier et exécuter le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-130">Schedule and run hello pipeline.</span></span>

<span data-ttu-id="9ffc4-131">Pour obtenir un didacticiel, consultez [charger des données à partir de tooSQL de stockage d’objets blob Azure Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-131">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="9ffc4-132">Chargement à partir de SQL Server</span><span class="sxs-lookup"><span data-stu-id="9ffc4-132">Load from SQL Server</span></span>
<span data-ttu-id="9ffc4-133">tooload tooSQL de SQL Server Data Warehouse, vous pouvez utiliser Integration Services (SSIS), transfert de fichiers plats ou expédier les disques tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-133">tooload data from SQL Server tooSQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks tooMicrosoft.</span></span> <span data-ttu-id="9ffc4-134">Lire un résumé de hello différent du chargement de processus et les liens tootutorials sur toosee.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-134">Read on toosee a summary of hello different loading processes and links tootutorials.</span></span>

<span data-ttu-id="9ffc4-135">tooplan une migration complète des données à partir de SQL Server tooSQL entrepôt de données, consultez hello [présentation de la Migration][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-135">tooplan a full data migration from SQL Server tooSQL Data Warehouse, see hello [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="9ffc4-136">Utilisation d’Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="9ffc4-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="9ffc4-137">Si vous utilisez déjà tooload de packages Integration Services (SSIS) dans SQL Server, vous pouvez mettre à jour votre toouse de packages SQL Server en tant que source de hello et l’entrepôt de données SQL en tant que destination de hello.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-137">If you are already using Integration Services (SSIS) packages tooload into SQL Server, you can update your packages toouse SQL Server as hello source and SQL Data Warehouse as hello destination.</span></span> <span data-ttu-id="9ffc4-138">Cela est rapide et facile toodo, et constitue un bon choix si vous n’essayez pas toomigrate votre chargement traiter les données toouse déjà dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-138">This is quick and easy toodo, and is a good choice if you are not trying toomigrate your loading process toouse data already in hello cloud.</span></span> <span data-ttu-id="9ffc4-139">compromis de Hello est la charge de hello sera plus lente que l’utilisation de PolyBase, car cette SSIS n’effectue pas de charge de hello en parallèle.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-139">hello tradeoff is hello load will be slower than using PolyBase because this SSIS does not perform hello load in parallel.</span></span>

<span data-ttu-id="9ffc4-140">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="9ffc4-140">Summary of loading process:</span></span>

1. <span data-ttu-id="9ffc4-141">Passez en revue votre instance de SQL Server Integration Services package toopoint toohello pour la source de hello et base de données de l’entrepôt de données SQL hello pour la destination de hello.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-141">Revise your Integration Services package toopoint toohello SQL Server instance for hello source and hello SQL Data Warehouse database for hello destination.</span></span>
2. <span data-ttu-id="9ffc4-142">Migrez votre tooSQL schéma entrepôt de données, s’il n’y ne figure pas déjà.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-142">Migrate your schema tooSQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="9ffc4-143">Mappage de hello de modification dans vos packages d’utiliser uniquement les types de données de hello sont pris en charge par SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-143">Change hello mapping in your packages use only hello data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="9ffc4-144">Planifier et exécuter le package de hello.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-144">Schedule and run hello package.</span></span>

<span data-ttu-id="9ffc4-145">Pour obtenir un didacticiel, consultez [charger des données à partir de SQL Server tooAzure l’entrepôt de données SQL (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-145">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="9ffc4-146">Utilisation d’AZCopy (recommandé pour des données de moins de 10 To)</span><span class="sxs-lookup"><span data-stu-id="9ffc4-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="9ffc4-147">Si la taille de vos données est < 10 To, vous pouvez exporter les données de salutation à partir de fichiers tooflat de SQL Server, copiez le stockage d’objets blob tooAzure hello fichiers et ensuite utiliser les données de salutation tooload PolyBase dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9ffc4-147">If your data size is < 10 TB, you can export hello data from SQL Server tooflat files, copy hello files tooAzure blob storage, and then use PolyBase tooload hello data into SQL Data Warehouse</span></span>

<span data-ttu-id="9ffc4-148">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="9ffc4-148">Summary of loading process:</span></span>

1. <span data-ttu-id="9ffc4-149">Utiliser les données de tooexport salutation bcp utilitaire de ligne de commande à partir de fichiers tooflat de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-149">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="9ffc4-150">Utiliser des données de toocopy hello AZCopy utilitaire de ligne de commande de stockage d’objets blob tooAzure fichiers plats.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-150">Use hello AZCopy command-line utility toocopy data from flat files tooAzure blob storage.</span></span>
3. <span data-ttu-id="9ffc4-151">Utilisez PolyBase tooload dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-151">Use PolyBase tooload into SQL Data Warehouse.</span></span>

<span data-ttu-id="9ffc4-152">Pour obtenir un didacticiel, consultez [charger des données à partir de tooSQL de stockage d’objets blob Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-152">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="9ffc4-153">Utilisation de bcp</span><span class="sxs-lookup"><span data-stu-id="9ffc4-153">Use bcp</span></span>
<span data-ttu-id="9ffc4-154">Si vous avez une petite quantité de données, vous pouvez utiliser bcp tooload directement dans l’entrepôt de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-154">If you have a small amount of data you can use bcp tooload directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="9ffc4-155">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="9ffc4-155">Summary of loading process:</span></span>

1. <span data-ttu-id="9ffc4-156">Utiliser les données de tooexport salutation bcp utilitaire de ligne de commande à partir de fichiers tooflat de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-156">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="9ffc4-157">Utiliser les données de tooload de bcp de plat les fichiers directement tooSQL l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-157">Use bcp tooload data from flat files directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="9ffc4-158">Pour obtenir un didacticiel, consultez [charger des données à partir de SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-158">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="9ffc4-159">Utilisation des fonctions d’importation/exportation (recommandé pour les données supérieures à 10 To)</span><span class="sxs-lookup"><span data-stu-id="9ffc4-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="9ffc4-160">Si la taille de vos données est de 10 To > et que vous souhaitez toomove il tooAzure, nous vous recommandons d’utiliser notre service d’expédition de disque [Import/Export][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-160">If your data size is > 10 TB and you want toomove it tooAzure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="9ffc4-161">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="9ffc4-161">Summary of loading process</span></span>

1. <span data-ttu-id="9ffc4-162">Utiliser données tooexport de hello bcp utilitaire de ligne de commande à partir de fichiers tooflat de SQL Server sur des disques transférables.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-162">Use hello bcp command-line utility tooexport data from SQL Server tooflat files on transferrable disks.</span></span>
2. <span data-ttu-id="9ffc4-163">Expédier hello disques tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-163">Ship hello disks tooMicrosoft.</span></span>
3. <span data-ttu-id="9ffc4-164">Microsoft charge les données de salutation dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9ffc4-164">Microsoft loads hello data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="9ffc4-165">Charger à partir de HDInsight</span><span class="sxs-lookup"><span data-stu-id="9ffc4-165">Load from HDInsight</span></span>
<span data-ttu-id="9ffc4-166">SQL Data Warehouse prend en charge le chargement des données à partir de HDInsight par le biais de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="9ffc4-167">processus de Hello est hello identique à celui du chargement de données à partir du stockage d’objets Blob Azure - à l’aide de données de PolyBase tooconnect tooHDInsight tooload.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-167">hello process is hello same as loading data from Azure Blob Storage - using PolyBase tooconnect tooHDInsight tooload data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="9ffc4-168">1. Utilisation de PolyBase et de T-SQL</span><span class="sxs-lookup"><span data-stu-id="9ffc4-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="9ffc4-169">Résumé du processus de chargement :</span><span class="sxs-lookup"><span data-stu-id="9ffc4-169">Summary of loading process:</span></span>

1. <span data-ttu-id="9ffc4-170">Déplacez votre tooHDInsight de données et les stocker dans des fichiers texte, format ORC ou Parquet.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-170">Move your data tooHDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="9ffc4-171">Configurer des objets externes dans l’emplacement de l’entrepôt de données SQL toodefine hello et un format de données de hello.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-171">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data.</span></span>
3. <span data-ttu-id="9ffc4-172">Exécuter les données de salutation tooload une commande T-SQL en parallèle dans une nouvelle table de base de données.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-172">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<span data-ttu-id="9ffc4-173">Pour obtenir un didacticiel, consultez [charger des données à partir de tooSQL de stockage d’objets blob Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-173">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="9ffc4-174">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9ffc4-174">Recommendations</span></span>
<span data-ttu-id="9ffc4-175">La plupart de nos partenaires proposent des solutions de chargement.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="9ffc4-176">toofind plus d’informations, consultez une liste de nos [les partenaires de solutions][solution partners].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-176">toofind out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="9ffc4-177">Si vos données provenant d’une source non relationnelle et que vous souhaitez tooload dans des données SQL de l’entrepôt vous devez tootransform dans les lignes et les colonnes avant de les charger.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-177">If your data is coming from a non-relational source and you want tooload it into SQL Data Warehouse you will need tootransform it into rows and columns before you load it.</span></span> <span data-ttu-id="9ffc4-178">les données de salutation transformée n’a pas besoin toobe stockée dans une base de données, il peut être stocké dans des fichiers texte.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-178">hello transformed data doesn't need toobe stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="9ffc4-179">Créer des statistiques sur des données nouvellement chargées.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="9ffc4-180">Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="9ffc4-181">Dans l’ordre tooget hello optimiser les performances de vos requêtes, il est important toocreate des statistiques sur toutes les colonnes de toutes les tables après hello d’abord chargement ou de toutes les modifications importantes se produisent dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="9ffc4-181">In order tooget hello best performance from your queries, it's important toocreate statistics on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="9ffc4-182">Pour plus d’informations, consultez [Statistiques][Statistics].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ffc4-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ffc4-183">Next steps</span></span>
<span data-ttu-id="9ffc4-184">Pour plus de conseils de développement, consultez hello [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="9ffc4-184">For more development tips, see hello [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
