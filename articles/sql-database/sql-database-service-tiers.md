---
title: "Niveaux de service et de performances de Microsoft Azure SQL Database | Microsoft Docs"
description: "Comparaison entre les niveaux de service et de performances de Microsoft Azure SQL Database pour des bases de données uniques et présentation des pools élastiques SQL"
keywords: "options de base de données,performances de base de données"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: f5c5c596-cd1e-451f-92a7-b70d4916e974
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: b27b78788614d32e6c0c4267fe0ce504ebd2f444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>Options de performances disponibles pour Microsoft Azure SQL Database

[Microsoft Azure SQL Database](sql-database-technical-overview.md) offre quatre niveaux de service pour des bases de données uniques ou [regroupées](sql-database-elastic-pool.md). Ces niveaux de service comprennent les niveaux **De base**, **Standard**, **Premium** et **Premium RS**. Dans chaque niveau de service sont plusieurs niveaux de performances ([dtu](sql-database-what-is-a-dtu.md)) et les options de stockage toohandle tailles différentes charges de travail et des données. Calcul supplémentaires fournissent des performances supérieures et ressources de stockage conçu la capacité et le débit de plus en plus élevé toodeliver. Vous pouvez modifier les niveaux de service et de performances et le stockage de manière dynamique, sans aucun temps d’arrêt. 
- Les niveaux de service **De base**, **Standard** et **Premium** proposent tous un contrat de niveau de service garantissant un temps d’activité de 99,99 %. Par ailleurs, ils offrent des options de continuité d’activité flexibles, des fonctionnalités de gestion de la sécurité et une facturation à l’heure. 
- Hello **Premium RS** couche fournit hello mêmes niveaux de performances que hello niveau Premium avec un contrat SLA réduit, car il s’exécute avec un nombre inférieur de copies redondantes à une base de données hello autres niveaux de service. Par conséquent, dans l’événement hello défaillance d’un service, vous devrez peut-être toorecover votre base de données d’une sauvegarde avec de décalage de 5 minutes tooa.

> [!IMPORTANT]
> Une base de données SQL Azure obtenait un ensemble de garantie de ressources et hello attendu des caractéristiques de performances de votre base de données ne sont pas affectées par toute autre base de données dans Azure. 

## <a name="choosing-a-service-tier"></a>Choix d’un niveau de service
Hello tableau suivant fournit des exemples de niveaux hello meilleures adaptés pour les charges de travail d’application.

| Niveau de service | Charges de travail cibles |
| :--- | --- |
| **De base** | Idéal pour une petite base de données prenant en général en charge une seule opération active à la fois. Exemple : bases de données utilisées pour le développement ou le test ou pour des applications à petite échelle rarement utilisées. |
| **Standard** |Hello toooption go pour les applications cloud avec les exigences de performances d’e/s toomedium basse, prise en charge de plusieurs requêtes simultanées. Exemple : applications Web ou de groupe de travail. |
| **Premium** | Option conçue pour un volume transactionnel élevé avec de hautes exigences en matière de performances d’E/S, en prenant en charge un grand nombre d’utilisateurs simultanés. Exemple : bases de données prenant en charge des applications critiques. |
| **Premium RS** | Conçu pour les charges de travail gourmandes en e/s qui ne nécessitent pas de garanties de disponibilité le plus élevés hello. Exemples incluent le test des charges de travail hautes performances, ou une charge de travail analytique où la base de données hello n’est pas système hello d’enregistrement. |
|||

Vous pouvez créer des bases de données uniques avec des ressources dédiées au sein d’un niveau de service avec un [niveau de performances](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) spécifique. Vous pouvez aussi créer des bases de données dans un [pool élastique SQL](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus). Dans un pool élastique SQL, les ressources de calcul et de stockage hello sont partagées entre plusieurs bases de données au sein d’un serveur logique unique. 

Les ressources disponibles pour les bases de données uniques sont exprimées en termes d’unités de transaction de base de données (DTU) et celles des pools élastiques, en termes d’unités de transaction de base de données élastique (eDTU). Pour en savoir plus sur les DTU et les eDTU, voir [Explication des unités de transaction de base de données (DTU) et des unités de transaction de base de données élastique (eDTU)](sql-database-what-is-a-dtu.md).

