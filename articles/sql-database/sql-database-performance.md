---
title: "aaaMonitor et améliorer les performances - base de données SQL Azure | Documents Microsoft"
description: "Hello, que base de données SQL Azure offre des performances des outils toohelp vous identifiez les zones qui peuvent améliorer les performances des requêtes en cours."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a>Surveiller et améliorer les performances
Azure SQL Database identifie les problèmes potentiels de votre base de données et recommande les actions susceptibles d’améliorer les performances de votre charge de travail en fournissant des recommandations et des actions de réglage intelligent.

tooreview vos performances de la base de données, les utilisez hello **performances** vignette sur la page de vue d’ensemble de hello ou naviguez vers le bas trop « Prise en charge + dépannage » section :

   ![Afficher les performances](./media/sql-database-performance/entries.png)

Dans la section de hello « Prise en charge + dépannage », vous pouvez utiliser hello suivant pages :


1. [Vue d’ensemble des performances](#performance-overview) toomonitor les performances de votre base de données. 
2. [Recommandations relatives aux performances](#performance-recommendations) recommandations relatives aux performances toofind qui peut améliorer les performances de votre charge de travail.
3. [Query Performance Insight](#query-performance-insight) principales requêtes consommatrices de ressources toofind.
4. [Le paramétrage automatique](#automatic-tuning) toolet base de données SQL Azure optimiser automatiquement votre base de données.

## <a name="performance-overview"></a>Vue d'ensemble des performances
Cette vue fournit un résumé des performances de votre base de données et vous aide à optimiser les performances et à résoudre les problèmes. 

![Performances](./media/sql-database-performance/performance.png)

* Hello **recommandations** vignette fournit une décomposition des recommandations pour votre base de données de paramétrage (recommandations les trois premières sont affichées s’il existe plusieurs). Cliquez sur cette vignette pour accéder trop**[recommandations relatives aux performances](#performance-recommendations)**. 
* Hello **paramétrage activité** vignette fournit un résumé de hello en cours et terminée de réglage des actions pour votre base de données, ce qui vous donne un aperçu rapide de l’historique de hello du paramétrage d’activité. Cliquez sur cette vignette pour accéder toohello complète réglage d’affichage de l’historique de votre base de données.
* Hello **réglage automatique** vignette affiche hello [réglage automatique de la configuration](sql-database-automatic-tuning-enable.md) pour votre base de données (options d’analyse qui sont automatiquement appliqués tooyour de base de données). En cliquant sur cette vignette ouvre la boîte de dialogue de configuration hello automation.
* Hello **les requêtes de base de données** vignette affiche hello résumé des performances des requêtes hello pour votre base de données (globale DTU d’utilisation et haut requêtes consommatrices de ressources). Cliquez sur cette vignette pour accéder trop**[Query Performance Insight](#query-performance-insight)**.

## <a name="performance-recommendations"></a>Recommandations en matière de performances
Cette page fournit des [recommandations de réglage intelligent](sql-database-advisor.md) qui peuvent améliorer les performances de votre base de données. Hello les types de recommandations suivants s’affichent sur cette page :

* Recommandations sur les index toocreate ou les déplacer.
* Recommandations de problèmes de schéma sont identifiées dans la base de données hello.
* Recommandations quand les requêtes peuvent tirer parti des requêtes paramétrables.

![Performances](./media/sql-database-performance/recommendations.png)

Vous trouverez également un historique complet des actions qui ont été appliquées dans hello en cours de paramétrage.

En savoir comment toofind un appliquer les recommandations relatives aux performances dans [trouver et appliquer les recommandations relatives aux performances](sql-database-advisor-portal.md) l’article.

## <a name="automatic-tuning"></a>Réglage automatique
Azure SQL Database peut régler automatiquement les performances de base de données en appliquant les [recommandations relatives aux performances](sql-database-advisor.md). toolearn plus, lisez [article Paramétrage automatique](sql-database-automatic-tuning.md). tooenable, lecture [comment le paramétrage automatique tooenable](sql-database-automatic-tuning-enable.md).

## <a name="query-performance-insight"></a>Query Performance Insight
[Query Performance Insight](sql-database-query-performance.md) permet toospend moins de temps résolution des problèmes de performances de la base de données en fournissant :

* Une meilleure compréhension de la consommation des ressources des bases de données (DTU). 
* Hello processeur supérieure consomme des requêtes, qui peuvent potentiellement être paramétrées pour améliorer les performances. 
* Bonjour capacité toodrill vers le bas dans les détails de hello d’une requête. 

  ![tableau de bord des performances](./media/sql-database-query-performance/performance.png)

Trouver plus d’informations sur cette page dans l’article de hello  **[comment toouse Query Performance Insight](sql-database-query-performance.md)**.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Guide des performances de base de données SQL Azure pour les bases de données uniques](sql-database-performance-guidance.md)
* [Quand utiliser un pool élastique ?](sql-database-elastic-pool-guidance.md)

