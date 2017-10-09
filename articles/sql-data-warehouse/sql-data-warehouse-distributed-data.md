---
title: "aaaHow distributed fonctionnement des données dans l’entrepôt de données SQL Azure | Documents Microsoft"
description: "Découvrez comment les données sont distribuées pour des options massivement parallèles de traitement (MPP) et hello pour distribuer des tables dans Azure SQL Data Warehouse et Parallel Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: bae494a6-7ac5-4c38-8ca3-ab2696c63a9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 9a712d8d5251e4391ede245105918283aaa4b193
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-data-and-distributed-tables-for-massively-parallel-processing-mpp"></a>Données et tables distribuées pour le traitement massivement parallèle (MPP)
Découvrez comment les données utilisateur sont distribuées dans Azure SQL Data Warehouse et Parallel Data Warehouse, qui sont des systèmes de traitement massivement parallèle (MPP) de Microsoft. Conception de votre toouse de l’entrepôt de données données distribuées permettent effectivement vous tooachieve hello du traitement des requêtes avantages de l’architecture MPP de hello. Certains choix de conception de base de données peuvent avoir un impact significatif sur l’amélioration des performances des requêtes.  

> [!NOTE]
> Azure SQL Data Warehouse et hello d’utilisation Parallel Data Warehouse (MPP) le traitement parallèle massif même concevoir, mais ont quelques différences en raison de hello sous-jacent de plateforme. SQL Data Warehouse est une plateforme PaaS (Platform as a Service) qui s’exécute sur Azure. Parallel Data Warehouse s’exécute sur Analytics Platform System (APS), une application locale qui s’exécute sur Windows Server.
> 
> 

## <a name="what-is-distributed-data"></a>Présentation des données distribuées
Dans l’entrepôt de données SQL et Parallel Data Warehouse, les données distribuées fait référence toouser les données qui sont stockées dans plusieurs emplacements sur hello système MPP. Chacun de ces emplacements fonctionne comme un stockage indépendant et d’une unité de traitement qui exécute des requêtes sur sa partie des données de hello. Données distribuées sont toorunning fondamentaux des requêtes parallèles tooachieve haute performances des requêtes.

toodistribute des données, l’entrepôt de données hello attribue à chaque ligne d’un emplacement de tooone distribuée de table utilisateur.  Vous pouvez distribuer des tables par hachage ou par tourniquet. méthode de distribution Hello est spécifié dans hello l’instruction CREATE TABLE. 

## <a name="hash-distributed-tables"></a>Tables distribuées par hachage
Hello suivant le diagramme illustre comment un complet (table non distribuées) est stocké comme une table de hachage distribué. Une fonction déterministe assigne chaque distribution tooone toobelong des lignes. Dans la définition de la table hello, une des colonnes de hello est désignée en tant que colonne de distribution hello. fonction de hachage Hello utilise valeur hello hello distribution colonne tooassign chaque distribution tooa de ligne.

Il existe des considérations de performances pour la sélection d’une colonne de distribution, telles que la distinction, inclinaison de données et les types de requêtes exécutées sur le système de hello hello hello.

![Table distribuée](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "Table distribuée")  

* Chaque ligne appartient tooone distribution.  
* Un algorithme de hachage déterministe assigne chaque distribution tooone de ligne.  
* nombre de Hello de lignes de table par distribution varie comme indiqué par hello différentes tailles de tables.

## <a name="round-robin-distributed-tables"></a>Tables distribuées par tourniquet
Une table distribuée alternée distribue les lignes de hello en affectant chaque distribution tooa des lignes de manière séquentielle. Tooload rapide des données dans une table de tourniquet, mais les performances des requêtes peuvent être plus lent.  Jointure d’une table de répétition alternée généralement requiert remaniement hello lignes tooenable hello requête tooproduce un résultat exact, qui prend du temps.

