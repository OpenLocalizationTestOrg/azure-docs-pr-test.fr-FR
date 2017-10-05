---
title: "Charger des exemples de données dans SQL Data Warehouse | Documents Microsoft"
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
ms.openlocfilehash: 1e0df958a2f18fe1e988168918e5cfd293f84e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="ce969-103">Charger des exemples de données dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ce969-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="ce969-104">Suivez ces étapes simples pour charger et interroger l’exemple de base de données Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="ce969-104">Follow these simple steps to load and query the Adventure Works Sample database.</span></span> <span data-ttu-id="ce969-105">Ces scripts utilisent d’abord sqlcmd pour exécuter SQL qui crée des tables et des vues.</span><span class="sxs-lookup"><span data-stu-id="ce969-105">These scripts first use sqlcmd to run SQL which will create tables and views.</span></span> <span data-ttu-id="ce969-106">Une fois que les tables ont été créées, les scripts utilisent bcp pour charger les données.</span><span class="sxs-lookup"><span data-stu-id="ce969-106">Once tables have been created, the scripts will use bcp to load data.</span></span>  <span data-ttu-id="ce969-107">Si sqlcmd et bcp ne sont pas encore installés, suivez ces liens pour [installer bcp][install bcp] et [installer sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="ce969-107">If you don't already have sqlcmd and bcp installed, follow these links to [install bcp][install bcp] and to [install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="ce969-108">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="ce969-108">Load sample data</span></span>
1. <span data-ttu-id="ce969-109">Téléchargez le fichier zip [Exemples de scripts Adventure Works pour SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="ce969-109">Download the [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="ce969-110">Extrayez les fichiers du fichier zip téléchargé dans un répertoire sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ce969-110">Extract the files from downloaded zip to a directory on your local machine.</span></span>
3. <span data-ttu-id="ce969-111">Modifiez le fichier extrait aw_create.bat et définissez les variables suivantes au début du fichier.</span><span class="sxs-lookup"><span data-stu-id="ce969-111">Edit the extracted file aw_create.bat and set the following variables found at the top of the file.</span></span>  <span data-ttu-id="ce969-112">Veillez à ne laisser aucun espace entre le « = » et le paramètre.</span><span class="sxs-lookup"><span data-stu-id="ce969-112">Be sure to leave no whitespace between the "=" and the parameter.</span></span>  <span data-ttu-id="ce969-113">Vous trouverez ci-dessous des exemples de ce à quoi vos modifications peuvent ressembler.</span><span class="sxs-lookup"><span data-stu-id="ce969-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="ce969-114">À partir d'une invite de commande Windows, exécutez le fichier aw_create.bat modifié.</span><span class="sxs-lookup"><span data-stu-id="ce969-114">From a Windows cmd prompt, run the edited aw_create.bat.</span></span>  <span data-ttu-id="ce969-115">Assurez-vous que vous êtes dans le répertoire où vous avez enregistré votre version modifiée du fichier aw_create.bat.</span><span class="sxs-lookup"><span data-stu-id="ce969-115">Be sure you are in the directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="ce969-116">Ce script va...</span><span class="sxs-lookup"><span data-stu-id="ce969-116">This script will...</span></span>
   
   * <span data-ttu-id="ce969-117">Supprimer les tables ou vues Adventure Works qui existent déjà dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="ce969-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="ce969-118">Créer les tables et les vues Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="ce969-118">Create the Adventure Works tables and views</span></span>
   * <span data-ttu-id="ce969-119">Charger chaque table Adventure Works à l'aide de bcp.</span><span class="sxs-lookup"><span data-stu-id="ce969-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="ce969-120">Valider le nombre de lignes pour chaque table Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="ce969-120">Validate the row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="ce969-121">Collecter les statistiques sur chaque colonne pour chaque table Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="ce969-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="ce969-122">Interrogation des données de l'exemple</span><span class="sxs-lookup"><span data-stu-id="ce969-122">Query sample data</span></span>
<span data-ttu-id="ce969-123">Lorsque vous avez chargé des exemples de données dans SQL Data Warehouse, vous pouvez exécuter rapidement quelques requêtes.</span><span class="sxs-lookup"><span data-stu-id="ce969-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="ce969-124">Pour exécuter une requête, connectez-vous à votre base de données Adventure Works nouvellement créée dans Azure SQL DW avec Visual Studio et SSDT, comme le décrit le document [Effectuer des requêtes avec Visual Studio][query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="ce969-124">To run a query, connect to your newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in the [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="ce969-125">Exemple d'instruction simple select pour obtenir toutes les informations des employés :</span><span class="sxs-lookup"><span data-stu-id="ce969-125">Example of simple select statement to get all the info of the employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="ce969-126">Exemple de requête plus complexe à l'aide de constructions telles que GROUP BY pour examiner le montant total de toutes les ventes chaque jour :</span><span class="sxs-lookup"><span data-stu-id="ce969-126">Example of a more complex query using constructs such as GROUP BY to look at the total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="ce969-127">Exemple d'instruction SELECT avec une clause WHERE pour filtrer les commandes antérieures à une date donnée :</span><span class="sxs-lookup"><span data-stu-id="ce969-127">Example of a SELECT with a WHERE clause to filter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="ce969-128">SQL Data Warehouse prend en charge presque toutes les constructions T-SQL prises en charge par SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ce969-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="ce969-129">Toutes les différences sont documentées dans notre documentation sur la [migration du code][migrate code].</span><span class="sxs-lookup"><span data-stu-id="ce969-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce969-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ce969-130">Next steps</span></span>
<span data-ttu-id="ce969-131">Maintenant que vous avez eu l’occasion d’essayer certaines requêtes avec des exemples de données, découvrez comment [développer][develop], [charger][load] ou [migrer][migrate] vers SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ce969-131">Now that you've had a chance to try some queries with sample data, check out how to [develop][develop], [load][load], or [migrate][migrate] to SQL Data Warehouse.</span></span>

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