toodecide sur un niveau de service, commencez par déterminer les fonctionnalités de base de données minimale hello dont vous avez besoin :

| **Fonctionnalités de niveau de service** | **De base** | **Standard** | **Premium** | **Premium RS**|
| :-- | --: | --: | --: | --: |
| Taille maximale de la base de données unique | 2 Go | 250 Go | 4 To*  | 500 Go  |
| Taille maximale du pool élastique | 156 Go | 2,9 To | 4 To* | 750 Go |
| Taille maximale de la base de données dans un pool élastique | 2 Go | 250 Go | 500 Go | 500 Go |
| Nombre maximal de bases de données par pool | 500  | 500 | 100 | 100 |
| DTU max de la base de données unique | 5 | 100 | 4000 | 1 000 |
| DTU max de la base de données dans un pool élastique | 5 | 3000 | 4000 | 1 000 |
| Période de rétention de sauvegarde de bases de données | 7 jours | 35 jours | 35 jours | 35 jours |
||||||

> [!IMPORTANT]
> Stockage jusqu'à too4 to est actuellement disponible dans hello suivant régions : nous East2, ouest des États-Unis, nous Gov Virginie, Europe de l’ouest, Allemagne Central, Asie du Sud, l’est du Japon, est de l’Australie, Canada Central et est du Canada. Consultez l’article [Limitations 4 To actuelles](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize).
>

Une fois que vous avez déterminé le niveau de service approprié hello, vous êtes du niveau de performance prêt toodetermine hello (nombre hello de dtu) et la quantité de stockage hello pour la base de données hello. 

- Hello les niveaux de performance S2 et S3 Bonjour **Standard** couche sont souvent un bon point de départ. 
- Pour les bases de données avec des exigences élevées en termes de processeur ou des e/s, hello les niveaux de performance Bonjour **Premium** couche sont point de départ droite hello. 
- Hello **Premium** niveau offre plus d’UC et commence à 10 fois plus d’e/s par rapport toohello plus haut niveau de performances hello **Standard** couche.
- Hello **PremiumRS** niveau offre des performances hello Hello **Premium** couche à un coût moindre, mais avec un contrat SLA de réduction.

> [!IMPORTANT]
> Hello de révision [les pools élastiques SQL](sql-database-elastic-pool.md) pour plus d’informations hello sur le regroupement des bases de données dans élastique SQL pools de ressources de calcul et de stockage tooshare. reste Hello de cette rubrique se concentre sur les niveaux de service et les niveaux de performance des bases de données uniques.
>

## <a name="single-database-service-tiers-and-performance-levels"></a>Niveau de service et niveau de performances d’une base de données unique
Il existe plusieurs niveaux de performances et capacités de stockage au sein de chaque niveau de service pour les bases de données uniques. 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>Mise à l’échelle supérieure ou inférieure d’une base de données unique

Après avoir choisi un niveau de service et un niveau de performances initiaux, vous pouvez mettre à l’échelle supérieure ou inférieure une base de données unique de façon dynamique sur la base de votre expérience concrète.  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

La modification de hello service niveau et/ou les performances au niveau d’une base de données crée un réplica de base de données d’origine hello nouveau niveau de performances hello et bascule ensuite les connexions sur le réplica de toohello. Aucune donnée n’est perdue pendant ce processus, mais pendant hello instants lorsque nous basculer toohello réplica, connexions toohello base de données sont désactivés, certaines transactions en vol peuvent être annulées. Durée Hello pour hello passage varie, mais il est généralement moins de 4 secondes est inférieure à 30 secondes 99 % du temps de hello. S’il existe un grand nombre de transactions en vol au niveau des connexions de moment hello sont désactivées, hello durée pour hello passage peut être plue longue.  

Durée Hello du processus de montée en puissance parallèle entier hello dépend à la fois taille hello et base de données de la couche de service de hello avant et après modification de hello. Par exemple, le basculement d’une base de données de 250 Go vers, depuis ou dans un niveau de service Standard ne demande pas plus de 6 heures. Pour une base de données de hello même taille changement des niveaux de performance au sein de la couche de service Premium hello, il doit se terminer dans les 3 heures.

