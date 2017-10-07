---
title: "aaaGranting accès tooAzure base de données SQL | Documents Microsoft"
description: "En savoir plus sur l’octroi d’accès tooMicrosoft base de données SQL Azure."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 8e71b04c-bc38-4153-8f83-f2b14faa31d9
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/06/2017
ms.author: rickbyh
ms.openlocfilehash: 4c32fafa7e98b731ff2f9bf4666da7e4a3145286
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-access-control"></a>Contrôle d’accès à Azure SQL Database
sécurité tooprovide, base de données SQL contrôle l’accès avec les règles de pare-feu limitant la connectivité par adresse IP, les mécanismes d’authentification nécessitant des utilisateurs tooprove leur identité et les mécanismes d’autorisation limitant les actions de toospecific les utilisateurs et les données. 

> [!IMPORTANT]
> Pour une vue d’ensemble des fonctionnalités de sécurité de base de données SQL hello, consultez [vue d’ensemble de la sécurité SQL](sql-database-security-overview.md). Pour obtenir un didacticiel, consultez [Sécuriser votre base de données Azure SQL Database](sql-database-security-tutorial.md).

## <a name="firewall-and-firewall-rules"></a>Pare-feu et règles de pare-feu
Microsoft Azure SQL Database fournit un service de base de données relationnelle pour Azure et d’autres applications basées sur Internet. toohelp protéger vos données, les pare-feu empêchent le serveur de base de données de tous les accès tooyour jusqu'à ce que vous spécifiez les ordinateurs sur lesquels l’autorisation. les pare-feu Hello accorde toodatabases d’accès basé sur hello adresse IP de chaque demande d’origine. Pour en savoir plus, consultez [Vue d’ensemble des règles de pare-feu d’Azure SQL Database](sql-database-firewall-configure.md).

Hello service de base de données SQL Azure est disponible uniquement via le port TCP 1433. tooaccess une base de données SQL à partir de votre ordinateur, vérifiez que le pare-feu de votre ordinateur client autorise les communications TCP sortantes sur le port TCP 1433. Si elles ne sont pas nécessaire pour les autres applications, bloquez les connexions entrantes sur le port TCP 1433. 

