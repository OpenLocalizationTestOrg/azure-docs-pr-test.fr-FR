---
title: aaaAzure solution SQL Analytique de journal Analytique | Documents Microsoft
description: "Hello solution d’Analytique de SQL Azure permet de gérer vos bases de données SQL Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>Surveiller Azure SQL Database à l’aide d’Azure SQL Analytics (version préliminaire) dans Log Analytics

![Symbole Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-symbol.png)

Hello solution Analytique de SQL Azure dans Azure journal Analytique collecte et visualise les métriques de performances importantes SQL Azure. À l’aide de mesures hello que vous recueillez avec la solution de hello, vous pouvez créer des alertes et des règles d’analyse personnalisés. Par ailleurs, vous pouvez surveiller les mesures associées à Azure SQL Database et aux pools élastiques au sein de plusieurs abonnements Azure et pools élastiques, et afficher ces données. solution de Hello vous aide également à tooidentify des problèmes au niveau de chaque couche de la pile de votre application.  Il utilise [métriques des diagnostics Azure](log-analytics-azure-storage.md) avec Analytique de journal consulte des données de toopresent sur toutes les bases de données SQL Azure et les pools élastiques dans un seul espace de travail Analytique de journal.

Actuellement, cette solution de la version préliminaire prend en charge des too150, des bases de données Azure SQL 000 et 5 000 Pools élastiques SQL par espace de travail.

Hello solution Analytique de SQL Azure, comme d’autres disponibles pour l’Analytique des journaux, permet de surveiller et de recevoir des notifications sur le contrôle d’intégrité hello de vos ressources Azure, dans ce cas, la base de données SQL Azure. Base de données SQL Microsoft Azure est un service de base de données relationnelle évolutif qui fournit familiers tooapplications de fonctionnalités similaire à SQL Server en cours d’exécution dans hello cloud Azure. Analytique de journal vous permet de toocollect, mettre en corrélation et visualiser les données structurées et non structurées.

## <a name="connected-sources"></a>Sources connectées

Hello solution d’Analytique de SQL Azure n’utilise pas d’agents tooconnect toohello service d’Analytique de journal.

Hello tableau suivant décrit les sources de hello connecté sont pris en charge par cette solution.

| Source connectée | Support | Description |
| --- | --- | --- |
| [Agents Windows](log-analytics-windows-agents.md) | Non | Les agents Windows directs ne sont pas utilisés par la solution de hello. |
| [Agents Linux](log-analytics-linux-agents.md) | Non | Les agents Linux directs ne sont pas utilisés par la solution de hello. |
| [Groupe d’administration SCOM](log-analytics-om-agents.md) | Non | Une connexion directe à partir de hello SCOM agent tooLog Analytique n’est pas utilisée par la solution de hello. |
| [Compte Azure Storage](log-analytics-azure-storage.md) | Non | Analytique de journal ne lit pas les données de salutation à partir d’un compte de stockage. |
| [Diagnostics Azure](log-analytics-azure-storage.md) | Oui | Les données de mesure Azure sont envoyées tooLog Analytique directement par Azure. |

## <a name="prerequisites"></a>Composants requis