> [!TIP]
> toocheck sur état hello d’une base de données SQL en cours, opération de mise à l’échelle, vous pouvez utiliser hello suivant la requête : ```select * from sys.dm_operation_status```.
>

* Si vous mettez à niveau tooa couche ou des performances niveau de service, taille maximale de la base de données de hello n’augmente pas, sauf si vous spécifiez explicitement une plus grande taille maximale.
* toodowngrade une base de données, base de données hello doit être inférieure à la taille maximale autorisée hello de niveau de service cible hello. 
* Lors de la mise à niveau une base de données avec [géo-réplication](sql-database-geo-replication-portal.md) activé, mettre à niveau son niveau de performances de votre choix de bases de données secondaires toohello avant la mise à niveau de base de données primaire hello (conseils généraux). Lorsque la mise à niveau tooa autre édition ugrading hello base de données secondaire est tout d’abord requis. 
* Lorsque vous rétrogradez une base de données avec [géo-réplication](sql-database-geo-replication-portal.md) activé, à la rétrogradation de son niveau de performances de votre choix de bases de données primaires toohello avant de rétrograder la base de données secondaire hello (conseils généraux). Lorsque vous rétrogradez tooa autre édition déclassement hello base de données primaire est tout d’abord requis. 

* Hello offres de service de restauration sont différentes pour hello divers niveaux de service. Si vous sont rétrogradation toohello **base** niveau, vous aurez une durée de rétention de sauvegarde inférieure - consultez [les sauvegardes de base de données SQL Azure](sql-database-automated-backups.md).
* Hello nouvelles propriétés de base de données hello ne sont pas appliquées tant que hello modifications ont été effectuées.


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>Limitations actuelles des bases de données P11 et P15 avec une taille maximale de 4 To

Dans certaines régions (précédemment mentionnées), la taille maximale prise en charge est de 4 To pour des bases de données P11 et P15. Hello des considérations et limitations suivantes s’appliquent tooP11 et bases de données P15 avec maxsize de 4 To :

