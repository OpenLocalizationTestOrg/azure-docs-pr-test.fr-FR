---
title: aaaAzure SQL connexions et utilisateurs | Documents Microsoft
description: "En savoir plus sur la gestion de la sécurité de la base de données SQL, en particulier toomanage base de sécurité de connexion et d’accès via le compte du principal au niveau du serveur hello."
keywords: "sécurité sql database, gestion de la sécurité de base de données, sécurité de connexion,sécurité de base de données, accès aux bases de données"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/23/2017
ms.author: rickbyh
ms.openlocfilehash: dff889b9fed09146a10008c0d11ca9e71d91df5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-and-granting-database-access"></a>Contrôle et octroi de l’accès à la base de données

Lorsque les règles de pare-feu ont été configurés, personnes peuvent se connecter tooa base de données SQL comme un des comptes d’administrateur hello, en tant que propriétaire de base de données hello ou un utilisateur de base de données dans la base de données hello.  

>  [!NOTE]  
>  Cette rubrique s’applique tooAzure SQL server et tooboth de la base de données SQL et SQL Data Warehouse bases de données qui sont créées sur le serveur de SQL Azure hello. Par souci de simplicité, la base de données SQL est utilisé lorsque vous faites référence tooboth de base de données SQL et SQL Data Warehouse. 
>

> [!TIP]
> Pour obtenir un didacticiel, consultez [Sécuriser votre base de données Azure SQL Database](sql-database-security-tutorial.md).
>


## <a name="unrestricted-administrative-accounts"></a>Comptes d’administration non restreints
Il existe deux comptes d’administration (**Administrateur de serveur** et **Administrateur Active Directory**) qui agissent en tant qu’administrateurs. Ouvrez de ces comptes d’administrateur de votre serveur SQL, tooidentify hello portail Azure et accédez toohello des propriétés de votre serveur SQL server.

![Administrateurs SQL Server](./media/sql-database-manage-logins/sql-admins.png)

- **Administrateur de serveur**   
Lorsque vous créez un serveur SQL Azure, vous devez désigner une **connexion d’administrateur de serveur**. SQL server crée ce compte comme un compte de connexion dans la base de données master hello. Ce compte se connecte à l’aide de l’authentification SQL Server (nom d’utilisateur et mot de passe). Un seul de ces comptes peut exister.   
- **Administrateur Azure Active Directory**   
Un compte Azure Active Directory individuel ou de groupe de sécurité peut également être configuré en tant qu’administrateur. Il est facultatif tooconfigure un administrateur Azure AD, mais un administrateur Azure AD doit être configuré si vous souhaitez que les comptes d’Azure AD toouse tooSQL tooconnect base de données. Pour plus d’informations sur la configuration d’accès Azure Active Directory, consultez [tooSQL de connexion de base de données ou SQL données entrepôt par à l’aide d’authentification Azure Active Directory](sql-database-aad-authentication.md) et [SSMS prend en charge pour Azure AD MFA avec SQL Base de données et SQL Data Warehouse](sql-database-ssms-mfa-authentication.md).
 

Hello **administrateur du serveur** et **AD Azure admin** comptes a hello suivant caractéristiques :
- Il s’agit de hello seuls comptes qui peuvent se connecter automatiquement tooany base de données SQL sur le serveur de hello. (tooconnect tooa base de données utilisateur autres comptes doivent être propriétaire de hello Hello de base de données, ou avoir un compte d’utilisateur dans la base de données utilisateur hello.)
- Ces comptes d’entrent des bases de données utilisateur en tant que hello `dbo` utilisateur et qu’ils disposent d’autorisations hello dans les bases de données utilisateur hello. (propriétaire hello d’une base de données utilisateur entre également la base de données hello comme hello `dbo` utilisateur.) 
- Ces comptes n’entrez pas hello `master` base de données comme hello `dbo` utilisateur et des autorisations limitées dans master. 
- Ces comptes ne sont pas membres de hello standard SQL Server `sysadmin` rôle serveur fixe, ce qui n’est pas disponible dans la base de données SQL.  
- Ces comptes peuvent créer, modifier et supprimer des bases de données, des connexions, des utilisateurs de MASTER et des règles de pare-feu au niveau du serveur.
- Ces comptes peuvent ajouter et supprimer des membres toohello `dbmanager` et `loginmanager` rôles.
- Ces comptes peuvent afficher hello `sys.sql_logins` (table système).

