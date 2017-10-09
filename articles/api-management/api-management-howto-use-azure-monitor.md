---
title: "aaaMonitor gestion des API avec l’Analyseur de Azure | Documents Microsoft"
description: "Découvrez comment toomonitor Azure API Management de service à l’aide du moniteur de Windows Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a>Gestion des API avec Azure Monitor
Azure Monitor est un nouveau service Azure qui fournit une source unique d’analyse pour toutes vos ressources Azure. Dans le Gestionnaire d’Azure, vous pouvez visualiser, interroger, Router, archiver et prendre des mesures sur les métriques hello et journaux provenant des ressources Azure telles que la gestion de l’API. 

Hello suivant vidéo montre comment toomonitor gestion des API à l’aide du moniteur de Windows Azure. Pour en savoir plus sur Azure Monitor, consultez [Prise en main d’Azure Monitor]. 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a>Mesures
Gestion des API émet actuellement cinq métriques et nous prévoyons de tooadd plus Bonjour futures. Ces mesures sont émis à chaque minute, pratiquement visibilité en temps réel dans l’état de hello et l’intégrité de votre API. Voici un résumé des métriques de hello :
* Nombre total de demandes de passerelle : nombre hello de l’API des demandes de période de hello. 
* Demandes réussies de passerelle : hello différentes demandes d’API qui a reçu des codes de réponse HTTP réussies, y compris 304, 307 et rien de plus petite que 301 (par exemple, 200). 
* Passerelle de demandes ayant échoué : le nombre de hello de demandes de l’API qui a reçu des codes de réponse HTTP erronés, y compris 400 et toute valeur supérieure à 500.
* Demandes non autorisées de passerelle : nombre de hello de demandes d’API qui a reçu des codes de réponse HTTP, y compris 401 et 403 429. 
* Autres demandes de passerelle : nombre de hello des demandes de l’API qui a reçu des codes de réponse HTTP qui n’appartiennent pas tooany Hello précédant les catégories (par exemple, 418).

Vous pouvez accéder aux mesures dans votre service de gestion des API, ou accéder aux mesures de toutes vos ressources Azure dans Azure Monitor. métriques de tooview dans votre service de gestion des API :
1. Ouvrez hello portail Azure.
2. Atteindre le service de gestion des API tooyour.
3. Cliquez sur **Mesures**.

![Panneau Mesures][metrics-blade]

Pour plus d’informations sur la façon toouse métriques, consultez [vue d’ensemble de mesures].

## <a name="activity-logs"></a>Journaux d’activité
Journaux d’activité donnent une idée des opérations hello qui ont été effectuées sur les services de gestion des API. Ils étaient auparavant nommés « Journaux d’audit » ou « Journaux des opérations ». À l’aide des journaux d’activité, vous pouvez déterminer hello », qui et à quel moment » pour toutes les opérations (PUT, POST, DELETE) effectuées sur votre service de gestion des API d’écriture. 

> [!NOTE]
> Journaux d’activité n’incluent pas les opérations de lecture (GET) ou les opérations effectuées dans hello portail classique de serveur de publication ou à l’aide de hello des API de gestion d’origine.

Vous pouvez accéder aux journaux d’activité dans votre service de Gestion des API, ou accéder aux journaux de toutes vos ressources Azure dans Azure Monitor. tooview activité enregistre dans votre service de gestion des API :
1. Ouvrez hello portail Azure.
2. Atteindre le service de gestion des API tooyour.
3. Cliquez sur **Journal d’activité**.

![Panneau Journaux d’activité][activity-logs-blade]

Pour plus d’informations sur la façon toouse métriques, consultez [vue d’ensemble des journaux d’activité].

## <a name="alerts"></a>Alertes
Vous pouvez configurer des alertes tooreceive basés sur les journaux d’activité et de métriques. Moniteur de Azure vous permet de tooconfigure un hello toodo alerte suivant lorsqu’il déclenche :

* Envoyer un e-mail de notification
* Appeler un webhook
* Appeler une application logique Azure

Vous pouvez configurer des règles d’alerte dans votre service de Gestion des API, ou dans Azure Monitor. tooconfigure dans Gestion des API : 
1. Ouvrez hello portail Azure.
2. Atteindre le service de gestion des API tooyour.
3. Cliquez sur **Règles d'alerte**.

![Panneau Règles d’alerte][alert-rules-blade]

Pour plus d’informations sur l’utilisation des alertes, consultez [Présentation des alertes].

## <a name="diagnostic-logs"></a>Journaux de diagnostic
Les journaux de diagnostic offrent des informations détaillées sur les opérations et erreurs qui sont importantes pour l’audit ainsi qu’à des fins de dépannage. Les journaux de diagnostic diffèrent des journaux d’activité. Journaux d’activité fournissent des informations sur les opérations de hello qui ont été effectuées sur vos ressources Azure. Les journaux de diagnostic fournissent des informations sur les opérations effectuées par votre ressource.

Gestion des API fournit actuellement des tests de diagnostic des journaux (traités par lot toutes les heures) API individuel demander à chaque entrée ayant hello suivant structure :

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

Vous pouvez accéder aux journaux de diagnostic dans votre service de Gestion des API, ou accéder aux journaux de toutes vos ressources Azure dans Azure Monitor. tooview des journaux de diagnostic dans votre service de gestion des API :
1. Ouvrez hello portail Azure.
2. Atteindre le service de gestion des API tooyour.
3. Cliquez sur **Journal de diagnostic**.

![Panneau Journaux de diagnostic][diagnostic-logs-blade]

Pour plus d’informations sur la façon toouse métriques, consultez [vue d’ensemble des journaux de Diagnostic].

## <a name="next-step"></a>Étape suivante

* [Prise en main d’Azure Monitor]
* [vue d’ensemble de mesures]
* [vue d’ensemble des journaux d’activité]
* [vue d’ensemble des journaux de Diagnostic]
* [Présentation des alertes]

[Prise en main d’Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md
[vue d’ensemble de mesures]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[vue d’ensemble des journaux d’activité]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[vue d’ensemble des journaux de Diagnostic]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[Présentation des alertes]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
