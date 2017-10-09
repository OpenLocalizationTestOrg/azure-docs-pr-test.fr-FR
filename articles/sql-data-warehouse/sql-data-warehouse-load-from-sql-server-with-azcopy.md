---
title: "données aaaLoad à partir de SQL Server dans Azure SQL Data Warehouse (PolyBase) | Documents Microsoft"
description: "Utilise les données de tooexport bcp à partir de fichiers tooflat de SQL Server, le stockage blob tooAzure AZCopy tooimport données et les données de salutation tooingest PolyBase dans Azure SQL Data Warehouse."
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
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="f4046-103">Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="f4046-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="f4046-104">Utilisez bcp et des données de tooload d’utilitaires de ligne de commande AZCopy à partir du stockage d’objets blob tooAzure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f4046-104">Use bcp and AZCopy command-line utilities tooload data from SQL Server tooAzure blob storage.</span></span> <span data-ttu-id="f4046-105">Puis utilisez les données de salutation tooload PolyBase ou Azure Data Factory dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f4046-105">Then use PolyBase or Azure Data Factory tooload hello data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f4046-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f4046-106">Prerequisites</span></span>
<span data-ttu-id="f4046-107">toostep dans ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="f4046-107">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="f4046-108">Base de données SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f4046-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="f4046-109">utilitaire de ligne de commande bcp Hello installé</span><span class="sxs-lookup"><span data-stu-id="f4046-109">hello bcp command line utility installed</span></span>
* <span data-ttu-id="f4046-110">Hello utilitaire de ligne de commande SQLCMD installé</span><span class="sxs-lookup"><span data-stu-id="f4046-110">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="f4046-111">Vous pouvez télécharger les utilitaires bcp et sqlcmd hello hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="f4046-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="f4046-112">Importer des données dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f4046-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="f4046-113">Dans ce didacticiel, vous créez une table dans Azure SQL Data Warehouse et importer des données dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="f4046-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="f4046-114">Étape 1 : Créer une table dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f4046-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f4046-115">À partir d’une invite de commandes, utilisez sqlcmd toorun hello est suivant de requête toocreate une table de votre instance de :</span><span class="sxs-lookup"><span data-stu-id="f4046-115">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="f4046-116">Consultez [vue d’ensemble de la Table] [ Table Overview] ou [syntaxe CREATE TABLE] [ CREATE TABLE syntax] pour plus d’informations sur la création d’une table sur SQL Data Warehouse et hello  options disponibles dans la clause WITH de hello.</span><span class="sxs-lookup"><span data-stu-id="f4046-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="f4046-117">Étape 2 : Créer un fichier de données source</span><span class="sxs-lookup"><span data-stu-id="f4046-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="f4046-118">Ouvrez le bloc-notes, puis copiez hello après des lignes de données dans un nouveau fichier texte, puis enregistrez ce fichier tooyour répertoire temp local, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="f4046-118">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="f4046-119">Il est important tooremember que bcp.exe ne prend pas en charge l’encodage du fichier hello UTF-8.</span><span class="sxs-lookup"><span data-stu-id="f4046-119">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="f4046-120">Utilisez des fichiers ASCII ou codés en UTF-16 lors de l’utilisation de bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="f4046-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="f4046-121">Étape 3 : Se connecter et importer des données de hello</span><span class="sxs-lookup"><span data-stu-id="f4046-121">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="f4046-122">À l’aide de bcp, vous pouvez connecter et importer des données hello à l’aide de hello commande en remplaçant des valeurs hello comme appropriées suivantes :</span><span class="sxs-lookup"><span data-stu-id="f4046-122">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="f4046-123">Vous pouvez vérifier les données ont été chargées en exécutant hello suivant la requête à l’aide de sqlcmd de hello :</span><span class="sxs-lookup"><span data-stu-id="f4046-123">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="f4046-124">Cela doit retourner hello suivant des résultats :</span><span class="sxs-lookup"><span data-stu-id="f4046-124">This should return hello following results:</span></span>

