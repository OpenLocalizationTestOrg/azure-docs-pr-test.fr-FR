---
title: "Vue d’ensemble des alertes dans Microsoft Azure et Azure Monitor | Microsoft Docs"
description: "Les alertes vous permettent d’analyser des mesures de ressources, événements ou journaux Azure, puis d’envoyer des alertes quand une condition spécifiée est remplie."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a6dea224-57bf-43d8-a292-06523037d70b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: robb
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3d30ce72a3be298eba1f4e8f8d33b769971c96cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="what-are-alerts-in-microsoft-azure"></a>Que sont les alertes dans Microsoft Azure ?
Cet article décrit les différentes sources d’alertes dans Microsoft Azure, les objectifs et avantages de ces alertes, ainsi que leur utilisation. Il s’applique plus particulièrement à Azure Monitor, mais fait toutefois référence à certains autres services d’alerte. Dans Azure, les alertes constituent une méthode de surveillance. Elles permettent de définir des conditions à propos de données et d’être informé lorsque les dernières données de surveillance répondent à ces conditions.

## <a name="taxonomy-of-azure-alerts"></a>Classification des alertes Azure
Azure utilise les termes suivants pour décrire les alertes et leurs fonctions :
* **Alerte** : définition de critères (une ou plusieurs règles ou conditions) qui est activée lorsque les critères sont remplis.
* **Actif** : état indiquant que les critères définis sont remplis.
* **Résolu** : état indiquant que les critères définis ne sont plus remplis après l’avoir été.
* **Notification** : action entreprise lorsqu’une alerte devient active.
* **Action** : appel émis vers le destinataire d’une notification (par exemple, en envoyant un e-mail ou en publiant une URL Webhook). Les notifications peuvent généralement déclencher plusieurs actions.

## <a name="alerts-in-different-azure-services"></a>Alertes dans différents services Azure
Les alertes sont disponibles dans plusieurs services de surveillance Azure. Pour plus d’informations sur l’utilisation de ces services, [consultez cet article](./monitoring-overview.md). Voici le détail des types d’alertes disponibles dans Azure :

| Service | Type d’alerte | Services pris en charge | Description |
|---|---|---|---|
| Azure Monitor | [Alertes de métriques](./insights-alerts-portal.md) | [Métriques prises en charge d’Azure Monitor](./monitoring-supported-metrics.md) | Réception d’une notification lorsqu’une métrique de plateforme répond à une condition définie (par exemple, si le pourcentage d’UC d’une machine virtuelle est supérieur à 90 depuis cinq minutes). |
| Azure Monitor | [Alertes de journal d’activité](./monitoring-activity-log-alerts.md) | Tous les types de ressources disponibles dans Azure Resource Manager | Réception d’une notification quand un nouvel événement du [Journal d’activité Azure](./monitoring-overview-activity-logs.md) répond aux conditions définies (par exemple, si une opération « Supprimer la machine virtuelle » se produit dans myProductionResourceGroup ou si un nouvel événement État du service actif s’affiche). |
| Application Insights | [Alertes de métriques](../application-insights/app-insights-alerts.md) | Toute application instrumentée pour envoyer des données à Application Insights | Réception d’une notification lorsqu’une métrique d’application répond à une condition définie (par exemple, si le temps de réponse du serveur est supérieur à 2 secondes). |
| Application Insights | [Alertes de test web](../application-insights/app-insights-monitor-web-app-availability.md) | Tout site web instrumenté pour envoyer des données à Application Insights | Réception d’une notification lorsque la réactivité ou la disponibilité d’un site web est inférieure aux attentes. |
| Log Analytics | [Alertes Log Analytics](../log-analytics/log-analytics-alerts.md) | Tout service configuré pour envoyer des données vers Log Analytics | Réception d’une notification lorsqu’une requête de recherche Log Analytics concernant des métriques ou des données d’événement répond à certains critères. |

## <a name="alerts-on-azure-monitor-data"></a>Alertes pour des données Azure Monitor
Il existe deux types d’alertes de données dans Azure Monitor : les alertes de métriques et les alertes du journal d’activité.

