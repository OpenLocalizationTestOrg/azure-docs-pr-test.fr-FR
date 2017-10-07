---
title: "modèle d’aaaData pour la sauvegarde Azure"
description: "Cet article présente des informations détaillées sur le modèle de données Power BI pour les rapports de sauvegarde Azure."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 0767c330-690d-474d-85a6-aa8ddc410bb2
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/26/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5e3e7ca13c7a3f007c206bd56b8753166a2c264b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-model-for-azure-backup-reports"></a>Modèle de données pour les rapports de sauvegarde Azure
Cet article décrit le modèle de données de Power BI hello utilisé pour créer des rapports d’Azure Backup. À l’aide de ce modèle de données, vous pouvez filtrer les rapports existants basés sur les champs appropriés et créer plus important encore, vos propres rapports à l’aide de tables et les champs dans le modèle de hello. 

## <a name="creating-new-reports-in-power-bi"></a>Création de rapports dans Power BI
Power BI fournit des fonctionnalités de personnalisation à l’aide de laquelle vous pouvez [créer des rapports à l’aide du modèle de données hello](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/).

## <a name="using-azure-backup-data-model"></a>Utilisation du modèle de données de sauvegarde Azure
Vous pouvez utiliser hello suivant champs fournis comme faisant partie des données de hello toocreate rapports de modèle et personnaliser des rapports existants.

### <a name="alert"></a>Alerte
Ce tableau présente les champs de base et les agrégations des différents champs liés aux alertes.

| Champ | Type de données | Description |
| --- | --- | --- |
| #AlertsCreatedInPeriod |Nombre entier |Nombre d’alertes créées dans l’intervalle de temps sélectionné |
| %ActiveAlertsCreatedInPeriod |Pourcentage |Pourcentage d’alertes actives dans l’intervalle de temps sélectionné |
| %CriticalAlertsCreatedInPeriod |Pourcentage |Pourcentage d’alertes critiques dans l’intervalle de temps sélectionné |
| AlertOccurenceDate |Date |Date de création de l’alerte |
| AlertSeverity |Texte |Gravité d’alerte hello par exemple, critique |
| AlertStatus |Texte |État d’alerte hello par exemple, actif |
| AlertType |Texte |Type d’alerte hello généré par exemple, sauvegarde |
| AlertUniqueId |Texte |Id unique de hello a généré l’alerte |
| AsOnDateTime |Date/Heure |Dernière actualisation de la ligne sélectionnée de hello |
| AvgResolutionTimeInMinsForAlertsCreatedInPeriod |Nombre décimal |Alerte de tooresolve temps moyen (en minutes) pour l’intervalle de temps sélectionné |
| EntityState |Texte |État actuel de l’objet d’alerte hello par exemple, actif, supprimé |

### <a name="backup-item"></a>Élément de sauvegarde
Ce tableau présente les champs de base et les agrégations des différents champs liés à l’élément de sauvegarde.

| Champ | Type de données | Description |
| --- | --- | --- |
| #BackupItems |Nombre entier |Nombre d’éléments de sauvegarde |
| #UnprotectedBackupItems |Nombre entier |Nombre d’éléments de sauvegarde arrêtés à des fins de protection ou configurés pour les sauvegardes, mais dont les sauvegardes n’ont pas démarré|
| AsOnDateTime |Date/Heure |Dernière actualisation de la ligne sélectionnée de hello |
| BackupItemFriendlyName |Texte |Nom convivial de l’élément de sauvegarde |
| BackupItemId |Texte |ID de l’élément de sauvegarde |
| BackupItemName |Texte |Nom de l’élément de sauvegarde |
| BackupItemType |Texte |Type d’élément de sauvegarde, par exemple, Machine virtuelle, Dossier de fichiers |
| EntityState |Texte |État actuel de l’objet d’élément de sauvegarde hello par exemple, actif, supprimé |
| LastBackupDateTime |Date/Heure |Heure de la dernière sauvegarde de l’élément de sauvegarde sélectionné |
| LastBackupState |Texte |État de la dernière sauvegarde de l’élément de sauvegarde sélectionné par exemple, Réussite, Échec |
| LastSuccessfulBackupDateTime |Date/Heure |Heure de la dernière sauvegarde réussie de l’élément de sauvegarde sélectionné |
| ProtectionState |Texte |État de protection actuel de sauvegarder l’élément hello par exemple, protégé, ProtectionStopped |

