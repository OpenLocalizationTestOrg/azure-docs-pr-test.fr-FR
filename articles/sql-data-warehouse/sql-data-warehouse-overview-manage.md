---
title: "aaaManage de bases de données dans l’entrepôt de données SQL Azure | Documents Microsoft"
description: "Vue d’ensemble de la gestion des bases de données SQL Data Warehouse. Inclut des outils de gestion, des unités DWU et une montée en puissance des performances, une résolution des problèmes de performances des requêtes, la mise en œuvre de stratégies de sécurité adaptées et la restauration d’une base de données en cas d’altération des données ou de panne au niveau régional."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a>Gestion de bases de données dans Azure SQL Data Warehouse
SQL Data Warehouse automatise de nombreux aspects de la gestion de vos bases de données. Par exemple, performances tooscale vous suffit de tooadjust payez hello à droite au niveau des ressources de calcul et permet à SQL Data Warehouse hello se charger de montée en puissance parallèle et de mise à l’échelle back.

Vous devez à toomonitor sans aucun doute votre tooidentify de charge de travail, vos performances doit ainsi résoudre les problèmes des requêtes longues. Vous devez également tooperform quelques autorisations de toomanage de tâches de sécurité pour les utilisateurs et les connexions.

Cette présentation couvre ces aspects de la gestion de SQL Data Warehouse.

* Outils de gestion
* Mise à l’échelle des ressources de calcul
* Suspension et reprise
* Meilleures pratiques pour les performances
* Surveillance des requêtes
* Sécurité
* Sauvegarde et restauration

## <a name="management-tools"></a>Outils de gestion
Vous pouvez utiliser diverses bases de données toomanage outils dans l’entrepôt de données SQL. Lorsque vous gérez des bases de données, vous allez développer les préférences de l’outil pour chaque type de tâche, vous devez tooperform.

### <a name="azure-portal"></a>Portail Azure
Hello [portail Azure] [ Azure portal] est un portail web où vous pouvez créer, mettre à jour et supprimer les bases de données et surveiller les ressources de base de données. Cet outil est très utile est si vous débutez avec Azure, la gestion d’un petit nombre de bases de données associées, ou devez tooquickly faire quelque chose.

tooget main hello portail Azure, consultez [créer un entrepôt de données SQL (portail Azure)][Create a SQL Data Warehouse (Azure portal)].

### <a name="sql-server-data-tools-in-visual-studio"></a>SQL Server Data Tools dans Visual Studio
[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) dans Visual Studio vous permet de tooconnect à gérer et développer vos bases de données. Si vous êtes un développeur d’applications familiarisé avec Visual Studio ou d’autres environnements de développement intégré (IDE), essayez la fonction SSDT de Visual Studio.

SSDT inclut hello Explorateur d’objets SQL Server qui vous permet de toovisualize, connectez-vous, puis exécuter des scripts sur les bases de données SQL Data Warehouse. tooquickly connecter tooSQL l’entrepôt de données, vous pouvez cliquer simplement sur hello **ouvert dans Visual Studio** bouton dans la barre de commandes hello lors de l’affichage des détails de base de données hello Bonjour portail classique Azure.  

tooget main SSDT dans Visual Studio, consultez [requête Azure SQL Data Warehouse avec Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].

### <a name="command-line-tools"></a>Outils de ligne de commande
Les outils de ligne de commande sont la solution idéale pour l’automatisation de vos charges de travail.  PowerShell et sqlcmd sont deux façons intéressantes tooautomate votre processus.  Nous vous recommandons de ces outils pour gérer un grand nombre de serveurs logiques et déployer les modifications des ressources dans un environnement de production comme tâches hello nécessaires peuvent être basée sur un script et puis automatisées.

### <a name="dynamic-management-views"></a>Vues de gestion dynamique (DMV)
Vues de gestion dynamique sont hello indispensables de gestion de l’entrepôt de données SQL. Presque toutes les informations qui met en évidence dans le portail de hello s’appuie sur les vues de gestion dynamique. toosee une liste de DMV de l’entrepôt de données SQL, consultez [les vues système SQL Data Warehouse][SQL Data Warehouse system views].

