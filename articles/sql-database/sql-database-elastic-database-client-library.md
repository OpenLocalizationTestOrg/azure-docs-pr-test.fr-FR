---
title: "bases de données cloud évolutives aaaBuilding | Documents Microsoft"
description: "Créer des applications de base de données évolutives .NET avec la bibliothèque cliente de base de données élastique hello"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 1f11c52d-13c1-4994-b9b1-5b1ae2f9255f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: ca34eff2078c0700dee1bc587f264bbfca979eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="building-scalable-cloud-databases"></a>Conception de bases de données cloud évolutives
La montée en charge des bases de données peut être aisément accomplie à l’aide de fonctionnalités et d’outils évolutifs de bases de données SQL Azure. En particulier, vous pouvez utiliser hello **bibliothèque cliente de base de données élastique** toocreate et gérer des bases de données à grande échelle. Cette fonctionnalité vous permet de développer facilement des applications partitionnées à l'aide de centaines, voire de milliers, de bases de données SQL Azure. [Travaux élastique](sql-database-elastic-jobs-powershell.md) peut ensuite être utilisé toohelp facilité de gestion de ces bases de données.

bibliothèque de hello tooinstall, accédez trop[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="documentation"></a>Documentation
1. [Prise en main des outils de base de données élastiques](sql-database-elastic-scale-get-started.md)
2. [Fonctionnalités des bases de données élastiques](sql-database-elastic-scale-introduction.md)
3. [Gestion des cartes de partitions](sql-database-elastic-scale-shard-map-management.md)
4. [Migrer tooscale-out de bases de données existant](sql-database-elastic-convert-to-use-elastic-tools.md)
5. [Routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md)
6. [Requêtes sur plusieurs partitions](sql-database-elastic-scale-multishard-querying.md)
7. [Ajout d’une partition à l’aide des outils de base de données élastique](sql-database-elastic-scale-add-a-shard.md)
8. [Applications multi-locataires avec des outils de base de données élastique et la sécurité au niveau des lignes](sql-database-elastic-tools-multi-tenant-row-level-security.md)
9. [Mettre à niveau les applications de la bibliothèque cliente](sql-database-elastic-scale-upgrade-client-library.md) 
10. [Vue d'ensemble des requêtes élastiques](sql-database-elastic-query-overview.md)
11. [Glossaire des outils de base de données élastique](sql-database-elastic-scale-glossary.md)
12. [Bibliothèque cliente de la base de données élastique avec Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
13. [Bibliothèque cliente de bases de données élastiques avec Dapper](sql-database-elastic-scale-working-with-dapper.md)
14. [Outil de fractionnement et de fusion](sql-database-elastic-scale-overview-split-and-merge.md)
15. [Compteurs de performances pour le Gestionnaire de cartes de partitions](sql-database-elastic-database-client-library.md) 
16. [FAQ des outils de bases de données élastiques](sql-database-elastic-scale-faq.md)

## <a name="client-capabilities"></a>Fonctionnalités du client
Montée en puissance parallèle à l’aide des applications *partitionnement* présente des défis pour les développeurs hello ainsi que les administrateur hello. bibliothèque cliente de Hello simplifie les tâches de gestion de hello en fournissant des outils qui permettent à la fois aux développeurs et administrateurs de gérer les bases de données à grande échelle. Dans un exemple classique, il existe de nombreuses bases de données, appelées « fragments », toomanage. Les clients sont localisés dans hello la même base de données, et qu’il existe une base de données par client (un schéma locataire unique). bibliothèque cliente de Hello comprend ces fonctionnalités :

- **Gestion de carte de partitions**: une base de données spéciale appelée hello « Gestionnaire de carte de partitions » est créé. Gestion de carte de partitions est la capacité hello pour une application toomanage les métadonnées sur ses partitions. Les développeurs peuvent utiliser cette bases de données tooregister fonctionnalité comme partitions, décrivent les mappages de clés de partitionnement individuels ou des bases de données de plages de clés toothose et mettre à jour ces métadonnées en tant que nombre de hello et composition de bases de données évolue de modifications de capacité tooreflect. Sans la bibliothèque cliente de base de données élastique hello, il vous faudrait toospend beaucoup de temps à écrire du code de gestion hello lors de l’implémentation du partitionnement. Pour plus d'informations, consultez [Gestion des cartes de partitions](sql-database-elastic-scale-shard-map-management.md).

- **Routage dépendant des données**: imaginez une demande dans une application hello. Selon la valeur de clé de partitionnement hello de demande de hello, application hello doit hello toodetermine correct de base de données basée sur la valeur de clé hello. Il ouvre ensuite une demande de connexion toohello de base de données tooprocess hello. Routage dépendant des données permet hello tooopen des connexions avec un seul appel simple dans la carte de partitions hello de l’application hello. Routage dépendant des données a une autre zone du code d’infrastructure qui est maintenant couvert par les fonctionnalités de la bibliothèque cliente de base de données élastique hello. Pour plus d'informations, consultez [Routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md).
- **Requêtes sur plusieurs partitions**: l'interrogation de plusieurs partitions fonctionne lorsqu'une demande implique plusieurs (ou toutes les) partitions. Une requête de plusieurs partition exécute hello même code T-SQL sur toutes les partitions ou un ensemble de partitions. résultats de Hello de hello participant à des partitions sont fusionnés dans un résultat global défini à l’aide de la sémantique de UNION ALL. Hello fonctionnalité tel qu’exposé via la bibliothèque cliente de hello gère de nombreuses tâches, y compris : gestion des connexions, gestion des threads, la gestion des erreurs et les résultats intermédiaires du traitement. MSQ peut interroger des toohundreds de partitions. Pour plus d'informations, consultez [Requête sur plusieurs partitions](sql-database-elastic-scale-multishard-querying.md).

En règle générale, les clients à l’aide des outils de base de données élastique peuvent s’attendre tooget toutes les fonctionnalités T-SQL lors de l’envoi des opérations de partitions local en tant qu’opérations opposés toocross-partition qui ont leur propre sémantique.

## <a name="next-steps"></a>Étapes suivantes
Essayez de hello [exemple d’application](sql-database-elastic-scale-get-started.md) qui montre les fonctions hello du client. 

bibliothèque de hello tooinstall, accédez trop[bibliothèque cliente de base de données élastique](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Pour obtenir des instructions sur l’utilisation d’outil de fusion et fractionnement hello, consultez hello [vue d’ensemble de l’outil de fusion et fractionnement](sql-database-elastic-scale-overview-split-and-merge.md).

[La bibliothèque cliente de la base de données élastique est maintenant accessible en open source !](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

Utilisez les [requêtes élastiques](sql-database-elastic-query-overview.md).

Hello bibliothèque est disponible en tant que logiciel open source sur [GitHub](https://github.com/Azure/elastic-db-tools). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

