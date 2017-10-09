---
title: "fichier de données d’aaaLoad à partir de volumes partagés de cluster dans la base de données SQL Azure (bcp) | Documents Microsoft"
description: "Pour une taille de données de petite taille, utilise les données de tooimport bcp dans la base de données SQL Azure."
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="227f9-103">Charger des données à partir d’un fichier CSV une base de données SQL Azure (fichiers plats)</span><span class="sxs-lookup"><span data-stu-id="227f9-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="227f9-104">Vous pouvez utiliser les données de tooimport hello bcp utilitaire de ligne de commande à partir d’un fichier CSV dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="227f9-104">You can use hello bcp command-line utility tooimport data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="227f9-105">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="227f9-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="227f9-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="227f9-106">Prerequisites</span></span>
<span data-ttu-id="227f9-107">les étapes toocomplete hello dans cet article, vous devez :</span><span class="sxs-lookup"><span data-stu-id="227f9-107">toocomplete hello steps in this article, you need:</span></span>

* <span data-ttu-id="227f9-108">Serveur logique et base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="227f9-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="227f9-109">utilitaire de ligne de commande de Hello bcp installé</span><span class="sxs-lookup"><span data-stu-id="227f9-109">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="227f9-110">utilitaire de ligne de commande de Hello sqlcmd installé</span><span class="sxs-lookup"><span data-stu-id="227f9-110">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="227f9-111">Vous pouvez télécharger les utilitaires bcp et sqlcmd hello hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="227f9-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="227f9-112">Données au format ASCII ou UTF-16</span><span class="sxs-lookup"><span data-stu-id="227f9-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="227f9-113">Si vous essayez de ce didacticiel avec vos propres données, vos données doivent toouse hello ASCII ou UTF-16 encodage bcp ne prenant pas en charge UTF-8.</span><span class="sxs-lookup"><span data-stu-id="227f9-113">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="227f9-114">1. Créer une table de destination</span><span class="sxs-lookup"><span data-stu-id="227f9-114">1. Create a destination table</span></span>
<span data-ttu-id="227f9-115">Définir une table dans la base de données SQL en tant que table de destination hello.</span><span class="sxs-lookup"><span data-stu-id="227f9-115">Define a table in SQL Database as hello destination table.</span></span> <span data-ttu-id="227f9-116">les colonnes dans la table de hello Hello doivent correspondre toohello des données dans chaque ligne de votre fichier de données.</span><span class="sxs-lookup"><span data-stu-id="227f9-116">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="227f9-117">toocreate une table, ouvrez une invite de commandes et utilisez sqlcmd.exe hello de toorun commande suivante :</span><span class="sxs-lookup"><span data-stu-id="227f9-117">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="227f9-118">2. Créer un fichier de données source</span><span class="sxs-lookup"><span data-stu-id="227f9-118">2. Create a source data file</span></span>
<span data-ttu-id="227f9-119">Ouvrez le bloc-notes, puis copiez hello après des lignes de données dans un nouveau fichier texte, puis enregistrez ce fichier tooyour répertoire temp local, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="227f9-119">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="227f9-120">Ces données sont au format ASCII.</span><span class="sxs-lookup"><span data-stu-id="227f9-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="227f9-121">(Facultatif) tooexport vos propres données à partir d’une base de données SQL Server, ouvrez une invite de commandes et exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="227f9-121">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="227f9-122">Remplacez TableName, ServerName, DatabaseName, Username et Password par vos propres informations.</span><span class="sxs-lookup"><span data-stu-id="227f9-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a><span data-ttu-id="227f9-123">3. Charger des données hello</span><span class="sxs-lookup"><span data-stu-id="227f9-123">3. Load hello data</span></span>
<span data-ttu-id="227f9-124">les données de salutation tooload, ouvrez une invite de commandes et exécutez les hello commande suivante, en remplaçant les valeurs hello pour le nom du serveur, nom de base de données, nom d’utilisateur et mot de passe avec vos propres informations.</span><span class="sxs-lookup"><span data-stu-id="227f9-124">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="227f9-125">Utilisez cette commande hello tooverify données a été correctement chargées.</span><span class="sxs-lookup"><span data-stu-id="227f9-125">Use this command tooverify hello data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="227f9-126">résultats de Hello doivent ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="227f9-126">hello results should look like this:</span></span>

