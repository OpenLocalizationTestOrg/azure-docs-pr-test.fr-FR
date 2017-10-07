---
title: "une base de données SQL Azure à partir d’une sauvegarde d’aaaRestore | Documents Microsoft"
description: "En savoir plus sur la restauration de Point-à-temps, ce qui vous permet de tooroll arrière un point précédent tooa de base de données SQL Azure dans le temps (haut too35 jours)."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: fd1d334d-a035-4a55-9446-d1cf750d9cf7
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.openlocfilehash: 84ecc306a2072445c10dbf1e9d7cf3d1b43860cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a>Récupérer une base de données SQL Azure à l’aide des sauvegardes automatisées d’une base de données
SQL Database fournit trois options pour la récupération de base de données à l’aide des [sauvegardes de base de données automatisées](sql-database-automated-backups.md) et des [sauvegardes depuis la rétention à long terme](sql-database-long-term-retention.md). Vous pouvez effectuer une restauration à partir d’une sauvegarde de base de données vers :

* Une base de données sur hello récupérée du même serveur logique tooa spécifié un point dans le temps au sein de la période de rétention hello. 
* Une base de données hello même serveur logique récupérée toohello heure de suppression pour une base de données supprimée.
* Une base de données sur n’importe quel serveur logique dans n’importe quelle région récupérée point toohello des sauvegardes quotidiennes de hello plus récente dans le stockage blob de géo-répliquées (RA-GRS).

> [!IMPORTANT]
> Vous ne pouvez pas remplacer une base de données existante lors de la restauration.
>

Vous pouvez également utiliser [les sauvegardes de base de données automatiques](sql-database-automated-backups.md) toocreate un [copie de base de données](sql-database-copy.md) sur n’importe quel serveur logique dans n’importe quelle région. 

## <a name="recovery-time"></a>Temps de récupération
Hello toorestore de temps de récupération une base de données à l’aide de sauvegardes automatisées de base de données est affecté par plusieurs facteurs : 

* taille Hello hello de base de données
* niveau de performance Hello de base de données hello
* nombre de Hello des journaux de transactions impliquées
* quantité de Hello d’activité qui a besoin de toobe relus point de restauration toorecover toohello
* la bande passante du réseau Hello si hello restaurez est tooa autre région 
* nombre de Hello de demandes de restauration simultanés en cours de traitement dans la région cible hello. 
  
  Pour une base de données très volumineux et/ou active, restauration de hello peut prendre plusieurs heures. En cas de panne prolongée dans une région, il est possible qu’un grand nombre de demandes de géorestauration soient traitées par d’autres régions. Lorsqu’il existe de nombreuses requêtes, les temps de récupération hello peuvent augmenter pour les bases de données dans cette région. La plupart des restaurations de bases de données se terminent dans un délai de 12 heures.
  
Il n’existe aucune restauration ne toodo en bloc des fonctionnalités intégrées. Hello [base de données SQL Azure : récupération de serveur complète](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) script est un exemple de la manière d’accomplir cette tâche.

> [!IMPORTANT]
> toorecover à l’aide des sauvegardes automatisées, vous devez être membre du rôle de collaborateur du serveur SQL hello dans l’abonnement de hello ou être propriétaire de l’abonnement hello. Vous pouvez récupérer à l’aide de hello portail Azure, PowerShell ou hello API REST. Vous ne pouvez pas utiliser Transact-SQL. 
> 

## <a name="point-in-time-restore"></a>Limite de restauration dans le temps

