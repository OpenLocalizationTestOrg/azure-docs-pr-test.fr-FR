---
title: "requêtes d’analytique aaaRun sur plusieurs bases de données SQL Azure | Documents Microsoft"
description: "Extraire des données à partir de bases de données du locataire dans une base de données d’analyse pour une analyse hors connexion"
keywords: "didacticiel sur les bases de données SQL"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a>Extraire des données à partir de bases de données du locataire dans une base de données d’analyse pour une analyse hors connexion

Dans ce didacticiel, vous utilisez une tâche élastique toorun l’interrogation chaque base de données client. travail de Hello extrait des données de ventes de ticket et les charge dans une base de données analytique (ou l’entrepôt de données) pour l’analyse. Hello base de données analytique est ensuite interrogée insights tooextract à partir de ces données opérationnelles quotidiennes de tous les locataires.


Ce didacticiel vous explique comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer la base de données analytique hello client
> * Créer une tâche planifiée des données tooretrieve et remplir la base de données analytique hello

toocomplete ce didacticiel, assurez-vous que hello est suivant les conditions préalables sont remplies :

* Hello Wingtip SaaS application est déployée. toodeploy en moins de cinq minutes, consultez [déployer et Explorer hello Wingtip SaaS application](sql-database-saas-tutorial.md)
* Azure PowerShell est installé. Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).
* version la plus récente Hello de SQL Server Management Studio (SSMS) est installée. [Télécharger et installer SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a>Modèle d’analyse opérationnelle du locataire

Une des opportunités de hello avec les applications SaaS donnée toouse hello client riche qui est stocké dans le cloud de hello. Utilisez cette insights toogain de données dans l’opération de hello et l’utilisation de votre application et vos clients. Ces données peuvent guide de développement des fonctionnalités, de facilité d’utilisation et autres investissements dans l’application hello et la plateforme. Lorsqu’il se fait dans une seule base de données mutualisée, l’accès à ces données est facile, mais pas si simple lors d’une distribution à grande échelle sur des milliers de bases de données. Une approche tooaccessing ces données sont les travaux élastique toouse, qui permettent des résultats de la requête retourne des résultats à partir de la tâche d’exécution toobe est capturée dans une base de données de sortie et de la table.

## <a name="get-hello-wingtip-application-scripts"></a>Obtenir les scripts d’application hello Wingtip

Hello Wingtip SaaS scripts et code source d’applications sont disponibles dans hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) référentiel github. [Étapes de scripts de Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="deploy-a-database-for-tenant-analytics-results"></a>Déployer une base de données pour les résultats d’analyse du locataire

Ce didacticiel requiert que vous toohave qu'un Bonjour déployé toocapture de base de données résultant de l’exécution du travail de scripts, qui contiennent des requêtes retournant des résultats. À cet effet, nous allons créer une base de données appelée tenantanalytics.

1. Ouvrir... \\Modules d’apprentissage\\Analytique opérationnelle\\locataire Analytique\\*TenantAnalyticsDB.ps1 de démonstration* Bonjour *PowerShell ISE* et définissez Hello valeur suivante :
   * **$DemoScenario** = **2***Déployer une base de données d’analyse opérationnelle*
1. Appuyez sur **F5** script de démo hello toorun (ce hello appels *TenantAnalyticsDB.ps1 de déployer* script) qui crée la base de données analytique hello client.

## <a name="create-some-data-for-hello-demo"></a>Créer des données pour une démonstration de hello

1. Ouvrir... \\Modules d’apprentissage\\Analytique opérationnelle\\locataire Analytique\\*TenantAnalyticsDB.ps1 de démonstration* Bonjour *PowerShell ISE* et définissez Hello valeur suivante :
   * **$DemoScenario** = **1***Acheter des tickets pour des événements dans tous les lieux*
1. Appuyez sur **F5** toorun hello script et créer un ticket de l’historique des achats.


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a>Créer un analytique de locataire tooretrieve tâche planifiée sur des achats de ticket

Ce script crée une travail tooretrieve fournisseur des informations à partir de tous les clients. Une fois agrégées en une seule table, vous pouvez obtenir des métriques instructif riches sur un ticket d’achat de modèles sur les locataires hello.

1. Ouvrez SSMS et se connecter toohello catalogue -&lt;utilisateur&gt;. database.windows.net server
1. Ouvrez ...\\Modules d’apprentissage\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*.
1. Modifier &lt;utilisateur&gt;, nom d’utilisateur utilisez hello utilisé lorsque vous avez déployé l’application de Wingtip SaaS hello haut hello du script de hello, **sp\_ajouter\_cible\_groupe\_membre** et **sp\_ajouter\_jobstep**
1. Avec le bouton droit sur, sélectionnez **connexion**et vous connecter toohello catalogue -&lt;utilisateur&gt;. database.windows.net server, si vous êtes pas déjà connecté
1. Assurez-vous que vous êtes connecté toohello **jobaccount** base de données, puis appuyez sur **F5** pour exécuter le script de hello

* **SP\_ajouter\_cible\_groupe** crée le nom du groupe cible hello *TenantGroup*, maintenant nous avons besoin de membres de cibles tooadd.
* **SP\_ajouter\_cible\_groupe\_membre** ajoute un *server* cibler un type de membre qui juge toutes les bases de données dans le serveur (Notez il s’agit hello customer1 - &lt;Utilisateur&gt; serveur contenant les bases de données clientes hello) au moment du travail de l’exécution doit être incluse dans la tâche de hello.
* **sp\_add\_job** crée un nouveau travail hebdomadaire planifié appelé « Achat de tickets par tous les locataires ».
* **SP\_ajouter\_jobstep** crée de toutes les informations d’achat de ticket hello étape de travail hello contenant tooretrieve de texte de commande T-SQL à partir de tous les locataires et hello copie retourner le jeu de résultats dans une table appelée  *AllTicketsPurchasesfromAllTenants*
* vues restantes de Hello dans le script de hello affichent existence hello d’objets de hello et de surveiller l’exécution du travail. Passez en revue la valeur d’état hello de hello **cycle de vie** état de colonne toomonitor hello. Une seule fois, a réussi, hello travail a correctement terminé sur toutes les bases de données client et deux bases de données supplémentaires contenant hello hello référencent table.

Script de hello en cours d’exécution doit entraîner des résultats similaires :

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a>Créer un tooretrieve de travail un récapitulatif du ticket des achats auprès de tous les locataires

Ce script crée une somme de tooretrieve de travail de tous les achats de ticket à partir de tous les clients.

1. Ouvrez SSMS et se connecter toohello *catalogue -&lt;utilisateur&gt;. database.windows.net* server
1. Fichier ouvert hello... \\Modules d’apprentissage\\fourniture et catalogue\\Analytique opérationnelle\\locataire Analytique\\*TicketPurchasesfromAllTenants.sql de résultats*
1. Modifier &lt;utilisateur&gt;, nom d’utilisateur utilisez hello utilisé lorsque vous avez déployé l’application de Wingtip SaaS hello dans le script hello, Bonjour **sp\_ajouter\_jobstep** procédure stockée
1. Avec le bouton droit sur, sélectionnez **connexion**et vous connecter toohello catalogue -&lt;utilisateur&gt;. database.windows.net server, si vous êtes pas déjà connecté
1. Assurez-vous que vous êtes connecté toohello **tenantanalytics** base de données, puis appuyez sur **F5** pour exécuter le script de hello

Script de hello en cours d’exécution doit entraîner des résultats similaires :

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* **sp\_add\_job** crée un travail hebdomadaire planifié appelé « ResultsTicketsOrders ».

* **SP\_ajouter\_jobstep** crée de toutes les informations d’achat de ticket hello étape de travail hello contenant tooretrieve de texte de commande T-SQL à partir de tous les locataires et hello copie retourner le jeu de résultats dans une table appelée CountofTicketOrders

* vues restantes de Hello dans le script de hello affichent existence hello d’objets de hello et de surveiller l’exécution du travail. Passez en revue la valeur d’état hello de hello **cycle de vie** état de colonne toomonitor hello. Une seule fois, a réussi, hello travail a correctement terminé sur toutes les bases de données client et deux bases de données supplémentaires contenant hello hello référencent table.


## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Déployez une base de données d’analyse du locataire
> * Créer un travail planifié tooretrieve de données analytiques sur locataires

Félicitations !

## <a name="additional-resources"></a>Ressources supplémentaires

* Supplémentaires [didacticiels qui reposent sur hello application Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Tâches élastiques](sql-database-elastic-jobs-overview.md)
