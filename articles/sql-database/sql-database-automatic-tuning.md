---
title: "aaaSQL de base de données - le paramétrage automatique | Documents Microsoft"
description: "Base de données SQL analyse la requête SQL et automatiquement s’adapte à la charge de travail toouser."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: jovanpop
ms.openlocfilehash: 897a8deaabedb6727dc49958c64d0433c5f2e4f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-tuning"></a>Réglage automatique

Base de données SQL Azure est un service de données entièrement géré qui surveille les requêtes hello qui sont exécutées sur la base de données hello et peuvent améliorer les performances des charges de travail hello automatiquement. Base de données SQL Azure a un mécanisme d’intelligence intégrée qui peut optimiser et améliorer les performances de vos requêtes en adaptant dynamiquement la charge de travail tooyour hello de base de données automatiquement. Réglage automatique dans la base de données SQL Azure peut être une des fonctionnalités hello plus importantes que vous pouvez activer sur les performances de toooptimize de base de données SQL Azure de vos requêtes.

Consultez cet article pour hello trop[activer le réglage automatique](sql-database-automatic-tuning-enable.md) à l’aide de hello portail Azure.

## <a name="why-automatic-tuning"></a>À quoi sert le réglage automatique ?

Une des principales tâches de hello dans l’administration de la base de données classique analyse la charge de travail hello, identifiant SQL critiques des requêtes, les index qui doivent être ajoutés à des performances de tooimprove et rarement utilisée index. Base de données SQL Azure fournit un aperçu détaillé dans les requêtes hello et les index que vous avez besoin de toomonitor. Toutefois, la surveillance permanente de la base de données est une tâche difficile et fastidieuse, en particulier lors du traitement de plusieurs bases de données. Gérer un très grand nombre de bases de données peut être impossible toodo efficacement même avec tous les outils disponibles et les rapports qui fournissent des base de données SQL Azure et le portail Azure. Au lieu de surveillance et de paramétrage de votre base de données manuellement, vous pouvez envisager de délégation des hello surveillance et de paramétrage des actions tooAzure base de données SQL à l’aide de la fonctionnalité de réglage automatique. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>Comment fonctionne le réglage automatique ?

Base de données SQL Azure a un processus de surveillance et d’analyse continue de performances qui constamment hello caractéristique de votre charge de travail utilise pour détecter et identifier des améliorations et des problèmes potentiels.

![Processus de réglage automatique](./media/sql-database-automatic-tuning/tuning-process.png)

Cela permet de processus toodynamically de la base de données SQL Azure adapter la charge de travail tooyour en recherchant les plans et les index peuvent améliorer les performances de vos charges de travail et les index affecte vos charges de travail. En fonction de ces résultats, le réglage automatique effectue des actions de réglage qui améliorent les performances de votre charge de travail. En outre, base de données SQL Azure surveille en permanence les performances après toute modification apportée par tooensure de réglage automatique qu’elle améliore les performances de votre charge de travail. Toute action qui n’a pas amélioré les performances est automatiquement annulée. Ce processus de vérification est une fonctionnalité clé qui permet de s’assurer que toute modification apportée par le paramétrage automatique ne diminue pas les performances de hello de votre charge de travail.

Deux aspects de réglage automatique sont disponibles dans Azure SQL Database :

 -  La **gestion automatique des index**, qui identifie les index qui doivent être ajoutés à votre base de données et ceux qui doivent être supprimés.
 -  La **correction du plan automatique** (déployée prochainement, déjà disponible dans SQL Server 2017), qui identifie les plans problématiques et résout les problèmes de performances du plan SQL.

## <a name="automatic-index-management"></a>Gestion automatique des index

Dans Azure SQL Database, la gestion des index est facile, car Azure SQL Database s’informe sur votre charge de travail et s’assure que vos données sont toujours indexées de manière optimale. Pour assurer des performances optimales de votre charge de travail, l’index doit être correctement conçu. La gestion automatique des index peut vous aider à les optimiser. Gestion automatique des index peuvent résoudre les problèmes de performances dans les bases de données indexées de manière incorrecte, ou mettre à jour et améliorez les index sur le schéma de base de données existant hello. 

### <a name="why-do-you-need-index-management"></a>Pourquoi utiliser la gestion des index ?

