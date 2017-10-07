---
title: "aaaView des données analytiques Azure Web Apps | Documents Microsoft"
description: "Vous pouvez utiliser insights de toogain solution hello Azure Web Apps Analytique sur vos applications Web Azure en collectant des mesures différentes pour toutes les ressources de votre application Web Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 20ff337f-b1a3-4696-9b5a-d39727a94220
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: banders
ms.openlocfilehash: 7e9725f95c9faf01da89184975ad5444dd19ff95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-analytic-data-for-metrics-across-all-your-azure-web-app-resources"></a>Afficher des données analytiques pour des métriques sur toutes les ressources de votre application Azure Web

![Symbole Web Apps](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)  
Hello les solutions Azure Web Apps Analytique (version préliminaire) fournit des informations sur votre [Azure Web Apps](../app-service-web/app-service-web-overview.md) en collectant des mesures différentes pour toutes les ressources de votre application Web Azure. Avec la solution de hello, vous pouvez analyser et rechercher des données de l’application web ressource métrique.

À l’aide de la solution de hello, vous pouvez afficher le :

- Applications Web supérieur avec un temps de réponse le plus élevé de hello
- Le nombre de requêtes sur vos applications web, dont celles qui ont réussi et échoué
- Les applications web avec le trafic entrant et sortant le plus conséquent
- Les plans de service avec l’utilisation la plus élevée du processeur et de la mémoire
- Les opérations du journal des activités Azure Web Apps

## <a name="connected-sources"></a>Sources connectées

Contrairement à la plupart des autres solutions Log Analytics, les données ne sont pas collectées pour Azure Web Apps des agents. Toutes les données utilisées par la solution de hello proviennent directement d’Azure.

| Source connectée | Pris en charge | Description |
| --- | --- | --- |
| [Agents Windows](log-analytics-windows-agents.md) | Non | solution de Hello ne collecte pas les informations des agents de Windows. |
| [Agents Linux](log-analytics-linux-agents.md) | Non | solution de Hello ne collecte pas les informations des agents de Linux. |
| [Groupe d’administration SCOM](log-analytics-om-agents.md) | Non | solution de Hello ne collecte pas les informations des agents dans un groupe d’administration SCOM connecté. |
| [Compte Azure Storage](log-analytics-azure-storage.md) | Non | solution de Hello ne contient pas les informations de collection à partir du stockage Azure. |

## <a name="prerequisites"></a>Composants requis

- tooaccess informations sur les métriques de ressources d’application Web Azure, vous devez avoir un abonnement Azure.

## <a name="configuration"></a>Configuration

Effectuer hello suivant solution étapes tooconfigure hello Azure Web Apps Analytique vos espaces de travail.

