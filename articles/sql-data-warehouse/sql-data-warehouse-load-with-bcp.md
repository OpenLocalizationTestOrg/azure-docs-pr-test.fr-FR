---
title: "données de tooload aaaUse bcp dans SQL Data Warehouse | Documents Microsoft"
description: "Découvrez quels bcp est et comment toouse pour les scénarios d’entreposage de données."
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
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="49cc5-103">Chargement des données avec BCP</span><span class="sxs-lookup"><span data-stu-id="49cc5-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49cc5-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="49cc5-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="49cc5-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="49cc5-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="49cc5-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="49cc5-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="49cc5-107">BCP</span><span class="sxs-lookup"><span data-stu-id="49cc5-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="49cc5-108">**[bcp] [ bcp]**  est un utilitaire de chargement en masse de ligne de commande qui vous permet de toocopy des données entre SQL Server, les fichiers de données et SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49cc5-108">**[bcp][bcp]** is a command-line bulk load utility that allows you toocopy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="49cc5-109">Utilisez bcp tooimport grand nombre de lignes dans des tables de l’entrepôt de données SQL ou de tooexport des données à partir des tables SQL Server dans les fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="49cc5-109">Use bcp tooimport large numbers of rows into SQL Data Warehouse tables or tooexport data from SQL Server tables into data files.</span></span> <span data-ttu-id="49cc5-110">Sauf lorsque utilisé avec l’option queryout hello, bcp ne nécessite aucune connaissance de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="49cc5-110">Except when used with hello queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="49cc5-111">bcp est un moyen simple et rapide toomove petits jeux de données dans et hors d’une base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49cc5-111">bcp is a quick and easy way toomove smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="49cc5-112">varie en quantité exacte de Hello de données qu’il sont recommandées de tooload/extraction via bcp sur de réseau de centre de données Azure toohello de connexion.</span><span class="sxs-lookup"><span data-stu-id="49cc5-112">hello exact amount of data that is recommended tooload/extract via bcp will depend on you network connection toohello Azure data center.</span></span>  <span data-ttu-id="49cc5-113">En règle générale, les tables de dimension peuvent être chargées et extraites facilement avec bcp. Toutefois, bcp n’est pas recommandé pour le chargement ou l’extraction de volumes de données élevés.</span><span class="sxs-lookup"><span data-stu-id="49cc5-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="49cc5-114">Polybase est hello recommandé outil pour le chargement et l’extraction des volumes importants de données comme il le fait mieux tirer parti d’architecture de traitement parallèle massif hello d’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="49cc5-114">Polybase is hello recommended tool for loading and extracting large volumes of data as it does a better job leveraging hello massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="49cc5-115">Avec bcp, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="49cc5-115">With bcp you can:</span></span>

* <span data-ttu-id="49cc5-116">Utilisez un utilitaire de ligne de commande simple tooload de données dans l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="49cc5-116">Use a simple command-line utility tooload data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="49cc5-117">Utiliser un utilitaire de ligne de commande simple de données de tooextract à partir de l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="49cc5-117">Use a simple command-line utility tooextract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="49cc5-118">Ce didacticiel vous explique comment :</span><span class="sxs-lookup"><span data-stu-id="49cc5-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="49cc5-119">Importer des données dans une table à l’aide de bcp de hello dans la commande</span><span class="sxs-lookup"><span data-stu-id="49cc5-119">Import data into a table using hello bcp in command</span></span>
* <span data-ttu-id="49cc5-120">Exporter des données à partir d’un bcp de hello table en utilisant des commandes</span><span class="sxs-lookup"><span data-stu-id="49cc5-120">Export data from a table uisng hello bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="49cc5-121">Composants requis</span><span class="sxs-lookup"><span data-stu-id="49cc5-121">Prerequisites</span></span>
<span data-ttu-id="49cc5-122">toostep dans ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="49cc5-122">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="49cc5-123">Base de données SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="49cc5-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="49cc5-124">utilitaire de ligne de commande bcp Hello installé</span><span class="sxs-lookup"><span data-stu-id="49cc5-124">hello bcp command line utility installed</span></span>
* <span data-ttu-id="49cc5-125">Hello utilitaire de ligne de commande SQLCMD installé</span><span class="sxs-lookup"><span data-stu-id="49cc5-125">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="49cc5-126">Vous pouvez télécharger les utilitaires bcp et sqlcmd hello hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="49cc5-126">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="49cc5-127">Importer des données dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="49cc5-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="49cc5-128">Dans ce didacticiel, vous créez une table dans Azure SQL Data Warehouse et importer des données dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="49cc5-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="49cc5-129">Étape 1 : Créer une table dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="49cc5-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="49cc5-130">À partir d’une invite de commandes, utilisez sqlcmd toorun hello est suivant de requête toocreate une table de votre instance de :</span><span class="sxs-lookup"><span data-stu-id="49cc5-130">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="49cc5-131">Consultez [vue d’ensemble de la Table] [ Table Overview] ou [syntaxe CREATE TABLE] [ CREATE TABLE syntax] pour plus d’informations sur la création d’une table sur SQL Data Warehouse et hello  options disponibles dans la clause WITH de hello.</span><span class="sxs-lookup"><span data-stu-id="49cc5-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="49cc5-132">Étape 2 : Créer un fichier de données source</span><span class="sxs-lookup"><span data-stu-id="49cc5-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="49cc5-133">Ouvrez le bloc-notes, puis copiez hello après des lignes de données dans un nouveau fichier texte, puis enregistrez ce fichier tooyour répertoire temp local, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="49cc5-133">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="49cc5-134">Il est important tooremember que bcp.exe ne prend pas en charge l’encodage du fichier hello UTF-8.</span><span class="sxs-lookup"><span data-stu-id="49cc5-134">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="49cc5-135">Utilisez des fichiers ASCII ou codés en UTF-16 lors de l’utilisation de bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="49cc5-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="49cc5-136">Étape 3 : Se connecter et importer des données de hello</span><span class="sxs-lookup"><span data-stu-id="49cc5-136">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="49cc5-137">À l’aide de bcp, vous pouvez connecter et importer des données hello à l’aide de hello commande en remplaçant des valeurs hello comme appropriées suivantes :</span><span class="sxs-lookup"><span data-stu-id="49cc5-137">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="49cc5-138">Vous pouvez vérifier les données ont été chargées en exécutant hello suivant la requête à l’aide de sqlcmd de hello :</span><span class="sxs-lookup"><span data-stu-id="49cc5-138">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="49cc5-139">Cela doit retourner hello suivant des résultats :</span><span class="sxs-lookup"><span data-stu-id="49cc5-139">This should return hello following results:</span></span>

