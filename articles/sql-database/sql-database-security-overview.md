---
title: "Vue d’ensemble de la sécurité d’Azure SQL Database | Microsoft Docs"
description: "Découvrez les aspects liés à la sécurité d’Azure SQL Database et de SQL Server, notamment les différences entre le cloud et SQL Server en local."
services: sql-database
documentationcenter: 
author: tmullaney
manager: jhubbard
editor: 
ms.assetid: a012bb85-7fb4-4fde-a2fc-cf426c0a56bb
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: On Demand
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 14a7fdb304e90aec10bee9167817f564870cd6c1
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="securing-your-sql-database"></a>Sécurisation de votre base de données SQL

Cet article présente les principes de la sécurisation de la couche Données d’une application à l’aide de la base de données SQL Microsoft Azure. Plus spécifiquement, cet article vous offre un aperçu sur les ressources dédiées à la protection des données, au contrôle d’accès et à la surveillance proactive. 

Pour obtenir une présentation complète des fonctionnalités de sécurité disponibles sur toutes les versions de SQL, consultez la section [Sécurité et protection (moteur de base de données)](https://msdn.microsoft.com/library/bb510589). Des informations supplémentaires sont également disponibles dans le [livre blanc technique sur la sécurité et la base de données SQL Azure](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf) (PDF).

## <a name="protect-data"></a>Protéger les données
SQL Database protège vos données grâce au chiffrement : il utilise [Transport Layer Security](https://support.microsoft.com/kb/3135244) pour les données en mouvement, [Transparent Data Encryption](/sql/relational-databases/security/encryption/transparent-data-encryption-azure-sql) pour les données au repos et [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) pour les données en cours d’utilisation. 

> [!IMPORTANT]
>Toutes les connexions à la base de données SQL Microsoft Azure doivent être chiffrées à tout moment (via SSL/TLS) lorsque les données sont « en transit » depuis et vers la base de données. Dans la chaîne de connexion de votre application, vous devez spécifier des paramètres permettant de chiffrer la connexion et *non* d’approuver le certificat de serveur (le système effectue cette opération pour vous lorsque vous copiez la chaîne de connexion hors du portail Azure). Dans le cas contraire, la connexion ne vérifie pas l’identité du serveur et peut être la cible d’attaques de type MITM (« Man-In-The-Middle »). Pour le pilote ADO.NET, par exemple, ces paramètres de chaîne de connexion sont les suivants : **Encrypt=True** et **TrustServerCertificate=False**. 

Vous pouvez également utiliser les méthodes de chiffrement des données suivantes :

* [chiffrement au niveau des cellules](https://msdn.microsoft.com/library/ms179331.aspx) permet de chiffrer des colonnes spécifiques, voire des cellules de données, avec des clés de chiffrement différentes.
* S’il vous faut un module de sécurité matériel ou si vous devez gérer la hiérarchie des clés de chiffrement de manière centralisée, consultez l’article de blog relatif au [coffre de clés Microsoft Azure avec SQL Server dans une machine virtuelle Azure](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

## <a name="control-access"></a>Contrôler l’accès
SQL Database protège vos données en limitant l’accès à votre base de données via des règles de pare-feu, des mécanismes d’authentification demandant aux utilisateurs de prouver leur identité, une autorisation pour accéder aux données en fonction des droits et des appartenances associés à un rôle, ainsi qu’à l’aide de la sécurité au niveau des lignes et du masquage de données dynamiques. Pour une description de l’utilisation des fonctionnalités de contrôle d’accès dans SQL Database, consultez [Azure SQL Database access control (Contrôle d’accès d’Azure SQL Database)](sql-database-control-access.md).

> [!IMPORTANT]
> La gestion des bases de données et des serveurs logiques dans Azure est contrôlée par les attributions de rôle de votre compte d’utilisateur du portail. Pour en savoir plus à ce sujet, voir [Contrôle d’accès en fonction du rôle dans le portail Azure](../active-directory/role-based-access-control-what-is.md).
>

### <a name="firewall-and-firewall-rules"></a>Pare-feu et règles de pare-feu
Pour aider à protéger vos données, les pare-feu empêchent tout accès à votre serveur de base de données jusqu’à ce que vous spécifiiez les ordinateurs qui disposent d’autorisations grâce aux [règles de pare-feu](sql-database-firewall-configure.md). Le pare-feu octroie l’accès à la base de données en fonction de l’adresse IP d’origine de chaque demande.

### <a name="authentication"></a>Authentification
L’authentification de base de données SQL fait référence au processus de validation de votre identité lorsque vous vous connectez à la base de données. Une base de données SQL prend en charge deux types d’authentification :

* **L’authentification SQL**, qui utilise un nom d’utilisateur et un mot de passe. Lorsque vous avez créé un serveur logique pour votre base de données, vous avez spécifié un compte de connexion « Admin serveur », associé à un nom d’utilisateur et à un mot de passe. À l’aide de ces informations d’identification, vous pouvez vous authentifier auprès de n’importe quelle base de données sur ce serveur, en tant que propriétaire de la base de données, ou « dbo ». 
* **L’authentification Azure Active Directory**, qui utilise des identités gérées par Azure Active Directory et qui est prise en charge pour les domaines gérés et intégrés. Utilisez l’authentification Active Directory (sécurité intégrée) [dans la mesure du possible](https://msdn.microsoft.com/library/ms144284.aspx). Si vous souhaitez utiliser l’authentification Azure Active Directory, vous devez créer un autre administrateur de serveur appelé « administrateur Azure AD », autorisé à gérer les groupes et utilisateurs Active Directory Azure. Cet administrateur peut également effectuer toutes les opérations d’un administrateur de serveur ordinaire. Pour une procédure pas à pas relative à la création d’un administrateur Azure AD pour activer l’authentification Azure Active Directory, consultez [Connexion à la base de données SQL avec l’authentification Azure Active Directory](sql-database-aad-authentication.md) .

### <a name="authorization"></a>Autorisation
Le terme « autorisation » fait référence aux actions qu’un utilisateur peut exécuter dans une base de données Azure SQL Database et qui sont contrôlées par les rôles détenus et les autorisations sur les objets. Nous vous recommandons, à titre de meilleure pratique, d’accorder aux utilisateurs des privilèges aussi réduits que possible. Le compte d’administrateur du serveur avec lequel vous vous connectez appartient au groupe « db_owner », qui est autorisé à effectuer tout type d’opérations dans la base de données. Enregistrez ce compte pour l’utiliser lors du déploiement des mises à niveau de schéma et d’autres opérations de gestion. Utilisez le compte « ApplicationUser », doté d’autorisations plus limitées, pour vous connecter à la base de données à partir de votre application, en bénéficiant du niveau de privilèges le moins élevé requis par cette dernière.

### <a name="row-level-security"></a>Sécurité au niveau des lignes
La sécurité au niveau des lignes permet aux clients de contrôler l’accès aux lignes d’une table de base de données en fonction des caractéristiques de l’utilisateur qui exécute une requête (par exemple, appartenance à un groupe ou contexte d’exécution). Pour plus d’informations, consultez [Sécurité au niveau des lignes](https://msdn.microsoft.com/library/dn765131).

### <a name="data-masking"></a>Masquage de données 
Le masquage des données dynamiques de base de données SQL limite l’exposition des données sensibles en les masquant aux utilisateurs sans privilège. Le masquage de données dynamiques détecte automatiquement les données potentiellement sensibles dans Azure SQL Database et fournit des recommandations pouvant donner lieu à une action permettant de masquer ces champs, avec un impact minimal sur la couche d’application. Il dissimule les données sensibles dans le jeu de résultats d’une requête dans les champs de la base de données désignés. Les données de la base de données ne sont pas modifiées. Pour plus d’informations, consultez [Masquage de données dynamiques dans une base de données SQL](sql-database-dynamic-data-masking-get-started.md) et découvrez comment le masquage de données dynamiques permet de limiter l’exposition des données sensibles.

## <a name="proactive-monitoring"></a>Surveillance proactive
SQL Database protège vos données en fournissant des fonctionnalités d’audit et de détection des menaces. 

### <a name="auditing"></a>Audit
L’audit SQL Database suit les activités de base de données et vous aide à maintenir la conformité réglementaire en enregistrant les événements de base de données dans un journal d’audit de votre compte de stockage Azure. L’audit vous permet de comprendre les activités de base de données en cours, d’analyser et d’examiner l’historique des activités pour identifier les menaces potentielles ou les violations de sécurité et abus présumés. Pour en savoir plus, consultez [Prise en main de l’audit SQL Database](sql-database-auditing.md).  

### <a name="threat-detection"></a>Détection de menaces
La fonctionnalité de détection des menaces complète celle d’audit en fournissant une couche supplémentaire d’informations de sécurité intégrée au service Azure SQL Database, lequel vise à détecter les tentatives inhabituelles ou potentiellement dangereuses d’accès à des bases de données ou d’exploitation des failles de sécurité de celles-ci. Vous êtes alerté en cas d’activités suspectes, de vulnérabilités potentielles, d’attaques par injection de code SQL et de modèles d’accès anormaux à la base de données. Les alertes Threat Detection peuvent être consultées à partir d’[Azure Security Center](https://azure.microsoft.com/services/security-center/). Elles fournissent des détails sur les activités suspectes et recommandent l’action à entreprendre pour analyser et prévenir la menace. La fonctionnalité Threat Detection coûte 15 USD/serveur/mois. Elle sera gratuite les 60 premiers jours. Pour en savoir plus, consultez [Prise en main de Threat Detection pour la base de données SQL](sql-database-threat-detection.md).
 
### <a name="data-masking"></a>Masquage de données 
Le masquage des données dynamiques de base de données SQL limite l’exposition des données sensibles en les masquant aux utilisateurs sans privilège. Le masquage de données dynamiques détecte automatiquement les données potentiellement sensibles dans Azure SQL Database et fournit des recommandations pouvant donner lieu à une action permettant de masquer ces champs, avec un impact minimal sur la couche d’application. Il dissimule les données sensibles dans le jeu de résultats d’une requête dans les champs de la base de données désignés. Les données de la base de données ne sont pas modifiées. Pour en savoir plus, consultez [Masquage de données dynamiques dans une base de données SQL](sql-database-dynamic-data-masking-get-started.md).
 
## <a name="compliance"></a>Conformité
Non seulement Azure SQL Database propose les fonctions ci-dessus et des fonctionnalités permettant à votre application de répondre à différentes exigences en matière de sécurité, mais il participe également à des audits réguliers et est certifié conforme à de nombreuses normes actuelles. Pour en savoir plus, accédez au [Centre de confidentialité Microsoft Azure](https://azure.microsoft.com/support/trust-center/), qui inclut la liste la plus à jour des [certifications de conformité de la base de données SQL](https://azure.microsoft.com/support/trust-center/services/).

## <a name="next-steps"></a>Étapes suivantes

- Pour une description de l’utilisation des fonctionnalités de contrôle d’accès dans SQL Database, consultez [Azure SQL Database access control (Contrôle d’accès d’Azure SQL Database)](sql-database-control-access.md).
- Pour une présentation de l’audit de base de données, consultez [Audit de base de données SQL](sql-database-auditing.md).
- Pour une description de la détection des menaces, consultez [Détection de menaces pour les bases de données SQL](sql-database-threat-detection.md).
