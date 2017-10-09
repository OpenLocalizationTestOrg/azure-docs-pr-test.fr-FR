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
# <a name="load-sample-data-into-sql-data-warehouse"></a>Charger des exemples de données dans SQL Data Warehouse
Suivez ces tooload des étapes simples et la base de données Adventure Works exemple de requête hello. Ces scripts d’abord utilisent sqlcmd toorun SQL qui crée des tables et des vues. Une fois que les tables ont été créées, les scripts hello utilise bcp tooload données.  Si vous n’avez pas encore sqlcmd et bcp installé, suivez ces liens trop[installer bcp] [ install bcp] et trop[installer sqlcmd][install sqlcmd].

## <a name="load-sample-data"></a>Charger les exemples de données
1. Télécharger hello [Adventure Works exemples de Scripts pour SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] fichier zip.
2. Extrayez les fichiers de hello du répertoire de tooa zip téléchargé sur votre ordinateur local.
3. Modifiez les hello extrait fichier aw_create.bat et définissez les hello suivant des variables qui figurent en haut de hello du fichier de hello.  N’être tooleave qu’aucun espace blanc entre = « hello » et le paramètre hello.  Vous trouverez ci-dessous des exemples de ce à quoi vos modifications peuvent ressembler.
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. À partir d’une invite de commandes Windows, exécutez hello modifié aw_create.bat.  Veillez à ce que vous êtes dans le répertoire hello où vous avez enregistré votre version modifiée du aw_create.bat.
   Ce script va...
   
   * Supprimer les tables ou vues Adventure Works qui existent déjà dans votre base de données.
   * Créer des vues et tables de Adventure Works hello
   * Charger chaque table Adventure Works à l'aide de bcp.
   * Valider le nombre de lignes hello pour chaque table Adventure Works
   * Collecter les statistiques sur chaque colonne pour chaque table Adventure Works.

## <a name="query-sample-data"></a>Interrogation des données de l'exemple
Lorsque vous avez chargé des exemples de données dans SQL Data Warehouse, vous pouvez exécuter rapidement quelques requêtes.  toorun une requête, connectez tooyour nouvellement créée de la base de données Adventure Works dans l’entrepôt de données SQL Azure à l’aide de Visual Studio et SSDT, comme décrit dans hello [requête avec Visual Studio] [ query with Visual Studio] document.

Exemple de simple Sélectionnez instruction tooget toutes informations hello des employés de hello :

```sql
SELECT * FROM DimEmployee;
```

Exemple d’une requête plus complexe à l’aide des constructions telles que GROUP BY toolook à la quantité totale de hello pour toutes les ventes chaque jour :

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Exemple d’une instruction SELECT avec une toofilter de clause WHERE ordres d’avant une date donnée :

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

SQL Data Warehouse prend en charge presque toutes les constructions T-SQL prises en charge par SQL Server.  Toutes les différences sont documentées dans notre documentation sur la [migration du code][migrate code].

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez une chance tootry des requêtes avec des exemples de données, consultez Procédure trop[développer][develop], [charger][load], ou [ migrer] [ migrate] tooSQL l’entrepôt de données.

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
