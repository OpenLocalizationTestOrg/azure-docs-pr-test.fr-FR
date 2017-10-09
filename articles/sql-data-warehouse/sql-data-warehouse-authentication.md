---
title: aaaAuthentication tooAzure SQL Data Warehouse | Documents Microsoft
description: Azure Active Directory (AAD) et SQL Server authentication tooAzure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a>Authentification tooAzure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Présentation de la sécurité](sql-data-warehouse-overview-manage-security.md)
> * [Authentification](sql-data-warehouse-authentication.md)
> * [Chiffrement (portail)](sql-data-warehouse-encryption-tde.md)
> * [Chiffrement (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

tooconnect tooSQL l’entrepôt de données, vous devez passer les informations d’identification de sécurité à des fins d’authentification. Lors de l’établissement d’une connexion, certains paramètres de connexion sont configurés dans le cadre de l’établissement de votre session de requête.  

Pour plus d’informations sur la sécurité et la manière dont entrepôt de données tooyour tooenable connexions, consultez [sécuriser une base de données SQL Data Warehouse][Secure a database in SQL Data Warehouse].

## <a name="sql-authentication"></a>Authentification SQL
tooconnect tooSQL l’entrepôt de données, vous devez fournir hello informations suivantes :

* Nom complet du serveur
* Authentification SQL
* Nom d’utilisateur
* Mot de passe
* Base de données par défaut (facultatif)

Par défaut, la connexion connecte toohello *master* pas votre base de données utilisateur et de base de données. base de données tooconnect tooyour utilisateur, vous pouvez choisir toodo deux choses :

* Spécifiez la base de données par défaut hello lors de l’inscription de votre serveur avec l’Explorateur d’objets SQL Server dans SSDT, SSMS, ou dans votre chaîne de connexion d’application de hello. Par exemple, inclure le paramètre de InitialCatalog hello pour une connexion ODBC.
* Mettez en surbrillance la base de données utilisateur hello avant de créer une session dans SSDT.

> [!NOTE]
> instruction Transact-SQL de Hello **utilisez MyDatabase ;** n’est pas prise en charge pour la modification de la base de données hello pour une connexion. Pour obtenir des conseils connexion tooSQL l’entrepôt de données avec SSDT, consultez toohello [requête avec Visual Studio] [ Query with Visual Studio] l’article.
> 
> 

## <a name="azure-active-directory-aad-authentication"></a>Authentification Azure Active Directory (AAD)
[Azure Active Directory] [ What is Azure Active Directory] l’authentification est un mécanisme de connexion tooMicrosoft Azure SQL Data Warehouse à l’aide des identités dans Azure Active Directory (Azure AD). Avec l’authentification Azure Active Directory, vous pouvez gérer de manière centralisée les identités hello d’utilisateurs de base de données et d’autres services de Microsoft dans un emplacement central. Gestion des ID fournit un emplacement unique aux utilisateurs de SQL Data Warehouse toomanage et simplifie la gestion de l’autorisation. 

### <a name="benefits"></a>Avantages
Les avantages d’Azure Active Directory incluent :

* Fournit une authentification de serveur alternatif tooSQL.
* Vous aide à arrêter la prolifération hello des identités des utilisateurs sur les serveurs de base de données.
* Permet la rotation de mot de passe à un emplacement unique
* Gérer les autorisations de base de données à l’aide de groupes (AAD) externes.
* Élimine le stockage des mots de passe en activant l’authentification intégrée Windows et les autres formes d’authentification prises en charge par Azure Active Directory.
* Base de données utilise contenus utilisateurs tooauthenticate des identités au niveau de base de données hello.
* Prend en charge l’authentification basée sur le jeton pour les applications qui se connectent tooSQL l’entrepôt de données.
* Prend en charge Multi-Factor Authentication avec l’authentification universelle Active Directory pour SQL Server Management Studio. Pour obtenir une description de Multi-Factor Authentication, consultez [Prise en charge SSMS de Azure AD MFA avec la base de données SQL et SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

> [!NOTE]
> Azure Active Directory est encore relativement nouveau et présente certaines limitations. tooensure qu’Azure Active Directory est adapté à votre environnement, consultez [les fonctionnalités Azure AD et limitations][Azure AD features and limitations], plus précisément hello considérations supplémentaires.
> 
> 

### <a name="configuration-steps"></a>Configuration
Suivez ces étapes tooconfigure Active d’authentification Azure Directory.

1. Créer et renseigner un répertoire Azure Active Directory
2. Associer facultatif : Ou modifier hello active directory qui est associé à votre abonnement Azure
3. Créer un administrateur Azure Active Directory pour Azure SQL Data Warehouse
4. Configurer vos ordinateurs clients
5. Créer des utilisateurs de base de données dans votre base de données mappée de tooAzure identités AD
6. Se connecter tooyour l’entrepôt de données à l’aide d’identités Azure AD

Actuellement, les utilisateurs Azure Active Directory ne sont pas affichés dans l’Explorateur d’objets SSDT. Pour résoudre ce problème, afficher les utilisateurs de hello dans [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).

### <a name="find-hello-details"></a>Rechercher des détails de hello
* authentification Azure Active Directory Hello étapes tooconfigure et d’utilisation sont presque identiques pour la base de données SQL Azure et Azure SQL Data Warehouse. Suivez hello détaillées des étapes décrites dans la rubrique de hello [tooSQL de connexion de base de données ou SQL données entrepôt par à l’aide d’authentification Azure Active Directory](../sql-database/sql-database-aad-authentication.md).
* Créer des rôles de base de données personnalisée et ajouter des rôles d’utilisateurs toohello. Accordez ensuite des autorisations granulaires toohello rôles. Pour plus d’informations, consultez [Prise en main des autorisations du moteur de base de données](https://msdn.microsoft.com/library/mt667986.aspx).

## <a name="next-steps"></a>Étapes suivantes
toostart interrogation votre entrepôt de données avec Visual Studio et d’autres applications, consultez [requête avec Visual Studio][Query with Visual Studio].

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