### <a name="calendar"></a>Calendrier
Ce tableau fournit plus d’informations sur les champs liés au calendrier.

| Champ | Type de données | Description |
| --- | --- | --- |
| Date |Date |Date sélectionnée pour le filtrage des données |
| DateKey |Texte |Clé unique pour chaque élément de date |
| DayDiff |Nombre décimal |Écart en jours pour filtrer les données par exemple, 0 indique des données du jour en cours, -1 indique des données du jour précédent, 0 et -1 indiquent des données du jour en cours et précédent  |
| Mois |Texte |Mois de l’année hello sélectionnée pour le filtrage des données, mois commence le premier jour et se termine le 31 jours |
| MonthDate | Date |Date mois hello lorsque mois se termine, sélectionné pour le filtrage des données |
| MonthDiff |Nombre décimal |Écart en mois du filtrage des données par exemple, 0 indique des données du mois en cours, -1 indique des données du mois précédent, 0 et -1 indiquent des données du mois en cours et précédent |
| Semaine |Texte |Semaine sélectionnée pour filtrer les données, la semaine commence le dimanche et se termine le samedi |
| WeekDate |Date |Date semaine hello lorsque la semaine se termine, sélectionné pour le filtrage des données |
| WeekDiff |Nombre décimal |Écart en semaines pour filtrer les données par exemple, 0 indique des données de la semaine en cours, -1 indique des données de la semaine précédente, 0 et -1 indiquent des données de la semaine en cours et précédente |
| Year |Texte |Année du calendrier sélectionnée pour filtrer les données |
| YearDate |Date |Date de l’année hello lorsque année se termine, sélectionné pour le filtrage des données |

### <a name="job"></a>Travail
Ce tableau présente les champs de base et les agrégations des différents champs liés aux travaux.

| Champ | Type de données | Description |
| --- | --- | --- |
| #JobsCreatedInPeriod |Nombre entier |Nombre de travaux créés dans hello période sélectionnée |
| %FailuresForJobsCreatedInPeriod |Pourcentage |Pourcentage de la tâche globale échecs Bonjour période sélectionnée |
| 80thPercentileDataTransferredInMBForBackupJobsCreatedInPeriod |Nombre décimal |80E centile de données transférées en Mo pour **sauvegarde** travaux créés dans hello période sélectionnée |
| AsOnDateTime |Date/Heure |Dernière actualisation de la ligne sélectionnée de hello |
| AvgBackupDurationInMinsForJobsCreatedInPeriod |Nombre décimal |Temps moyen en minutes pour les travaux de **sauvegarde terminés** créés dans l’intervalle de temps sélectionné |
| AvgRestoreDurationInMinsForJobsCreatedInPeriod |Nombre décimal |Temps moyen en minutes pour les travaux de **restauration terminés** créés dans l’intervalle de temps sélectionné |
| BackupStorageDestination |Texte |Destination du stockage de sauvegarde, par exemple, Cloud, Disque  |
| EntityState |Texte |État actuel de l’objet de tâche hello par exemple, actif, supprimé |
| JobFailureCode |Texte |Chaîne de Code d’échec en raison du type d’échec de travail survenu |
| JobOperation |Texte |Opération pour laquelle le travail est exécuté, par exemple, Sauvegarde, Restauration, Configuration de sauvegarde |
| JobStartDate |Date |Date de démarrage de l’exécution du travail |
| JobStartTime |Temps |Heure de démarrage de l’exécution du travail |
| JobStatus |Texte |État de hello terminé, par exemple, tâche terminée, a échoué |
| JobUniqueId |Texte |Tâche de hello tooidentify Id unique |

