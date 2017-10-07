---
title: "aaaResolving de base de données SQL de T-SQL Azure de migration de différences | Documents Microsoft"
description: "Instructions Transact-SQL qui ne sont pas entièrement prises en charge dans Azure SQL Database"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: c05abd9e-28a7-4c97-9bdf-bc60d08fc92e
ms.service: sql-database
ms.custom: load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 03/17/2017
ms.author: rickbyh
ms.openlocfilehash: 3852013338bfdc6c7da9d1d879c54781682bc635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resolving-transact-sql-differences-during-migration-toosql-database"></a>Résolution des différences de Transact-SQL au cours de la migration tooSQL de base de données   
Lorsque [migrer votre base de données](sql-database-cloud-migrate.md) à partir de SQL Server tooAzure SQL Server, vous pouvez constater que votre base de données requiert certains refonte avant hello SQL Server peuvent être migré. Cette rubrique fournit des tooassist conseils vous en effectuant cette nouvelle ingénierie et présentation hello sous-jacent raisons pour lesquelles hello refonte est nécessaire. toodetect incompatibilités, utilisez hello [données Migration Assistant (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).

## <a name="overview"></a>Vue d'ensemble
La plupart des fonctionnalités Transact-SQL utilisées par les applications sont entièrement prises en charge dans Microsoft SQL Server et Azure SQL Database. Bonjour, par exemple, les principaux composants SQL telles que les types de données, opérateurs, chaîne, arithmétiques, logiques et les fonctions de curseur, fonctionnent de façon identique dans SQL Server et la base de données SQL. Il existe toutefois quelques différences au niveau des éléments du langage de définition de données (DDL) et des éléments du langage de manipulation de données (DML). Ceux-ci génèrent en effet des instructions et des requêtes T-SQL qui ne sont que partiellement prises en charge (nous y reviendrons plus loin dans cette rubrique).

En outre, certaines fonctionnalités et syntaxe non prise en charge du tout, car la base de données SQL Azure est conçu tooisolate les fonctionnalités des dépendances sur la base de données master hello et le système d’exploitation de hello. Ainsi, de nombreuses activités de niveau serveur sont inappropriées pour SQL Database. Les instructions et les options T-SQL ne sont pas disponibles si elles configurent des options de niveau serveur et des composants du système d’exploitation, ou spécifient la configuration du système de fichiers. Si de telles fonctionnalités sont nécessaires, vous trouverez la plupart du temps une alternative appropriée en procédant différemment à partir de SQL Database ou d’un autre service/d’une autre fonctionnalité Azure. 

Par exemple, haute disponibilité est créée dans Azure, configuration Always On n’est pas nécessaire (bien que vous souhaiterez tooconfigure géo-réplication active pour la récupération plus rapide en cas de hello d’urgence). Par conséquent, les instructions T-SQL liées tooavailability groupes ne sont pas pris en charge par la base de données SQL, et tooAlways associés des vues de gestion dynamique hello sur sont également pas pris en charge.

Pour obtenir la liste des fonctionnalités hello qui sont pris en charge et non pris en charge par la base de données SQL, consultez [comparaison des fonctionnalités de base de données SQL Azure](sql-database-features.md). liste Hello sur cette page complète de cette rubrique instructions et des fonctionnalités et se concentre sur les instructions Transact-SQL.

## <a name="transact-sql-syntax-statements-with-partial-differences"></a>Instructions Transact-SQL avec des différences partielles
les instructions DDL (langage de définition de données) Hello core sont disponibles, mais certaines instructions DDL ont la sélection élective d’extensions toodisk connexes et les fonctionnalités prises en charge. 

- Les instructions CREATE et ALTER DATABASE ont plus d’une trentaine d’options. les instructions de Hello incluent le placement des fichiers FILESTREAM et les options de service broker qui s’appliquent uniquement des tooSQL Server. Cela ne peut pas déterminer si vous créez des bases de données avant de migrer, mais si vous migrez le code T-SQL qui crée les bases de données, vous devez comparer [CREATE DATABASE (base de données de SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) avec la syntaxe SQL Server hello à [créer Base de données (SQL Server Transact-SQL)](https://msdn.microsoft.com/library/ms176061.aspx) toomake que vous utilisez toutes les options de hello sont pris en charge. CRÉER une base de données pour la base de données SQL Azure a également l’objectif de service et les options de mise à l’échelle élastique qui s’appliquent uniquement tooSQL de base de données.
- les instructions CREATE et ALTER TABLE Hello ont des options de table de fichiers qui ne peut pas être utilisées sur la base de données SQL car FILESTREAM n’est pas pris en charge.
- Pour les instructions CREATE et ALTER login sont pris en charge mais la base de données SQL n’offre pas toutes les options de hello. toomake de qu'encourage de votre base de données plus portable, base de données SQL à l’aide contenu aux utilisateurs de base de données au lieu des comptes de connexion chaque fois que possible. Pour plus d’informations, consultez [CREATE/ALTER LOGIN](https://msdn.microsoft.com/library/ms189828.aspx) et [Contrôle et octroi de l’accès à la base de données](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).

## <a name="transact-sql-syntax-not-supported-in-sql-database"></a>Syntaxe Transact-SQL non prise en charge dans SQL Database   
En outre toohello connexes des instructions de tooTransact-SQL non pris en charge les fonctionnalités décrites dans [comparaison des fonctionnalités de base de données SQL Azure](sql-database-features.md), hello instructions et les groupes d’instructions suivants, ne sont pas pris en charge. Par conséquent, si votre base de données toobe migré est à l’aide de hello suivantes des fonctionnalités, remanier votre tooeliminate T-SQL les fonctionnalités T-SQL et les instructions suivantes.

- Classement des objets système
- Connexions associées : instructions de point de terminaison, `ORIGINAL_DB_NAME`. Base de données SQL ne prend pas en charge l’authentification Windows, mais ne prend pas en charge l’authentification Azure Active Directory similaire hello. Certains types d’authentification nécessitent la version la plus récente de SSMS hello. Pour plus d’informations, consultez [tooSQL de connexion de base de données ou SQL données entrepôt par à l’aide d’authentification Azure Active Directory](sql-database-aad-authentication.md).
- Requêtes dans plusieurs bases de données à l’aide de noms à trois ou quatre parties. (Les requêtes sur plusieurs bases de données en lecture seule sont prises en charge à l’aide d’une [requête de base de données élastique](sql-database-elastic-query-overview.md).)
- Chaînage d’appartenance entre plusieurs bases de données, paramètre `TRUSTWORTHY`
- `DATABASEPROPERTY` Utilisez `DATABASEPROPERTYEX` à la place.
- `EXECUTE AS LOGIN` Utilisez « EXECUTE AS USER » à la place.
- Le chiffrement est pris en charge, à l’exception de la gestion de clés extensible.
- Gestion des événements : événements, notifications d’événements, notifications de requête.
- Placement des fichiers : syntaxe liée toodatabase placement des fichiers, la taille et les fichiers de base de données qui sont gérées automatiquement par Microsoft Azure.
- Haute disponibilité : syntaxe liée toohigh disponibilité, qui est gérée via votre compte Microsoft Azure. Cela inclut la syntaxe pour la sauvegarde, la restauration, la fonctionnalité AlwaysOn, la mise en miroir de bases de données, la copie des journaux de transaction et les modes de récupération.
- Lecteur de journal : syntaxe qui s’appuie sur le lecteur de journal hello, qui n’est pas disponible sur la base de données SQL : réplication par émission, la Capture de données modifiées. SQL Database peut être un abonné d’un article de réplication par émission.
- Fonctions : `fn_get_sql`, `fn_virtualfilestats`,`fn_virtualservernodes`
- Tables globales temporaires
- Matériel : Les paramètres de serveur liées toohardware liés à la syntaxe : telles que la mémoire, threads de travail, l’affinité du processeur, indicateurs de trace. Utilisez plutôt les niveaux de service.
- `HAS_DBACCESS`
- `KILL STATS JOB`
- `OPENQUERY`, `OPENROWSET`, `OPENDATASOURCE` et noms en quatre parties
- .NET Framework : intégration du CLR à SQL Server
- Recherche sémantique
- Informations d’identification du serveur : utilisez à la place les [informations d’identification incluses dans l’étendue de la base de données](https://msdn.microsoft.com/library/mt270260.aspx).
- Éléments au niveau du serveur : les rôles de serveur, `IS_SRVROLEMEMBER`, `sys.login_token`, `GRANT`, `REVOKE` et `DENY` des autorisations de niveau serveur ne sont pas disponibles, bien que certains soient remplacés par des autorisations au niveau base de données. Certaines vues de gestion dynamique utiles au niveau du serveur ont des vues de gestion dynamique équivalentes au niveau de la base de données.
- `SET REMOTE_PROC_TRANSACTIONS`
- `SHUTDOWN`
- `sp_addmessage`
- Options `sp_configure` et `RECONFIGURE`. Certaines options sont disponibles à l’aide [d’ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).
- `sp_helpuser`
- `sp_migrate_user_to_contained`
- L’Agent SQL Server : Syntaxe repose sur la base de données MSDB hello SQL Server Agent ou hello : alertes, des opérateurs, des serveurs d’administration centrale. Utilisez des scripts tels qu’Azure PowerShell à la place.
- Audit SQL Server : utilisez plutôt l’audit SQL Database.
- SQL Server trace
- Indicateurs de trace : l’indicateur de trace certains éléments ont été déplacés toocompatibility modes.
- Débogage Transact-SQL
- Déclencheurs : déclencheurs au niveau du serveur ou de connexion
- `USE`instruction : toochange hello contexte tooa autre base de données, vous devez effectuer une nouvelle connexion toohello base de données.

## <a name="full-transact-sql-reference"></a>Référence complète Transact-SQL
Pour plus d'informations sur la grammaire, l'utilisation et les exemples Transact-SQL, consultez [Référence Transact-SQL (moteur de la base de données)](https://msdn.microsoft.com/library/bb510741.aspx) dans la documentation en ligne de SQL Server. 

### <a name="about-hello-applies-to-tags"></a>À propos des balises de hello « S’applique à »
Hello référence Transact-SQL inclut tooSQL de rubriques connexes Server versions 2008 toohello présent. Sous le titre de rubrique hello, il existe une barre d’icônes et liste hello quatre SQL Server ainsi que l’applicabilité indique. Par exemple, la fonction des groupes de disponibilité ont été introduits dans SQL Server 2012. Le [CREATE AVAILABILTY GROUP](https://msdn.microsoft.com/library/ff878399.aspx) rubrique indique que l’instruction de hello s’applique aux **SQL Server (à partir de 2012)**. instruction de Hello ne s’applique pas tooSQL Server 2008, SQL Server 2008 R2, base de données SQL Azure, Azure SQL Data Warehouse ou Parallel Data Warehouse.

Dans certains cas, le sujet général de hello d’une rubrique peut être utilisé dans un produit, mais il existe des différences mineures entre les produits. différences de Hello sont affichées en points milieu dans la rubrique hello comme il convient. Dans certains cas, le sujet général de hello d’une rubrique peut être utilisé dans un produit, mais il existe des différences mineures entre les produits. différences de Hello sont affichées en points milieu dans la rubrique hello comme il convient. Par exemple une rubrique de CREATE TRIGGER hello est disponible dans la base de données SQL. Mais hello **ALL SERVER** option des déclencheurs de niveau serveur, indique que les déclencheurs de niveau serveur ne peut pas être utilisées dans la base de données SQL. Utilisez plutôt des déclencheurs de niveau base de données.

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir la liste des fonctionnalités hello qui sont pris en charge et non pris en charge par la base de données SQL, consultez [comparaison des fonctionnalités de base de données SQL Azure](sql-database-features.md). liste Hello sur cette page complète de cette rubrique instructions et des fonctionnalités et se concentre sur les instructions Transact-SQL.