## <a name="distributed-storage-locations-are-called-distributions"></a>Les emplacements de stockage distribués sont appelés des distributions.
Chaque emplacement distribué est appelé une distribution. Lorsqu’une requête s’exécute en parallèle, chaque point de distribution effectue une requête SQL sur sa partie des données de hello. Entrepôt de données SQL utilise la requête de base de données SQL toorun hello. Parallel Data Warehouse utilise la requête SQL Server toorun hello. Cette conception d’architecture sans partage est montée en puissance parallèle tooachieving fondamentaux calcul parallèle.

### <a name="can-i-view-hello-distributions"></a>Afficher les distributions hello ?
Chaque point de distribution possède un ID de distribution et n’est visible dans les vues système qui se rapportent tooSQL l’entrepôt de données et Parallel Data Warehouse. Vous pouvez utiliser les performances des requêtes tootroubleshoot hello distribution ID et autres problèmes. Pour obtenir la liste de vues du système hello, consultez hello [vue de système MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="difference-between-a-distribution-and-a-compute-node"></a>Différence entre une distribution et un nœud de calcul
Une distribution est une unité de base de hello pour le stockage de données distribuées et le traitement des requêtes en parallèle. Les distributions sont regroupées en nœuds de calcul. Chaque nœud de calcul gère une ou plusieurs distributions.  

* Système de plateforme Analytique utilise des nœuds de calcul comme un composant central de hello matériel architecture et avec montée en charge les fonctions. Elle utilise toujours les huit distributions par nœud de calcul, comme indiqué dans le diagramme hello pour les tables de hachage distribué. Hello du nombre de nœuds de calcul et par conséquent hello nombre de distributions, est déterminée par un nombre de nœuds de calcul que vous achetez pour dispositif de hello hello. Par exemple, si vous achetez huit nœuds, vous obtenez 64 distributions (8 nœuds x 8 distributions/nœud). 
* SQL Data Warehouse a un nombre fixe de 60 distributions et un nombre variable de nœuds de calcul. les nœuds de calcul Hello sont implémentés avec des ressources de calcul et de stockage Azure. nombre de Hello de nœuds de calcul peut changer en fonction toohello principal service la charge de travail et hello des capacités informatiques (Dwu) vous spécifiez pour l’entrepôt de données hello. Lorsque hello des nœuds de calcul changent, nombre de hello de distributions par nœud de calcul change également. 

### <a name="can-i-view-hello-compute-nodes"></a>Puis-je afficher les nœuds de calcul hello ?
Chaque nœud de calcul possède un ID de nœud et est visible dans les vues système qui se rapportent tooSQL l’entrepôt de données et Parallel Data Warehouse.  Vous pouvez voir le nœud de calcul hello en recherchant la colonne de node_id hello dans les vues système dont les noms commencent par sys.pdw_nodes. Pour obtenir la liste de vues du système hello, consultez hello [vue de système MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="Replicated"></a>Tables répliquées
Une table est répliquée possède un entièrement la copie de la table de hello stockées sur chaque nœud de calcul. Réplication d’une table supprime les données de tootransfer besoin de hello entre les nœuds de calcul avant une jointure ou une agrégation. Les tables répliquées sont uniquement possibles avec les tables de petite taille en raison de hello table complète de stockage supplémentaire requis toostore hello sur chaque nœud de calcul.  

Hello diagramme suivant illustre une table répliquée est stockée sur chaque nœud de calcul. Pour SQL Data Warehouse, répliquée hello est la base de données de distribution tooa entièrement copiée sur chaque nœud de calcul. Pour Parallel Data Warehouse, table répliquée de hello est stocké sur tous les disques affectés toohello de nœud de calcul.  Cette stratégie de disque met en œuvre des groupes de fichiers SQL Server.  

![Table répliquée](media/sql-data-warehouse-distributed-data/replicated-table.png "Table répliquée") 

## <a name="next-steps"></a>Étapes suivantes
les tables toouse distribué efficacement, consultez [distribuer des tables SQL Data Warehouse](sql-data-warehouse-tables-distribute.md)  