Dans le cadre du processus de connexion hello, connexions à partir de machines virtuelles sont des adresses IP différentes tooa redirigé et port unique pour chaque rôle de travail. numéro de port Hello est comprise de hello too11999 11000. Pour plus d’informations sur les ports TCP, consultez [Ports au-delà de 1433 pour ADO.NET 4.5 et SQL Database2](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="authentication"></a>Authentification

Une base de données SQL prend en charge deux types d’authentification :

* **L’authentification SQL**, qui utilise un nom d’utilisateur et un mot de passe. Lorsque vous avez créé un serveur logique de hello pour votre base de données, vous avez spécifié un compte de connexion « server admin » avec un nom d’utilisateur et un mot de passe. À l’aide de ces informations d’identification, vous pouvez vous authentifier tooany de base de données sur ce serveur en tant que propriétaire de base de données hello ou « dbo ». 
* **L’authentification Azure Active Directory**, qui utilise des identités gérées par Azure Active Directory et qui est prise en charge pour les domaines gérés et intégrés. Utilisez l’authentification Active Directory (sécurité intégrée) [dans la mesure du possible](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode). Si vous souhaitez toouse authentification Azure Active Directory, vous devez créer un autre administrateur de serveur appelé hello « Azure AD admin », ce qui est autorisé de groupes et utilisateurs d’Azure AD tooadminister. Cet administrateur peut également effectuer toutes les opérations d’un administrateur de serveur ordinaire. Consultez [connexion tooSQL de base de données en utilisant authentification Azure Active Directory](sql-database-aad-authentication.md) pour une procédure pas à pas toocreate un tooenable d’administrateur Azure AD authentification Azure Active Directory.

Hello du moteur de base de données ferme les connexions qui restent inactives pendant plus de 30 minutes. Hello connexion doit à nouveau de connexion avant de pouvoir être utilisé. En continu les connexions actives tooSQL de base de données nécessitent une nouvelle autorisation (opération effectuée par le moteur de base de données hello) au moins toutes les 10 heures. moteur de base de données Hello tente de renouvellement d’autorisation à l’aide de mot de passe soumis hello et aucune entrée utilisateur n’est requise. Pour des raisons de performances, lorsqu’un mot de passe est réinitialisé dans la base de données SQL, hello connexion n’est pas être authentifiés, même si la connexion de hello est réinitialisée en raison de tooconnection le regroupement. Ce comportement est différent de hello de local SQL Server. Si le mot de passe hello a été modifié depuis hello connexion a été initialement autorisée, connexion de hello doit se terminer et établir une nouvelle connexion à l’aide du nouveau mot de passe hello. Un utilisateur avec hello `KILL DATABASE CONNECTION` autorisation peut terminer explicitement une tooSQL de connexion de base de données à l’aide de hello [KILL](https://docs.microsoft.com/sql/t-sql/language-elements/kill-transact-sql) commande.

Comptes d’utilisateur peuvent être créées dans la base de données master hello et peuvent avoir des autorisations dans toutes les bases de données sur le serveur de hello, ou ils peuvent être créés dans la base de données hello lui-même (appelé utilisateurs contenus). Pour plus d’informations sur la création et la gestion des connexions, consultez [Gérer les connexions](sql-database-manage-logins.md). tooenhance portabilité et expansion, utilisez l’extensibilité de relation contenant-contenu de la base de données utilisateurs tooenhance. Pour plus d’informations sur les utilisateurs à relation contenant-contenu, consultez [Utilisateurs de base de données à relation contenant-contenu - Rendre votre base de données portable](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), [CREATE USER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-user-transact-sql) et [Bases de données à relation contenant-contenu](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases).

Comme meilleure pratique votre application doit utiliser un tooauthenticate compte dédié, cette façon, vous pouvez limiter les autorisations hello toohello application et réduire les risques de hello d’activités malveillantes au cas où votre code d’application est vulnérable tooa d’injection SQL attaque. Hello recommandé consiste toocreate un [utilisateur de base de données](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), qui permet à votre application tooauthenticate toohello directement la base de données. 

## <a name="authorization"></a>Autorisation

Autorisation fait référence toowhat un utilisateur peut faire au sein d’une base de données SQL Azure, et cela est contrôlé par la base de données de votre compte utilisateur [appartenances au rôle](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) et [autorisations au niveau de l’objet](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine). Comme meilleure pratique, vous devriez hello d’utilisateurs des privilèges minimaux nécessaires. compte d’administrateur de serveur Hello que vous connectez à l’aide est un membre de db_owner ayant autorité toodo quoi que ce soit dans la base de données hello. Enregistrez ce compte pour l’utiliser lors du déploiement des mises à niveau de schéma et d’autres opérations de gestion. Utiliser le compte de « ApplicationUser » de hello avec tooconnect d’autorisations plus limitée à partir de votre base de données application toohello avec hello des privilèges minimaux requis par votre application. Pour plus d’informations, consultez [Gérer les connexions](sql-database-manage-logins.md).

En général, seuls les administrateurs doivent accéder toohello `master` base de données. Routine tooeach utilisateur base de données access doit être par les utilisateurs non administrateurs de base de données contenus dans chaque base de données. Lorsque vous utilisez les utilisateurs de base de données, vous n’avez pas besoin de connexions toocreate Bonjour `master` base de données. Pour plus d’informations, voir [Utilisateurs de base de données à relation contenant-contenu - Rendre votre base de données portable](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable).

Vous devez vous familiariser avec hello suivant les fonctionnalités qui peuvent être utilisé toolimit ou élever des autorisations :   
* [L’emprunt d’identité](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server) et [signature de module](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/signing-stored-procedures-in-sql-server) peut être utilisé toosecurely élever les autorisations temporairement.
* [sécurité au niveau des lignes](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) peut être utilisée pour limiter le nombres de lignes accessibles par l’utilisateur.
* [Le masquage des données](sql-database-dynamic-data-masking-get-started.md) peut être exposition toolimit utilisé des données sensibles.
* [Procédures stockées](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) peut être utilisé toolimit actions hello qui peuvent être effectuées sur la base de données hello.

## <a name="next-steps"></a>Étapes suivantes

- Pour une vue d’ensemble des fonctionnalités de sécurité de base de données SQL hello, consultez [vue d’ensemble de la sécurité SQL](sql-database-security-overview.md).
- toolearn en savoir plus sur les règles de pare-feu, consultez [des règles de pare-feu](sql-database-firewall-configure.md).
- toolearn sur les utilisateurs et les connexions, consultez [gérer des connexions](sql-database-manage-logins.md). 
- Pour une discussion sur la surveillance proactive, consultez [Audit de base de données](sql-database-auditing.md) et [Détection des menaces pour SQL Database](sql-database-threat-detection.md).
- Pour obtenir un didacticiel, consultez [Sécuriser votre base de données Azure SQL Database](sql-database-security-tutorial.md).
