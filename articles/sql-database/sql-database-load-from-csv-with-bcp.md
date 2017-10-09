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
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>Charger des données à partir d’un fichier CSV une base de données SQL Azure (fichiers plats)
Vous pouvez utiliser les données de tooimport hello bcp utilitaire de ligne de commande à partir d’un fichier CSV dans la base de données SQL Azure.

## <a name="before-you-begin"></a>Avant de commencer
### <a name="prerequisites"></a>Composants requis
les étapes toocomplete hello dans cet article, vous devez :

* Serveur logique et base de données SQL Azure
* utilitaire de ligne de commande de Hello bcp installé
* utilitaire de ligne de commande de Hello sqlcmd installé

Vous pouvez télécharger les utilitaires bcp et sqlcmd hello hello [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Données au format ASCII ou UTF-16
Si vous essayez de ce didacticiel avec vos propres données, vos données doivent toouse hello ASCII ou UTF-16 encodage bcp ne prenant pas en charge UTF-8. 

## <a name="1-create-a-destination-table"></a>1. Créer une table de destination
Définir une table dans la base de données SQL en tant que table de destination hello. les colonnes dans la table de hello Hello doivent correspondre toohello des données dans chaque ligne de votre fichier de données.

toocreate une table, ouvrez une invite de commandes et utilisez sqlcmd.exe hello de toorun commande suivante :

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


## <a name="2-create-a-source-data-file"></a>2. Créer un fichier de données source
Ouvrez le bloc-notes, puis copiez hello après des lignes de données dans un nouveau fichier texte, puis enregistrez ce fichier tooyour répertoire temp local, C:\Temp\DimDate2.txt. Ces données sont au format ASCII.

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

(Facultatif) tooexport vos propres données à partir d’une base de données SQL Server, ouvrez une invite de commandes et exécutez hello commande suivante. Remplacez TableName, ServerName, DatabaseName, Username et Password par vos propres informations.

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a>3. Charger des données hello
les données de salutation tooload, ouvrez une invite de commandes et exécutez les hello commande suivante, en remplaçant les valeurs hello pour le nom du serveur, nom de base de données, nom d’utilisateur et mot de passe avec vos propres informations.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Utilisez cette commande hello tooverify données a été correctement chargées.

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

résultats de Hello doivent ressembler à ceci :

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

## <a name="next-steps"></a>Étapes suivantes
toomigrate une base de données SQL Server, consultez [migration de base de données SQL Server](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
