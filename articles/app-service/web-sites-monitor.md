---
title: Analyser les application dans Azure App Service | Microsoft Docs
description: "Découvrez comment surveiller les applications dans Azure App Service à l’aide du Portail Azure."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 25d3776920d683fffedcd8ac6ed0e84dfe875974
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a>Surveillance des applications dans Azure App Service
[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) fournit des fonctionnalités de surveillance intégrées dans le [Portail Azure](https://portal.azure.com).
Ces fonctionnalités comprennent notamment la possibilité d’examiner les **quotas** et les **métriques** d’une application et du plan App Service, la configuration **d’alertes**, et même une **mise à l’échelle** automatique en fonction de ces métriques.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a>Présentation des quotas et des métriques
### <a name="quotas"></a>Quotas
Les applications hébergées dans App Service sont soumises à certaines *limites* concernant les ressources qu’elles peuvent utiliser. Ces limites sont définies par le **plan App Service** associé à l’application.

Si l’application est hébergée dans un plan **Gratuit** ou **Partagé**, les limites relatives aux ressources utilisables par l’application sont définies sous la forme de **quotas**.

Si l’application est hébergée dans un plan **De base**, **Standard** ou **Premium**, les limites applicables aux ressources que l’application peut utiliser sont définies par la **taille** (Petite, Moyenne, Grande) et par le **nombre d’instances** (1, 2, 3, ...) du **plan App Service**.

Les **quotas** des applications **gratuites** ou **partagées** sont les suivants :

* **CPU(short)**
  * Quantité d’UC autorisée pour cette application dans un intervalle de cinq minutes. Ce quota se réinitialise toutes les cinq minutes.
* **CPU(Day)**
  * Quantité totale d’UC autorisée pour cette application sur une journée. Ce quota se réinitialise toutes les 24 heures à minuit en temps universel coordonné.
* **Mémoire**
  * Quantité totale de mémoire autorisée pour cette application.
* **Bande passante**
  * Quantité totale de bande passante sortante autorisée pour cette application sur une journée.
    Ce quota se réinitialise toutes les 24 heures à minuit en temps universel coordonné.
* **Système de fichiers**
  * Quantité totale de stockage autorisée.

Le seul quota applicable aux applications hébergées sur les plans **De base**, **Standard** et **Premium** est **Système de fichiers**.

Pour plus d’informations sur les quotas, limites et fonctionnalités spécifiques disponibles pour les différentes références (SKU) App Service, consultez [Limites du service d’abonnement Azure](../azure-subscription-service-limits.md#app-service-limits)

#### <a name="quota-enforcement"></a>Application de quotas
Si l’utilisation d’une application dépasse le quota **CPU (short)** (Temps processeur (jour)), **CPU (Day)** (Temps processeur (jour)) ou **Bande passante**, l’application sera arrêtée jusqu’à la réinitialisation du quota. Pendant ce laps de temps, toutes les requêtes entrantes donneront lieu à une erreur **HTTP 403**.
![][http403]

Si le quota **Mémoire** d’une application est dépassé, l’application sera redémarrée.

En cas de dépassement du quota **Système de fichiers** , toute opération d’écriture échouera, y compris l’écriture dans les journaux.

Vous pouvez augmenter ou supprimer les quotas de votre application en procédant à la mise à niveau de votre plan App Service.

### <a name="metrics"></a>Mesures
**Mesures** fournissent des informations sur le comportement de l’application ou du plan App Service.

Pour une **application**, les métriques disponibles sont les suivantes :

* **Temps de réponse moyen**
  * Temps moyen, en millisecondes, nécessaire à l’application pour traiter les requêtes.
* **Plage de travail moyenne de la mémoire**
  * Quantité moyenne de mémoire, en MiB, utilisée par l’application.
* **Temps processeur**
  * Quantité d’UC, en secondes, consommée par l’application. Pour plus d’informations sur cette métrique, voir [Temps processeur et pourcentage UC](#cpu-time-vs-cpu-percentage).
* **Données entrantes**
  * Quantité de bande passante entrante, en MiB, consommée par l’application.
* **Données sortantes**
  * Quantité de bande passante sortante, en MiB, consommée par l’application.
* **Http 2xx**
  * Nombre de requêtes donnant lieu à un code d’état HTTP >= 200, mais < 300.
* **Http 3xx**
  * Nombre de requêtes donnant lieu à un code d’état HTTP >= 300, mais < 400.
* **Http 401**
  * Nombre de requêtes donnant lieu à un code d’état HTTP 401.
* **Http 403**
  * Nombre de requêtes donnant lieu à un code d’état HTTP 403.
* **Http 404**
  * Nombre de requêtes donnant lieu à un code d’état HTTP 404.
* **Http 406**
  * Nombre de requêtes donnant lieu à un code d’état HTTP 406.
* **Http 4xx**
  * Nombre de requêtes donnant lieu à un code d’état HTTP >= 400, mais < 500.
* **Erreurs de serveur http**
  * Nombre de requêtes donnant lieu à un code d’état HTTP >= 500, mais < 600.
* **Plage de travail de la mémoire**
  * Quantité de mémoire actuelle, en MiB, utilisée par l’application.
* **Demandes**
  * Nombre total de requêtes, quel que soit leur code d’état HTTP résultant.

Pour un **plan App Service**, les métriques disponibles sont les suivantes :

> [!NOTE]
> Les métriques du plan App Service sont uniquement disponibles pour les plans des références (SKU) **De base**, **Standard** et **Premium**.
> 
> 

* **Pourcentage UC**
  * Utilisation moyenne de l’UC dans toutes les instances du plan.
* **Pourcentage de mémoire**
  * Utilisation moyenne de la mémoire dans toutes les instances du plan.
* **Données entrantes**
  * Utilisation moyenne de la bande passante entrante dans toutes les instances du plan.
* **Données sortantes**
  * Utilisation moyenne de la bande passante sortante dans toutes les instances du plan.
* **Longueur de file d'attente de disque**
  * Nombre moyen de requêtes de lecture et d’écriture mises en file d’attente sur le stockage. Une longueur de file d’attente de disque élevée est une indication d’une application susceptible d’être ralentie en raison d’un nombre d’E/S de disque excessif.
* **Longueur de la file d’attente HTTP**
  * Nombre moyen de requêtes HTTP qui devaient se trouver dans la file d’attente avant d’être exécutées. Une longueur de file d’attente HTTP élevée ou croissante est le symptôme d’un plan surchargé.

### <a name="cpu-time-vs-cpu-percentage"></a>Temps processeur et pourcentage UC
<!-- To do: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

2 métriques reflètent l’utilisation de l’UC : **Temps processeur** et**Pourcentage UC**.

La métrique **Temps processeur** est utile pour les applications hébergées dans un plan **Gratuit** ou**Partagé**, car l’un des quotas de ces applications est défini en minutes d’UC utilisées par l’application.

D’un autre côté, la métrique **Pourcentage UC** est utile pour les applications hébergées dans les plans **De base**, **Standard** et **Premium**, car le nombre d’instances de ces applications peut être augmenté, et cette métrique est une bonne indication de l’utilisation globale dans toutes les instances.

## <a name="metrics-granularity-and-retention-policy"></a>Granularité des métriques et stratégie de rétention
Les métriques d’une application et d’un plan App Service sont journalisées et agrégées par le service avec les granularités et les stratégies de rétention suivantes :

* Les métriques de granularité **Minute** sont conservées **48 heures**
* Les métriques de granularité **Hour** sont conservées **30 jours**
* Les métriques de granularité **Day** sont conservées **90 jours**

## <a name="monitoring-quotas-and-metrics-in-the-azure-portal"></a>Surveillance des quotas et des métriques dans le Portail Azure
Vous pouvez examiner l’état des différents **quotas** et **métriques** en affectant une application dans le [Portail Azure](https://portal.azure.com).

![][quotas]
Les **quotas** sont accessibles sous Paramètres &gt; **Quotas**. L’expérience utilisateur vous permet de consulter : (1) le nom du quota, (2) son intervalle de réinitialisation, (3) sa limite actuelle et (4) sa valeur actuelle.

![][metrics]
Les **mesures** sont directement accessibles à partir du panneau de ressources. Vous pouvez également personnaliser le graphique en : (1) **cliquant** sur ce dernier, puis en sélectionnant (2) **Modifier le graphique**.
À ce stade, vous pouvez modifier (3) **l’intervalle de temps**, (4) le **type de graphique** et (5) les **métriques** à afficher.  

Pour plus d’informations sur les métriques, voir [Surveiller les mesures de qualité du service](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

## <a name="alerts-and-autoscale"></a>Alertes et mise à l’échelle automatique
Les métriques d’une application ou d’un plan App Service peuvent être raccordées aux alertes. Pour plus d’informations, voir [Réception de notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

Les applications App Service hébergées dans les plans App Service De base, Standard ou Premium prennent en charge la **mise à l’échelle automatique**. Cette fonctionnalité vous permet de configurer des règles qui surveillent les métriques du plan App Service et qui peuvent augmenter ou diminuer le nombre d’instances en fournissant les ressources supplémentaires requises ou en allégeant les coûts lorsque l’application est surapprovisionnée. Pour plus d’informations sur la mise à l’échelle automatique, voir [Mise à l’échelle](../monitoring-and-diagnostics/insights-how-to-scale.md) et [Meilleures pratiques pour la mise à l’échelle automatique d’Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-best-practices.md).

> [!NOTE]
> Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="whats-changed"></a>Changements apportés
* Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
