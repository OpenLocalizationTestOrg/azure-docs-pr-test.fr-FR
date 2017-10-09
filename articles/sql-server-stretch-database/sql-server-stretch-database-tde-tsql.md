---
title: "aaaEnable chiffrement Transparent des données pour Stretch TSQL de base de données - Azure | Documents Microsoft"
description: "Activer le chiffrement transparent des données (TDE) pour SQL Server Stretch Database sur Azure TSQL"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a>Activer le chiffrement transparent des données (TDE) pour Stretch Database sur Azure (Transact-SQL)
> [!div class="op_single_selector"]
> * [Portail Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Chiffrement transparent des données (TDE) vous aide à protéger contre les menaces hello d’activités malveillantes en effectuant le chiffrement en temps réel et le déchiffrement de la base de données de hello, les sauvegardes associées et les fichiers journaux des transactions au repos sans nécessiter de modifications toohello application.

Stockage hello d’une base de données entière est chiffré à l’aide d’une clé de chiffrement de base de données hello appelée de clé symétrique. clé de chiffrement de base de données Hello est protégé par un certificat de serveur intégré. certificat de serveur intégré Hello est unique pour chaque serveur Azure. Microsoft alterne automatiquement ces certificats au moins tous les 90 jours. Pour obtenir une description générale du chiffrement transparent des données, consultez [Chiffrement transparent des données (TDE)].

## <a name="enabling-encryption"></a>Activation du chiffrement
tooenable chiffrement transparent des données pour une base de données Azure stocke hello les données migrées à partir d’une base de données SQL Server compatible Stretch, hello suivant choses :

1. Se connecter toohello *master* base de données sur hello serveur Azure hébergement hello de base de données à l’aide d’une connexion qui est un administrateur ou un membre de hello **dbmanager** rôle dans la base de données master hello
2. Exécutez hello suivant de base de données instruction tooencrypt hello.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Désactivation du chiffrement
toodisable chiffrement transparent des données pour une base de données Azure stocke hello les données migrées à partir d’une base de données SQL Server compatible Stretch, hello suivant choses :

1. Se connecter toohello *master* de la base de données à l’aide d’une connexion qui est un administrateur ou un membre de hello **dbmanager** rôle dans la base de données master hello
2. Exécutez hello suivant de base de données instruction tooencrypt hello.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a>Vérification de chiffrement
état du chiffrement tooverify pour une base de données Azure stocke hello les données migrées à partir d’une base de données SQL Server compatible Stretch, hello suivant choses :

1. Se connecter toohello *master* ou instance de base de données à l’aide d’une connexion qui est un administrateur ou un membre de hello **dbmanager** rôle dans la base de données master hello
2. Exécutez hello suivant de base de données instruction tooencrypt hello.

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

Un résultat de ```1``` indique une base de données chiffrée, ```0``` indique une base de données non chiffrée.

<!--Anchors-->
[Chiffrement transparent des données (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
