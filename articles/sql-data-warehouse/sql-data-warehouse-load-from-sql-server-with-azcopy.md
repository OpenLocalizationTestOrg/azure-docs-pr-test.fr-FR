---
title: "Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (PolyBase) | Microsoft Docs"
description: "Utilise BCP pour exporter des données à partir de SQL Server vers des fichiers plats, AZCopy pour importer des données dans le stockage d’objets blob Azure et PolyBase pour recevoir les données dans Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 08f94bc26d8b1e1f5a56dfccd41e394dbd721024
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="21a54-103">Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="21a54-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="21a54-104">Utilisez les utilitaires de ligne de commande BCP et AZCopy pour charger des données à partir de SQL Server dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="21a54-104">Use bcp and AZCopy command-line utilities to load data from SQL Server to Azure blob storage.</span></span> <span data-ttu-id="21a54-105">Utilisez ensuite PolyBase ou Azure Data Factory pour charger les données dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="21a54-105">Then use PolyBase or Azure Data Factory to load the data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="21a54-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="21a54-106">Prerequisites</span></span>
<span data-ttu-id="21a54-107">Pour parcourir ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="21a54-107">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="21a54-108">Base de données SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="21a54-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="21a54-109">Utilitaire en ligne de commande bcp installé</span><span class="sxs-lookup"><span data-stu-id="21a54-109">The bcp command line utility installed</span></span>
* <span data-ttu-id="21a54-110">Utilitaire en ligne de commande SQLCMD installé</span><span class="sxs-lookup"><span data-stu-id="21a54-110">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="21a54-111">Pour télécharger les utilitaires bcp et sqlcmd, accédez au [Centre de téléchargement Microsoft][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="21a54-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="21a54-112">Importer des données dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="21a54-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="21a54-113">Dans ce didacticiel, vous allez créer une table dans Azure SQL Data Warehouse et importer des données dans la table.</span><span class="sxs-lookup"><span data-stu-id="21a54-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="21a54-114">Étape 1 : Créer une table dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="21a54-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="21a54-115">À partir d’une invite de commandes, utilisez sqlcmd pour exécuter la requête suivante, afin de créer une table sur votre instance :</span><span class="sxs-lookup"><span data-stu-id="21a54-115">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

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
> <span data-ttu-id="21a54-116">Consultez la page [Table Overview][Table Overview] (Vue d’ensemble des tables) ou la [syntaxe de CREATE TABLE][CREATE TABLE syntax] pour en savoir plus sur la création d’une table dans SQL Data Warehouse et les options disponibles dans la clause WITH.</span><span class="sxs-lookup"><span data-stu-id="21a54-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="21a54-117">Étape 2 : Créer un fichier de données source</span><span class="sxs-lookup"><span data-stu-id="21a54-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="21a54-118">Ouvrez le Bloc-notes, copiez les lignes de données suivantes dans un nouveau fichier texte, puis enregistrez ce fichier dans votre répertoire temporaire local C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="21a54-118">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="21a54-119">Il est important de se souvenir que bcp.exe ne prend pas en charge le codage de fichier UTF-8.</span><span class="sxs-lookup"><span data-stu-id="21a54-119">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="21a54-120">Utilisez des fichiers ASCII ou codés en UTF-16 lors de l’utilisation de bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="21a54-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="21a54-121">Étape 3 : Connecter et importer les données</span><span class="sxs-lookup"><span data-stu-id="21a54-121">Step 3: Connect and import the data</span></span>
<span data-ttu-id="21a54-122">Grâce à bcp, vous pouvez connecter et importer les données à l’aide de la commande suivante, qui remplace de manière appropriée les valeurs :</span><span class="sxs-lookup"><span data-stu-id="21a54-122">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="21a54-123">Vous pouvez vérifier que les données ont été chargées en exécutant la requête suivante à l’aide de sqlcmd :</span><span class="sxs-lookup"><span data-stu-id="21a54-123">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="21a54-124">Les résultats suivants doivent s’afficher :</span><span class="sxs-lookup"><span data-stu-id="21a54-124">This should return the following results:</span></span>

| <span data-ttu-id="21a54-125">DateId</span><span class="sxs-lookup"><span data-stu-id="21a54-125">DateId</span></span> | <span data-ttu-id="21a54-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="21a54-126">CalendarQuarter</span></span> | <span data-ttu-id="21a54-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="21a54-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21a54-128">20150101</span><span class="sxs-lookup"><span data-stu-id="21a54-128">20150101</span></span> |<span data-ttu-id="21a54-129">1</span><span class="sxs-lookup"><span data-stu-id="21a54-129">1</span></span> |<span data-ttu-id="21a54-130">3</span><span class="sxs-lookup"><span data-stu-id="21a54-130">3</span></span> |
| <span data-ttu-id="21a54-131">20150201</span><span class="sxs-lookup"><span data-stu-id="21a54-131">20150201</span></span> |<span data-ttu-id="21a54-132">1</span><span class="sxs-lookup"><span data-stu-id="21a54-132">1</span></span> |<span data-ttu-id="21a54-133">3</span><span class="sxs-lookup"><span data-stu-id="21a54-133">3</span></span> |
| <span data-ttu-id="21a54-134">20150301</span><span class="sxs-lookup"><span data-stu-id="21a54-134">20150301</span></span> |<span data-ttu-id="21a54-135">1</span><span class="sxs-lookup"><span data-stu-id="21a54-135">1</span></span> |<span data-ttu-id="21a54-136">3</span><span class="sxs-lookup"><span data-stu-id="21a54-136">3</span></span> |
| <span data-ttu-id="21a54-137">20150401</span><span class="sxs-lookup"><span data-stu-id="21a54-137">20150401</span></span> |<span data-ttu-id="21a54-138">2</span><span class="sxs-lookup"><span data-stu-id="21a54-138">2</span></span> |<span data-ttu-id="21a54-139">4</span><span class="sxs-lookup"><span data-stu-id="21a54-139">4</span></span> |
| <span data-ttu-id="21a54-140">20150501</span><span class="sxs-lookup"><span data-stu-id="21a54-140">20150501</span></span> |<span data-ttu-id="21a54-141">2</span><span class="sxs-lookup"><span data-stu-id="21a54-141">2</span></span> |<span data-ttu-id="21a54-142">4</span><span class="sxs-lookup"><span data-stu-id="21a54-142">4</span></span> |
| <span data-ttu-id="21a54-143">20150601</span><span class="sxs-lookup"><span data-stu-id="21a54-143">20150601</span></span> |<span data-ttu-id="21a54-144">2</span><span class="sxs-lookup"><span data-stu-id="21a54-144">2</span></span> |<span data-ttu-id="21a54-145">4</span><span class="sxs-lookup"><span data-stu-id="21a54-145">4</span></span> |
| <span data-ttu-id="21a54-146">20150701</span><span class="sxs-lookup"><span data-stu-id="21a54-146">20150701</span></span> |<span data-ttu-id="21a54-147">3</span><span class="sxs-lookup"><span data-stu-id="21a54-147">3</span></span> |<span data-ttu-id="21a54-148">1</span><span class="sxs-lookup"><span data-stu-id="21a54-148">1</span></span> |
| <span data-ttu-id="21a54-149">20150801</span><span class="sxs-lookup"><span data-stu-id="21a54-149">20150801</span></span> |<span data-ttu-id="21a54-150">3</span><span class="sxs-lookup"><span data-stu-id="21a54-150">3</span></span> |<span data-ttu-id="21a54-151">1</span><span class="sxs-lookup"><span data-stu-id="21a54-151">1</span></span> |
| <span data-ttu-id="21a54-152">20150801</span><span class="sxs-lookup"><span data-stu-id="21a54-152">20150801</span></span> |<span data-ttu-id="21a54-153">3</span><span class="sxs-lookup"><span data-stu-id="21a54-153">3</span></span> |<span data-ttu-id="21a54-154">1</span><span class="sxs-lookup"><span data-stu-id="21a54-154">1</span></span> |
| <span data-ttu-id="21a54-155">20151001</span><span class="sxs-lookup"><span data-stu-id="21a54-155">20151001</span></span> |<span data-ttu-id="21a54-156">4</span><span class="sxs-lookup"><span data-stu-id="21a54-156">4</span></span> |<span data-ttu-id="21a54-157">2</span><span class="sxs-lookup"><span data-stu-id="21a54-157">2</span></span> |
| <span data-ttu-id="21a54-158">20151101</span><span class="sxs-lookup"><span data-stu-id="21a54-158">20151101</span></span> |<span data-ttu-id="21a54-159">4</span><span class="sxs-lookup"><span data-stu-id="21a54-159">4</span></span> |<span data-ttu-id="21a54-160">2</span><span class="sxs-lookup"><span data-stu-id="21a54-160">2</span></span> |
| <span data-ttu-id="21a54-161">20151201</span><span class="sxs-lookup"><span data-stu-id="21a54-161">20151201</span></span> |<span data-ttu-id="21a54-162">4</span><span class="sxs-lookup"><span data-stu-id="21a54-162">4</span></span> |<span data-ttu-id="21a54-163">2</span><span class="sxs-lookup"><span data-stu-id="21a54-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="21a54-164">Étape 4 : Créer des statistiques sur vos données nouvellement chargées</span><span class="sxs-lookup"><span data-stu-id="21a54-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="21a54-165">Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="21a54-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="21a54-166">Pour optimiser les performances de vos requêtes, il est important de créer les statistiques sur toutes les colonnes de toutes les tables après le premier chargement ou après toute modification substantielle dans les données.</span><span class="sxs-lookup"><span data-stu-id="21a54-166">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="21a54-167">Pour une explication détaillée des statistiques, consultez la rubrique [Statistiques][Statistics] dans le groupe de rubriques sur le développement.</span><span class="sxs-lookup"><span data-stu-id="21a54-167">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="21a54-168">Voici un exemple rapide de la création de statistiques sur le tableau chargé dans cet exemple</span><span class="sxs-lookup"><span data-stu-id="21a54-168">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="21a54-169">À partir d’une invite sqlcmd, exécutez les instructions CREATE STATISTICS suivantes :</span><span class="sxs-lookup"><span data-stu-id="21a54-169">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="21a54-170">Exporter des données de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="21a54-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="21a54-171">Dans ce didacticiel, vous allez créer un fichier de données à partir d’une table de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="21a54-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="21a54-172">Nous allons exporter les données créées plus haut vers un nouveau fichier de données, DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="21a54-172">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="21a54-173">Étape 1 : Exporter les données</span><span class="sxs-lookup"><span data-stu-id="21a54-173">Step 1: Export the data</span></span>
<span data-ttu-id="21a54-174">L’utilitaire bcp vous permet de connecter et d’exporter les données à l’aide de la commande suivante, qui remplace de manière appropriée les valeurs :</span><span class="sxs-lookup"><span data-stu-id="21a54-174">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="21a54-175">Pour vérifier que les données ont été exportées, ouvrez le nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="21a54-175">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="21a54-176">Les données du fichier doivent correspondre au texte ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="21a54-176">The data in the file should match the text below:</span></span>

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
> <span data-ttu-id="21a54-177">En raison de la nature des systèmes distribués, l’ordre des données peut ne pas être identique entre les différentes bases de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="21a54-177">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="21a54-178">Une autre option consiste à utiliser la fonction **queryout** de l’utilitaire bcp pour écrire un extrait de requête au lieu d’exporter la totalité de la table.</span><span class="sxs-lookup"><span data-stu-id="21a54-178">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="21a54-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="21a54-179">Next steps</span></span>
<span data-ttu-id="21a54-180">Pour accéder à une vue d’ensemble du chargement, consultez [Charger des données dans SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="21a54-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="21a54-181">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="21a54-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
