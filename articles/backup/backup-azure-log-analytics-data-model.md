---
title: "modèle de données Analytique aaaLog pour la sauvegarde Azure"
description: "Cet article présente des informations détaillées sur le modèle de données Log Analytics pour les données de sauvegarde Azure."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: dfd5c73d-0d34-4d48-959e-1936986f9fc0
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 04ac16e38b896851f60b1c4ffbea4343347ae32c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-model-for-azure-backup-data"></a>Modèle de données Log Analytics pour les données de sauvegarde Azure
Cet article décrit le modèle de données hello utilisé pour pousser des rapports tooLog données Analytique. À l’aide de ce modèle de données, vous pouvez créer des requêtes personnalisées, des tableaux de bord et les utiliser dans OMS. 

## <a name="using-azure-backup-data-model"></a>Utilisation du modèle de données de sauvegarde Azure
Vous pouvez utiliser hello suivant des champs fournis dans le cadre des éléments visuels toocreate du modèle de données hello, des requêtes personnalisées et du tableau de bord en fonction de vos besoins.

### <a name="alert"></a>Alerte
Ce tableau fournit plus d’informations sur les champs liés aux alertes.

| Champ | Type de données | Description |
| --- | --- | --- |
| AlertUniqueId_s |Texte |Id unique de hello a généré l’alerte |
| AlertType_s |Texte |Type Hello a généré l’alerte, par exemple, sauvegarde |
| AlertStatus_s |Texte |État d’alerte hello, par exemple, Active |
| AlertOccurenceDateTime_s |Date/Heure |Date et heure de la création de l’alerte |
| AlertSeverity_s |Texte |Gravité d’alerte hello, par exemple, critique |
| EventName_s |Texte |Ce champ représente le nom de cet événement, qui est toujours AzureBackupCentralReport |
| BackupItemUniqueId_s |Texte |Id unique de toowhich de sauvegarder l’élément hello que cette alerte appartient trop|
| SchemaVersion_s |Texte |Ce champ indique la version actuelle du schéma de hello, il est **V1** |
| State_s |Texte |État actuel de l’objet alert hello, par exemple, actif, supprimé |
| BackupManagementType_s |Texte |Type de fournisseur pour la sauvegarde, par exemple, IaaSVM, toowhich FileFolder cette alerte appartient trop|
| Nom d'opération |Texte |Ce champ représente le nom de l’opération en cours hello - alerte |
| Catégorie |Texte |Ce champ représente la catégorie de données de diagnostic poussées tooLog Analytique, il est AzureBackupReport |
| Ressource |Texte |Il s’agit des ressources hello pour lequel les données sont collectées, il affiche le nom du coffre Recovery Services |
| ProtectedServerUniqueId_s |Texte |Id unique de hello protégé toowhich que cette alerte appartient trop|
| VaultUniqueId_s |Texte |Id unique de hello protégé toowhich que cette alerte appartient trop|
| SourceSystem |Texte |Système de source de données actuelle hello - Azure |
| ResourceId |Texte |Ce champ représente l’ID de la ressource pour laquelle les données sont collectées ; affiche l’ID du coffre Recovery Services |
| SubscriptionId |Texte |Ce champ représente l’id d’abonnement de ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceGroup |Texte |Ce champ représente le groupe de ressources de la ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceProvider |Texte |Ce champ représente hello fournisseur de ressources pour lequel les données sont en cours collectées - Microsoft.RecoveryServices |
| ResourceType |Texte |Ce champ représente le type de ressource de hello pour lesquels les données sont en cours collectées - coffres |

### <a name="backupitem"></a>BackupItem
Ce tableau fournit plus d’informations sur les champs liés aux éléments de sauvegarde.

