---
title: "aaaSecuring bases de données PaaS dans Azure | Documents Microsoft"
description: " Découvrez les bonnes pratiques de sécurité Azure SQL Database et SQL Data Warehouse pour protéger vos applications mobiles et web PaaS. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: a7f9a2846b59dcb05e82f2ad88b41c5213295603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-databases-in-azure"></a>Sécurisation des bases de données PaaS dans Azure

Dans cet article, nous abordons un ensemble de bonnes pratiques de sécurité [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) et [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/) pour protéger vos applications mobiles et web PaaS. Ces recommandations sont dérivées de notre expérience avec Azure et les expériences hello de clients comme vous-même.

## <a name="azure-sql-database-and-sql-data-warehouse"></a>Azure SQL Database et SQL Data Warehouse
[Azure SQL Database](../sql-database/sql-database-technical-overview.md) et [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) fournissent un service de base de données relationnelle pour vos applications basées sur Internet. Examinons les services qui protègent vos applications et vos données lors de l’utilisation de SQL Database et de SQL Data Warehouse dans un déploiement PaaS :

- Authentification Azure Active Directory (au lieu de l'authentification SQL Server)
- Pare-feu SQL Azure
- Chiffrement transparent des données (TDE)

## <a name="best-practices"></a>Meilleures pratiques

### <a name="use-a-centralized-identity-repository-for-authentication-and-authorization"></a>Utiliser un référentiel d’identités centralisé pour l’authentification et l’autorisation

Bases de données SQL Azure peuvent être configuré toouse un des deux types d’authentification :

- **L’authentification SQL** utilise un nom d’utilisateur et un mot de passe. Lorsque vous avez créé un serveur logique de hello pour votre base de données, vous avez spécifié un compte de connexion « server admin » avec un nom d’utilisateur et un mot de passe. À l’aide de ces informations d’identification, vous pouvez authentifier tooany de base de données sur ce serveur en tant que propriétaire de base de données hello.

- **L’authentification Azure Active Directory** utilise des identités gérées par Azure Active Directory et est prise en charge pour les domaines gérés et intégrés. toouse authentification Azure Active Directory, vous devez créer un autre administrateur de serveur appelé hello « Azure AD admin », ce qui est autorisé de groupes et utilisateurs d’Azure AD tooadminister. Cet administrateur peut également effectuer toutes les opérations d’un administrateur de serveur ordinaire.

[L’authentification Active Directory Azure](../active-directory/develop/active-directory-authentication-scenarios.md) est un mécanisme de connexion tooAzure de la base de données SQL et SQL Data Warehouse à l’aide des identités dans Azure Active Directory (AD). Azure AD fournit une authentification de serveur alternatif tooSQL, vous pouvez arrêter la prolifération de hello des identités des utilisateurs sur les serveurs de base de données. Permet d’authentification Azure AD toocentrally vous gérer les identités de hello des utilisateurs de base de données et d’autres services de Microsoft dans un emplacement central. Gestion des ID fournit un emplacement unique aux utilisateurs de base de données de toomanage et simplifie la gestion de l’autorisation.  

Avantages de l’utilisation de l’authentification Azure AD au lieu de l’authentification SQL sont les suivants :

- Permet une rotation du mot de passe dans un emplacement unique.
- Gère des autorisations de base de données à l'aide de groupes Azure AD externes.
- Élimine le stockage des mots de passe en activant l’authentification Windows intégrée et d'autres formes d’authentification prises en charge par Azure AD.
- Base de données utilise contenus utilisateurs tooauthenticate des identités au niveau de base de données hello.
- Prend en charge l’authentification basée sur le jeton pour les applications qui se connectent tooSQL de base de données.
- Prend en charge ADFS (fédération de domaine) ou l’authentification utilisateur/mot de passe native pour un répertoire Azure AD local sans synchronisation du domaine.
- Prend en charge les connexions à partir de SQL Server Management Studio qui utilisent l’authentification universelle Active Directory, notamment [Multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md). MFA comprend une authentification forte avec une gamme d’options de vérification simples (appel téléphonique, SMS, cartes à puce avec code PIN ou notification d’application mobile). Pour plus d’informations, voir [Prise en charge de SSMS pour Azure AD MFA avec la base de données SQL et SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

toolearn en savoir plus sur l’authentification Azure AD, consultez :

- [Connexion tooSQL de base de données ou SQL données entrepôt par à l’aide d’authentification Azure Active Directory](../sql-database/sql-database-aad-authentication.md)
- [Authentification tooAzure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-authentication.md)
- [L’authentification basée sur le jeton prend en charge la base de données SQL Azure à l’aide de l’authentification Azure AD](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)

> [!NOTE]
> tooensure qu’Azure Active Directory est adapté à votre environnement, consultez [les fonctionnalités Azure AD et limitations](../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations), plus précisément hello considérations supplémentaires.
>
>

### <a name="restrict-access-based-on-ip-address"></a>Restreindre l’accès en fonction de l’adresse IP
Vous pouvez créer des règles de pare-feu qui spécifient des plages d’adresses IP acceptables. Ces règles peuvent être ciblés sur hello serveur et les niveaux de base de données. Nous recommandons d’utiliser des règles de pare-feu de niveau base de données chaque fois que possible tooenhance sécurité et toomake votre base de données plus portable. Il sont préférable d’utiliser les règles de pare-feu de niveau serveur pour les administrateurs et lorsque vous disposez de plusieurs bases de données qui ont hello même conditions d’accès, mais vous ne souhaitez pas temps toospend configuration individuellement de chaque base de données.

Les restrictions d'adresse IP source de SQL Database par défaut autorisent l’accès à partir de n’importe quelle adresse Azure (notamment d'autres abonnements et clients). Vous pouvez limiter cette tooonly permettent à votre instance de hello de tooaccess adresses IP. Même avec votre pare-feu SQL et les restrictions d’adresse IP, l’authentification forte est toujours nécessaire. Consultez les recommandations hello plus haut dans cet article.

toolearn en savoir plus sur le pare-feu SQL Azure et les restrictions IP, consultez :

- [Contrôle d’accès à Azure SQL Database](../sql-database/sql-database-control-access.md)
- [Configuration des règles de pare-feu de la base de données SQL Azure - Vue d’ensemble](../sql-database/sql-database-firewall-configure.md)
- [Configurer une règle de pare-feu de niveau serveur de base de données SQL Azure à l’aide de hello portail Azure](../sql-database/sql-database-configure-firewall-settings.md)

### <a name="encryption-of-data-at-rest"></a>Chiffrement des données au repos
L’option [Transparent Data Encryption (TDE)](https://msdn.microsoft.com/library/azure/bb934049) est activée par défaut. TDE chiffre de manière transparente les fichiers journaux et les données SQL Server, Azure SQL Database et Azure SQL Data Warehouse. Chiffrement transparent des données sont ainsi protégées contre des fichiers de toohello d’un accès direct ou de leur sauvegarde. Ainsi, vous tooencrypt des données au repos sans modifier les applications existantes. Chiffrement transparent des données doivent toujours rester activée ; Toutefois, cela n’empêchera pas un utilisateur malveillant à l’aide du chemin d’accès normal hello. Chiffrement transparent des données fournit toocomply de capacité hello avec nombreuses lois, réglementations et instructions établies dans différents secteurs professionnels.

Azure SQL gère les problèmes clés liés à TDE. Avec le chiffrement transparent des données, en local spécial soin tooensure récupérabilité et lors du déplacement de bases de données. Dans des scénarios plus sophistiqués, hello clés peuvent être explicitement gérées dans le coffre de clés Azure via la gestion de clés extensible (consultez [activer le chiffrement transparent des données sur SQL Server à l’aide de EKM](/security/encryption/enable-tde-on-sql-server-using-ekm)). Cela permet également d’utiliser la méthode BYOK (Bring Your Own Key) au moyen de la fonctionnalité Azure Key Vault BYOK.

Azure SQL fournit un chiffrement pour les colonnes par le biais d’[Always Encrypted](/sql/relational-databases/security/encryption/always-encrypted-database-engine). Cela permet l’accès seulement les applications autorisées toosensitive colonnes. À l’aide de ce type de chiffrement de limite de valeurs des colonnes chiffrées tooequality des requêtes SQL.

Le chiffrement au niveau de l’application doit également être utilisé pour des données sélectionnées. Problèmes de souveraineté de données peuvent parfois être atténués par chiffrement des données avec une clé qui est conservée dans le pays correct de hello. Cela empêche le transfert de données même accidentelle de provoquer un problème, car il est hello toodecrypt impossible des données sans clé hello, en supposant un algorithme fort sont utilisées (par exemple, AES 256).

Vous pouvez utiliser la base de données sécurisée hello de toohelp précautions supplémentaires telles que la conception d’un système sécurisé, chiffrer les ressources confidentielles et créer un pare-feu autour des serveurs de base de données hello.

## <a name="next-steps"></a>Étapes suivantes
Cet article a introduit vous tooa collection de base de données SQL et SQL Data Warehouse meilleures pratiques de sécurité pour sécuriser votre PaaS applications web et mobiles. toolearn savoir plus sur la sécurisation de vos déploiements PaaS, consultez :

- [Sécurisation des déploiements PaaS](security-paas-deployments.md)
- [Sécurisation des applications mobiles et web PaaS à l’aide d’Azure App Services](security-paas-applications-using-app-services.md)