| <span data-ttu-id="f4046-125">DateId</span><span class="sxs-lookup"><span data-stu-id="f4046-125">DateId</span></span> | <span data-ttu-id="f4046-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="f4046-126">CalendarQuarter</span></span> | <span data-ttu-id="f4046-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="f4046-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4046-128">20150101</span><span class="sxs-lookup"><span data-stu-id="f4046-128">20150101</span></span> |<span data-ttu-id="f4046-129">1</span><span class="sxs-lookup"><span data-stu-id="f4046-129">1</span></span> |<span data-ttu-id="f4046-130">3</span><span class="sxs-lookup"><span data-stu-id="f4046-130">3</span></span> |
| <span data-ttu-id="f4046-131">20150201</span><span class="sxs-lookup"><span data-stu-id="f4046-131">20150201</span></span> |<span data-ttu-id="f4046-132">1</span><span class="sxs-lookup"><span data-stu-id="f4046-132">1</span></span> |<span data-ttu-id="f4046-133">3</span><span class="sxs-lookup"><span data-stu-id="f4046-133">3</span></span> |
| <span data-ttu-id="f4046-134">20150301</span><span class="sxs-lookup"><span data-stu-id="f4046-134">20150301</span></span> |<span data-ttu-id="f4046-135">1</span><span class="sxs-lookup"><span data-stu-id="f4046-135">1</span></span> |<span data-ttu-id="f4046-136">3</span><span class="sxs-lookup"><span data-stu-id="f4046-136">3</span></span> |
| <span data-ttu-id="f4046-137">20150401</span><span class="sxs-lookup"><span data-stu-id="f4046-137">20150401</span></span> |<span data-ttu-id="f4046-138">2</span><span class="sxs-lookup"><span data-stu-id="f4046-138">2</span></span> |<span data-ttu-id="f4046-139">4</span><span class="sxs-lookup"><span data-stu-id="f4046-139">4</span></span> |
| <span data-ttu-id="f4046-140">20150501</span><span class="sxs-lookup"><span data-stu-id="f4046-140">20150501</span></span> |<span data-ttu-id="f4046-141">2</span><span class="sxs-lookup"><span data-stu-id="f4046-141">2</span></span> |<span data-ttu-id="f4046-142">4</span><span class="sxs-lookup"><span data-stu-id="f4046-142">4</span></span> |
| <span data-ttu-id="f4046-143">20150601</span><span class="sxs-lookup"><span data-stu-id="f4046-143">20150601</span></span> |<span data-ttu-id="f4046-144">2</span><span class="sxs-lookup"><span data-stu-id="f4046-144">2</span></span> |<span data-ttu-id="f4046-145">4</span><span class="sxs-lookup"><span data-stu-id="f4046-145">4</span></span> |
| <span data-ttu-id="f4046-146">20150701</span><span class="sxs-lookup"><span data-stu-id="f4046-146">20150701</span></span> |<span data-ttu-id="f4046-147">3</span><span class="sxs-lookup"><span data-stu-id="f4046-147">3</span></span> |<span data-ttu-id="f4046-148">1</span><span class="sxs-lookup"><span data-stu-id="f4046-148">1</span></span> |
| <span data-ttu-id="f4046-149">20150801</span><span class="sxs-lookup"><span data-stu-id="f4046-149">20150801</span></span> |<span data-ttu-id="f4046-150">3</span><span class="sxs-lookup"><span data-stu-id="f4046-150">3</span></span> |<span data-ttu-id="f4046-151">1</span><span class="sxs-lookup"><span data-stu-id="f4046-151">1</span></span> |
| <span data-ttu-id="f4046-152">20150801</span><span class="sxs-lookup"><span data-stu-id="f4046-152">20150801</span></span> |<span data-ttu-id="f4046-153">3</span><span class="sxs-lookup"><span data-stu-id="f4046-153">3</span></span> |<span data-ttu-id="f4046-154">1</span><span class="sxs-lookup"><span data-stu-id="f4046-154">1</span></span> |
| <span data-ttu-id="f4046-155">20151001</span><span class="sxs-lookup"><span data-stu-id="f4046-155">20151001</span></span> |<span data-ttu-id="f4046-156">4</span><span class="sxs-lookup"><span data-stu-id="f4046-156">4</span></span> |<span data-ttu-id="f4046-157">2</span><span class="sxs-lookup"><span data-stu-id="f4046-157">2</span></span> |
| <span data-ttu-id="f4046-158">20151101</span><span class="sxs-lookup"><span data-stu-id="f4046-158">20151101</span></span> |<span data-ttu-id="f4046-159">4</span><span class="sxs-lookup"><span data-stu-id="f4046-159">4</span></span> |<span data-ttu-id="f4046-160">2</span><span class="sxs-lookup"><span data-stu-id="f4046-160">2</span></span> |
| <span data-ttu-id="f4046-161">20151201</span><span class="sxs-lookup"><span data-stu-id="f4046-161">20151201</span></span> |<span data-ttu-id="f4046-162">4</span><span class="sxs-lookup"><span data-stu-id="f4046-162">4</span></span> |<span data-ttu-id="f4046-163">2</span><span class="sxs-lookup"><span data-stu-id="f4046-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="f4046-164">Étape 4 : Créer des statistiques sur vos données nouvellement chargées</span><span class="sxs-lookup"><span data-stu-id="f4046-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="f4046-165">Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="f4046-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="f4046-166">Dans l’ordre tooget hello optimiser les performances de vos requêtes, il est important que créer des statistiques sur toutes les colonnes de toutes les tables après le premier chargement de hello ou toutes les modifications importantes se produisent dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="f4046-166">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="f4046-167">Pour obtenir une explication détaillée des statistiques, consultez hello [statistiques] [ Statistics] rubrique dans le groupe de développement hello de rubriques.</span><span class="sxs-lookup"><span data-stu-id="f4046-167">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="f4046-168">Voici un exemple rapide de la façon dont les statistiques toocreate sur hello déposée chargement dans cet exemple</span><span class="sxs-lookup"><span data-stu-id="f4046-168">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="f4046-169">Exécutez hello suivant les instructions CREATE STATISTICS à partir d’une invite de commandes sqlcmd :</span><span class="sxs-lookup"><span data-stu-id="f4046-169">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="f4046-170">Exporter des données de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f4046-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="f4046-171">Dans ce didacticiel, vous allez créer un fichier de données à partir d’une table de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f4046-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="f4046-172">Vous exporterez les données hello créée précédemment tooa nouveau fichier de données appelé DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="f4046-172">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="f4046-173">Étape 1 : Exporter les données de salutation</span><span class="sxs-lookup"><span data-stu-id="f4046-173">Step 1: Export hello data</span></span>
<span data-ttu-id="f4046-174">L’utilitaire bcp de hello, vous pouvez connecter et exporter des données à l’aide de hello commande en remplaçant des valeurs hello comme appropriées suivantes :</span><span class="sxs-lookup"><span data-stu-id="f4046-174">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="f4046-175">Vous pouvez vérifier hello données a été correctement exportées en ouvrant le fichier hello.</span><span class="sxs-lookup"><span data-stu-id="f4046-175">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="f4046-176">les données de salutation dans le fichier de hello doivent correspondre au texte hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f4046-176">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="f4046-177">En raison de la nature toohello des systèmes distribués, ordre des données hello peut-être pas hello même sur les bases de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f4046-177">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="f4046-178">Une autre option consiste à toouse hello **queryout** fonction de bcp toowrite une requête extrait au lieu d’exporter la totalité de la table hello.</span><span class="sxs-lookup"><span data-stu-id="f4046-178">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f4046-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f4046-179">Next steps</span></span>
<span data-ttu-id="f4046-180">Pour accéder à une vue d’ensemble du chargement, consultez [Charger des données dans SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="f4046-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="f4046-181">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="f4046-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