| Champ | Type de données | Description |
| --- | --- | --- |
| EventName_s |Texte |Ce champ représente le nom de cet événement, qui est toujours AzureBackupCentralReport |  
| BackupItemUniqueId_s |Texte |Id unique de l’élément de sauvegarde hello |
| BackupItemId_s |Texte |ID de l’élément de sauvegarde |
| BackupItemName_s |Texte |Nom de l’élément de sauvegarde |
| BackupItemFriendlyName_s |Texte |Nom convivial de l’élément de sauvegarde |
| BackupItemType_s |Texte |Type d’élément de sauvegarde, par exemple, Machine virtuelle, Dossier de fichiers |
| ProtectedServerName_s |Texte |Nom du serveur protégé toowhich sauvegarder l’élément appartient trop|
| ProtectionState_s |Texte |État de protection actuel d’élément de sauvegarde hello, par exemple, protégé, ProtectionStopped |
| SchemaVersion_s |Texte |Ce champ indique la version actuelle du schéma de hello, il est **V1** |
| State_s |Texte |État actuel de hello sauvegarder l’élément objet, par exemple, actif, supprimé |
| BackupManagementType_s |Texte |Type de fournisseur pour la sauvegarde, par exemple, IaaSVM, toowhich FileFolder appartient trop de cet élément de sauvegarde|
| Nom d'opération |Texte |Ce champ représente le nom de l’opération en cours hello - BackupItem |
| Catégorie |Texte |Ce champ représente la catégorie de données de diagnostic poussées tooLog Analytique, il est AzureBackupReport |
| Ressource |Texte |Il s’agit des ressources hello pour lequel les données sont collectées, il affiche le nom du coffre Recovery Services |
| SourceSystem |Texte |Système de source de données actuelle hello - Azure |
| ResourceId |Texte |Ce champ représente l’ID de la ressource pour laquelle les données sont collectées ; affiche l’ID du coffre Recovery Services |
| SubscriptionId |Texte |Ce champ représente l’id d’abonnement de ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceGroup |Texte |Ce champ représente le groupe de ressources de la ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceProvider |Texte |Ce champ représente hello fournisseur de ressources pour lequel les données sont en cours collectées - Microsoft.RecoveryServices |
| ResourceType |Texte |Ce champ représente le type de ressource de hello pour lesquels les données sont en cours collectées - coffres |

### <a name="backupitemassociation"></a>BackupItemAssociation
Ce tableau fournit des détails sur les associations d’éléments de sauvegarde avec différentes entités.

| Champ | Type de données | Description |
| --- | --- | --- |
| EventName_s |Texte |Ce champ représente le nom de cet événement, qui est toujours AzureBackupCentralReport |  
| BackupItemUniqueId_s |Texte |Id unique de l’élément de sauvegarde hello |
| SchemaVersion_s |Texte |Ce champ indique la version actuelle du schéma de hello, il est **V1** |
| State_s |Texte |État actuel de l’objet hello sauvegarder l’élément association, par exemple, actif, supprimé |
| BackupManagementType_s |Texte |Type de fournisseur pour la sauvegarde, par exemple, IaaSVM, toowhich FileFolder appartient trop de cet élément de sauvegarde|
| Nom d'opération |Texte |Ce champ représente le nom de l’opération en cours hello - BackupItemAssociation |
| Catégorie |Texte |Ce champ représente la catégorie de données de diagnostic poussées tooLog Analytique, il est AzureBackupReport |
| Ressource |Texte |Il s’agit des ressources hello pour lequel les données sont collectées, il affiche le nom du coffre Recovery Services |
| PolicyUniqueId_g |Texte |Id tooidentify hello stratégie unique, l’élément de sauvegarde est trop associé|
| ProtectedServerUniqueId_s |Texte |Id unique de hello protégé toowhich serveur qu'appartient trop de cet élément de sauvegarde|
| VaultUniqueId_s |Texte |Id unique de toowhich de coffre hello qu'appartient trop de cet élément de sauvegarde|
| SourceSystem |Texte |Système de source de données actuelle hello - Azure |
| ResourceId |Texte |Ce champ représente l’ID de la ressource pour laquelle les données sont collectées ; affiche l’ID du coffre Recovery Services |
| SubscriptionId |Texte |Ce champ représente l’id d’abonnement de ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceGroup |Texte |Ce champ représente le groupe de ressources de la ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceProvider |Texte |Ce champ représente hello fournisseur de ressources pour lequel les données sont en cours collectées - Microsoft.RecoveryServices |
| ResourceType |Texte |Ce champ représente le type de ressource de hello pour lesquels les données sont en cours collectées - coffres |

### <a name="job"></a>Travail
Ce tableau fournit plus d’informations sur les champs liés aux travaux.

