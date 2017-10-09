---
title: authentification de facteurs aaaMulti - SQL Azure | Documents Microsoft
description: "Utilisez l’authentification multi-facteur avec SSMS pour la base de données SQL et SQL Data Warehouse."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2017
ms.author: rickbyh
ms.openlocfilehash: 57ef63b7c7f2c5cf64c3e1ee194d865ee5b14177
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>Authentification universelle avec SQL Database et SQL Data Warehouse (prise en charge de SSMS pour MFA)
Azure SQL Database et Azure SQL Data Warehouse prennent en charge les connexions à partir de SQL Server Management Studio (SSMS) à l’aide de *l’authentification universelle Active Directory*. 
**Télécharger hello la dernière version de SSMS** - sur l’ordinateur client de hello, télécharger la version la plus récente de SSMS, hello à partir de [télécharger SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Pour toutes les fonctionnalités de hello dans cette rubrique, utilisez au moins 2017 juillet, version 17,2.  boîte de dialogue connexion plus récent Hello, ressemble à ceci : ![1mfa-universal-connect](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "la zone de nom d’utilisateur hello se termine.")  

## <a name="hello-five-authentication-options"></a>options d’authentification Hello cinq  
- L’authentification universelle Active Directory prend en charge deux méthodes d’authentification non interactive d’hello (`Active Directory - Password` l’authentification et `Active Directory - Integrated` authentification). Les méthodes d’authentification `Active Directory - Password` et `Active Directory - Integrated` non interactives peuvent être utilisées dans de nombreuses applications (ADO.NET, JDBC, ODBC, etc.). Ces deux méthodes n’entraînent jamais l’affichage de boîtes de dialogue contextuelles.

- L’authentification `Active Directory - Universal with MFA` est une méthode interactive prenant également en charge *Azure Multi-Factor Authentication* (MFA). Azure MFA permet toodata d’accès de sauvegarde et d’applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple. Il fournit une authentification forte avec un éventail d’options de vérification simple (appel téléphonique, message texte, les cartes à puce avec code confidentiel ou notification d’application mobile), méthode hello toochoose permettant aux utilisateurs qu’ils préfèrent. L’authentification multifacteur (MFA) interactive avec Azure AD peut afficher une boîte de dialogue contextuelle de validation.

Pour une description de Multi-Factor Authentication, consultez la rubrique [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md).
Pour les étapes de configuration, consultez [Configuration de l’authentification multifacteur aux bases de données Azure SQL pour SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Nom de domaine Azure AD et paramètre d’ID de locataire   

À partir de [SSMS version du 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), les utilisateurs qui sont importés dans hello Active Directory en cours à partir d’autres annuaires Azure Active Directory en tant que les utilisateurs invités, peuvent fournir le nom de domaine hello Azure AD, ou ID de locataire lorsqu’ils se connectent. Les utilisateurs invités incluent les utilisateurs qui sont invités à partir d’autres annuaires Azure AD, de comptes Microsoft, tels qu’outlook.com, hotmail.com et live.com, ou d’autres comptes, comme gmail.com. Cette information, permet **universels Active Directory avec l’authentification de l’authentification Multifacteur** hello tooidentify correct de l’authentification d’autorité. Cette option est également requise toosupport les comptes Microsoft (MSA) tels que outlook.com, hotmail.com, live.com ou comptes non-MSA. ID de ces utilisateurs souhaitant toobe authentifié à l’aide de l’authentification universelle doit entrer leur nom de domaine Azure AD ou d’un client. Ce paramètre représente Bonjour actuelle Azure AD domaine nom/client ID Bonjour À qu'azure serveur est lié. Par exemple, si le serveur Azure est associé au domaine Azure AD `contosotest.onmicrosoft.com` où utilisateur `joe@contosodev.onmicrosoft.com` est hébergé comme un utilisateur importé de domaine Azure AD `contosodev.onmicrosoft.com`, hello tooauthenticate requis de nom de domaine cet utilisateur est `contosotest.onmicrosoft.com`. Lors de l’utilisateur de hello est un utilisateur natif de hello Azure AD lié tooAzure serveur et n’est pas un compte MSA, aucun ID de client ou le nom de domaine n’est requis. le paramètre tooenter hello (commençant par SSMS version 17,2), Bonjour **connecter tooDatabase** boîte de dialogue, la boîte de dialogue hello terminée, en sélectionnant **Active Directory - universel avec l’authentification Multifacteur** l’authentification, Cliquez sur **Options**, hello complète **nom d’utilisateur** zone, puis cliquez sur hello **propriétés de connexion** onglet. Vérifiez hello **ID de client ou le nom de domaine AD** zone et fournissez d’autorité d’authentification, tels que nom de domaine hello (**contosotest.onmicrosoft.com**) ou hello GUID de l’ID de client hello.  
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-toobusiness-support"></a>Toobusiness d’entreprise AD Azure prend en charge   
Les utilisateurs Active Directory Azure pris en charge pour les scénarios d’Azure AD B2B en tant que les utilisateurs invités (consultez [Nouveautés Azure B2B collaboration](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) peuvent se connecter tooSQL de base de données et SQL Data Warehouse uniquement dans le cadre des membres d’un groupe créé dans AD Azure actuel et mappé manuellement à l’aide de hello Transact-SQL `CREATE USER` instruction dans une base de données. Par exemple, si `steve@gmail.com` est invité tooAzure AD `contosotest` (avec le domaine Azure Ad de hello `contosotest.onmicrosoft.com`), regrouper un répertoire Azure AD, telles que `usergroup` doit être créée dans hello Azure AD contenant hello `steve@gmail.com` membre. Ensuite, l’administrateur Azure AD SQL ou le propriétaire de la base de données Azure AD doit créer ce groupe pour une base de données spécifique (MyDatabase) en exécutant une instruction Transact-SQL `CREATE USER [usergroup] FROM EXTERNAL PROVIDER`. Une fois que l’utilisateur de base de données hello est créé, puis hello utilisateur `steve@gmail.com` pouvez vous connecter trop`MyDatabase` à l’aide de l’option authentification hello SSMS `Active Directory – Universal with MFA support`. Hello usergroup, par défaut, a hello uniquement se connecter d’autorisation et n’importe quel autre accès aux données qui devront toobe accordée dans hello normalement. Notez que l’utilisateur `steve@gmail.com` un utilisateur invité doit hello case à cocher et ajouter le nom de domaine hello AD `contosotest.onmicrosoft.com` Bonjour SSMS **propriété de connexion** boîte de dialogue. Hello **ID de client ou le nom de domaine Active Directory** option est uniquement pris en charge pour hello universel avec les options de connexion de l’authentification Multifacteur, sinon elle est grisée.

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>Limites de l’authentification universelle pour la base de données SQL et SQL Data Warehouse
* SSMS et SqlPackage.exe sont hello seuls outils actuellement activées pour l’authentification Multifacteur via l’authentification universelle Active Directory.
* SSMS version 17.2 prend en charge l’accès simultané de plusieurs utilisateurs à l’aide de l’authentification universelle avec MFA. Version 17,0 et 17.1, limitée un journal dans une instance de SSMS à l’aide du compte Azure Active Directory unique de l’authentification universelle tooa. toolog dans en tant qu’un autre compte Azure AD, vous devez utiliser une autre instance de SSMS. (Cette restriction est limitée tooActive authentification universelle Active ; vous pouvez vous connecter les serveurs de toodifferent à l’aide de l’authentification de mot de passe Active Directory, l’authentification intégrée Active Directory ou l’authentification SQL Server).
* SSMS prend en charge l’authentification universelle Active Directory pour la visualisation de l’Explorateur d’objets, de l’Éditeur de requête et du magasin de requêtes.
* SSMS version 17.2 fournit une prise en charge de l’Assistant DacFx pour l’exportation, l’extraction et le déploiement de la base de données. Une fois qu’un utilisateur spécifique est authentifié via la boîte de dialogue de l’authentification initiale hello à l’aide de l’authentification universelle, hello DacFx Assistant hello même manière que pour tous les autres méthodes d’authentification.
* Hello, Concepteur de tables SSMS ne prend pas en charge l’authentification universelle.
* Il n’existe aucune configuration logicielle supplémentaire nécessaire pour l’authentification universelle Active Directory, sauf que vous devez utiliser une version prise en charge de SSMS.  
* version d’Active Directory Authentication Library (ADAL) Hello pour l’authentification universelle a été ADAL.dll 3.13.9 disponible publié tooits mis à jour plus récente. Consultez [Active Directory Authentication Library 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).


## <a name="next-steps"></a>Étapes suivantes

- Pour les étapes de configuration, consultez [Configuration de l’authentification multifacteur aux bases de données Azure SQL pour SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).
- Accorder à d’autres d’accès de la base de données tooyour : [l’authentification de base de données SQL et d’autorisation : octroi de l’accès](sql-database-manage-logins.md)  
- Assurez-vous que d’autres personnes peuvent se connecter via le pare-feu hello : [règle de pare-feu de configurer un base de données SQL Azure au niveau du serveur à l’aide de hello le portail Azure](sql-database-configure-firewall-settings.md)  
- [Configurer et gérer l’authentification Azure Active Directory avec SQL Database ou SQL Data Warehouse](sql-database-aad-authentication-configure.md)  
- [Microsoft SQL Server Data-Tier Application Framework (17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [Importer un tooa de fichier BACPAC nouvelle base de données de SQL Azure](../sql-database/sql-database-import.md)  
- [Exporter un fichier BACPAC de tooa de base de données SQL Azure](../sql-database/sql-database-export.md)  
- Interface C# [Interface IUniversalAuthProvider](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
