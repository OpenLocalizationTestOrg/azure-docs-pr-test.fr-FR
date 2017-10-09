---
title: "aaaUse Analytique de journal avec une application mutualisée de base de données SQL | Documents Microsoft"
description: "Configurer et d’utiliser l’Analytique des journaux (OMS) avec la base de données SQL Azure hello exemple d’application de Wingtip SaaS"
keywords: "didacticiel sur les bases de données SQL"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a>Configurer et d’utiliser l’Analytique des journaux (OMS) avec application de Wingtip SaaS hello

Dans ce didacticiel, vous configurez et utilisez *Log Analytics ([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* pour surveiller les pools élastiques et les bases de données. Il repose sur hello [didacticiel sur l’analyse des performances et de gestion](sql-database-saas-tutorial-performance-monitoring.md)et montre comment toouse *Analytique de journal* tooaugment hello d’analyse et d’alerte fourni Bonjour portail Azure. Log Analytics est particulièrement adapté à la surveillance et aux alertes à grande échelle, car il prend en charge des centaines de pools et des centaines de milliers de bases de données. Il offre également une solution de surveillance unique qui permet d’intégrer la surveillance de différents services Azure et applications dans plusieurs abonnements Azure.

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Installer et configurer Log Analytics (OMS)
> * Utiliser des bases de données et des pools de toomonitor Analytique de journal

toocomplete ce didacticiel, assurez-vous que hello est suivant des conditions préalables requises sont effectuées :

* Hello Wingtip SaaS application est déployée. toodeploy en moins de cinq minutes, consultez [déployer et Explorer hello Wingtip SaaS application](sql-database-saas-tutorial.md)
* Azure PowerShell est installé. Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

Consultez hello [didacticiel sur l’analyse des performances et de gestion](sql-database-saas-tutorial-performance-monitoring.md) pour une présentation des scénarios de SaaS hello et de modèles et de leur impact sur les exigences de hello sur une solution d’analyse.

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a>Surveillance et gestion des performances avec Log Analytics (OMS)

Pour SQL Database, la surveillance et les alertes sont disponibles pour les bases de données et les pools. Ce intégrées d’analyse et de génération d’alertes sont spécifique à la ressource et pratique pour un petit nombre de ressources, mais il est moins bien adaptés toomonitoring les installations de grande taille ou pour fournir une vue unifiée plusieurs abonnements et les différentes ressources.

Pour les scénarios à volumes élevés, il est possible d’utiliser Log Analytics. Il s’agit d’un service Azure séparé qui fournit l’analytique sur les journaux de diagnostic émis et télémétrie collecté dans un journal analytique espace de travail, ce qui peut collecter des données de télémétrie d’un grand nombre de services et tooquery utilisé et définie des alertes. Log Analytics offre un langage de requête intégré et des outils d’analyse et de visualisation des données opérationnelles. Hello solution d’Analytique de SQL fournit plusieurs prédéfinies par pool élastique et une base de données d’analyse et les alertes de vues et des requêtes et vous permet d’ajouter vos propres requêtes ad hoc et enregistrer ces besoins. OMS offre également un concepteur de vues personnalisées.

Les solutions journal Analytique analytique et les espaces de travail peuvent être ouverts dans hello portail Azure et dans OMS. Hello portail Azure est le point d’accès hello plus récente, mais peut être cachée dans certaines zones du portail OMS hello.

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a>Démarrer hello charge générateur toocreate données tooanalyze

1. Ouvrez **PerformanceMonitoringAndManagement.ps1 de démonstration** Bonjour **PowerShell ISE**. Laissez ce script ouverte souhaité toorun plusieurs scénarios de génération de charge hello au cours de ce didacticiel.
1. Si vous avez moins de cinq clients, approvisionner un lot de locataires tooprovide un contexte de surveillance plus intéressant :
   1. Définissez **$DemoScenario = 1,** **Provision a batch of tenants** (Configurer un lot de locataires).
   1. Appuyez sur **F5** script de hello toorun.

1. Définissez **$DemoScenario** = 2, **Generate normal intensity load (approx 40 DTU)** (Générer une charge d’intensité normale [environ 40 DTU]).
1. Appuyez sur **F5** script de hello toorun.

## <a name="get-hello-wingtip-application-scripts"></a>Obtenir les scripts d’application hello Wingtip

Hello Wingtip Tickets scripts et code source d’applications sont disponibles dans hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) référentiel github. Fichiers de script se trouvent dans hello [dossier Modules d’apprentissage](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules). Télécharger hello **Modules d’apprentissage** dossier tooyour ordinateur local en conservant sa structure de dossiers.

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a>Installation et configuration Analytique de journal et hello solution d’Analytique de SQL Azure

Analytique de journal est un service distinct qui doit toobe configuré. Log Analytics collecte des données de journaux et de télémétrie dans un espace de travail dédié à l’analyse. Un espace de travail constitue une ressource, et tout comme les autres ressources d’Azure, il doit être créé. Lors de l’espace de travail hello n’a pas besoin toobe créé Bonjour même groupe de ressources en tant qu’applications hello qui est analysé, il est souvent judicieux hello la plupart des. Dans les cas de hello de hello Wingtip SaaS application, cela permet de toobe d’espace de travail hello facilement supprimé avec l’application hello en la supprimant le groupe de ressources hello.

1. Ouvrir... \\Modules d’apprentissage\\l’analyse des performances et gestion\\Analytique de journal\\*LogAnalytics.ps1 de démonstration* Bonjour **PowerShell ISE**.
1. Appuyez sur **F5** script de hello toorun.

À ce stade, vous devez être en mesure d’Analytique de journal ouvert dans le portail Azure hello (ou du portail OMS hello). Il prendra quelques minutes pour toobe de télémétrie collectées dans l’espace de travail Analytique de journal hello et toobecome visible. Hello plu que vous laissez le système hello collecte des données hello plus intéressante expérience de hello sera. Il est maintenant temps toograb une boisson - simplement Assurez-vous Générateur de charge hello est en cours d’exécution !


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a>Utiliser l’Analytique des journaux et hello des bases de données et des pools de toomonitor de solution SQL Analytique


Dans cet exercice, ouvrez Analytique de journal et toolook de portail OMS hello à télémétrie hello collectée pour les pools et les bases de données hello.

1. Parcourir toohello [portail Azure](https://portal.azure.com) ouvrir Analytique de journal en cliquant sur plus de services, puis recherchez Analytique de journal :

   ![Ouvrir Log Analytics](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. Sélectionnez l’espace de travail hello nommé *wtploganalytics -&lt;utilisateur&gt;*.

1. Sélectionnez **vue d’ensemble** tooopen hello solution Analytique de journal Bonjour portail Azure.
   ![Lien Vue d’ensemble](media/sql-database-saas-tutorial-log-analytics/click-overview.png)

    **IMPORTANT**: il peut prendre quelques minutes avant de la solution de hello est active. Soyez patient !

1. Cliquez sur hello Analytique de SQL Azure vignette tooopen dessus.

    ![Vue d’ensemble](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![Analytics](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. Bonjour vue dans hello solution panneau fait défiler vers le côté, avec sa propre barre de défilement en bas de hello (actualisation hello panneau si nécessaire).

1. Explorez hello différentes vues en cliquant dessus ou sur des ressources individuelles tooopen un Explorateur de zoom, où vous pouvez utiliser le curseur de temps hello Bonjour haut gauche ou cliquez sur une verticale toofocus dans la barre d’une tranche de temps plus étroite. Dans cette vue, vous pouvez sélectionner individuels toofocus de bases de données ou les pools de ressources spécifiques :

    ![Graphique](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. Dans le panneau de solution hello, si vous faites défiler toohello droite vous verrez certaines requêtes enregistrées que vous pouvez cliquer sur tooopen et Explorer. Vous pouvez essayer de les modifier de différentes manières et enregistrer les requêtes intéressantes que vous obtenez. Vous pourrez alors les rouvrir et les utiliser avec d’autres ressources.

1. Dans le panneau espace de travail Analytique de journal hello sélectionnez portail OMS tooopen hello même solution.

    ![OMS](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. Dans le portail OMS hello, vous pouvez configurer des alertes. Cliquez sur la partie d’alerte hello de base de données hello vue DTU.

1. Bonjour recherche de journal qui s’affiche vous verrez un graphique à barres des métriques hello représenté.

    ![recherche dans les journaux](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. Si vous cliquez sur l’alerte dans la barre d’outils hello vous sera en mesure de toosee hello alerte et vous pouvez le modifier.

    ![Ajouter une règle d’alerte](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

Hello analyses et alertes dans le journal Analytique et OMS basé sur des requêtes sur les données hello dans l’espace de travail hello, contrairement aux hello d’alerte sur chaque panneau des ressources, qui est spécifique à la ressource. Ainsi, vous pouvez par exemple définir une alerte qui examine toutes les bases de données plutôt que d’en définir une par base de données. Vous pouvez également créer une alerte qui utilise une requête composite portant sur plusieurs types de ressources. Les requêtes sont limitées uniquement par les données hello disponibles dans l’espace de travail hello.

Analytique de journal pour la base de données SQL est facturé pour basé sur le volume de données hello dans l’espace de travail hello. Dans ce didacticiel, vous avez créé un espace de travail gratuit, qui est limitée too500MB par jour. Une fois cette limite est atteinte données ne sont plus ajoutées toohello espace de travail.


## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]
> * Installer et configurer Log Analytics (OMS)
> * Utiliser des bases de données et des pools de toomonitor Analytique de journal

[Didacticiel sur l’analyse des locataires](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a>Ressources supplémentaires

* [D’autres didacticiels qui reposent sur le déploiement de l’application hello initiale Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Azure Log Analytics](../log-analytics/log-analytics-azure-sql.md)
* [OMS](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
