---
title: "Utilisation de bcp pour charger des données dans SQL Data Warehouse | Microsoft Docs"
description: "Découvrez bcp et apprenez comment utiliser cette solution avec les scénarios d’entreposage de données."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 7596eac10fdf53380d85128265430ce07b551fe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="27eb5-103">Chargement des données avec BCP</span><span class="sxs-lookup"><span data-stu-id="27eb5-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27eb5-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="27eb5-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="27eb5-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="27eb5-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="27eb5-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="27eb5-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="27eb5-107">BCP</span><span class="sxs-lookup"><span data-stu-id="27eb5-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="27eb5-108">**[bcp][bcp]** est un utilitaire de ligne de commande de chargement par lots qui vous permet de charger des données entre SQL Server, des fichiers de données et SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27eb5-108">**[bcp][bcp]** is a command-line bulk load utility that allows you to copy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="27eb5-109">Utilisez bcp pour importer un nombre important de lignes dans les tables SQL Data Warehouse ou pour exporter des données des tables SQL Server dans les fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="27eb5-109">Use bcp to import large numbers of rows into SQL Data Warehouse tables or to export data from SQL Server tables into data files.</span></span> <span data-ttu-id="27eb5-110">L’utilitaire bcp, sauf lorsqu’il est utilisé avec l’option queryout, ne nécessite aucune connaissance de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="27eb5-110">Except when used with the queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="27eb5-111">bcp permet d’importer et d’exporter rapidement et simplement des ensembles de données plus petits de la base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27eb5-111">bcp is a quick and easy way to move smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="27eb5-112">La quantité exacte de données qu’il est recommandé de charger/extraire via bcp dépend de la connexion de votre réseau au centre de données Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="27eb5-112">The exact amount of data that is recommended to load/extract via bcp will depend on you network connection to the Azure data center.</span></span>  <span data-ttu-id="27eb5-113">En règle générale, les tables de dimension peuvent être chargées et extraites facilement avec bcp. Toutefois, bcp n’est pas recommandé pour le chargement ou l’extraction de volumes de données élevés.</span><span class="sxs-lookup"><span data-stu-id="27eb5-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="27eb5-114">Polybase est l’outil recommandé pour le chargement et l’extraction de volumes de données élevés, car il exploite plus efficacement l’architecture MPP (Massively Parallel Processing) de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27eb5-114">Polybase is the recommended tool for loading and extracting large volumes of data as it does a better job leveraging the massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="27eb5-115">Avec bcp, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="27eb5-115">With bcp you can:</span></span>