- Un abonnement Azure. Si vous n’en avez pas, créez-en un [gratuitement](https://azure.microsoft.com/free/).
- Un espace de travail Log Analytics. Vous pouvez utiliser un élément existant, ou en [créez un nouveau](log-analytics-get-started.md) avant de commencer à utiliser cette solution.
- Activer les Diagnostics de Azure pour vos bases de données SQL Azure et les pools élastiques et [toosend les configurer leur tooLog données Analytique](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).

## <a name="configuration"></a>Configuration

Effectuer hello suivant l’espace de travail suit tooadd hello Analytique de SQL Azure solution tooyour.

1. Ajouter l’espace de travail tooyour hello pour Azure SQL Analytique solution à partir de [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).
2. Bonjour portail Azure, cliquez sur **nouveau** (hello + symbole), puis dans la liste de hello des ressources, sélectionnez **analyse + gestion**.  
    ![Surveillance et gestion](./media/log-analytics-azure-sql/monitoring-management.png)
3. Bonjour **analyse + gestion** liste **afficher tous les**.
4. Bonjour **recommandé** , cliquez sur **plus** et dans la nouvelle liste de hello, recherchez **Analytique de SQL Azure (aperçu)** et sélectionnez-le.  
    ![Solution Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. Bonjour **Analytique de SQL Azure (aperçu)** panneau, cliquez sur **créer**.  
    ![Créer](./media/log-analytics-azure-sql/portal-create.png)
6. Bonjour **créer une nouvelle solution** panneau, espace de travail hello select que vous souhaitez tooadd hello solution tooand, puis cliquez sur **créer**.  
    ![Ajouter tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="tooconfigure-multiple-azure-subscriptions"></a>tooconfigure plusieurs abonnements Azure

toosupport plusieurs abonnements, utiliser hello PowerShell script [journalisation de métriques de ressources Azure d’activer à l’aide de PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/). Indiquez l’ID de ressource d’espace de travail hello en tant que paramètre lors de l’exécution des données de diagnostic hello script toosend à partir des ressources dans l’espace de travail d’un abonnement Azure tooa dans un autre abonnement Azure.

**Exemple**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a>À l’aide de la solution de hello

Lorsque vous ajoutez d’espace de travail hello solution tooyour, hello Analytique de SQL Azure vignette est ajouté tooyour espace de travail, et elle s’affiche dans la vue d’ensemble. vignette de Hello montre nombre hello de bases de données SQL Azure et les pools élastiques SQL Azure qui les solutions hello sont connectée à.

![Vignette Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>Affichage des données Azure SQL Analytics

Cliquez sur hello **Analytique de SQL Azure** tableau de bord vignette tooopen hello Analytique de SQL Azure. tableau de bord Hello inclut les panneaux hello défini ci-dessous. Chaque panneau répertorie les ressources too15 (abonnement serveur, pool élastique et base de données). Cliquez sur un tableau de bord hello hello pour ressources tooopen pour cette ressource spécifique. Pool élastique ou base de données contient des graphiques de hello de mesures pour une ressource sélectionnée. Cliquez sur une boîte de dialogue graphique tooopen hello recherche de journal.

| Panneau | Description |
|---|---|
| Abonnements | Liste des abonnements avec le nombre de bases de données, de pools et de serveurs connectés. |
| Serveurs | Liste des serveurs avec le nombre de bases de données et de pools connectés. |
| Pools élastiques | Liste des pools d’élastiques connectés avec maximale Go et eDTU Bonjour observé de période. |
|Bases de données | Liste des bases de données connectées avec Go et les DTU maximale BONJOUR observé période.|


### <a name="analyze-data-and-create-alerts"></a>Analyser les données et créer des alertes

Vous pouvez facilement créer des alertes avec les données hello provenant des ressources de base de données SQL Azure. Voici quelques requêtes utiles de [Recherche dans les journaux](log-analytics-log-searches.md) que vous pouvez utiliser pour créer des alertes :

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


*DTU élevé sur Azure SQL Database*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

*DTU élevé sur un pool élastique Azure SQL Database*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

Vous pouvez utiliser ces tooalert les requêtes basées sur une alerte sur les seuils spécifiques pour la base de données SQL Azure et de pools élastiques. tooconfigure une alerte pour votre espace de travail OMS :

#### <a name="tooconfigure-an-alert-for-your-workspace"></a>tooconfigure une alerte pour votre espace de travail

1. Accédez toohello [portail OMS](http://mms.microsoft.com/) et connectez-vous.
2. Ouvrez l’espace de travail hello que vous avez configuré pour la solution de hello.
3. Sur la page de vue d’ensemble de hello, cliquez sur hello **Analytique de SQL Azure (aperçu)** vignette.
4. Exécutez une des requêtes d’exemple hello.
5. Dans la recherche dans les journaux, cliquez sur **Alerte**.  
![création d’une alerte dans la recherche](./media/log-analytics-azure-sql/create-alert01.png)
6. Sur hello **ajouter une règle d’alerte** page, configurez les propriétés appropriées hello et hello seuils spécifiques que vous souhaitez puis cliquez sur **enregistrer**.  
![ajout d’une règle d’alerte](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>Utilisation des données Azure SQL Analytics

Par exemple, une des requêtes les plus utiles hello que vous pouvez effectuer est utilisation de DTU toocompare hello pour tous les Pools élastiques de SQL Azure dans tous vos abonnements Azure. Unités de débit de base de données (UDBD) fournit un moyen toodescribe hello capacité relative d’un niveau de performance des bases de données basique, Standard et Premium et les pools. Les DTU sont une mesure combinant la quantité d’UC, la mémoire, les lectures et les écritures. À mesure que les dtu augmentent, hello puissance offerte par les augmentations de niveau de performances hello. Par exemple un niveau de performance avec 5 DTU présente une puissance 5 fois supérieure à un niveau de performance affichant 1 DTU. Un quota DTU maximal s’applique tooeach les pool élastique et le serveur.

Par hello suivant la requête de recherche de journal en cours d’exécution, vous pouvez facilement déterminer si vous êtes moteur ou plus en utilisant vos pools élastiques SQL Azure.

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello au-dessus de requête pourrait être modifié toohello suivant.
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

Bonjour l’exemple suivant, vous pouvez voir qu’un pool élastique a une utilisation élevée proche de 100 % tandis que d’autres personnes ont très peu d’utilisation DTU. Vous pouvez examiner les modifications récentes potentiels tootroubleshoot supplémentaires dans votre environnement à l’aide des journaux d’activité d’Azure.

![Résultats de la recherche dans les journaux - Utilisation élevée](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>Voir aussi

- Utilisez [recherches de journal](log-analytics-log-searches.md) dans tooview d’Analytique de journal détaillé les données de SQL Azure.
- [Créer un tableau de bord personnalisé](log-analytics-dashboards.md) comportant les données Azure SQL.
- [Create and manage alert rules in Log Analytics with the OMS portal](log-analytics-alerts.md) (Créer et gérer des règles d’alerte dans Log Analytics dans Log Analytics à l’aide du portail OMS).