| Champ | Type de données | Description |
| --- | --- | --- |
| EventName_s |Texte |Ce champ représente le nom de cet événement, qui est toujours AzureBackupCentralReport |
| BackupItemUniqueId_s |Texte |Id unique de toowhich de sauvegarder l’élément hello que ce travail appartient trop|
| SchemaVersion_s |Texte |Ce champ indique la version actuelle du schéma de hello, il est **V1** |
| State_s |Texte |État actuel de l’objet de tâche hello, par exemple, actif, supprimé |
| BackupManagementType_s |Texte |Type de fournisseur pour la sauvegarde, par exemple, IaaSVM, toowhich FileFolder ce travail appartient trop|
| Nom d'opération |Texte |Ce champ représente le nom de l’opération en cours hello - tâche |
| Catégorie |Texte |Ce champ représente la catégorie de données de diagnostic poussées tooLog Analytique, il est AzureBackupReport |
| Ressource |Texte |Il s’agit des ressources hello pour lequel les données sont collectées, il affiche le nom du coffre Recovery Services |
| ProtectedServerUniqueId_s |Texte |Id unique de hello protégé toowhich que ce travail appartient trop|
| VaultUniqueId_s |Texte |Id unique de hello protégé toowhich que ce travail appartient trop|
| JobOperation_s |Texte |Opération pour laquelle le travail est exécuté, par exemple, Sauvegarde, Restauration, Configuration de sauvegarde |
| JobStatus_s |Texte |État de hello a terminé de tâche, par exemple, terminé, échec |
| JobFailureCode_s |Texte |Chaîne de Code d’échec en raison du type d’échec de travail survenu |
| JobStartDateTime_s |Date/Heure |Date et heure de démarrage de l’exécution du travail |
| BackupStorageDestination_s |Texte |Destination du stockage de sauvegarde, par exemple, Cloud, Disque  |
| JobDurationInSecs_s | Number |Durée totale de la tâche en secondes |
| DataTransferredInMB_s | Number |Données transférées en Mo pour ce travail|
| JobUniqueId_g |Texte |Tâche de hello tooidentify Id unique |
| SourceSystem |Texte |Système de source de données actuelle hello - Azure |
| ResourceId |Texte |Ce champ représente l’ID de la ressource pour laquelle les données sont collectées ; affiche l’ID du coffre Recovery Services |
| SubscriptionId |Texte |Ce champ représente l’id d’abonnement de ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceGroup |Texte |Ce champ représente le groupe de ressources de la ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceProvider |Texte |Ce champ représente hello fournisseur de ressources pour lequel les données sont en cours collectées - Microsoft.RecoveryServices |
| ResourceType |Texte |Ce champ représente le type de ressource de hello pour lesquels les données sont en cours collectées - coffres |

### <a name="policy"></a>Stratégie
Ce tableau fournit plus d’informations sur les champs liés à la stratégie.

