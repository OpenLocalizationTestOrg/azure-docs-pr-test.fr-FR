---
title: aaaOverview des alertes dans Microsoft Azure et Azure analyse | Documents Microsoft
description: "Les alertes vous métriques de ressources Azure toomonitor, des événements ou des journaux et être avertis lorsqu’une condition spécifiée est remplie."
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
ms.openlocfilehash: d080080666fedc9eefda6b35cdea3714785d2223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-alerts-in-microsoft-azure"></a>Que sont les alertes dans Microsoft Azure ?
Cet article décrit hello différentes sources d’alertes dans Microsoft Azure, quelles sont hello à des fins de ces alertes, leurs avantages et comment tooget main leur utilisation. Il spécifiquement s’applique tooAzure moniteur, mais fournit des pointeurs tooother services avec des alertes ainsi. Les alertes offrent une méthode d’analyse dans Azure qui vous tooconfigure conditions sur les données et devenir averti lorsque des conditions de hello correspondent hello dernières données d’analyse.

## <a name="taxonomy-of-azure-alerts"></a>Classification des alertes Azure
Suivant de hello Azure utilise des termes du contrat toodescribe alertes et leurs fonctions :
* **Alerte** : définition de critères (une ou plusieurs règles ou conditions) qui est activée lorsque les critères sont remplis.
* **Active** - hello état lorsque hello les critères définis par une alerte est remplie.
* **Résolu** - hello état lorsque hello les critères définis par une alerte n’est plus remplie après avoir déjà remplies.
* **Notification** -hello action réalisée sur une alerte devient active.
* **Action** -un récepteur d’appel spécifique envoyé tooa d’une notification (par exemple, envoi par courrier électronique à une adresse ou validation de l’URL du webhook tooa). Les notifications peuvent généralement déclencher plusieurs actions.

## <a name="alerts-in-different-azure-services"></a>Alertes dans différents services Azure
Les alertes sont disponibles dans plusieurs services de surveillance Azure. Pour plus d’informations sur comment et quand toouse ces services, [, consultez cet article](./monitoring-overview.md). Voici le détail des types d’alerte hello disponible sur Azure :

| Service | Type d’alerte | Services pris en charge | Description |
|---|---|---|---|
| Azure Monitor | [Alertes de métriques](./insights-alerts-portal.md) | [Métriques prises en charge d’Azure Monitor](./monitoring-supported-metrics.md) | Recevoir une notification lorsque toutes les mesures au niveau de la plateforme répond à une condition spécifique (par exemple, % du processeur sur un ordinateur virtuel est supérieur à 90 pour hello 5 dernières minutes). |
| Azure Monitor | [Alertes de journal d’activité](./monitoring-activity-log-alerts.md) | Tous les types de ressources disponibles dans Azure Resource Manager | Recevoir une notification quand un nouvel événement Bonjour [journal des activités Azure](./monitoring-overview-activity-logs.md) correspond aux conditions spécifiques (par exemple, lorsqu’une opération « Supprimer VM » se produit dans myProductionResourceGroup ou lorsqu’un nouvel événement de l’intégrité du Service avec « Actif » en tant que état de Hello s’affiche). |
| Application Insights | [Alertes de métriques](../application-insights/app-insights-alerts.md) | N’importe quelle application instrumentée toosend données tooApplication Insights | Réception d’une notification lorsqu’une métrique d’application répond à une condition définie (par exemple, si le temps de réponse du serveur est supérieur à 2 secondes). |
| Application Insights | [Alertes de test web](../application-insights/app-insights-monitor-web-app-availability.md) | N’importe quel site Web instrumenté toosend données tooApplication Insights | Réception d’une notification lorsque la réactivité ou la disponibilité d’un site web est inférieure aux attentes. |
| Log Analytics | [Alertes Log Analytics](../log-analytics/log-analytics-alerts.md) | N’importe quel service configuré toosend données dans le journal Analytique | Réception d’une notification lorsqu’une requête de recherche Log Analytics concernant des métriques ou des données d’événement répond à certains critères. |