### <a name="policy"></a>Stratégie
Ce tableau présente les champs de base et les agrégations des différents champs liés aux stratégies.

| Champ | Type de données | Description |
| --- | --- | --- |
| #Policies |Nombre entier |Nombre de stratégies de sauvegarde qui existent dans le système de hello |
| #PoliciesInUse |Nombre entier |Nombre de stratégies actuellement utilisées pour la configuration des sauvegardes |
| AsOnDateTime |Date/Heure |Dernière actualisation de la ligne sélectionnée de hello |
| BackupDaysOfTheWeek |Texte |Jours de semaine hello lorsque les sauvegardes ont été planifiées |
| BackupFrequency |Texte |Fréquence à laquelle les sauvegardes sont exécutées, par exemple, Quotidienne, Hebdomadaire |
| BackupTimes |Texte |Date et heure auxquelles les sauvegardes sont planifiées |
| DailyRetentionDuration |Nombre entier |Durée totale de rétention en jours des sauvegardes configurées |
| DailyRetentionTimes |Texte |Date et heure auxquelles la rétention quotidienne est configurée |
| EntityState |Texte |État actuel de l’objet de stratégie de hello par exemple, actif, supprimé |
| MonthlyRetentionDaysOfTheMonth |Texte |Dates du mois hello sélectionnées pour la rétention mensuelle |
| MonthlyRetentionDaysOfTheWeek |Texte |Jours de semaine de hello sélectionnés pour la rétention mensuelle |
| MonthlyRetentionDuration |Nombre décimal |Durée totale de rétention en mois des sauvegardes configurées |
| MonthlyRetentionFormat |Texte |Type de configuration de la rétention mensuelle, par exemple, quotidienne pour une configuration quotidienne, hebdomadaire pour une configuration hebdomadaire |
| MonthlyRetentionTimes |Texte |Date et heure auxquelles la rétention mensuelle est configurée |
| MonthlyRetentionWeeksOfTheMonth |Texte |Semaines du mois hello lorsque rétention mensuelle est configuré, par exemple, premier, dernier etc.. |
| PolicyName |Texte |Nom de stratégie hello défini |
| PolicyUniqueId |Texte |Stratégie de hello tooidentify Id unique |
| RetentionType |Texte |Type de stratégie de rétention par exemple, Quotidienne, Hebdomadaire, Mensuelle, Annuelle |
| WeeklyRetentionDaysOfTheWeek |Texte |Jours de semaine de hello sélectionnés pour la rétention hebdomadaire |
| WeeklyRetentionDuration |Nombre décimal |Durée totale de rétention hebdomadaire en semaines des sauvegardes configurées |
| WeeklyRetentionTimes |Texte |Date et heure auxquelles la rétention hebdomadaire est configurée |
| YearlyRetentionDaysOfTheMonth |Texte |Dates du mois hello sélectionnées pour la rétention annuelle |
| YearlyRetentionDaysOfTheWeek |Texte |Jours de semaine de hello sélectionnés pour la rétention annuelle |
| YearlyRetentionDuration |Nombre décimal |Durée totale de rétention en années des sauvegardes configurées |
| YearlyRetentionFormat |Texte |Type de configuration de la rétention annuelle, par exemple, quotidienne pour une configuration quotidienne, hebdomadaire pour une configuration hebdomadaire |
| YearlyRetentionMonthsOfTheYear |Texte |Mois de l’année de hello sélectionné pour la rétention annuelle |
| YearlyRetentionTimes |Texte |Date et heure auxquelles la rétention annuelle est configurée |
| YearlyRetentionWeeksOfTheMonth |Texte |Semaines du mois hello lorsque rétention annuelle est configuré, par exemple, premier, dernier etc.. |

### <a name="protected-server"></a>Serveur protégé
Ce tableau fournit les champs de base et les agrégations des différents champs liés au serveur protégé.

