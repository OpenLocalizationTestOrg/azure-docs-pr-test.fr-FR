---
title: aaaAlert solution de gestion Operations Management Suite (OMS) | Documents Microsoft
description: "solution de gestion des alertes dans le journal Analytique de Hello vous permet d’analyser toutes les alertes hello dans votre environnement.  Dans les alertes de tooconsolidating plus générés au sein d’OMS, il importe les alertes à partir de groupes d’administration System Center Operations Manager connectés dans Analytique de journal."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fe5d534e-0418-4e2f-9073-8025e13271a8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: aff9bd8d88839c5227bb9ec3a1b5209a3cd7cdf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>Solution de gestion des alertes dans Operations Management Suite (OMS)

![Icône de gestion des alertes](media/log-analytics-solution-alert-management/icon.png)

Hello solution de gestion des alertes vous permet d’analyser toutes les alertes hello dans votre référentiel Analytique de journal.  Ces alertes peuvent provenir de diverses sources, y compris celles [créées par Log Analytics](log-analytics-alerts.md) ou [importées à partir de Nagios ou Zabbix](log-analytics-linux-agents.md).  Hello solution également importe les alertes de tous les [connecté des groupes d’administration System Center Operations Manager](log-analytics-om-agents.md).

## <a name="prerequisites"></a>Composants requis
solution de Hello fonctionne avec tous les enregistrements dans le référentiel d’Analytique de journal hello avec un type de **alerte**, de sorte que vous devez effectuer quelle que soit la configuration est requise toocollect ces enregistrements.

- Pour les alertes d’Analytique de journal, [créer des règles d’alerte](log-analytics-alerts.md) enregistrements d’alerte toocreate directement dans le référentiel de hello.
- Pour les alertes de Nagios et Zabbix, [configurer ces serveurs](log-analytics-linux-agents.md) toosend alertes tooLog Analytique.
- Pour les alertes de System Center Operations Manager, [se connecter à votre espace de travail de Operations Manager management groupe tooyour Analytique de journal](log-analytics-om-agents.md).  Toutes les alertes créées dans System Center Operations Manager sont importées dans Log Analytics.  

## <a name="configuration"></a>Configuration
Ajouter tooyour de solution de gestion des alertes hello espace de travail OMS à l’aide du processus de hello décrit dans [ajouter des solutions](log-analytics-add-solutions.md).  Aucune configuration supplémentaire n’est requise.

## <a name="management-packs"></a>Packs d’administration
Si votre groupe d’administration System Center Operations Manager est un espace de travail OMS tooyour connecté, hello suivant des packs d’administration est installé dans System Center Operations Manager lorsque vous ajoutez cette solution.  Il n’existe aucune configuration ou la maintenance hello des packs d’administration requis.  

* Microsoft System Center Advisor Alert Management (Microsoft.IntelligencePacks.AlertManagement)

Pour plus d’informations sur la façon dont les packs d’administration de solution sont mises à jour, consultez [connecter Operations Manager tooLog Analytique](log-analytics-om-agents.md).

## <a name="data-collection"></a>Collecte des données
### <a name="agents"></a>Agents
Hello tableau suivant décrit les sources de hello connecté sont pris en charge par cette solution.

| Source connectée | Support | Description |
|:--- |:--- |:--- |
| [Agents Windows](log-analytics-windows-agents.md) | Non |Les agents Windows directs ne génèrent pas d’alertes.  Des alertes Log Analytics peuvent être créées à partir d’événements et de données de performances collectées à partir des agents Windows. |
| [Agents Linux](log-analytics-linux-agents.md) | Non |Les agents Linux directs ne génèrent pas d’alertes.  Des alertes Log Analytics peuvent être créées à partir d’événements et de données de performances collectées à partir des agents Linux.  Alertes de Nagios et Zabbix sont collectées à partir de ces serveurs qui nécessitent l’agent Linux hello. |
| [Groupe d’administration de Microsoft System Center Operations Manager](log-analytics-om-agents.md) |Oui |Les alertes générées sur les agents d’Operations Manager sont remis toohello groupe d’administration et ensuite transmis tooLog Analytique.<br><br>Une connexion directe à partir d’Operations Manager agents tooLog Analytique n’est pas nécessaire. Données d’alerte sont transférées à partir de référentiel de hello gestion groupe toohello Analytique de journal. |


