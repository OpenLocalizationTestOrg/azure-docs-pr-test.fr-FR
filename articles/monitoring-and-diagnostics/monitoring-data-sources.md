---
title: "aaaConsume analyse les données à partir de Azure | Documents Microsoft"
description: "Obtenir des informations sur tous les hello analyse les sources de données disponibles sur Azure aujourd'hui."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/27/2017
ms.author: johnkem
ms.openlocfilehash: 3c7fdad7c25b4d456df395b453fa0e75d514b0b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-monitoring-data-from-azure"></a>Consommer des données d’analyse à partir d’Azure

Entre hello Azure plateforme, il déroule ensemble analyse les données dans un emplacement unique avec le pipeline de moniteur de Windows Azure hello, mais pratiquement reconnaître qu’aujourd'hui pas toutes les données d’analyse est encore disponible dans ce pipeline. Dans cet article, nous résume hello différentes méthodes que vous pouvez accéder par programme des données d’analyse à partir des services Azure.

## <a name="options-for-data-consumption"></a>Options pour la consommation de données

| Type de données | Catégorie | Services pris en charge | Méthodes d’accès |
| --- | --- | --- | --- |
| Mesures au niveau de la plateforme Azure Monitor | Mesures | [Consulter la liste ici](monitoring-supported-metrics.md) | <ul><li>**API REST :**[API métrique Azure Monitor](https://docs.microsoft.com/rest/api/monitor/metrics)</li><li>**Stockage d’objets blob ou concentrateur d’événements :**[Paramètres de diagnostic](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)</li></ul> |
| Mesures de SE invité Compute (ex. compteurs de performances) | Mesures | Machines virtuelles [Windows](../virtual-machines-dotnet-diagnostics.md) et Linux (v2), [Services cloud](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md), [Service Fabric](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md) | <ul><li>**Table ou blob de stockage :**[diagnostics Azure Windows ou Linux](../cloud-services/cloud-services-dotnet-diagnostics-storage.md)</li><li>**Concentrateur d’événements :**[Diagnostics Windows Azure](../event-hubs/event-hubs-streaming-azure-diags-data.md)</li></ul> |
| Mesures personnalisées ou d’application | Mesures | Toute application instrumentée avec Application Insights | <ul><li>**API REST :**[API REST d’Application Insights](https://dev.applicationinsights.io/reference)</li></ul> |
| Métriques de stockage | Mesures | Azure Storage | <ul><li>**Table de stockage :**[Analyse du stockage](https://docs.microsoft.com/rest/api/storageservices/storage-analytics)</li></ul> |
| Données de facturation | Mesures | Tous les services Azure | <ul><li>**API REST** [API Azure Resource Usage et RateCard](../billing/billing-usage-rate-card-overview.md)</li></ul> |
| Journal d’activité | Événements | Tous les services Azure | <ul><li>**API REST :**[API Événements Azure Monitor](https://docs.microsoft.com/rest/api/monitor/events)</li><li>**Stockage d’objets blob ou concentrateur d’événements :**[profil du journal](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile)</li></ul> |
| Journaux de diagnostics Azure Monitor | Événements | [Consulter la liste ici](monitoring-diagnostic-logs-schema.md) | <ul><li>**Stockage d’objets blob ou concentrateur d’événements :**[Paramètres de diagnostic](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)</li></ul> |
| Journaux de SE invité Compute (ex. IIS, ETW, syslogs) | Événements | Machines virtuelles [Windows](../virtual-machines-dotnet-diagnostics.md) et Linux (v2), [Services cloud](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md), [Service Fabric](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md) | <ul><li>**Table ou blob de stockage :**[diagnostics Azure Windows ou Linux](../cloud-services/cloud-services-dotnet-diagnostics-storage.md)</li><li>**Concentrateur d’événements :**[Diagnostics Windows Azure](../event-hubs/event-hubs-streaming-azure-diags-data.md)</li></ul> |
| Journaux App Service | Événements | App Services | <ul><li>**Stockage d’objets blob, table ou fichier :**[Diagnostics Web App](../app-service-web/web-sites-enable-diagnostic-log.md)</li></ul> |
| Journaux de stockage | Événements | Azure Storage | <ul><li>**Table de stockage :**[Analyse du stockage](https://docs.microsoft.com/rest/api/storageservices/storage-analytics)</li></ul> |
| Alertes Security Center | Événements | Azure Security Center | <ul><li>**API REST :**[Alertes de sécurité](https://msdn.microsoft.com/library/mt704050.aspx)</li></ul> |
| Création de rapports Active Directory | Événements | Azure Active Directory | <ul><li>**API REST :** [API Graph Azure Active Directory](../active-directory/active-directory-reporting-api-getting-started.md)</li></ul> |
| État des ressources de Security Center | État | [Toutes les ressources prises en charge](https://msdn.microsoft.com/library/mt704041.aspx#Anchor_1) | <ul><li>**API REST :**[États de sécurité](https://msdn.microsoft.com/library/mt704041.aspx)</li></ul> |
| Intégrité des ressources | État | Services pris en charge | <ul><li>**API REST :**[API REST Resource Health](https://azure.microsoft.com/blog/reduce-troubleshooting-time-with-azure-resource-health/)</li></ul> |
| Alertes de métrique Azure Monitor | Notifications | [Consulter la liste ici](monitoring-supported-metrics.md) | <ul><li>**Webhook:**[Alertes de métrique Azure](insights-webhooks-alerts.md)</li></ul> |
| Alertes Journal d’activité Azure Monitor | Notifications | Tous les services Azure | <ul><li>**Webhook :** Alertes Journal d’activité Azure</li></ul> |
| Notifications de mise à l’échelle automatique | Notifications | [Consulter la liste ici](monitoring-overview-autoscale.md#supported-services-for-autoscale) | <ul><li>**Webhook :**[Schéma de la charge utile du webhook de notification de mise à l’échelle automatique](insights-autoscale-to-webhook-email.md#autoscale-notification-webhook-payload-schema)</li></ul> |
| Alertes Requête de recherche Journal OMS | Notifications | OMS Log Analytics | <ul><li>**Webhook :**[Alertes Log Analytics](../log-analytics/log-analytics-alerts-actions.md#webhook-actions)</li></ul> |
| Alertes de métrique Application Insights | Notifications | Application Insights | <ul><li>**Webhook :**[Alertes Application Insights](../application-insights/app-insights-alerts.md)</li></ul> |
| Tests web Application Insights | Notifications | Application Insights | <ul><li>**Webhook :**[Alertes Application Insights](../application-insights/app-insights-alerts.md)</li></ul> |

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur les [mesures Azure Monitor](monitoring-overview-metrics.md)
- En savoir plus sur [hello du journal des activités Azure](monitoring-overview-activity-logs.md)
- En savoir plus sur les [journaux de diagnostic Azure](monitoring-overview-of-diagnostic-logs.md)
