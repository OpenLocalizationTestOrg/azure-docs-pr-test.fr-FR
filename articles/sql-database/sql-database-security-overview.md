---
title: "Présentation de la sécurité de base de données SQL d’aaaAzure | Documents Microsoft"
description: "En savoir plus sur la sécurité de base de données SQL Azure et SQL Server, y compris des différences de hello entre le cloud de hello et SQL Server sur site lorsqu’il s’agit de tooauthentication, d’autorisation, la sécurité de connexion, le chiffrement et la conformité."
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
ms.workload: data-management
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 7b0b0d1b59ec4018d9fb668bc8b6b56c9907e982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-your-sql-database"></a>Sécurisation de votre base de données SQL

Cet article explique les concepts de base hello de la sécurisation de couche de données hello d’une application à l’aide de la base de données SQL Azure. Plus spécifiquement, cet article vous offre un aperçu sur les ressources dédiées à la protection des données, au contrôle d’accès et à la surveillance proactive. 

Pour une vue d’ensemble complète des fonctionnalités de sécurité disponibles sur toutes les versions de SQL, consultez hello [centre de sécurité pour le moteur de base de données SQL Server et la base de données SQL Azure](https://msdn.microsoft.com/library/bb510589). Informations supplémentaires sont également disponibles dans hello [sécurité et la base de données SQL Azure Livre blanc technique](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf) (PDF).

## <a name="protect-data"></a>Protection des données
SQL Database protège vos données grâce au chiffrement : il utilise [Transport Layer Security](https://support.microsoft.com/kb/3135244) pour les données en mouvement, [Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242) pour les données au repos et [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) pour les données en cours d’utilisation. 

> [!IMPORTANT]
>Toutes les connexions tooAzure base de données SQL exiger le chiffrement (SSL/TLS) à toutes les heures pendant tooand « en transit » à partir de la base de données hello des données. Dans la chaîne de connexion de votre application, vous devez spécifier la connexion de paramètres tooencrypt hello et *pas* tootrust hello certificat de serveur (cela est fait pour vous si vous copiez votre chaîne de connexion de hello portail classique Azure) Sinon, connexion de hello ne vérifie pas l’identité hello du serveur de hello et est susceptibles d’être trop « man-in-the-middle » attaques. Pour le pilote ADO.NET hello, par exemple, ces paramètres de chaîne de connexion sont **Encrypt = True** et **TrustServerCertificate = False**. 

Pour les autres façons tooencrypt vos données, envisagez de :

* [Le chiffrement au niveau des cellules](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt des colonnes spécifiques ou même les cellules de données avec des clés de chiffrement différente.
* S’il vous faut un module de sécurité matériel ou si vous devez gérer la hiérarchie des clés de chiffrement de manière centralisée, consultez l’article de blog relatif au [coffre de clés Microsoft Azure avec SQL Server dans une machine virtuelle Azure](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

## <a name="control-access"></a>Contrôler l’accès
Base de données SQL protège vos données en limitant la base de données access tooyour à l’aide de règles de pare-feu, nécessitant des utilisateurs tooprove leur identité et autorisation toodata via les autorisations et les appartenances de rôle, ainsi que par le biais des mécanismes d’authentification sécurité de niveau ligne et masquage dynamique des données. Pour une présentation de l’utilisation de hello de fonctionnalités de contrôle d’accès dans la base de données SQL, consultez [contrôler l’accès](sql-database-control-access.md).

> [!IMPORTANT]
> La gestion des bases de données et des serveurs logiques dans Azure est contrôlée par les attributions de rôle de votre compte d’utilisateur du portail. Pour en savoir plus à ce sujet, voir [Contrôle d’accès en fonction du rôle dans le portail Azure](../active-directory/role-based-access-control-what-is.md).
>

### <a name="firewall-and-firewall-rules"></a>Pare-feu et règles de pare-feu
toohelp protéger vos données, les pare-feu empêchent le serveur de base de données de tous les accès tooyour jusqu'à ce que vous spécifiiez les ordinateurs à l’aide de l’autorisation [des règles de pare-feu](sql-database-firewall-configure.md). les pare-feu Hello accorde toodatabases d’accès basé sur hello adresse IP de chaque demande d’origine.

### <a name="authentication"></a>Authentification
L’authentification de base de données SQL fait référence à toohow vous prouver votre identité lors de la connexion de base de données toohello. Une base de données SQL prend en charge deux types d’authentification :

* **L’authentification SQL**, qui utilise un nom d’utilisateur et un mot de passe. Lorsque vous avez créé un serveur logique de hello pour votre base de données, vous avez spécifié un compte de connexion « server admin » avec un nom d’utilisateur et un mot de passe. À l’aide de ces informations d’identification, vous pouvez vous authentifier tooany de base de données sur ce serveur en tant que propriétaire de base de données hello ou « dbo ». 
* **L’authentification Azure Active Directory**, qui utilise des identités gérées par Azure Active Directory et qui est prise en charge pour les domaines gérés et intégrés. Utilisez l’authentification Active Directory (sécurité intégrée) [dans la mesure du possible](https://msdn.microsoft.com/library/ms144284.aspx). Si vous souhaitez toouse authentification Azure Active Directory, vous devez créer un autre administrateur de serveur appelé hello « Azure AD admin », ce qui est autorisé de groupes et utilisateurs d’Azure AD tooadminister. Cet administrateur peut également effectuer toutes les opérations d’un administrateur de serveur ordinaire. Consultez [connexion tooSQL de base de données en utilisant authentification Azure Active Directory](sql-database-aad-authentication.md) pour une procédure pas à pas toocreate un tooenable d’administrateur Azure AD authentification Azure Active Directory.

### <a name="authorization"></a>Autorisation
Autorisation fait référence toowhat un utilisateur peut faire au sein d’une base de données SQL Azure, et cela est contrôlé par les appartenances aux rôles de base de données de votre compte d’utilisateur et au niveau de l’objet des autorisations. Comme meilleure pratique, vous devriez hello d’utilisateurs des privilèges minimaux nécessaires. compte d’administrateur de serveur Hello que vous connectez à l’aide est un membre de db_owner ayant autorité toodo quoi que ce soit dans la base de données hello. Enregistrez ce compte pour l’utiliser lors du déploiement des mises à niveau de schéma et d’autres opérations de gestion. Utiliser le compte de « ApplicationUser » de hello avec tooconnect d’autorisations plus limitée à partir de votre base de données application toohello avec hello des privilèges minimaux requis par votre application.

### <a name="row-level-security"></a>Sécurité au niveau des lignes
La sécurité au niveau des lignes permet de clients toocontrol accès toorows dans une table de base de données en fonction des caractéristiques de hello d’utilisateur hello l’exécution d’une requête (par exemple, groupe d’appartenance ou contexte d’exécution). Pour plus d’informations, consultez [Sécurité au niveau des lignes](https://msdn.microsoft.com/library/dn765131).

### <a name="data-masking"></a>Masquage de données 
Masquage dynamique des données de base de données SQL limite l’exposition des données sensibles en les masquant aux utilisateurs privilèges toonon. Automatiquement de masquage dynamique des données permet de détecter des données potentiellement sensibles dans la base de données SQL Azure et fournit des conseils toomask ces champs, avec un impact minimal sur la couche d’application hello. Elle établit un masquage des données sensibles hello hello jeu de résultats d’une requête sur des champs de base de données désignée données hello hello de base de données ne sont pas modifiées. Pour plus d’informations, consultez [prise en main de la base de données SQL masquage dynamique des données](sql-database-dynamic-data-masking-get-started.md) peut être exposition toolimit utilisé des données sensibles.

## <a name="proactive-monitoring"></a>Surveillance proactive
SQL Database protège vos données en fournissant des fonctionnalités d’audit et de détection des menaces. 

### <a name="auditing"></a>Audit
L’audit de base de données SQL effectue le suivi des activités de la base de données et vous permet de toomaintain réglementaires, en enregistrant le journal d’audit de base de données événements tooan dans votre compte de stockage Azure. L’audit vous permet de toounderstand les activités en cours de la base de données, ainsi qu’analyser et examiner les menaces potentielles de tooidentify historique des activités ou violation présumée des abus et la sécurité. Pour en savoir plus, consultez [Prise en main de l’audit SQL Database](sql-database-auditing.md).  

### <a name="threat-detection"></a>Détection de menaces
La détection des menaces complète de l’audit, en fournissant une couche supplémentaire de l’intelligence de sécurité intégrée à un service de base de données SQL Azure hello qui détecte les tentatives inhabituel et potentiellement dangereux tooaccess ou exploitant une faille de bases de données. Vous êtes alerté en cas d’activités suspectes, de vulnérabilités potentielles, d’attaques par injection de code SQL et de modèles d’accès anormaux à la base de données. Alertes de détection de menaces peuvent être consultés dans [Azure Security Center](https://azure.microsoft.com/services/security-center/) et fournir des détails d’activité suspecte et recommandent la mesure sur la façon de tooinvestigate et d’atténuer les menaces de hello. La fonctionnalité Threat Detection coûte 15 USD/serveur/mois. Il sera disponible pour hello 60 premiers jours. Pour en savoir plus, consultez [Prise en main de Threat Detection pour la base de données SQL](sql-database-threat-detection.md).
 
### <a name="data-masking"></a>Masquage de données 
Masquage dynamique des données de base de données SQL limite l’exposition des données sensibles en les masquant aux utilisateurs privilèges toonon. Automatiquement de masquage dynamique des données permet de détecter des données potentiellement sensibles dans la base de données SQL Azure et fournit des conseils toomask ces champs, avec un impact minimal sur la couche d’application hello. Elle établit un masquage des données sensibles hello hello jeu de résultats d’une requête sur des champs de base de données désignée données hello hello de base de données ne sont pas modifiées. Pour en savoir plus, consultez [Masquage de données dynamiques dans une base de données SQL](sql-database-dynamic-data-masking-get-started.md).
 
## <a name="compliance"></a>Conformité
En outre toohello au-dessus de fonctions et fonctionnalités qui permettent à votre application de répondre aux exigences de sécurité différentes, base de données SQL Azure également participe à des audits réguliers et ont été certifié par rapport à un nombre de normes de conformité. Pour plus d’informations, consultez hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/), où vous trouverez la liste la plus récente de hello [les certifications de conformité de la base de données SQL](https://azure.microsoft.com/support/trust-center/services/).

## <a name="next-steps"></a>Étapes suivantes

- Pour une présentation de l’utilisation de hello de fonctionnalités de contrôle d’accès dans la base de données SQL, consultez [contrôler l’accès](sql-database-control-access.md).
- Pour une présentation de l’audit de base de données, consultez [Audit de base de données SQL](sql-database-auditing.md).
- Pour une description de la détection des menaces, consultez [Détection de menaces pour les bases de données SQL](sql-database-threat-detection.md).