### <a name="collection-frequency"></a>Fréquence de collecte
- Enregistrements d’alerte sont disponibles toohello solution dès qu’ils sont stockés dans le référentiel de hello.
- Données d’alerte sont envoyées à partir de l’administration d’Operations Manager hello tooLog groupe Analytique toutes les trois minutes.  

## <a name="using-hello-solution"></a>À l’aide de la solution de hello
Lorsque vous ajoutez d’espace de travail hello gestion des alertes solution tooyour OMS, hello **gestion des alertes** vignette est ajoutée tooyour du tableau de bord OMS.  Cette vignette affiche un nombre et une représentation graphique du nombre de hello d’alertes actives qui ont été générées dans hello des dernières 24 heures.  Vous ne pouvez pas modifier cet intervalle de temps.

![Vignette de gestion des alertes](media/log-analytics-solution-alert-management/tile.png)

Cliquez sur hello **gestion des alertes** vignette tooopen hello **gestion des alertes** tableau de bord.  tableau de bord Hello inclut des colonnes de hello Bonjour tableau suivant.  Chaque colonne répertorie hello top 10 alertes en faisant correspondre le nombre que les critères de la colonne pour hello spécifié plage étendue et d’heure.  Vous pouvez exécuter une recherche de journal qui fournit l’intégralité de la liste hello en cliquant sur **afficher tous les** bas hello de colonne de hello ou en cliquant sur en-tête de colonne hello.

| Colonne | Description |
|:--- |:--- |
| Alertes critiques |Toutes les alertes ayant le niveau de gravité Critique, regroupées selon le nom de l’alerte.  Cliquez sur un nom de l’alerte de toorun une recherche de journal retourner tous les enregistrements pour cette alerte. |
| Alertes d'avertissement |Toutes les alertes ayant le niveau de gravité Avertissement, regroupées selon le nom de l’alerte.  Cliquez sur un nom de l’alerte de toorun une recherche de journal retourner tous les enregistrements pour cette alerte. |
| Alertes SCOM actives |Toutes les alertes collectées à partir d’Operations Manager avec n’importe quel état autre que *fermé* groupées par source d’alerte hello généré. |
| Toutes les alertes actives |Toutes les alertes, quel que soit leur niveau de gravité, regroupées selon le nom de l’alerte. Seules les alertes Operations Manager n’ayant pas l’état *Fermé*. |

Si vous faites défiler toohello droite, tableau de bord hello répertorie plusieurs requêtes courantes que vous pouvez cliquer sur tooperform un [recherche de journal](log-analytics-log-searches.md) pour les données d’alerte.