| Champ | Type de données | Description |
| --- | --- | --- |
| EventName_s |Texte |Ce champ représente le nom de cet événement, qui est toujours AzureBackupCentralReport |
| SchemaVersion_s |Texte |Ce champ indique la version actuelle du schéma de hello, il est **V1** |
| State_s |Texte |État actuel de l’objet de stratégie de hello, par exemple, actif, supprimé |
| BackupManagementType_s |Texte |Type de fournisseur pour la sauvegarde, par exemple, IaaSVM, toowhich FileFolder appartient trop de cette stratégie|
| Nom d'opération |Texte |Ce champ représente le nom de l’opération en cours hello - stratégie |
| Catégorie |Texte |Ce champ représente la catégorie de données de diagnostic poussées tooLog Analytique, il est AzureBackupReport |
| Ressource |Texte |Il s’agit des ressources hello pour lequel les données sont collectées, il affiche le nom du coffre Recovery Services |
| PolicyUniqueId_g |Texte |Stratégie de hello tooidentify Id unique |
| PolicyName_s |Texte |Nom de stratégie hello défini |
| BackupFrequency_s |Texte |Fréquence à laquelle les sauvegardes sont exécutées, par exemple, Quotidienne, Hebdomadaire |
| BackupTimes_s |Texte |Date et heure auxquelles les sauvegardes sont planifiées |
| BackupDaysOfTheWeek_s |Texte |Jours de semaine hello lorsque les sauvegardes ont été planifiées |
| RetentionDuration_s |Nombre entier |Durée de rétention des sauvegardes configurées |
| DailyRetentionDuration_s |Nombre entier |Durée totale de rétention en jours des sauvegardes configurées |
| DailyRetentionTimes_s |Texte |Date et heure auxquelles la rétention quotidienne est configurée |
| WeeklyRetentionDuration_s |Nombre décimal |Durée totale de rétention hebdomadaire en semaines des sauvegardes configurées |
| WeeklyRetentionTimes_s |Texte |Date et heure auxquelles la rétention hebdomadaire est configurée |
| WeeklyRetentionDaysOfTheWeek_s |Texte |Jours de semaine de hello sélectionnés pour la rétention hebdomadaire |
| MonthlyRetentionDuration_s |Nombre décimal |Durée totale de rétention en mois des sauvegardes configurées |
| MonthlyRetentionTimes_s |Texte |Date et heure auxquelles la rétention mensuelle est configurée |
| MonthlyRetentionFormat_s |Texte |Type de configuration de la rétention mensuelle, par exemple, quotidienne pour une configuration quotidienne, hebdomadaire pour une configuration hebdomadaire |
| MonthlyRetentionDaysOfTheWeek_s |Texte |Jours de semaine de hello sélectionnés pour la rétention mensuelle |
| MonthlyRetentionWeeksOfTheMonth_s |Texte |Semaines du mois hello lorsque rétention mensuelle est configurée, par exemple, tout d’abord, etc. de la dernière. |
| YearlyRetentionDuration_s |Nombre décimal |Durée totale de rétention en années des sauvegardes configurées |
| YearlyRetentionTimes_s |Texte |Date et heure auxquelles la rétention annuelle est configurée |
| YearlyRetentionMonthsOfTheYear_s |Texte |Mois de l’année de hello sélectionné pour la rétention annuelle |
| YearlyRetentionFormat_s |Texte |Type de configuration de la rétention annuelle, par exemple, quotidienne pour une configuration quotidienne, hebdomadaire pour une configuration hebdomadaire |
| YearlyRetentionDaysOfTheMonth_s |Texte |Dates du mois hello sélectionnées pour la rétention annuelle |
| SourceSystem |Texte |Système de source de données actuelle hello - Azure |
| ResourceId |Texte |Ce champ représente l’ID de la ressource pour laquelle les données sont collectées ; affiche l’ID du coffre Recovery Services |
| SubscriptionId |Texte |Ce champ représente l’id d’abonnement de ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceGroup |Texte |Ce champ représente le groupe de ressources de la ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceProvider |Texte |Ce champ représente hello fournisseur de ressources pour lequel les données sont en cours collectées - Microsoft.RecoveryServices |
| ResourceType |Texte |Ce champ représente le type de ressource de hello pour lesquels les données sont en cours collectées - coffres |

### <a name="policyassociation"></a>PolicyAssociation
Ce tableau fournit des détails sur les associations de stratégies avec différentes entités.

| Champ | Type de données | Description |
| --- | --- | --- |
| EventName_s |Texte |Ce champ représente le nom de cet événement, qui est toujours AzureBackupCentralReport |
| SchemaVersion_s |Texte |Ce champ indique la version actuelle du schéma de hello, il est **V1** |
| State_s |Texte |État actuel de l’objet de stratégie de hello, par exemple, actif, supprimé |
| BackupManagementType_s |Texte |Type de fournisseur pour l’exécution, par exemple, IaaSVM, toowhich FileFolder appartient trop de cette stratégie de sauvegarde|
| Nom d'opération |Texte |Ce champ représente le nom de l’opération en cours hello - PolicyAssociation |
| Catégorie |Texte |Ce champ représente la catégorie de données de diagnostic poussées tooLog Analytique, il est AzureBackupReport |
| Ressource |Texte |Il s’agit des ressources hello pour lequel les données sont collectées, il affiche le nom du coffre Recovery Services |
| PolicyUniqueId_g |Texte |Stratégie de hello tooidentify Id unique |
| VaultUniqueId_s |Texte |Id unique de toowhich de coffre hello qu'appartient trop de cette stratégie|
| SourceSystem |Texte |Système de source de données actuelle hello - Azure |
| ResourceId |Texte |Ce champ représente l’ID de la ressource pour laquelle les données sont collectées ; affiche l’ID du coffre Recovery Services |
| SubscriptionId |Texte |Ce champ représente l’id d’abonnement de ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceGroup |Texte |Ce champ représente le groupe de ressources de la ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceProvider |Texte |Ce champ représente hello fournisseur de ressources pour lequel les données sont en cours collectées - Microsoft.RecoveryServices |
| ResourceType |Texte |Ce champ représente le type de ressource de hello pour lesquels les données sont en cours collectées - coffres |

