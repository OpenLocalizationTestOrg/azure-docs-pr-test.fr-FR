---
title: aaaMonitor Apps dans Azure App Service | Documents Microsoft
description: "Découvrez comment les applications toomonitor dans Azure App Service à l’aide de hello portail Azure."
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
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a>Surveillance des applications dans Azure App Service
[Service d’applications](http://go.microsoft.com/fwlink/?LinkId=529714) offre des fonctionnalités de surveillance intégrée dans hello [Azure Portal](https://portal.azure.com).
Cela inclut les hello capacité tooreview **quotas** et **métriques** pour une application, ainsi que les hello plan App Service, configuration **alertes** et même **demiseàl’échelle** automatiquement en fonction de ces mesures.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a>Présentation des quotas et des métriques
### <a name="quotas"></a>Quotas
Les applications hébergées dans le Service d’applications sont sujet toocertain *limites* sur les ressources qu’ils peuvent utiliser. Hello limites sont définies par hello **plan App Service** associé application hello.

Si l’application hello est hébergée dans un **libre** ou **Shared** planifier, puis hello des limites sur les ressources hello hello application peut utiliser sont définies par **Quotas**.

Si l’application hello est hébergée dans un **base**, **Standard** ou **Premium** planifier, puis les limites de hello sur ils peuvent utiliser des ressources hello sont définies par hello **taille** (Petite, moyenne, grande) et **le nombre d’instances** (1, 2, 3,...) de hello **plan App Service**.

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

Hello uniquement quota applicable tooapps hébergé sur **base**, **Standard** et **Premium** plans est **système de fichiers**.

Trouverez ici plus d’informations sur les fonctionnalités disponibles pour hello références (SKU) du Service d’application différents, les limites et quotas spécifiques de hello : [limites de Service d’abonnement Azure](../azure-subscription-service-limits.md#app-service-limits)

#### <a name="quota-enforcement"></a>Application de quotas
Si une application dans son utilisation dépasse hello **processeur (en bref)**, **UC (jour)**, ou **la bande passante** quota puis hello application s’arrête jusqu'à ce que le quota de hello définit nouveau. Pendant ce laps de temps, toutes les requêtes entrantes donneront lieu à une erreur **HTTP 403**.
![][http403]

Si hello application **mémoire** quota est dépassé, l’application hello sera redémarrage.

Si hello **Filesystem** quota est dépassé, puis toute écriture échoue, cela inclut l’écriture toologs.

Vous pouvez augmenter ou supprimer les quotas de votre application en procédant à la mise à niveau de votre plan App Service.

### <a name="metrics"></a>Mesures
**Métriques** fournissent des informations sur l’application hello, ou le comportement du plan App Service.

Pour un **Application**, hello les métriques disponibles sont :

* **Temps de réponse moyen**
  * temps moyen de Hello nécessaire pour les demandes de tooserve application hello en ms.
* **Plage de travail moyenne de la mémoire**
  * durée moyenne de Hello de mémoire en MIB utilisé par l’application hello.
* **Temps processeur**
  * quantité de Hello d’UC en secondes consommées par une application hello. Pour plus d’informations sur cette métrique, voir [Temps processeur et pourcentage UC](#cpu-time-vs-cpu-percentage).
* **Données entrantes**
  * Durée Hello consommée par l’application hello dans MIB de la bande passante entrante.
* **Données sortantes**
  * Durée Hello sortants de la bande passante consommée par l’application hello dans MIB.
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
  * Quantité de mémoire actuellement utilisée par l’application hello dans MIB.
* **Demandes**
  * Nombre total de requêtes, quel que soit leur code d’état HTTP résultant.

Pour un **plan App Service**, hello les métriques disponibles sont :

> [!NOTE]
> Les métriques du plan App Service sont uniquement disponibles pour les plans des références (SKU) **De base**, **Standard** et **Premium**.
> 
> 

* **Pourcentage UC**
  * Hello UC moyenne utilisée par toutes les instances du plan de hello.
* **Pourcentage de mémoire**
  * Hello moyenne de la mémoire utilisée par toutes les instances du plan de hello.
* **Données entrantes**
  * Hello entrants la bande passante moyenne utilisée par toutes les instances du plan de hello.
* **Données sortantes**
  * moyenne Hello sortant de la bande passante utilisée par toutes les instances du plan de hello.
* **Longueur de file d'attente de disque**
  * Nombre moyen de Hello de lecture et d’écriture de requêtes qui ont été mises en attente sur le stockage. Une longueur de file d’attente du disque élevée est une indication d’une application qui peut ralentir en raison d’e/s de disque tooexcessive.
* **Longueur de la file d’attente HTTP**
  * Nombre moyen de Hello de requêtes HTTP que toosit sur la file d’attente hello avant la réalisation. Une longueur de file d’attente HTTP élevée ou croissante est le symptôme d’un plan surchargé.

### <a name="cpu-time-vs-cpu-percentage"></a>Temps processeur et pourcentage UC
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

2 métriques reflètent l’utilisation de l’UC : **Temps processeur** et**Pourcentage UC**.

**Temps processeur** est utile pour les applications hébergées dans **libre** ou **Shared** plans, car l’un de leurs quotas est défini en minutes du processeur utilisées par l’application hello.

**Pourcentage de processeur** sur hello autre part est utile pour les applications hébergées dans **base**, **standard** et **premium** plans, car ils la montée en puissance et cette mesure est une bonne indication de hello l’utilisation globale dans toutes les instances.

## <a name="metrics-granularity-and-retention-policy"></a>Granularité des métriques et stratégie de rétention
Métriques pour un plan de service d’application et d’application sont enregistrés et agrégées par service hello avec hello suivant granularités et les stratégies de rétention :

* Les métriques de granularité **Minute** sont conservées **48 heures**
* Les métriques de granularité **Hour** sont conservées **30 jours**
* Les métriques de granularité **Day** sont conservées **90 jours**

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a>Surveillance des Quotas et des mesures hello portail Azure.
Vous pouvez consulter le statut hello Hello différents **quotas** et **métriques** affecter une application Bonjour [Azure Portal](https://portal.azure.com).

![][quotas]
Les **quotas** sont accessibles sous Paramètres &gt; **Quotas**. Hello UX permet à examiner : nom de quotas hello (1), (2) l’intervalle de réinitialisation, (3) limite actuelle et sa (4) actuel valeur.

![][metrics]
**Mesures** sont accessibles directement depuis le panneau des ressources de hello. Vous pouvez également personnaliser le graphique de hello par : (1) **cliquez sur** sur et sélectionnez (2) **modifier le graphique**.
À ce stade, vous pouvez modifier hello (3) **intervalle de temps**, (4) **type de graphique**et (5) **métriques** toodisplay.  

Pour plus d’informations sur les métriques, voir [Surveiller les mesures de qualité du service](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

## <a name="alerts-and-autoscale"></a>Alertes et mise à l’échelle automatique
Métriques pour un plan de l’application ou le Service d’applications peut être rattachée tooalerts, toolearn plus d’informations, consultez [recevoir des notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

Les applications App Service hébergées dans les plans App Service De base, Standard ou Premium prennent en charge la **mise à l’échelle automatique**. Cela vous permet des règles tooconfigure que surveiller les métriques du plan App Service et peuvent augmenter ou diminuer le nombre d’instance hello en fournissant des ressources supplémentaires en fonction des besoins ou enregistrement money lors de l’application hello est excessive. Plus d’informations sur l’échelle automatique ici : [comment tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) et ici [meilleures pratiques pour l’échelle automatique du moniteur de Windows Azure](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