tooget démarré, consultez [se connecter et requête avec sqlcmd][Connect and query with sqlcmd], et [créer une base de données (PowerShell)][Create a database (PowerShell)].

## <a name="scale-compute"></a>Mise à l’échelle des ressources de calcul
Dans SQL Data Warehouse, vous pouvez rapidement mettre les performances à l’échelle en augmentant ou diminuant les ressources de calcul du processeur, de la mémoire et de la bande passante d’E/S. tooscale des performances, vous toodo suffit ajuster nombre hello d’unités de l’entrepôt de données (Dwu) que SQL Data Warehouse alloue de la base de données tooyour. SQL Data Warehouse rend hello modifier rapidement et gère tous les toohardware de modifications sous-jacente hello ou logiciel.

toolearn en savoir plus sur la mise à l’échelle Dwu, consultez [mettre à l’échelle des performances].

## <a name="pause-and-resume"></a>Suspension et reprise
toosave des coûts, vous pouvez suspendre et reprendre des ressources à la demande de calcul. Par exemple, si vous n’utiliserez pas de base de données hello pendant la nuit de hello et le week-end, suspendre pendant les heures et reprendre la journée hello. Vous ne sera pas facturé pour Dwu lorsque la base de données hello est suspendue.

Pour plus d’informations, consultez [Suspension du calcul][Pause compute], et [Reprise du calcul][Resume compute].

## <a name="performance-best-practices"></a>Meilleures pratiques pour les performances
Lors de la mise en route avec une nouvelle technologie, découverte hello conseils et astuces fonctionnent correctement meilleures à partir du début de hello, peut de gagner beaucoup de temps.  Vous trouverez des meilleures pratiques dans plusieurs de nos rubriques.

toosee nombreux un résumé des considérations de hello plus importantes lors du développement de votre charge de travail, consultez [meilleures pratiques de l’entrepôt de données SQL][SQL Data Warehouse Best Practices].

## <a name="query-monitoring"></a>Surveillance des requêtes
Parfois, une requête est trop longue, mais vous n’êtes pas sûr de l’application est responsable de hello. SQL Data Warehouse a des vues de gestion dynamique (DMV) que vous pouvez utiliser toofigure hors de la requête est trop longue.

toofind longues requêtes, consultez [analyser votre charge de travail à l’aide des DMV][Monitor your workload using DMVs].

## <a name="security"></a>Sécurité
toomaintain un système sécurisé, vous devez être sur l’alerte de hello et protéger n’importe quel type d’accès non autorisé. Un système de sécurité doit toomake que les règles de pare-feu sont en place, seules les adresses IP peuvent se connecter. Il nécessite une authentification correcte des informations d’identification de l’utilisateur. Une fois un utilisateur a connecté toohello de base de données, utilisateur de hello ne doit avoir les autorisations tooperform un nombre minimal d’actions. toosecure des données, vous pouvez utiliser le chiffrement. Il est également important toohave l’audit et de suivi afin de vous pouvez retracer les événements s’il en existe toute activité suspecte.

toolearn sur la gestion de la sécurité, consultez toohello [vue d’ensemble de la sécurité][Security overview].

## <a name="backup-and-restore"></a>Sauvegarde et restauration
Le stockage de sauvegardes fiables de vos données est un élément essentiel de toute base de données de production. SQL Data Warehouse permet de sécuriser vos données en sauvegardant automatiquement vos bases de données actives à intervalles réguliers. Ces sauvegardes permettent de toorecover à partir des scénarios où vous avez vos données endommagées ou suppression accidentelle de vos données ou la base de données.  Pour la planification de sauvegarde données hello, stratégie de rétention et toorestore une base de données, voir [restaurer à partir de l’instantané][Restore from snapshot].

## <a name="next-steps"></a>Étapes suivantes
À l’aide des principes de conception d’une bonne base de données rend toomanage plus facilement vos bases de données dans l’entrepôt de données SQL. toolearn plus, chef sur toohello [vue d’ensemble du développement][Development overview].

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[mettre à l’échelle des performances]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