### <a name="protectedserver"></a>ProtectedServer
Ce tableau fournit plus d’informations sur les champs liés au serveur protégé.

| Champ | Type de données | Description |
| --- | --- | --- |
| EventName_s |Texte |Ce champ représente le nom de cet événement, qui est toujours AzureBackupCentralReport |
| ProtectedServerName_s |Texte |Nom du serveur protégé |
| SchemaVersion_s |Texte |Ce champ indique la version actuelle du schéma de hello, il est **V1** |
| State_s |Texte |État actuel de hello protégé par objet de serveur, par exemple, actif, supprimé |
| BackupManagementType_s |Texte |Type de fournisseur pour la sauvegarde, par exemple, IaaSVM, toowhich FileFolder ce serveur protégé appartient trop|
| Nom d'opération |Texte |Ce champ représente le nom de l’opération en cours hello - ProtectedServer |
| Catégorie |Texte |Ce champ représente la catégorie de données de diagnostic poussées tooLog Analytique, il est AzureBackupReport |
| Ressource |Texte |Il s’agit des ressources hello pour lequel les données sont collectées, il affiche le nom du coffre Recovery Services |
| ProtectedServerUniqueId_s |Texte |Id unique de hello de serveur protégé |
| RegisteredContainerId_s |Texte |ID du conteneur inscrit pour la sauvegarde |
| ProtectedServerType_s |Texte |Type de serveur protégé sauvegardé, par exemple, Windows |
| ProtectedServerFriendlyName_s |Texte |Nom convivial du serveur protégé |
| AzureBackupAgentVersion_s |Texte |Numéro de version de l’agent Backup |
| SourceSystem |Texte |Système de source de données actuelle hello - Azure |
| ResourceId |Texte |Ce champ représente l’ID de la ressource pour laquelle les données sont collectées ; affiche l’ID du coffre Recovery Services |
| SubscriptionId |Texte |Ce champ représente l’id d’abonnement de ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceGroup |Texte |Ce champ représente le groupe de ressources de la ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceProvider |Texte |Ce champ représente hello fournisseur de ressources pour lequel les données sont en cours collectées - Microsoft.RecoveryServices |
| ResourceType |Texte |Ce champ représente le type de ressource de hello pour lesquels les données sont en cours collectées - coffres |

### <a name="protectedserverassociation"></a>ProtectedServerAssociation
Ce tableau fournit des détails sur les associations de serveurs protégés avec d’autres entités.

| Champ | Type de données | Description |
| --- | --- | --- |
| EventName_s |Texte |Ce champ représente le nom de cet événement, qui est toujours AzureBackupCentralReport |
| SchemaVersion_s |Texte |Ce champ indique la version actuelle du schéma de hello, il est **V1** |
| State_s |Texte |État actuel de hello protégé objet association de serveur, par exemple, actif, supprimé |
| BackupManagementType_s |Texte |Type de fournisseur pour la sauvegarde, par exemple, IaaSVM, toowhich FileFolder ce serveur protégé appartient trop|
| Nom d'opération |Texte |Ce champ représente le nom de l’opération en cours hello - ProtectedServerAssociation |
| Catégorie |Texte |Ce champ représente la catégorie de données de diagnostic poussées tooLog Analytique, il est AzureBackupReport |
| Ressource |Texte |Il s’agit des ressources hello pour lequel les données sont collectées, il affiche le nom du coffre Recovery Services |
| ProtectedServerUniqueId_s |Texte |Id unique de hello de serveur protégé |
| VaultUniqueId_s |Texte |Id unique de toowhich de coffre hello que ce serveur protégé appartient trop|
| SourceSystem |Texte |Système de source de données actuelle hello - Azure |
| ResourceId |Texte |Ce champ représente l’ID de la ressource pour laquelle les données sont collectées ; affiche l’ID du coffre Recovery Services |
| SubscriptionId |Texte |Ce champ représente l’id d’abonnement de ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceGroup |Texte |Ce champ représente le groupe de ressources de la ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceProvider |Texte |Ce champ représente hello fournisseur de ressources pour lequel les données sont en cours collectées - Microsoft.RecoveryServices |
| ResourceType |Texte |Ce champ représente le type de ressource de hello pour lesquels les données sont en cours collectées - coffres |

### <a name="storage"></a>Storage
Ce tableau fournit plus d’informations sur les champs liés au stockage.