![Tableau de bord de gestion des alertes](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Enregistrements Log Analytics
Hello solution de gestion des alertes analyse tout enregistrement avec un type de **alerte**.  Alertes créées par le journal Analytique ou collectées à partir de Nagios ou Zabbix ne sont pas collectées directement par la solution de hello.

solution de Hello importe les alertes à partir de System Center Operations Manager et crée un enregistrement correspondant pour chaque avec un type de **alerte** et un SourceSystem de **OpsManager**.  Ces enregistrements ont les propriétés de hello Bonjour tableau suivant :  

| Propriété | Description |
|:--- |:--- |
| Type |*Alert* |
| SourceSystem |*OpsManager* |
| AlertContext |Détails de l’élément de données hello hello alerte toobe est généré au format XML à l’origine. |
| AlertDescription |Description détaillée de l’alerte de hello. |
| AlertId |GUID de l’alerte de hello. |
| AlertName |Nom de l’alerte de hello. |
| AlertPriority |Niveau de priorité d’alerte de hello. |
| AlertSeverity |Niveau de gravité d’alerte de hello. |
| AlertState |Dernier état de résolution d’alerte de hello. |
| LastModifiedBy |Nom d’utilisateur hello qui a modifié les alerte hello. |
| ManagementGroupName |Nom du groupe d’administration hello où hello a été généré. |
| RepeatCount |Nombre de fois où hello même alerte a été générée pour hello que même un objet analysé depuis en cours de résolution. |
| ResolvedBy |Nom d’utilisateur hello hello alerte résolue. Vide si l’alerte de hello n’a pas encore été résolu. |
| SourceDisplayName |Nom complet de hello analyse d’un objet qui a généré l’alerte de hello. |
| SourceFullName |Nom complet de l’objet qui a généré l’alerte de hello d’analyse de hello. |
| TicketId |ID de ticket pour l’alerte hello si l’environnement de System Center Operations Manager hello est intégré à un processus d’attribution des tickets pour les alertes.  Vide si aucun ID ticket n’est affecté. |
| TimeGenerated |Date et heure auxquelles hello alerte a été créé. |
| TimeLastModified |Dernière modification date et heure auxquelles l’alerte de hello. |
| TimeRaised |Date et heure auxquelles hello alerte a été générée. |
| TimeResolved |Date et heure auxquelles hello alerte a été résolu. Vide si l’alerte de hello n’a pas encore été résolu. |

## <a name="sample-log-searches"></a>Exemples de recherches dans les journaux
Hello tableau suivant fournit des exemples des recherches de journaux pour les enregistrements d’alerte collectées par cette solution : 

| Interroger | Description |
|:--- |:--- |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR |Alertes critiques déclenchées au cours de hello dernières 24 heures |
| Type=Alert AlertSeverity=warning TimeRaised>NOW-24HOUR |Alertes d’avertissement déclenchées au cours de hello dernières 24 heures |
| Type=Alert SourceSystem=OpsManager AlertState!=Closed TimeRaised>NOW-24HOUR &#124; measure count() as Count by SourceDisplayName |Sources avec les alertes actives déclenchées au cours de hello dernières 24 heures |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR AlertState!=Closed |Alertes critiques déclenchées au cours de hello dernières 24 heures qui sont toujours actifs |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-24HOUR AlertState=Closed |Alertes déclenchées au cours de hello dernières 24 heures qui sont maintenant fermées |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; measure count() as Count by AlertSeverity |Alertes déclenchées au cours de la journée précédente, regroupée par gravité de hello |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; sort RepeatCount desc |Alertes déclenchées au cours de la journée précédente, triée par nombre de répétitions de hello |


>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello précédant les requêtes modifierait toohello suivantes :
>
>| Interroger | Description |
|:---|:---|
| Alerte &#124; où SourceSystem == « OpsManager » et AlertSeverity == « erreur » et TimeRaised > ago(24 h) |Alertes critiques déclenchées au cours de hello dernières 24 heures |
| Alerte &#124; où AlertSeverity == « avertissement » et TimeRaised > ago(24 h) |Alertes d’avertissement déclenchées au cours de hello dernières 24 heures |
| Alerte &#124; où SourceSystem == « OpsManager » et AlertState ! = « Fermé » et TimeRaised > ago(24 h) &#124; résumer Count = count() par SourceDisplayName |Sources avec les alertes actives déclenchées au cours de hello dernières 24 heures |
| Alerte &#124 ; où SourceSystem == « OpsManager » et AlertSeverity == « erreur » et TimeRaised > ago(24 h) et AlertState != « Fermé » |Alertes critiques déclenchées au cours de hello dernières 24 heures qui sont toujours actifs |
| Alerte &#124 ; où SourceSystem == « OpsManager », TimeRaised > ago(24 h) et AlertState != « Fermé » |Alertes déclenchées au cours de hello dernières 24 heures qui sont maintenant fermées |
| Alerte &#124; où SourceSystem == « OpsManager » et TimeRaised > ago(1d) &#124 ; résumer Count = count() par AlertSeverity |Alertes déclenchées au cours de la journée précédente, regroupée par gravité de hello |
| Alerte &#124; où SourceSystem == « OpsManager » et TimeRaised > ago(1d) &#124 ; résumer Count = count() par RepeatCount desc |Alertes déclenchées au cours de la journée précédente, triée par nombre de répétitions de hello |


## <a name="next-steps"></a>Étapes suivantes
* Consultez [Alertes dans Log Analytics](log-analytics-alerts.md) pour obtenir des informations sur la génération d’alertes à partir de Log Analytics.
