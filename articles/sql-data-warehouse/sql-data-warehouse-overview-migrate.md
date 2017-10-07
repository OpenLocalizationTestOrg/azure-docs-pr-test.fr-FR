---
title: "aaaMigrate votre entrepôt de données de tooSQL solution | Documents Microsoft"
description: Conseils de migration pour mettre votre plateforme de SQL Data Warehouse tooAzure la solution.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a>Migrer votre tooAzure solution SQL Data Warehouse
Consultez les conséquences de la migration d’un tooAzure de solution de base de données SQL Data Warehouse existant. 

## <a name="profile-your-workload"></a>Profiler votre charge de travail
Avant de migrer, vous souhaitez toobe certaine que SQL Data Warehouse est hello bonne solution pour votre charge de travail. Entrepôt de données SQL est un analytique de tooperform système distribué conçu sur des données volumineuses.  Migration tooSQL de l’entrepôt de données nécessite des modifications de conception qui ne sont pas toounderstand trop difficile, mais peuvent prendre quelques tooimplement de temps. Si votre entreprise requiert un entrepôt de données d’entreprise, les avantages de hello valent effort de hello. Toutefois, si vous n’avez pas besoin power hello d’entrepôt de données SQL, il est plus économique toouse SQL Server ou une base de données SQL Azure.

Envisagez d’utiliser SQL Data Warehouse lorsque vous :
- Possédez plusieurs To de données
- Plan toorun analytique sur de grandes quantités de données
- Besoin de stockage et calcul de hello capacité tooscale 
- Choix des coûts de toosave en plaçant les ressources de calcul lorsque vous n’en avez pas besoin.

N’utilisez pas SQL Data Warehouse pour des charges de travail opérationnelles (OLTP) qui possèdent :
- Des lectures et écritures haute fréquence
- Un grand nombre de sélections singleton
- Des volumes élevés d’insertions à une seule ligne
- Des besoins de traitement ligne par ligne
- Des formats incompatibles (JSON, XML)


## <a name="plan-hello-migration"></a>Migration du plan de hello

Une fois que vous avez décidé de toomigrate un tooSQL existant de la solution l’entrepôt de données, il est important tooplan la migration hello avant de commencer. 

Un objectif de la planification est tooensure vos données, vos schémas de table, et votre code sont compatibles avec l’entrepôt de données SQL. Il existe certaines différences de compatibilité toowork autour entre votre système actuel et l’entrepôt de données SQL. De plus, migration de grandes quantités de données tooAzure prend du temps. Une planification minutieuse accélère la mise en route de votre tooAzure de données. 

Un autre objectif de la planification est conception toomake tooensure ajustements que votre solution tire parti des performances de requête hello Qu'entrepôt de données SQL est conçu tooprovide. Conception d’entrepôts de données pour la montée en puissance présente des modèles de conception et les méthodes traditionnelles ainsi ne sont pas toujours hello mieux. Bien que vous pouvez apporter certaines modifications de conception après la migration, apporter des modifications plus tôt dans le processus de hello enregistrera plus tard.

tooperform une migration réussie, vous devez toomigrate vos schémas de table, votre code et vos données. Lisez ces articles pour en apprendre davantage sur la migration :

-  [Migration de vos schémas](sql-data-warehouse-migrate-schema.md)
-  [Migration de votre code](sql-data-warehouse-migrate-code.md)
-  [Migration de vos données](sql-data-warehouse-migrate-data.md) 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a>Étapes suivantes
Hello CAT (équipe de consultants clients) a également certaines des instructions SQL Data Warehouse excellente, ils publient via les blogs.  Examinez leur article, [tooAzure de données de migration SQL Data Warehouse dans la pratique] [ Migrating data tooAzure SQL Data Warehouse in practice] pour obtenir des conseils supplémentaires sur la migration.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