### <a name="configuring-hello-firewall"></a>Configuration du pare-feu hello
Lorsque le pare-feu de niveau serveur hello est configuré pour une adresse IP individuelle ou une plage, hello **SQL server admin** et hello **administrateur Active Directory de Azure** peut se connecter toohello de base de données master et hello toutes les bases de données utilisateur. pare-feu de niveau serveur Hello initial peut être configuré via hello [portail Azure](sql-database-get-started-portal.md), à l’aide [PowerShell](sql-database-get-started-powershell.md) ou à l’aide de hello [API REST](https://msdn.microsoft.com/library/azure/dn505712.aspx). Une fois la connexion établie, les règles supplémentaires de pare-feu au niveau du serveur peuvent également être configurées à l’aide de [Transact-SQL](sql-database-configure-firewall-settings.md).

### <a name="administrator-access-path"></a>Chemin d’accès administrateur
Lorsque le pare-feu de niveau serveur hello est correctement configuré, hello **SQL server admin** et hello **administrateur Active Directory de Azure** peut se connecter à l’aide des outils clients tels que SQL Server Management Studio ou SQL Outils de données du serveur. Uniquement hello derniers outils fournissent toutes les fonctionnalités de hello et capacités. Hello diagramme suivant montre une configuration standard pour hello deux comptes d’administrateur.

![Chemin d’accès administrateur](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

Lorsque vous utilisez un port ouvert dans le pare-feu au niveau du serveur hello, les administrateurs peuvent se connecter tooany base de données SQL.

### <a name="connecting-tooa-database-by-using-sql-server-management-studio"></a>Connexion de base de données tooa à l’aide de SQL Server Management Studio
Pour une vue d’ensemble de la création d’un serveur, une base de données, les règles de pare-feu de niveau serveur et à l’aide de SQL Server Management Studio tooquery une base de données, consultez [prise en main des serveurs de base de données SQL Azure, les bases de données et les règles de pare-feu à l’aide de hello portail Azure et SQL Server Management Studio](sql-database-get-started-portal.md).

> [!IMPORTANT]
> Il est recommandé de toujours utiliser hello dernière version de Management Studio tooremain synchronisés avec les mises à jour tooMicrosoft Azure et base de données SQL. [Mettre à jour SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).


## <a name="additional-server-level-administrative-roles"></a>Rôles d’administration au niveau du serveur supplémentaires
En outre toohello au niveau du serveur d’administration rôles indiqué précédemment, base de données SQL fournit deux rôles d’administration restreintes dans les comptes d’utilisateur toowhich hello base de données master peuvent être ajoutés qu’accorder des autorisations tooeither créer des bases de données ou gérer connexions.

### <a name="database-creators"></a>Créateurs de base de données
Un de ces rôles d’administration est hello **dbmanager** rôle. Les membres de ce rôle peuvent créer des bases de données. toouse ce rôle, vous créez un utilisateur dans hello `master` de base de données, puis ajoutez hello utilisateur toohello **dbmanager** rôle de base de données. toocreate une base de données, utilisateur de hello doit être un utilisateur basé sur une connexion SQL Server dans la base de données master hello ou contenus utilisateur de base de données basée sur un utilisateur Azure Active Directory.

1. À l’aide d’un compte d’administrateur, connectez-vous toohello de base de données master.
2. Étape facultative : créer une connexion d’authentification SQL Server, à l’aide de hello [CREATE LOGIN](https://msdn.microsoft.com/library/ms189751.aspx) instruction. Exemple d’instruction :
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > Utilisez un mot de passe fort au moment de la création d’une connexion ou d’un utilisateur de base de données à relation contenant-contenu. Pour plus d’informations, consultez la page [Mots de passe forts](https://msdn.microsoft.com/library/ms161962.aspx).
    
   performances de tooimprove, connexions (principaux au niveau du serveur) sont temporairement mis en cache au niveau de base de données hello. cache d’authentification toorefresh hello, consultez [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx).

3. Dans la base de données master hello, créez un utilisateur à l’aide de hello [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) instruction. Hello utilisateur peut être un utilisateur Azure Active Directory contenu de l’authentification de base de données (si vous avez configuré votre environnement pour l’authentification Azure AD), ou un utilisateur de base de données de contenu de l’authentification SQL Server ou un utilisateur de l’authentification SQL Server basé sur SQL Connexion d’authentification serveur (créée à l’étape précédente de hello). Exemples d’instructions :
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. Ajouter un nouvel utilisateur hello, toohello **dbmanager** rôle de base de données à l’aide de hello [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx) instruction. Exemples d’instructions :
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > Hello dbmanager est un rôle de base de données dans la base de données master, donc vous ne pouvez ajouter un rôle de base de données utilisateur toohello dbmanager. Impossible d’ajouter un rôle toodatabase connexion au niveau du serveur.
    
5. Si nécessaire, configurez un pare-feu règle tooallow hello nouvel utilisateur tooconnect. (utilisateur hello peut-être être couverts par une règle de pare-feu existante).

Maintenant, utilisateur de hello peut se connecter à base de données master toohello et peut créer de nouvelles bases de données. compte Hello création hello de base de données devienne propriétaire de hello de base de données hello.

### <a name="login-managers"></a>Gestionnaires de connexion
Hello autre rôle d’administrateur est responsable de compte de connexion hello. Membres de ce rôle peuvent créer des connexions dans la base de données master hello. Si vous le souhaitez, vous pouvez terminer hello les mêmes étapes (créer une connexion et l’utilisateur et ajouter un utilisateur toohello **loginmanager** rôle) tooenable un utilisateur toocreate de nouvelles connexions dans master de hello. Les connexions ne sont généralement pas nécessaires lorsque le niveau de base de données Microsoft recommande l’utilisation des utilisateurs de base de données, ce qui s’authentifient auprès de hello au lieu d’utiliser des utilisateurs basés sur des connexions. Pour plus d’informations, voir [Utilisateurs de base de données à relation contenant-contenu - Rendre votre base de données portable](https://msdn.microsoft.com/library/ff929188.aspx).

## <a name="non-administrator-users"></a>Utilisateurs non administrateurs
En règle générale, les comptes non administrateurs n’accèdent pas besoin aux toohello de base de données master. Créer des utilisateurs de base de données au niveau de base de données hello à l’aide de hello [CREATE USER (Transact-SQL)](https://msdn.microsoft.com/library/ms173463.aspx) instruction. Hello utilisateur peut être un utilisateur Azure Active Directory contenu de l’authentification de base de données (si vous avez configuré votre environnement pour l’authentification Azure AD), ou un utilisateur de base de données de contenu de l’authentification SQL Server ou un utilisateur de l’authentification SQL Server basé sur SQL Connexion d’authentification serveur (créée à l’étape précédente de hello). Pour plus d’informations, voir [Utilisateurs de base de données à relation contenant-contenu - Rendre votre base de données portable](https://msdn.microsoft.com/library/ff929188.aspx). 

les utilisateurs toocreate, connecter toohello de base de données et exécuter les instructions toohello similaire exemple suivant :

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

Initialement, seul l’un des administrateurs de hello ou propriétaire hello de base de données hello peut créer des utilisateurs. tooauthorize des utilisateurs supplémentaires toocreate nouveaux utilisateurs, accorder ce hello utilisateur sélectionné `ALTER ANY USER` autorisation, en utilisant une instruction telle que :

```
GRANT ALTER ANY USER tooMary;
```

contrôle total de toogive des utilisateurs de base de données hello, rendre un membre de hello **db_owner** rôle de base de données fixe à l’aide de hello `ALTER ROLE` instruction.

> [!NOTE]
> Hello courants raison toocreate de base de données des utilisateurs basés sur des connexions, est lorsque les utilisateurs de l’authentification SQL Server qui doivent accéder aux bases de données toomultiple. Les utilisateurs basés sur des connexions sont liés toohello connexion et qu’un seul mot de passe qui est conservé pour que la connexion. Les utilisateurs de base de données contenu dans des bases de données individuelles sont des entités distinctes qui conservent leur propre mot de passe. Cela peut être source de confusion pour les utilisateurs de base de données contenu s’ils ne conservent pas un mot de passe identique.

### <a name="configuring-hello-database-level-firewall"></a>Configuration du pare-feu de niveau base de données hello
Comme meilleure pratique, les utilisateurs non-administrateurs doivent avoir uniquement les accès via les bases de données toohello de pare-feu hello qu’ils utilisent. Au lieu d’autoriser son adresse IP adresses hello au niveau du serveur par le biais du pare-feu et en leur donnant accès tooall bases de données, utilisez hello [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) pare-feu de base de données de niveau instruction tooconfigure hello. pare-feu de niveau base de données Hello ne peut pas être configuré à l’aide du portail de hello.

### <a name="non-administrator-access-path"></a>Chemin d’accès non administrateur
Pare-feu de niveau base de données hello est correctement configuré, les utilisateurs de base de données hello peuvent se connecter à l’aide des outils clients tels que SQL Server Management Studio ou SQL Server Data Tools. Uniquement hello derniers outils fournissent toutes les fonctionnalités de hello et capacités. Hello suivant schéma montre un chemin d’accès non-administrateur classique.

![Chemin d’accès non administrateur](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>Groupes et rôles
Gestion de l’accès efficace utilise les autorisations affectées toogroups et les rôles au lieu d’utilisateurs individuels. 

- Lorsque vous utilisez l’authentification Azure Active Directory, placez les utilisateurs Azure Active Directory dans un groupe Azure Active Directory. Créez un utilisateur de base de données pour le groupe de hello. Placer un ou plusieurs utilisateurs de base de données dans un [rôle de base de données](https://msdn.microsoft.com/library/ms189121) , puis affectez [autorisations](https://msdn.microsoft.com/library/ms191291.aspx) rôle de base de données toohello.

- Lorsque vous utilisez l’authentification SQL Server, créez les utilisateurs de base de données dans la base de données hello. Placer un ou plusieurs utilisateurs de base de données dans un [rôle de base de données](https://msdn.microsoft.com/library/ms189121) , puis affectez [autorisations](https://msdn.microsoft.com/library/ms191291.aspx) rôle de base de données toohello.

rôles de base de données Hello peuvent être tel que les rôles intégrés de hello **db_owner**, **db_ddladmin**, **db_datawriter**, **db_datareader**, **db_denydatawriter**, et **db_denydatareader**. **db_owner** est couramment utilisés toogrant une autorisation totale tooonly quelques utilisateurs. Hello autres rôles de base de données fixe sont utiles pour l’obtention d’une base de données simple dans le développement rapidement, mais ne sont pas recommandés pour la plupart des bases de données de production. Par exemple, hello **db_datareader** rôle de base de données fixe accorde l’accès en lecture tooevery table de base de données hello, qui est généralement plus d’est strictement nécessaire. Il est préférable de toouse hello [CREATE ROLE](https://msdn.microsoft.com/library/ms187936.aspx) instruction toocreate votre propre défini par l’utilisateur soigneusement accorder des autorisations minimales nécessaires aux besoins d’entreprise hello hello de chaque rôle et les rôles de base de données. Lorsqu’un utilisateur est un membre de plusieurs rôles, ils regroupent toutes les autorisations hello.

## <a name="permissions"></a>Autorisations
Il existe plus de 100 autorisations qui peuvent être accordées ou refusées individuellement dans la base de données SQL. La plupart de ces autorisations sont imbriquées. Par exemple, hello `UPDATE` sur un schéma inclut hello `UPDATE` autorisation sur chaque table dans ce schéma. Comme dans la plupart des systèmes d’autorisation, hello une autorisation refusées une instruction grant. Hello imbriqué et nombre hello d’autorisations, peut prendre une étude de toodesign un tooproperly de système d’autorisation appropriée protéger votre base de données. Démarrer avec la liste hello des autorisations au [autorisations (moteur de base de données)](https://msdn.microsoft.com/library/ms191291.aspx) et examinez hello [graphique de taille poster](http://go.microsoft.com/fwlink/?LinkId=229142) d’autorisations de hello.


### <a name="considerations-and-restrictions"></a>Considérations et restrictions
Lors de la gestion des connexions et les utilisateurs de base de données SQL, tenez compte des éléments suivants de hello :

* Vous devez être connecté toohello **master** de base de données lors de l’exécution hello `CREATE/ALTER/DROP DATABASE` instructions.   
* Hello toohello correspondant de base de données utilisateur **administrateur du serveur** connexion ne peut pas être modifiée ou supprimée. 
* Anglais-US est la langue par défaut de hello Hello **administrateur du serveur** connexion.
* Hello uniquement les administrateurs (**administrateur du serveur** connexion ou administrateur Azure AD) et les membres de hello Hello **dbmanager** rôle de base de données dans hello **master** ont de la base de données hello de tooexecute autorisation `CREATE DATABASE` et `DROP DATABASE` instructions.
* Vous devez être connecté toohello de base de données master lors de l’exécution hello `CREATE/ALTER/DROP LOGIN` instructions. L’utilisation de connexions est toutefois déconseillée. Préférez l’emploi d’utilisateurs de base de données à relation contenant-contenu.
* tooconnect tooa base de données utilisateur, vous devez fournir nom hello de base de données hello dans la chaîne de connexion hello.
* Uniquement hello au niveau du serveur principal connexion hello membres et de hello **loginmanager** rôle de base de données dans hello **master** base de données a hello de tooexecute autorisation `CREATE LOGIN`, `ALTER LOGIN`, et `DROP LOGIN` instructions.
* Lors de l’exécution hello `CREATE/ALTER/DROP LOGIN` et `CREATE/ALTER/DROP DATABASE` instructions dans une application ADO.NET, à l’aide des commandes paramétrées est interdit. Pour plus d’informations, voir [Commandes et paramètres](https://msdn.microsoft.com/library/ms254953.aspx).
* Lors de l’exécution hello `CREATE/ALTER/DROP DATABASE` et `CREATE/ALTER/DROP LOGIN` instructions, chacune de ces instructions doit être hello uniquement une instruction dans un lot Transact-SQL. Sinon, une erreur se produit. Par exemple, hello que Transact-SQL suivant vérifie l’existence de la base de données hello. S’il en existe un `DROP DATABASE` instruction est appelée base de données tooremove hello. Étant donné que hello `DROP DATABASE` instruction n’est pas hello une seule instruction dans le lot de hello, l’exécution suivante de hello instruction Transact-SQL génère une erreur.

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* Lors de l’exécution hello `CREATE USER` instruction avec hello `FOR/FROM LOGIN` option, il doit être hello uniquement une instruction dans un lot Transact-SQL.
* Lors de l’exécution hello `ALTER USER` instruction avec hello `WITH LOGIN` option, il doit être hello uniquement une instruction dans un lot Transact-SQL.
* trop`CREATE/ALTER/DROP` un utilisateur requiert hello `ALTER ANY USER` sur hello de base de données.
* Lorsque le propriétaire hello d’un rôle de base de données tente de tooadd ou supprimer un autre tooor d’utilisateur de base de données à partir de ce rôle de base de données, hello l’erreur suivante peut se produire : **utilisateur ou le rôle 'Name' n’existe pas dans cette base de données.** Cette erreur se produit, car l’utilisateur de hello n’est pas visible toohello propriétaire. tooresolve ce problème, accordez hello rôle propriétaire hello `VIEW DEFINITION` autorisation sur hello utilisateur. 


## <a name="next-steps"></a>Étapes suivantes

- toolearn en savoir plus sur les règles de pare-feu, consultez [pare-feu de base de données SQL Azure](sql-database-firewall-configure.md).
- Pour une vue d’ensemble de toutes les fonctionnalités de sécurité de base de données SQL hello, consultez [vue d’ensemble de la sécurité SQL](sql-database-security-overview.md).
- Pour obtenir un didacticiel, consultez [Sécuriser votre base de données Azure SQL Database](sql-database-security-tutorial.md).
- Pour plus d’informations sur les vues et procédures stockées, consultez [Création des vues et des procédures stockées](https://msdn.microsoft.com/library/ms365311.aspx).
- Pour plus d’informations sur l’octroi d’objet de base de données access tooa, consultez [tooa d’octroi de l’accès des objets de base de données](https://msdn.microsoft.com/library/ms365327.aspx)