* <span data-ttu-id="27eb5-116">Utiliser un utilitaire en ligne de commande simple pour charger des données dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27eb5-116">Use a simple command-line utility to load data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="27eb5-117">Utiliser un utilitaire en ligne de commande simple pour extraire des données de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27eb5-117">Use a simple command-line utility to extract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="27eb5-118">Ce didacticiel vous explique comment :</span><span class="sxs-lookup"><span data-stu-id="27eb5-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="27eb5-119">Importer des données dans une table à l’aide de la commande bcp in</span><span class="sxs-lookup"><span data-stu-id="27eb5-119">Import data into a table using the bcp in command</span></span>
* <span data-ttu-id="27eb5-120">Exporter des données d’une table à l’aide de la commande bcp out</span><span class="sxs-lookup"><span data-stu-id="27eb5-120">Export data from a table uisng the bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="27eb5-121">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="27eb5-121">Prerequisites</span></span>
<span data-ttu-id="27eb5-122">Pour parcourir ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="27eb5-122">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="27eb5-123">Base de données SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="27eb5-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="27eb5-124">Utilitaire en ligne de commande bcp installé</span><span class="sxs-lookup"><span data-stu-id="27eb5-124">The bcp command line utility installed</span></span>
* <span data-ttu-id="27eb5-125">Utilitaire en ligne de commande SQLCMD installé</span><span class="sxs-lookup"><span data-stu-id="27eb5-125">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="27eb5-126">Pour télécharger les utilitaires bcp et sqlcmd, accédez au [Centre de téléchargement Microsoft][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="27eb5-126">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="27eb5-127">Importer des données dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="27eb5-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="27eb5-128">Dans ce didacticiel, vous allez créer une table dans Azure SQL Data Warehouse et importer des données dans la table.</span><span class="sxs-lookup"><span data-stu-id="27eb5-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="27eb5-129">Étape 1 : Créer une table dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="27eb5-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="27eb5-130">À partir d’une invite de commandes, utilisez sqlcmd pour exécuter la requête suivante, afin de créer une table sur votre instance :</span><span class="sxs-lookup"><span data-stu-id="27eb5-130">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```

> [!NOTE]
> <span data-ttu-id="27eb5-131">Consultez la page [Table Overview][Table Overview] (Vue d’ensemble des tables) ou la [syntaxe de CREATE TABLE][CREATE TABLE syntax] pour en savoir plus sur la création d’une table dans SQL Data Warehouse et les options disponibles dans la clause WITH.</span><span class="sxs-lookup"><span data-stu-id="27eb5-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="27eb5-132">Étape 2 : Créer un fichier de données source</span><span class="sxs-lookup"><span data-stu-id="27eb5-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="27eb5-133">Ouvrez le Bloc-notes, copiez les lignes de données suivantes dans un nouveau fichier texte, puis enregistrez ce fichier dans votre répertoire temporaire local C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="27eb5-133">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> <span data-ttu-id="27eb5-134">Il est important de se souvenir que bcp.exe ne prend pas en charge le codage de fichier UTF-8.</span><span class="sxs-lookup"><span data-stu-id="27eb5-134">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="27eb5-135">Utilisez des fichiers ASCII ou codés en UTF-16 lors de l’utilisation de bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="27eb5-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="27eb5-136">Étape 3 : Connecter et importer les données</span><span class="sxs-lookup"><span data-stu-id="27eb5-136">Step 3: Connect and import the data</span></span>
<span data-ttu-id="27eb5-137">Grâce à bcp, vous pouvez connecter et importer les données à l’aide de la commande suivante, qui remplace de manière appropriée les valeurs :</span><span class="sxs-lookup"><span data-stu-id="27eb5-137">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="27eb5-138">Vous pouvez vérifier que les données ont été chargées en exécutant la requête suivante à l’aide de sqlcmd :</span><span class="sxs-lookup"><span data-stu-id="27eb5-138">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="27eb5-139">Les résultats suivants doivent s’afficher :</span><span class="sxs-lookup"><span data-stu-id="27eb5-139">This should return the following results:</span></span>

| <span data-ttu-id="27eb5-140">DateId</span><span class="sxs-lookup"><span data-stu-id="27eb5-140">DateId</span></span> | <span data-ttu-id="27eb5-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="27eb5-141">CalendarQuarter</span></span> | <span data-ttu-id="27eb5-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="27eb5-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="27eb5-143">20150101</span><span class="sxs-lookup"><span data-stu-id="27eb5-143">20150101</span></span> |<span data-ttu-id="27eb5-144">1</span><span class="sxs-lookup"><span data-stu-id="27eb5-144">1</span></span> |<span data-ttu-id="27eb5-145">3</span><span class="sxs-lookup"><span data-stu-id="27eb5-145">3</span></span> |
| <span data-ttu-id="27eb5-146">20150201</span><span class="sxs-lookup"><span data-stu-id="27eb5-146">20150201</span></span> |<span data-ttu-id="27eb5-147">1</span><span class="sxs-lookup"><span data-stu-id="27eb5-147">1</span></span> |<span data-ttu-id="27eb5-148">3</span><span class="sxs-lookup"><span data-stu-id="27eb5-148">3</span></span> |
| <span data-ttu-id="27eb5-149">20150301</span><span class="sxs-lookup"><span data-stu-id="27eb5-149">20150301</span></span> |<span data-ttu-id="27eb5-150">1</span><span class="sxs-lookup"><span data-stu-id="27eb5-150">1</span></span> |<span data-ttu-id="27eb5-151">3</span><span class="sxs-lookup"><span data-stu-id="27eb5-151">3</span></span> |
| <span data-ttu-id="27eb5-152">20150401</span><span class="sxs-lookup"><span data-stu-id="27eb5-152">20150401</span></span> |<span data-ttu-id="27eb5-153">2</span><span class="sxs-lookup"><span data-stu-id="27eb5-153">2</span></span> |<span data-ttu-id="27eb5-154">4</span><span class="sxs-lookup"><span data-stu-id="27eb5-154">4</span></span> |
| <span data-ttu-id="27eb5-155">20150501</span><span class="sxs-lookup"><span data-stu-id="27eb5-155">20150501</span></span> |<span data-ttu-id="27eb5-156">2</span><span class="sxs-lookup"><span data-stu-id="27eb5-156">2</span></span> |<span data-ttu-id="27eb5-157">4</span><span class="sxs-lookup"><span data-stu-id="27eb5-157">4</span></span> |
| <span data-ttu-id="27eb5-158">20150601</span><span class="sxs-lookup"><span data-stu-id="27eb5-158">20150601</span></span> |<span data-ttu-id="27eb5-159">2</span><span class="sxs-lookup"><span data-stu-id="27eb5-159">2</span></span> |<span data-ttu-id="27eb5-160">4</span><span class="sxs-lookup"><span data-stu-id="27eb5-160">4</span></span> |
| <span data-ttu-id="27eb5-161">20150701</span><span class="sxs-lookup"><span data-stu-id="27eb5-161">20150701</span></span> |<span data-ttu-id="27eb5-162">3</span><span class="sxs-lookup"><span data-stu-id="27eb5-162">3</span></span> |<span data-ttu-id="27eb5-163">1</span><span class="sxs-lookup"><span data-stu-id="27eb5-163">1</span></span> |
| <span data-ttu-id="27eb5-164">20150801</span><span class="sxs-lookup"><span data-stu-id="27eb5-164">20150801</span></span> |<span data-ttu-id="27eb5-165">3</span><span class="sxs-lookup"><span data-stu-id="27eb5-165">3</span></span> |<span data-ttu-id="27eb5-166">1</span><span class="sxs-lookup"><span data-stu-id="27eb5-166">1</span></span> |
| <span data-ttu-id="27eb5-167">20150801</span><span class="sxs-lookup"><span data-stu-id="27eb5-167">20150801</span></span> |<span data-ttu-id="27eb5-168">3</span><span class="sxs-lookup"><span data-stu-id="27eb5-168">3</span></span> |<span data-ttu-id="27eb5-169">1</span><span class="sxs-lookup"><span data-stu-id="27eb5-169">1</span></span> |
| <span data-ttu-id="27eb5-170">20151001</span><span class="sxs-lookup"><span data-stu-id="27eb5-170">20151001</span></span> |<span data-ttu-id="27eb5-171">4</span><span class="sxs-lookup"><span data-stu-id="27eb5-171">4</span></span> |<span data-ttu-id="27eb5-172">2</span><span class="sxs-lookup"><span data-stu-id="27eb5-172">2</span></span> |
| <span data-ttu-id="27eb5-173">20151101</span><span class="sxs-lookup"><span data-stu-id="27eb5-173">20151101</span></span> |<span data-ttu-id="27eb5-174">4</span><span class="sxs-lookup"><span data-stu-id="27eb5-174">4</span></span> |<span data-ttu-id="27eb5-175">2</span><span class="sxs-lookup"><span data-stu-id="27eb5-175">2</span></span> |
| <span data-ttu-id="27eb5-176">20151201</span><span class="sxs-lookup"><span data-stu-id="27eb5-176">20151201</span></span> |<span data-ttu-id="27eb5-177">4</span><span class="sxs-lookup"><span data-stu-id="27eb5-177">4</span></span> |<span data-ttu-id="27eb5-178">2</span><span class="sxs-lookup"><span data-stu-id="27eb5-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="27eb5-179">Étape 4 : Créer des statistiques sur vos données nouvellement chargées</span><span class="sxs-lookup"><span data-stu-id="27eb5-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="27eb5-180">Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="27eb5-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="27eb5-181">Pour optimiser les performances de vos requêtes, il est important de créer les statistiques sur toutes les colonnes de toutes les tables après le premier chargement ou après toute modification substantielle dans les données.</span><span class="sxs-lookup"><span data-stu-id="27eb5-181">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="27eb5-182">Pour une explication détaillée des statistiques, consultez la rubrique [Statistiques][Statistics] dans le groupe de rubriques sur le développement.</span><span class="sxs-lookup"><span data-stu-id="27eb5-182">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="27eb5-183">Voici un exemple rapide de la création de statistiques sur le tableau chargé dans cet exemple</span><span class="sxs-lookup"><span data-stu-id="27eb5-183">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="27eb5-184">À partir d’une invite sqlcmd, exécutez les instructions CREATE STATISTICS suivantes :</span><span class="sxs-lookup"><span data-stu-id="27eb5-184">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="27eb5-185">Exporter des données de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="27eb5-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="27eb5-186">Dans ce didacticiel, vous allez créer un fichier de données à partir d’une table de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27eb5-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="27eb5-187">Nous allons exporter les données créées plus haut vers un nouveau fichier de données, DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="27eb5-187">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="27eb5-188">Étape 1 : Exporter les données</span><span class="sxs-lookup"><span data-stu-id="27eb5-188">Step 1: Export the data</span></span>
<span data-ttu-id="27eb5-189">L’utilitaire bcp vous permet de connecter et d’exporter les données à l’aide de la commande suivante, qui remplace de manière appropriée les valeurs :</span><span class="sxs-lookup"><span data-stu-id="27eb5-189">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="27eb5-190">Pour vérifier que les données ont été exportées, ouvrez le nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="27eb5-190">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="27eb5-191">Les données du fichier doivent correspondre au texte ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="27eb5-191">The data in the file should match the text below:</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> <span data-ttu-id="27eb5-192">En raison de la nature des systèmes distribués, l’ordre des données peut ne pas être identique entre les différentes bases de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27eb5-192">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="27eb5-193">Une autre option consiste à utiliser la fonction **queryout** de l’utilitaire bcp pour écrire un extrait de requête au lieu d’exporter la totalité de la table.</span><span class="sxs-lookup"><span data-stu-id="27eb5-193">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="27eb5-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="27eb5-194">Next steps</span></span>
<span data-ttu-id="27eb5-195">Pour accéder à une vue d’ensemble du chargement, consultez [Charger des données dans SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="27eb5-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="27eb5-196">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="27eb5-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