Index accélérer de certaines de vos requêtes qui lisent des données à partir des tables de hello ; Toutefois, ils peuvent ralentir les requêtes de hello qui mettent à jour des données. Vous devez toocarefully analyser lorsque toocreate un index et les colonnes que vous devez tooinclude dans hello index. Certains index peuvent ne plus être nécessaires après un certain temps. Par conséquent, vous devez tooperiodically identifier et supprimer des index hello qui ne mettez pas d’avantages. Si vous ignorez hello index inutilisés, les performances des requêtes hello qui mettent à jour des données est diminuée sans aucun avantage sur les requêtes hello qui lisent des données. Index inutilisés affectent également les performances globales du système de hello, car les mises à jour supplémentaires besoin d’une journalisation inutile.

Recherche l’ensemble optimal de hello d’index qui améliorent les performances des requêtes hello lire les données de vos tables et ont un impact minimal sur les mises à jour peut nécessiter l’analyse continue et complexe.

Base de données SQL Azure utilise intelligence intégrée et des règles avancées pour analyser vos requêtes, identifier les index qui seraient optimales pour vos charges de travail en cours, et les index hello risque d’être supprimés. Base de données SQL Azure permet de s’assurer que vous disposez d’un ensemble minimal nécessaire d’index qui optimisent les requêtes hello qui lisent des données, avec un impact sur hello réduite hello autres requêtes.

### <a name="how-tooidentify-indexes-that-need-toobe-changed-in-your-database"></a>Comment tooidentify indexe que toobe besoin modifié dans votre base de données ?

Azure SQL Database facilite le processus de gestion des index. Base de données SQL Azure au lieu de processus fastidieux de hello d’analyse de la charge de travail manuelle et l’analyse de l’index, analyse votre charge de travail, identifie les requêtes hello pourraient être exécutées plus rapidement avec un nouvel index et identifie les index non utilisés ou en double. Pour plus d’informations sur l’identification des index à modifier, voir [Rechercher des recommandations d’index dans le portail Azure](sql-database-advisor-portal.md).

### <a name="automatic-index-management-considerations"></a>Considérations sur la gestion automatique des index

Si vous trouvez que les règles intégrées hello améliorent les performances de hello de votre base de données, vous pourrez permettre de la base de données SQL Azure gérer automatiquement les index.

Actions requises toocreate des index nécessaires dans les bases de données SQL Azure peuvent consomment des ressources et affecter temporairement les performances de la charge de travail. impact de hello toominimize de création d’index sur les performances de la charge de travail, base de données SQL Azure recherche la fenêtre du moment opportun hello pour toutes les opérations de gestion d’index. Action de paramétrage est reporté à plus tard si la base de données de hello doit tooexecute des ressources de votre charge de travail et démarré lors de la base de données hello possède suffisamment les ressources inutiles qui peuvent être utilisés pour la tâche de maintenance hello. Une fonctionnalité importante dans la gestion automatique des index est une vérification des actions de hello. Lors de la base de données SQL Azure crée ou supprime des index, un processus d’analyse analyse des performances de votre tooverify de charge de travail qu’action de hello d’améliorer les performances de hello. Si elle n’a pas d’apporter une amélioration significative : hello action est immédiatement annulée. De cette manière, Azure SQL Database s’assure que les actions automatiques ne nuisent pas aux performances de votre charge de travail. Index créés par le paramétrage automatique sont transparentes pour l’opération de maintenance hello sur le schéma sous-jacent de hello. Modifications de schéma telles que supprimer ou renommer des colonnes ne sont pas bloquées par la présence de hello des index créés automatiquement. Les index créés automatiquement par Azure SQL Database sont immédiatement supprimés lorsque la table ou les colonnes liées sont supprimées.

## <a name="automatic-plan-choice-correction"></a>Correction automatique du choix de plan

La correction automatique du plan est une nouvelle fonctionnalité de réglage automatique ajoutée dans SQL Server 2017 CTP2.0. Elle identifie les plans SQL qui ne se comportent pas de manière adéquate. Cette option de réglage automatique sera bientôt disponible sur Azure SQL Database. Pour en savoir plus, voir [Réglage automatique dans SQL Server 2017](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning).

## <a name="next-steps"></a>Étapes suivantes

- tooenable automatique de paramétrage dans la base de données SQL Azure et de laisser automatique paramétrage fonctionnalité entièrement gérer votre charge de travail, consultez [activer le réglage automatique](sql-database-automatic-tuning-enable.md).
- paramétrage manuel toouse, vous pouvez passer en revue [recommandations dans le portail Azure de paramétrage](sql-database-advisor-portal.md) et appliquer manuellement hello celles qui améliorent les performances de vos requêtes.
