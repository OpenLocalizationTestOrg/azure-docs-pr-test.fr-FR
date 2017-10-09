---
title: "exemples de données aaaLoad dans SQL Data Warehouse | Documents Microsoft"
description: "Charger des exemples de données dans SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="7d6d0-103">Charger des exemples de données dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7d6d0-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="7d6d0-104">Suivez ces tooload des étapes simples et la base de données Adventure Works exemple de requête hello.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-104">Follow these simple steps tooload and query hello Adventure Works Sample database.</span></span> <span data-ttu-id="7d6d0-105">Ces scripts d’abord utilisent sqlcmd toorun SQL qui crée des tables et des vues.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-105">These scripts first use sqlcmd toorun SQL which will create tables and views.</span></span> <span data-ttu-id="7d6d0-106">Une fois que les tables ont été créées, les scripts hello utilise bcp tooload données.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-106">Once tables have been created, hello scripts will use bcp tooload data.</span></span>  <span data-ttu-id="7d6d0-107">Si vous n’avez pas encore sqlcmd et bcp installé, suivez ces liens trop[installer bcp] [ install bcp] et trop[installer sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="7d6d0-107">If you don't already have sqlcmd and bcp installed, follow these links too[install bcp][install bcp] and too[install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="7d6d0-108">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="7d6d0-108">Load sample data</span></span>
1. <span data-ttu-id="7d6d0-109">Télécharger hello [Adventure Works exemples de Scripts pour SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] fichier zip.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-109">Download hello [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="7d6d0-110">Extrayez les fichiers de hello du répertoire de tooa zip téléchargé sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-110">Extract hello files from downloaded zip tooa directory on your local machine.</span></span>
3. <span data-ttu-id="7d6d0-111">Modifiez les hello extrait fichier aw_create.bat et définissez les hello suivant des variables qui figurent en haut de hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-111">Edit hello extracted file aw_create.bat and set hello following variables found at hello top of hello file.</span></span>  <span data-ttu-id="7d6d0-112">N’être tooleave qu’aucun espace blanc entre = « hello » et le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-112">Be sure tooleave no whitespace between hello "=" and hello parameter.</span></span>  <span data-ttu-id="7d6d0-113">Vous trouverez ci-dessous des exemples de ce à quoi vos modifications peuvent ressembler.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="7d6d0-114">À partir d’une invite de commandes Windows, exécutez hello modifié aw_create.bat.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-114">From a Windows cmd prompt, run hello edited aw_create.bat.</span></span>  <span data-ttu-id="7d6d0-115">Veillez à ce que vous êtes dans le répertoire hello où vous avez enregistré votre version modifiée du aw_create.bat.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-115">Be sure you are in hello directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="7d6d0-116">Ce script va...</span><span class="sxs-lookup"><span data-stu-id="7d6d0-116">This script will...</span></span>
   
   * <span data-ttu-id="7d6d0-117">Supprimer les tables ou vues Adventure Works qui existent déjà dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="7d6d0-118">Créer des vues et tables de Adventure Works hello</span><span class="sxs-lookup"><span data-stu-id="7d6d0-118">Create hello Adventure Works tables and views</span></span>
   * <span data-ttu-id="7d6d0-119">Charger chaque table Adventure Works à l'aide de bcp.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="7d6d0-120">Valider le nombre de lignes hello pour chaque table Adventure Works</span><span class="sxs-lookup"><span data-stu-id="7d6d0-120">Validate hello row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="7d6d0-121">Collecter les statistiques sur chaque colonne pour chaque table Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="7d6d0-122">Interrogation des données de l'exemple</span><span class="sxs-lookup"><span data-stu-id="7d6d0-122">Query sample data</span></span>
<span data-ttu-id="7d6d0-123">Lorsque vous avez chargé des exemples de données dans SQL Data Warehouse, vous pouvez exécuter rapidement quelques requêtes.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="7d6d0-124">toorun une requête, connectez tooyour nouvellement créée de la base de données Adventure Works dans l’entrepôt de données SQL Azure à l’aide de Visual Studio et SSDT, comme décrit dans hello [requête avec Visual Studio] [ query with Visual Studio] document.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-124">toorun a query, connect tooyour newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in hello [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="7d6d0-125">Exemple de simple Sélectionnez instruction tooget toutes informations hello des employés de hello :</span><span class="sxs-lookup"><span data-stu-id="7d6d0-125">Example of simple select statement tooget all hello info of hello employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="7d6d0-126">Exemple d’une requête plus complexe à l’aide des constructions telles que GROUP BY toolook à la quantité totale de hello pour toutes les ventes chaque jour :</span><span class="sxs-lookup"><span data-stu-id="7d6d0-126">Example of a more complex query using constructs such as GROUP BY toolook at hello total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="7d6d0-127">Exemple d’une instruction SELECT avec une toofilter de clause WHERE ordres d’avant une date donnée :</span><span class="sxs-lookup"><span data-stu-id="7d6d0-127">Example of a SELECT with a WHERE clause toofilter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="7d6d0-128">SQL Data Warehouse prend en charge presque toutes les constructions T-SQL prises en charge par SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="7d6d0-129">Toutes les différences sont documentées dans notre documentation sur la [migration du code][migrate code].</span><span class="sxs-lookup"><span data-stu-id="7d6d0-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d6d0-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7d6d0-130">Next steps</span></span>
<span data-ttu-id="7d6d0-131">Maintenant que vous avez une chance tootry des requêtes avec des exemples de données, consultez Procédure trop[développer][develop], [charger][load], ou [ migrer] [ migrate] tooSQL l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="7d6d0-131">Now that you've had a chance tootry some queries with sample data, check out how too[develop][develop], [load][load], or [migrate][migrate] tooSQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