| Champ | Type de données | Description |
| --- | --- | --- |
| #ProtectedServers |Nombre entier |Nombre de serveurs protégés |
| AsOnDateTime |Date/Heure |Dernière actualisation de la ligne sélectionnée de hello |
| AzureBackupAgentOSType |Texte |Type de système d’exploitation de l’agent Azure Backup |
| AzureBackupAgentOSVersion |Texte |Version de système d’exploitation de l’agent Azure Backup |
| AzureBackupAgentUpdateDate |Texte |Date de mise à jour de l’agent Backup |
| AzureBackupAgentVersion |Texte |Numéro de version de l’agent Backup |
| BackupManagementType |Texte |Type de fournisseur exécutant la sauvegarde, par exemple, Machine virtuelle IaaS, Dossier de fichiers |
| EntityState |Texte |État actuel de l’objet de serveur protégé hello par exemple, actif, supprimé |
| ProtectedServerFriendlyName |Texte |Nom convivial du serveur protégé |
| ProtectedServerName |Texte |Nom du serveur protégé |
| ProtectedServerType |Texte |Type de serveur protégé sauvegardé, par exemple, Conteneur de machine virtuelle IaaS |
| ProtectedServerName |Texte |Nom du serveur protégé toowhich sauvegarder l’élément appartient |
| RegisteredContainerId |Texte |ID du conteneur inscrit pour la sauvegarde |

### <a name="storage"></a>Storage
Ce tableau fournit les champs de base et les agrégations des différents champs liés au stockage.

| Champ | Type de données | Description |
| --- | --- | --- |
| #ProtectedInstances |Nombre décimal |Nombre d’instances protégées utilisées pour calculer le stockage frontal dans la facturation, calculé en fonction de la dernière valeur dans l’intervalle de temps sélectionné |
| AsOnDateTime |Date/Heure |Dernière actualisation de la ligne sélectionnée de hello |
| CloudStorageInMB |Nombre décimal |Stockage des sauvegardes dans le cloud utilisé par les sauvegardes, calculé en fonction de la dernière valeur dans l’intervalle de temps sélectionné |
| EntityState |Texte |État actuel de l’objet hello par exemple, actif, supprimé |
| LastUpdatedDate |Date |Date de dernière mise à jour de la ligne sélectionnée |

### <a name="time"></a>Temps
Ce tableau fournit plus d’informations sur les champs liés au temps.

| Champ | Type de données | Description |
| --- | --- | --- |
| Hour |Temps |Heure de la journée de hello, par exemple, 1:00:00 PM |
| HourNumber |Nombre décimal |Nombre d’heures le jour hello 13.00, par exemple, |
| Minute |Nombre décimal |Minute de hello heure |
| PeriodOfTheDay |Texte |Emplacement de période de temps dans le jour hello, par exemple, 12-3 AM |
| Temps |Temps |Heure du jour de hello, par exemple, 12:00:01 AM |
| TimeKey |Texte |Temps de toorepresent de valeur de clé |

### <a name="vault"></a>Coffre
Ce tableau fournit les champs de base et les agrégations des différents champs liés au coffre.

| Champ | Type de données | Description |
| --- | --- | --- |
| #Vaults |Nombre entier |Nombre de coffres |
| AsOnDateTime |Date/Heure |Dernière actualisation de la ligne sélectionnée de hello |
| AzureDataCenter |Texte |Centre de données dans lequel se trouve le coffre |
| EntityState |Texte |État actuel de l’objet de coffre hello par exemple, actif, supprimé |
| StorageReplicationType |Texte |Type de réplication de stockage pour l’archivage de hello, par exemple, GeoRedundant |
| SubscriptionId |Texte |Id d’abonnement du client hello sélectionnée pour la génération de rapports |
| VaultName |Texte |Nom du coffre de hello |
| VaultTags |Texte |Les balises associées toohello coffre |

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous passez en revue le modèle de données hello pour créer des rapports d’Azure Backup, consultez hello suivant des articles pour plus d’informations sur la création et l’affichage des rapports dans Power BI.

* [Création de rapports dans Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)
* [Filtrage de rapports dans Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