| Champ | Type de données | Description |
| --- | --- | --- |
| CloudStorageInBytes_s |Nombre décimal |Stockage des sauvegardes dans le cloud utilisé par les sauvegardes, calculé en fonction de la dernière valeur |
| ProtectedInstances_s |Nombre décimal |Nombre d’instances protégées utilisées pour calculer le stockage frontal dans la facturation, calculé en fonction de la dernière valeur |
| EventName_s |Texte |Ce champ représente le nom de cet événement, qui est toujours AzureBackupCentralReport |
| SchemaVersion_s |Texte |Ce champ indique la version actuelle du schéma de hello, il est **V1** |
| State_s |Texte |État actuel de l’objet de stockage hello, par exemple, actif, supprimé |
| BackupManagementType_s |Texte |Type de fournisseur pour la sauvegarde, par exemple, IaaSVM, toowhich FileFolder ce stockage appartient trop|
| Nom d'opération |Texte |Ce champ représente le nom de l’opération en cours hello - stockage |
| Catégorie |Texte |Ce champ représente la catégorie de données de diagnostic poussées tooLog Analytique, il est AzureBackupReport |
| Ressource |Texte |Il s’agit des ressources hello pour lequel les données sont collectées, il affiche le nom du coffre Recovery Services |
| ProtectedServerUniqueId_s |Texte |Id unique de hello protégé par le serveur pour lequel le stockage est calculé |
| VaultUniqueId_s |Texte |Id unique du coffre hello pour le stockage est calculée. |
| SourceSystem |Texte |Système de source de données actuelle hello - Azure |
| ResourceId |Texte |Ce champ représente l’ID de la ressource pour laquelle les données sont collectées ; affiche l’ID du coffre Recovery Services |
| SubscriptionId |Texte |Ce champ représente l’id d’abonnement de ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceGroup |Texte |Ce champ représente le groupe de ressources de la ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceProvider |Texte |Ce champ représente hello fournisseur de ressources pour lequel les données sont en cours collectées - Microsoft.RecoveryServices |
| ResourceType |Texte |Cette representse de champ de type de ressource de hello pour lesquels les données sont en cours collectées - coffres |

### <a name="vault"></a>Coffre
Ce tableau fournit plus d’informations sur les champs liés aux coffres.

| Champ | Type de données | Description |
| --- | --- | --- |
| EventName_s |Texte |Ce champ représente le nom de cet événement, qui est toujours AzureBackupCentralReport |
| SchemaVersion_s |Texte |Ce champ indique la version actuelle du schéma de hello, il est **V1** |
| State_s |Texte |État actuel de l’objet de coffre hello, par exemple, actif, supprimé |
| Nom d'opération |Texte |Ce champ représente le nom de l’opération en cours hello - coffre |
| Catégorie |Texte |Ce champ représente la catégorie de données de diagnostic poussées tooLog Analytique, il est AzureBackupReport |
| Ressource |Texte |Il s’agit des ressources hello pour lequel les données sont collectées, il affiche le nom du coffre Recovery Services |
| VaultUniqueId_s |Texte |Id unique de l’archivage de hello |
| VaultName_s |Texte |Nom du coffre de hello |
| AzureDataCenter_s |Texte |Centre de données dans lequel se trouve le coffre |
| StorageReplicationType_s |Texte |Type de réplication de stockage pour l’archivage hello, par exemple, GeoRedundant |
| SourceSystem |Texte |Système de source de données actuelle hello - Azure |
| ResourceId |Texte |Ce champ représente l’ID de la ressource pour laquelle les données sont collectées ; affiche l’ID du coffre Recovery Services |
| SubscriptionId |Texte |Ce champ représente l’id d’abonnement de ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceGroup |Texte |Ce champ représente le groupe de ressources de la ressource de hello (coffre-fort RS) pour lequel les données sont collectées |
| ResourceProvider |Texte |Ce champ représente hello fournisseur de ressources pour lequel les données sont en cours collectées - Microsoft.RecoveryServices |
| ResourceType |Texte |Ce champ représente le type de ressource de hello pour lesquels les données sont en cours collectées - coffres |

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous passez en revue le modèle de données hello pour créer des rapports d’Azure Backup, vous pouvez démarrer [création de tableau de bord](../log-analytics/log-analytics-dashboards.md) dans le journal Analytique et OMS.