| <span data-ttu-id="49cc5-140">DateId</span><span class="sxs-lookup"><span data-stu-id="49cc5-140">DateId</span></span> | <span data-ttu-id="49cc5-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="49cc5-141">CalendarQuarter</span></span> | <span data-ttu-id="49cc5-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="49cc5-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49cc5-143">20150101</span><span class="sxs-lookup"><span data-stu-id="49cc5-143">20150101</span></span> |<span data-ttu-id="49cc5-144">1</span><span class="sxs-lookup"><span data-stu-id="49cc5-144">1</span></span> |<span data-ttu-id="49cc5-145">3</span><span class="sxs-lookup"><span data-stu-id="49cc5-145">3</span></span> |
| <span data-ttu-id="49cc5-146">20150201</span><span class="sxs-lookup"><span data-stu-id="49cc5-146">20150201</span></span> |<span data-ttu-id="49cc5-147">1</span><span class="sxs-lookup"><span data-stu-id="49cc5-147">1</span></span> |<span data-ttu-id="49cc5-148">3</span><span class="sxs-lookup"><span data-stu-id="49cc5-148">3</span></span> |
| <span data-ttu-id="49cc5-149">20150301</span><span class="sxs-lookup"><span data-stu-id="49cc5-149">20150301</span></span> |<span data-ttu-id="49cc5-150">1</span><span class="sxs-lookup"><span data-stu-id="49cc5-150">1</span></span> |<span data-ttu-id="49cc5-151">3</span><span class="sxs-lookup"><span data-stu-id="49cc5-151">3</span></span> |
| <span data-ttu-id="49cc5-152">20150401</span><span class="sxs-lookup"><span data-stu-id="49cc5-152">20150401</span></span> |<span data-ttu-id="49cc5-153">2</span><span class="sxs-lookup"><span data-stu-id="49cc5-153">2</span></span> |<span data-ttu-id="49cc5-154">4</span><span class="sxs-lookup"><span data-stu-id="49cc5-154">4</span></span> |
| <span data-ttu-id="49cc5-155">20150501</span><span class="sxs-lookup"><span data-stu-id="49cc5-155">20150501</span></span> |<span data-ttu-id="49cc5-156">2</span><span class="sxs-lookup"><span data-stu-id="49cc5-156">2</span></span> |<span data-ttu-id="49cc5-157">4</span><span class="sxs-lookup"><span data-stu-id="49cc5-157">4</span></span> |
| <span data-ttu-id="49cc5-158">20150601</span><span class="sxs-lookup"><span data-stu-id="49cc5-158">20150601</span></span> |<span data-ttu-id="49cc5-159">2</span><span class="sxs-lookup"><span data-stu-id="49cc5-159">2</span></span> |<span data-ttu-id="49cc5-160">4</span><span class="sxs-lookup"><span data-stu-id="49cc5-160">4</span></span> |
| <span data-ttu-id="49cc5-161">20150701</span><span class="sxs-lookup"><span data-stu-id="49cc5-161">20150701</span></span> |<span data-ttu-id="49cc5-162">3</span><span class="sxs-lookup"><span data-stu-id="49cc5-162">3</span></span> |<span data-ttu-id="49cc5-163">1</span><span class="sxs-lookup"><span data-stu-id="49cc5-163">1</span></span> |
| <span data-ttu-id="49cc5-164">20150801</span><span class="sxs-lookup"><span data-stu-id="49cc5-164">20150801</span></span> |<span data-ttu-id="49cc5-165">3</span><span class="sxs-lookup"><span data-stu-id="49cc5-165">3</span></span> |<span data-ttu-id="49cc5-166">1</span><span class="sxs-lookup"><span data-stu-id="49cc5-166">1</span></span> |
| <span data-ttu-id="49cc5-167">20150801</span><span class="sxs-lookup"><span data-stu-id="49cc5-167">20150801</span></span> |<span data-ttu-id="49cc5-168">3</span><span class="sxs-lookup"><span data-stu-id="49cc5-168">3</span></span> |<span data-ttu-id="49cc5-169">1</span><span class="sxs-lookup"><span data-stu-id="49cc5-169">1</span></span> |
| <span data-ttu-id="49cc5-170">20151001</span><span class="sxs-lookup"><span data-stu-id="49cc5-170">20151001</span></span> |<span data-ttu-id="49cc5-171">4</span><span class="sxs-lookup"><span data-stu-id="49cc5-171">4</span></span> |<span data-ttu-id="49cc5-172">2</span><span class="sxs-lookup"><span data-stu-id="49cc5-172">2</span></span> |
| <span data-ttu-id="49cc5-173">20151101</span><span class="sxs-lookup"><span data-stu-id="49cc5-173">20151101</span></span> |<span data-ttu-id="49cc5-174">4</span><span class="sxs-lookup"><span data-stu-id="49cc5-174">4</span></span> |<span data-ttu-id="49cc5-175">2</span><span class="sxs-lookup"><span data-stu-id="49cc5-175">2</span></span> |
| <span data-ttu-id="49cc5-176">20151201</span><span class="sxs-lookup"><span data-stu-id="49cc5-176">20151201</span></span> |<span data-ttu-id="49cc5-177">4</span><span class="sxs-lookup"><span data-stu-id="49cc5-177">4</span></span> |<span data-ttu-id="49cc5-178">2</span><span class="sxs-lookup"><span data-stu-id="49cc5-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="49cc5-179">Étape 4 : Créer des statistiques sur vos données nouvellement chargées</span><span class="sxs-lookup"><span data-stu-id="49cc5-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="49cc5-180">Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="49cc5-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="49cc5-181">Dans l’ordre tooget hello optimiser les performances de vos requêtes, il est important que créer des statistiques sur toutes les colonnes de toutes les tables après le premier chargement de hello ou toutes les modifications importantes se produisent dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="49cc5-181">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="49cc5-182">Pour obtenir une explication détaillée des statistiques, consultez hello [statistiques] [ Statistics] rubrique dans le groupe de développement hello de rubriques.</span><span class="sxs-lookup"><span data-stu-id="49cc5-182">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="49cc5-183">Voici un exemple rapide de la façon dont les statistiques toocreate sur hello déposée chargement dans cet exemple</span><span class="sxs-lookup"><span data-stu-id="49cc5-183">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="49cc5-184">Exécutez hello suivant les instructions CREATE STATISTICS à partir d’une invite de commandes sqlcmd :</span><span class="sxs-lookup"><span data-stu-id="49cc5-184">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="49cc5-185">Exporter des données de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="49cc5-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="49cc5-186">Dans ce didacticiel, vous allez créer un fichier de données à partir d’une table de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49cc5-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="49cc5-187">Vous exporterez les données hello créée précédemment tooa nouveau fichier de données appelé DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="49cc5-187">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="49cc5-188">Étape 1 : Exporter les données de salutation</span><span class="sxs-lookup"><span data-stu-id="49cc5-188">Step 1: Export hello data</span></span>
<span data-ttu-id="49cc5-189">L’utilitaire bcp de hello, vous pouvez connecter et exporter des données à l’aide de hello commande en remplaçant des valeurs hello comme appropriées suivantes :</span><span class="sxs-lookup"><span data-stu-id="49cc5-189">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="49cc5-190">Vous pouvez vérifier hello données a été correctement exportées en ouvrant le fichier hello.</span><span class="sxs-lookup"><span data-stu-id="49cc5-190">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="49cc5-191">les données de salutation dans le fichier de hello doivent correspondre au texte hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="49cc5-191">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="49cc5-192">En raison de la nature toohello des systèmes distribués, ordre des données hello peut-être pas hello même sur les bases de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49cc5-192">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="49cc5-193">Une autre option consiste à toouse hello **queryout** fonction de bcp toowrite une requête extrait au lieu d’exporter la totalité de la table hello.</span><span class="sxs-lookup"><span data-stu-id="49cc5-193">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="49cc5-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="49cc5-194">Next steps</span></span>
<span data-ttu-id="49cc5-195">Pour accéder à une vue d’ensemble du chargement, consultez [Charger des données dans SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="49cc5-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="49cc5-196">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="49cc5-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
