---
title: "vue d’ensemble du développement d’Application de base de données d’aaaSQL | Documents Microsoft"
description: "En savoir plus sur les bibliothèques de connectivité disponible et les meilleures pratiques pour les applications qui se connectent tooSQL de base de données."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 17f04db600828f90c42c750c9abdb92cfa4ca817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-application-development-overview"></a>Vue d’ensemble du développement de base de données SQL
Cet article explique les considérations de base hello dont un développeur doit être conscient lors de l’écriture de code tooconnect tooAzure base de données SQL.

> [!TIP]
> Pour un didacticiel montrant comment toocreate un serveur, créer un pare-feu basé sur le serveur, afficher les propriétés de serveur, connectez-vous à l’aide de SQL Server Management Studio, la base de données master de requête hello, créer une base de données et une base de données vide, interroger les propriétés de la base de données, connexion à l’aide de SQL Server Management Studio et la base de données exemple de requête hello, consultez [didacticiel obtenir](sql-database-get-started-portal.md).
>

## <a name="language-and-platform"></a>Langage et plateforme
Plusieurs exemples de code sont à votre disposition pour divers langages et plateformes de programmation. Vous trouverez des exemples de code des liens toohello à : 

* Pour en savoir plus, voir [Bibliothèques de connexions pour SQL Database et SQL Server](sql-database-libraries.md)

## <a name="tools"></a>Outils 
Vous pouvez tirer parti des outils open source comme [cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli) et [VS Code](https://code.visualstudio.com/). En outre, Azure SQL Database fonctionne avec des outils Microsoft, tels que [Visual Studio](https://www.visualstudio.com/downloads/) et [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).  Vous pouvez également utiliser hello portail de gestion Azure PowerShell, et vous aider au moment de l’API REST gagnez en productivité supplémentaire.

## <a name="resource-limitations"></a>Limitations des ressources
Base de données SQL Azure gère la base de données de hello ressources tooa disponible à l’aide de deux mécanismes différents : gouvernance de ressources et de l’application de limites.

* Pour en savoir plus, voir [Limites de ressources de base de données SQL Azure](sql-database-resource-limits.md)

## <a name="security"></a>Sécurité
La base de données SQL Azure fournit des ressources permettant de limiter l’accès, de protéger les données et de surveiller les activités sur une base de données SQL.

* Pour en savoir plus, voir [Sécurisation de votre base de données SQL](sql-database-security-overview.md)

## <a name="authentication"></a>Authentification
* La base de données SQL Azure prend en charge les utilisateurs et les connexions de l’authentification SQL Server, ainsi que les utilisateurs et les connexions de [l’authentification Azure Active Directory](sql-database-aad-authentication.md) .
* Vous devez toospecify une base de données, au lieu des valeurs par défaut toohello *master* base de données.
* Vous ne pouvez pas utiliser hello Transact-SQL **myDatabaseName d’utilisation ;** instruction sur la base de données de base de données SQL tooswitch tooanother.
* Pour en savoir plus, consultez [Sécurité SQL Database : gérer la sécurité d’accès et de connexion aux bases de données](sql-database-manage-logins.md)

## <a name="resiliency"></a>Résilience
Lorsqu’une erreur temporaire se produit lors de la connexion tooSQL de base de données, votre code doit réessayer d’appel de hello.  Nous recommandons que la logique de nouvelle tentative utiliser la logique d’interruption, afin qu’il ne surchargent pas hello de base de données SQL avec une nouvelle tentative simultanée de plusieurs clients.

* Exemples de code : pour les exemples de code qui illustrent la logique de nouvelle tentative, consultez les exemples pour la langue hello de votre choix à : [bibliothèques de connexions de base de données SQL et SQL Server](sql-database-libraries.md)
* Pour en savoir plus, consultez [Messages d’erreur pour les programmes clients SQL Database](sql-database-develop-error-messages.md)

## <a name="managing-connections"></a>Gestion des connexions
* Dans la logique de connexion client, substituez hello par défaut du délai d’attente toobe 30 secondes.  valeur par défaut de Hello de 15 secondes est trop courte pour les connexions qui dépendent de hello internet.
* Si vous utilisez un [pool de connexions](http://msdn.microsoft.com/library/8xx3tyca.aspx), hello de connexion que tooclose hello instantanée votre programme n’utilise pas activement il et prépare tooreuse pas il.

## <a name="network-considerations"></a>Remarques relatives au réseau
* Vérifiez le pare-feu hello permet les communications TCP sortantes sur le port 1433 sur ordinateur hello qui héberge votre programme client.  Pour en savoir plus, consultez [Configurer un pare-feu sur une base de données SQL Azure à l’aide du portail Azure](sql-database-configure-firewall-settings.md)
* Si votre programme client connecte tooSQL de base de données pendant l’exécution de votre client sur une machine virtuelle Azure (VM), vous devez ouvrir certaines plages de ports sur hello machine virtuelle. Pour en savoir plus, consultez [Ports au-delà de 1433 pour ADO.NET 4.5 et SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md)
* TooAzure de connexions de client de base de données SQL parfois ignorer hello proxy et interagir directement avec la base de données hello. Les ports autres que le port 1433 deviennent importants. Pour plus d’informations, consultez [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md) (Architecture de connectivité d’Azure SQL Database) et [Ports au-delà de 1433 pour ADO.NET 4.5 et SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="data-sharding-with-elastic-scale"></a>Partitionnement de données avec mise à l’échelle élastique
Élastique simplifie hello montée (en charge). 

* [Modèles de conception pour les applications SaaS mutualisées avec Base de données SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md)
* [Prise en main de l'infrastructure élastique d’Azure SQL Database (version préliminaire)](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a>Étapes suivantes
Explorer tous les hello [fonctionnalités de base de données SQL](sql-database-technical-overview.md)