- Si vous choisissez une option maxsize de 4 To hello lors de la création d’une base de données (à l’aide d’une valeur de 4 To ou 4096 Go), hello Créer commande échoue avec une erreur si la base de données hello est déployée dans une région non pris en charge.
- Pour des bases de données P11 et P15 existants situés dans une des régions de hello pris en charge, vous pouvez augmenter hello maxsize stockage too4 to. Cela peut être vérifiée à l’aide de hello [sélectionner les DATABASEPROPERTYEX](https://msdn.microsoft.com/library/ms186823.aspx) ou en examinant la taille de base de données de hello en hello portail Azure. La mise à niveau un P11 existant ou un P15 base de données ne peut être effectuée par une connexion du principal au niveau du serveur ou par les membres du rôle de base de données dbmanager hello. 
- Si une opération de mise à niveau est exécutée dans une configuration de hello région prise en charge est immédiatement mis à jour. base de données Hello reste en ligne pendant le processus de mise à niveau hello. Toutefois, vous ne peut pas utiliser hello complète 4 To de stockage jusqu'à ce que les fichiers de base de données réelle hello ont été mis à niveau maxsize de nouveau toohello. longueur Hello temps nécessaire dépend de taille hello de mise à niveau de la base de données hello.  
- Lors de la création ou de la mise à jour d’une base de données P11 ou P15, vous n’avez le choix qu’entre les tailles maximales de 1 To ou de 4 To. Les tailles de stockage intermédiaires ne sont actuellement pas prises en charge. Lorsque vous créez un P11/P15, option de stockage hello par défaut de 1 To est présélectionnée. Pour les bases de données situées dans une des régions de hello pris en charge, vous pouvez augmenter too4TB maximale de stockage hello pour une nouvelle ou existante base de données. Pour toutes les autres régions, la taille maximale ne peut pas être supérieure à 1 To. les prix Hello ne changent pas lorsque vous sélectionnez 4 To de stockage inclus.
- Hello maxsize de base de données de 4 To ne peut pas être modifié too1 to même si stockage actuel de hello utilisé est inférieur à 1 To. Par conséquent, vous ne pouvez pas rétrograder un tooa P11 - 4/P15 - 4 To P11 - 1 to/P15 - 1 To ou un niveau de performances inférieur, par exemple, tooP1-P6) jusqu'à ce que nous fournissons des options de stockage supplémentaire pour reste hello Hello niveaux de performances. Cette restriction s’applique également toohello restauration et scénarios, y compris le point-à-temps, la géo-restauration, long-terme sauvegarde-rétention et la copie de base de données. Une fois qu’une base de données est configuré avec l’option de 4 To hello, toutes les opérations de restauration de cette base de données doivent être exécutées dans un P11/P15 avec maxsize de 4 To.
- Lorsque la création ou la mise à niveau une base de données dans une région non pris en charge, P11/P15 hello créez ou la mise à niveau échoue avec hello message d’erreur suivant : **P11 et P15 base de données avec des too4TB de stockage sont disponibles dans nous East2, ouest des États-Unis, nous Gov Virginie, Europe de l’ouest, centre de l’Allemagne, Asie du Sud-est, est du Japon, est de l’Australie, centre du Canada et est du Canada.**
- Pour les scénarios de géoréplication active :
   - Configuration d’une relation de géo-réplication : si la base de données primaire hello est P11 ou P15, hello secondary(ies) doit également être P11 ou P15 ; les niveaux de performances inférieurs sont rejetées en tant que bases de données secondaires, car ils ne sont pas capables de prendre en charge de 4 To.
   - La mise à niveau hello base de données primaire dans une relation de géo-réplication : modification hello maxsize too4 to sur une base de données principal déclenche hello même modifier sur la base de données secondaire hello. Les deux mises à niveau doivent être établies pour modification hello sur l’effet de tootake principal hello. Région pour l’option de 4 To hello présente les limitations (voir ci-dessus). Si hello secondaire dans une région qui ne prend pas en charge les 4 To, hello principal n’est pas mis à niveau.
- À l’aide du service d’importation/exportation hello pour le chargement des bases de données P11 - 4/P15 - 4 To n’est pas pris en charge. Utiliser trop de SqlPackage.exe[importer](sql-database-import.md) et [exporter](sql-database-export.md) données.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-portal"></a>Gérer les niveaux de service de base de données unique et les niveaux de performances à l’aide de hello portail Azure

tooset ou modification hello de niveau de service, de niveau de performance ou de quantité de stockage pour une base de SQL Azure nouveau ou existante à l’aide de hello portail Azure, ouvrez hello **configuration des performances** fenêtre pour votre base de données en cliquant sur  **Niveau de tarification (échelle dtu)** - comme indiqué dans hello suivant capture d’écran. 

- Définissez ou modifiez le niveau de service hello en sélectionnant le niveau de service hello pour votre charge de travail. 
- Définir ou modifier le niveau de performance hello (**dtu**) au sein d’un niveau de service à l’aide de hello **DTU** curseur.
- Définir ou modifier la quantité de stockage hello pour le niveau de performances à l’aide de hello hello **stockage** curseur. 

  ![Configurer le niveau de service et le niveau de performances](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> Parcourez la section [Limitations actuelles des bases de données P11 et P15 avec une taille maximale de 4 To](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize) lors de la sélection d’un niveau de service P11 ou P15.
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>Gérer les niveaux de service et les niveaux de performances d’une base de données unique via PowerShell

niveaux de service de bases de données SQL Azure tooset ou modifier les niveaux de performance et quantité de stockage à l’aide de PowerShell, utilisent hello suivant d’applets de commande PowerShell. Si vous avez besoin de tooinstall ou mise à niveau de PowerShell, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps). 

| Applet de commande | Description |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Crée une base de données |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Obtient une ou plusieurs bases de données|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Définit les propriétés d’une base de données, ou déplace une base de données existante dans un pool élastique|