* **Alertes de métrique** : ces alertes se déclenchent quand la valeur d’une métrique spécifiée dépasse le seuil défini. Ces alertes génèrent une notification lorsqu’elles sont activées (quand le seuil est atteint et que la condition d’alerte est remplie) et lorsqu’elles sont résolues (quand le seuil est de nouveau atteint et que la condition n’est plus remplie). Pour obtenir la liste croissante des mesures disponibles prises en charge par Azure Monitor, voir [Liste des mesures prises en charge sur Azure Monitor](monitoring-supported-metrics.md).
* **Alertes du journal d’activité** : alertes du journal de streaming qui sont déclenchées lorsqu’un événement du journal d’activité généré répond aux critères de filtre que vous avez définis. Ces alertes ne peuvent être qu’à l’état actif, puisque le moteur d’alerte ne fait qu’appliquer les critères de filtre aux nouveaux événements. Ces alertes peuvent être utilisées pour être informé lorsqu’un nouvel incident d’état du service se produit ou lorsqu’un utilisateur ou une application effectue une opération dans votre abonnement (par exemple, « Supprimer la machine virtuelle »).

Pour les données du journal de diagnostic disponible dans Azure Monitor, nous vous suggérons de router les données dans Log Analytics et d’utiliser une alerte Log Analytics. Le diagramme suivant récapitule les sources de données d’Azure Monitor, et explique comment créer des alertes à partir de ces données.

![Alertes expliquées](./media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="how-do-i-receive-a-notification-on-an-azure-monitor-alert"></a>Comment faire pour recevoir une notification concernant une alerte Azure Monitor ?
Auparavant, les alertes Azure des différents services utilisaient leurs propres méthodes de notification intégrées. À présent, Azure Monitor propose un regroupement de notifications réutilisable appelé « groupe d’actions ». Les groupes d’actions spécifient un ensemble de destinataires pour une notification (autant d’adresses e-mail, de numéros de téléphone (pour SMS) ou d’URL Webhook que souhaité), et dès qu’une alerte faisant référence au groupe d’actions est activée, tous les destinataires reçoivent la notification. Vous pouvez ainsi réutiliser un groupe de destinataires (par exemple, votre liste d’ingénieurs techniques) pour plusieurs objets d’alerte. Pour le moment, seules les alertes du journal d’activité utilisent les groupes d’actions. Toutefois, il est prévu que d’autres types d’alertes Azure utilisent ces groupes d’actions.

Les groupes d’actions prennent en charge les notifications par publication d’URL Webhook, en plus des notifications par adresse e-mail et numéro de téléphone. Vous pouvez ainsi utiliser l’automatisation et la correction avec, par exemple :
    - Runbook Azure Automation
    - Fonction Azure
    - Application logique Azure
    - Un service tiers

Les alertes de métriques n’utilisent pas encore les groupes d’actions. Dans une alerte de métrique, vous pouvez configurer des notifications pour :
* envoyer des notifications par courrier électronique à l’administrateur de service, aux coadministrateurs ou aux adresses e-mail supplémentaires que vous spécifiez ;
* appeler un webhook, qui permet de lancer des actions d’automatisation supplémentaires.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez obtenir des informations sur les règles d’alerte et leur configuration avec :

* En savoir plus sur les [métriques](monitoring-overview-metrics.md)
* Configurer les [alertes métriques par le biais du portail Azure](insights-alerts-portal.md)
* Configurer les [alertes métriques dans PowerShell](insights-alerts-powershell.md)
* Configurer l’[interface de ligne de commande des alertes métriques](insights-alerts-command-line-interface.md)
* Configurer les [alertes métriques au moyen de l’API REST Azure Monitor](https://msdn.microsoft.com/library/azure/dn931945.aspx)
* En savoir plus sur les [journaux d’activité](monitoring-overview-activity-logs.md)
* Configurer les [alertes de journal d’activité par le biais du portail Azure](monitoring-activity-log-alerts.md)
* Configurer les [alertes de journal d’activité au moyen de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Consulter le [schéma de webhook d’alerte de journal d’activité](monitoring-activity-log-alerts-webhook.md)
* Apprenez-en plus sur les [notifications de service](monitoring-service-notifications.md)
* En savoir plus sur les [groupes d’actions](monitoring-action-groups.md)
