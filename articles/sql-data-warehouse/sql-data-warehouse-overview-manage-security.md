---
title: "aaaSecure une base de données SQL Data Warehouse | Documents Microsoft"
description: "Conseils relatifs à la sécurisation d’une base de données dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>Sécuriser une base de données dans SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Présentation de la sécurité](sql-data-warehouse-overview-manage-security.md)
> * [Authentification](sql-data-warehouse-authentication.md)
> * [Chiffrement (portail)](sql-data-warehouse-encryption-tde.md)
> * [Chiffrement (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

Cet article explique les concepts de base hello de la sécurisation de votre base de données de l’entrepôt de données SQL Azure. Plus spécifiquement, cet article vous offre un aperçu sur les ressources dédiées à la limitation de l’accès, à la protection des données et à la surveillance des activités sur une base de données.

## <a name="connection-security"></a>Sécurité de la connexion
Sécurité de connexion fait référence à toohow vous limitez et sécurisez les connexions tooyour base de données à l’aide de règles de pare-feu et de chiffrement de la connexion.

Règles de pare-feu sont utilisés par les deux hello hello et serveur de base de données tooreject tentatives de connexion à partir d’adresses IP qui n’ont pas été explicitement dans la liste approuvée. tooallow des connexions à partir de votre application ou l’adresse IP publique de l’ordinateur client, vous devez d’abord créer une règle de pare-feu de niveau serveur à l’aide de hello portail Azure, les API REST ou PowerShell. Comme meilleure pratique, vous devez restreindre les plages d’adresses IP hello autorisés via le pare-feu de votre serveur autant que possibles.  tooaccess Azure SQL Data Warehouse à partir de votre ordinateur local, assurez-vous que le pare-feu hello sur votre réseau et l’ordinateur local autorise les communications sortantes sur le port TCP 1433.  Pour plus d’informations, consultez [Pare-feu d’Azure SQL Database][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule] et [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Connexions tooyour SQL Data Warehouse sont chiffrées par défaut.  Chiffrement modification toodisable des paramètres de connexion sont ignorés.

## <a name="authentication"></a>Authentification
L’authentification fait référence toohow vous prouver votre identité lors de la connexion de base de données toohello. SQL Data Warehouse prend actuellement en charge l’authentification SQL Server avec un nom d’utilisateur et un mot de passe, ainsi qu’Azure Active Directory. 

Lorsque vous avez créé un serveur logique de hello pour votre base de données, vous avez spécifié un compte de connexion « server admin » avec un nom d’utilisateur et un mot de passe. À l’aide de ces informations d’identification, vous pouvez authentifier tooany de base de données sur ce serveur en tant que propriétaire de base de données hello ou « dbo » via l’authentification SQL Server.

Toutefois, comme il est recommandé aux utilisateurs de votre organisation doivent utiliser un compte différent de tooauthenticate. De cette manière, vous pouvez limiter les autorisations hello toohello application et réduire les risques de hello d’activités malveillantes au cas où votre code d’application est d’attaque par injection de SQL tooa vulnérable. 

toocreate un utilisateur authentifié de SQL Server, connexion toohello **master** sur votre serveur avec votre connexion d’administrateur de serveur de base de données et créez une nouvelle connexion serveur.  En outre, il est une bonne idée de toocreate un utilisateur dans la base de données master hello pour les utilisateurs d’Azure SQL Data Warehouse. Création d’un utilisateur dans master permet une toologin d’utilisateur à l’aide des outils tels que SSMS sans spécifier un nom de base de données.  Cela leur permet également toouse hello objet explorer tooview toutes les bases de données sur un serveur SQL server.

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Puis, connectez tooyour **base de données SQL Data Warehouse** avec votre connexion d’administration de serveur et créez un utilisateur de base de données en fonction de la connexion au serveur hello vous venez de créer.

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Si un utilisateur prévoyez d’effectuer des opérations supplémentaires telles que la création de connexions ou la création de nouvelles bases de données, ils devront également toobe affecté toohello `Loginmanager` et `dbmanager` rôles dans la base de données master hello. Pour plus d’informations sur ces autres rôles et l’authentification tooa de base de données SQL, consultez [gestion des bases de données et des connexions dans la base de données SQL Azure][Managing databases and logins in Azure SQL Database].  Pour plus d’informations sur Azure AD pour l’entrepôt de données SQL, consultez [connexion tooSQL données entrepôt par à l’aide d’authentification Azure Active Directory][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication].

## <a name="authorization"></a>Autorisation
Autorisation fait référence toowhat vous pouvez effectuer dans une base de données Azure SQL Data Warehouse, et cela est contrôlé par les autorisations et les appartenances aux rôles de votre compte d’utilisateur. Comme meilleure pratique, vous devriez hello d’utilisateurs des privilèges minimaux nécessaires. Azure SQL Data Warehouse rend cette toomanage facile avec les rôles dans T-SQL :

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

compte d’administrateur de serveur Hello que vous connectez à l’aide est un membre de db_owner ayant autorité toodo quoi que ce soit dans la base de données hello. Enregistrez ce compte pour l’utiliser lors du déploiement des mises à niveau de schéma et d’autres opérations de gestion. Utiliser le compte de « ApplicationUser » de hello avec tooconnect d’autorisations plus limitée à partir de votre base de données application toohello avec hello des privilèges minimaux requis par votre application.

Il existe façons toofurther limite un utilisateur peut faire avec la base de données SQL Azure :

* Niveau de granularité [autorisations] [ Permissions] vous permettent de contrôle les opérations que vous pouvez sur des colonnes, tables, vues, procédures et autres objets de base de données hello. Utilisation des autorisations granulaires toohave hello un contrôle optimal et accordez hello les autorisations minimales nécessaires. système d’autorisation granulaire Hello est quelque peu complexe et nécessite quelques toouse étude efficacement.
* [Rôles de base de données] [ Database roles] autres que db_datareader et db_datawriter peuvent être utilisé toocreate les comptes d’utilisateur application plus puissants ou des comptes de gestion moins puissants. rôles de base de données fixe intégrée Hello fournissent un moyen simple toogrant des autorisations, mais peuvent entraîner l’octroi d’autorisations plus que nécessaire.
* [Procédures stockées] [ Stored procedures] peut être utilisé toolimit actions hello qui peuvent être effectuées sur la base de données hello.

Gérer des bases de données et les serveurs logiques dans hello portail classique Azure ou à l’aide des API Azure Resource Manager de hello est contrôlé par les attributions de rôles de votre compte d’utilisateur du portail. Pour en savoir plus à ce sujet, consultez [Contrôle d’accès en fonction du rôle dans le portail Azure][Role-based access control in Azure Portal].

## <a name="encryption"></a>Chiffrement
Azure SQL données entrepôt Transparent Data Encryption (TDE) protège contre les menaces hello d’activités malveillantes en effectuant le chiffrement en temps réel et déchiffrement de vos données au repos.  Lorsque vous chiffrez votre base de données, les sauvegardes associées et les fichiers journaux des transactions sont chiffrées sans nécessiter de toutes les applications de tooyour de modifications. Stockage hello d’une base de données entière est chiffré à l’aide d’une clé de chiffrement de base de données hello appelée de clé symétrique. Dans la base de données SQL, clé de chiffrement de base de données hello est protégé par un certificat de serveur intégré. certificat de serveur intégré Hello est unique pour chaque serveur de base de données SQL. Microsoft alterne automatiquement ces certificats au moins tous les 90 jours. algorithme de chiffrement Hello utilisé par SQL Data Warehouse est AES-256. Pour obtenir une description générale du chiffrement transparent des données, consultez la page [Transparent Data Encryption][Transparent Data Encryption].

Vous pouvez chiffrer votre base de données à l’aide de hello [Azure Portal] [ Encryption with Portal] ou [T-SQL][Encryption with TSQL].

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations et des exemples sur la connexion tooyour SQL Data Warehouse avec différents protocoles, consultez [connecter tooSQL Data Warehouse][Connect tooSQL Data Warehouse].

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
