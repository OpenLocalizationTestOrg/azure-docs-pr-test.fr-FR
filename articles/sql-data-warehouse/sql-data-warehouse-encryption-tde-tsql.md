---
title: "aaaTransparent chiffrement des données dans l’entrepôt de données SQL (T-SQL) | Documents Microsoft"
description: "Chiffrement transparent des données (TDE) dans SQL Data Warehouse (T-SQL)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a>Prise en main du chiffrement transparent des données (TDE)
> [!div class="op_single_selector"]
> * [Présentation de la sécurité](sql-data-warehouse-overview-manage-security.md)
> * [Authentification](sql-data-warehouse-authentication.md)
> * [Chiffrement (portail)](sql-data-warehouse-encryption-tde.md)
> * [Chiffrement (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Autorisations requises
tooenable Transparent Data Encryption (TDE), vous devez être un administrateur ou un membre du rôle dbmanager de hello.

## <a name="enabling-encryption"></a>Activation du chiffrement
Suivez ces étapes de tooenable chiffrement transparent des données d’un entrepôt de données SQL :

1. Se connecter toohello *master* base de données serveur hello hébergeant hello de base de données à l’aide d’une connexion qui est un administrateur ou un membre de hello **dbmanager** rôle dans la base de données master hello
2. Exécutez hello suivant de base de données instruction tooencrypt hello.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Désactivation du chiffrement
Suivez ces étapes de toodisable chiffrement transparent des données d’un entrepôt de données SQL :

1. Se connecter toohello *master* de la base de données à l’aide d’une connexion qui est un administrateur ou un membre de hello **dbmanager** rôle dans la base de données master hello
2. Exécutez hello suivant de base de données instruction tooencrypt hello.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> Un entrepôt de données SQL en pause doit être repris avant d’apporter des modifications des paramètres de TDE toohello.
> 
> 

## <a name="verifying-encryption"></a>Vérification de chiffrement
état du chiffrement tooverify pour un entrepôt de données SQL, suivez les étapes de hello ci-dessous :

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

## <a name="encryption-dmvs"></a>DMV de chiffrement
* [sys.databases][sys.databases] 
* [sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