> [!TIP]
> Pour un exemple de script PowerShell qui surveille les métriques de performances hello d’une base de données, il ajuste le niveau de performance supérieur tooa et crée une règle d’alerte sur l’une des mesures de performance hello, consultez [analyse et mise à l’échelle un seul SQL de la base de données à l’aide de PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-cli"></a>Gérer les niveaux de service de base de données unique et les niveaux de performances à l’aide de hello CLI d’Azure

niveaux de service de bases de données SQL Azure tooset ou modifier les niveaux de performance et quantité de stockage à l’aide de hello CLI d’Azure, utilisent des éléments suivants de hello [base de données SQL Azure CLI](/cli/azure/sql/db) commandes. Hello d’utilisation [Cloud Shell](/azure/cloud-shell/overview) toorun hello CLI dans votre navigateur, ou [installer](/cli/azure/install-azure-cli) sur Windows, Linux ou macOS. Pour créer et gérer les pools élastiques SQL, voir [Pools élastiques](sql-database-elastic-pool.md).

| Applet de commande | Description |
| --- | --- |
|[az sql db create](/cli/azure/sql/db#create) |Crée une base de données|
|[az sql db list](/cli/azure/sql/db#list)|Répertorie toutes les bases de données et les entrepôts de données d’un serveur, ou toutes les bases de données d’un pool élastique|
|[az sql db list-editions](/cli/azure/sql/db#list-editions)|Répertorie les objectifs de service disponibles et les limites de stockage|
|[az sql db list-usages](/cli/azure/sql/db#list-usages)|Renvoie les données d’utilisation de la base de données|
|[az sql db show](/cli/azure/sql/db#show)|Obtient une base de données ou un entrepôt de données|
|[az sql db update](/cli/azure/sql/db#update)|Met à jour une base de données|

> [!TIP]
> Pour un exemple de script CLI d’Azure qui met à l’échelle un niveau de performance différents de tooa de base de données SQL Azure unique après interrogation des informations sur la taille de base de données hello hello, consultez [utilisez CLI toomonitor et l’échelle une base de données SQL](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>Gérer es niveaux de service et les niveaux de performances d’une base de données unique via Transact-SQL

niveaux de service de bases de données SQL Azure tooset ou modifier les niveaux de performance et la quantité de stockage avec Transact-SQL, utilisent hello suivant de commandes T-SQL. Vous pouvez émettre ces commandes à l’aide du portail Azure, de hello [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), ou tout autre programme qui peut se connecter le serveur de base de données SQL Azure tooan et passer Transact-SQL commandes. 

| Commande | Description |
| --- | --- |
|[CREATE DATABASE (Azure SQL Database)](/sql/t-sql/statements/create-database-azure-sql-database)|Crée une base de données. Vous devez être connecté toohello base de données master toocreate une base de données.|
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modifie une base de données SQL Azure. |
|[sys.database_service_objectives (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Retourne hello edition (niveau de service), objectif de service (niveau de tarification) et nom du pool élastique, le cas échéant, pour une base de données SQL Azure ou d’un entrepôt de données SQL Azure. Si une session toohello la base de données master sur un serveur de base de données SQL Azure, retourne des informations sur toutes les bases de données. Pour l’entrepôt de données SQL Azure, vous devez être connecté toohello de base de données master.|
|[sys.database_usage (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|Répertorie le nombre de hello, type et la durée des bases de données sur un serveur de base de données SQL Azure.|

exemple Hello présente hello maxsize en cours de modification à l’aide de la commande ALTER DATABASE hello :

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-hello-rest-api"></a>Gérer les bases de données uniques à l’aide des API REST de hello

tooset ou modification de niveaux de service de bases de données SQL Azure, les niveaux de performance et la quantité de stockage à l’aide de hello API REST, consultez [API REST de Azure SQL Database](/rest/api/sql/).

## <a name="next-steps"></a>Étapes suivantes

* En savoir plus sur les [DTU](sql-database-what-is-a-dtu.md).
* toolearn sur la surveillance de l’utilisation DTU, consultez [de surveillance et de réglage des performances](sql-database-troubleshoot-performance.md).