## <a name="alerts-on-azure-monitor-data"></a>Alertes pour des données Azure Monitor
Il existe deux types d’alertes de données dans Azure Monitor : les alertes de métriques et les alertes du journal d’activité.

* **Alertes métriques** -cette alerte se déclenche lorsque la valeur de hello d’une métrique spécifique dépasse un seuil que vous attribuez. alerte de Hello génère une notification lorsque l’alerte de hello est « activé » (quand hello seuil est atteint et la condition d’alerte hello est remplie) ainsi que lorsqu’il est « résolu » (si le seuil de hello est atteint à nouveau et condition de hello n’est plus remplie). Pour obtenir la liste croissante des mesures disponibles prises en charge par Azure Monitor, voir [Liste des mesures prises en charge sur Azure Monitor](monitoring-supported-metrics.md).
* **Alertes du journal d’activité** : alertes du journal de streaming qui sont déclenchées lorsqu’un événement du journal d’activité généré répond aux critères de filtre que vous avez définis. Ces alertes ont uniquement un état « Activé », étant donné que le moteur d’alerte hello applique simplement hello filtre critères tooany un nouvel événement. Ces alertes peuvent être utilisé toobecome notifié lorsqu’un nouvel incident de l’intégrité du Service se produit ou lorsqu’un utilisateur ou une application effectue une opération dans votre abonnement, par exemple, « Supprimer l’ordinateur virtuel. »

Pour les données du journal de Diagnostic disponibles dans l’Analyseur de Azure, nous vous suggérons de données de routage hello dans Analytique de journal et à l’aide d’une alerte d’Analytique de journal. Hello diagramme suivant résume les sources de données dans le moniteur de Windows Azure et, dans son concept, comment vous pouvez avertir que ses données.

![Alertes expliquées](./media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="how-do-i-receive-a-notification-on-an-azure-monitor-alert"></a>Comment faire pour recevoir une notification concernant une alerte Azure Monitor ?
Auparavant, les alertes Azure des différents services utilisaient leurs propres méthodes de notification intégrées. À présent, Azure Monitor propose un regroupement de notifications réutilisable appelé « groupe d’actions ». Groupes d’actions spécifient un ensemble de destinataires d’une notification--n’importe quel nombre d’adresses de messagerie, les numéros de téléphone (pour SMS) ou URL du webhook--et lorsqu’une alerte est activée que références hello groupe d’actions, tous les récepteurs recevoir cette notification. Ainsi, vous tooreuse un regroupement de récepteurs (par exemple, votre sur appel ingénieur liste) sur plusieurs objets d’alerte. Pour le moment, seules les alertes du journal d’activité utilisent les groupes d’actions. Toutefois, il est prévu que d’autres types d’alertes Azure utilisent ces groupes d’actions.

Groupes d’actions prennent en charge la notification en validant l’URL du webhook tooa dans les adresses de tooemail d’addition et de numéros SMS. Vous pouvez ainsi utiliser l’automatisation et la correction avec, par exemple :
    - Runbook Azure Automation
    - Fonction Azure
    - Application logique Azure
    - Un service tiers

Les alertes de métriques n’utilisent pas encore les groupes d’actions. Dans une alerte de métrique, vous pouvez configurer des notifications pour :
* Envoyer des notifications toohello service administrateur, les administrateurs du tooco ou tooadditional adresses de messagerie que vous spécifiez.
* Appels webhook, ce qui vous permet de toolaunch automation supplémentaires.

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
* Hello de révision [webhook alerte schéma des journaux d’activité](monitoring-activity-log-alerts-webhook.md)
* Apprenez-en plus sur les [notifications de service](monitoring-service-notifications.md)
* En savoir plus sur les [groupes d’actions](monitoring-action-groups.md)
