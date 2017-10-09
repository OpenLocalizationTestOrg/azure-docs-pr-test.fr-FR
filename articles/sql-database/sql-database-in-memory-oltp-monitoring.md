---
title: "stockage en mémoire XTP aaaMonitor | Documents Microsoft"
description: "Estimer et surveiller la capacité et l’utilisation du stockage en mémoire XTP ; résoudre l’erreur de capacité 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a>Surveiller le stockage OLTP In-Memory
Lorsque vous utilisez [OLTP en mémoire](sql-database-in-memory.md), les données des tables à mémoire optimisée et les variables de table résident dans un stockage OLTP en mémoire. Chaque niveau de service Premium a une taille de stockage maximale OLTP en mémoire, qui est décrit dans hello [article des niveaux de Service de base de données SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels). Une fois que cette limite est dépassée, des opérations d’insertion et de mise à jour peuvent commencer à échouer (en générant l’erreur 41823). À ce stade serez tooeither delete tooreclaim mémoire, ou que vous mettez à niveau le niveau de performances hello de votre base de données.

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a>Déterminer si les données correspondront au sein de l’extrémité de stockage en mémoire hello
Déterminer l’extrémité de stockage hello : consultez hello [article des niveaux de Service de base de données SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) pour les majuscules du stockage hello des différents niveaux de service Premium hello.

Estimation de la configuration requise pour une table optimisée en mémoire fonctionne même hello de mémoire moyen pour SQL Server en tant qu’il effectue dans la base de données SQL Azure. Prenez quelques minutes tooreview cette rubrique sur [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).

Notez que la table de hello et les lignes de la variable table, ainsi que les index, sont pris en compte taille des données utilisateur max hello. En outre, ALTER TABLE doit suffisamment toocreate place une nouvelle version de la totalité de la table hello et ses index.

## <a name="monitoring-and-alerting"></a>Surveillance et alerte
Vous pouvez surveiller l’utilisation de stockage en mémoire sous forme de pourcentage de hello [cap de stockage pour votre niveau de performances](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) Bonjour Azure [portal](https://portal.azure.com/): 

* Dans Panneau de base de données hello, boîte de l’utilisation de ressources hello rechercher, puis cliquez sur Modifier.
* Puis sélectionnez la métrique de hello `In-Memory OLTP Storage percentage`.
* tooadd une alerte, cliquez sur Panneau métrique hello du tooopen zone hello l’utilisation des ressources, puis cliquez sur Ajouter une alerte.

Ou utilisez hello suivant l’utilisation du stockage en mémoire de requête tooshow hello :

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>Résoudre les situations de mémoire insuffisante - erreur 41823
Quand la mémoire devient insuffisante, les opérations INSERT, UPDATE et CREATE échouent en générant le message d’erreur 41823.

Message d’erreur 41823 indique que les tables optimisées en mémoire hello et variables de table ont dépassé la taille maximale de hello.

tooresolve cette erreur, soit :

* Supprimer les données de tables mémoire optimisées de hello, tootraditional de données potentiellement déchargement hello, les tables sur disque ; ou,
* Mise à niveau tooone de niveau de service hello stockage suffisant en mémoire pour les données de salutation, vous devez tookeep dans des tables optimisées en mémoire.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’instructions sur la surveillance, consultez [Analyse de base de données SQL Azure à l’aide de vues de gestion dynamique](sql-database-monitoring-with-dmvs.md).