| <span data-ttu-id="227f9-127">DateId</span><span class="sxs-lookup"><span data-stu-id="227f9-127">DateId</span></span> | <span data-ttu-id="227f9-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="227f9-128">CalendarQuarter</span></span> | <span data-ttu-id="227f9-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="227f9-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="227f9-130">20150101</span><span class="sxs-lookup"><span data-stu-id="227f9-130">20150101</span></span> |<span data-ttu-id="227f9-131">1</span><span class="sxs-lookup"><span data-stu-id="227f9-131">1</span></span> |<span data-ttu-id="227f9-132">3</span><span class="sxs-lookup"><span data-stu-id="227f9-132">3</span></span> |
| <span data-ttu-id="227f9-133">20150201</span><span class="sxs-lookup"><span data-stu-id="227f9-133">20150201</span></span> |<span data-ttu-id="227f9-134">1</span><span class="sxs-lookup"><span data-stu-id="227f9-134">1</span></span> |<span data-ttu-id="227f9-135">3</span><span class="sxs-lookup"><span data-stu-id="227f9-135">3</span></span> |
| <span data-ttu-id="227f9-136">20150301</span><span class="sxs-lookup"><span data-stu-id="227f9-136">20150301</span></span> |<span data-ttu-id="227f9-137">1</span><span class="sxs-lookup"><span data-stu-id="227f9-137">1</span></span> |<span data-ttu-id="227f9-138">3</span><span class="sxs-lookup"><span data-stu-id="227f9-138">3</span></span> |
| <span data-ttu-id="227f9-139">20150401</span><span class="sxs-lookup"><span data-stu-id="227f9-139">20150401</span></span> |<span data-ttu-id="227f9-140">2</span><span class="sxs-lookup"><span data-stu-id="227f9-140">2</span></span> |<span data-ttu-id="227f9-141">4</span><span class="sxs-lookup"><span data-stu-id="227f9-141">4</span></span> |
| <span data-ttu-id="227f9-142">20150501</span><span class="sxs-lookup"><span data-stu-id="227f9-142">20150501</span></span> |<span data-ttu-id="227f9-143">2</span><span class="sxs-lookup"><span data-stu-id="227f9-143">2</span></span> |<span data-ttu-id="227f9-144">4</span><span class="sxs-lookup"><span data-stu-id="227f9-144">4</span></span> |
| <span data-ttu-id="227f9-145">20150601</span><span class="sxs-lookup"><span data-stu-id="227f9-145">20150601</span></span> |<span data-ttu-id="227f9-146">2</span><span class="sxs-lookup"><span data-stu-id="227f9-146">2</span></span> |<span data-ttu-id="227f9-147">4</span><span class="sxs-lookup"><span data-stu-id="227f9-147">4</span></span> |
| <span data-ttu-id="227f9-148">20150701</span><span class="sxs-lookup"><span data-stu-id="227f9-148">20150701</span></span> |<span data-ttu-id="227f9-149">3</span><span class="sxs-lookup"><span data-stu-id="227f9-149">3</span></span> |<span data-ttu-id="227f9-150">1</span><span class="sxs-lookup"><span data-stu-id="227f9-150">1</span></span> |
| <span data-ttu-id="227f9-151">20150801</span><span class="sxs-lookup"><span data-stu-id="227f9-151">20150801</span></span> |<span data-ttu-id="227f9-152">3</span><span class="sxs-lookup"><span data-stu-id="227f9-152">3</span></span> |<span data-ttu-id="227f9-153">1</span><span class="sxs-lookup"><span data-stu-id="227f9-153">1</span></span> |
| <span data-ttu-id="227f9-154">20150801</span><span class="sxs-lookup"><span data-stu-id="227f9-154">20150801</span></span> |<span data-ttu-id="227f9-155">3</span><span class="sxs-lookup"><span data-stu-id="227f9-155">3</span></span> |<span data-ttu-id="227f9-156">1</span><span class="sxs-lookup"><span data-stu-id="227f9-156">1</span></span> |
| <span data-ttu-id="227f9-157">20151001</span><span class="sxs-lookup"><span data-stu-id="227f9-157">20151001</span></span> |<span data-ttu-id="227f9-158">4</span><span class="sxs-lookup"><span data-stu-id="227f9-158">4</span></span> |<span data-ttu-id="227f9-159">2</span><span class="sxs-lookup"><span data-stu-id="227f9-159">2</span></span> |
| <span data-ttu-id="227f9-160">20151101</span><span class="sxs-lookup"><span data-stu-id="227f9-160">20151101</span></span> |<span data-ttu-id="227f9-161">4</span><span class="sxs-lookup"><span data-stu-id="227f9-161">4</span></span> |<span data-ttu-id="227f9-162">2</span><span class="sxs-lookup"><span data-stu-id="227f9-162">2</span></span> |
| <span data-ttu-id="227f9-163">20151201</span><span class="sxs-lookup"><span data-stu-id="227f9-163">20151201</span></span> |<span data-ttu-id="227f9-164">4</span><span class="sxs-lookup"><span data-stu-id="227f9-164">4</span></span> |<span data-ttu-id="227f9-165">2</span><span class="sxs-lookup"><span data-stu-id="227f9-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="227f9-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="227f9-166">Next steps</span></span>
<span data-ttu-id="227f9-167">toomigrate une base de données SQL Server, consultez [migration de base de données SQL Server](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="227f9-167">toomigrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