1. Activer la solution Azure Web Apps Analytique hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).
2. [Activer tooOMS de journalisation de métriques de ressource Azure à l’aide de PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

Hello les solutions Azure Web Apps Analytique collecte les deux ensemble de mesures à partir de Azure :

- Métriques Azure Web Apps
  - Plage de travail moyenne de la mémoire
  - Temps de réponse moyen
  - Octets reçus et envoyés
  - Temps processeur
  - Requêtes
  - Plage de travail de la mémoire
  - Httpxxx
- Métriques du plan App Service
  - Octets reçus et envoyés
  - Pourcentage UC
  - Longueur de file d'attente de disque
  - Longueur de la file d’attente HTTP
  - Pourcentage de mémoire

Les mesures du plan App Service sont collectées uniquement si vous utilisez un plan de service dédié. Cela ne s’applique pas toofree ou partagé les plans App Service.

Si vous ajoutez la solution hello à l’aide du portail OMS hello, vous verrez hello suivant vignette. Vous devez trop[activer tooOMS de journalisation de métriques de ressource Azure à l’aide de PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

![Notification d’exécution de l’évaluation](./media/log-analytics-azure-web-apps-analytics/performing-assessment.png)

Après avoir configuré la solution de hello, données doivent démarrer le flux tooyour espace de travail dans les 15 minutes.

## <a name="using-hello-solution"></a>À l’aide de la solution de hello

Lorsque vous ajoutez d’espace de travail hello Azure Web Apps Analytique solution tooyour, hello **Azure Web Apps Analytique** vignette est ajoutée le tableau de bord de présentation tooyour. Cette vignette affiche un nombre de hello Azure Web Apps que hello solution n’a accès tooin votre abonnement Azure.

![Mosaïque Azure Web Apps Analytics](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-tile.png)

### <a name="view-azure-web-apps-analytics-information"></a>Afficher les informations d’Azure Web Apps Analytics

Cliquez sur hello **Azure Web Apps Analytique** vignette tooopen hello **Azure Web Apps Analytique** tableau de bord. tableau de bord Hello inclut les panneaux hello Bonjour tableau suivant. Chaque panneau répertorie les articles tooten mise en correspondance que les critères du panneau pour hello spécifié plage étendue et d’heure. Vous pouvez exécuter une recherche de journal qui retourne tous les enregistrements en cliquant sur **afficher tous les** bas hello du Panneau de hello ou en cliquant sur hello panneau en-tête.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| Colonne | Description |
| --- | --- |
| Azure Webapps |   |
| Tendances de requêtes Web Apps | Affiche un graphique en courbes de hello tendance de demande d’applications Web pour la plage de dates hello que vous avez sélectionné et affiche une liste de demandes de dix web hello supérieur. Cliquez sur hello ligne graphique toorun une recherche de journal pour<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code> <br>Cliquez sur un toorun d’élément de demande web pour hello web demande métrique tendance qui demandent une recherche de journal. |
| Temps de réponse de Web Apps | Affiche un graphique linéaire du temps de réponse des applications Web hello pour la plage de dates hello que vous avez sélectionné. Également affiche une liste d’une liste de hello Web dix premières réponse des applications délai d’attente. Cliquez sur hello graphique toorun une recherche de journal pour<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code><br> Cliquez sur une application Web de toorun une recherche de journal retournant des temps de réponse pour hello Web App. |
| Trafic de Web Apps | Affiche un graphique en courbes pour le trafic Web Apps, en Mo et répertorie le haut hello le trafic des applications Web. Cliquez sur hello graphique toorun une recherche de journal pour<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code><br> Il affiche toutes les applications Web avec le trafic de la dernière minute de hello. Cliquez sur un toorun de l’application Web, une recherche de journal affichant les octets reçus et envoyés pour hello Web App. |
| Plans Azure App Service |   |
| Plans App Service avec utilisation du processeur &gt; 80 % | Affiche hello le nombre total de l’application Service prévoit l’utilisation du processeur supérieure à 80 % et listes hello top 10 des Plans App Service par l’utilisation du processeur. Cliquez sur toorun d’exposition totale hello pour une recherche de journal<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code><br> Cela affiche une liste de vos plans App Service et leur utilisation moyenne du processeur. Cliquez sur un toorun du Plan App Service une recherche de journal indiquant son utilisation UC moyenne. |
| Plans App Service avec utilisation de mémoire &gt; 80 % | Affiche hello le nombre total de l’application Service prévoit l’utilisation de mémoire supérieure à 80 % et listes hello top 10 des Plans App Service par l’utilisation de la mémoire. Cliquez sur toorun d’exposition totale hello pour une recherche de journal<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code><br> Cela affiche une liste de vos plans App Service et leur utilisation moyenne de la mémoire. Cliquez sur un toorun du Plan App Service une recherche de journal qui indique son utilisation moyenne de la mémoire. |
| Journaux d’activité Azure Web Apps |   |
| Audit des activité Azure Web Apps | Affiche hello nombre total d’applications Web avec [journaux d’activité](log-analytics-activity.md) et listes hello opérations du journal des activités 10 premiers. Cliquez sur toorun d’exposition totale hello pour une recherche de journal<code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code><br> Il affiche la liste de hello opérations du journal des activités. Cliquez sur une toorun opération du journal des activités une recherche de journal qui répertorie les enregistrements hello pour l’opération de hello. |



### <a name="azure-web-apps"></a>Azure Web Apps 

Dans le tableau de bord hello, vous pouvez descendre tooget plus de détails sur les métriques de vos applications Web. Ce premier ensemble de lames tendance hello de demandes d’applications Web hello, nombre d’erreurs (par exemple, HTTP404), le trafic et temps de réponse moyen au fil du temps. Il montre également une répartition de ces mesures pour différentes applications web.

![Panneaux Azure Web Apps](./media/log-analytics-azure-web-apps-analytics/web-apps-dash01.png)

Raison principale de vous indiquer que les données sont afin que vous pouvez identifier une application Web avec un temps de réponse élevé et recherchez toofind hello cause. Une limite de seuil est également appliqué toohelp vous que plus facilement identifient hello celles avec des problèmes.

- Les applications web en rouge ont un temps de réponse supérieur à 1 seconde.
- Les applications web en orange ont un temps de réponse supérieur à 0,7 seconde et inférieur à 1 seconde.
- Les applications web en vert ont un temps de réponse inférieur à 0,7 seconde.

Bonjour suivant l’image d’exemple de recherche de journal, vous pouvez voir que hello *anugup3* application web a un temps de réponse beaucoup plus important que hello d’autres applications web.

![Exemple de recherche de journal](./media/log-analytics-azure-web-apps-analytics/web-app-search-example.png)

### <a name="app-service-plans"></a>Plans App Service

Si vous utilisez des plans de service dédiés, vous pouvez également collecter des mesures pour vos plans App Service. Dans cette vue, vous pouvez voir vos plans App Service avec une utilisation élevée du processeur ou de la mémoire (&gt; 80 %). Il montre également hello principaux services d’application avec une utilisation élevée du processeur ou de mémoire. De même, une limite de seuil est appliqué toohelp vous que plus facilement identifient hello celles avec des problèmes.

- Les plans App Service en rouge ont une utilisation du processeur/de la mémoire supérieure à 80 %.
- Les plans App Service en orange ont une utilisation du processeur/de la mémoire supérieure à 60 % et inférieure à 80 %.
- Les plans App Service en vert ont une utilisation du processeur/de la mémoire inférieure à 60 %.

![Panneaux de plan Azure App Service](./media/log-analytics-azure-web-apps-analytics/web-apps-dash02.png)

## <a name="azure-web-apps-log-searches"></a>Recherches dans les journaux Azure Web Apps

Hello **des requêtes de liste de Azure Web Apps demandés** vous montre toutes les hello relatives des journaux d’activité pour les applications Web, qui fournit des informations sur les opérations de hello qui ont été effectuées sur vos ressources d’applications Web. Il répertorie également tous les hello les opérations et nombre hello de fois où ils se sont produites.

À l’aide d’une des requêtes de recherche de journal hello comme point de départ, vous pouvez facilement créer une alerte. Par exemple, vous pourriez toocreate une alerte lorsque le temps de réponse moyen d’une mesure est supérieur à la seconde.

## <a name="next-steps"></a>Étapes suivantes

- Créez une [alerte](log-analytics-alerts-creating.md) pour une mesure spécifique.
- Utilisez [recherche de journal](log-analytics-log-searches.md) tooview détaillée des informations à partir de vos journaux d’activité.
