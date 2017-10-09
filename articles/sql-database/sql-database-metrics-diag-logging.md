---
title: "aaaAzure SQL de la base de données des métriques et la journalisation des diagnostics | Documents Microsoft"
description: "En savoir plus sur la configuration de l’utilisation des ressources Azure SQL Database ressource toostore, la connectivité et des statistiques d’exécution de requête."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a>Journalisation des métriques et diagnostics d’Azure SQL Database 
Azure SQL Database peut émettre des journaux de métriques et de diagnostics pour faciliter la surveillance. Vous pouvez configurer l’utilisation des ressources toostore base de données SQL Azure, aux employés et les sessions et connectivité dans une de ces ressources Azure :
- **Stockage Azure** : pour archiver des quantités importantes de données de télémétrie à un petit prix
- **Azure Event Hub** : pour intégrer des données de télémétrie Azure SQL Database à votre solution de surveillance personnalisée ou à vos pipelines très actifs
- **Azure Analytique de journal**: pour prédéfinies hello solution avec reporting, de génération d’alertes et de limiter les fonctionnalités de surveillance 

    ![architecture](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a>Activation de la journalisation

La journalisation des métriques et diagnostics n’est pas activée par défaut. Vous pouvez activer et gérer des mesures et journalisation des diagnostics à l’aide d’une des méthodes suivantes de hello :
- Portail Azure
- PowerShell
- Interface de ligne de commande Azure
- API REST 
- Modèle Resource Manager

Lorsque vous activez les métriques et la journalisation des diagnostics, vous devez toospecify hello ressource Azure où les données sélectionnées sont collectées. Options disponibles :
- Log Analytics
- Event Hub
- Stockage Azure 

Vous pouvez approvisionner une nouvelle ressource Azure ou sélectionner une ressource existante. Après avoir sélectionné la ressource de stockage hello, vous devez toospecify le toocollect de données. Les options disponibles sont les suivantes :

- **[Métriques de 1 minute](sql-database-metrics-diag-logging.md#1-minute-metrics)** : contient Pourcentage DTU, Limite DTU, Pourcentage UC, Pourcentage de lecture de données physiques, Pourcentage d’écriture du journal, Connexions réussies/en échec/bloquées par pare-feu, Pourcentage de sessions, Pourcentage de workers, Stockage, Pourcentage de stockage, Pourcentage de stockage XTP

Si vous spécifiez un compte de AzureStorage ou de concentrateur d’événements, vous pouvez spécifier un toospecify de stratégie de rétention de données qui est antérieures à la période de temps sélectionné est supprimé. Si vous spécifiez Analytique de journal, stratégie de rétention hello dépend de niveau de tarification sélectionné hello. Pour en savoir plus, voir [Tarification de Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/). 

Nous vous recommandons de lire les deux hello [vue d’ensemble des métriques dans Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) et [vue d’ensemble de Azure des journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) les articles toogain comprendre non seulement comment journalisation tooenable, mais hello les catégories de journaux et les mesures prises en charge par hello divers services Azure.

### <a name="azure-portal"></a>Portail Azure

métriques de tooenable et de collection de journaux de diagnostic Bonjour portail Azure, accédez de base de données SQL Azure tooyour ou page de pool élastique, puis cliquez sur **les paramètres de Diagnostic**.

   ![Activer Bonjour portail Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a>PowerShell

tooenable métriques et la journalisation des diagnostics à l’aide de PowerShell, utilisez hello suivant de commandes :

- stockage tooenable de journaux de Diagnostic dans un compte de stockage, utilisez cette commande :

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   Hello ID de compte de stockage concerne les id de ressource hello toowhich de compte de stockage hello souhaité toosend hello se connecte.

- tooenable de diffusion en continu de journaux de Diagnostic tooan concentrateur d’événements, utilisez la commande :

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   Hello ID de règle de Bus de Service est une chaîne au format suivant :

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- Utilisez la commande tooenable envoi de journaux de Diagnostic tooa Analytique de journal espace de travail :

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- Vous pouvez obtenir l’id de ressource hello de votre espace de travail Analytique des journaux à l’aide de hello de commande suivante :

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

Vous pouvez combiner ces paramètres tooenable plusieurs options de sortie.

### <a name="cli"></a>Interface de ligne de commande

métriques de tooenable et à l’aide de la journalisation de diagnostics hello CLI d’Azure, hello utilisation suivant de commandes :

- stockage tooenable de journaux de Diagnostic dans un compte de stockage, utilisez cette commande :

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   Hello ID de compte de stockage concerne les id de ressource hello toowhich de compte de stockage hello souhaité toosend hello se connecte.

- tooenable de diffusion en continu de journaux de Diagnostic tooan concentrateur d’événements, utilisez la commande :

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   Hello ID de règle de Bus de Service est une chaîne au format suivant :

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- Utilisez la commande tooenable envoi de journaux de Diagnostic tooa Analytique de journal espace de travail :

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

Vous pouvez combiner ces paramètres tooenable plusieurs options de sortie.

### <a name="rest-api"></a>API REST

Découvrez comment trop[modifier les paramètres de Diagnostic à l’aide de hello API REST de Azure analyse](https://msdn.microsoft.com/library/azure/dn931931.aspx). 

### <a name="resource-manager-template"></a>Modèle Resource Manager

Découvrez comment trop[activer les paramètres de Diagnostic lors de la création de ressources à l’aide du Gestionnaire de ressources du modèle](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md). 

## <a name="stream-into-log-analytics"></a>Envoyer à Log Analytics 
Les journaux de diagnostic et les mesures de base de données SQL Azure peuvent être diffusés en Analytique de journal à l’aide d’option intégrée « envoi » tooLog Analytique de hello dans le portail de hello, ou en activant l’Analytique des journaux dans un paramètre de diagnostic via les applets de commande Azure PowerShell, CLI d’Azure ou Azure moniteur reste API.

### <a name="installation-overview"></a>Vue d’ensemble de l’installation

La surveillance d’une flotte Azure SQL Database est simple avec Log Analytics. Trois étapes sont requises :

1.  Créer une ressource Log Analytics
2.  Configurer des métriques de toorecord de bases de données et les journaux de diagnostic dans hello créé Analytique de journal
3.  Installer la solution **Azure SQL Analytics** à partir de la galerie de Log Analytics

### <a name="create-log-analytics-resource"></a>Créer une ressource Log Analytics

1. Cliquez sur **nouveau** dans le menu de gauche hello.
2. Cliquez sur **Surveillance et gestion**.
3. Cliquez sur **Log Analytics**.
4. Remplissez hello Analytique de journal formulaire avec des informations supplémentaires hello requis : nom de l’espace de travail, abonnement, groupe de ressources, l’emplacement et niveau de tarification.

   ![Log Analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a>Configurer des métriques de toorecord de bases de données et les journaux de diagnostic

Hello tooconfigure de façon plus simple où les bases de données enregistrent leurs mesures est hello portail Azure. Dans hello portail Azure, accédez de ressource de base de données SQL Azure tooyour et cliquez sur **paramètres de diagnostic**. 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a>Installer la solution d’Analytique de SQL Azure hello à partir de la galerie  

1. Une fois hello ressource d’Analytique de journal est créée et vos données circulent dans celui-ci, installer des solutions d’Analytique de SQL Azure. Cela peut être effectué à partir de hello **galerie des Solutions** que vous pouvez trouver sur la page d’accueil de hello OMS et dans le menu latéral de hello. Dans la galerie hello, recherchez et cliquez sur **Analytique de SQL Azure** solution et cliquez sur **ajouter**.

   ![solution de surveillance](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. Dans votre page d’accueil de Microsoft Operations Management Suite, une nouvelle vignette intitulée **Azure SQL Analytics** s’affiche. En sélectionnant cette vignette, tableau de bord hello Analytique de SQL Azure s’ouvre.

### <a name="using-azure-sql-analytics-solution"></a>Utilisation de la solution Azure SQL Analytics

Analytique de SQL Azure est un tableau de bord hiérarchique qui vous permet de toonavigate via la hiérarchie de hello de ressources de la base de données SQL Azure. Cela permet de capacité vous toodo principales analyse également, mais il vous permet de tooscope votre droit de hello toojust analyse jeu de ressources.
Tableau de bord contient des listes de hello de différentes ressources sous la ressource de hello sélectionné. Par exemple, pour un abonnement sélectionné, vous pouvez voir hello tous les serveurs, les pools élastiques et les bases de données qui appartiennent toohello sélectionné l’abonnement. En outre, pour les bases de données et les Pools élastiques, vous pouvez voir les métriques d’utilisation de ressources hello d’une ressource. Celles-ci incluent des graphiques pour DTU, UC, E/S, journal, sessions, workers, connexions et stockage en Go.

## <a name="stream-into-azure-event-hub"></a>Envoyer à Azure Event Hub

Les journaux de diagnostic et les mesures de base de données SQL Azure peuvent être diffusés à un concentrateur d’événements à l’aide d’option d’intégré « flux tooan concentrateur d’événements » hello dans le portail de hello, ou en activant l’Id de règle de Bus de Service dans un paramètre de diagnostic via les applets de commande PowerShell Azure, CLI d’Azure ou Azure moniteur reste API. 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a>Quelles toodo avec des métriques et des journaux de diagnostic dans le concentrateur d’événements ?
Une fois que les données de salutation sélectionnée sont diffusée en continu dans le concentrateur d’événements, vous êtes un tooenabling proche étape des scénarios d’analyses avancés. Concentrateurs d’événements joue le rôle hello « porte d’entrée » pour un pipeline d’événements, et une fois que les données sont collectées dans un concentrateur d’événements, il peut être transformé et stockées à l’aide de n’importe quel fournisseur analytique en temps réel ou des cartes de traitement par lot/stockage. Concentrateurs d’événements dissocie production hello d’un flux d’événements à partir de la consommation de ces événements, hello afin que les consommateurs d’événements peuvent accéder à des événements de hello sur leur propre calendrier. Pour plus d’informations sur Event Hub, voir :

- [Qu’est-ce qu’Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) ?
- [Prise en main des hubs d’événements](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


Voici quelques méthodes que vous pouvez utiliser la capacité de diffusion en continu de hello :

-   Afficher l’intégrité du service par diffusion en continu de « chemin réactif » données tooPowerBI - concentrateurs d’événements à l’aide de flux Analytique et Power BI, vous pouvez facilement transformer vos données métriques et des diagnostics dans près des informations en temps réel sur vos services Azure. Pour une vue d’ensemble du mode de tooset d’un service Event Hubs, traiter les données avec le flux de données Analytique et utiliser Power BI comme sortie, consultez [Analytique de flux de données et Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).
-   Flux de données des journaux toothird tiers journalisation et les données de télémétrie flux – concentrateurs d’événements à l’aide de diffusion en continu vous peuvent obtenir de vos mesures et les journaux de diagnostic dans toodifferent des journaux et surveillance analytique solutions tierces. 
-   Générer une télémétrie personnalisée et la plateforme de journalisation : Si vous disposez déjà d’une plateforme de télémétrie personnalisées ou sont simplement penser à la génération 1, hello hautement évolutive de publication / abonnement nature des concentrateurs d’événements vous permet de tooflexibly d’acquisition des journaux de diagnostic. Consultez [toousing de guide de Dan Rosanova concentrateurs d’événements dans une plateforme de télémétrie à l’échelle mondiale](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="stream-into-azure-storage"></a>Envoyer à Stockage Azure

Les journaux de diagnostic et les mesures de base de données SQL Azure peuvent être stockées dans le stockage Azure à l’aide de l’option des « Archiver le compte de stockage tooa » hello intégrée Bonjour portail Azure, ou en activant le stockage Azure dans un paramètre de diagnostic via les applets de commande PowerShell Azure, CLI d’Azure ou Azure API REST de moniteur.

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a>Schéma des métriques et des journaux de diagnostic dans le compte de stockage hello

Une fois que vous avez configuré des mesures et de collection de journaux de diagnostic, un conteneur de stockage est créé dans le compte de stockage hello sélectionné lorsque hello premières lignes de données sont disponibles. structure Hello de ces objets BLOB est la suivante :

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
Ou, plus simplement :

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

Par exemple, un nom d’objet blob pour des métriques sur 1 minute pourrait être :

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

Au cas où vous souhaiteriez données hello toorecord hello Pool élastique, le nom d’objet blob est un peu différent :

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a>Télécharger les métriques et journaux de Stockage Azure

Consultez [Télécharger les journaux de métriques et diagnostics de Stockage Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs).

## <a name="1-minute-metrics"></a>Métriques de 1 minute

| |  |
|---|---|
|**Ressource**|**Métriques**|
|Base de données|Pourcentage DTU, Limite DTU, Pourcentage UC, Pourcentage de lecture de données physiques, Pourcentage d’écriture du journal, Connexions réussies/en échec/bloquées par pare-feu, Pourcentage de sessions, Pourcentage de workers, Stockage, Pourcentage de stockage, Pourcentage de stockage XTP, blocages |
|Pool élastique|Pourcentage DTU, eDTU utilisé, Limite eDTU, Pourcentage UC, Pourcentage de lecture de données physiques, Pourcentage d’écriture du journal, Pourcentage de sessions, Pourcentage de workers, Stockage, Pourcentage de stockage, Limite de stockage, Pourcentage de stockage XTP |
|||

## <a name="next-steps"></a>Étapes suivantes

- Lire les deux hello [vue d’ensemble des métriques dans Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) et [vue d’ensemble de Azure des journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain comprendre non seulement comment tooenable journalisation, mais hello métriques et connecter les catégories prise en charge par hello divers services Azure.
- Lisez ces toolearn des articles sur les concentrateurs d’événements :
   - [Qu’est-ce qu’Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) ?
   - [Prise en main des hubs d’événements](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- Consultez [Télécharger les journaux de métriques et diagnostics de Stockage Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs).