Vous pouvez restaurer une base de données tooan précédemment point dans le temps en tant que nouvelle base de données sur hello même serveur logique à l’aide de hello le portail Azure, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), ou hello [API REST](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Pour un exemple de script PowerShell montrant comment tooperform une restauration de point-à-temps d’une base de données, consultez [restaurer une base de données SQL à l’aide de PowerShell](scripts/sql-database-restore-database-powershell.md).
>

base de données Hello peut être de niveau de service tooany restaurée ou des performances niveau et comme une base de données ou dans un pool élastique. Vérifiez dispose de suffisamment de ressources sur le serveur logique de hello ou dans hello pool élastique toowhich vous restaurez la base de données hello. Une fois terminé, hello restauré la base de données est en ligne et accessible, normal. base de données restaurée de Hello est facturée au taux normales, en fonction de son niveau de performances et de la couche de service. Vous n’entraînent aucun frais jusqu'à ce que la restauration de base de données hello est terminée.

Vous restaurez généralement une base de données tooan point précédemment à des fins de récupération. Ce faisant, vous pouvez traiter hello restauré la base de données en remplacement de la base de données d’origine hello ou tooretrieve des données à partir de l’utiliser et ensuite mettre à jour de la base de données d’origine hello. 

* ***Base de données de remplacement :*** si la base de données restaurée de hello est destinée à remplacer pour base de données d’origine hello, vous devez vérifier le niveau de performance hello et/ou de niveau de service sont approprié et l’échelle de la base de données hello si nécessaire. Vous pouvez renommer la base de données d’origine hello et puis nommez hello restauré de base de données hello d’origine à l’aide de la commande ALTER DATABASE hello dans T-SQL. 
* ***Récupération de données :*** si vous envisagez de données tooretrieve de toorecover de base de données hello restaurée à partir d’une erreur utilisateur ou une application, vous devez toowrite et que vous exécutez hello nécessaire récupération scripts tooextract de données à partir de toohello de base de données restaurée de hello base de données d’origine. Bien que l’opération de restauration hello peut prendre un toocomplete beaucoup de temps, hello restauration de base de données est visible dans la liste de base de données hello tout au long du processus de restauration hello. Si vous supprimez la base de données hello pendant la restauration de hello, opération de restauration hello est annulée et vous n’êtes pas facturé pour une base de données hello qui n’a pas abouti restauration de hello. 

### <a name="azure-portal"></a>Portail Azure

point de tooa toorecover à l’aide de l’heure hello portail Azure, page hello ouvert pour votre base de données cliquez sur **restaurer** sur la barre d’outils hello.

![point-in-time-restore](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

## <a name="deleted-database-restore"></a>Restauration d’une base de données supprimée
Vous pouvez restaurer une heure de suppression de base de données supprimée toohello pour une base de données supprimée sur hello même serveur logique à l’aide de hello portail Azure, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), ou hello [REST (mode de création = restauration)](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Pour obtenir un exemple PowerShell script montrant comment toorestore une base de données supprimée, consultez [restaurer une base de données SQL à l’aide de PowerShell](scripts/sql-database-restore-database-powershell.md).
>

> [!IMPORTANT]
> Si vous supprimez une instance de serveur Azure SQL Database, toutes ses bases de données sont également supprimées et ne peuvent pas être récupérées. Il n'existe aucune prise en charge pour la restauration d'un serveur supprimé pour l'instant.
> 

### <a name="azure-portal"></a>Portail Azure

toorecover un supprimés au cours de la base de données sa [période de rétention](sql-database-service-tiers.md) à l’aide de hello portail Azure, page hello ouvert pour votre serveur et dans la zone d’opérations hello, cliquez sur **bases de données supprimées**.

![deleted-database-restore-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)


![deleted-database-restore-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

## <a name="geo-restore"></a>Géo-restauration
Vous pouvez restaurer une base de données SQL sur un serveur quelconque dans n’importe quelle région Azure à partir de hello géo-répliquées complètes et différentielles sauvegardes les plus récentes. Géo-restauration utilise une sauvegarde géo-redondant comme source et peut être utilisé toorecover un même si la base de données hello ou centre de données est inaccessible en raison de la panne de tooan. 

Géo-restauration est l’option de récupération par défaut hello lorsque votre base de données n’est pas disponible en raison d’un incident dans la région de hello où la base de données hello est hébergé. Si un incident à grande échelle dans résultats de la région une indisponibilité de votre application de base de données, vous pouvez restaurer une base de données du serveur de tooa hello des sauvegardes géo-répliquées dans toute autre région. Il existe un décalage entre le lorsqu’une sauvegarde différentielle est effectuée et il est géorépliqué tooan Azure blob dans une autre région. Ce délai peut atteindre des tooan heures, par conséquent, si un incident se produit, il peut y avoir des pertes de données tooone heures. Hello après l’illustration montre la restauration de base de données hello à partir de la dernière sauvegarde disponible hello dans une autre région.

![Restauration géographique](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> Pour obtenir un exemple PowerShell script montrant comment tooperform une géo-restauration, consultez [restaurer une base de données SQL à l’aide de PowerShell](scripts/sql-database-restore-database-powershell.md).
> 

La restauration dans le temps sur un géo-réplica secondaire n’est pas prise en charge actuellement. La restauration dans le temps peut être effectuée uniquement sur une base de données primaire. Pour plus d’informations sur l’utilisation de toorecover géo-restauration en cas de panne, consultez [récupérer en cas de panne](sql-database-disaster-recovery.md).

> [!IMPORTANT]
> Récupération à partir de sauvegardes est hello plus simple d’un incident de hello disponibles dans la base de données SQL avec des solutions de récupération hello RPO plus long et le temps de récupération d’estimation (ERT). Pour des solutions utilisant des bases de données De base, la géorestauration est souvent une solution de récupération d’urgence raisonnable avec un ERT de 12 heures. Pour des solutions utilisant des bases de données Standard ou Premium de plus grande taille qui nécessitent des temps de récupération plus courts, vous devez envisager d’utiliser une [géoréplication active](sql-database-geo-replication-overview.md). Géo-réplication Active offre un RPO beaucoup plus faible et un ERT car il ne nécessite que vous lancez une base de données secondaire de basculement tooa continuellement répliquée. Pour plus d’informations sur les choix de continuité des activités, voir [À propos de la continuité des activités](sql-database-business-continuity.md).
> 

### <a name="azure-portal"></a>Portail Azure

toogeo-restaurer une base de données lors de sa [période de rétention](sql-database-service-tiers.md) hello portail Azure, ouvrez la page de bases de données SQL hello, puis cliquez sur **ajouter**. Bonjour **sélectionner une source** zone de texte, sélectionnez **sauvegarde**. Spécifier une sauvegarde hello de récupération tooperform hello dans la région de hello et sur le serveur hello de votre choix. 

## <a name="programmatically-performing-recovery-using-automated-backups"></a>Exécution par programme d’une récupération à l’aide des sauvegardes automatisées
Comme nous l’avons vu précédemment, en outre toohello portail Azure, la récupération de la base de données peut être effectuée par programme à l’aide d’Azure PowerShell ou hello API REST. Hello les tableaux suivants décrire ensemble hello des commandes disponibles.

### <a name="powershell"></a>PowerShell
| Applet de commande | Description |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Obtient une ou plusieurs bases de données. |
| [Get-AzureRMSqlDeletedDatabaseBackup](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | Obtient une base de données supprimée que vous pouvez restaurer. |
| [Get-AzureRmSqlDatabaseGeoBackup](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) |Obtient une sauvegarde géo-redondante d’une base de données. |
| [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) |Restaure une base de données SQL. |
|  | |

### <a name="rest-api"></a>de l’API REST
| API | Description |
| --- | --- |
| [REST (createMode=Recovery)](https://msdn.microsoft.com/library/azure/mt163685.aspx) |Restaure une base de données |
| [Créer ou mettre à jour l’état de la base de données](https://msdn.microsoft.com/library/azure/mt643934.aspx) |État de hello retourne pendant une opération de restauration |
|  | |

## <a name="summary"></a>Résumé
Les sauvegardes automatiques protègent vos bases de données des erreurs utilisateur et des erreurs d’application, de la suppression accidentelle d’une base de données et des interruptions prolongées. Cette fonctionnalité intégrée est disponible pour tous les niveaux de service et de performances. 

## <a name="next-steps"></a>Étapes suivantes
* Pour une vue d’ensemble de la continuité des activités et des scénarios, consultez [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md)
* toolearn sur les sauvegardes de base de données SQL Azure automatisée, consultez [sauvegardes automatisées de base de données SQL](sql-database-automated-backups.md)
* toolearn sur la rétention de sauvegarde à long terme, consultez [rétention de sauvegarde à long terme](sql-database-long-term-retention.md)
* tooconfigure, gérer et restaurer à partir de la rétention à long terme des sauvegardes automatisées dans un coffre Azure Recovery Services à l’aide de hello Azure portail, consultez [configurer et utiliser à long terme de rétention de sauvegarde](sql-database-long-term-backup-retention-configure.md). 
* toolearn sur les options de récupération plus rapides, consultez [géo-réplication active](sql-database-geo-replication-overview.md)  
